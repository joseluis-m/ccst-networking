# Dominio 5: Diagnosing Problems

## Resumen ejecutivo

Este dominio es el más orientado a la práctica operativa del examen: cubre desde las metodologías formales de resolución de problemas y las mejores prácticas de help desk, hasta el uso de herramientas de diagnóstico (ping, traceroute, Wireshark), los métodos de acceso remoto a dispositivos de red (SSH, Telnet, consola, VPN, NMS) y los comandos `show` fundamentales de Cisco IOS. Es un dominio donde el examen pide tanto conocimiento conceptual (cuándo y por qué usar cada herramienta) como reconocimiento práctico de salidas de comandos. Presta especial atención a la tabla de comandos `show` y sus propósitos, a la metodología half-split y al efecto de los cortafuegos sobre los resultados de diagnóstico.

---

## Conceptos clave

### 5.1 — Metodologías de troubleshooting y buenas prácticas de help desk

🔑 *Analogía:* Resolver un problema de red sin metodología es como buscar las llaves debajo de la farola porque hay luz — puedes pasarte horas mirando donde no es. El método half-split es como una búsqueda binaria: cada medición reduce el espacio del problema a la mitad.

#### Documentación de red

Existen cinco tipos fundamentales de documentación de red. Sin ella, no se puede diagnosticar correctamente, porque no sabes cómo *debería* funcionar la red.

| Tipo de documentación | Contenido |
|----------------------|-----------|
| **Diagramas de red** | Físicos (cables, racks) y lógicos (IPs, flujos de tráfico) |
| **Descripciones** | Principios de diseño, aplicaciones soportadas, *intent* (intención) detrás de cada configuración, sistema de nombres, esquema de direccionamiento IP, funcionamiento de la automatización y dónde encontrar el código fuente |
| **Baselines** | Mediciones periódicas del comportamiento normal: utilización de ancho de banda, frecuencia de fallos de enlace, tiempo de convergencia, retardos. Se actualizan regularmente para detectar tendencias. |
| **Failure reports** | Informes de cada incidencia: síntomas, causa raíz, solución temporal, solución permanente. Son una mina de información para troubleshooting futuro. Deben almacenarse en un **sistema de ticketing** bien diseñado. |
| **Hardware y software** | Copias locales de manuales del fabricante y documentación crítica. Si la red cae, no podrás acceder a recursos en Internet para repararla. |

**Regla de oro:** *Si tendrías que explicar algo al soporte técnico del fabricante a las 2 de la madrugada, documéntalo.*

#### Gestión del cambio (Change Management)

Todo cambio en la red debe seguir un proceso formal que incluya: procedimientos de prueba previos, documentación del cambio (qué se resuelve, cómo, por qué), y un **backout plan** (instrucciones para restaurar rápidamente el estado previo al cambio si algo falla). Los cambios se realizan durante **change windows** (ventanas de cambio), que son cortes de servicio planificados para un módulo específico de la red.

#### Triaje y priorización

**Triaje** es el proceso de determinar la importancia relativa de cada fallo y en qué orden deben trabajarse. No todos los fallos son iguales: una red completamente caída para 10.000 dispositivos exige movilizar a todo el equipo inmediatamente; 200 hosts con rendimiento degradado pueden esperar un análisis en un par de días. El triaje es vital para organizar el trabajo diario de un **NOC (Network Operations Center)**.

#### Terminología de fallos

| Término | Significado |
|---------|-------------|
| **MTBF** (Mean Time Between Failures) | Tiempo medio entre fallos consecutivos. Se mide por tipo de fallo, por severidad y globalmente. |
| **MTBM** (Mean Time Between Mistakes) | Tiempo medio entre errores humanos. Un MTBM bajo indica un sistema frágil o excesivamente complejo. |
| **Dwell time** | Tiempo que el fallo existe antes de ser detectado. Objetivo: minimizarlo. |
| **MTTR** (Mean Time To Repair) | Tiempo total de indisponibilidad. Puede incluir o no el dwell time (depende de la política local). |
| **MTTI** (Mean Time To Innocence) | Tiempo para demostrar que el problema no es de la red. Consejo: no te centres en esto; toma ownership del problema y ayuda aunque no sea "tu culpa". |

#### Resiliencia y fragilidad

- **Sistemas frágiles** fallan fácilmente ante presiones ambientales (fallo de enlace, error humano, fallo hardware/software).
- **Sistemas resilientes** sobreviven a esas presiones gracias a la **redundancia** (caminos paralelos que eliminan **single points of failure**).
- Añadir un segundo camino aumenta la resiliencia ~50%. Un tercer camino añade ~25% adicional. Más allá de 2-3 caminos, la complejidad añadida puede empeorar la reacción ante fallos.
- **Shared fate** (destino compartido): cuando dos recursos "redundantes" comparten un componente crítico oculto (por ejemplo, ambos servidores conectados a la misma fuente de alimentación, o dos fibras del mismo cable). Es casi imposible eliminarlo completamente, pero hay que ser consciente de ello.

#### El método half-split

Es la técnica de troubleshooting más efectiva, desarrollada a partir de décadas de experiencia en electrónica. Tiene dos fases que se repiten cíclicamente:

**Fase 1 — Medir (Measure):** Orientarse al punto actual de la red y observar: ¿Cómo debería funcionar esto? ¿Qué modelo explica lo que está pasando? ¿Qué puedo medir para confirmar o descartar una hipótesis?

**Fase 2 — Dividir (Split):** Decidir hacia dónde moverse: izquierda (hacia el origen), derecha (hacia el destino), arriba (salir del módulo) o abajo (profundizar en un componente).

**Estrategia inicial recomendada:**

1. Primero, comprueba el **cambio más reciente** (la mayoría de fallos se deben a cambios).
2. Después, revisa los **puntos donde suelen ocurrir fallos**.
3. Si no se resuelve rápidamente, aplica el **half-split formal**: selecciona origen y destino, elige un punto intermedio, mide, y divide el espacio del problema en mitades sucesivas.

**Ejemplo práctico:** Host *A* no puede alcanzar el servidor *X* a través de Internet. Se empieza en el router *F* (punto medio), se hace ping a *X*. Si funciona, el problema está entre *A* y *F*. Se sigue dividiendo: access point *B*, switch *C*, host *D* como testigos. Al final se descubre que *A* puede alcanzar al router *F* pero no al firewall *G* → se orienta a la causa: ¿filtro de paquetes o default gateway incorrecto? Se valida con un ping extendido desde *F* usando la IP de su interfaz con *G*. Resultado: **default gateway de *A* mal configurado**.

#### Tipos de corrección

| Tipo | Descripción |
|------|-------------|
| **Permanent fix** | Devuelve la red al estado pre-fallo, está bien documentada, reduce la deuda técnica y encaja en la arquitectura global |
| **Temporary fix** | Solución provisional hasta que se diseñe, pruebe y despliegue una solución mejor. Aumenta la deuda técnica. |

**Consejo:** *No hay nada más permanente que una solución temporal.* No permitas que los fixes temporales se acumulen.

#### Post-mortem

Reunión tras cada incidencia para responder: ¿Cuál fue la causa raíz? ¿Cómo prevenimos que se repita? ¿Cuál fue el dwell time y cómo lo reducimos? ¿Cómo afecta esto a la arquitectura? Lo más importante: **centrarse en arreglar el problema, no en buscar culpables**.

---

### 5.2 — Captura de paquetes con Wireshark

🔑 *Analogía:* Wireshark es como una cámara de seguridad para tu red: graba todo el tráfico que pasa por una interfaz, lo decodifica fotograma a fotograma, y te permite rebobinar y analizar exactamente qué ocurrió en cada momento.

#### Propósito de un analizador de paquetes

Cuando los problemas no pueden diagnosticarse solo con ping o traceroute (por ejemplo, "la conexión es lenta pero no falla"), necesitas capturar y examinar el flujo real de paquetes. Un analizador de paquetes permite ver errores como paquetes descartados, retransmisiones TCP, handshakes incompletos y patrones anómalos de tráfico.

#### Wireshark: herramienta principal

**Wireshark** es la herramienta de captura y análisis de paquetes más utilizada en la industria de redes. Es open-source y gratuita (wireshark.org).

**Pantalla de captura — tres paneles:**

| Panel | Contenido |
|-------|-----------|
| **Superior** | Lista de paquetes capturados (resumen por línea) |
| **Inferior izquierdo** | Decodificación detallada del paquete seleccionado (Wireshark conoce miles de formatos de protocolo) |
| **Inferior derecho** | Hex dump del paquete en bruto (útil para patrones o protocolos no decodificados) |

**Funcionalidades clave:**

- **Selección de interfaz:** Al abrir Wireshark, se presenta una lista de interfaces de red desde las que se puede capturar. Se pueden seleccionar múltiples interfaces simultáneamente.
- **Filtros de captura:** Permiten capturar solo un subconjunto del tráfico (ej: solo HTTP en puerto TCP 80). Esencial para reducir el volumen de datos.
- **Análisis de flujos:** Con práctica, se pueden trazar flujos completos de paquetes y detectar errores como paquetes descartados, retransmisiones TCP, ACKs duplicados.

#### Archivos .pcap y .pcapng

Wireshark utiliza el formato **`.pcap`** o **`.pcapng`** para guardar capturas de paquetes. Este formato es estándar en la industria y es compatible con la mayoría de herramientas de captura y análisis. Puedes:

- **Guardar** una captura para examinarla después o como registro de un fallo.
- **Abrir** archivos .pcap/.pcapng existentes, incluyendo colecciones públicas de capturas (como las de netresec.com) que contienen ejemplos de operación normal de protocolos, ataques de red, malware y ejercicios de pentesting.

---

### 5.3 — Comandos de diagnóstico básicos e interpretación

🔑 *Analogía:* `ping` es como llamar a una puerta para ver si hay alguien en casa. `traceroute` es como seguir el recorrido de un paquete postal para ver por qué oficinas intermedias pasa. `nslookup` es como llamar a la operadora para preguntar el número de teléfono asociado a un nombre. `ipconfig` es como mirar tu propio DNI de red.

#### Tabla de comandos de diagnóstico por sistema operativo

| Función | **Windows** | **macOS** | **Linux** |
|---------|-------------|-----------|-----------|
| Ver configuración IP | `ipconfig /all` | `ifconfig` | `ifconfig` o `ip addr` |
| Liberar/renovar DHCP | `ipconfig /release` + `/renew` | `sudo ipconfig set en0 BOOTP` → `DHCP` | Varía por distribución |
| Limpiar caché DNS | `ipconfig /flushdns` | — | — |
| Ver direcciones MAC | `getmac /v` | `ifconfig` (campo ether) | `ifconfig` (campo ether) |
| Tabla ARP | `arp -a` | `arp -a` | `arp -a` |
| Tabla de rutas | `Get-NetRoute` (PowerShell) | `netstat -rn` | `ip route` |
| Ping | `ping` | `ping` | `ping` |
| Traceroute | `tracert` (usa ICMP) | `traceroute` (usa UDP) | `traceroute` (usa UDP) |
| Resolución DNS | `nslookup` | `nslookup` | `nslookup` |

#### ping — Verificación de conectividad

Envía paquetes **ICMP echo request** y espera **ICMP echo reply**. Verifica la conectividad IP entre origen y destino.

**Estrategia de diagnóstico escalonado con ping:**

1. `ping <default gateway>` → ¿Funciona la conectividad local?
2. `ping <IP remota conocida>` → ¿Funciona el enrutamiento?
3. `ping <nombre de dominio>` → ¿Funciona la resolución DNS?

Si el paso 1 falla, el problema es local (cable, configuración IP, interfaz). Si el paso 1 funciona pero el 2 falla, el problema es de enrutamiento. Si los pasos 1 y 2 funcionan pero el 3 falla, el problema es DNS.

**Opciones útiles de ping:** `-c` (número de paquetes), `-s` (tamaño), `-t` (TTL), `-4`/`-6` (forzar IPv4/IPv6), `-i` (seleccionar interfaz de salida).

#### traceroute / tracert — Descubrimiento de ruta

Descubre el camino que sigue un paquete hasta su destino, utilizando **TTL incremental**: envía paquetes con TTL=1 (primer router responde con ICMP TTL Expired), TTL=2 (segundo router responde), y así sucesivamente hasta alcanzar el destino.

**Diferencias entre plataformas:** Windows (`tracert`) usa ICMP echo; Linux/macOS (`traceroute`) usan UDP. Los túneles (VPN, GRE) ocultan los routers intermedios que encapsulan.

#### nslookup — Resolución DNS

Consulta un servidor DNS para obtener la dirección IP asociada a un nombre de dominio, o viceversa.

#### Efecto de los cortafuegos en los resultados

Los cortafuegos y filtros de paquetes pueden alterar significativamente los resultados de las herramientas de diagnóstico:

- **Asterisco (\*) en traceroute:** Indica que el dispositivo en ese salto está configurado para no enviar respuestas ICMP TTL Expired, o que algún dispositivo intermedio filtra/bloquea esas respuestas ICMP. No significa necesariamente que el camino esté roto.
- **Ping fallido no siempre = destino inalcanzable:** Muchos firewalls bloquean ICMP echo request/reply como medida de seguridad. Un ping fallido puede deberse al firewall, no a un problema de conectividad.
- **Filtros de paquetes en routers:** Las listas de control de acceso (ACL) pueden bloquear tráfico selectivamente por origen, destino o protocolo. Al diagnosticar un fallo de conectividad, se pueden considerar tanto los filtros de paquetes como un default gateway incorrecto como posibles causas.

**Descubrimiento de IP pública:** Dado que NAT traduce la IP privada a una pública, para conocer tu IP pública debes usar servicios web externos (Google "what is my IP", `curl http://tnx.nl/ip`, checkip.amazonaws.com).

---

### 5.4 — Formas de acceso y recolección de datos de dispositivos de red

🔑 *Analogía:* Acceder a un router es como acceder a una caja fuerte: puedes hacerlo presencialmente (consola), por teléfono seguro (SSH), por teléfono sin cifrar (Telnet), o a través de un intermediario de confianza (jump host con RDP). Un NMS es como un panel de control centralizado que monitoriza todas las cajas fuertes simultáneamente.

#### Gestión In-band vs. Out-of-band (OOB)

| Método | Descripción |
|--------|-------------|
| **In-band** | Gestión a través de las mismas interfaces que transportan tráfico de usuarios. Más económico pero si la red cae, pierdes el acceso de gestión. |
| **Out-of-band (OOB)** | Red de gestión dedicada separada, conectada a puertos de management específicos. Sigue funcionando aunque la red de producción caiga. |

#### Métodos de acceso remoto

| Método | Protocolo/Herramienta | Propósito | Seguridad |
|--------|-----------------------|-----------|-----------|
| **Console** | Puerto serie (RJ-45, USB, multi-pin) | Configuración inicial, recuperación ante fallos totales. "Plan B" si todo lo demás falla. | Físico (requiere acceso al dispositivo o terminal server) |
| **Telnet** | Protocolo TCP texto plano (puerto 23) | Acceso remoto al CLI vía IP. | **No seguro** — todo viaja sin cifrar. Solo usar para configurar SSH inicialmente y después deshabilitarlo. |
| **SSH** (Secure Shell) | Protocolo TCP cifrado (puerto 22) | Acceso remoto seguro al CLI. Sustituto de Telnet. | Cifrado de extremo a extremo. Soporta autenticación por contraseña y por par de claves SSH. PuTTY es el cliente más usado en Windows. |
| **RDP** (Remote Desktop Protocol) | Protocolo de escritorio remoto (puerto 3389) | Conectar a un jump host/servidor intermedio desde el que acceder a dispositivos de red. | Cifrado. Se usa para acceder indirectamente al router sin exponerlo a Internet. |
| **VPN** (Virtual Private Network) | IPsec, SSL | Crear un túnel cifrado sobre Internet para acceder a la red interna de la organización como si estuvieras dentro. | Cifrado. Protege contra escucha e interceptación en redes públicas (Wi-Fi). |
| **Terminal emulator** | PuTTY, SecureCRT, Terminal (macOS/Linux) | Software que establece la sesión serie (console) o SSH/Telnet con el dispositivo. Necesario tanto para acceso por console como remoto. | Depende del protocolo subyacente (SSH=seguro, Telnet=inseguro). |

**Terminal server:** Router con interfaces serie conectadas a los puertos console de múltiples dispositivos. Permite acceso remoto al console sin presencia física.

**Virtual terminal (vty lines):** Interfaces virtuales en Cisco IOS para conexiones remotas Telnet/SSH. Se configuran con `line vty 0 4`.

#### Tres reglas de seguridad para gestión remota

1. **Usar siempre SSH** para gestionar dispositivos. Deshabilitar Telnet después de configurar SSH.
2. **Controlar el acceso físico** al puerto console colocando los equipos en salas seguras.
3. **Nunca permitir conexiones de gestión desde fuera de la red.** Desde Internet, conectar primero a un jump host interno mediante RDP/SSH/VPN, y desde ahí acceder al router por SSH a la interfaz interna.

#### Network Management System (NMS)

Cuando la escala o complejidad crece, los operadores pasan de gestión manual a un **NMS** con los siguientes componentes:

- **State database:** Estado actual de cada dispositivo y salud general de la red.
- **SSOT (Single Source of Truth):** Configuración intencionada de cada dispositivo. Se compara con el estado real para detectar desviaciones.
- **Time series database:** Snapshots periódicos del estado de red e historial de eventos. Permite "rebobinar" y hacer root cause analysis.
- **Automation system:** Scripts que extraen datos del SSOT y aplican configuraciones, o que recogen estado de los dispositivos para la state database.
- **Dashboard (single pane of glass):** Vista rápida del estado de la red con alertas ante fallos, sobrecarga o indisponibilidad.

**Protocolos y métodos de recolección de datos:**

| Método | Descripción |
|--------|-------------|
| **SNMP** | Protocolo legacy para gestión de red. Formato MIB. Inseguro — muchos operadores buscan eliminarlo. |
| **NETCONF/YANG** | NETCONF transporta datos en formato YANG (markup legible por humanos y máquinas, basado en XML/tags). Moderno y preferido. |
| **CLI (scripts)** | Los scripts automatizan comandos CLI, parsean la salida y la almacenan en bases de datos o CSV. También pueden inyectar configuración al router vía CLI. |
| **Machine interface (gRPC)** | Interfaces diseñadas para automatización que acceden a datos nativos del dispositivo. |

#### Cloud-Managed Networks (Meraki)

Los fabricantes (incluido Cisco con **Meraki**) ofrecen gestión de red basada en la nube. Los dispositivos (APs, routers, switches) envían su estado y telemetría a la plataforma cloud del fabricante. La plataforma funciona como un NMS pero hospedado externamente. El tráfico de datos de los usuarios **no pasa por la nube del fabricante** — solo metadatos y estado de los dispositivos.

#### Triaje y sistema de trabajo (Ticketing)

Todo equipo de operaciones necesita un sistema para que los usuarios reporten problemas, se haga **triaje** (evaluar importancia y dificultad de reparación), y se priorice y gestione la carga de trabajo. Los failure reports alimentan este sistema de ticketing.

---

### 5.5 — Comandos `show` básicos en dispositivos Cisco

🔑 *Analogía:* Los comandos `show` son como las ventanas de inspección de una máquina industrial: cada una te muestra un aspecto diferente del funcionamiento interno sin necesidad de abrir la máquina ni modificar nada.

#### Niveles de privilegio y modos de operación

| Modo | Prompt | Nivel | Capacidad |
|------|--------|-------|-----------|
| **User EXEC** | `router>` | Nivel 1 | Solo lectura: ver información básica (versión, estado de interfaces). No se puede cambiar nada. |
| **Privileged EXEC (Enable)** | `router#` | Nivel 15 | Lectura y escritura completas. Acceso a todos los comandos `show` y a `config terminal`. |
| **Global Configuration** | `router(config)#` | — | Modificar la configuración global del dispositivo. |
| **Configuration Sub-mode** | `router(config-if)#`, `router(config-router)#`, etc. | — | Modificar configuración de interfaces, protocolos de enrutamiento, etc. `exit` sube un nivel. |

Para pasar de User EXEC a Privileged EXEC: comando `enable` (requiere la contraseña configurada con `enable secret`).

#### Help system y auto-completado

| Función | Cómo usarlo | Resultado |
|---------|-------------|-----------|
| **`?` (interrogación)** | Escribir `?` al final de un comando parcial | Muestra todas las opciones disponibles en ese punto del comando |
| **Tab (auto-complete)** | Escribir las primeras letras y pulsar Tab | Completa el comando si las letras identifican un único comando posible. Funciona con comandos multilínea: `co`+Tab → `copy`, `ru`+Tab → `running-config`, `st`+Tab → `startup-config` |

#### Running config vs. Startup config

| Configuración | Almacenamiento | Comportamiento |
|--------------|----------------|----------------|
| **Running configuration** (`show running-config`) | RAM (volátil) | Configuración activa actualmente. Se pierde al reiniciar. |
| **Startup configuration** (`show startup-config`) | NVRAM (no volátil) | Configuración que se carga al arrancar. Persiste tras reinicio. |

Los cambios desde CLI modifican solo la running config. Para que persistan: `copy running-config startup-config` (abreviado `copy run start`). ¿Por qué dos configuraciones? Protección contra errores: si te desconectas por un comando erróneo, basta con reiniciar para recuperar la configuración anterior.

#### Tabla maestra de comandos `show`

| Comando | Qué muestra | Cuándo usarlo |
|---------|-------------|---------------|
| `show running-config` | Configuración completa activa en RAM | Verificar toda la configuración actual: IPs, ACLs, rutas estáticas, hostname, protocolos |
| `show version` | Versión de IOS, modelo del router, número de serie, memoria, motivo del último reinicio (crash/manual/power cycle), tiempo de actividad | Identificar hardware/software, comprobar si hubo un crash reciente, verificar modelo y memoria |
| `show inventory` | Lista de componentes físicos: chasis, fuentes de alimentación, fan trays, módulos. Incluye PID (Product ID), VID (versión hardware) y SN (número de serie) | Identificar hardware instalado, planificar repuestos, verificar números de serie para contratos de soporte |
| `show ip interface brief` | Tabla resumen de todas las interfaces: nombre, IP asignada, estado (up/down), protocolo (up/down) | Vista rápida del estado de todas las interfaces y sus IPs. Primer comando a ejecutar para verificar configuración IP. |
| `show interfaces` | Información detallada de todas las interfaces: MAC, IP, máscara, MTU, ancho de banda, encapsulación, contadores de paquetes, errores, drops | Diagnóstico profundo: comprobar errores, drops, estado físico y lógico |
| `show interfaces <nombre>` | Lo mismo pero solo para una interfaz específica (ej: `show interfaces fastethernet1`) | Cuando necesitas detalles de una interfaz concreta |
| `show interfaces status` | Estado resumido de cada puerto del switch: nombre, estado (connected/notconnect), VLAN, dúplex, velocidad, tipo | Verificar rápidamente qué puertos del switch están activos, en qué VLAN y a qué velocidad |
| `show ip route` | Tabla de enrutamiento completa: redes destino, código de origen (C=connected, S=static, O=OSPF...), next hop, interfaz de salida, gateway of last resort | Diagnosticar problemas de alcanzabilidad. Es el primer sitio donde mirar si un ping falla. |
| `show cdp neighbors` | Dispositivos Cisco directamente conectados: Device ID, interfaz local, interfaz remota, capacidad (R=Router, S=Switch), plataforma | Descubrir la topología física. Funciona sin IP configurada (CDP opera a nivel 2). Clave para verificar que las conexiones físicas son correctas. |
| `show mac address-table` | Tabla de direcciones MAC del switch: VLAN, MAC, tipo (Dynamic/Static), puerto | Verificar qué dispositivos ha aprendido el switch y en qué puerto están |
| `show switch` | Información del stack de switches (si aplica) | Entornos con switches apilados |

#### Interpretación del estado de interfaces

Las dos líneas de estado de `show interfaces` son las más importantes:

| Estado | Significado |
|--------|-------------|
| **Interface is up, line protocol is up** | Todo correcto: interfaz habilitada y comunicación con el otro extremo establecida |
| **Interface is up, line protocol is down** | Interfaz habilitada pero no hay comunicación capa 2 con el otro extremo (problema de cableado, configuración de velocidad/dúplex, o el otro extremo no responde) |
| **Interface is administratively down, line protocol is down** | Interfaz deshabilitada manualmente con el comando `shutdown` |

#### Interpretación de `show ip route`

Cada línea de la tabla de enrutamiento muestra:

- **Letra de código** (cómo se aprendió la ruta): `C` = Connected (directamente conectada), `S` = Static (configurada manualmente), `O` = OSPF, `R` = RIP, `B` = BGP, etc.
- **Red destino** con máscara
- **Información de next hop** y/o interfaz de salida
- **Tiempo** que la ruta lleva en la tabla
- **Gateway of last resort:** Ruta por defecto (0.0.0.0/0). Si dice "not set", el router no tiene ruta por defecto y descartará paquetes cuyo destino no coincida con ninguna ruta.

#### CDP (Cisco Discovery Protocol)

Protocolo propietario de Cisco, ligero, que descubre automáticamente dispositivos vecinos. Funciona **a nivel de capa 2**, por lo que opera incluso sin configuración IP. Muestra: ID del dispositivo remoto, interfaz local y remota por la que están conectados, capacidades (R=Router, S=Switch, H=Host, etc.) y plataforma.

---

## 🎯 Puntos críticos para el examen

- **Documentación:** Los cinco tipos son diagramas, descripciones, baselines, failure reports, y hardware/software. Las baselines son esenciales porque sin ellas no puedes saber si algo funciona "peor de lo normal".
- **Triaje** = determinar importancia del fallo y en qué orden trabajar. No confundir con diagnosticar.
- **Half-split:** Dos fases → **medir** (orientar + observar) y **dividir** (moverse en la dirección correcta). Se empieza en el punto medio entre origen y destino y se reduce el espacio del problema a la mitad en cada iteración.
- **Backout plan** = instrucciones para restaurar el estado previo al cambio si algo sale mal. Imprescindible en todo proceso de change management.
- **Post-mortem:** Centrarse en arreglar el problema, no en buscar culpables. Documentar causa raíz, dwell time, y cómo prevenir recurrencia.
- **Temporary fix vs. permanent fix:** El temporal aumenta deuda técnica y debe reemplazarse. *Nada es más permanente que un fix temporal.*
- **False positive:** Algo parece roto pero no lo está. Cuidado con perseguir anomalías que resultan ser comportamiento normal.
- **Wireshark:** Herramienta open-source de captura/análisis de paquetes. Tres paneles (lista, decodificación, hex dump). Formato de archivo: **`.pcap`** y **`.pcapng`** (estándar de la industria). Se puede guardar, abrir y compartir.
- **Efecto de firewalls:** Los asteriscos (*) en traceroute significan que ICMP está filtrado/bloqueado, no necesariamente que la ruta esté rota. Ping fallido no siempre = destino inalcanzable.
- **Estrategia de ping escalonado:** (1) gateway → (2) IP remota → (3) nombre de dominio. Cada paso descarta una capa de problemas.
- **tracert** (Windows) usa ICMP; **traceroute** (Linux/macOS) usa UDP.
- **SSH siempre preferido sobre Telnet** para gestión remota. Telnet solo para configuración inicial de SSH.
- **Console** = acceso directo al CLI, "plan B" si la red cae. No requiere IP configurada.
- **VPN** = túnel cifrado para acceder a la red interna desde fuera (remoto). IPsec o SSL.
- **RDP** = usado para conectar a un jump host intermedio desde el cual acceder a los dispositivos.
- **NMS** = sistema centralizado con state database, SSOT, dashboard. Protocolos: SNMP (legacy), NETCONF/YANG (moderno), CLI/scripts, gRPC.
- **Meraki** = gestión cloud de Cisco. Los datos de usuario NO pasan por la nube del fabricante.
- **Niveles de privilegio:** `>` = nivel 1 (solo lectura). `#` = nivel 15 (lectura/escritura completa). Comando `enable` sube de nivel.
- **`?`** = ayuda contextual en cualquier punto del comando. **Tab** = autocompletar.
- **Running config** = activa en RAM, se pierde al reiniciar. **Startup config** = en NVRAM, se carga al arrancar. `copy run start` para guardar cambios.
- **`show ip route`:** Buscar primero si existe ruta hacia el destino. Si no existe → problema de enrutamiento. `C` = connected, `S` = static, `O` = OSPF. Gateway of last resort = ruta por defecto.
- **`show cdp neighbors`:** Funciona sin IP (capa 2). Muestra solo dispositivos Cisco directamente conectados.
- **`show ip interface brief`:** Vista rápida de IPs y estados. Si Status=up pero Protocol=down → problema de cableado/enlace.
- **`show mac address-table`:** En switches. Dynamic = aprendido del tráfico. Asocia MAC → puerto → VLAN.

---

## Mini-resumen

- **Metodología y help desk:** Documentar todo (diagramas, descripciones, baselines, failure reports, manuales locales). Usar **triaje** para priorizar fallos en el NOC. Seguir **change management** con backout plan y change windows. Aplicar el método **half-split**: empezar en el punto medio entre origen y destino, medir, dividir, repetir. Tras resolver, hacer **post-mortem** (sin culpables). Cuidado con los **false positives** y con las soluciones temporales que se vuelven permanentes.
- **Wireshark y .pcap/.pcapng:** Herramienta open-source de captura y análisis de paquetes. Tres paneles (lista, decodificación, hex dump). Filtros de captura para reducir volumen. Se guardan y abren archivos en formato **`.pcap`** o **`.pcapng`**. Permite diagnosticar problemas invisibles para ping (retransmisiones TCP, paquetes descartados, handshakes fallidos).
- **Comandos de diagnóstico:** `ping` verifica conectividad (ICMP echo). Estrategia escalonada: gateway → IP remota → dominio. `traceroute`/`tracert` descubre la ruta salto a salto (TTL incremental). `nslookup` resuelve DNS. `ipconfig`/`ifconfig`/`ip addr` muestran la configuración IP local. Los **firewalls pueden bloquear ICMP**, causando falsos negativos en ping y asteriscos en traceroute.
- **Acceso a dispositivos:** **Console** (acceso directo, "plan B"), **SSH** (remoto cifrado, siempre preferido), **Telnet** (remoto sin cifrar, solo provisional), **RDP** (escritorio remoto a jump host), **VPN** (túnel cifrado para acceso desde fuera). **Terminal emulators** (PuTTY, etc.) necesarios para console y SSH. **NMS** centraliza monitorización (SNMP, NETCONF/YANG, CLI/scripts, gRPC). **Meraki** = gestión cloud. Gestión **in-band** (misma red) vs. **out-of-band** (red dedicada de gestión). Tres reglas: usar SSH, controlar acceso físico al console, nunca permitir gestión directa desde Internet.
- **Comandos `show` de Cisco:** Nivel 1 (`>`) = solo lectura; nivel 15 (`#`) = lectura/escritura. `?` para ayuda contextual, Tab para autocompletar. `show running-config` (config activa en RAM), `show version` (IOS, modelo, último reinicio), `show inventory` (componentes físicos con PID/SN), `show ip interface brief` (resumen rápido IP/estado), `show interfaces` (detalles completos por interfaz), `show interfaces status` (estado de puertos del switch), `show ip route` (tabla de enrutamiento: C/S/O + gateway of last resort), `show cdp neighbors` (vecinos Cisco directos, funciona sin IP), `show mac address-table` (MAC→puerto→VLAN en switches), `show switch` (info de stacks).
