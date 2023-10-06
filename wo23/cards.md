Discutir soluciones propuestas para hacer que la minería de Bitcoin sea más sostenible, como el uso de energía renovable.
-------------------------------------------------------------------------------------------------------------------------

- Discurso pobrista donde se reduce la demanda en vez de ampliar la oferta. Basado en culpabilizar al usuario de un bien o servicio que está disfrutando.
- El problema principal es que la mayoría de las personas no le otorgan valor a bitcoin ¿para que consumir tanto para nada?

- Diversos estudios con muy mala metodología, variaciones de 300%
- Estimado de Bitcoin mining council (que no se puede saber bien, variaciones del 300%) de consumo global de Bitcoin es de 348 TWh. 
- Videojuegos 214/75(25 centrales nucleares) Twh. Luces navideñas (solo US) 201 TWh. 650 TWh por el sistema bancario.
- No me voy a meter en ese lodazal, Voy a explicar la metodología que se suele usar y en que podemos estar seguros con respecto a ella.
- Las estimaciones se basan en pasar de ExaHashes a Teravatios/hora (mirando los equipos) y luego viendo la ip de los pools que la filtran ver el mix energético del pais en cuestión e interpolar.
- 50-60% es energia renovable. 
- Según BMC 0.17% de la energía global y 0.11% de las emisiones del CO2. 
- BMC miente sobre que la eficiencia de minado mejora, si mejora, pero para dar mas seguridad a la red de Bicoin, no a disminuir la cantidad de CO2.
- La minería de Bitcoin puede funcionar donde la oferta no llega a la demanda y/o donde se necesite generar calor.
		- Picos en energía renovable. (Tejas).
		- Antiguas industrias cierran y dejan una sobreproducción. Alcoa en Tejas con BitDeer.
		- Gas de plataformas petrolíferas o minipozos. Texas y Dakota del Norte.
		- Cultivar tulipanes en Holanda.
- Bitcoin no usa renovables, las renovables usan bitcoin para ser mas rentables. También esto ocurre con energía no renovable. 
- Bitcoin está donde hay desperdicio de energía, renovable o no. Pero la renovable desperdicia mas al ser poco almacenable.

Analizar cómo la minería de Bitcoin ha evolucionado hacia una mayor centralización debido a la concentración de poder en grandes operaciones de minería.
--------------------------------------------------------------------------------------------------------------------------------------------------------

Esta relacionado con:

Explorar la evolución de la minería de Bitcoin desde las CPU hasta las ASIC (Circuitos Integrados de Aplicación Específica) y cómo esto ha afectado la accesibilidad a la minería.
----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

- Primero CPUs. (un CPU) un voto.
- Despues GPUs. Aprovechar el paralelismo de las tarjetas Gráficas. Laszlo Hanyecz, el de las 2 pizzas por 10,000 Bitcoin. 2010
- Despues vinieron las FPGAs (Field Programmable Gate Arrays). 2011
- Finalmente las ASIC (Aplication specific integrated circuit) Avalon, Bitmain con su Asic Boost (20% de ahorro energético y que querían patentar) Destapado por Gregory Maxwell
	- y que dio problemas para desplegar Segwit y que acabó con la BlockSize wars y su final con el USAF.
- A día de hoy el minado se concentra donde se desperdicia energía. Usando Hardware especifico para ello. Da a lugar a posibles tensiones en función de la Geopolítica de los paises:
	- Donde se crean estos chips?
	- Donde hay energía mas barata?
- Irónicamente la minería de ASICs mejora la seguridad de Bitcoin frente a los ordenadores de propósito general.

Explorar otras formas de validación de transacciones, como la Proof of Stake (PoS), y cómo se comparan con la minería de Prueba de Trabajo (PoW).
-------------------------------------------------------------------------------------------------------------------------------------------------

Problemas del Proof of Stake:

- Económicos: Proof of stake es una plutocracia mientras que proof of work es una meritocracia. Los que mas tienen somenten a un impuesto inflacionario a los que menos tienen.
		- También tienen un impuesto inflacionario los que no ponen nada en juego, por pocos conocimientos técnicos o por no terner el mínimo requerido en los protocolos PoS.
		- En realidad el Staking no te beneficia, te obligan al stake o a someterse a un impuesto inflacionario.
		- Los beneficios del stake están sometidos a impuesto, un rendimiento del 10% de la red con un 35% de impuestos le da la mitad al estado en 22 años. 
- Filosóficos: No hay nada en juego "Nothing at stake". Añadir una columna en una BD no cuesta nada, Es un argumento circular pensar que puedes poner reglas desde dentro de esa misma BD. 
		- En cierta medida es intentar ofuscar el problema, no resolverlo.
		- Votar una versión particular de la blockchain no tiene costo. Los mineros racionales deberían minar en cada rama que compita que vean para maximizar beneficios. 
		- Se intenta solucionar poniendo penalizaciones, ventanas de tiempo...
- Técnicos: No puedes reconstruir una cadena de bloques con proof of stake desde 0 sin confiar en alguien (Autoridades certificadoras). 
		- Esto da lugar a ataques de largo recorrido y a una subjetividad débil.
- Políticos: La descentralización cuesta, por que es como la libertad o la guerra. 
		- Proof of Stake es una solucion sociopolítica para un problema técnico. 
		- Proof of stake es un poder imaginario o abstracto frente al poder físico real como dice Jameson Lowery.

Discutir cómo la competencia en la minería de Bitcoin puede llevar a la innovación y a la optimización del hardware.
--------------------------------------------------------------------------------------------------------------------

- Cualquier aumento de demanda de un bien en un principio aumenta la innovación y optimización a la hora de crear ese bien.
- Restricciones comerciales de EEUU a Huawei.
- La fundicion (foundry) de Huawei (SIMC) ha hecho chips de minado (MinerVa) diseñados por Hisilicon para probar su proceso de fabricación de chips.
		- Antes los hacian de 5nm con el proceso de ASML pero ya no debido a las SANCIONES COMERCIALES impuestas por Estados Unidos. ASML están sacando chips de 3nm.
		- Asianometry, Huawei Mate 60 pro, Chip Kirin 9000s de 7 nanómetros de SMIC (China) 

- Sería mejor un algoritmo que fuera ASIC resistant -> GPU mining, o HD minning. Mejor RandomX de Monero. 
- Se trata de reducir la diferencia entre minar con un equipo potente pero que vale para mas cosas que para minar -> Se incentiva mas el I+D en equipos de propósito general 
	- (Nvidia se ha beneficiado de esto). Aunque sometas al mercado a shocks de demanda.
	- Aunque tambien con los ASICs se fomenta mejorar la litografía. 
		- SIMC ha hecho chips de minado minerVa para probar su proceso n+2 dado que un chip de minado tiene muchas estructuras repetidas y es un buen caso de uso para mejorar el nodo.

Discutir las actualizaciones y cambios previstos en el protocolo de Bitcoin que pueden afectar a los mineros.
-------------------------------------------------------------------------------------------------------------

- En principio el minado debe ser independiente de las mejoras del protocolo, aunque no siempre ha sido así con el AsicBoost de Bitmain (patentado).
- Cuando las Drive chains (Bip 300-301), cadenas laterales, Ordinals o cualquier otra manera de representar un activo en la cadena de bloques de Bitcoin se conjugue con un mercado descentralizado,
- Habrá oportunidades de hacer arbitraje MEV Miner Extractable value en Bitcoin.
	- Front/Back running: Si ves a alguien que va a hacer una compra grande, es de esperar que el precio suba. Si compras antes que éste, ganas dinero.
	- Sandwiching.
- Degrada la capacidad de un nodo de Bitcoin de estimar las fees adecuadas.
- La mineria puede ser mas o menos rentable en función del MEV, y esto puede llegar a ser una fuerza centralizadora en el protocolo.

Discutir cómo podría evolucionar la minería de Bitcoin en el futuro, especialmente a medida que las recompensas por bloque disminuyen.
--------------------------------------------------------------------------------------------------------------------------------------

- Basado en "A model for Bitcoin's security and the declining block subsidy"
		https://uncommoncore.co/wp-content/uploads/2019/10/A-model-for-Bitcoins-security-and-the-declining-block-subsidy-v1.06.pdf
- Esperar mas por las confirmaciones.
- Quiebra de Mineros. Liquidación de sus activos (includio Bitcoin). Pueden reestructurar su deuda.
- Mineros no minar tx de menos de X sat/VByte. 
- O imponer fees por cantidad de valor transmitido.
- 


https://medium.com/@ksimsek19/feather-forking-f9f3d5b5f9aa

Comentar las amenazas regulatorias y legales para los mineros de Bitcoin en diferentes jurisdicciones.
------------------------------------------------------------------------------------------------------

- Prohibir el PoW en Europa. O directamente en China prohibir Bitcoin.

Discutir los riesgos asociados con la minería de Bitcoin, como ataques del 51% y la posibilidad de manipulación.
----------------------------------------------------------------------------------------------------------------

- Colusión con reguladores para no minar ciertas transacciones.


