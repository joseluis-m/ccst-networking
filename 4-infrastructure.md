# Dominio 4: Infrastructure

## Resumen ejecutivo

Este dominio evalúa tu capacidad para trabajar con el hardware físico de red: identificar dispositivos, puertos e indicadores luminosos; interpretar diagramas de red para cablear correctamente; y comprender cómo los switches y routers mueven paquetes a través de la infraestructura. Es el dominio más práctico y "manos en el hierro" del examen, con preguntas que combinan identificación visual de hardware con conceptos fundamentales de conmutación y enrutamiento. Presta especial atención a las diferencias entre switches Layer 2 y routers/switches Layer 3, y al proceso de decisión de reenvío basado en tablas MAC vs. tablas de enrutamiento IP.

---

## Conceptos clave

### 4.1 — Indicadores luminosos (Status Lights) en dispositivos Cisco

🔑 *Analogía:* Los LEDs de un dispositivo de red son como los testigos del salpicadero de un coche: verde fijo significa "todo bien", verde parpadeante significa "en marcha y trabajando", amarillo indica "atención, algo no va del todo bien", y rojo es "avería — actúa ahora".

Casi todos los puertos de un dispositivo de red tienen un LED asociado. Estos indicadores son la **primera herramienta de diagnóstico** cuando te acercas físicamente a un equipo.

**Significados generales estándar:**

| Estado del LED | Significado |
|----------------|-------------|
| **Verde fijo (solid green)** | Puerto operativo correctamente, enlace activo |
| **Verde parpadeante (flashing green)** | Puerto conectado y transmitiendo/recibiendo datos activamente |
| **Amarillo/Ámbar fijo (solid yellow/amber)** | El puerto está en proceso de conexión o tiene un fallo menor (error condition) |
| **Rojo fijo (solid red)** | El puerto ha sufrido un fallo grave (malfunction) |
| **Apagado (off)** | Sin enlace, puerto deshabilitado o cable desconectado |

**Advertencia importante para el examen:** Estos significados son los **convencionales**, pero **no son universales** en todos los dispositivos. Cisco advierte explícitamente que los colores y estados pueden significar cosas diferentes según el modelo de equipo. Por ejemplo, en el Cisco 1120 Connected Grid Router, un LED verde parpadeante en un puerto pluggable indica que la interfaz se puede extraer de forma segura — no que esté transmitiendo datos. En algunos data centers de gran escala, los operadores programan los LEDs para usar azul en lugar de verde y solo luces fijas, porque el volumen de luces parpadeantes dificulta encontrar fallos.

**Regla de oro:** Si no estás seguro, consulta siempre el manual del equipo específico. Pero para el examen, los significados estándar de la tabla anterior son los que se evaluarán.

**LEDs adicionales comunes en dispositivos:**

Además de los LEDs por puerto, los dispositivos suelen tener indicadores de sistema: **POWER** (alimentación activa), **STATUS/SYS** (estado general del sistema), **ALARM** (alarma activa). Algunos módulos de servidor insertados en routers ISR tienen sus propios indicadores de alimentación, estado y botón de reset independientes del router principal.

---

### 4.2 — Diagramas de red y cableado

🔑 *Analogía:* Un diagrama físico es como el plano de fontanería de un edificio (muestra por dónde van las tuberías). Un diagrama lógico es como el mapa de presión del agua (muestra hacia dónde fluye y a qué velocidad). Ambos son imprescindibles pero muestran cosas diferentes.

#### Tipos de diagramas de red

| Característica | **Diagrama físico** | **Diagrama lógico** |
|----------------|---------------------|---------------------|
| **Muestra** | Ubicación real de equipos, recorrido de cables, racks, patch panels | Flujo de paquetes, conexiones lógicas entre dispositivos |
| **Incluye** | Longitudes de cable, posición en rack, tipos de conector | Direcciones IP, protocolos de enrutamiento, políticas de filtrado |
| **No incluye normalmente** | Direcciones IP ni protocolos | Patch panels, recorrido físico de cables ni ubicaciones en rack |
| **Se usa para** | Planificar cableado, evitar cables redundantes en el mismo conducto, estimar longitudes | Seguir el flujo del tráfico, diagnosticar problemas lógicos, entender la topología |

**Reglas mnemotécnicas:**

- Diagramas **físicos** → siguen el recorrido de los **cables**.
- Diagramas **lógicos** → siguen el recorrido de los **paquetes**.

#### Equipamiento en un rack

Al entrar en una sala de comunicaciones o data center encontrarás pocas categorías de equipos, aunque todos se parezcan externamente: **routers**, **switches**, **patch panels**, **servidores**, **almacenamiento**, **equipos ópticos** y **otros middleboxes** (firewalls, IDS, balanceadores). La única forma fiable de identificarlos es por sus **etiquetas y números de modelo**.

La altura de los equipos se mide en **rack units (RU)**: 1 RU = 1,75 pulgadas = 44,45 mm. Un switch pequeño puede ocupar 1 RU; un router grande con módulos puede ocupar 3-4 RU. Planificar la disposición del rack debe incluir espacio para **organizadores de cable** (fingerboards, lacing bars, cable shelves) que evitan el "cable spaghetti" y reducen fallos por tensión en los conectores.

#### Patch panels y gestión de cables

Los **patch panels** se utilizan cuando el cableado cambia frecuentemente (por ejemplo, conectar equipos a rosetas de pared). Permiten reconectar sin manipular los cables permanentes de la instalación. En la práctica, se interponen entre el cableado estructurado del edificio y los puertos de switches/routers.

**Buenas prácticas de cableado:**

- Usar organizadores horizontales tipo D-ring para mantener cables en filas ordenadas.
- Los cables de cobre **nunca deben tener bucles** (actúan como antenas y generan interferencia); se deben cortar a la longitud correcta.
- Los cables de fibra sí pueden tener bucles controlados para absorber exceso de longitud.
- Cables colgando de sus propios conectores generan tensión mecánica (*strain*) que puede provocar fallos. Los strain gauges en los cables comerciales mitigan este problema, pero la gestión de cables adecuada es imprescindible.
- Las bandejas de cables aéreas (overhead cable trays) han sustituido a los suelos técnicos elevados en la mayoría de diseños modernos. Hay que calcular peso y calor generado por los cables al diseñarlas.

#### Alimentación y refrigeración

Los routers y switches de gama alta suelen tener **fuentes de alimentación redundantes** (reemplazables en caliente en muchos casos) y **bandejas de ventiladores (fan trays)** también reemplazables. La refrigeración del data center se gestiona mediante **CRAC (Computer Room Air Conditioner)** que empuja aire frío bajo el suelo técnico o por conductos superiores. Los racks se orientan creando **pasillos fríos (cold aisle)** por el frente y **pasillos calientes (hot aisle)** por la parte trasera, donde se expulsa el aire caliente. El sellado del hot aisle mejora enormemente la eficiencia de refrigeración. Algunos data centers a gran escala usan **refrigeración evaporativa** con aire exterior.

---

### 4.3 — Puertos en dispositivos de red

🔑 *Analogía:* Los puertos de un router son como las puertas de un aeropuerto — cada una tiene un propósito específico: la puerta de embarque principal (Ethernet para datos), la puerta de servicio (consola para mantenimiento), la puerta de carga (fibra para grandes volúmenes a larga distancia) y la puerta VIP (management para acceso de administración separado).

#### Tabla de tipos de puertos

| Puerto | Conector típico | Velocidad | Función principal |
|--------|-----------------|-----------|-------------------|
| **Console** | RJ-45 (Ethernet baja velocidad), USB, o multi-pin serie | Baja (9600-115200 bps) | Acceso directo al CLI del dispositivo para configuración inicial o recuperación. Es el "plan B" si falla todo lo demás. |
| **Auxiliary (AUX)** | RJ-45 o DB-25 | Baja | Acceso alternativo al CLI, históricamente para conexión por módem. Similar al console. |
| **Management** | RJ-45 (1 GbE) | 1 Gbps | Conecta a la red de gestión out-of-band (OOB). Nunca transporta datos de usuario. No todos los operadores usan OOB; algunos gestionan in-band. |
| **Ethernet (RJ-45)** | RJ-45 | 100 Mbps – 10 Gbps | Puertos de datos para conectar hosts, switches u otros routers. Pueden soportar PoE. |
| **SFP / SFP+ / QSFP** | Pluggable (LC fibra o RJ-45 cobre) | 1G / 10G / 40G / 100G | Interfaces modulares que aceptan diferentes transceptores según necesidad (fibra multimode, single-mode, cobre). Ofrecen flexibilidad de despliegue. |
| **Fibra (fijo)** | LC, SC, ST | Varía | Puertos ópticos fijos de alta velocidad. Menos comunes que los pluggables. |
| **USB** | USB-A o USB-C | Varía | Para console (con cable USB-a-RJ45/DB9), almacenamiento de configuraciones, o actualizaciones de firmware. |
| **PoE (Power over Ethernet)** | RJ-45 | 1 Gbps típico | Puertos Ethernet que además suministran alimentación eléctrica al dispositivo conectado (APs, IP Phones, cámaras). |

#### Puertos fijos vs. modulares

Los dispositivos de red tienen dos tipos de puertos:

- **Puertos fijos:** Soldados permanentemente a la placa. No se pueden reemplazar. Se identifican porque no tienen tornillos de sujeción a su alrededor.
- **Puertos modulares (NIM, SM, line cards):** Insertados en ranuras del chasis. Se pueden extraer y reemplazar. Se identifican por los tornillos laterales de sujeción. Las **line cards** son módulos más grandes con su propio motor de reenvío; los **NIM (Network Interface Modules)** usan el motor de reenvío del router principal.

**Combo ports:** Algunos puertos GigabitEthernet ofrecen un RJ-45 y un slot SFP adyacentes, pero **solo uno puede estar activo a la vez**. Insertar un SFP desactiva automáticamente el RJ-45 correspondiente.

#### Numeración de puertos Cisco

La convención sigue el formato: **TipoVelocidad Slot/Subslot/Puerto**

| Formato | Significado | Ejemplo |
|---------|-------------|---------|
| **GE1** | Puerto fijo, sin módulos | GigabitEthernet puerto 1 |
| **GE0/1** | Slot de módulo / Puerto | Módulo 0, puerto 1 |
| **GE0/0/1** | Slot / Subslot / Puerto | Slot 0, subslot 0, puerto 1 |
| **TE0/0/4** | Ten Gigabit, slot 0, subslot 0, puerto 4 | Puerto 10G fijo |

Prefijos de velocidad: **FE** = FastEthernet (100M), **GE** = GigabitEthernet (1G), **TE** = TenGigabitEthernet (10G). Los puertos pares suelen estar en la fila inferior; los impares en la superior.

---

### 4.4 — Conceptos básicos de enrutamiento

🔑 *Analogía:* Un router es como una oficina de correos central entre barrios. Cuando envías una carta a alguien de tu propio barrio, el cartero local (switch) la entrega directamente. Pero si el destino está en otro barrio, la carta debe pasar primero por la oficina central (router/default gateway) que decide por qué ruta enviarla al barrio correcto.

#### Red local vs. red remota

La distinción fundamental es:

| Concepto | Red local (same segment) | Red remota (different segment) |
|----------|--------------------------|-------------------------------|
| **Definición** | Hosts en el mismo segmento/broadcast domain, accesibles sin pasar por un router | Hosts en un segmento diferente, accesibles solo a través de un router |
| **Comunicación** | El host envía directamente usando la dirección MAC del destino (descubierta por ARP/ND) | El host envía al default gateway usando la MAC del router |
| **Dirección física destino** | MAC del host destino | MAC del router (default gateway) |
| **Dirección IP destino** | IP del host destino | IP del host destino (se mantiene a lo largo de toda la ruta) |
| **Broadcast** | Se reciben | No cruzan el router |

**Cómo decide un host si el destino es local o remoto:** El host compara la dirección IP de destino con su propia IP y máscara de subred. Si ambas direcciones pertenecen a la misma red (mismo prefijo), el destino es local. Si no, es remoto y el paquete se envía al default gateway.

#### Default gateway (puerta de enlace predeterminada)

Es la dirección IP del router al que un host envía **todos los paquetes cuyo destino no está en su red local**. Se configura de tres formas: vía **DHCP** (automáticamente), mediante **Router Advertisements** en IPv6 (SLAAC), o **manualmente** en la configuración de red del host.

**Proceso de envío a un destino remoto:**

1. El host *A* quiere enviar un paquete a *G* (red remota).
2. *A* determina que *G* no está en su segmento local.
3. *A* construye el paquete con **IP destino = G** pero **MAC destino = router C** (su default gateway).
4. El router *C* recibe el paquete (porque la MAC destino coincide con la suya), examina la **IP destino** y consulta su **tabla de enrutamiento (RIB)**.
5. *C* encuentra la ruta hacia la red de *G*, reemplaza la cabecera de capa 2 con una nueva (MAC destino = siguiente salto *D*) y reenvía el paquete.
6. El proceso se repite en cada router hasta llegar al destino final.

**Dato clave:** En cada salto, la **cabecera de capa 2 (MAC) cambia** pero la **cabecera de capa 3 (IP) permanece igual**. Esto es fundamental y es una pregunta frecuente en el examen.

#### Tabla de enrutamiento (RIB)

Cada router mantiene una tabla que contiene: **red destino**, **interfaz de salida** y **next hop** (siguiente salto). La tabla se construye a partir de tres fuentes:

| Fuente | Descripción |
|--------|-------------|
| **Interfaces conectadas** | Redes directamente conectadas al router (automático) |
| **Rutas estáticas** | Configuradas manualmente por el operador |
| **Protocolos de enrutamiento dinámico** | Aprendidas automáticamente de otros routers (RIP, OSPF, EIGRP, BGP, IS-IS) |

Al conjunto de métodos para construir la tabla de enrutamiento se le denomina **control plane**.

**Longest Prefix Match:** Cuando existen múltiples rutas posibles hacia un destino, el router siempre elige la que tiene el **prefijo más largo** (más específico). Ejemplo: si hay rutas hacia /56, /58 y /60 que cubren la IP destino, el router elige la /60 aunque su ruta tenga más saltos. Las rutas con diferente longitud de prefijo se tratan como **destinos distintos**.

**Métricas:** Si hay varias rutas con el mismo prefijo, el router elige la de **menor coste/métrica** (por ejemplo, menor número de saltos o mayor ancho de banda).

#### Protocolos de enrutamiento

| Tipo | Protocolo | Cómo funciona |
|------|-----------|---------------|
| **Distance-vector** | RIP, EIGRP (DUAL) | Cada router comparte con sus vecinos las redes que conoce y el coste para alcanzarlas. Algoritmo Bellman-Ford. |
| **Link-state** | OSPF, IS-IS | Cada router comparte información sobre sus vecinos directos. Todos construyen un mapa completo de la red (LSDB) y calculan la ruta más corta (SPF/Dijkstra). |
| **Path-vector** | BGP | Cada router comparte la lista completa de routers que hay que atravesar para llegar al destino. Decisión basada en políticas. |

#### Routing loops y TTL

Un **routing loop** ocurre cuando los paquetes circulan indefinidamente entre routers por una configuración incorrecta. El **TTL (Time-to-Live)** del paquete IP se decrementa en 1 en cada salto; cuando llega a 0, el paquete se descarta. Esto previene que los loops consuman recursos indefinidamente. Las tramas de capa 2 (switched) **no tienen TTL**, por lo que un loop en una red conmutada es potencialmente más destructivo — de ahí la importancia de **STP**.

#### ICMP Redirect y DHCP Relay

- **ICMP Redirect:** Cuando un router recibe un paquete que debe reenviar por la misma interfaz por la que lo recibió, puede enviar un mensaje ICMP redirect al host de origen indicándole un mejor default gateway para ese destino.
- **DHCP Relay:** Los routers no reenvían broadcasts, por lo que un host en un segmento sin servidor DHCP no puede obtener dirección. La solución: configurar el router como **DHCP relay**, que recibe el broadcast DHCP y lo reenvía como unicast al servidor DHCP en otro segmento.

#### Switch Layer 2 vs. Switch Layer 3 vs. Router

| Característica | **Switch Layer 2** | **Router / Switch Layer 3** |
|----------------|--------------------|-----------------------------|
| Reenvía según | Dirección **MAC** (física, capa 2) | Dirección **IP** (interfaz, capa 3) |
| Tabla de decisión | **MAC address table** (forwarding/bridge table) | **Routing table (RIB)** |
| Broadcast domain | **No separa** — todos los puertos están en el mismo broadcast domain (salvo VLANs) | **Separa** — cada interfaz es un broadcast domain distinto |
| Aprendizaje | Examina la MAC origen de cada trama recibida (bridge learning) | Protocolos de enrutamiento, rutas estáticas, interfaces conectadas |
| TTL | No decrementa (las tramas no tienen TTL) | Decrementa en 1 por cada salto |
| Velocidad histórica | Hardware (muy rápido) | Software (lento originalmente) → Hardware actual (igual de rápido) |
| Loop prevention | **STP (Spanning Tree Protocol)** | **TTL** + algoritmos de enrutamiento sin loops |

**¿Qué es un switch Layer 3?** Un dispositivo con hardware de conmutación de alta velocidad (como un switch) pero que toma decisiones basadas en direcciones IP (como un router). El término surgió como compromiso comercial cuando se crearon los primeros routers con reenvío por hardware. Hoy en día, el término "switch" puede referirse tanto a un Layer 2 como a un Layer 3, por lo que siempre hay que clarificar cuál de los dos es.

---

### 4.5 — Conceptos básicos de switching

🔑 *Analogía:* Un switch es como un recepcionista de hotel que aprende en qué habitación está cada huésped. La primera vez que alguien baja al vestíbulo, el recepcionista anota su nombre y número de habitación. Las siguientes veces, ya sabe exactamente dónde enviar los mensajes sin preguntar a todo el hotel.

#### Tabla de direcciones MAC (MAC Address Table / Forwarding Table)

Es la tabla central que un switch usa para decidir por qué puerto reenviar cada trama. Contiene asociaciones entre **direcciones MAC** y **puertos**.

**Proceso de bridge learning (aprendizaje):**

1. El switch recibe una trama por el **puerto 1** con **MAC origen = A**.
2. El switch registra en su tabla: "MAC A → Puerto 1".
3. El switch examina la **MAC destino** de la trama.
4. Si la MAC destino **está en la tabla** → reenvía solo por el puerto correspondiente (**forwarding**).
5. Si la MAC destino **no está en la tabla** → reenvía por **todos los puertos activos** excepto el de origen (**flooding**).
6. Si la MAC destino es **broadcast** (ff:ff:ff:ff:ff:ff) o **multicast** → reenvía por todos los puertos activos.

**Ejemplo de salida `show mac address-table`:**

| VLAN | MAC Address | Type | Ports |
|------|-------------|------|-------|
| All | 0000.5E44.4444 | STATIC | CPU |
| 1 | 0000.5E11.1111 | Dynamic | Fe1 |
| 1 | 0000.5E22.2222 | Dynamic | Fe2 |

- Las entradas **Dynamic** se aprenden automáticamente del tráfico de la red.
- Las entradas **Static** están configuradas manualmente o son propias del sistema.
- La columna **VLAN** indica a qué VLAN pertenece esa asociación.

#### MAC Address Filtering (filtrado MAC)

El filtrado MAC es el proceso por el cual un switch decide **no reenviar** una trama cuando la MAC destino está asociada al **mismo puerto** por donde se recibió la trama. Si host *A* y host *B* están ambos conectados al puerto 1, y *A* envía una trama a *B*, el switch ve que la MAC destino (*B*) se alcanza por el puerto 1, que es el mismo por donde llegó la trama. El switch **descarta** la trama (no la reenvía) porque *B* ya la ha recibido al estar en el mismo segmento. Esto reduce el tráfico innecesario y es clave para la escalabilidad de las redes.

En el contexto de seguridad (home routers), el filtrado MAC también se refiere a la función **Block List** que permite bloquear dispositivos específicos basándose en su dirección MAC. Si la MAC de un dispositivo está en la lista de bloqueo, el router/AP rechaza su conexión a la red.

#### Spanning Tree Protocol (STP)

Cuando hay **múltiples switches interconectados**, pueden formarse bucles (loops) por los que las tramas circulan indefinidamente — las tramas de capa 2 **no tienen TTL**. STP previene esto:

1. **Elige un root bridge** (switch raíz) como referencia.
2. **Calcula el camino más corto** desde cada switch al root bridge usando métricas asignadas a cada enlace.
3. **Bloquea los puertos** que no están en el camino más corto, dejando solo los puertos en estado **forwarding** necesarios para una topología sin loops.

El camino más corto **nunca puede ser un loop** (un loop siempre recorrería algún tramo dos veces). Si la topología cambia (un enlace cae o se añade un switch), STP **recalcula** y los switches deben reaprender las asociaciones MAC.

#### VLANs (Virtual LANs)

Una VLAN es un **segmento de red de capa 2 definido lógicamente**, no físicamente. Permite agrupar puertos de uno o varios switches en un mismo broadcast domain, independientemente de su ubicación física.

**Conceptos clave:**

- Cada VLAN es un **broadcast domain separado**. Los broadcasts de una VLAN no llegan a puertos de otra VLAN.
- Los dispositivos en **la misma VLAN** pueden comunicarse directamente (como si estuvieran en el mismo switch físico).
- Los dispositivos en **VLANs diferentes** solo pueden comunicarse a través de un **router o switch Layer 3** — necesitan enrutamiento entre VLANs (inter-VLAN routing).
- Los switches gestionados permiten asignar cada puerto a una VLAN específica.
- **VLAN 1** es la VLAN por defecto en switches Cisco; todos los puertos pertenecen a ella inicialmente. La interfaz VLAN 1 es donde se configura la dirección IP de gestión del switch.

**Relación con SSID en Wi-Fi:** Cada SSID en un AP inalámbrico representa un broadcast domain separado, conceptualmente equivalente a una VLAN. Dispositivos conectados a SSIDs diferentes solo pueden comunicarse a través de un router.

**Configuración del switch (conceptos):**

- Los puertos individuales del switch **no necesitan dirección IP** porque no enrutan paquetes IP; solo conmutan tramas por MAC.
- Se configura una **única dirección IP en la interfaz VLAN 1** (o la VLAN de gestión) para permitir acceso remoto al switch (Telnet/SSH).
- El acceso inicial al switch se realiza por el **puerto console**, igual que en un router.

---

## 🎯 Puntos críticos para el examen

- **LEDs:** Verde fijo = OK. Verde parpadeante = transmitiendo datos. Amarillo = problema o conectando. Rojo = fallo grave. Apagado = sin enlace. Pero **siempre consulta el manual** del dispositivo específico.
- **Puerto console** = acceso directo al CLI para configuración inicial/recuperación. **Management port** = red de gestión OOB separada del tráfico de usuario. Son puertos diferentes con propósitos diferentes.
- **Diagrama físico** → muestra cables, racks, patch panels, recorridos. **Diagrama lógico** → muestra IPs, protocolos, flujo de paquetes. El examen puede pedir que identifiques cuál usar para cada tarea.
- **Numeración de puertos Cisco:** GE0/0/1 = GigabitEthernet, Slot 0, Subslot 0, Puerto 1. Identifica el prefijo de velocidad (FE, GE, TE) y la jerarquía slot/subslot/port.
- **Combo ports (RJ-45 + SFP):** Solo uno puede estar activo a la vez. Insertar un SFP desactiva el RJ-45 adyacente.
- **Default gateway** = la IP del router al que el host envía todo el tráfico que no es para su red local. Si no está configurado o es incorrecto, el host no puede alcanzar redes remotas.
- **Envío a red remota:** El host pone la **MAC del router** como destino de capa 2, pero la **IP del destino final** en capa 3. **La MAC cambia en cada salto; la IP se mantiene durante todo el camino.**
- **Longest Prefix Match:** El router elige siempre la ruta con el prefijo **más largo** (más específico) que cubra la IP destino, independientemente de la métrica.
- **Switch Layer 2:** Reenvía por MAC, no separa broadcast domains (salvo VLANs), no tiene TTL.  **Router / Layer 3 switch:** Reenvía por IP, separa broadcast domains, decrementa TTL.
- **Bridge learning:** El switch aprende las MAC **de origen** de las tramas que recibe y las asocia al puerto de entrada. Nunca aprende de las MAC de destino.
- **STP** previene loops en redes conmutadas (Layer 2). **TTL** previene loops en redes enrutadas (Layer 3). No confundirlos.
- **VLANs:** Cada VLAN = un broadcast domain separado. Comunicación entre VLANs = requiere router/switch L3. **VLAN 1** = VLAN por defecto en Cisco.
- **Switch IP:** Se configura en **interface VLAN 1**, no en puertos individuales. Los puertos del switch no tienen IP.
- **MAC filtering en switch:** Si la MAC destino se alcanza por el mismo puerto que la MAC origen, el switch **no reenvía** la trama (ya llegó).
- **1 RU = 1,75 pulgadas = 44,45 mm.** Los equipos de red se miden en RUs para planificar el espacio en rack.

---

## Mini-resumen

- **Status lights:** Verde fijo = operativo; verde parpadeante = transmitiendo; amarillo = error/conectando; rojo = fallo; apagado = sin enlace. Varían según modelo — consultar siempre el manual del equipo concreto.
- **Diagramas y cableado:** Los diagramas **físicos** muestran recorrido de cables, racks y patch panels; los **lógicos** muestran IPs, protocolos y flujo de paquetes. En el rack (medido en **RU** de 44,45 mm), se organizan cables con fingerboards, lacing bars y cable trays aéreos. Los patch panels facilitan reconexiones frecuentes. Fuentes de alimentación y fan trays suelen ser redundantes y reemplazables.
- **Puertos:** **Console** (CLI directo, configuración inicial), **management** (red OOB de gestión), **Ethernet/RJ-45** (datos, con posible PoE), **SFP/pluggable** (modulares para fibra o cobre según necesidad), **USB** (console alternativo, almacenamiento). Numeración: Tipo + Slot/Subslot/Puerto (GE0/0/1). Combo ports: solo un modo activo (RJ-45 o SFP).
- **Routing:** El host envía paquetes para redes remotas al **default gateway** (MAC router + IP destino final). El router consulta su **tabla de enrutamiento (RIB)** y aplica **longest prefix match** para elegir la mejor ruta. Fuentes de rutas: conectadas, estáticas, dinámicas (RIP, OSPF, EIGRP, IS-IS, BGP). En cada salto, la **MAC cambia** pero la **IP se mantiene**. El **TTL** se decrementa para evitar routing loops. **ICMP redirect** optimiza el gateway; **DHCP relay** permite DHCP entre segmentos.
- **Switching:** El switch aprende direcciones MAC del tráfico de origen (**bridge learning**) y construye una **MAC address table**. Si conoce el puerto destino → reenvía solo ahí (**forwarding**). Si no → flooding por todos los puertos. **STP** previene loops bloqueando puertos redundantes. **VLANs** crean broadcast domains lógicos separados; cada VLAN necesita un router para comunicarse con otra. **VLAN 1** es la VLAN por defecto donde se configura la IP de gestión del switch.
- **Layer 2 vs. Layer 3:** Switches L2 conmutan por MAC (sin TTL, sin separar broadcasts salvo VLANs, STP contra loops). Routers y switches L3 enrutan por IP (con TTL, separan broadcasts, protocolos de enrutamiento contra loops). El término "switch Layer 3" = router con hardware de conmutación de alta velocidad.
