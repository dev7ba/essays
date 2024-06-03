# Todo sobre la mempool. Por dev7ba

## ¿Que és la mempool?

La mempool es una de las tres bases de datos principales que tiene un nodo de Bitcoin junto con el conjunto de salidas de transaciones no gastadas (UTXO set) y los bloques minados. En su interior se almacena una caché, esto es, una BD temporal de transaciones que están a la espera de ser minadas. A pesar de parecer algo simple, esta base de datos está interrelacionada con varias funcionalidades que ofrece el protocolo: la retransmision de transaciones por parte de la red P2P, el incremento de tasas (fees) para que se mine con mas prioridad una transacción, y el correcto funcionamiento de protocolos de segunda capa como Lighting Network entre otras. 

Debido a que el código de la mempool no es parte del consenso del protocolo, el entusiasta de Bitcoin no suele estar informado de la historia de sus cambios, pasados y futuros, ni de su funcionamiento actual. Este documento pretende poner fin a ello de la manera mas exahustiva posible a fecha de hoy.

## ¿Para qué tenemos una mempool?

### La retransmision de transacciones

Aunque parezca mentira, sin una mempool no podemos retransmitir transacciones. Un nodo de bitcoin debe mantener el uso de memoria, procesador y red en unos niveles razonables para consegir ser nuestra fortaleza monetaria soberana. Si no tenemos una memoria de las transacciones que ya hemos retransmitido a nuestos pares, es trivial hacer un ataque de denegacion de servicio a nuestro nodo, ya que no puede discernir si una transacion ya la hemos retransmitido o no. Por ello, un nodo de Bitcoin, sólamente retransmite una transacion a sus pares, si la transacion recibida no estaba en la mempool. Esto es un ejemplo de regla de las muchas que veremos mas adelante. Podemos tener un nodo con una mempool mínima (5MB), y sin retransmision de transaciones (pero si de bloques) con la opción `-blocksonly`.

## Apéndice

### Parámentros de configuración de la mempool:

- `-blocksonly`: Reduce la mempool a 5MB y deshabilita la retransmisión de transaciones a los pares.



