# CCST Networking 100-150 — Preguntas de práctica
## Dominio 3: Endpoints and Media Types (30 preguntas)

---

**Pregunta 1. [Multiple Choice — Single Answer]**

Un técnico necesita conectar un PC de escritorio a un switch de red en una oficina. ¿Qué conector debe tener el cable Ethernet que utilice?

A) RJ-11

B) RJ-45

C) BNC

D) LC

<details>
<summary>Respuesta</summary>
✅ Correcta: B) RJ-45

💡 Explicación: El conector RJ-45 es el estándar para Ethernet en LANs. Tiene 8 pines (4 pares) y es rectangular con una lengüeta de enganche. RJ-11 es para telefonía (más pequeño, 2-6 pines). BNC es un conector coaxial para TV/DOCSIS. LC es un conector de fibra óptica.
</details>

---

**Pregunta 2. [Multiple Choice — Single Answer]**

¿Cuál es la distancia máxima soportada por los cables de par trenzado de categorías Cat 5e a Cat 7?

A) 30 metros

B) 55 metros

C) 100 metros

D) 1.500 metros

<details>
<summary>Respuesta</summary>
✅ Correcta: C) 100 metros

💡 Explicación: Todos los cables de par trenzado desde Cat 5e hasta Cat 7 tienen una distancia máxima general de 100 metros. Más allá de esa distancia la señal se degrada y se necesita fibra o un repetidor. Cat 8 es la excepción, con solo 30 metros. La distancia de 1.500 m es típica de fibra multimode.
</details>

---

**Pregunta 3. [Multiple Choice — Single Answer]**

¿Qué tipo de fibra óptica utiliza un láser como fuente de luz y puede alcanzar distancias de hasta 80 km?

A) Multimode

B) Single-mode

C) UTP

D) STP

<details>
<summary>Respuesta</summary>
✅ Correcta: B) Single-mode

💡 Explicación: La fibra single-mode tiene un núcleo pequeño (8-10 µm), utiliza láser de alta potencia como fuente de luz y alcanza hasta ~80 km (ampliable con amplificadores). Multimode usa LED, tiene un núcleo más grande y alcanza ~1,5 km. UTP y STP son tipos de cable de cobre, no de fibra.
</details>

---

**Pregunta 4. [Multiple Choice — Single Answer]**

¿Qué diferencia fundamental distingue al espectro utilizado por Wi-Fi del utilizado por redes celulares?

A) Wi-Fi usa espectro licenciado y celular usa espectro no licenciado

B) Wi-Fi usa espectro no licenciado y celular usa espectro licenciado

C) Ambos usan espectro licenciado pero con diferentes frecuencias

D) Ambos usan espectro no licenciado pero con diferente potencia

<details>
<summary>Respuesta</summary>
✅ Correcta: B) Wi-Fi usa espectro no licenciado y celular usa espectro licenciado

💡 Explicación: Wi-Fi opera en espectro no licenciado (cualquiera puede instalar un AP sin permiso gubernamental, con límite de potencia de ~250 mW). Las redes celulares operan en espectro licenciado, donde los operadores pagan por el derecho exclusivo de usar frecuencias específicas, eliminando la interferencia de otros dispositivos.
</details>

---

**Pregunta 5. [Multiple Choice — Single Answer]**

¿Qué función cumple un IoT Gateway (hub) en una red?

A) Amplifica la señal Wi-Fi para cubrir mayor área

B) Convierte los protocolos propietarios de los dispositivos IoT a IP estándar
  
C) Convierte los protocolos propietarios de los dispositivos IP estándar a IoT

D) Filtra el tráfico de broadcast entre VLANs

<details>
<summary>Respuesta</summary>
✅ Correcta: B) Convierte los protocolos propietarios de los dispositivos IoT a IP

💡 Explicación: El IoT Gateway actúa como traductor entre los protocolos propietarios de los dispositivos IoT (Bluetooth, ZWave, CAN, etc.) y el protocolo IP estándar, permitiendo que los datos lleguen al sistema de análisis central a través de la red IP. No es un amplificador Wi-Fi ni un dispositivo de filtrado de VLANs.
</details>

---

**Pregunta 6. [Multiple Choice — Single Answer]**

Un administrador ejecuta el comando `ipconfig /all` en un equipo Windows. ¿Cuál de los siguientes datos NO aparecerá en la salida?

A) Dirección IPv4 y máscara de subred

B) Servidor DHCP y lease time

C) Tabla de enrutamiento del host

D) Dirección física (MAC) de la interfaz

<details>
<summary>Respuesta</summary>
✅ Correcta: C) Tabla de enrutamiento del host

💡 Explicación: `ipconfig /all` muestra la dirección IPv4, IPv6 link-local, máscara de subred, gateway, servidores DNS, dirección MAC, si la IP fue asignada por DHCP, el servidor DHCP y los tiempos de lease. Para ver la tabla de enrutamiento en Windows se usa `Get-NetRoute` en PowerShell, no `ipconfig`.
</details>

---

**Pregunta 7. [Multiple Choice — Single Answer]**

¿Qué banda de frecuencia Wi-Fi tiene mayor alcance y mejor penetración de paredes, pero está más congestionada por dispositivos como microondas y Bluetooth?

A) 5 GHz

B) 6 GHz

C) 2,4 GHz

D) 900 MHz

<details>
<summary>Respuesta</summary>
✅ Correcta: C) 2,4 GHz

💡 Explicación: La banda de 2,4 GHz ofrece mayor alcance y mejor penetración de paredes, pero está muy congestionada porque la comparten microondas, dispositivos Bluetooth, monitores de bebé y otros aparatos. Solo tiene 3 canales no solapados (1, 6, 11). La banda de 5 GHz tiene menos interferencia pero menor alcance, y la de 6 GHz tiene canales aún más amplios pero alcance muy corto.
</details>

---

**Pregunta 8. [Multiple Choice — Single Answer]**

Un técnico necesita instalar cableado de red en el espacio de retorno de aire acondicionado (plenum) de un edificio comercial. ¿Qué tipo de cable es obligatorio en esta ubicación?

A) Cable STP estándar

B) Cable Cat 8

C) Cable plenum

D) Cable coaxial blindado

<details>
<summary>Respuesta</summary>
✅ Correcta: C) Cable plenum

💡 Explicación: Los cables plenum tienen un recubrimiento especial que no emite gases tóxicos al quemarse. Son obligatorios en los espacios de retorno de aire acondicionado (plenum) de edificios comerciales por normativa de seguridad contra incendios. Los cables estándar (STP, Cat 8, coaxial) no tienen necesariamente esta certificación.
</details>

---

**Pregunta 9. [Multiple Choice — Single Answer]**

¿Qué conector de fibra óptica es el más utilizado en redes actuales, tiene forma rectangular pequeña y permite alta densidad de puertos?

A) SC (Square Connector)

B) ST (Straight Tip)

C) LC (Lucent/Little Connector)

D) FC (Ferrule Connector)

<details>
<summary>Respuesta</summary>
✅ Correcta: C) LC (Lucent/Little Connector)

💡 Explicación: El conector LC es el más usado en redes actuales. Es rectangular, pequeño, con enganche por pestaña, y permite alta densidad de puertos en switches y paneles de parcheo. SC es cuadrado (push-pull), ST es redondo con bayoneta (legacy), y FC es redondo con rosca (telecomunicaciones/vibración).
</details>

---

**Pregunta 10. [Multiple Choice — Single Answer]**

¿Cuál es la principal defensa del cable de par trenzado contra las interferencias electromagnéticas?

A) El recubrimiento de plástico exterior

B) El trenzado de los pares

C) La conexión a tierra del conector RJ-45

D) El uso de fibra de vidrio como aislante interno

<details>
<summary>Respuesta</summary>
✅ Correcta: B) El trenzado de los pares

💡 Explicación: En el cable de par trenzado, los hilos de cada par se trenzan entre sí de forma que los campos magnéticos de cada hilo se cancelan mutuamente, reduciendo la interferencia electromagnética. Esta es la principal defensa contra el ruido. El blindaje metálico (STP) proporciona protección adicional, pero el trenzado es la defensa fundamental.
</details>

---

**Pregunta 11. [Multiple Choice — Single Answer]**

Un teléfono IP necesita alimentación eléctrica pero no hay enchufe disponible cerca. ¿Qué tecnología permite alimentar el teléfono directamente a través del cable Ethernet?

A) CSMA/CA

B) PoE

C) SFP+

D) WDM

<details>
<summary>Respuesta</summary>
✅ Correcta: B) PoE

💡 Explicación: PoE (Power over Ethernet) permite alimentar dispositivos pequeños como teléfonos IP, cámaras y APs Wi-Fi directamente a través del cable Ethernet, eliminando la necesidad de un enchufe separado. El estándar 802.3af (Type 1) proporciona hasta 12,95 W, suficiente para un teléfono IP. CSMA/CA es el método de acceso al medio Wi-Fi, SFP+ es una interfaz pluggable de 10G, y WDM es multiplexación por longitud de onda en fibra.
</details>

---

**Pregunta 12. [Multiple Choice — Single Answer]**

En Linux moderno, ¿qué comando se utiliza para ver la configuración IP de todas las interfaces de red?

A) ipconfig /all

B) ifconfig

C) ip addr

D) getmac /v

<details>
<summary>Respuesta</summary>
✅ Correcta: C) ip addr

💡 Explicación: En Linux moderno, `ip addr` es el comando recomendado para ver la configuración IP (similar a `ifconfig` pero con formato más compacto). `ipconfig /all` es exclusivo de Windows. `ifconfig` funciona en macOS y Linux legacy pero está siendo reemplazado por `ip addr`. `getmac /v` es un comando de Windows para ver las direcciones MAC.
</details>

---

**Pregunta 13. [Multiple Choice — Single Answer]**

¿Qué método de acceso al medio utiliza Wi-Fi para evitar colisiones antes de transmitir datos?

A) CSMA/CD (Collision Detection)

B) CSMA/CA (Collision Avoidance)

C) Token passing

D) TDMA (Time Division Multiple Access)

<details>
<summary>Respuesta</summary>
✅ Correcta: B) CSMA/CA (Collision Avoidance)

💡 Explicación: Wi-Fi usa CSMA/CA para evitar colisiones mediante señalización RTS/CTS (Request to Send / Clear to Send) antes de transmitir. CSMA/CD es el método de Ethernet cableado, que detecta colisiones después de que ocurren. No confundir ambos: CA = Wi-Fi (evita), CD = Ethernet cableado (detecta).
</details>

---

**Pregunta 14. [Multiple Choice — Single Answer]**

Un administrador ejecuta `tracert 8.8.8.8` en Windows y observa un asterisco (*) en el salto número 5. ¿Qué indica esto?

A) El router del salto 5 tiene un fallo hardware y debe ser reemplazado para garantizar la seguridad de la red

B) El router del salto 5 no envía respuestas ICMP o un firewall intermedio las bloquea

C) La conexión se ha perdido completamente a partir del salto 5

D) El paquete ha llegado al destino en el salto 5

<details>
<summary>Respuesta</summary>
✅ Correcta: B) El router del salto 5 no envía respuestas ICMP o un firewall intermedio las bloquea

💡 Explicación: Un asterisco (*) en la salida de traceroute/tracert indica que el router en ese salto no responde con mensajes ICMP, ya sea porque tiene las respuestas ICMP deshabilitadas por configuración o porque un firewall intermedio las bloquea. No significa necesariamente un fallo hardware ni que la conexión se haya perdido.
</details>

---

**Pregunta 15. [Multiple Choice — Single Answer]**

¿Qué estándar Wi-Fi introdujo la banda de 6 GHz y se identifica comercialmente como Wi-Fi 6E?

A) 802.11ac

B) 802.11n

C) 802.11ax

D) 802.11be

<details>
<summary>Respuesta</summary>
✅ Correcta: C) 802.11ax

💡 Explicación: 802.11ax es Wi-Fi 6/6E. La variante 6E añade la banda de 6 GHz al soporte de 2,4 y 5 GHz. Introdujo OFDMA y mejora el rendimiento en entornos de alta densidad. 802.11ac es Wi-Fi 5 (solo 5 GHz), 802.11n es Wi-Fi 4 (2,4/5 GHz), y 802.11be es Wi-Fi 7 (con canales de 320 MHz).
</details>

---

**Pregunta 16. [Multiple Choice — Single Answer]**

Un técnico necesita un cable para conectar dos switches que están en edificios separados a 500 metros de distancia. ¿Qué tipo de medio es el más adecuado?

A) Cable Cat 5e UTP

B) Cable Cat 6a STP

C) Fibra multimode

D) Cable coaxial DOCSIS

<details>
<summary>Respuesta</summary>
✅ Correcta: C) Fibra multimode

💡 Explicación: A 500 metros, el cable de cobre no es viable (distancia máxima de 100 m para Cat 5e a Cat 7). La fibra multimode alcanza ~1,5 km con LED y es más económica que single-mode, lo que la hace ideal para conexiones dentro de un campus. El cable coaxial DOCSIS no se usa para interconectar switches.
</details>

---

**Pregunta 17. [Multiple Choice — Choose Two]**

¿Cuáles de las siguientes son ventajas de la fibra óptica frente al cable de cobre? (Elige dos)

A) Es completamente inmune a interferencias electromagnéticas

B) Es más económica y fácil de instalar que el cobre

C) Ofrece mayor distancia de transmisión

D) Puede alimentar dispositivos endpoint mediante PoE

<details>
<summary>Respuesta</summary>
✅ Correcta: A) y C)

💡 Explicación: La fibra transmite con luz, no con electricidad, por lo que es completamente inmune a interferencias electromagnéticas (A). Además, alcanza distancias mucho mayores: ~1,5 km (multimode) o ~80 km (single-mode), frente a los 100 m del cobre (C). La fibra es más cara y frágil que el cobre (B es falsa), y no puede transmitir energía eléctrica para PoE (D es falsa).
</details>

---

**Pregunta 18. [Multiple Choice — Choose Two]**

¿Cuáles de las siguientes son fuentes habituales de interferencia que afectan a la señal Wi-Fi en la banda de 2,4 GHz? (Elige dos)

A) Hornos microondas

B) Cables de fibra óptica cercanos

C) Dispositivos Bluetooth

D) Cables coaxiales blindados

<details>
<summary>Respuesta</summary>
✅ Correcta: A) y C)

💡 Explicación: Los hornos microondas operan a 2,4 GHz, la misma frecuencia que Wi-Fi, causando interferencia directa (A). Los dispositivos Bluetooth también transmiten en 2,4 GHz y son una fuente habitual de interferencia (C). Los cables de fibra óptica (B) son inmunes a interferencias electromagnéticas y no las causan. Los cables coaxiales blindados (D) están diseñados para no emitir ni recibir interferencias significativas.
</details>

---

**Pregunta 19. [Multiple Choice — Choose Two]**

Un administrador necesita diagnosticar un problema de conectividad en un PC Windows. ¿Cuáles de los siguientes pasos forman parte de la estrategia de diagnóstico escalonado con ping? (Elige dos)

A) Hacer ping al gateway por defecto para verificar conectividad local

B) Hacer ping a una dirección MAC para verificar la capa 2

C) Hacer ping a un nombre de dominio para verificar DNS y enrutamiento

D) Hacer ping al servidor DHCP para renovar la IP automáticamente (proceso DORA)

<details>
<summary>Respuesta</summary>
✅ Correcta: A) y C)

💡 Explicación: La estrategia escalonada de ping es: (1) ping al gateway por defecto → verifica conectividad local; (2) ping a una IP remota → verifica enrutamiento; (3) ping a un nombre de dominio → verifica DNS + enrutamiento. Ping no puede dirigirse a una dirección MAC (opera en capa 3 con ICMP), y no sirve para renovar direcciones IP (eso es `ipconfig /renew`).
</details>

---

**Pregunta 20. [Multiple Choice — Choose Two]**

¿Cuáles de las siguientes afirmaciones sobre WPA Enterprise son correctas? (Elige dos)

A) Utiliza un servidor RADIUS externo para autenticar a cada usuario individualmente

B) Genera la clave pública a partir del SSID y una contraseña compartida por todos los usuarios

C) Es más seguro que WPA-PSK porque el atacante no puede derivar la clave inicial

D) No requiere ninguna infraestructura de servidor adicional

<details>
<summary>Respuesta</summary>
✅ Correcta: A) y C)

💡 Explicación: WPA Enterprise usa un servidor RADIUS externo para generar la clave pública y autenticar usuarios individualmente (A), lo que lo hace más seguro porque el atacante no puede derivar la clave inicial (C). La opción B describe WPA-PSK (Personal), donde la clave se genera del SSID + contraseña compartida. La opción D es falsa: Enterprise requiere un servidor RADIUS como infraestructura adicional.
</details>

---

**Pregunta 21. [Multiple Choice — Choose Two]**

¿Cuáles de las siguientes son diferencias entre `tracert` en Windows y `traceroute` en Linux/macOS? (Elige dos)

A) Windows envía paquetes ICMP Echo, mientras que Linux/macOS envían paquetes UDP

B) Windows no muestra el RTT (tiempo de ida y vuelta) pero Linux y macOS sí que lo muestran

C) El nombre del comando es `tracert` en Windows y `traceroute` en Linux/macOS

D) Traceroute en Linux no usa TTL incremental, a diferencia de Windows y macOS

<details>
<summary>Respuesta</summary>
✅ Correcta: A) y C)

💡 Explicación: Las dos diferencias principales son: (1) Windows usa paquetes ICMP Echo mientras que Linux/macOS usan paquetes UDP (A); y (2) el nombre del comando es diferente: `tracert` en Windows vs. `traceroute` en Linux/macOS (C). Ambos muestran RTT (B es falsa) y ambos usan TTL incremental como mecanismo de descubrimiento de ruta (D es falsa).
</details>

---

**Pregunta 22. [Multiple Choice — Choose Two]**

¿Cuáles de las siguientes son características de un servidor como endpoint de red? (Elige dos)

A) Se conecta habitualmente de forma cableada por Ethernet

B) Aloja servicios como webs, bases de datos y servicios cloud

C) Se conecta principalmente por Wi-Fi para facilitar su movilidad entre racks

D) Utiliza exclusivamente direcciones IP privadas y nunca se expone a Internet

<details>
<summary>Respuesta</summary>
✅ Correcta: A) y B)

💡 Explicación: Los servidores se conectan de forma cableada por Ethernet (a menudo con múltiples interfaces para redundancia y rendimiento) y alojan servicios como webs, bases de datos y servicios cloud. Los servidores rara vez usan Wi-Fi (C es falsa) y pueden usar tanto IPs privadas como públicas según su función (D es falsa).
</details>

---

**Pregunta 23. [Drag and Drop]**

Arrastra cada conector a su descripción física correcta.

**Elementos a arrastrar:**
- RJ-45
- RJ-11
- SC
- ST

**Categorías destino:**
- Rectangular con 8 pines y lengüeta de enganche — estándar de Ethernet
- Más pequeño que el anterior, con 2-6 pines — telefonía POTS
- Conector de fibra cuadrado con enganche push-pull
- Conector de fibra redondo con giro y presión (bayoneta)

<details>
<summary>Respuesta</summary>
✅ Correcta:

- RJ-45 → Rectangular con 8 pines y lengüeta de enganche — estándar de Ethernet

- RJ-11 → Más pequeño que el anterior, con 2-6 pines — telefonía POTS

- SC → Conector de fibra cuadrado con enganche push-pull

- ST → Conector de fibra redondo con giro y presión (bayoneta)

💡 Explicación: RJ-45 es el conector Ethernet estándar (8 pines, rectangular). RJ-11 es más pequeño y se usa para telefonía. SC (Square/Subscriber Connector) es cuadrado con push-pull. ST (Straight Tip) es redondo con mecanismo de bayoneta, típico de instalaciones legacy.
</details>

---

**Pregunta 24. [Drag and Drop]**

Arrastra cada categoría de cable Ethernet a su velocidad máxima.

**Elementos a arrastrar:**
- Cat 5e
- Cat 6a
- Cat 8

**Categorías destino:**
- 1 Gbps
- 10 Gbps
- 25–40 Gbps

<details>
<summary>Respuesta</summary>
✅ Correcta:

- Cat 5e → 1 Gbps

- Cat 6a → 10 Gbps

- Cat 8 → 25–40 Gbps

💡 Explicación: Cat 5e soporta hasta 1 Gbps a 100 m (el más común en oficinas). Cat 6a soporta 10 Gbps a 100 m (data centers, backbone). Cat 8 alcanza 25–40 Gbps pero solo a 30 m (conexiones cortas en data centers). Cada categoría superior mejora velocidad y/o protección contra interferencias.
</details>

---

**Pregunta 25. [Drag and Drop]**

Arrastra cada comando al sistema operativo donde se utiliza para ver la configuración IP completa.

**Elementos a arrastrar:**
- ipconfig /all
- ifconfig
- ip addr

**Categorías destino:**
- Windows
- macOS (y Linux legacy)
- Linux moderno

<details>
<summary>Respuesta</summary>
✅ Correcta:

- ipconfig /all → Windows

- ifconfig → macOS (y Linux legacy)

- ip addr → Linux moderno

💡 Explicación: Cada SO tiene su propio comando: `ipconfig /all` es exclusivo de Windows, `ifconfig` se usa en macOS y en Linux legacy (aunque en macOS sigue siendo el principal), y `ip addr` es el comando recomendado en Linux moderno, con formato más compacto e información de lease DHCP.
</details>

---

**Pregunta 26. [Drag and Drop]**

Arrastra cada tipo de fibra óptica a sus características.

**Elementos a arrastrar:**
- Multimode
- Single-mode

**Categorías destino:**
- Núcleo grande (50-62,5 µm), fuente LED, ~1,5 km máx., menor coste, interior de edificios
- Núcleo pequeño (8-10 µm), fuente láser, ~80 km máx., mayor coste, WAN y larga distancia

<details>
<summary>Respuesta</summary>
✅ Correcta:

- Multimode → Núcleo grande (50-62,5 µm), fuente LED, ~1,5 km máx., menor coste, interior de edificios

- Single-mode → Núcleo pequeño (8-10 µm), fuente láser, ~80 km máx., mayor coste, WAN y larga distancia

💡 Explicación: Multimode tiene un núcleo mayor que permite que la luz "rebote" (más dispersión), usa LED más barato y es adecuado para distancias cortas dentro de edificios o campus. Single-mode tiene un núcleo muy pequeño que permite una sola trayectoria de luz (menos dispersión), usa láser y alcanza distancias de decenas de kilómetros para WAN y backbone.
</details>

---

**Pregunta 27. [Drag and Drop]**

Arrastra cada estándar Wi-Fi a su nombre comercial.

**Elementos a arrastrar:**
- 802.11n
- 802.11ac
- 802.11ax
- 802.11be

**Categorías destino:**
- Wi-Fi 4
- Wi-Fi 5
- Wi-Fi 6/6E
- Wi-Fi 7

<details>
<summary>Respuesta</summary>
✅ Correcta:

- 802.11n → Wi-Fi 4

- 802.11ac → Wi-Fi 5

- 802.11ax → Wi-Fi 6/6E

- 802.11be → Wi-Fi 7

💡 Explicación: La Wi-Fi Alliance adoptó nombres comerciales simplificados: 802.11n = Wi-Fi 4 (introdujo MIMO y dual-band), 802.11ac = Wi-Fi 5 (MU-MIMO, solo 5 GHz), 802.11ax = Wi-Fi 6/6E (OFDMA, añade 6 GHz), 802.11be = Wi-Fi 7 (canales de 320 MHz, Multi-Link Operation).
</details>

---

**Pregunta 28. [Hotspot]**

Se muestra un rack de red con cuatro dispositivos conectados a un switch PoE mediante cable Ethernet:

| Posición | Dispositivo | Potencia necesaria |
|----------|------------|-------------------|
| **A** | Teléfono IP | 10 W |
| **B** | Cámara PTZ | 20 W |
| **C** | AP Wi-Fi 6 | 40 W |
| **D** | Servidor de rack | 500 W |

El switch soporta PoE+ (802.3at, hasta 25,5 W por puerto).

**Señala los dispositivos que NO podrán alimentarse por PoE+ y necesitarán un enchufe eléctrico independiente.**

<details>
<summary>Respuesta</summary>
✅ Correcta: Posición C — AP Wi-Fi 6 (40 W) y Posición D — Servidor de rack (500 W)

💡 Explicación: PoE+ (802.3at) proporciona hasta 25,5 W por puerto. El teléfono IP (10 W) y la cámara PTZ (20 W) están dentro del límite. El AP Wi-Fi 6 (40 W) supera los 25,5 W de PoE+ (necesitaría PoE++ con 802.3bt Type 3, hasta 51 W). El servidor (500 W) excede con creces cualquier estándar PoE. El AP Wi-Fi 6 (C) también es correcto si el switch no soporta PoE++.
</details>

---

**Pregunta 29. [Hotspot]**

Se muestra una tabla con la salida parcial del comando `ipconfig /all` en un PC Windows:

| Campo | Valor |
|-------|-------|
| Dirección IPv4 | 192.168.1.50 |
| Máscara de subred | 255.255.255.0 |
| Gateway por defecto | 192.168.1.1 |
| Servidor DNS | 8.8.8.8 |
| DHCP habilitado | Sí |
| Servidor DHCP | 192.168.1.1 |
| Dirección física | ¿? |

**¿Qué tipo de dirección aparecerá en el campo "Dirección física"?**

A) La dirección IPv6 link-local del host

B) La dirección MAC de la interfaz de red

C) La dirección IP del servidor DHCP

D) La dirección de broadcast de la subred

<details>
<summary>Respuesta</summary>
✅ Correcta: B) La dirección MAC de la interfaz de red

💡 Explicación: En la salida de `ipconfig /all`, el campo "Dirección física" (Physical Address) muestra la dirección MAC de la interfaz de red, con formato XX-XX-XX-XX-XX-XX (6 bytes hexadecimales separados por guiones en Windows). Es el identificador único de hardware de la tarjeta de red.
</details>

---

**Pregunta 30. [Hotspot]**

Se muestra una red de campus con tres escenarios de cableado:

| Escenario | Origen | Destino | Distancia | Medio a seleccionar |
|-----------|--------|---------|-----------|-------------------|
| **A** | PC oficina | Switch planta | 30 m | ¿? |
| **B** | Switch edificio 1 | Switch edificio 2 | 800 m | ¿? |
| **C** | Router campus | Router sede remota | 50 km | ¿? |

¿Qué tipo de medio en el escenario B es el más adecuado para 800 metros entre edificios?**

A) Cable Cat 6a UTP

B) Cable Cat 8

C) Fibra multimode

D) Cable coaxial DOCSIS

<details>
<summary>Respuesta</summary>
✅ Correcta: C) Fibra multimode

💡 Explicación: A 800 metros, el cable de cobre no es viable (máximo 100 m para Cat 5e–Cat 7, y 30 m para Cat 8). La fibra multimode alcanza hasta ~1,5 km y es más económica que single-mode, siendo ideal para conexiones entre edificios de un campus. El cable coaxial DOCSIS se usa para TV/Internet residencial, no para interconectar switches. Para el escenario C (50 km) se necesitaría fibra single-mode.
</details>

---

✅ 30 preguntas del Dominio 3 completadas.

📊 **Desglose por objetivo:**

| Objetivo | Tema | Preguntas | Total |
|----------|------|-----------|:-----:|
| **3.1** | Cables, conectores, fibra, cobre, PoE, SFP | 1, 2, 3, 8, 9, 10, 11, 16, 17, 23, 24, 26, 30 | **13** |
| **3.2** | Wi-Fi vs. celular vs. cableado, 802.11, interferencias | 4, 7, 13, 15, 18, 27 | **6** |
| **3.3** | Dispositivos endpoint: IoT, ordenadores, móviles, IP Phone | 5, 22, 28 | **3** |
| **3.4** | Conectividad Windows/Linux/Mac, comandos, SSID, WPA | 6, 12, 14, 19, 20, 21, 25, 29 | **8** |
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
| Fácil (40%) | **12** | 1, 2, 4, 5, 7, 9, 12, 13, 23, 24, 25, 29 |
| Medio (40%) | **12** | 3, 6, 8, 10, 11, 14, 15, 17, 18, 26, 27, 30 |
| Difícil (20%) | **6** | 16, 19, 20, 21, 22, 28 |
