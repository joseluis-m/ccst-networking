# CCST Networking 100-150 — Preguntas de práctica
## Dominio 5: Diagnosing Problems (30 preguntas)

---

**Pregunta 1. [Multiple Choice — Single Answer]**

En la metodología de troubleshooting half-split, ¿cuál es el primer paso recomendado antes de aplicar la técnica formal de dividir el espacio del problema?

A) Reinstalar el firmware de todos los routers y switches

B) Comprobar el cambio más reciente realizado en la red

C) Reemplazar todos los cables de la ruta afectada

D) Abrir un caso con el fabricante del equipo notificando el problema

<details>
<summary>Respuesta</summary>
✅ Correcta: B) Comprobar el cambio más reciente realizado en la red

💡 Explicación: La estrategia inicial recomendada es primero comprobar el cambio más reciente (la mayoría de fallos se deben a cambios), después revisar los puntos donde suelen ocurrir fallos, y solo entonces aplicar el half-split formal si no se resuelve rápidamente.
</details>

---

**Pregunta 2. [Multiple Choice — Single Answer]**

¿Qué formato de archivo utiliza Wireshark como estándar de la industria para guardar y compartir capturas de paquetes?

A) .xlsx

B) .pcap/.pcapng

C) .csv

D) .log/.txt

<details>
<summary>Respuesta</summary>
✅ Correcta: B) .pcap/.pcapng
💡 Explicación: Wireshark utiliza los formatos .pcap y .pcapng como estándar de la industria para guardar capturas de paquetes. Estos formatos son compatibles con la mayoría de herramientas de captura y análisis de red. Se pueden guardar, abrir y compartir para diagnóstico colaborativo.
</details>

---

**Pregunta 3. [Multiple Choice — Single Answer]**

Un usuario no puede acceder a ningún sitio web. El técnico ejecuta los siguientes comandos con estos resultados:

```
C:\> ping 192.168.1.1
Reply from 192.168.1.1: bytes=32 time=1ms TTL=64

C:\> ping 8.8.8.8
Reply from 8.8.8.8: bytes=32 time=15ms TTL=117

C:\> ping www.google.com
Ping request could not find host www.google.com
```

¿Cuál es el problema más probable?

A) El cable de red del PC está desconectado

B) El default gateway no funciona o no está configurado correctamente

C) El servidor DNS no funciona o no está configurado correctamente

D) El firewall del ISP está bloqueando todo el tráfico

<details>
<summary>Respuesta</summary>
✅ Correcta: C) El servidor DNS no funciona o no está configurado correctamente

💡 Explicación: El ping al gateway (paso 1) funciona → la conectividad local está bien. El ping a la IP remota 8.8.8.8 (paso 2) funciona → el enrutamiento está bien. Pero el ping al nombre de dominio (paso 3) falla → la resolución DNS no funciona. El problema es que el DNS no está configurado correctamente o el servidor DNS no responde.
</details>

---

**Pregunta 4. [Multiple Choice — Single Answer]**

¿Qué protocolo de acceso remoto es siempre preferido sobre Telnet para la gestión de dispositivos de red?

A) RDP

B) SSH

C) FTP

D) HTTP

<details>
<summary>Respuesta</summary>
✅ Correcta: B) SSH

💡 Explicación: SSH (Secure Shell) proporciona cifrado de extremo a extremo para el acceso remoto al CLI, y siempre debe preferirse sobre Telnet, que transmite todo en texto plano sin cifrar. Telnet solo debe usarse para configurar SSH inicialmente y después deshabilitarse. RDP es para escritorio remoto (jump hosts), no para gestión directa del CLI.
</details>

---

**Pregunta 5. [Multiple Choice — Single Answer]**

Un administrador ejecuta `show running-config` en un router Cisco y realiza un cambio de configuración. ¿Qué debe hacer para que el cambio persista tras un reinicio?

A) El cambio se guarda automáticamente en NVRAM

B) Ejecutar `copy running-config startup-config`

C) Ejecutar `reload` inmediatamente

D) Ejecutar `show startup-config` para activar el cambio

<details>
<summary>Respuesta</summary>

✅ Correcta: B) Ejecutar `copy running-config startup-config`

💡 Explicación: Los cambios desde CLI modifican solo la running config (almacenada en RAM volátil). Para que persistan tras un reinicio, se debe copiar la running a la startup: `copy running-config startup-config` (abreviado `copy run start`). La startup config se almacena en NVRAM (no volátil) y se carga al arrancar. Esto protege contra errores: si un comando erróneo te desconecta, basta con reiniciar para recuperar la configuración anterior.
</details>

---

**Pregunta 6. [Multiple Choice — Single Answer]**

Un administrador observa la siguiente salida en un router Cisco:

```
router> show ip route
        ^
% Invalid input detected at '^' marker.
```

¿Cuál es la causa más probable del error?

A) La tabla de enrutamiento está vacía

B) El comando `show ip route` no existe en Cisco IOS

C) El administrador está en modo User EXEC

D) La interfaz de red del router está deshabilitada

<details>
<summary>Respuesta</summary>

✅ Correcta: C) El administrador está en modo User EXEC

💡 Explicación: El prompt `router>` indica modo User EXEC (nivel 1, solo lectura básica). El comando `show ip route` requiere privileged EXEC (nivel 15, prompt `router#`). El administrador debe ejecutar `enable` (e introducir la contraseña de enable secret) para acceder al nivel 15, donde tiene acceso completo a todos los comandos `show` y a `config terminal`.
</details>

---

**Pregunta 7. [Multiple Choice — Single Answer]**

¿Qué tipo de documentación de red registra mediciones periódicas del comportamiento normal (utilización de ancho de banda, frecuencia de fallos, retardos) para poder detectar desviaciones?

A) Diagramas de red

B) Failure reports

C) Baselines

D) Descripciones de diseño

<details>
<summary>Respuesta</summary>
✅ Correcta: C) Baselines

💡 Explicación: Las baselines son mediciones periódicas del comportamiento normal de la red: utilización de ancho de banda, frecuencia de fallos de enlace, tiempo de convergencia, retardos. Se actualizan regularmente y permiten detectar tendencias. Sin baselines, no se puede determinar si algo funciona "peor de lo normal".
</details>

---

**Pregunta 8. [Multiple Choice — Single Answer]**

Un administrador ejecuta el siguiente comando en un switch Cisco:

```
Switch# show mac address-table
          Mac Address Table
-------------------------------------------
   Vlan    Mac Address       Type        Ports
   ----    -----------       ----        -----
   1       0000.5E11.1111    DYNAMIC     Fa0/1
   1       0000.5E22.2222    DYNAMIC     Fa0/2
   1       0000.5E33.3333    STATIC      CPU
```

¿Qué indica la entrada de tipo DYNAMIC asociada al puerto Fa0/1?

A) Esa dirección MAC fue configurada manualmente por el administrador

B) Esa dirección MAC fue aprendida automáticamente del tráfico de red

C) Esa dirección MAC pertenece a la CPU del propio switch

D) Esa dirección MAC ha sido bloqueada por el filtrado MAC

<details>
<summary>Respuesta</summary>
✅ Correcta: B) Esa dirección MAC fue aprendida automáticamente del tráfico de red

💡 Explicación: Las entradas DYNAMIC se crean automáticamente cuando el switch examina la MAC de origen de las tramas que recibe y las asocia al puerto de entrada (bridge learning). Las entradas STATIC están configuradas manualmente o son del propio sistema (como la entrada CPU). El switch usa esta tabla para reenviar tramas de forma eficiente al puerto correcto.
</details>

---

**Pregunta 9. [Multiple Choice — Single Answer]**

¿Cuál es la diferencia principal entre gestión in-band y out-of-band (OOB)?

A) In-band usa SSH y OOB usa solo Telnet

B) In-band gestiona a través de las mismas interfaces de tráfico de usuarios; OOB usa una red de gestión dedicada y separada

C) In-band solo funciona con routers; OOB solo funciona con switches

D) In-band usa una red de gestión dedicada y separada; OOB gestiona a través de las mismas interfaces de tráfico de usuarios

<details>
<summary>Respuesta</summary>
✅ Correcta: B) In-band gestiona a través de las mismas interfaces de tráfico de usuarios; OOB usa una red de gestión dedicada y separada

💡 Explicación: Gestión in-band utiliza las mismas interfaces que transportan datos de usuario: es más económico pero si la red cae, pierdes el acceso de gestión. Gestión out-of-band (OOB) usa una red dedicada separada conectada a puertos de management específicos, y sigue funcionando aunque la red de producción caiga.
</details>

---

**Pregunta 10. [Multiple Choice — Single Answer]**

Un administrador ejecuta en un router Cisco:

```
Router# show ip interface brief
Interface           IP-Address    OK? Method Status    Protocol
GigabitEthernet0/0  192.168.1.1   YES manual up        up
GigabitEthernet0/1  10.0.0.1      YES manual up        down
GigabitEthernet0/2  unassigned    YES unset  administratively down down
```

¿Qué indica el estado de GigabitEthernet0/1 (Status: up, Protocol: down)?

A) La interfaz funciona correctamente sin problemas

B) La interfaz está habilitada pero no hay comunicación capa 2 con el otro extremo

C) La interfaz ha sido deshabilitada manualmente con el comando `shutdown` y no hay comunicación

D) La dirección IP está duplicada en la red

<details>
<summary>Respuesta</summary>
✅ Correcta: B) La interfaz está habilitada pero no hay comunicación capa 2 con el otro extremo

💡 Explicación: "Interface is up, line protocol is down" significa que la interfaz está habilitada (no se ha ejecutado `shutdown`) pero no puede establecer comunicación de capa 2 con el otro extremo. Las causas típicas son: cable defectuoso, configuración de velocidad/dúplex no coincidente, o el equipo del otro extremo no responde. GE0/2 muestra "administratively down" — esa sí fue deshabilitada con `shutdown`.
</details>

---

**Pregunta 11. [Multiple Choice — Single Answer]**

¿Qué comando Cisco IOS muestra los dispositivos Cisco directamente conectados y funciona incluso sin configuración IP, operando a nivel de capa 2?

A) show ip route

B) show cdp neighbors

C) show running-config

D) show version

<details>
<summary>Respuesta</summary>
✅ Correcta: B) show cdp neighbors

💡 Explicación: CDP (Cisco Discovery Protocol) es propietario de Cisco y opera a nivel de capa 2, por lo que funciona incluso sin IP configurada. Muestra: Device ID, interfaz local y remota, capacidades (R=Router, S=Switch), y plataforma de los dispositivos Cisco directamente conectados. Es clave para verificar conexiones físicas y descubrir la topología.
</details>

---

**Pregunta 12. [Multiple Choice — Single Answer]**

Un técnico necesita descubrir por qué un paquete no llega a su destino. Ejecuta `tracert 10.0.5.1` desde un PC Windows y observa:

```
  1     1 ms     1 ms     1 ms  192.168.1.1
  2    10 ms    10 ms    10 ms  10.0.0.1
  3     *        *        *     Request timed out.
  4    15 ms    15 ms    15 ms  10.0.5.1
```

¿Qué indica el asterisco (*) en el salto 3?

A) El router del salto 3 está completamente caído y el paquete toma una ruta alternativa

B) El router del salto 3 no envía respuestas ICMP o un firewall intermedio las bloquea

C) La conexión se ha perdido permanentemente a partir del salto 3

D) El DNS no puede resolver la dirección del salto 3

<details>
<summary>Respuesta</summary>
✅ Correcta: B) El router del salto 3 no envía respuestas ICMP o un firewall intermedio las bloquea

💡 Explicación: El asterisco (*) indica que el dispositivo en ese salto no envía respuestas ICMP TTL Expired, ya sea porque las tiene deshabilitadas o porque un firewall las filtra. Esto no significa que la ruta esté rota — de hecho, el paquete llega al destino en el salto 4 (10.0.5.1), confirmando que el camino es funcional. Un ping fallido o asteriscos en traceroute no siempre implican un problema de conectividad.
</details>

---

**Pregunta 13. [Multiple Choice — Single Answer]**

¿Qué significa la sigla MTTR en el contexto de gestión de fallos de red?

A) Mean Time To Route — tiempo medio para encontrar una ruta alternativa

B) Mean Time To Repair — tiempo medio de indisponibilidad hasta la reparación

C) Maximum Throughput Transfer Rate — tasa máxima de transferencia

D) Mean Time To Reboot — tiempo medio de reinicio del dispositivo

<details>
<summary>Respuesta</summary>
✅ Correcta: B) Mean Time To Repair — tiempo total de indisponibilidad hasta la reparación

💡 Explicación: MTTR (Mean Time To Repair) mide el tiempo total de indisponibilidad, que puede incluir o no el dwell time (tiempo que el fallo existe antes de ser detectado) según la política local. Otras métricas clave son MTBF (tiempo medio entre fallos), MTBM (tiempo medio entre errores humanos) y MTTI (tiempo para demostrar que el problema no es de la red).
</details>

---

**Pregunta 14. [Multiple Choice — Single Answer]**

¿Qué servicio web se necesita utilizar para descubrir la dirección IP pública de un host que está detrás de NAT?

A) nslookup dirigido al default gateway

B) El comando `ipconfig /all` muestra tanto IP privada como IP pública

C) Un servicio externo como checkip.amazonaws.com

D) El comando `show ip route` en el router

<details>
<summary>Respuesta</summary>
✅ Correcta: C) Un servicio externo como Google "what is my IP" o checkip.amazonaws.com

💡 Explicación: NAT traduce la IP privada a una pública, por lo que `ipconfig /all` solo muestra la IP privada del host. Para conocer la IP pública asignada por NAT, es necesario consultar un servicio web externo (Google "what is my IP", `curl http://tnx.nl/ip`, checkip.amazonaws.com) que ve la dirección desde la perspectiva de Internet.
</details>

---

**Pregunta 15. [Multiple Choice — Single Answer]**

¿Qué característica distingue a Cisco Meraki de un NMS tradicional on-premises?

A) Meraki es un analizador de paquetes como Wireshark

B) Meraki es una plataforma de gestión de red basada en la nube

C) Meraki requiere acceso por console a cada dispositivo para funcionar

D) Meraki solo gestiona routers, no switches ni APs

<details>
<summary>Respuesta</summary>
✅ Correcta: B) Meraki es una plataforma de gestión de red basada en la nube

💡 Explicación: Cisco Meraki ofrece gestión cloud: los dispositivos (APs, routers, switches) envían su estado y telemetría a la plataforma cloud del fabricante, que funciona como un NMS hospedado externamente. Dato clave: el tráfico de datos de los usuarios NO pasa por la nube del fabricante — solo metadatos y estado de los dispositivos transitan por ella.
</details>

---

**Pregunta 16. [Multiple Choice — Choose Two]**

¿Cuáles de los siguientes son componentes de un Network Management System (NMS)? (Elige dos)

A) State database que almacena el estado actual de cada dispositivo

B) Cable tester que verifica la integridad física de cada enlace de cobre

C) Dashboard que muestra una vista rápida del estado de la red con alertas

D) Servidor DHCP que asigna direcciones IP a todos los hosts de la red

<details>
<summary>Respuesta</summary>
✅ Correcta: A) y C)

💡 Explicación: Un NMS incluye: state database (estado actual y salud general de la red), SSOT (configuración intencionada), time series database (historial), automation system (scripts) y dashboard (single pane of glass con alertas). Un cable tester (B) es una herramienta física independiente, y un servidor DHCP (D) es un servicio de red, no un componente de NMS.
</details>

---

**Pregunta 17. [Multiple Choice — Choose Two]**

¿Cuáles de las siguientes son reglas de seguridad fundamentales para la gestión remota de dispositivos de red? (Elige dos)

A) Usar siempre SSH para gestionar dispositivos y deshabilitar Telnet

B) Permitir conexiones de gestión directas desde Internet para mayor comodidad

C) Nunca permitir conexiones de gestión directas desde fuera de la red

D) Dejar el puerto console accesible sin restricciones para facilitar el soporte rápido

<details>
<summary>Respuesta</summary>
✅ Correcta: A) y C)

💡 Explicación: Las tres reglas de seguridad son: (1) usar siempre SSH y deshabilitar Telnet después de configurar SSH (A), (2) controlar el acceso físico al console, y (3) nunca permitir gestión directa desde Internet — conectar primero a un jump host interno mediante RDP/SSH/VPN (C). Las opciones B y D violan directamente estas reglas de seguridad.
</details>

---

**Pregunta 18. [Multiple Choice — Choose Two]**

¿Cuáles de las siguientes situaciones producirían un false positive en el diagnóstico de red? (Elige dos)

A) Un ping falla porque el firewall del destino bloquea ICMP

B) Un enlace se cae físicamente y los usuarios pierden conectividad

C) Un traceroute muestra asteriscos en un salto porque el router tiene deshabilitadas las respuestas ICMP

D) Un switch se reinicia y todos los hosts conectados pierden conectividad temporalmente

<details>
<summary>Respuesta</summary>
✅ Correcta: A) y C)

💡 Explicación: Un false positive ocurre cuando algo parece roto pero no lo está. Un ping fallido por firewall ICMP (A) sugiere un problema de conectividad que no existe. Asteriscos en traceroute por respuestas ICMP deshabilitadas (C) sugieren un router problemático cuando en realidad el tráfico fluye normalmente. Las opciones B y D son fallos reales, no false positives.
</details>

---

**Pregunta 19. [Multiple Choice — Choose Two]**

¿Cuáles de las siguientes son las dos fases del método half-split de troubleshooting? (Elige dos)

A) Medir — orientarse al punto actual y observar qué modelo explica lo que está pasando

B) Reemplazar — orientarse al punto actual y sustituir todos los componentes del camino afectado

C) Dividir — decidir hacia dónde moverse

D) Escalar — transferir el problema al fabricante del equipo

<details>
<summary>Respuesta</summary>
✅ Correcta: A) y C)

💡 Explicación: El método half-split tiene dos fases que se repiten cíclicamente: Fase 1 — Medir: orientarse, observar y crear hipótesis sobre qué explica el comportamiento. Fase 2 — Dividir: decidir hacia dónde moverse (izquierda/derecha/arriba/abajo) para reducir el espacio del problema a la mitad en cada iteración.
</details>

---

**Pregunta 20. [Multiple Choice — Choose Two]**

Un administrador necesita recoger datos de configuración y estado de dispositivos Cisco para alimentar un NMS. ¿Cuáles de los siguientes son métodos modernos y preferidos? (Elige dos)

A) SNMP

B) NETCONF/YANG

C) Fax de las salidas de `show running-config` impresas

D) Scripts CLI

<details>
<summary>Respuesta</summary>
✅ Correcta: B) y D)

💡 Explicación: NETCONF/YANG es el método moderno y preferido (B): transporta datos en formato YANG legible por humanos y máquinas. Los scripts CLI (D) automatizan la ejecución de comandos, parsean la salida y la almacenan. SNMP (A) es legacy e inseguro, formato MIB — muchos operadores buscan eliminarlo. La opción C es absurda en contexto moderno.
</details>

---

**Pregunta 21. [Multiple Choice — Choose Two]**

¿Cuáles de los siguientes elementos debe incluir un proceso formal de change management en una red? (Elige dos)

A) Un backout plan con instrucciones para restaurar el estado previo al cambio si algo falla

B) Documentación del cambio y procedimientos de prueba previos

C) Permiso verbal del primer usuario que reporte un problema, sin documentación escrita

D) Ejecución del cambio en horario de máximo tráfico para probar bajo condiciones reales

<details>
<summary>Respuesta</summary>
✅ Correcta: A) y B)

💡 Explicación: Todo cambio en la red debe incluir: procedimientos de prueba previos, documentación del cambio (qué, cómo, por qué), y un backout plan para restaurar rápidamente el estado anterior si algo falla. Los cambios se realizan durante change windows (cortes planificados), no en horario de máximo tráfico. La documentación escrita es imprescindible.
</details>

---

**Pregunta 22. [Drag and Drop]**

Arrastra cada comando Cisco `show` a la información que muestra.

**Elementos a arrastrar:**
- show version
- show ip route
- show cdp neighbors
- show running-config

**Categorías destino:**
- Versión de IOS, modelo del router, número de serie, motivo del último reinicio, tiempo de actividad
- Tabla de enrutamiento completa: redes destino, código de origen (C/S/O), next hop, gateway of last resort
- Dispositivos Cisco directamente conectados: Device ID, interfaz local/remota, capacidades, plataforma
- Configuración completa activa en RAM: IPs, ACLs, rutas estáticas, hostname, protocolos

<details>
<summary>Respuesta</summary>
✅ Correcta:

- show version → Versión de IOS, modelo del router, número de serie, motivo del último reinicio, tiempo de actividad

- show ip route → Tabla de enrutamiento completa: redes destino, código de origen (C/S/O), next hop, gateway of last resort

- show cdp neighbors → Dispositivos Cisco directamente conectados: Device ID, interfaz local/remota, capacidades, plataforma

- show running-config → Configuración completa activa en RAM: IPs, ACLs, rutas estáticas, hostname, protocolos

💡 Explicación: Cada comando `show` tiene un propósito diagnóstico específico. `show version` identifica hardware/software. `show ip route` diagnostica alcanzabilidad. `show cdp neighbors` descubre topología física (capa 2). `show running-config` verifica toda la configuración activa.
</details>

---

**Pregunta 23. [Drag and Drop]**

Arrastra cada método de acceso a dispositivos de red a su descripción.

**Elementos a arrastrar:**
- Console
- SSH
- Telnet
- VPN

**Categorías destino:**
- Acceso directo al CLI via puerto serie/USB; no requiere IP configurada; "plan B" si la red cae
- Acceso remoto cifrado al CLI via TCP puerto 22; siempre preferido para gestión
- Acceso remoto sin cifrar via TCP puerto 23; solo para configuración inicial de SSH
- Túnel cifrado sobre Internet para acceder a la red interna como si estuvieras dentro

<details>
<summary>Respuesta</summary>
✅ Correcta:

- Console → Acceso directo al CLI via puerto serie/USB; no requiere IP configurada; "plan B" si la red cae

- SSH → Acceso remoto cifrado al CLI via TCP puerto 22; siempre preferido para gestión

- Telnet → Acceso remoto sin cifrar via TCP puerto 23; solo para configuración inicial de SSH

- VPN → Túnel cifrado sobre Internet para acceder a la red interna como si estuvieras dentro

💡 Explicación: Console es físico y el último recurso. SSH cifra todo y es el método preferido. Telnet no cifra nada y debe deshabilitarse tras configurar SSH. VPN crea un túnel cifrado (IPsec o SSL) que permite acceder a recursos internos de forma segura desde ubicaciones remotas.
</details>

---

**Pregunta 24. [Drag and Drop]**

Ordena los pasos de la estrategia de diagnóstico escalonado con ping (del primero al tercero).

**Elementos a arrastrar:**
- Ping a un nombre de dominio → ¿Funciona la resolución DNS?
- Ping al default gateway → ¿Funciona la conectividad local?
- Ping a una IP remota conocida → ¿Funciona el enrutamiento?

**Posiciones destino:**
- Paso 1
- Paso 2
- Paso 3

<details>
<summary>Respuesta</summary>
✅ Correcta:

- Paso 1 → Ping al default gateway → ¿Funciona la conectividad local?

- Paso 2 → Ping a una IP remota conocida → ¿Funciona el enrutamiento?

- Paso 3 → Ping a un nombre de dominio → ¿Funciona la resolución DNS?

💡 Explicación: Cada paso descarta una capa de problemas. Si el paso 1 falla → problema local (cable, IP, interfaz). Si paso 1 OK pero paso 2 falla → problema de enrutamiento. Si pasos 1 y 2 OK pero paso 3 falla → problema de DNS. Se avanza solo si el paso anterior tiene éxito.
</details>

---

**Pregunta 25. [Drag and Drop]**

Arrastra cada tipo de documentación de red a su contenido.

**Elementos a arrastrar:**
- Baselines
- Failure reports
- Descripciones

**Categorías destino:**
- Mediciones periódicas del comportamiento normal: utilización de ancho de banda, retardos, frecuencia de fallos
- Informes de cada incidencia: síntomas, causa raíz, solución temporal, solución permanente
- Principios de diseño, aplicaciones soportadas, esquema de direccionamiento IP, sistema de nombres

<details>
<summary>Respuesta</summary>
✅ Correcta:

- Baselines → Mediciones periódicas del comportamiento normal: utilización de ancho de banda, retardos, frecuencia de fallos

- Failure reports → Informes de cada incidencia: síntomas, causa raíz, solución temporal, solución permanente

- Descripciones → Principios de diseño, aplicaciones soportadas, esquema de direccionamiento IP, sistema de nombres

💡 Explicación: Las baselines permiten detectar desviaciones del comportamiento normal. Los failure reports alimentan el sistema de ticketing y son una mina de información para troubleshooting futuro. Las descripciones documentan la intención de diseño y el funcionamiento esperado de la red.
</details>

---

**Pregunta 26. [Drag and Drop]**

Arrastra cada prompt de Cisco IOS a su nivel de privilegio y capacidad.

**Elementos a arrastrar:**
- router>
- router#
- router(config)#

**Categorías destino:**
- User EXEC (nivel 1): solo lectura, información básica; no se puede cambiar nada
- Privileged EXEC (nivel 15): lectura/escritura completas, todos los comandos show y config terminal
- Global Configuration: modificar la configuración global del dispositivo

<details>
<summary>Respuesta</summary>
✅ Correcta:

- router> → User EXEC (nivel 1): solo lectura, información básica; no se puede cambiar nada

- router# → Privileged EXEC (nivel 15): lectura/escritura completas, todos los comandos show y config terminal

- router(config)# → Global Configuration: modificar la configuración global del dispositivo

💡 Explicación: El símbolo `>` indica nivel 1 (lectura). El símbolo `#` indica nivel 15 (control total). Para pasar de `>` a `#` se ejecuta el comando `enable`. Desde `#` se accede a configuración global con `config terminal`, y desde ahí a sub-modos como `config-if` para interfaces.
</details>

---

**Pregunta 27. [Hotspot]**

Se muestra la siguiente salida del comando `show ip route` en un router Cisco:

```
Router# show ip route
Gateway of last resort is not set

C    192.168.1.0/24 is directly connected, GigabitEthernet0/0
S    10.0.0.0/8 [1/0] via 192.168.1.254
O    172.16.0.0/16 [110/20] via 192.168.1.254
```

Un paquete llega al router con destino 8.8.8.8. **Señala qué ocurrirá con ese paquete.**

A) Se reenviará por la ruta estática hacia 10.0.0.0/8 ya que el gateway of last resort no está configurado

B) Se reenviará por la ruta OSPF hacia 172.16.0.0/16 ya que el gateway of last resort no está configurado

C) Se reenviará por la interfaz GigabitEthernet0/0 directamente

D) Se descartará porque no existe ruta hacia 8.8.8.8 y el gateway of last resort no está configurado

<details>
<summary>Respuesta</summary>
✅ Correcta: D) Se descartará porque no existe ruta hacia 8.8.8.8 y el gateway of last resort no está configurado

💡 Explicación: Ninguna de las tres rutas en la tabla cubre 8.8.8.8 (no pertenece a 192.168.1.0/24, ni a 10.0.0.0/8, ni a 172.16.0.0/16). El "Gateway of last resort is not set" indica que no hay ruta por defecto (0.0.0.0/0). Sin ruta que cubra el destino, el router descarta el paquete. Este es exactamente el tipo de diagnóstico que se realiza con `show ip route` cuando un ping falla.
</details>

---

**Pregunta 28. [Hotspot]**

Se muestra la siguiente salida del comando `show interfaces status` en un switch Cisco:

```
Switch# show interfaces status
Port      Name      Status       Vlan  Duplex  Speed  Type
Fa0/1     PC-Admin  connected    1     a-full  a-100  10/100BaseTX
Fa0/2     Printer   notconnect   1     auto    auto   10/100BaseTX
Fa0/3     Server    connected    10    a-full  a-1000 10/100/1000BaseTX
Fa0/4     AP-WiFi   connected    1     a-full  a-100  10/100BaseTX
```

Un técnico reporta que la impresora no puede comunicarse con la red. **Señala el puerto que indica el problema y su causa.**

A) Fa0/1 — velocidad incorrecta a 100 Mbps

B) Fa0/2 — "notconnect" indica que no hay enlace físico

C) Fa0/3 — la impresora está en VLAN 10 en lugar de VLAN 1

D) Fa0/4 — el AP Wi-Fi está consumiendo todo el ancho de banda

<details>
<summary>Respuesta</summary>
✅ Correcta: B) Fa0/2 — estado "notconnect" indica que no hay enlace físico

💡 Explicación: El puerto Fa0/2 etiquetado como "Printer" muestra estado "notconnect", lo que significa que no hay enlace físico activo. Las causas más probables son: cable desconectado, cable defectuoso, o la impresora está apagada. Este es uno de los primeros indicadores que se verifican con `show interfaces status` — un vistazo rápido a qué puertos están activos, en qué VLAN y a qué velocidad.
</details>

---

**Pregunta 29. [Hotspot]**

Se muestra la siguiente salida del comando `show cdp neighbors` en un router:

```
Router# show cdp neighbors
Device ID    Local Intrfce   Holdtme  Capability  Platform    Port ID
Switch-Core  Gig 0/0         162      S I         WS-C3750   Gig 0/1
Switch-Acc1  Gig 0/1         145      S I         WS-C2960   Gig 0/24
Router-WAN   Gig 0/2         130      R S I       ISR4321    Gig 0/0/0
```

**Señala qué dispositivo tiene capacidad de Router (R) además de Switch (S).**

A) Switch-Core (Capability: S I)

B) Switch-Acc1 (Capability: S I)

C) Router-WAN (Capability: R S I)

D) Ninguno — CDP no muestra capacidades

<details>
<summary>Respuesta</summary>
✅ Correcta: C) Router-WAN (Capability: R S I)

💡 Explicación: La columna Capability muestra las capacidades de cada vecino: R=Router, S=Switch, I=IGMP. Solo Router-WAN tiene "R S I", indicando que es un dispositivo con capacidad de router. Los otros dos (Switch-Core y Switch-Acc1) solo muestran "S I" (switch). CDP descubre esta información automáticamente a nivel de capa 2, sin necesidad de IP configurada.
</details>

---

**Pregunta 30. [Hotspot]**

Un usuario de Windows ejecuta `ipconfig /all` y obtiene la siguiente salida:

```
Ethernet adapter Local Area Connection:
   Connection-specific DNS Suffix  . :
   Physical Address. . . . . . . . : 00-1A-2B-3C-4D-5E
   DHCP Enabled. . . . . . . . . . : Yes
   IPv4 Address. . . . . . . . . . : 169.254.45.123
   Subnet Mask . . . . . . . . . . : 255.255.0.0
   Default Gateway . . . . . . . . :
   DNS Servers . . . . . . . . . . :
```

El usuario no puede acceder a ningún recurso de red. **Señala el campo que revela la causa raíz del problema.**

A) Physical Address — la MAC es inválida

B) DHCP Enabled — el DHCP debería estar deshabilitado

C) La dirección 169.254.x.x indica que DHCP falló

D) Subnet Mask — la máscara /16 es incorrecta para una red corporativa

<details>
<summary>Respuesta</summary>
✅ Correcta: C) La dirección 169.254.x.x indica que DHCP falló y se autoasignó una dirección APIPA

💡 Explicación: La dirección 169.254.45.123 pertenece al rango link-local/APIPA (169.254.0.0/16), que se autoasigna cuando un host con DHCP habilitado no puede contactar con ningún servidor DHCP. Los campos Default Gateway y DNS Servers están vacíos, confirmando que DHCP no pudo completar la asignación. La causa raíz puede ser: servidor DHCP caído, cable desconectado al switch, o problema de red entre el host y el servidor DHCP.
</details>

---

✅ 30 preguntas del Dominio 5 completadas.

📊 **Desglose por objetivo:**

| Objetivo | Tema | Preguntas | Total |
|----------|------|-----------|:-----:|
| **5.1** | Metodologías troubleshooting, help desk, ticketing, documentación, triaje | 1, 7, 13, 19, 21, 25 | **6** |
| **5.2** | Wireshark: propósito, paneles, .pcap/.pcapng | 2 | **1** |
| **5.3** | Comandos diagnóstico: ping, ipconfig, tracert, nslookup; efecto de firewalls | 3, 12, 14, 18, 24, 30 | **6** |
| **5.4** | Acceso a dispositivos: SSH, Telnet, Console, VPN, RDP, NMS, Meraki, scripts | 4, 9, 15, 16, 17, 20, 23 | **7** |
| **5.5** | Comandos show Cisco: show run, cdp, ip interface brief, ip route, version, mac table | 5, 6, 8, 10, 11, 22, 26, 27, 28, 29 | **10** |
| | | **TOTAL** | **30** |

📋 **Desglose por tipo de pregunta:**

| Tipo | Cantidad | Preguntas |
|------|:--------:|-----------|
| Multiple Choice (1 respuesta) | **15** | 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15 |
| Multiple Choice (Choose Two) | **6** | 16, 17, 18, 19, 20, 21 |
| Drag and Drop | **5** | 22, 23, 24, 25, 26 |
| Hotspot | **4** | 27, 28, 29, 30 |

🖥️ **Preguntas con salida simulada de comando: 10**
→ Preguntas 3, 6, 8, 10, 12, 27, 28, 29, 30 + contexto de comando en P5

🔧 **Preguntas de escenario de troubleshooting: 7**
→ Preguntas 3, 10, 12, 14, 18, 28, 30

🎯 **Desglose por dificultad:**

| Nivel | Cantidad | Preguntas |
|-------|:--------:|-----------|
| Fácil (40%) | **12** | 1, 2, 4, 5, 7, 9, 11, 13, 22, 23, 24, 25 |
| Medio (40%) | **12** | 3, 6, 8, 10, 12, 14, 15, 17, 19, 26, 28, 29 |
| Difícil (20%) | **6** | 16, 18, 20, 21, 27, 30 |
