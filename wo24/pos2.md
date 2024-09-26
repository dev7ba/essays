1) ¿Cómo se llega al consenso en Bitcoin?
  - La prueba de trabajo es una cantidad de energía física real gastada, que es infalsificable, fácilmente comprobable y acumulable.
  - Cada página (o bloque) conteniendo transacciones tiene una prueba de trabajo y una firma con una función criptográfica hash que evita que se modifiquen páginas anteriores del libro de cuentas sin tener que rehacer la prueba de trabajo de nuevo de todas las páginas desde el presente a ese pasado.
  - Las "paginas modernas dependen de las antiguas" mediente una función de un solo sentido.
  - Los nodos de Bitcoin tienen como protocolo elegir la cadena de trabajo mas larga. 
  - Esto provoca un coste de oportutidad en los mineros a la hora de votar por una nueva página de ese libro:
        - Si mino en el pasado tengo que superar al resto.
        - Minar en el presente no me supone ningún esfuerzo.
   - ... que hace que se mine sobre las páginas ya minadas en vez de otras en el pasado.
1.1) ¿Cómo se llega al consenso en POS?
  - Los mineros votan según una cantidad de dinero (stake) que tienes en la cadena. 
  - Aparte de que es un sistema plutocrático en vez de meritocrático, tiene graves repercusiones en la descentralización: 
  - Se llega al consenso dependiendo una buena comunicación entre nodos y si estos presentan historiales diferentes se necesita de una entidad centralizada para decir cuál es el historial correcto.
    - Pueden presentar historiales diferentes porque sin prueba de trabajo no cuesta "nada" modificar una base de datos.
    - Para defender o intentar hacer viable el PoS se caen en argumentos circulares tipo "si nos engañas te penalizamos"->Me da lo mismo que me penalices en tu cadena yo ofrezco otra.
    - y/o argumentos en los que la asencia de prueba es la prueba de ausencia.-> Internet no me falla nunca por lo que nunca me fallará.
    - PoS no te protege de que te cambien el pasado, te proteje en una ventana de tiempo en una red concreta a la que tienes que estar bien conectado.
    - Los nodos nuevos deben confiar en los viejos.
1.2) Ataque del 51%.
    - En PoW no se pueden quitar los bitcoin, Los mineros no pueden sobreescribir el pasado. Sólamente pueden seleccionar las transacciones que meten. (Pueden hacer censura)
    - El PoS no está garantizado el pasado de forma descentralizada. y pueden hacer también censura. 
    - En Bitcoin se excluye del minado el capital que no se puede convertir en ASICS.
    - En PoS se excluye del minado el capital que no puede convertirse en unidad monetaria. Si ya tienen el 51% olvídate.
    - En PoW tienes la dinámica de incrementar las fees para vencer y subvencionar los ASICS no censores.
1.3) Los Pools de minería:
    - Sirven para reducir la varianza en el beneficio por minar los bloques de Bitcoin 10 minutos.
    En Bitcoin:
    - No custodian ASICS, no son mineros, son un servicio informático bastante simple con un algoritmo muy simple. Pueden estar en cualquier jurisdicción.
    - Algunos protocolos permiten al minero elegir el contenido del bloque a minar.
    - Los mineros pueden cambiar de Pool de mineria en 1 segundo.
    En PoS:
    - Tienes que tener monedas online con el consiguiente problema. Esto es una fuerza centralizadora porque el usuario medio no entiende de seguridad.
    - Degenera en pools de mineria o contratos inteligentes donde depositas tu dinero. 
        - Delegas la elección de transacciones y validador en una entidad centralizada (Lido)
        - Permiso para salir porque reinvierten en deudas y préstamos.
        - Degenera aún mas con la introdución del MEV donde el algoritmo de minado es una pieza de ingeniería de software complicada, que en el fondo hace un poco PoW. que hay que mantener
1.4) Frente a una partición de red o Sybil attack con entidad central comprometida:
    - Los nodos PoS pueden ofrecer cada uno una alternativa de Historial. No puedes saber cuál es cual.
    - Los nodos PoW con que un nodo sea honesto puede descartar al resto. Además, presentar varios historiales es inviable económicamente.

2) Ejemplos de fallos en PoS.
  - Todos derivan de una falacia de argumento circular: pensar que se puede poner reglas en una BD dentro de esa misma BD. 
  - "Nothing at Stake". No cuesta nada modificar una BD. Puedes tener varios historiales paralelos partiendo del mismo inicio haciendo grinding (barato).
  - Votar una versión en particular no tiene costo de oportunidad. Los mineros pueden minar en todas las cadenas posibles.
    - Solucionarlo con penalizaciones a que se "equivocaron" en un bloque dado o votaron en dos versiones de ella en el corto plazo,
    (mientras tienes tu nodo arrancado) y no te partan la red.
  - "Long range attacks" Cada versión de la cadena de bloques que existe o que es posible que exista puede ser revivida y ejecutarse sin problema.
    - Se pueden juntar los mineros con menos stake y rehacer la cadena para tener ellos más en el historial final. 
    - ¿Cómo un nodo recién arrancado o desconectado un tiempo sabe cuál es cual?.
    - Confían en el medio de comunicación, y que "internet" y la red P2P no tienen particiones.
  - Lo solucionan con "Subjetividad Débil". Una entidad centralizada que te dice cuál es la verdad.
    - Una solución sociopolítica a un problema técnico.
  - Presentar un historial falso a través de cualquier medio tiene coste 0 una vez se ha hecho una vez.
  - El PoS no se acumula retroactivamente, PoW si. Proof of Stake se debería llamar proof of temporal stake. 
  - PoS no puede proteger el pasado. El staking solamente tiene sentido en el pequeño periodo de tiempo que ocurre.
  - Old private keys attack. Se pueden vender claves privadas

3) Preminado y origen Ethereum.
  - Los precios eran fijos pero las cantidades no. 
  - Manipulación de precio.
  - Primer año los mineros un 26% del preminado.
  - 1 bitcoin 2000 ethers.
  - Preston Byrne: el flujo de Bitcoin a EthSuisse fué exactamente exponencial, como si fuera un Bot.

4) Futuro incierto Ethereum.
  - Promesa de "el código es ley".
  - DAO.
  - Pasar del 5 eth por bloque a 4 porque hay inflacción. Perjudica a los tenedores.
  - Intentan pasar a POS. Sin fecha fija y la consiguiente inseguridad regulatoria. ¿Cuánto invierto?
  - Pasar de 4 al 3 ethers por bloque.
  - Los mineros de GPU los dejaron en la miseria con el difficulty bomb y cambios a POS. La fecha de paso a POS es incierta para los mineros.
  - Tardan 6 años (de 2016 a 2022) debido a la enorme complejidad.
  - Te pagan por ser rico.
  - Si hay inflacción: una proporcion de las fees se destruye. (los ether del initial coin offering no)
  - Ahora llaman a que quemen el dinero que gastan en fees "ultrasound money". Perjudica al usuario y beneficia al tenedor. EIP1559.
  - Después de que las SEC obligara a los tenedores de Ether centralizados a censurar las transacciones de tornado cash Ethereum se parece a un banco con una API de contratos inteligentes. Ha caído en captura regulatoria.
  - Validadores piden 32 ethereum liquidez. ¿Quien va a poner esto online? 
  - Cuanto mas dinero tiene un validador o Lido. Mas capital tiene para invertir en MEV y ganar aún mas.
  - Una cola de un año para entrar como validador.
  - Los validadores serían presionados por el caso de Tornado Cash? Tienen proceso KYC los validadores?
  - PoS se ataca con doble gasto a partir del 67% de staking centralizado. 68% lo tienen 11 proveedores de servicios.
  - Lido tiene el 31.6% del staking y no es descentralizado. Alex & Ryan berkmans. Lido no votó por capar su tamaño. Además es un sitema con permiso con un puñado de operadores del nodo  - Nodos de ETH 2.0 no guarda el historial. Pierdes toda la confianza. Porque los nuevos nodos deben confiar en los existentes. Que pasa si los nodos existentes son capturados.

5) En PoW:
  - Bitcoin es la única BD en donde el activo es el apunto contable en la BD. No es un IOU. debido a la prueba de trabajo.
  - La complejidad de PoS frente a PoW es mucho mayor. 
  - La complejidad es la enemiga de la seguridad.

Hay literatura sobre algoritmos pBFT (practical Bizantine fault tolerant algorithm) pero no es aplicable al marco teórico de Bitcoin de descentralización, entrada si permiso, Resistencia ataque de Sybil (creación de credenciales de acceso sin límite), resistencia a la censura... etc porque:
        - No resisten ataques de Sybil (credenciales son gratis en un entorno descentralizado).
        - Estan pensados para entornos federados en donde el número de nodos es fijo.
        - No escalan bien por el número de mensajes que se tienen que mandar entre ellos es cuadrático frente a lineal como en redes P2P como Bitcoin.
        - Suelen requerir de condiciones de sincronía muy estrictas. 
        - No se soporta la entrada y salida de nodos sin confianza.
        - En ese entorno federado las condiciones de convergencia se dan si sólamente si menos de 1/3 de los nodos fallan.
        - El mas avanzado es el Honey Badger of pBFT.


