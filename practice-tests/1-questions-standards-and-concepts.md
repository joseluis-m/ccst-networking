# CCST Networking 100-150 — Preguntas de práctica
## Dominio 1: Standards and Concepts (30 preguntas)

---

**Pregunta 1. [Multiple Choice — Single Answer]**

¿Qué capa del modelo OSI es responsable del formato y cifrado de datos antes de entregarlos a la capa de sesión?

A) Application

B) Presentation

C) Transport

D) Data Link

<details>
<summary>Respuesta</summary>
✅ Correcta: B) Presentation

💡 Explicación: La capa 6 (Presentation) se encarga del formato y cifrado de datos (por ejemplo, SSL/TLS, JPEG). Application (capa 7) es la interfaz con el usuario, Transport (capa 4) gestiona la entrega extremo a extremo, y Data Link (capa 2) maneja el direccionamiento físico.
</details>

---

**Pregunta 2. [Multiple Choice — Single Answer]**

Un técnico necesita medir el throughput entre dos hosts dentro de la red local de la oficina, sin involucrar la conexión a Internet. ¿Qué herramienta debería utilizar?

A) Un speed test como Ookla

B) El comando ping

C) iPerf

D) traceroute

<details>
<summary>Respuesta</summary>
✅ Correcta: C) iPerf

💡 Explicación: iPerf mide el rendimiento entre dos puntos cualesquiera de la red (LAN o Internet) instalando un servidor y un cliente. Un speed test como Ookla mide el rendimiento hacia el ISP, no entre hosts internos. Ping mide latencia (no throughput) y traceroute muestra la ruta de los paquetes.
</details>

---

**Pregunta 3. [Multiple Choice — Single Answer]**

¿Qué tipo de red opera dentro de un vehículo y conecta sensores mediante protocolos como CAN bus?

A) PAN

B) LAN

C) CAN

D) MAN

<details>
<summary>Respuesta</summary>
✅ Correcta: C) CAN
  
💡 Explicación: CAN (Car Area Network) opera dentro de un vehículo y utiliza protocolos como CAN bus para conectar sensores. PAN cubre el entorno de una persona (Bluetooth), LAN cubre un edificio o campus, y MAN cubre una ciudad o área metropolitana.
</details>

---

**Pregunta 4. [Multiple Choice — Single Answer]**

Una empresa usa Salesforce para gestionar sus relaciones con clientes. Los empleados acceden a la aplicación vía navegador web sin instalar ni gestionar nada. ¿Qué modelo de servicio cloud representa este escenario?

A) IaaS

B) PaaS

C) SaaS

D) On-premises

<details>
<summary>Respuesta</summary>
✅ Correcta: C) SaaS

💡 Explicación: SaaS (Software as a Service) proporciona la aplicación completa accesible vía web; el usuario simplemente la usa. Salesforce, Gmail y Office 365 son ejemplos de SaaS. En IaaS el usuario gestiona las apps sobre infraestructura del proveedor, en PaaS desarrolla aplicaciones, y on-premises implica gestionar todo localmente.
</details>

---

**Pregunta 5. [Multiple Choice — Single Answer]**

Un paquete IP viaja desde el Host A al Host B a través de dos routers. ¿Qué afirmación describe correctamente lo que ocurre con las direcciones en cada router?

A) Las direcciones IP y las direcciones MAC se mantienen iguales en todo el camino

B) Las direcciones MAC cambian en cada salto; las direcciones IP permanecen iguales

C) Las direcciones IP cambian en cada salto; las direcciones MAC permanecen iguales

D) Tanto las direcciones IP como las MAC se regeneran aleatoriamente en cada router

<details>
<summary>Respuesta</summary>
✅ Correcta: B) Las direcciones MAC cambian en cada salto; las direcciones IP permanecen iguales

💡 Explicación: Cada router descarta la trama de capa 2 y crea una nueva con las direcciones MAC del siguiente salto, pero el paquete de capa 3 (con las IPs origen y destino) permanece intacto durante toda la ruta. Esto es fundamental para entender la diferencia entre reenvío de capa 2 y capa 3.
</details>

---

**Pregunta 6. [Multiple Choice — Choose Two]**

¿Cuáles de los siguientes son componentes del delay (latencia) de red? (Elige dos)

A) Serialization delay — tiempo necesario para clockear los bits del paquete al medio

B) Goodput delay — tiempo necesario para filtrar los datos útiles del tráfico total

C) Queueing delay — tiempo de espera en cola cuando la interfaz de salida está saturada

D) Bandwidth delay — tiempo de espera mientras se calcula la capacidad máxima del enlace

<details>
<summary>Respuesta</summary>
✅ Correcta: A) y C)

💡 Explicación: Los tres componentes del delay son: propagation delay (distancia física), serialization delay (clockear bits al medio) y queueing delay (espera en cola por saturación). "Goodput delay" y "bandwidth delay" no existen como componentes del delay; son términos inventados como distractores.
</details>

---

**Pregunta 7. [Multiple Choice — Single Answer]**

¿Cuál es el orden correcto de los pasos que sigue DHCP para asignar una dirección IPv4 a un host?

A) Request → Discover → Offer → Acknowledge

B) Discover → Offer → Request → Acknowledge

C) Offer → Discover → Acknowledge → Request

D) Discover → Request → Offer → Acknowledge

<details>
<summary>Respuesta</summary>
✅ Correcta: B) Discover → Offer → Request → Acknowledge
  
💡 Explicación: El proceso DHCP sigue el acrónimo DORA: el cliente envía un broadcast Discover buscando un servidor, el servidor responde con una Offer, el cliente acepta con un Request, y el servidor confirma con un Acknowledge que incluye IP, máscara, gateway, DNS y lease time.
</details>

---

**Pregunta 8. [Drag and Drop]**

Arrastra cada protocolo a su número de puerto correcto.

**Elementos a arrastrar:**
- HTTPS
- DNS
- FTP (control)
- TFTP

**Categorías destino:**
- Puerto 21
- Puerto 53
- Puerto 69
- Puerto 443

<details>
<summary>Respuesta</summary>
✅ Correcta:
  
- FTP (control) → Puerto 21

- DNS → Puerto 53

- TFTP → Puerto 69

- HTTPS → Puerto 443

💡 Explicación: FTP usa el puerto 21 para control (y 20 para datos). DNS usa el puerto 53. TFTP usa el puerto 69 sobre UDP. HTTPS usa el puerto 443 sobre TCP. Estos son puertos estándar que aparecen frecuentemente en el examen CCST.
</details>

---

**Pregunta 9. [Multiple Choice — Single Answer]**

En el modelo TCP/IP de 4 capas, ¿qué capa equivale a las capas 1 y 2 del modelo OSI y maneja tecnologías como Ethernet y Wi-Fi?

A) Application

B) Transport

C) Internet

D) Network Interface

<details>
<summary>Respuesta</summary>
✅ Correcta: D) Network Interface

💡 Explicación: La capa Network Interface del modelo TCP/IP agrupa las capas Physical (1) y Data Link (2) del OSI, manejando tecnologías como Ethernet y Wi-Fi. Application agrupa las capas 5-7, Transport equivale a la capa 4, e Internet equivale a la capa 3.
</details>

---

**Pregunta 10. [Multiple Choice — Single Answer]**

Un usuario de VoIP experimenta cortes y distorsiones en el audio durante una llamada. ¿Qué problema de red es la causa más probable?

A) Bandwidth insuficiente en el enlace troncal

B) Jitter elevado entre paquetes consecutivos

C) Dirección IP duplicada en la red

D) Error en la configuración DNS del servidor VoIP

<details>
<summary>Respuesta</summary>
✅ Correcta: B) Jitter elevado entre paquetes consecutivos

💡 Explicación: El jitter es la variación del delay entre paquetes consecutivos y es especialmente dañino para aplicaciones de streaming y VoIP porque produce interrupciones en el audio. Las aplicaciones usan buffers para compensarlo, pero los buffers añaden delay adicional. Las otras opciones no producen el síntoma específico de cortes y distorsiones intermitentes.
</details>

---

**Pregunta 11. [Multiple Choice — Single Answer]**

¿En qué capa del modelo OSI opera un switch para reenviar datos?

A) Capa 1 — Physical

B) Capa 2 — Data Link

C) Capa 3 — Network

D) Capa 4 — Transport

<details>
<summary>Respuesta</summary>
✅ Correcta: B) Capa 2 — Data Link

💡 Explicación: Un switch reenvía tramas (frames) basándose en direcciones MAC, que corresponden a la capa 2 (Data Link). Los routers operan en capa 3 (Network) usando direcciones IP. La capa 1 maneja señales físicas y la capa 4 gestiona la comunicación extremo a extremo.
</details>

---

**Pregunta 12. [Multiple Choice — Choose Two]**

¿Cuáles de los siguientes protocolos utilizan TCP como protocolo de transporte? (Elige dos)

A) DHCP

B) SFTP

C) TFTP

D) HTTPS

<details>
<summary>Respuesta</summary>
✅ Correcta: B) SFTP y D) HTTPS

💡 Explicación: SFTP (puerto 22) y HTTPS (puerto 443) utilizan TCP porque requieren entrega fiable de datos. DHCP usa UDP en los puertos 67/68 porque funciona por broadcast, y TFTP usa UDP en el puerto 69 porque es un protocolo trivial sin garantías de entrega.
</details>

---

**Pregunta 13. [Multiple Choice — Single Answer]**

Durante el proceso de encapsulación, ¿qué unidad de datos se crea cuando el protocolo IP añade las direcciones IP origen y destino al segmento de la capa de transporte?

A) Trama (frame)

B) Bits

C) Paquete (packet)

D) Datos de aplicación

<details>
<summary>Respuesta</summary>
✅ Correcta: C) Paquete (packet)

💡 Explicación: Cuando la capa de red (IP) encapsula el segmento añadiendo direcciones IP origen y destino, el resultado es un paquete (packet). El orden de encapsulación es: Datos → Segmento (capa 4) → Paquete (capa 3) → Trama (capa 2) → Bits (capa 1).
</details>

---

**Pregunta 14. [Drag and Drop]**

Arrastra cada paso del proceso DHCP a su posición correcta en la secuencia (del 1 al 4).

**Elementos a arrastrar:**
- Acknowledge
- Discover
- Offer
- Request

**Posiciones destino:**
- Paso 1
- Paso 2
- Paso 3
- Paso 4

<details>
<summary>Respuesta</summary>
✅ Correcta:

- Paso 1 → Discover

- Paso 2 → Offer

- Paso 3 → Request

- Paso 4 → Acknowledge

💡 Explicación: DORA: (1) Discover — el cliente envía un broadcast buscando servidor DHCP; (2) Offer — el servidor ofrece una IP disponible; (3) Request — el cliente acepta la oferta por broadcast; (4) Acknowledge — el servidor confirma la asignación con IP, máscara, gateway, DNS y lease time.
</details>

---

**Pregunta 15. [Multiple Choice — Single Answer]**

¿Qué protocolo es la base de las herramientas `ping` y `traceroute` y opera directamente sobre IP sin usar TCP ni UDP?

A) DNS

B) NTP

C) ICMP

D) SNMP

<details>
<summary>Respuesta</summary>
✅ Correcta: C) ICMP

💡 Explicación: ICMP (Internet Control Message Protocol) es un protocolo de capa 3 que opera directamente sobre IP. Es la base de ping (usa mensajes echo request/reply) y traceroute (usa mensajes TTL expired). DNS usa UDP/TCP, NTP usa UDP, y SNMP no aparece en este contexto.
</details>

---

**Pregunta 16. [Multiple Choice — Single Answer]**

Una startup necesita que sus desarrolladores creen y desplieguen una aplicación web sin preocuparse de gestionar servidores, sistemas operativos ni bases de datos. ¿Qué modelo de servicio cloud es el más adecuado?

A) SaaS

B) PaaS

C) IaaS

D) Private cloud

<details>
<summary>Respuesta</summary>
✅ Correcta: B) PaaS

💡 Explicación: PaaS (Platform as a Service) proporciona infraestructura más bases de datos, librerías y herramientas de desarrollo; el usuario solo necesita desarrollar y desplegar aplicaciones (por ejemplo, Google App Engine, Heroku). SaaS ofrece la app completa ya hecha, IaaS solo ofrece infraestructura base, y private cloud es un modelo de propiedad, no de servicio.
</details>

---

**Pregunta 17. [Multiple Choice — Single Answer]**

¿Qué topología de red conecta cada host a un dispositivo central como un switch, de modo que un fallo en un cable afecta solo al host conectado por ese cable?

A) Bus

B) Ring

C) Star

D) Mesh

<details>
<summary>Respuesta</summary>
✅ Correcta: C) Star

💡 Explicación: En la topología star (estrella), cada host conecta individualmente a un dispositivo central (switch/router). Un fallo de cable afecta solo a ese host. Su desventaja es el punto único de fallo en el dispositivo central. Es la topología más utilizada en LANs actuales.
</details>

---

**Pregunta 18. [Hotspot]**

Host A genera datos y los envía a un Dispositivo X, que los reenvía examinando direcciones MAC. Desde allí, los datos llegan a un Dispositivo Y, que examina las direcciones IP, descarta la trama, crea una nueva con nuevas MACs y reenvía el paquete. Finalmente los datos llegan al Host B.

**¿Qué tipo de dispositivo es el Dispositivo Y?**

A) Hub

B) Switch

C) Router

D) Access Point

<details>
<summary>Respuesta</summary>
✅ Correcta: C) Router

💡 Explicación: El Dispositivo Y examina direcciones IP (capa 3), descarta la trama de capa 2 y crea una nueva con nuevas direcciones MAC del siguiente salto — este comportamiento es exclusivo de un router. El Dispositivo X, que reenvía basándose en MACs, es un switch. Un hub simplemente reenvía todo sin examinar direcciones, y un access point proporciona conectividad inalámbrica.
</details>

---

**Pregunta 19. [Multiple Choice — Choose Two]**

¿Cuáles de las siguientes topologías se utilizan frecuentemente en redes WAN? (Elige dos)

A) Bus

B) Ring

C) Hub-and-spoke

D) Star directa con un solo switch

<details>
<summary>Respuesta</summary>
✅ Correcta: B) Ring y C) Hub-and-spoke

💡 Explicación: En WANs se usan frecuentemente las topologías ring (anillo, cada nodo conecta al siguiente formando un circuito cerrado con redundancia) y hub-and-spoke (un nodo central conecta a múltiples spoke, en versión single-homed o dual-homed). La topología bus ya no se usa en despliegues reales, y star con un solo switch es típica de LANs, no de WANs.
</details>

---

**Pregunta 20. [Multiple Choice — Single Answer]**

¿Qué tipo de registro DNS se utiliza para traducir un nombre de dominio a una dirección IPv6?

A) A

B) AAAA

C) MX

D) CNAME

<details>
<summary>Respuesta</summary>
✅ Correcta: B) AAAA

💡 Explicación: El registro AAAA traduce un nombre de dominio a una dirección IPv6. El registro A traduce a IPv4. MX identifica servidores de correo del dominio y CNAME crea un alias (nombre alternativo) para otro nombre de dominio.
</details>

---

**Pregunta 21. [Multiple Choice — Single Answer]**

En la jerarquía de resolución DNS, ¿qué servidor es el primero al que el host envía su consulta y que se encarga de recorrer la cadena completa si no tiene la respuesta en caché?

A) Root server

B) TLD server

C) Authoritative server

D) Recursive server

<details>
<summary>Respuesta</summary>
✅ Correcta: D) Recursive server

💡 Explicación: El host envía su consulta al servidor recursive (configurado normalmente por DHCP). Si no tiene la respuesta en caché, este servidor consulta secuencialmente al root server, al TLD server y al authoritative server hasta obtener la IP final. Los otros tres tipos no reciben consultas directas del host.
</details>

---

**Pregunta 22. [Multiple Choice — Single Answer]**

Un enlace de red tiene un bandwidth de 1 Gbps. Un administrador observa que el throughput medido es de 750 Mbps y el goodput es de 700 Mbps. ¿Cuál de las siguientes afirmaciones es correcta?

A) El enlace tiene un problema porque el throughput debería igualar al bandwidth

B) Es un comportamiento normal

C) El goodput debería ser mayor que el throughput porque solo cuenta los datos útiles

D) Los 50 Mbps de diferencia entre throughput y goodput representan el propagation delay

<details>
<summary>Respuesta</summary>
✅ Correcta: B) Es un comportamiento normal: el throughput siempre es menor que el bandwidth, y el goodput siempre es menor que el throughput

💡 Explicación: La relación correcta es siempre: bandwidth > throughput > goodput. El throughput es menor que el bandwidth por overhead de protocolos, encapsulación y margen operativo. El goodput es menor que el throughput porque excluye cabeceras y retransmisiones, contando solo los datos útiles entregados sin error. La diferencia no es un "delay" sino overhead de protocolo.
</details>

---

**Pregunta 23. [Drag and Drop]**

Arrastra cada modelo de servicio cloud a su ejemplo correcto.

**Elementos a arrastrar:**
- IaaS
- PaaS
- SaaS

**Categorías destino:**
- AWS EC2, Azure VMs
- Google App Engine, Heroku
- Gmail, Salesforce, Office 365

<details>
<summary>Respuesta</summary>
✅ Correcta:

- IaaS → AWS EC2, Azure VMs

- PaaS → Google App Engine, Heroku

- SaaS → Gmail, Salesforce, Office 365

💡 Explicación: IaaS proporciona infraestructura base (máquinas virtuales como EC2). PaaS añade plataforma de desarrollo (App Engine, Heroku). SaaS entrega la aplicación completa lista para usar (Gmail, Salesforce). Cada nivel añade mayor abstracción: IaaS < PaaS < SaaS.
</details>

---

**Pregunta 24. [Multiple Choice — Single Answer]**

¿Cuál es la principal desventaja de la topología ring en una WAN?

A) Requiere un dispositivo central que puede ser punto único de fallo

B) Cada nodo añade delay y el bandwidth disponible se reparte entre los nodos

C) Un fallo en el cable compartido afecta a todos los hosts de la red

D) No soporta más de dos hosts conectados simultáneamente

<details>
<summary>Respuesta</summary>
✅ Correcta: B) Cada nodo añade delay y el bandwidth disponible se reparte entre los nodos

💡 Explicación: En una topología ring, los datos pasan secuencialmente por cada nodo, lo que añade delay acumulativo, y el bandwidth se comparte entre todos los nodos del anillo. La opción A describe la desventaja de star/hub-and-spoke, la C describe bus, y la D es falsa.
</details>

---

**Pregunta 25. [Multiple Choice — Choose Two]**

¿Cuáles de los siguientes son factores clave que una organización debe considerar al elegir entre cloud público y privado? (Elige dos)

A) El número de capas del modelo OSI que utiliza la aplicación

B) La propiedad de los datos y las preocupaciones de seguridad

C) Los patrones de acceso y la conectividad a Internet disponible

D) La versión del protocolo TCP utilizada por el proveedor cloud

<details>
<summary>Respuesta</summary>
✅ Correcta: B) y C)

💡 Explicación: Los factores para elegir entre cloud público y privado incluyen: propiedad de los datos, patrones de acceso, conectividad a Internet disponible, cultura corporativa y preocupaciones de seguridad. El número de capas OSI y la versión de TCP son irrelevantes para esta decisión empresarial.
</details>

---

**Pregunta 26. [Multiple Choice — Single Answer]**

¿Qué dispositivos se encuentran en el nivel stratum 0 de la jerarquía NTP?

A) Servidores NTP corporativos conectados a Internet

B) Routers de borde que distribuyen tiempo a la LAN

C) Relojes atómicos y dispositivos GPS de alta precisión

D) Clientes NTP que sincronizan su reloj por primera vez

<details>
<summary>Respuesta</summary>
✅ Correcta: C) Relojes atómicos y dispositivos GPS de alta precisión

💡 Explicación: En la jerarquía NTP, stratum 0 son dispositivos de referencia de alta precisión (relojes atómicos, GPS). Stratum 1 son servidores conectados directamente a ellos, y cada nivel adicional (stratum 2, 3...) está un salto más lejos de la fuente de tiempo original. Los servidores corporativos y routers operan en stratums superiores.
</details>

---

**Pregunta 27. [Multiple Choice — Choose Two]**

¿Cuáles de las siguientes son características exclusivas de TCP que no posee UDP? (Elige dos)

A) Establecimiento de conexión mediante three-way handshake

B) Cabecera de solo 8 bytes para minimizar el overhead

C) Control de flujo mediante ventana deslizante (windowed flow control)

D) Capacidad de transportar consultas DNS y tráfico de streaming

<details>
<summary>Respuesta</summary>
✅ Correcta: A) y C)

💡 Explicación: TCP se distingue de UDP por ser connection-oriented con three-way handshake (SYN → SYN-ACK → ACK) y por implementar windowed flow control (el emisor envía un número limitado de bytes antes de esperar confirmación). La cabecera de 8 bytes (B) es característica de UDP, no de TCP. Y tanto TCP como UDP pueden transportar DNS (D), por lo que no es exclusivo de ninguno.
</details>

---

**Pregunta 28. [Hotspot]**

Se muestra un camino de red entre Host A y Host B con los siguientes enlaces y velocidades:
- Host A → Switch 1: **1 Gbps**
- Switch 1 → Router 1: **100 Mbps**
- Router 1 → Router 2: **1 Gbps**
- Router 2 → Switch 2: **500 Mbps**
- Switch 2 → Host B: **1 Gbps**

**Señala el enlace que determina el throughput máximo de extremo a extremo entre Host A y Host B.**

A) Host A → Switch 1 (1 Gbps)

B) Switch 1 → Router 1 (100 Mbps)

C) Router 1 → Router 2 (1 Gbps)

D) Router 2 → Switch 2 (500 Mbps)

<details>
<summary>Respuesta</summary>
✅ Correcta: B) Switch 1 → Router 1 (100 Mbps)

💡 Explicación: El bandwidth del camino viene determinado por el enlace más lento de toda la ruta, que actúa como cuello de botella. De los cinco enlaces, Switch 1 → Router 1 con 100 Mbps es el más lento, por lo que limita el throughput máximo de extremo a extremo independientemente de la velocidad de los demás enlaces.
</details>

---

**Pregunta 29. [Multiple Choice — Choose Two]**

¿Cuáles de las siguientes afirmaciones describen correctamente cómo los proveedores cloud organizan su infraestructura para garantizar resiliencia? (Elige dos)

A) Organizan la infraestructura en regiones, que son áreas geográficas independientes

B) Utilizan un único data center centralizado para minimizar la latencia de todos los clientes

C) Dentro de cada región, crean zonas de disponibilidad con fuentes de energía y red separadas

D) Almacenan todos los datos de los clientes exclusivamente en on-premises para mayor seguridad

<details>
<summary>Respuesta</summary>
✅ Correcta: A) y C)

💡 Explicación: Los proveedores cloud organizan su infraestructura en regiones (áreas geográficas independientes) y zonas de disponibilidad (infraestructuras independientes dentro de una región con fuentes de energía y red separadas). Un único data center centralizado (B) es lo contrario de resiliencia, y almacenar datos on-premises (D) contradice el modelo cloud.
</details>

---

**Pregunta 30. [Drag and Drop]**

Arrastra cada tipo de red al alcance geográfico que le corresponde.

**Elementos a arrastrar:**
- PAN
- LAN
- MAN
- WAN

**Categorías destino:**
- Alrededor de una persona (Bluetooth, ZWave)
- Edificio o campus (Ethernet, Wi-Fi)
- Ciudad o área metropolitana (fibra, tecnología óptica)
- País, continente o global (fibra submarina, MPLS)

<details>
<summary>Respuesta</summary>
✅ Correcta:

- PAN → Alrededor de una persona (Bluetooth, ZWave)

- LAN → Edificio o campus (Ethernet, Wi-Fi)

- MAN → Ciudad o área metropolitana (fibra, tecnología óptica)

- WAN → País, continente o global (fibra submarina, MPLS)

💡 Explicación: Las redes se clasifican por alcance geográfico creciente: PAN (personal), LAN (edificio/campus), MAN (metropolitana), WAN (global). Cada tipo utiliza tecnologías adaptadas a su escala, desde Bluetooth para PAN hasta fibra submarina y MPLS para WAN.
</details>

---

✅ 30 preguntas del Dominio 1 completadas.

📊 **Desglose por objetivo:**

| Objetivo | Tema | Preguntas | Total |
|----------|------|-----------|:-----:|
| **1.1** | Modelos OSI/TCP-IP, tramas, paquetes, encapsulación | 1, 5, 9, 11, 13, 18, 27 | **7** |
| **1.2** | Bandwidth, throughput, latencia, delay, jitter, speed test, iPerf | 2, 6, 10, 22, 28 | **5** |
| **1.3** | LAN, WAN, MAN, CAN, PAN, WLAN, topologías | 3, 17, 19, 24, 30 | **5** |
| **1.4** | Cloud vs. on-premises: SaaS, PaaS, IaaS, trabajo remoto | 4, 16, 23, 25, 29 | **5** |
| **1.5** | TCP, UDP, FTP, SFTP, TFTP, HTTP, HTTPS, DHCP, DNS, ICMP, NTP | 7, 8, 12, 14, 15, 20, 21, 26 | **8** |
| | | **TOTAL** | **30** |

📋 **Desglose por tipo de pregunta:**

| Tipo | Cantidad | Preguntas |
|------|:--------:|-----------|
| Multiple Choice (1 respuesta) | **18** | 1, 2, 3, 4, 5, 7, 9, 10, 11, 13, 15, 16, 17, 20, 21, 22, 24, 26 |
| Multiple Choice (Choose Two) | **6** | 6, 12, 19, 25, 27, 29 |
| Drag and Drop | **4** | 8, 14, 23, 30 |
| Hotspot | **2** | 18, 28 |

🎯 **Desglose por dificultad:**

| Nivel | Cantidad | Preguntas |
|-------|:--------:|-----------|
| Fácil (40%) | **12** | 1, 3, 4, 7, 8, 11, 13, 15, 17, 20, 23, 26 |
| Medio (40%) | **12** | 2, 5, 6, 9, 10, 12, 14, 16, 19, 21, 24, 30 |
| Difícil (20%) | **6** | 18, 22, 25, 27, 28, 29 |
