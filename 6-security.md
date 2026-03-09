# Dominio 6: Security

## Resumen ejecutivo

Este dominio cubre los fundamentos de seguridad de redes desde tres ángulos complementarios: cómo los firewalls filtran tráfico (6.1), los conceptos teóricos fundacionales de seguridad — CIA, AAA, cifrado, amenazas, ataques (6.2) — y la configuración básica de seguridad inalámbrica en un router doméstico (6.3). Es el dominio más amplio conceptualmente: combina terminología de seguridad, clasificación de ataques, herramientas defensivas, criptografía y seguridad Wi-Fi. Para el examen, presta especial atención a la tríada CIA, el proceso AAA, los factores de autenticación MFA, las diferencias entre tipos de ataques (spam vs. phishing, DoS vs. DDoS, directo vs. reflexión), el funcionamiento del filtrado stateful, y la tabla comparativa WPA/WPA2/WPA3 con Personal vs. Enterprise.

---

## Conceptos clave

### 6.1 — Cómo los firewalls filtran tráfico

🔑 *Analogía:* Un firewall es como un portero de discoteca con lista de invitados: comprueba cada paquete contra un conjunto de reglas y decide si lo deja pasar (permit) o lo bloquea (deny). Un firewall stateful además recuerda quién salió, para solo dejar entrar respuestas de conversaciones que empezaron desde dentro.

#### Filtrado de paquetes por reglas (ACL)

Las **access control lists** (ACL, listas de control de acceso) son conjuntos de políticas aplicadas al reenvío de paquetes en un router o firewall. Cada regla especifica:

| Campo | Función |
|-------|---------|
| **Número de grupo** | Identifica un conjunto asociado de reglas |
| **Acción: `permit` o `deny`** | Reenviar o descartar el paquete si coincide |
| **Dirección origen** | Coincidir con la IP de origen (`any` = cualquiera, `host X.X.X.X` = una IP específica) |
| **Dirección destino** | Coincidir con la IP de destino |
| **Protocolo/puerto** (opcional) | Coincidir con protocolo (TCP, UDP, IP) y puerto específico (por ejemplo, `eq telnet`, `eq 80`) |

**Regla implícita final:** Si un paquete no coincide con ninguna regla de la lista, **se descarta** (deny implícito). Por eso toda access list debe terminar con `permit ip any any` si quieres permitir el resto del tráfico.

**Aplicación a una interfaz:** Las access lists se aplican a una interfaz con dirección (`in` o `out`):
```
access-list 101 deny tcp any host 192.0.2.1 eq telnet
access-list 101 permit ip any any
interface FastEthernet 1
  ip access-group 101 in
```

Esto bloquea Telnet hacia 192.0.2.1 desde cualquier origen, pero permite todo lo demás, en la interfaz de entrada.

#### Filtrado stateful (Stateful Packet Filtering)

El filtrado stateful es el mecanismo principal de los firewalls modernos. Funciona como un **espejo unidireccional**: permite tráfico originado desde la red interna y bloquea tráfico originado desde la red externa.

**Proceso paso a paso:**

1. Host interno *A* envía TCP SYN hacia servidor externo *C*.
2. El firewall *B* anota esta conexión y abre un "agujero" temporal para permitir el SYN-ACK esperado de *C*.
3. *C* responde con SYN-ACK → el firewall lo permite (coincide con el estado esperado).
4. *A* envía ACK → la conexión TCP está establecida. El firewall configura sus filtros para permitir paquetes de *C* con el número de puerto correcto.
5. Si un host externo *D* intenta iniciar una conexión hacia *A* (sin que *A* la haya solicitado), el firewall **descarta los paquetes** porque no hay estado previo.

#### Filtrado contextual y firewalls de aplicación

**Filtrado contextual** va más allá del estado de la conexión: examina el **contenido** de los paquetes con conocimiento profundo de la aplicación.

- **WAF (Web Application Firewall):** Inspecciona peticiones HTTP buscando formatos incorrectos, ataques de inyección, secuencias inválidas, recursos inexistentes.
- **IDS (Intrusion Detection System):** Compara el tráfico contra bases de datos de patrones de malware conocido y patrones de ataque aprendidos. Descarta paquetes sospechosos.

**Un firewall moderno es una colección de servicios de seguridad** en un solo dispositivo (físico o virtual): filtrado stateful, IDS, NAT, filtrado contextual, filtrado por dirección/puerto y otras funciones.

#### Defensa en profundidad (Defense in Depth)

Nunca depender de una sola línea de defensa. El atacante debe atravesar **múltiples capas** defensivas, cada una con vulnerabilidades diferentes: red separada (segmentación), 2FA para acceder a la red, 2FA adicional para la aplicación, ACLs, monitorización y logging.

---

### 6.2 — Conceptos fundacionales de seguridad

🔑 *Analogía:* La tríada CIA es como proteger un documento legal: **Confidencialidad** = que solo lo lean las partes autorizadas; **Integridad** = que nadie altere su contenido; **Disponibilidad** = que esté accesible cuando se necesite. AAA es el control de acceso al edificio: te identifican (autenticación), te dicen a qué plantas puedes ir (autorización), y registran tus movimientos (contabilidad).

#### La tríada CIA

| Pilar | Definición | Métodos de protección |
|-------|-----------|----------------------|
| **Confidentiality** (Confidencialidad) | Proteger la información del acceso por partes no autorizadas. "Parte" incluye personas, procesos y aplicaciones. | Lifecycle controls (destruir datos innecesarios), **encryption**, segmentation, **access control**, monitoring/detection |
| **Integrity** (Integridad) | Confianza en que los datos no han sido modificados (intencionada o accidentalmente) durante su almacenamiento o transmisión | Encryption (datos alterados no se descifran correctamente), segmentation, access control, monitoring/detection, **resilience** (restaurar al estado original) |
| **Availability** (Disponibilidad) | Capacidad de los usuarios de acceder a los recursos y datos que necesitan para trabajar. Principal foco ante ataques DDoS. | Segmentation (aislar subsistemas comprometidos), access control, monitoring/detection, **resilience** (sobrevivir a ataques DoS) |

**Shift left:** Integrar seguridad y privacidad desde las fases de **diseño y pruebas**, no solo en la operación. Incluir cifrado, segmentación, control de acceso y monitorización como requisitos de diseño. Realizar penetration testing antes del despliegue.

#### AAA: Authentication, Authorization, Accounting

| Fase | Función | Ejemplo |
|------|---------|---------|
| **Authentication** (Autenticación) | Verificar la identidad del usuario | Introducir usuario/contraseña + código 2FA. El servidor AAA valida las credenciales y devuelve un token. |
| **Authorization** (Autorización) | Verificar los permisos del usuario para acceder a un recurso específico | El router compara el token contra políticas y decide si el usuario puede acceder al servidor solicitado. |
| **Accounting** (Contabilidad) | Registrar qué hace el usuario: qué datos envía, recibe, a qué accede, cuándo | El router registra (log) todo el tráfico entre el usuario y el servidor. |

**Proceso típico:** Host *A* intenta conectar al servidor *D*. El router *C* intercepta la solicitud y la envía al servidor AAA (*B*), que desafía al usuario con autenticación. Si es válida, devuelve un token. El router *C* evalúa el token contra las políticas de autorización. Si está autorizado, permite el tráfico y lo registra (accounting).

#### Factores de autenticación y MFA

Los sistemas de autenticación se basan en tres factores:

| Factor | Tipo | Ejemplos |
|--------|------|----------|
| **Something you know** | Conocimiento | Contraseña, passphrase, PIN |
| **Something you have** | Posesión | Teléfono móvil, hardware token, USB key, app de autenticación |
| **Something you are** | Biométrico | Huella dactilar, reconocimiento facial, iris |

- **2FA (Two-Factor Authentication):** Combina dos factores, normalmente "algo que sabes" + "algo que tienes".
- **MFA (Multi-Factor Authentication):** Utiliza dos o más factores de categorías diferentes. Es el estándar recomendado porque las contraseñas solas son la forma más débil de autenticación.

**Formas comunes de 2FA:**

| Método | Cómo funciona | Vulnerabilidad |
|--------|---------------|----------------|
| **Código SMS** | Código enviado por texto al teléfono | Clonación/intercambio de SIM, robo de teléfono |
| **Token rotativo (app/hardware)** | App o dispositivo genera código cada ~60 segundos, sincronizado con el servidor | Pérdida del dispositivo |
| **Push notification** | La app del servicio envía notificación al móvil que el usuario debe aprobar | Fatiga de notificaciones, aprobación accidental |

**Sistemas passwordless:** Eliminan "algo que sabes" y combinan "algo que tienes" (dispositivo físico) + "algo que eres" (biométrico). Los sistemas biométricos **no almacenan imágenes** del rostro o huella, sino un **hash criptográfico** derivado de ellas.

#### Complejidad de contraseñas

La **fortaleza** de una contraseña se mide en **entropy bits**: cuántos intentos necesitaría un ataque de fuerza bruta para descubrirla.

**Regla clave:** Una vez incluido un mínimo de variación (mayúsculas, símbolos, números), la **longitud es el factor más importante**. Un password de 15 caracteres con poca variación es más seguro que uno de 10 con mucha variación.

**Directrices:**
- Mínimo 8 caracteres; más largo = más fuerte
- Nunca reutilizar contraseñas entre sistemas
- Evitar información personal fácil de adivinar
- Evitar repetición de caracteres
- Usar password managers para generar contraseñas fuertes y únicas
- Passphrases: combinar 3-4 palabras sin sentido separadas por símbolos → fáciles de recordar, difíciles de adivinar

**¿Cambiar contraseñas periódicamente?** Su utilidad se cuestiona porque los atacantes modernos instalan backdoors en días. Pero es **obligatorio** cambiarlas tras una filtración (breach) de un fichero de contraseñas.

#### Identity stores (Active Directory)

Los servidores AAA raramente almacenan directamente las credenciales. En su lugar, consultan un **identity store**: una aplicación especializada que centraliza servicios de AAA, directorio de usuarios, control de acceso a edificios, y sistemas de comunicación internos.

| Identity Store | Descripción |
|---------------|-------------|
| **Active Directory (AD)** | Servicio de directorio de Microsoft para redes Windows. El más ampliamente desplegado. El servidor que ejecuta AD DS proporciona AAA, directorio ligero (LDAP) y otros servicios. |
| **OpenLDAP** | Alternativa open-source. Más complejo de configurar y gestionar. |
| **JumpCloud** | Identity store basado en SaaS (nube). |

#### Amenazas y vulnerabilidades

| Término | Definición |
|---------|------------|
| **Attack surface** | Toda superficie donde la red conecta con el exterior, con usuarios, o donde interactúan humanos y ordenadores. Cada interfaz, software, hardware y punto de conexión es superficie de ataque. |
| **Vulnerability** | Punto de ataque posible contra un sistema defensivo. Se clasifican mediante el sistema **CVE** (Common Vulnerabilities and Exposures) de MITRE: exploitability, tipo de acceso necesario, acceso obtenido, difusión del software, disponibilidad de parche. |
| **Zero day** | Vulnerabilidad previamente desconocida sin mitigación disponible. |
| **Threat** | Violación potencial de la seguridad. Puede incluir información sobre los objetivos del atacante y la vulnerabilidad que planea explotar. |
| **Threat actor** | Persona u organización detrás de la amenaza o ataque. |
| **Exploit** | Herramienta que permite a un atacante explotar una vulnerabilidad. Se venden en bibliotecas en Internet. |
| **Risk** | Evento potencial que puede interrumpir operaciones: combina la existencia de threat actors, exploits disponibles, vulnerabilidades en la superficie de ataque, y evaluación del daño potencial. |

#### Tabla de tipos de amenazas y ataques

| Tipo de ataque | Descripción | Objetivo |
|---------------|-------------|----------|
| **Social engineering** | Manipular a personas para que entreguen credenciales, permitan acceso físico, o realicen acciones perjudiciales. Incluye tailgating, pretextos, deepfakes, LLMs para crafting de emails. | Obtener beachhead (punto de acceso inicial) en la red |
| **Spam** | Correo no solicitado (publicidad, newsletters, estafas) enviado masivamente a muchas personas. **No personalizado.** | Distribución masiva: instalar malware, robar datos, generar clics |
| **Phishing** | Correo personalizado al destinatario. El atacante investiga a la víctima e imita organizaciones de confianza (Google, bancos). **Personalizado.** | Obtener credenciales, instalar malware, acceder a cuentas |
| **Malware** | Software autorreplicante: virus, gusanos, spyware, keyloggers. Tres acciones principales: impedir acceso a datos (ransomware/wiper), registrar interacciones (keylogger), filtrar datos. Se propaga por red, webs infectadas, USB, cadena de suministro. | Disrupción, robo de datos, extorsión |
| **Ransomware** | Subtipo de malware que cifra los datos del usuario con una clave desconocida. Exige pago (ransom) para entregar la clave de descifrado. | Extorsión directa |
| **Supply chain attack** | Acceso a la red a través de un elemento de la cadena de suministro (proveedor HVAC de Target, código de SolarWinds, Exchange Server de Microsoft). Muy difíciles de detectar. | Acceso masivo a múltiples organizaciones |
| **MITM (Man-in-the-Middle)** | El atacante se interpone entre dos partes, descifrando y re-cifrando el tráfico transparentemente. Puede ver datos en claro e inyectar contenido malicioso. | Interceptar credenciales, datos, inyectar malware |
| **DoS (Denial of Service)** | Agotar un recurso finito para denegar el uso de un servicio. Lanzado desde pocos dispositivos. **No requiere acceso previo a la red.** | Tumbar un servicio, distraer al equipo de seguridad, dañar reputación |
| **DDoS (Distributed DoS)** | DoS lanzado desde cientos/miles de dispositivos distribuidos (botnet). | Consumir ancho de banda o recursos a gran escala |
| **DDoS directo (burner)** | Los dispositivos del botnet envían tráfico directamente a la víctima con sus IPs reales. "Quema" el botnet (los dispositivos quedan expuestos). **Sin spoofing de dirección.** | Saturar enlaces e interfaces del objetivo por volumen |
| **DDoS reflexión** | El botnet envía tráfico con IP origen falsificada (spoofed = IP de la víctima) a servidores legítimos (por ejemplo, DNS). Estos responden con paquetes grandes hacia la víctima. **Amplifica** el ataque. No "quema" el botnet. | Amplificar tráfico hacia la víctima sin exponer el botnet |
| **Resource exhaustion** | Agotar recursos específicos: caché DNS de servidor recursivo, caché TCP de sesiones half-open, caché NAT. | Denegar servicio sin necesitar gran ancho de banda |

#### Lateral movement y acciones post-intrusión

Una vez dentro de la red, el atacante se mueve lateralmente usando cachés DNS/ARP locales, credenciales almacenadas en navegadores, y exploits contra software interno. Las acciones principales son:

- **C2 (Command and Control):** Instalar un sistema de comunicación periódica con un servidor externo para mantener el acceso persistente.
- **Data exfiltration:** Copiar datos sensibles fuera de la red (vía VPN custom, USB, consultas DNS). Pueden venderse o usarse como extorsión.
- **Ransomware:** Cifrar datos in situ y exigir rescate.

#### Cifrado (Encryption)

El cifrado se usa para cuatro propósitos fundamentales: **confidencialidad** (mantener datos privados), **integridad** (detectar modificaciones), **nonrepudiation** (probar que alguien envió algo), y **autenticación** (probar identidad).

| Tipo | Nombre | Claves | Ventajas | Desventajas |
|------|--------|--------|----------|-------------|
| **Simétrico** (Shared/Secret key) | AES, TKIP | Una sola clave compartida entre emisor y receptor | Rápido, eficiente, implementable en hardware | Si el atacante obtiene la clave, puede descifrar y falsificar |
| **Asimétrico** (Public key) | RSA, ECC | Par de claves: pública (publicada) + privada (secreta). Lo cifrado con una solo se descifra con la otra. | No requiere compartir secreto. Funciona en redes abiertas. Permite firmas criptográficas. | Más lento, más complejo, computacionalmente costoso. Solo para bloques pequeños. |

**Uso combinado en la práctica:** Los protocolos seguros (HTTPS, TLS, QUIC) usan criptografía asimétrica para **intercambiar una clave de sesión** (session key), y después usan criptografía simétrica para **cifrar el flujo de datos** (más rápido y eficiente).

**Firmas criptográficas (Cryptographic hashes):** El emisor genera un hash del contenido usando su clave privada. El receptor genera otro hash con la clave pública del emisor. Si coinciden: los datos no han sido alterados (integridad) y fueron enviados por el emisor declarado (nonrepudiation). Los hashes son repetibles pero **no reversibles** — no puedes recuperar los datos originales a partir del hash.

#### Certificados

En el contexto del establecimiento de sesiones seguras (TLS, QUIC), un **certificate** (certificado) contiene información sobre el host/servidor y se intercambia durante la conexión junto con la clave y el cipher (algoritmo de cifrado). Los certificados permiten verificar la identidad del servidor con el que te comunicas. **DKIM** en email es un ejemplo práctico: el servidor de correo firma los campos del mensaje con su clave privada, y el receptor verifica la firma usando la clave pública publicada en DNS.

#### Contramedidas anti-spam y anti-phishing

| Mecanismo | Función |
|-----------|---------|
| **DKIM** (DomainKeys Identified Mail) | El servidor emisor firma campos del email (from, to, body, subject) con su clave privada. El receptor verifica con la clave pública del emisor (publicada en DNS). Si no coinciden, el email fue alterado. |
| **SPF** (Sender Policy Framework) | Registro DNS que lista las IPs autorizadas para enviar correo desde un dominio. Si el emisor no está en la lista, el email se descarta. |
| **DMARC** | Política del dominio emisor que combina DKIM + SPF. El receptor verifica el email contra estas políticas. |
| **Spam filter** | Busca palabras clave, frases, adjuntos sospechosos, enlaces sospechosos, HTML malicioso. Asigna una puntuación de spam; si supera el umbral, se marca como spam. |

**Detección manual de phishing:** Verificar la dirección del destinatario (¿es la tuya?), copiar y pegar la dirección del remitente en un editor de texto (¿el dominio coincide con los enlaces?), **nunca clicar enlaces directamente** (copiar el enlace, verificar el dominio real), no abrir adjuntos de remitentes desconocidos. Si es sospechoso, buscar el dominio en Whois y reportar al contacto de abuse.

---

### 6.3 — Seguridad inalámbrica básica en un router doméstico

🔑 *Analogía:* WEP es como una cerradura antigua que cualquier ladrón con un clip puede abrir. WPA-PSK es como una cerradura moderna con llave compartida entre los vecinos — segura pero si uno la pierde, todos están en riesgo. WPA Enterprise es como un edificio con recepción: cada residente tiene su propia tarjeta de acceso emitida por un servidor central.

#### Evolución: WEP → WPA → WPA2 → WPA3

| Protocolo | Año | Claves | Características | Estado |
|-----------|-----|--------|-----------------|--------|
| **WEP** | 1999 | 64/128 bits | Diseñado para ofrecer seguridad equivalente a conexión cableada. Ataques viables descubiertos rápidamente. | **Retirado en 2004** por la Wi-Fi Alliance. No usar nunca. Reemplazar cualquier AP que solo soporte WEP. |
| **WPA** | 2003 | 256 bits | Tres mejoras sobre WEP: (1) claves de 256 bits, (2) **message integrity code** (MIC) en cada paquete para detectar manipulación, (3) **autenticación** de usuarios/hosts (no solo cifrado). | Superado por WPA2/WPA3 |
| **WPA2** | 2004 | 256 bits | Versión más segura de WPA. Mejoras en cifrado y protocolos de autenticación. Estándar durante muchos años. | Ampliamente usado, pero reemplazado por WPA3 |
| **WPA3** | 2018 | 256+ bits | Versión más segura que WPA2. Mejoras en protección contra ataques offline de diccionario, cifrado individual por sesión. | Recomendado |

#### Personal vs. Enterprise

| Modo | Clave inicial | Requisitos | Uso recomendado |
|------|---------------|------------|-----------------|
| **WPA-PSK (Personal)** | Pre-Shared Key: la clave pública se genera a partir del SSID y otra información conocida. Todos los dispositivos usan la misma contraseña. | Solo el AP. No requiere infraestructura adicional. | **Redes domésticas** y pequeñas oficinas |
| **WPA Enterprise** | La clave pública la proporciona un **servidor externo** (RADIUS). Cada usuario tiene credenciales individuales. | Servidor de autenticación externo (RADIUS). | **Redes corporativas** donde se necesita autenticación individual |

**¿Por qué Enterprise es más seguro?** Porque el atacante no conoce la información utilizada para generar la clave pública inicial. En PSK, la clave se deriva del SSID (público) y la contraseña compartida.

#### Proceso de cifrado WPA

1. Al iniciar la sesión entre un dispositivo y el AP, se selecciona una clave pública (vía PSK o servidor Enterprise).
2. El AP usa esta clave pública para **intercambiar claves privadas** (session keys).
3. Las claves privadas se usan para cifrar los datos que viajan por el aire.
4. Los operadores deben **cambiar la clave privada regularmente**.

Para espiar una conexión WPA, un atacante necesitaría descubrir la clave actual **y** predecir la siguiente — posible pero muy difícil.

#### SSID y buenas prácticas

**SSID (Service Set Identifier):** Nombre que identifica una red Wi-Fi. No está vinculado a un AP ni a un canal específico; es un **conjunto de servicios**. Cada SSID representa un **dominio de broadcast separado** (equivalente a una VLAN).

**Buenas prácticas para redes domésticas:**

- **Cambiar siempre** el SSID y la contraseña por defecto de fábrica.
- Seleccionar una contraseña **larga** (la longitud importa más que los símbolos) y fácil de recordar.
- **Siempre usar cifrado** — sin él, cualquiera que reciba la señal puede capturar los datos (wardriving).
- Usar **WPA-PSK** como mínimo; WPA2 o WPA3 preferido.
- Considerar crear SSIDs separados: uno principal (hosts, streaming) con acceso a la red interna, y uno **guest** (invitados, IoT) con acceso solo a Internet.
- Las redes con SSID oculto (no emitido) requieren introducir manualmente el nombre para conectarse.

#### Configuración Wi-Fi en hosts

En todos los sistemas operativos (Windows, macOS, Android, iOS), la configuración básica es:

1. Seleccionar la red Wi-Fi (SSID) de la lista de redes disponibles.
2. Introducir la contraseña.
3. Conectar.

Opciones adicionales relevantes: auto-conexión a redes conocidas, **Random hardware address** (MAC aleatoria para evitar tracking entre redes), red pública vs. privada (Windows: pública = no anuncia presencia ni permite conexiones entrantes).

---

## 🎯 Puntos críticos para el examen

- **Tríada CIA:** Confidentiality (proteger del acceso no autorizado), Integrity (datos no modificados), Availability (recursos accesibles). Los métodos de protección se solapan (encryption, segmentation, access control, monitoring aparecen en las tres).
- **AAA:** Authentication = verificar identidad. Authorization = verificar permisos. Accounting = registrar actividad. Son tres fases secuenciales, no intercambiables.
- **Tres factores de autenticación:** Something you know (contraseña), something you have (token/teléfono), something you are (biométrico). **MFA** = combinar factores de categorías diferentes. Contraseñas = factor más débil.
- **Password strength:** La **longitud** es el factor más importante una vez incluida variación mínima. Se mide en entropy bits. Password de 15 caracteres con poca variación > password de 10 con mucha variación.
- **Active Directory:** Identity store más desplegado. Servicio de directorio de Microsoft que proporciona AAA y directorio LDAP.
- **Cifrado simétrico:** Una sola clave compartida. Rápido. Usado para cifrar datos en flujo. **Asimétrico:** Par de claves pública/privada. Lento. Usado para intercambiar claves de sesión y crear firmas. Los protocolos reales **combinan ambos**.
- **Certificados:** Contienen información del host, se intercambian al establecer conexiones seguras. Permiten verificar la identidad del servidor.
- **Cryptographic hash:** Firma repetible pero no reversible. Sirve para autenticación, validación de integridad y nonrepudiation.
- **Firewalls stateful:** "Espejo unidireccional" — permiten tráfico de sesiones iniciadas desde dentro, bloquean conexiones nuevas desde fuera. Clave: rastrean el **estado de la conexión TCP** (SYN → SYN-ACK → ACK).
- **Access lists (ACL):** Reglas permit/deny evaluadas en orden. **Deny implícito** al final si no hay coincidencia. Siempre terminar con `permit ip any any` si quieres permitir el resto.
- **Spam vs. Phishing:** Spam = masivo, no personalizado. Phishing = personalizado al destinatario. Ambos son social engineering.
- **DoS vs. DDoS:** DoS = pocos dispositivos, agota recursos locales. DDoS = cientos/miles de dispositivos (botnet). **Directo** = IPs reales, "quema" botnet, sin spoofing. **Reflexión** = IPs falsificadas, amplificación vía servidores DNS, no "quema" botnet.
- **Malware:** Software autorreplicante. Tres acciones: impedir acceso (ransomware), registrar interacciones (keylogger), filtrar datos.
- **MITM:** Atacante entre dos partes, descifra y re-cifra transparentemente. Puede ver datos en claro e inyectar contenido.
- **Supply chain attack:** Entrada vía proveedor o software de terceros. Ejemplos: Target (HVAC), SolarWinds (código infectado), Microsoft Exchange (backdoor).
- **WEP = NUNCA usar** (retirado 2004). WPA ≥ WPA2 ≥ WPA3 en orden de seguridad creciente.
- **WPA Personal (PSK):** Clave compartida derivada del SSID. Para hogares. **WPA Enterprise:** Clave de servidor RADIUS. Para empresas. Enterprise es más seguro porque el atacante no conoce los datos usados para la clave pública.
- **WPA mejoras sobre WEP:** (1) claves de 256 bits, (2) MIC (integridad), (3) autenticación de usuarios.
- **SSID:** Identifica la red Wi-Fi. Cada SSID = dominio de broadcast separado. Cambiar siempre el SSID y contraseña por defecto.
- **Defense in depth:** Múltiples capas de defensa con vulnerabilidades diferentes. Nunca una sola línea.
- **Zero trust:** No hay "dentro" ni "fuera" de la red. Autenticación continua para cada acceso a cada recurso.
- **Shift left:** Integrar seguridad desde el diseño, no solo en operación.
- **DKIM/SPF/DMARC:** Mecanismos de verificación de email. DKIM firma campos del mensaje. SPF lista IPs autorizadas. DMARC combina ambos como política.

---

## Mini-resumen

- **Firewalls (6.1):** Las ACL definen reglas `permit`/`deny` por IP origen/destino, protocolo y puerto. Deny implícito al final. El filtrado **stateful** rastrea el estado TCP y funciona como espejo unidireccional (permite respuestas, bloquea conexiones nuevas de fuera). El filtrado **contextual** (WAF, IDS) inspecciona contenido con conocimiento de la aplicación. Un firewall moderno combina stateful + IDS + NAT + filtrado por puerto/dirección. **Defense in depth** = múltiples capas defensivas con vulnerabilidades diferentes.
- **Conceptos de seguridad (6.2):** **CIA** = confidencialidad + integridad + disponibilidad; métodos comunes: encryption, segmentation, access control, monitoring, resilience. **AAA** = autenticación (verificar identidad) → autorización (verificar permisos) → accounting (registrar actividad). **MFA** combina factores de distintas categorías (know/have/are); contraseñas = factor más débil; longitud > variación en password strength. **Active Directory** = identity store más desplegado (Microsoft). **Cifrado simétrico** (una clave, rápido, datos en flujo) + **asimétrico** (par de claves, lento, intercambio de claves y firmas) se combinan en protocolos reales. **Certificates** verifican identidad del servidor. **Hashes** = firmas no reversibles para integridad/nonrepudiation. **Amenazas:** social engineering (spam=masivo, phishing=personalizado), malware (autorreplicante: ransomware, keyloggers, wipers), supply chain attacks (vía proveedores), MITM (interceptación transparente), DoS/DDoS (agotar recursos; directo=IPs reales, reflexión=IPs falsificadas+amplificación). **Lateral movement** → C2 → data exfiltration → ransomware. **Zero trust** = autenticación continua sin asumir perímetro. **DKIM/SPF/DMARC** = defensa a nivel de email.
- **Seguridad Wi-Fi (6.3):** WEP retirado (2004), nunca usar. **WPA** (2003): claves 256-bit, MIC, autenticación de usuarios — tres mejoras sobre WEP. **WPA2** más seguro que WPA. **WPA3** más seguro que WPA2. **Personal (PSK):** clave compartida, para hogares. **Enterprise:** servidor RADIUS, credenciales individuales, para empresas, más seguro. Siempre cambiar SSID y contraseña por defecto. Siempre usar cifrado (mínimo WPA-PSK). Crear SSIDs separados para red interna y guest. SSID = dominio de broadcast separado.
