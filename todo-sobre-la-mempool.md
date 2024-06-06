# Todo sobre la mempool. Por dev7ba.

## ¿Que és la mempool?

La mempool es una de las tres bases de datos principales que tiene un nodo de Bitcoin, junto con el conjunto de salidas de transaciones no gastadas (UTXO set) y los bloques minados. En su interior se almacena una caché, esto es, una BD temporal de transacciones que están a la espera de ser minadas. A pesar de parecer algo simple, esta base de datos está interrelacionada con varias funcionalidades que ofrece el protocolo: la retransmision de transaciones por parte de la red P2P, el incremento de tasas (o fees) para que se mine con mas prioridad una transacción, y el correcto funcionamiento de protocolos de segunda capa como Lighting Network entre otras. 

Debido a que el código de la mempool no es parte del consenso del protocolo -que es inconfigurable-, sino de la política -configurable por el usuario-, el entusiasta de Bitcoin no suele estar informado de la historia de sus cambios, pasados y futuros, ni de su funcionamiento actual, ya que no se debate en público tanto como modificaciones del consenso que son mas visibles ya que nos atañen a todos por igual y a la vez. Este documento pretende poner fin a ello de la manera mas exahustiva posible a fecha de hoy.

## ¿Para qué tenemos una mempool?

### Para la retransmision de transacciones

Aunque parezca mentira, sin una mempool no podemos retransmitir transacciones. Un nodo de Bitcoin debe mantener el uso de memoria, procesador y red en unos niveles razonables para consegir ser nuestra "fortaleza monetaria soberana". Si no tenemos una memoria de las transacciones que ya hemos retransmitido a nuestos pares, es trivial hacer un ataque de denegacion de servicio a nuestro nodo, ya que no puede discernir si una transacción ya la hemos retransmitido o no, inundando la red de transacciones redundantes. Por ello, un nodo de Bitcoin, sólamente retransmite una transación a sus pares, si la transación recibida es válida (standard) y no estaba anteriormente en la mempool (la incluye en ella a continuación). Esto es un ejemplo de regla de las muchas que veremos mas adelante[^1]. 

Pero hay que tener en cuenta que debido a la naturaleza de estas reglas (algunas configurables), no existe una entidad única de mempool, sino que cada nodo tiene su "vista", o conjunto de transaciones, en funcion de su configuración, versión y nodos a los que se conecte (y a la vez, la configuración, version... etc. de cada uno de ellos, recursivamente). Esto puede provocar que algunas transaciones, especialmente las de pocas fees, no lleguen a los mineros en ciertas ocasiones límite, lo que puede provocar frustración. Veremos también algunos ejemplos mas adelante. 

#### ¿Pero para qué queremos retransmitir transaciones?

¿No sería mucho mas sencillo mandar las transaciones a los mineros y ya está? Evidentemente no, porque la red de bitcoin cuida del anonimato tanto de los usuarios como de los mineros. Es decir, no hace suposiciones sobre quien es quien dentro de la red ni establece barreras de entrada a la misma. Supongamos que los mineros se anuncian con su dirección ip. ¿Quien sería el responsable del directorio de dichas direcciones ip?. Esto atenta contra la descentralización de la red. Además, si enviamos las transaciones directamente a los mineros se podría censurarles y obligarles a vigilar quien hace qué, atentando contra el anonimato y la libertad de la red. Una red P2P evita esto enviando las transmisiones "al conjunto de la red" sin dato adicional alguno salvo el de la propia transacción.

### Para la reducción del tiempo de retransmisión de bloques

Evidentamente los nodos de Bitcoin validan los bloques minados recibidos antes de retransmitirlos a la red, y (evidentente) también validan las transaciones según van siendo recibidas antes de almacenarlas en la mempool. Esta validación contínua de transacciones reduce el tiempo de validación (y por lo tanto de retransmisión) de los bloques nuevos, ya que normalmente (salvo nodos recién arrancados), tendremos ya validadas la mayoría de las transacciones que forman parte de los bloques minados. Además, con la introducción del [envío de bloques compactos](https://bitcoinops.org/en/topics/compact-block-relay/) los nodos ya sólamente envían la cabecera del bloque minado junto con un conjunto de ids cortos para cada transaccion, reconstruyendo la mayor parte del bloque (si no todo) desde los datos de la mempool. De hecho, segun [estadísticas](https://www.dsn.kastel.kit.edu/bitcoin/#nodes) el tiempo medio de propagación de los bloques es menor que el de las transaciones. (~1 segundo frente a ~6 seg). Esto es lo esperable, ya que las transaciones de asentamiento de UTXOs suelen tener muchas entradas, y por lo tanto muchas operaciones de firma, desplazando la media de tiempo de validación. Además, las transaciones suelen ser, de media, mas grandes que el envío de un bloque compacto.

### Para la estimación de tasas por transación

El nodo de bitcoin core, por defecto, puede mostrar una [estimación](https://mempoolexplorer.com/feeEstimation) de las tasas que debes pagar en función del tamaño de una transación para que ésta sea minada dentro de un tiempo dado. Esta estimación se basa en un [algoritmo](https://gist.github.com/morcos/d3637f015bc4e607e1fd10d8351e9f41) que conceptualmente es muy sencillo: simplemente se observa el historial de transacciones de la mempool y devuelve la tasa de pago menor de forma que un ratio grande de transaciones con esta tasa haya sido confirmada en el tiempo por el que se le pregunta al algoritmo. Las críticas a éste algoritmo suelen ser por su rigidez, ya que no recoge correctamente los cambios bruscos en el tamaño o histograma de tasas de la mempool. Sin embargo, su principal bondad, es que es un algoritmo que no puede ser engañado por los mineros para subir la estimación de las tasas artificialmente, debido a que no usa ningún dato de estas tasas de los bloques minados. Sólamente necesita saber cuando una transacción ha sido minada con respecto a cuando fué introducida en la mempool.

Hay que tener el cuenta que la precisión en el cálculo de las estimaciones nunca puede ser buena, ya que dependen de dos procesos estocásticos: el tiempo de minado de un bloque, y la cantidad y tamaño de transaciones que llegan a la red P2P en cada momento.

### Para ofrecer el mejor bloque posible a los mineros

Para tener descentralización en la red de Bitcoin, es necesario que un nodo pueda ser ejecutado por el mayor número posible de personas, y para eso es necesario que el tamaño de bloque tenga un tamaño fijo y "pequeño", así se pone un límite a la velocidad de crecimiento de la base de datos de UTXOs, indispensable para la validación de las nuevas transaciones. Debido a este límite en el tamaño de bloques, los mineros tienen el incentivo de incluir en el siguiente bloque a minar las transacciones que les dan mas beneficio. Este problema de optimización combinatoria se llama el [problema de la mochila](https://es.wikipedia.org/wiki/Problema_de_la_mochila) o (knapsack problem) y no puede ser resuelto en un [tiempo polinómico](https://es.wikipedia.org/wiki/NP-completo), Sin embargo dado que las transacciones tienen por lo general un tamaño mucho mas pequeño que el del bloque, este problema se puede aproximar muy fácilmente al supuesto óptimo ordenando las transaciones de mayor a menor según el ratio satoshis/VByte y rellenando en este orden el bloque a minar.

Este algortimo se complica aún mas debido a la relación de dependencia que tienen algunas transaciones de la mempool, ya sea por el uso de CPFP (Child Pays for parent), esto es, un "hijo" con una alta tasa paga la inclusión de un transaccion "padre" con una tasa mas baja, o bien por el uso de una cartera de bitcoin en la que tienes menos UTXOs que pagos simultáneos quieres realizar, (y por tanto tienes que usar las salidas de transaciones que todavía no han sido minadas). Este algoritmo junto con el de reemplazo de transaciones por tasas mas altas ([Replace By fee](https://bitcoinops.org/en/topics/replace-by-fee/)) lo veremos mas adelante[^3]. 

## La mempool no es parte del consenso de Bitcoin, pero es mas restrictivo que éste

Minar un bloque tiene un coste computacional muy alto, de incluso varias decenas de miles de euros, sin embargo crear una transación y mandarla a la red no implica un gran coste computacional. Es esperable que se pongan unas restricciones de seguridad mas grandes al tipo de transaciones que se envian a la red que a las que se minan en un bloque: si alguien quiere hacer un ataque, es mucho mas barato hacerlo vía spam de algún tipo de transacciones que via spam de bloques. La diferencia entre consenso (reglas que tienen que cumplir las transaciones en un bloque) y la política (reglas que tienen que cumplir una transacción en la mempool) se encuentran definidas en los ficheros de [consenso](https://github.com/bitcoin/bitcoin/blob/master/src/consensus/consensus.h) y [política](https://github.com/bitcoin/bitcoin/blob/master/src/policy/policy.h) correspondientes. Vamos a dar unos cuantos ejemplos representativos de posibles ataques y su solución imponiendo límites que no se encuentran en el consenso de bloque:

- Se puede crear una transacción con el [máximo coste posible de validación](https://bitcointalk.org/?topic=140078) y con el [tamaño máximo](https://mempool.space/tx/bb41a757f405890fb0f5856228e23b715702d714d59bf2b1feb70d8b2b4e3e08) en la que la última firma que se valida sea inválida. Imagina mandar cientos de estas transacciones que obligan a gastar varios [segundos](https://rusty.ozlabs.org/2015/07/08/the-megatransaction-why-does-it-take-25-seconds.html) a una CPU corriente para validarla y luego resultar que no son correctas ninguna. Por ello hay un máximo de firmas por transacción (dependiendo de su tipo) y un tamaño de transación máxima en la mempool (que no en un bloque minado).

- Otro ejemplo de ataque es el de sustitución. Debido a que las transaciones pueden depender entre sí, se pueden formar "arboles invertidos" de transaciones, en donde muchísimas transacciones pueden depender de la salida de una sola transación todavía sin confirmar. Podríamos llenar la mempool de transaciones que dependen de ésta, "gastar" los recusos de ancho de banda de todos los nodos de la red para difundir estas transaciones, y una vez hecho, cambiar la transación padre por una que paga mas fees que la anterior pero a otra salida, y obligar a desalojar una gran cantidad de transaciones ya enviadas a la red, si se repite esto constantemente podemos saturar el ancho de banda de muchos nodos. Por ello hay una profundidad máxima y tamaño máximo de transaciones dependientes en la política del protocolo (25 hijas y 101KvBytes respectivamente). Además, las políticas de reemplazo exigen que se deba pagar adicionalmentes mas tasas que la suma de las tasas de las transaciones hijas. Sin embargo, en el consenso de bloque sólo se pide que las transaciones estén en orden de gasto, es decir que un padre aparezca en el bloque antes que un hijo.

- Un ataque muy conocido es el de dust limit. En él se envían transaciones con muy poca cantidad que saturan la base de datos de utxos con muy poco capital. Por ello se establece una cantidad mínima en una salida de transación para poder reenviarla. Así se limita la propagación a los mineros de este tipo de transaciones.

- Tamaño de op_return: Para evitar la introducción de datos que no corresponden a transaciones, el tamaño máximo de datos que puede ir detrás de una instrucción op_return es de 80Bytes. Aunque esta restricción esta obsoleta debido a la introducción de ordinals usando taproot. 

Todas los problemas expuestos en estos ejemplos son resueltos en la política de la mempool (y reenvío de transaciones), no en el consenso del bloque, por lo tanto es posible que un minero cree un bloque obviando los límites impuestos. Si violar estos límites se considera spam o no lo dejamos a interpretación del lector, sin embargo no se considera un problema para el protocolo Bitcoin en cuanto a su seguridad de red.

### Una mempool mas restrictiva ayuda a evitar problemas de consenso en el despliegue de softforks.

En las reglas de consenso, en lo concerniente al formato de las transacciones que se pueden encontrar en un bloque minado, una transacción es **válida por defecto**. Es decir, se considera correcta salvo que incumpla con alguna de las reglas actuales del protocolo. Esto sirve para dejar espacio a la posibilidad de modificaciones futuras mediante bifurcación suave o softfork.

Un softfork es un cambio en el consenso de Bitcoin de forma que a partir de un punto en el tiempo, las reglas del consenso se vuelven mas rígidas, es decir, si una bifurcación trata sobre la introducción de un nuevo tipo de transacción, el conjunto de todas las transaciones válidas posibles se reduce con respecto al consenso anterior que introducía la regla del "valido por defecto" explicada anteriormente. 

Por el contrario, y por completitud, comentaremos que una bifurcación dura o hardfork **relaja** las reglas del consenso. Por ejemplo, permitir bloques de tamaño mas grande es un hardfork, ya que el conjunto de bloques posibles aumenta con respecto al consenso anterior.

Una bifurcación suave permite la compatibilidad hacia atrás en el protocolo de Bitcoin, es decir, permite que no se tengan que actualizar los nodos antiguos si no quieren, simplemente, éstos no validarán los nuevos tipos de transacción debido a la regla de "válido por defecto". Esto es un comportamiento necesario para hacer de Bitcoin un protocolo "sin permiso", ya que no obliga a actualizarte. Sin embargo, en la política de la mempool las transacciones son **inválidas por defecto** al menos que se sigan las reglas actuales. Veámos por qué:

Durante el despliege de Taproot (un softfork) los mineros señalaron que sus nodos ya se habían actualizado, sin embargo algunos no lo hicieron en realidad. Si Taproot se activa y alguien manda una transación (de Taproot) inválida, y si en los nodos no actualizados, **por defecto** se aceptaran éstas transacciones (inválidas) como válidas en la mempool, éstas se incluirían en su bloque a minar, provocando una bifurcación de la red entre mineros que rechazan estas transaciones inválidas y los que no lo hacen. 

Sin embargo, si, como debe de ser, los nodos no actualizados, no incluyen por defecto en su mempool a transaciones que no siguen las reglas de consenso estrictamente, éstas transacciones inválidas no entran la mempool, y por lo tanto no son minadas, evitando una bifurcación de la red. 

Después de la activación del softfork de Taproot, los pools de minería F2Pool y AntPool no minaron ninguna transación de este tipo durante muchos bloques. Lo que indica que, pese a señalar la activación, no estaban actualizados[^2].

## Consistencia en la política de los nodos.



## Apéndice

### Parámentros de configuración de la mempool:

- `-blocksonly`: Reduce la mempool a 5MB y deshabilita la retransmisión de transaciones a los pares.
- `-maxmempool`:<n>: Donde <n> es el tamaño máximo que puede alcanzar nuestra mempool en MB, por defecto es 300. Las transaciones que no quepan en la mempool con tasa (fee) mas baja son desalojadas.

### RPC relacionados con la mempool:
- `estimatesmartfee`: Devuelve una estimación de las fees a pagar en satoshis/VByte.


[^1]: Podemos tener un nodo con una [mempool mínima](https://github.com/bitcoin/bitcoin/blob/master/doc/reduce-memory.md) (5MB), y sin retransmision de transaciones (pero si de bloques) con la opción `-blocksonly`.
[^2]: [MIT Bitcoin Expo 2022](https://www.youtube.com/watch?v=s_I_Nj5GMgk) a partir de minuto 12:30, Gloria Zhao, investigación de 0xB10C.
[^3]: Además hay que tener en cuenta el máximo número de firmas posibles dentro de un bloque (maxSigops).
