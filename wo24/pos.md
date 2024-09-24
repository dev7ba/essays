1) Como se llega a consenso en PoS
  En PoS el que tiene mas unidades monetarias es el que ordena o mina las transacciones. 
  Es una plutocracia que tiene control de un oligopolio sobre:
    - La selección de transacciones (censura, con permiso)
    - Somete a inflacción a los que menos tienen (literal porque el protocolo para su funcionamiento correcto necesita una cantidad mínima de staking para poder escalar).
    - Su beneficio solo puede crecer, no tiene incentivo ninguno para gastar.
    - A esto se le añade el problema de la distribución inicial de capital.
    - Te pagan por ser rico.
  - Ethereum excluye del minado al capital que no puede adquirir unidades monetarias. Un censor con la mayoría del stake no se puede derrocar.
2) Ejemplos de fallos en PoS.
  - Todos derivan de una falacia de argumento circular: pensar que se puede poner reglas en una BD dentro de esa misma BD. 
  - "Nothing at Stake". No cuesta nada modificar una BD. Puedes tener varios historiales paralelos partiendo del mismo inicio haciendo grinding (barato).
  - Votar una versión en particular no tiene costo de oportunidad. Los mineros pueden minar en todas las cadenas posibles.
    - Solucionarlo con penalizaciones a que se "equivocaron" en un bloque dado o votaron en dos versiones de ella en el corto plazo,
    (mientras tienes tu nodo arrancado) y no te partan la red.
    - No se puede comprobar si alguien está haciendo esto (grinding)?
  - "Long range attacks" Cada versión de la cadena de bloques que existe o que es posible que exista puede ser revivida y ejecutarse sin problema.
    - Se pueden juntar los mineros con menos stake y rehacer la cadena para tener ellos más en el historial final. 
    - ¿Cómo un nodo recién arrancado o desconectado un tiempo sabe cuál es cual?.
    - Confían en el medio de comunicación, y que "internet" y la red P2P no tienen particiones.
  - Lo solucionan "Subjetividad Débil". Una entidad centralizada que te dice cuál es la verdad, ¿Y si esa entidad centralizada es la que hace Grinding?.
    - Una solución sociopolítica a un problema técnico.
  - Presentar un historial falso a través de cualquier medio tiene coste 0 una vez se ha hecho una vez.
  - El PoS no se acumula retroactivamente, PoW si. Proof of Stake se debería llamar proof of temporal stake. 
  - PoS no puede proteger el pasado. El staking solamente tiene sentido en el pequeño periodo de tiempo que ocurre.
  - Old private keys attack. Se pueden vender claves privadas
  - Ausencia de prueba no es prueba de ausencia.
3) Preminado y origen.
  - Los precios eran fijos pero las cantidades no. 
  - Manipulación de precio.
  - Primer año los mineros un 26% del preminado.
  - 1 bitcoin 2000 ethers.
  - Preston Byrne: el flujo de Bitcoin a EthSuisse fué exactamente exponencial, como si fuera un Bot.
4) Futuro incierto.
  - Promesa de "el código es ley".
  - DAO.
  - Pasar del 5 eth por bloque a 4 porque hay inflacción. Perjudica a los tenedores.
  - Intentan pasar a POS
  - Pasar de 4 al 3 ethers por bloque.
  - Los mineros de GPU los dejaron en la miseria con el difficulty bomb y cambios a POS. La fecha de paso a POS es incierta para los mineros.
  - Te pagan por ser rico.
  - Si hay inflacción: una proporcion de las fees se destruye. (los ether del initial coin offering no)
  - Ahora llaman a que quemen el dinero que gastan en fees "ultrasound money".


5) Comparación con PoW

En PoW:
1) Es una meritocracia y un censor puede ser derrotado haciendo mas trabajo que él.
  - Necesitas un ancla exterior como la PoW, un "coste irrefutable" que establezca un coste de oportunidad.
  - La resistencia a la censura en PoW se basa en pagar más fees (tasas) a los mineros.
  - Bitcoin es la única BD en donde el activo es el apunto contable en la BD. No es un IOU. debido a la prueba de trabajo.
