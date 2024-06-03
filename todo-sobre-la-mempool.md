# Todo sobre la mempool. Por dev7ba

## ¿Que és la mempool?

La mempool es una de las tres bases de datos principales que tiene un nodo de Bitcoin junto con el conjunto de salidas de transaciones no gastadas (UTXO set) y los bloques minados. En su interior se almacena una caché, esto es, una BD temporal, de transaciones que están a la espera de ser minadas. A pesar de parecer algo simple, esta base de datos está interrelacionada con varias funcionalidades que ofrece el protocolo: la retransmision de transaciones por parte de la red P2P, el incremento de tasas (fees) para que se mine con mas prioridad una transacción, y el correcto funcionamiento de protocolos de segunda capa como Lighting Network entre otras. 

Debido a que el código de la mempool no es parte del consenso del protocolo, el entusiasta de Bitcoin no suele estar informado de la historia de sus cambios, pasados y futuros, ni de su funcionamiento actual. Este documento pretende poner fin a ello.




