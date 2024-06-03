# Todo sobre la mempool. Por dev7ba.

## ¿Que és la mempool?

La mempool es una de las tres bases de datos principales que tiene un nodo de Bitcoin junto con el conjunto de salidas de transaciones no gastadas (UTXO set) y los bloques minados. En su interior se almacena una caché, esto es, una BD temporal de transaciones que están a la espera de ser minadas. A pesar de parecer algo simple, esta base de datos está interrelacionada con varias funcionalidades que ofrece el protocolo: la retransmision de transaciones por parte de la red P2P, el incremento de tasas (fees) para que se mine con mas prioridad una transacción, y el correcto funcionamiento de protocolos de segunda capa como Lighting Network entre otras. 

Debido a que el código de la mempool no es parte del consenso del protocolo, el entusiasta de Bitcoin no suele estar informado de la historia de sus cambios, pasados y futuros, ni de su funcionamiento actual. Este documento pretende poner fin a ello de la manera mas exahustiva posible a fecha de hoy.

## ¿Para qué tenemos una mempool?

### La retransmision de transacciones

Aunque parezca mentira, sin una mempool no podemos retransmitir transacciones. Un nodo de bitcoin debe mantener el uso de memoria, procesador y red en unos niveles razonables para consegir ser nuestra fortaleza monetaria soberana. Si no tenemos una memoria de las transacciones que ya hemos retransmitido a nuestos pares, es trivial hacer un ataque de denegacion de servicio a nuestro nodo, ya que no puede discernir si una transacion ya la hemos retransmitido o no. Por ello, un nodo de Bitcoin, sólamente retransmite una transacion a sus pares, si la transacion recibida no estaba en la mempool. Esto es un ejemplo de regla de las muchas que veremos mas adelante. [^1] 

#### ¿Pero para qué queremos retransmitir transaciones?

¿No sería mucho mas sencillo mandar las transaciones a los mineros y ya está? Evidentemente no, porque la red de bitcoin cuida del anonimato tanto de los usuarios como de los mineros. Es decir, no hace suposiciones sobre quien es quien dentro de la red ni establece barreras de entrada a la misma. Supongamos que los mineros se anuncian con su dirección ip. ¿Quien sería el responsable del directorio de dichas direcciones ip?. Esto atenta contra la descentralización de la red. Además, si enviamos las transaciones directamente a los mineros se podría censurarles y obligarles a vigilar quien hace qué, atentando contra el anonimato y la libertad de la red. Una red P2P evita esto enviando las transmisiones "al conjunto de la red" sin dato ninguno.

### Reducción del tiempo de retransmisión de bloques

Los nodos que tienen mempool validan las transaciones según son recibidas antes de almacenarlas en esta. Esto reduce el tiempo de validación (y por lo tanto de retransmisión) de los bloques recién minados ya que normalmente (salvo nodos recién arrancados), tendremos ya validadas la mayoría de las transacciones que forma parte de los bloques. Además, con la introducción del [envío de bloques compactos](https://bitcoinops.org/en/topics/compact-block-relay/) los nodos ya sólamente envían la cabecera del bloque minado junto con un conjunto de ids cortos para cada transacion, reconstruyendo la mayor parte del bloque (si no todo) desde los datos de la mempool. De hecho, segun [estadísticas](https://www.dsn.kastel.kit.edu/bitcoin/#nodes) el tiempo medio de propagación de los bloques es menor que el de las transaciones. (~1 segundo frente a ~6 seg). Esto es lo esperable, ya que las transaciones de asentamiento de UTXOs suelen tener muchas entradas, y por lo tanto muchas operaciones de firma. Además, las transaciones pueden ser, de media, mas grandes que el envío de un bloque compacto.

### Estimación de tasas por transación.

El nodo de bitcoin core, por defecto, puede mostrar una [estimación](https://mempoolexplorer.com/feeEstimation) de las tasas que debes pagar en función del tamaño de una transación para que ésta sea minada dentro de un tiempo dado. Esta estimación se basa en un [algoritmo](https://gist.github.com/morcos/d3637f015bc4e607e1fd10d8351e9f41) que conceptualmente es muy sencillo: simplemente se observa el historial de transacciones de la mempool y devuelve la tasa de pago menor de forma que un ratio grande de transaciones con esta tasa haya sido confirmada en el tiempo por el que se le pregunta al algoritmo. Éste algoritmo suele ser muy rígido, y no recoge correctamente los cambios bruscos en el tamaño o histograma de tasas de la mempool. Sin embargo es un algoritmo que no puede ser engañado por los mineros (para subir la estimación de las tasas artificialmente), por que no usa ningún dato de los bloques minados, salvo si una transacción ha sido minada o no y cuando. 

Hay que tener el cuenta que la precisión en el cálculo de las estimaciones nunca puede ser buena, ya que dependen de dos procesos estocásticos: el tiempo de minado de un bloque, y la cantidad y tamaño de transaciones que llegan a la red P2P en cada momento.

## Apéndice

### Parámentros de configuración de la mempool:

- `-blocksonly`: Reduce la mempool a 5MB y deshabilita la retransmisión de transaciones a los pares.
- `-maxmempool`=<n>: Donde <n> es el tamaño máximo que puede alcanzar nuestra mempool en MB, por defecto es 300. Las transaciones que no quepan en la mempool con tasa (fee) mas baja son desalojadas.

### RPC relacionados con la mempool:
- `estimatesmartfee`: Devuelve una estimación de las fees a pagar en satoshis/VByte.


[^1]: Podemos tener un nodo con una [mempool mínima](https://github.com/bitcoin/bitcoin/blob/master/doc/reduce-memory.md) (5MB), y sin retransmision de transaciones (pero si de bloques) con la opción `-blocksonly`.
