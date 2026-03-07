# CCST Networking 100-150 — Preguntas de práctica
## Dominio 4: Infrastructure (30 preguntas)

---

**Pregunta 1. [Multiple Choice — Single Answer]**
Un técnico se acerca a un switch Cisco y observa que el LED de un puerto está en verde fijo (solid green). ¿Qué indica este estado?

A) El puerto está transmitiendo datos activamente
B) El puerto está operativo correctamente con un enlace activo
C) El puerto tiene un fallo menor y está intentando conectarse
D) El puerto no tiene cable conectado

<respuesta>
✅ Correcta: B) El puerto está operativo correctamente con un enlace activo
💡 Explicación: Verde fijo (solid green) indica que el puerto está operativo y tiene un enlace activo. Verde parpadeante (flashing green) indica que está transmitiendo/recibiendo datos activamente. Amarillo indica un fallo menor o que está en proceso de conexión. Un LED apagado indica que no hay enlace o cable conectado.
</respuesta>

---

**Pregunta 2. [Multiple Choice — Single Answer]**
¿Qué tipo de diagrama de red muestra la ubicación real de los equipos, el recorrido de los cables, los racks y los patch panels?

A) Diagrama lógico
B) Diagrama físico
C) Diagrama de flujo de datos
D) Diagrama de protocolo

<respuesta>
✅ Correcta: B) Diagrama físico
💡 Explicación: Un diagrama físico muestra la ubicación real de equipos, recorrido de cables, racks, patch panels y longitudes de cable. Un diagrama lógico muestra el flujo de paquetes, direcciones IP, protocolos y conexiones lógicas. La regla mnemotécnica es: diagramas físicos siguen los cables; diagramas lógicos siguen los paquetes.
</respuesta>

---

**Pregunta 3. [Multiple Choice — Single Answer]**
¿Cuál es la función principal del puerto console en un router o switch Cisco?

A) Transportar datos de usuario a alta velocidad
B) Conectar a la red de gestión out-of-band (OOB)
C) Proporcionar acceso directo al CLI para configuración inicial o recuperación
D) Suministrar alimentación PoE a dispositivos conectados

<respuesta>
✅ Correcta: C) Proporcionar acceso directo al CLI para configuración inicial o recuperación
💡 Explicación: El puerto console ofrece acceso directo al CLI del dispositivo para configuración inicial o recuperación cuando no hay conectividad de red. Es el "plan B" si falla todo lo demás. Opera a baja velocidad (9600-115200 bps) y usa conectores RJ-45, USB o serie. La opción B describe el puerto management (OOB), no el console.
</respuesta>

---

**Pregunta 4. [Multiple Choice — Single Answer]**
Un host con dirección 192.168.1.50/24 quiere enviar un paquete a 10.0.0.100. ¿Qué dirección MAC utilizará como destino en la trama de capa 2?

A) La MAC del host 10.0.0.100
B) La MAC de broadcast (ff:ff:ff:ff:ff:ff)
C) Su propia MAC
D) La MAC de su default gateway (router)

<respuesta>
✅ Correcta: D) La MAC de su default gateway (router)
💡 Explicación: El host compara 10.0.0.100 con su propia red (192.168.1.0/24) y determina que el destino es remoto (diferente prefijo). Para destinos remotos, el host construye la trama con MAC destino = MAC del default gateway (router), pero mantiene la IP destino = 10.0.0.100 en la cabecera de capa 3. La MAC cambia en cada salto; la IP se mantiene durante todo el camino.
</respuesta>

---

**Pregunta 5. [Multiple Choice — Single Answer]**
¿Cómo aprende un switch las direcciones MAC de los dispositivos conectados a sus puertos?

A) Examinando la dirección MAC de destino de cada trama recibida
B) Mediante consultas ARP a todos los dispositivos de la red
C) Examinando la dirección MAC de origen de cada trama recibida (bridge learning)
D) Consultando un servidor DHCP central que le proporciona la tabla MAC

<respuesta>
✅ Correcta: C) Examinando la dirección MAC de origen de cada trama recibida (bridge learning)
💡 Explicación: El proceso de bridge learning funciona así: cuando el switch recibe una trama por un puerto, registra la MAC de origen y la asocia al puerto de entrada en su MAC address table. Nunca aprende de las MAC de destino. Este proceso es automático y crea entradas de tipo "Dynamic" en la tabla.
</respuesta>

---

**Pregunta 6. [Multiple Choice — Single Answer]**
En la nomenclatura de puertos Cisco, ¿qué indica la designación GE0/0/1?

A) GigabitEthernet, módulo fijo, puerto 1
B) GigabitEthernet, Slot 0, Subslot 0, Puerto 1
C) GigabitEthernet, VLAN 0, Interfaz 0, Puerto 1
D) GigabitEthernet, velocidad 0 Gbps, 0 errores, Puerto 1

<respuesta>
✅ Correcta: B) GigabitEthernet, Slot 0, Subslot 0, Puerto 1
💡 Explicación: La convención Cisco sigue el formato TipoVelocidad Slot/Subslot/Puerto. GE = GigabitEthernet (1G), seguido de Slot 0, Subslot 0, Puerto 1. Otros prefijos de velocidad son FE (FastEthernet, 100M) y TE (TenGigabitEthernet, 10G).
</respuesta>

---

**Pregunta 7. [Multiple Choice — Single Answer]**
¿Qué mecanismo previene routing loops en paquetes IP de capa 3?

A) STP (Spanning Tree Protocol)
B) TTL (Time-to-Live)
C) VLAN tagging
D) MAC address filtering

<respuesta>
✅ Correcta: B) TTL (Time-to-Live)
💡 Explicación: El TTL del paquete IP se decrementa en 1 en cada salto de router; cuando llega a 0, el paquete se descarta, evitando que circule indefinidamente. STP (opción A) previene loops en redes conmutadas de capa 2, no en redes enrutadas. Las tramas de capa 2 no tienen TTL, lo que hace los loops L2 potencialmente más destructivos.
</respuesta>

---

**Pregunta 8. [Multiple Choice — Single Answer]**
Un switch recibe una trama cuya dirección MAC destino no está en su MAC address table. ¿Qué acción toma?

A) Descarta la trama silenciosamente
B) Envía un mensaje ICMP de error al origen
C) Reenvía la trama por todos los puertos activos excepto el de origen (flooding)
D) Almacena la trama hasta que el destino envíe tráfico y se registre su MAC

<respuesta>
✅ Correcta: C) Reenvía la trama por todos los puertos activos excepto el de origen (flooding)
💡 Explicación: Cuando la MAC destino es desconocida (no está en la tabla), el switch realiza flooding: reenvía la trama por todos los puertos activos excepto el puerto por donde la recibió. Cuando el destino responda, el switch aprenderá su MAC (bridge learning) y las tramas siguientes se enviarán solo al puerto correcto (forwarding).
</respuesta>

---

**Pregunta 9. [Multiple Choice — Single Answer]**
¿Qué unidad de medida se utiliza para la altura de los equipos montados en un rack de red?

A) Centímetros (cm)
B) Rack Units (RU) — 1 RU = 1,75 pulgadas
C) Pulgadas estándar sin denominación especial
D) Milímetros métricos (mm estándar)

<respuesta>
✅ Correcta: B) Rack Units (RU) — 1 RU = 1,75 pulgadas
💡 Explicación: La altura en racks se mide en RU (Rack Units), donde 1 RU = 1,75 pulgadas = 44,45 mm. Un switch pequeño puede ocupar 1 RU; un router grande con módulos puede ocupar 3-4 RU. Esta medida es estándar en la industria para planificar el espacio en armarios de comunicaciones y data centers.
</respuesta>

---

**Pregunta 10. [Multiple Choice — Single Answer]**
¿Cuál es la VLAN por defecto en switches Cisco, donde se configura la dirección IP de gestión del switch?

A) VLAN 0
B) VLAN 1
C) VLAN 100
D) VLAN 999

<respuesta>
✅ Correcta: B) VLAN 1
💡 Explicación: VLAN 1 es la VLAN por defecto en switches Cisco. Todos los puertos pertenecen a ella inicialmente. La interfaz VLAN 1 es donde se configura la dirección IP de gestión del switch para permitir acceso remoto (Telnet/SSH). Los puertos individuales del switch no necesitan dirección IP porque no enrutan — solo conmutan tramas por MAC.
</respuesta>

---

**Pregunta 11. [Multiple Choice — Single Answer]**
¿Qué protocolo utilizan los switches para prevenir bucles (loops) en redes conmutadas de capa 2?

A) TTL (Time-to-Live)
B) BGP (Border Gateway Protocol)
C) STP (Spanning Tree Protocol)
D) OSPF (Open Shortest Path First)

<respuesta>
✅ Correcta: C) STP (Spanning Tree Protocol)
💡 Explicación: STP previene loops en redes conmutadas eligiendo un root bridge como referencia, calculando el camino más corto de cada switch al root, y bloqueando los puertos que no están en ese camino. Las tramas de capa 2 no tienen TTL, por lo que sin STP un loop sería potencialmente destructivo. TTL previene loops en capa 3, y BGP/OSPF son protocolos de enrutamiento.
</respuesta>

---

**Pregunta 12. [Multiple Choice — Single Answer]**
Un router Cisco tiene combo ports con un RJ-45 y un slot SFP adyacentes. Un técnico inserta un módulo SFP de fibra. ¿Qué ocurre con el puerto RJ-45 adyacente?

A) Ambos puertos quedan activos simultáneamente
B) El puerto RJ-45 se desactiva automáticamente
C) El SFP se desactiva porque el RJ-45 tiene prioridad
D) Se requiere reiniciar el dispositivo para activar el SFP

<respuesta>
✅ Correcta: B) El puerto RJ-45 se desactiva automáticamente
💡 Explicación: En los combo ports, solo uno puede estar activo a la vez. Insertar un módulo SFP desactiva automáticamente el puerto RJ-45 adyacente. No es posible usar ambos simultáneamente ni se requiere reinicio. El SFP tiene prioridad sobre el RJ-45 cuando se inserta.
</respuesta>

---

**Pregunta 13. [Multiple Choice — Single Answer]**
Un router tiene las siguientes rutas en su tabla de enrutamiento:
- 10.0.0.0/8 → Interfaz GE0/0
- 10.1.0.0/16 → Interfaz GE0/1
- 10.1.1.0/24 → Interfaz GE0/2

Un paquete llega con destino 10.1.1.50. ¿Por qué interfaz lo reenviará el router?

A) GE0/0 (ruta /8)
B) GE0/1 (ruta /16)
C) GE0/2 (ruta /24)
D) Descartará el paquete porque hay rutas ambiguas

<respuesta>
✅ Correcta: C) GE0/2 (ruta /24)
💡 Explicación: El router aplica Longest Prefix Match: siempre elige la ruta con el prefijo más largo (más específico) que cubra la IP destino. Las tres rutas cubren 10.1.1.50, pero /24 es el prefijo más largo, por lo que el router elige GE0/2. Las rutas con diferente longitud de prefijo se tratan como destinos distintos.
</respuesta>

---

**Pregunta 14. [Multiple Choice — Single Answer]**
¿Qué función cumple un DHCP relay configurado en un router?

A) Asigna direcciones IP a los hosts directamente desde el router
B) Recibe el broadcast DHCP de un segmento sin servidor DHCP y lo reenvía como unicast al servidor DHCP en otro segmento
C) Bloquea las solicitudes DHCP no autorizadas para mejorar la seguridad
D) Traduce direcciones IPv4 de DHCP a direcciones IPv6

<respuesta>
✅ Correcta: B) Recibe el broadcast DHCP de un segmento sin servidor DHCP y lo reenvía como unicast al servidor DHCP en otro segmento
💡 Explicación: Los routers no reenvían broadcasts entre interfaces. Si un host está en un segmento sin servidor DHCP local, su broadcast Discover nunca llegará al servidor. El DHCP relay resuelve esto: el router recibe el broadcast DHCP y lo reenvía como unicast al servidor DHCP en otro segmento, permitiendo la asignación de direcciones.
</respuesta>

---

**Pregunta 15. [Multiple Choice — Single Answer]**
¿En qué interfaz de un switch Cisco se configura la dirección IP para gestión remota?

A) En cada puerto Ethernet individual
B) En el puerto console
C) En la interfaz VLAN 1 (o la VLAN de gestión)
D) En la interfaz loopback 0

<respuesta>
✅ Correcta: C) En la interfaz VLAN 1 (o la VLAN de gestión)
💡 Explicación: Los puertos individuales de un switch no necesitan dirección IP porque solo conmutan tramas por MAC. Se configura una única dirección IP en la interfaz VLAN 1 (o la VLAN de gestión designada) para permitir acceso remoto al switch vía Telnet o SSH. El puerto console es para acceso físico directo al CLI, no para gestión IP remota.
</respuesta>

---

**Pregunta 16. [Multiple Choice — Single Answer]**
¿Cuál es la diferencia entre un patch panel y un switch en un rack de comunicaciones?

A) El patch panel reenvía tramas basándose en direcciones MAC; el switch solo conecta cables
B) El patch panel permite reconectar cableado sin manipular los cables permanentes de la instalación; el switch conmuta tráfico de red activamente
C) El patch panel proporciona PoE; el switch no
D) No hay diferencia funcional; son términos intercambiables

<respuesta>
✅ Correcta: B) El patch panel permite reconectar cableado sin manipular los cables permanentes de la instalación; el switch conmuta tráfico de red activamente
💡 Explicación: Los patch panels son dispositivos pasivos que se interponen entre el cableado estructurado del edificio y los puertos de switches/routers, permitiendo reconectar sin manipular los cables permanentes. Un switch es un dispositivo activo que conmuta tramas basándose en direcciones MAC. No son intercambiables.
</respuesta>

---

**Pregunta 17. [Multiple Choice — Choose Two]**
¿Cuáles de las siguientes afirmaciones describen correctamente cómo funciona el envío de un paquete a una red remota? (Elige dos)

A) El host pone como MAC destino la dirección MAC de su default gateway (router)
B) El host pone como MAC destino la dirección MAC del host destino final
C) La dirección IP destino se mantiene igual durante todo el camino a través de los routers
D) La dirección IP destino cambia en cada salto de router

<respuesta>
✅ Correcta: A) y C)
💡 Explicación: Para destinos remotos, el host construye la trama con MAC destino = MAC del router (default gateway) y la IP destino = IP del host final. En cada salto, la cabecera de capa 2 (MAC) cambia (se reemplaza con la MAC del siguiente salto), pero la cabecera de capa 3 (IP) permanece igual durante todo el camino. Esta es una distinción fundamental del examen.
</respuesta>

---

**Pregunta 18. [Multiple Choice — Choose Two]**
¿Cuáles de las siguientes son características de un switch Layer 2? (Elige dos)

A) Reenvía tramas basándose en direcciones MAC usando su MAC address table
B) Decrementa el TTL de cada paquete que procesa
C) No separa dominios de broadcast por defecto (salvo con VLANs)
D) Toma decisiones de reenvío basadas en direcciones IP y su tabla de enrutamiento (RIB)

<respuesta>
✅ Correcta: A) y C)
💡 Explicación: Un switch Layer 2 reenvía tramas usando direcciones MAC (A) y no separa dominios de broadcast por defecto — todos los puertos comparten el mismo broadcast domain salvo que se configuren VLANs (C). La opción B (decrementar TTL) y D (decisiones por IP/RIB) son funciones de routers y switches Layer 3, no de switches Layer 2.
</respuesta>

---

**Pregunta 19. [Multiple Choice — Choose Two]**
¿Cuáles de las siguientes son fuentes de información para construir la tabla de enrutamiento (RIB) de un router? (Elige dos)

A) Redes directamente conectadas a las interfaces del router
B) Entradas MAC aprendidas por bridge learning
C) Rutas estáticas configuradas manualmente por el operador
D) Tramas de broadcast recibidas por los puertos del switch

<respuesta>
✅ Correcta: A) y C)
💡 Explicación: La tabla de enrutamiento se construye a partir de tres fuentes: interfaces conectadas (automáticas), rutas estáticas (manuales) y protocolos de enrutamiento dinámico (RIP, OSPF, EIGRP, BGP, IS-IS). Bridge learning (B) es el mecanismo de los switches L2 para construir su MAC table, no la RIB del router. Las tramas de broadcast (D) no contribuyen a la tabla de enrutamiento.
</respuesta>

---

**Pregunta 20. [Multiple Choice — Choose Two]**
¿Cuáles de las siguientes afirmaciones sobre VLANs son correctas? (Elige dos)

A) Cada VLAN es un broadcast domain separado — los broadcasts de una VLAN no llegan a otra
B) Los dispositivos en VLANs diferentes pueden comunicarse directamente sin necesidad de un router
C) Los dispositivos en la misma VLAN pueden comunicarse directamente como si estuvieran en el mismo switch físico
D) Las VLANs solo pueden configurarse si todos los puertos están en el mismo switch físico

<respuesta>
✅ Correcta: A) y C)
💡 Explicación: Cada VLAN es un broadcast domain separado (A), y los dispositivos en la misma VLAN se comunican directamente sin importar su ubicación física (C). La opción B es falsa: la comunicación entre VLANs diferentes requiere obligatoriamente un router o switch Layer 3 (inter-VLAN routing). La opción D es falsa: las VLANs pueden extenderse por múltiples switches.
</respuesta>

---

**Pregunta 21. [Multiple Choice — Choose Two]**
¿Cuáles de las siguientes son buenas prácticas de gestión de cableado en un rack? (Elige dos)

A) Crear bucles en los cables de cobre para absorber exceso de longitud
B) Usar organizadores horizontales tipo D-ring para mantener cables ordenados
C) Cortar los cables de cobre a la longitud correcta en lugar de dejar exceso
D) Dejar cables colgando de sus conectores para facilitar el acceso rápido

<respuesta>
✅ Correcta: B) y C)
💡 Explicación: Los organizadores tipo D-ring mantienen los cables en filas ordenadas (B). Los cables de cobre deben cortarse a la longitud correcta (C) porque los bucles actúan como antenas y generan interferencia. La opción A es incorrecta: solo los cables de fibra pueden tener bucles controlados. La opción D es incorrecta: cables colgando generan tensión mecánica (strain) que provoca fallos.
</respuesta>

---

**Pregunta 22. [Multiple Choice — Choose Two]**
¿Cuáles de las siguientes son diferencias entre el puerto console y el puerto management de un router Cisco? (Elige dos)

A) El puerto console proporciona acceso directo al CLI para configuración inicial; el management conecta a una red OOB de gestión
B) El puerto console opera a alta velocidad (10 Gbps); el management opera a baja velocidad
C) El management nunca transporta datos de usuario; se reserva exclusivamente para administración del dispositivo
D) El console requiere conectividad IP completa; el management funciona sin red

<respuesta>
✅ Correcta: A) y C)
💡 Explicación: El console ofrece acceso directo al CLI sin necesidad de red IP, para configuración inicial o recuperación (A). El management conecta a una red OOB (out-of-band) de gestión separada del tráfico de usuario (C). La opción B invierte las velocidades (console es baja velocidad; management es 1 GbE). La opción D también invierte la funcionalidad (console no necesita IP; management sí).
</respuesta>

---

**Pregunta 23. [Drag and Drop]**
Arrastra cada estado de LED a su significado estándar en dispositivos Cisco.

**Elementos a arrastrar:**
- Verde fijo (solid green)
- Verde parpadeante (flashing green)
- Amarillo/Ámbar fijo (solid amber)
- Apagado (off)

**Categorías destino:**
- Puerto operativo correctamente, enlace activo
- Puerto conectado, transmitiendo/recibiendo datos activamente
- Puerto en proceso de conexión o con un fallo menor
- Sin enlace, puerto deshabilitado o cable desconectado

<respuesta>
✅ Correcta:
- Verde fijo → Puerto operativo correctamente, enlace activo
- Verde parpadeante → Puerto conectado, transmitiendo/recibiendo datos activamente
- Amarillo/Ámbar fijo → Puerto en proceso de conexión o con un fallo menor
- Apagado → Sin enlace, puerto deshabilitado o cable desconectado
💡 Explicación: Estos son los significados estándar convencionales evaluados en el examen CCST. Nota: Cisco advierte que los colores pueden variar según el modelo, por lo que siempre se debe consultar el manual del equipo específico. El LED rojo fijo (no incluido aquí) indica fallo grave.
</respuesta>

---

**Pregunta 24. [Drag and Drop]**
Arrastra cada tipo de puerto a su función principal.

**Elementos a arrastrar:**
- Console
- Management
- SFP/SFP+
- PoE Ethernet

**Categorías destino:**
- Acceso directo al CLI para configuración inicial o recuperación
- Conectar a la red de gestión out-of-band (OOB), nunca transporta datos de usuario
- Interfaces modulares que aceptan transceptores de fibra o cobre según necesidad
- Puerto de datos que además suministra alimentación eléctrica al dispositivo conectado

<respuesta>
✅ Correcta:
- Console → Acceso directo al CLI para configuración inicial o recuperación
- Management → Conectar a la red de gestión out-of-band (OOB), nunca transporta datos de usuario
- SFP/SFP+ → Interfaces modulares que aceptan transceptores de fibra o cobre según necesidad
- PoE Ethernet → Puerto de datos que además suministra alimentación eléctrica al dispositivo conectado
💡 Explicación: Cada tipo de puerto tiene una función específica. El console es el "plan B" para acceso directo. El management separa la administración del tráfico de datos. Los SFP ofrecen flexibilidad de medio físico. Los puertos PoE combinan datos y alimentación eléctrica.
</respuesta>

---

**Pregunta 25. [Drag and Drop]**
Arrastra cada característica al tipo de dispositivo correcto.

**Elementos a arrastrar:**
- Reenvía según dirección MAC; usa MAC address table
- Reenvía según dirección IP; usa tabla de enrutamiento (RIB)
- Previene loops con STP
- Previene loops con TTL

**Categorías destino:**
- Switch Layer 2
- Router / Switch Layer 3

<respuesta>
✅ Correcta:
- Reenvía según dirección MAC; usa MAC address table → Switch Layer 2
- Reenvía según dirección IP; usa tabla de enrutamiento (RIB) → Router / Switch Layer 3
- Previene loops con STP → Switch Layer 2
- Previene loops con TTL → Router / Switch Layer 3
💡 Explicación: Los switches L2 operan con MACs y usan STP contra loops (las tramas no tienen TTL). Los routers y switches L3 operan con IPs, usan la RIB para decisiones de reenvío, y el TTL previene routing loops decrementándose en cada salto.
</respuesta>

---

**Pregunta 26. [Drag and Drop]**
Arrastra cada tipo de diagrama de red al tipo de información que muestra.

**Elementos a arrastrar:**
- Diagrama físico
- Diagrama lógico

**Categorías destino:**
- Ubicación real de equipos, recorrido de cables, posición en rack, longitudes de cable, patch panels
- Flujo de paquetes, direcciones IP, protocolos de enrutamiento, políticas de filtrado, conexiones lógicas

<respuesta>
✅ Correcta:
- Diagrama físico → Ubicación real de equipos, recorrido de cables, posición en rack, longitudes de cable, patch panels
- Diagrama lógico → Flujo de paquetes, direcciones IP, protocolos de enrutamiento, políticas de filtrado, conexiones lógicas
💡 Explicación: Los diagramas físicos siguen el recorrido de los cables y muestran la infraestructura tangible. Los diagramas lógicos siguen el recorrido de los paquetes y muestran la topología abstracta. Cada uno se usa para tareas diferentes: físico para planificar cableado, lógico para diagnosticar problemas de tráfico.
</respuesta>

---

**Pregunta 27. [Drag and Drop]**
Arrastra cada paso del proceso STP a su posición correcta en la secuencia (del 1 al 3).

**Elementos a arrastrar:**
- Calcular el camino más corto desde cada switch al root bridge
- Elegir un root bridge (switch raíz) como referencia
- Bloquear los puertos que no están en el camino más corto

**Posiciones destino:**
- Paso 1
- Paso 2
- Paso 3

<respuesta>
✅ Correcta:
- Paso 1 → Elegir un root bridge (switch raíz) como referencia
- Paso 2 → Calcular el camino más corto desde cada switch al root bridge
- Paso 3 → Bloquear los puertos que no están en el camino más corto
💡 Explicación: STP primero elige un root bridge como punto de referencia central. Luego cada switch calcula la ruta más corta al root bridge usando métricas de enlace. Finalmente, los puertos que no forman parte de ningún camino más corto se bloquean, dejando solo una topología sin loops con puertos en estado forwarding.
</respuesta>

---

**Pregunta 28. [Hotspot]**
*Descripción del diagrama:* Se muestra un rack de comunicaciones con los siguientes equipos montados de arriba a abajo:

| Posición | Equipo | Descripción |
|----------|--------|-------------|
| **A** | Patch panel 24 puertos | Dispositivo pasivo con puertos RJ-45 numerados, sin LEDs de actividad |
| **B** | Switch Cisco 24 puertos | Dispositivo activo con LEDs en cada puerto, etiqueta "Catalyst 2960" |
| **C** | Router Cisco | Dispositivo con puertos GE0/0, GE0/1, un puerto Console y un Management |
| **D** | Organizador de cable | Barra metálica horizontal tipo D-ring sin puertos |

Un técnico necesita conectar un cable patch entre una roseta de pared (cableado estructurado) y un puerto del switch. **Señala por qué equipo pasará primero el cable desde la roseta de pared.**

<respuesta>
✅ Correcta: Posición A — Patch panel 24 puertos
💡 Explicación: Los patch panels se interponen entre el cableado estructurado del edificio (rosetas de pared) y los puertos de los switches. El cable desde la roseta de pared llega primero al patch panel, y desde ahí un cable patch corto conecta al switch. Esto permite reconectar sin manipular los cables permanentes de la instalación.
</respuesta>

---

**Pregunta 29. [Hotspot]**
*Descripción del diagrama:* Se muestra una red con tres dispositivos (Host A, Switch S1, Router R1) y la siguiente tabla MAC del switch S1:

| VLAN | MAC Address | Type | Ports |
|------|-------------|------|-------|
| 1 | 0000.AA11.1111 | Dynamic | Fa0/1 |
| 1 | 0000.BB22.2222 | Dynamic | Fa0/2 |
| 1 | 0000.CC33.3333 | Dynamic | Fa0/3 |

Host A (MAC: 0000.AA11.1111, conectado a Fa0/1) envía una trama con MAC destino 0000.DD44.4444, que NO está en la tabla.

**Señala qué acción tomará el switch S1 al recibir esta trama.**

A) Descartar la trama porque la MAC destino no está registrada
B) Reenviar la trama solo por el puerto Fa0/3
C) Reenviar la trama por los puertos Fa0/2 y Fa0/3 (flooding por todos excepto Fa0/1)
D) Enviar un mensaje de error ARP al Host A

<respuesta>
✅ Correcta: C) Reenviar la trama por los puertos Fa0/2 y Fa0/3 (flooding por todos excepto Fa0/1)
💡 Explicación: La MAC 0000.DD44.4444 no está en la tabla del switch, así que realiza flooding: reenvía la trama por todos los puertos activos excepto el de origen (Fa0/1). Esto significa que la trama sale por Fa0/2 y Fa0/3. Si el dispositivo destino responde, el switch aprenderá su MAC y la asociará al puerto correspondiente.
</respuesta>

---

**Pregunta 30. [Hotspot]**
*Descripción del diagrama:* Se muestra la siguiente topología simplificada:

```
[PC-A: 192.168.1.10/24] --- [Switch L2] --- [Router: 192.168.1.1] --- [Internet] --- [Server: 8.8.8.8]
```

PC-A tiene configurado como default gateway 192.168.1.1 y quiere acceder al servidor 8.8.8.8.

**Señala qué cabeceras tendrá el paquete cuando sale de PC-A hacia el switch:**

| Campo | Valor |
|-------|-------|
| **MAC origen** | ¿? |
| **MAC destino** | ¿? |
| **IP origen** | ¿? |
| **IP destino** | ¿? |

A) MAC origen = PC-A, MAC destino = Server, IP origen = PC-A, IP destino = Server
B) MAC origen = PC-A, MAC destino = Router, IP origen = PC-A, IP destino = Server
C) MAC origen = PC-A, MAC destino = Router, IP origen = PC-A, IP destino = Router
D) MAC origen = Router, MAC destino = Server, IP origen = PC-A, IP destino = Server

<respuesta>
✅ Correcta: B) MAC origen = PC-A, MAC destino = Router, IP origen = PC-A, IP destino = Server
💡 Explicación: PC-A determina que 8.8.8.8 es una red remota (distinto prefijo a 192.168.1.0/24). Construye la trama con MAC destino = MAC del router (su default gateway 192.168.1.1) para que el switch la entregue al router en capa 2. Pero la IP destino se mantiene como 8.8.8.8 (el servidor final). La MAC cambia en cada salto; la IP permanece durante todo el camino.
</respuesta>

---

✅ 30 preguntas del Dominio 4 completadas.

📊 **Desglose por objetivo:**

| Objetivo | Tema | Preguntas | Total |
|----------|------|-----------|:-----:|
| **4.1** | Luces de estado (LEDs) en dispositivos Cisco | 1, 23 | **2** |
| **4.2** | Diagramas de red, cableado, racks, patch panels | 2, 9, 16, 21, 26, 28 | **6** |
| **4.3** | Puertos: console, management, SFP, PoE, numeración | 3, 6, 12, 22, 24 | **5** |
| **4.4** | Routing: default gateway, L2 vs. L3, longest prefix match, RIB, TTL | 4, 7, 13, 14, 17, 19, 25, 30 | **8** |
| **4.5** | Switching: MAC table, bridge learning, flooding, STP, VLAN, filtering | 5, 8, 10, 11, 15, 18, 20, 27, 29 | **9** |
| | | **TOTAL** | **30** |

📋 **Desglose por tipo de pregunta:**

| Tipo | Cantidad | Preguntas |
|------|:--------:|-----------|
| Multiple Choice (1 respuesta) | **16** | 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16 |
| Multiple Choice (Choose Two) | **6** | 17, 18, 19, 20, 21, 22 |
| Drag and Drop | **5** | 23, 24, 25, 26, 27 |
| Hotspot | **3** | 28, 29, 30 |

🎯 **Desglose por dificultad:**

| Nivel | Cantidad | Preguntas |
|-------|:--------:|-----------|
| Fácil (40%) | **12** | 1, 2, 3, 5, 7, 9, 10, 11, 15, 23, 24, 26 |
| Medio (40%) | **12** | 4, 6, 8, 12, 14, 16, 17, 18, 20, 25, 27, 28 |
| Difícil (20%) | **6** | 13, 19, 21, 22, 29, 30 |
