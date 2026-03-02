# Dominio 1: Standards and Concepts

## Resumen ejecutivo

Este dominio cubre los fundamentos teóricos sobre los que se construye todo el networking: modelos de red (OSI y TCP/IP), la diferencia entre bandwidth y throughput, los tipos de redes por alcance geográfico, el paradigma cloud versus on-premises, y los protocolos esenciales de la pila TCP/IP. Es el dominio más conceptual del examen y sirve de base para comprender los cinco restantes.

---

## Conceptos clave

### 1.1 — Bloques fundamentales de las redes

#### Modelo OSI (7 capas)

🔑 *Analogía:* Como el sistema postal — cada capa añade un sobre con instrucciones específicas (remitente, destino, tipo de envío) antes de entregar el paquete a la siguiente oficina.

El modelo OSI fue propuesto en 1978 por la ISO como un marco de referencia de siete capas para describir cómo los protocolos transportan datos de un host a otro. Las capas, de abajo a arriba, son:

| Capa | Nombre | Función principal | Unidad de datos | Ejemplo |
|------|--------|-------------------|-----------------|---------|
| 7 | Application | Interfaz con el usuario/aplicación | Datos | HTTP, FTP, DNS |
| 6 | Presentation | Formato y cifrado de datos | Datos | SSL/TLS, JPEG |
| 5 | Session | Gestión de sesiones | Datos | NetBIOS |
| 4 | Transport | Entrega fiable o no fiable extremo a extremo | Segmento | TCP, UDP |
| 3 | Network | Direccionamiento lógico y enrutamiento | Paquete (packet) | IP, ICMP |
| 2 | Data Link | Direccionamiento físico y acceso al medio | Trama (frame) | Ethernet, Wi-Fi |
| 1 | Physical | Señales eléctricas/ópticas/radio | Bits | Cables, conectores |

**Mapeo simplificado con protocolos IP** (el que se usa en la práctica):

- **Capa 1** → Señalización física (cobre, fibra, wireless).
- **Capa 2** → Direcciones MAC, switches, protocolos de enlace.
- **Capa 3** → IP, direcciones IP, routers.
- **Capa 4** → TCP, UDP, QUIC.
- **Capas 5-7** → Se agrupan en el espacio de aplicación.

**Proceso de encapsulación paso a paso** (según el libro):

1. La aplicación envía un bloque de datos al protocolo de transporte a través de un socket.
2. El protocolo de transporte encapsula los datos en un **segmento**.
3. El protocolo de red (IP) encapsula el segmento en un **paquete**, añadiendo direcciones IP origen y destino.
4. La interfaz física encapsula el paquete en una **trama**, añadiendo direcciones MAC origen y destino, y transmite la trama al medio.
5. Un **switch** reenvía la trama basándose en la dirección MAC.
6. Un **router** elimina la encapsulación de capa 2, examina el paquete, determina la interfaz de salida y reencapsula el paquete en una nueva trama con nuevas direcciones MAC.
7. El host destino deshace todas las capas de encapsulación hasta entregar los datos a la aplicación correcta (identificada por el número de puerto).

#### Modelo TCP/IP (DoD) — 4 capas

| Capa TCP/IP | Equivalencia OSI | Protocolos clave |
|-------------|------------------|------------------|
| Application | Capas 5, 6, 7 | HTTP, FTP, DNS, DHCP, SSH |
| Transport | Capa 4 | TCP, UDP |
| Internet | Capa 3 | IPv4, IPv6, ICMP |
| Network Interface | Capas 1 y 2 | Ethernet, Wi-Fi |

El modelo TCP/IP es menos específico que el OSI pero más práctico: fue desarrollado antes que el OSI y refleja directamente cómo funciona la suite de protocolos IP.

#### Frames vs. Packets

| Concepto | Capa | Dirección que usa | Dispositivo que lo procesa |
|----------|------|-------------------|---------------------------|
| **Frame** (trama) | Capa 2 (Data Link) | Dirección MAC | Switch |
| **Packet** (paquete) | Capa 3 (Network) | Dirección IP | Router |

Un frame envuelve un packet. Cada vez que un paquete cruza un router, la trama se descarta y se crea una nueva con las direcciones MAC del siguiente salto, pero el paquete interior permanece intacto.

---

### 1.2 — Bandwidth vs. Throughput

🔑 *Analogía:* El bandwidth es el número de carriles de una autopista; el throughput es cuántos coches realmente circulan por ella en un momento dado.

| Concepto | Definición |
|----------|------------|
| **Bandwidth** | Capacidad máxima teórica de un enlace (ej: 1 Gbps). |
| **Throughput** | Cantidad de datos que realmente se transfieren en condiciones reales. Siempre menor que el bandwidth. |
| **Goodput** | Datos útiles entregados sin error. Siempre menor que el throughput (debido a headers y retransmisiones). |

**¿Por qué el throughput es siempre menor que el bandwidth?**

1. Los protocolos de control (routing, etc.) consumen parte del ancho de banda.
2. Hay overhead por tamaños mínimos de trama y encapsulación (cabeceras IPv6 ≈ 40 bytes, Ethernet ≈ 20 bytes).
3. Se necesita margen para absorber picos de tráfico. La mayoría de operadores consideran un enlace "lleno" al **80%** de utilización.

**Bandwidth del enlace vs. bandwidth del camino:** La velocidad máxima entre dos puntos viene determinada por el enlace más lento de toda la ruta (el cuello de botella).

#### Latency (Delay)

El delay es el tiempo que tarda un paquete en ir del emisor al receptor. Tiene tres componentes principales:

1. **Distancia física (propagation delay):** Las señales viajan más rápido por fibra que por cobre, y más rápido por cable que por satélite.
2. **Serialization delay:** Tiempo necesario para "clockear" los bits del paquete al medio. A mayor bandwidth, menor serialization delay.
3. **Queueing delay:** Cuando llega más tráfico del que la interfaz de salida puede transmitir, los paquetes esperan en cola. Si la cola se llena, se descartan paquetes.

#### Jitter

Variación del delay entre paquetes consecutivos. Es especialmente dañino para aplicaciones de streaming y VoIP porque produce interrupciones. Las aplicaciones usan buffers para compensar el jitter, pero los buffers añaden delay adicional.

#### Speed Test vs. iPerf

| Herramienta | Qué mide | Cuándo usarla |
|-------------|----------|---------------|
| **Speed test** (ej: Ookla) | Rendimiento de tu conexión a Internet y del proveedor local | Verificar que el ISP entrega el servicio contratado |
| **iPerf** | Rendimiento entre dos puntos cualesquiera (LAN o Internet) | Medir rendimiento de la red local o entre sitios específicos |

iPerf requiere instalar un servidor (`iperf3 -s`) y un cliente (`iperf3 -c <IP>`). Envía 10 bloques de datos por TCP y reporta throughput del emisor y receptor.

---

### 1.3 — Tipos de redes y topologías

🔑 *Analogía:* Las redes se clasifican por alcance como las carreteras: senderos personales (PAN), calles urbanas (LAN), carreteras comarcales (CAN/MAN) y autopistas nacionales (WAN).

#### Tipos de red por alcance

| Tipo | Alcance | Tecnología típica | Ejemplo |
|------|---------|-------------------|---------|
| **PAN** (Personal Area Network) | Alrededor de una persona | Bluetooth, ZWave | Smartwatch ↔ teléfono |
| **LAN** (Local Area Network) | Edificio / campus | Ethernet, Wi-Fi | Red de oficina |
| **WLAN** (Wireless LAN) | Edificio / campus (inalámbrico) | Wi-Fi (802.11) | Red Wi-Fi corporativa |
| **CAN** (Car Area Network) | Un vehículo | Protocolos CAN bus, wired/wireless | Sensores de un coche |
| **MAN** (Metropolitan Area Network) | Ciudad / área metropolitana | Fibra, tecnología óptica | Red metropolitana de un ISP |
| **WAN** (Wide Area Network) | País / continente / global | Fibra submarina, MPLS, Internet | Red corporativa entre sedes |

#### Topologías físicas

| Topología | Descripción | Ventaja | Desventaja |
|-----------|-------------|---------|------------|
| **Bus** | Todos los hosts comparten un único cable coaxial | Simple y barata | Un fallo en el cable afecta a todos. Ya no se usa. |
| **Star** (Estrella) | Cada host conecta a un dispositivo central (switch/router) | Fácil gestión; un fallo de cable afecta solo a un host | Punto único de fallo en el dispositivo central |
| **Ring** (Anillo) | Cada nodo conecta al siguiente formando un circuito cerrado | Dos caminos posibles (redundancia si es dual); pocas interfaces por nodo | Cada nodo añade delay; el bandwidth disponible se reparte |
| **Hub-and-spoke** | Un nodo central conecta a múltiples nodos "spoke" | Soporta muchos endpoints con cableado mínimo | Single-homed = punto único de fallo; dual-homed = más complejo |

Las topologías **star** y **hub-and-spoke** son las más relevantes hoy en día. La topología bus ya no se usa en despliegues reales. En WANs, se usan frecuentemente topologías **ring** y **hub-and-spoke** (simple o dual-homed).

---

### 1.4 — Cloud vs. On-Premises

🔑 *Analogía:* On-premises es como tener tu propia cocina en casa; cloud público es como comer en un restaurante — no te preocupas de la infraestructura, pero tampoco la controlas.

#### Quién es dueño de los recursos

| Modelo | Propiedad | Ubicación |
|--------|-----------|-----------|
| **Public cloud** | El proveedor cloud posee y opera la infraestructura | Data centers del proveedor |
| **Private cloud** | La organización posee y opera los recursos | On-premises o en colocación |
| **Hybrid cloud** | Mezcla de servicios públicos y privados | Ambas ubicaciones |
| **Multi-cloud** | Uso de más de un proveedor cloud público | Múltiples proveedores |
| **On-premises** | El equipamiento está físicamente en las instalaciones del usuario | Instalaciones propias |

#### Modelos de servicio (aaS)

| Modelo | Qué proporciona el proveedor | Qué gestiona el usuario | Ejemplo |
|--------|------------------------------|-------------------------|---------|
| **IaaS** (Infrastructure as a Service) | Servidores, red, conectividad a Internet | Instalar apps, construir topologías virtuales | AWS EC2, Azure VMs |
| **PaaS** (Platform as a Service) | Todo lo de IaaS + bases de datos, librerías, herramientas de desarrollo | Desarrollar y desplegar aplicaciones | Google App Engine, Heroku |
| **SaaS** (Software as a Service) | Aplicación completa accesible vía web | Simplemente usar la aplicación | Salesforce, Gmail, Office 365 |

**Resiliencia cloud:** Los proveedores organizan su infraestructura en **regiones** (áreas geográficas independientes) y **zonas de disponibilidad** (infraestructuras independientes dentro de una región con fuentes de energía y red separadas).

**Conectividad al cloud:** Las dos formas principales son **VPN** (enlace virtual cifrado sobre Internet) y **conexión directa** (circuito dedicado entre el cliente y el proveedor).

**Factores para elegir público vs. privado:** Propiedad de los datos, patrones de acceso, conectividad a Internet disponible, cultura corporativa y preocupaciones de seguridad. No hay una respuesta única; depende del caso de uso.

**Remote/hybrid work:** El cloud facilita el trabajo remoto e híbrido porque los servicios son accesibles desde cualquier ubicación con conexión a Internet, sin necesidad de estar en la red corporativa física (aunque a menudo se usa VPN para mayor seguridad).

---

### 1.5 — Protocolos y aplicaciones de red comunes

🔑 *Analogía:* Los protocolos son como los idiomas del networking — TCP es una conversación formal con acuse de recibo, UDP es gritar un mensaje y seguir andando.

#### TCP vs. UDP

| Característica | TCP | UDP |
|---------------|-----|-----|
| Tipo | **Connection-oriented** | **Connectionless** |
| Fiabilidad | Entrega garantizada, en orden | Sin garantía de entrega ni orden |
| Control de flujo | Sí (ventana deslizante) | No |
| Control de errores | Sí (retransmisión) | No (solo checksum opcional) |
| Establecimiento | Three-way handshake (SYN → SYN-ACK → ACK) | No requiere conexión previa |
| Overhead | Mayor (cabecera más grande) | Menor (cabecera de solo 8 bytes) |
| Uso típico | Web (HTTP/HTTPS), email, transferencia de ficheros | DNS, streaming de voz/vídeo, broadcast/multicast |

**TCP three-way handshake:**
1. El cliente envía un **SYN** con un número de secuencia inicial.
2. El servidor responde con un **SYN-ACK** (confirma y envía su propio SYN).
3. El cliente completa con un **ACK**. La conexión queda establecida.

TCP usa **windowed flow control**: el emisor puede enviar un número limitado de bytes (ventana) antes de esperar confirmación. Si el receptor detecta un paquete perdido (hueco en números de secuencia), solicita retransmisión.

#### Tabla de protocolos clave

| Protocolo | Puerto(s) | Transporte | Función |
|-----------|-----------|------------|---------|
| **FTP** | 20 (datos), 21 (control) | TCP | Transferencia de archivos. Usa dos conexiones separadas (control + datos). No cifrado → obsoleto. |
| **SFTP** | 22 | TCP | Transferencia segura de archivos basada en SSH. Reemplaza a FTP. |
| **TFTP** | 69 | UDP | Transferencia trivial: sin autenticación, sin cifrado, sin corrección de errores. Usado para cargar configuraciones en dispositivos de red. |
| **HTTP** | 80 | TCP | Transporte de páginas web (HTML, imágenes, vídeos). Métodos clave: GET, HEAD, POST. |
| **HTTPS** | 443 | TCP | HTTP + cifrado TLS. Estándar actual para todo el tráfico web. |
| **DNS** | 53 | UDP (consultas) / TCP (transferencias de zona) | Traduce nombres de dominio a direcciones IP. Sistema jerárquico: root servers → TLD servers → authoritative servers. |
| **DHCP** | 67 (servidor), 68 (cliente) | UDP | Asignación automática de IP, máscara, gateway y DNS a los hosts. Proceso: **Discover → Offer → Request → Acknowledge**. |
| **ICMP** | N/A (protocolo de capa 3) | IP directo | Mensajes de control y error. Base de `ping` (echo request/reply) y `traceroute` (TTL expired). |
| **NTP** | 123 | UDP | Sincronización de reloj entre dispositivos de red. Arquitectura de stratums: stratum 0 (reloj atómico/GPS) → stratum 1 → stratum 2... |

#### DHCP en detalle

El proceso DHCP para IPv4 sigue cuatro pasos (conocido como **DORA**):

1. **Discover:** El cliente envía un broadcast buscando un servidor DHCP.
2. **Offer:** El servidor DHCP responde con una dirección IP disponible.
3. **Request:** El cliente acepta la oferta y lo confirma por broadcast.
4. **Acknowledge:** El servidor confirma la asignación, incluyendo máscara de subred, default gateway, servidores DNS y **lease time** (tiempo de alquiler de la dirección).

#### DNS en detalle

El DNS es un sistema jerárquico distribuido. Los nombres se procesan de derecha a izquierda (de menos específico a más específico): `.com` → `example` → `www`.

Tipos de registros DNS clave: **A** (IPv4), **AAAA** (IPv6), **MX** (servidores de correo), **CNAME** (alias), **SOA** (autoridad de zona).

Tipos de servidores DNS: **recursive** (el que consulta el host), **root** (devuelve el TLD server correcto), **TLD** (devuelve el authoritative server), **authoritative** (devuelve la dirección IP final).

#### NTP en detalle

NTP sincroniza los relojes de red con precisión de milisegundos. Funciona con un modelo **cliente/servidor** jerárquico basado en **stratums**: stratum 0 son dispositivos de alta precisión (relojes atómicos, GPS), stratum 1 son servidores conectados directamente a ellos, y cada nivel adicional está un salto más lejos de la fuente de tiempo.

---

## 🎯 Puntos críticos para el examen

- **Capas OSI:** Memorizar las 7 capas en orden (Physical, Data Link, Network, Transport, Session, Presentation, Application). Saber que los switches operan en capa 2 (frames/MACs) y los routers en capa 3 (packets/IPs).
- **Encapsulación:** Datos → Segmento (capa 4) → Paquete (capa 3) → Trama (capa 2) → Bits (capa 1). El proceso inverso es la **desencapsulación**.
- **TCP vs. UDP:** TCP es connection-oriented con three-way handshake y garantía de entrega; UDP es connectionless, más rápido pero sin garantías. Saber qué protocolos usan cada uno.
- **Bandwidth ≠ Throughput:** Bandwidth es teórico/máximo; throughput es real y siempre menor. Goodput es aún menor (solo datos útiles sin errores).
- **DHCP = DORA:** Discover → Offer → Request → Acknowledge. Funciona por broadcast en UDP.
- **DNS jerárquico:** Host → Recursive server → Root server → TLD server → Authoritative server → Respuesta IP.
- **Speed test vs. iPerf:** Speed test mide tu conexión al ISP; iPerf puede medir cualquier segmento de red (incluyendo la LAN local).
- **Cloud: IaaS < PaaS < SaaS** (de menor a mayor nivel de abstracción). Public = infraestructura ajena; Private = infraestructura propia; Hybrid = mezcla de ambas.

---

## Mini-resumen

- El **modelo OSI** tiene 7 capas; el **modelo TCP/IP** tiene 4. En la práctica, los protocolos IP se mapean a 4 capas del OSI: physical, data link, network y transport.
- **Bandwidth** es la capacidad máxima teórica; **throughput** es lo que realmente se transfiere; los tres componentes del delay son distancia física, serialization delay y queueing.
- Las redes se clasifican por alcance: **PAN < LAN/WLAN < CAN < MAN < WAN**. Las topologías más relevantes hoy son **star** (LAN) y **hub-and-spoke/ring** (WAN).
- En cloud, **IaaS** ofrece infraestructura, **PaaS** añade plataforma de desarrollo, y **SaaS** entrega la aplicación completa. La elección entre público y privado depende de seguridad, costes y cultura corporativa.
- **TCP** (fiable, orientado a conexión) y **UDP** (rápido, sin conexión) son los dos transportes fundamentales. Los protocolos de aplicación clave son: FTP/SFTP/TFTP (ficheros), HTTP/HTTPS (web), DNS (nombres), DHCP (asignación IP), ICMP (diagnóstico), NTP (tiempo).

---

✅ Dominio 1 completado. Listo para continuar con el Dominio 2.
