<img width="835" height="550" alt="image" src="https://github.com/user-attachments/assets/73c25dcc-8dbf-4bab-b4e5-a5c20ce8c104" /># CCST Networking 100-150 — Preguntas de práctica
## Dominio 6: Security (30 preguntas)

---

**Pregunta 1. [Multiple Choice — Single Answer]**

Un firewall stateful recibe un paquete TCP SYN desde un host externo intentando iniciar una conexión hacia un servidor interno, sin que ningún host interno haya iniciado esa conversación previamente. ¿Qué acción toma el firewall?

A) Permite el paquete porque es un SYN válido

B) Descarta el paquete porque no existe un estado previo de conexión iniciada desde dentro

C) Reenvía el paquete al servidor DNS para validación

D) Reenvía el paquete porque no existe un estado previo de conexión iniciada desde dentro

<details>
<summary>Respuesta</summary>
✅ Correcta: B) Descarta el paquete porque no existe un estado previo de conexión iniciada desde dentro

💡 Explicación: El filtrado stateful funciona como un espejo unidireccional: permite tráfico de sesiones iniciadas desde la red interna y bloquea conexiones nuevas iniciadas desde fuera. Si no hay un estado previo (un SYN saliente registrado), el firewall descarta el paquete entrante porque no corresponde a ninguna conversación legítima.
</details>

---

**Pregunta 2. [Multiple Choice — Single Answer]**

¿Cuáles son los tres pilares de la tríada CIA en seguridad de la información?

A) Connectivity, Integration, Authentication

B) Confidentiality, Integrity, Availability

C) Certification, Identity, Authorization

D) Control, Inspection, Access

<details>
<summary>Respuesta</summary>
✅ Correcta: B) Confidentiality, Integrity, Availability

💡 Explicación: La tríada CIA define los tres objetivos fundamentales de seguridad: Confidentiality (proteger datos del acceso no autorizado), Integrity (asegurar que los datos no han sido modificados), y Availability (garantizar que los recursos están accesibles cuando se necesitan). Los métodos de protección (encryption, segmentation, access control, monitoring) se solapan entre los tres pilares.
</details>

---

**Pregunta 3. [Multiple Choice — Single Answer]**

Un empleado recibe un correo electrónico que parece venir de su banco, dirigido a él por su nombre completo, mencionando transacciones recientes reales, y pidiéndole que haga clic en un enlace para "verificar su identidad". ¿Qué tipo de ataque describe este escenario?

A) Spam

B) Phishing

C) DoS

D) Supply chain attack

<details>
<summary>Respuesta</summary>
✅ Correcta: B) Phishing

💡 Explicación: El phishing se distingue del spam porque es personalizado al destinatario: el atacante investiga a la víctima e imita organizaciones de confianza. El correo está dirigido por nombre, menciona datos reales y solicita credenciales — todas señales de phishing. El spam es masivo y no personalizado. Un DoS busca tumbar un servicio, y un supply chain attack entra vía proveedores.
</details>

---

**Pregunta 4. [Multiple Choice — Single Answer]**

¿Qué protocolo de seguridad Wi-Fi fue retirado en 2004 por la Wi-Fi Alliance y nunca debe utilizarse?

A) WPA

B) WPA2

C) WEP

D) WPA3

<details>
<summary>Respuesta</summary>
✅ Correcta: C) WEP

💡 Explicación: WEP (Wired Equivalent Privacy, 1999) fue retirado en 2004 porque se descubrieron rápidamente ataques viables contra él. Usaba claves de solo 64/128 bits. Cualquier AP que solo soporte WEP debe ser reemplazado. WPA (2003), WPA2 (2004) y WPA3 (2018) son las alternativas seguras, en orden de seguridad creciente.
</details>

---

**Pregunta 5. [Multiple Choice — Single Answer]**

¿Qué ocurre si un paquete no coincide con ninguna regla de una access list (ACL) en un router Cisco?

A) El paquete se permite por defecto

B) El paquete se descarta (deny implícito al final de toda ACL)

C) El paquete se reenvía al administrador para revisión manual

D) El paquete se almacena en buffer hasta que se añada una regla

<details>
<summary>Respuesta</summary>
✅ Correcta: B) El paquete se descarta (deny implícito al final de toda ACL)

💡 Explicación: Toda access list tiene una regla implícita final que descarta cualquier paquete que no coincida con ninguna regla explícita (deny implícito). Por eso, si se quiere permitir el resto del tráfico, la ACL debe terminar con `permit ip any any`. Sin esta regla final, todo lo no especificado será bloqueado.
</details>

---

**Pregunta 6. [Multiple Choice — Single Answer]**

En el proceso AAA, ¿cuál es la función de la fase de Authorization?

A) Verificar la identidad del usuario mediante credenciales

B) Verificar los permisos del usuario para acceder a un recurso específico

C) Registrar qué datos envía y recibe el usuario

D) Cifrar la comunicación entre el usuario y el servidor

<details>
<summary>Respuesta</summary>
✅ Correcta: B) Verificar los permisos del usuario para acceder a un recurso específico

💡 Explicación: AAA tiene tres fases secuenciales: Authentication verifica la identidad del usuario (A es falsa porque describe Authentication). Authorization verifica los permisos del usuario autenticado para acceder a recursos específicos. Accounting registra toda la actividad del usuario (C describe Accounting). Las tres fases son distintas y no intercambiables.
</details>

---

**Pregunta 7. [Multiple Choice — Single Answer]**

Una empresa detecta que sus archivos han sido cifrados por un software malicioso que exige un pago para entregar la clave de descifrado. ¿Qué tipo de malware describe este escenario?

A) Keylogger

B) Wiper

C) Ransomware

D) Spyware

<details>
<summary>Respuesta</summary>
✅ Correcta: C) Ransomware

💡 Explicación: Ransomware es un subtipo de malware que cifra los datos del usuario con una clave desconocida y exige un pago (ransom) para entregar la clave de descifrado. Un keylogger registra las pulsaciones de teclado, un wiper destruye datos sin posibilidad de recuperación, y un spyware recopila información sin conocimiento del usuario.
</details>

---

**Pregunta 8. [Multiple Choice — Single Answer]**

¿Qué factor de autenticación representa una huella dactilar o el reconocimiento facial?

A) Something you know (algo que sabes)

B) Something you have (algo que tienes)

C) Something you are (algo que eres)

D) Something you share (algo que compartes)

<details>
<summary>Respuesta</summary>
✅ Correcta: C) Something you are (algo que eres)

💡 Explicación: Los tres factores de autenticación son: something you know (contraseña, PIN), something you have (teléfono, token hardware), y something you are (biométrico: huella dactilar, reconocimiento facial, iris). La huella y el reconocimiento facial son biométricos — "algo que eres". Los sistemas biométricos no almacenan la imagen sino un hash criptográfico derivado de ella.
</details>

---

**Pregunta 9. [Multiple Choice — Single Answer]**

¿Qué ventaja tiene WPA Enterprise sobre WPA-PSK (Personal)?

A) WPA Enterprise no necesita contraseña para conectarse

B) WPA Enterprise usa un servidor RADIUS

C) WPA Enterprise usa claves de 64 bits que son más rápidas de procesar

D) WPA Enterprise no requiere ninguna infraestructura adicional

<details>
<summary>Respuesta</summary>
✅ Correcta: B) WPA Enterprise usa un servidor RADIUS

💡 Explicación: En WPA-PSK, la clave se deriva del SSID (público) y una contraseña compartida, lo que da al atacante información parcial. En WPA Enterprise, la clave pública la proporciona un servidor RADIUS con credenciales individuales por usuario, así que el atacante no conoce los datos usados para generar la clave. Enterprise sí requiere infraestructura adicional (servidor RADIUS).
</details>

---

**Pregunta 10. [Multiple Choice — Single Answer]**

Un atacante envía tráfico masivo a servidores DNS públicos con la dirección IP origen falsificada (spoofed) de la víctima. Los servidores DNS responden con paquetes grandes dirigidos a la víctima. ¿Qué tipo de ataque describe este escenario?

A) DoS por resource exhaustion

B) DDoS directo (burner)

C) DDoS por reflexión

D) MITM

<details>
<summary>Respuesta</summary>
✅ Correcta: C) DDoS por reflexión

💡 Explicación: En un DDoS por reflexión, el botnet envía tráfico con IP origen falsificada (la IP de la víctima) a servidores legítimos (como DNS). Estos responden con paquetes grandes hacia la víctima, amplificando el ataque. No "quema" el botnet porque las IPs reales del botnet nunca se exponen. En un DDoS directo, los dispositivos envían tráfico con sus IPs reales, quedando expuestos.
</details>

---

**Pregunta 11. [Multiple Choice — Single Answer]**

¿Cuál es el identity store más ampliamente desplegado en redes corporativas para proporcionar AAA y directorio LDAP?

A) OpenLDAP

B) JumpCloud

C) Active Directory

D) RADIUS standalone

<details>
<summary>Respuesta</summary>
✅ Correcta: C) Active Directory

💡 Explicación: Active Directory (AD) es el servicio de directorio de Microsoft y el identity store más ampliamente desplegado. El servidor que ejecuta AD DS proporciona AAA, directorio ligero (LDAP) y otros servicios para redes Windows. OpenLDAP es una alternativa open-source más compleja, y JumpCloud es un identity store SaaS basado en la nube.
</details>

---

**Pregunta 12. [Multiple Choice — Single Answer]**

Un administrador configura la siguiente ACL en un router Cisco:

```
access-list 101 deny tcp any host 10.0.0.5 eq 23
access-list 101 permit ip any any
```

¿Qué efecto tiene esta configuración?

A) Bloquea todo el tráfico hacia 10.0.0.5

B) Bloquea solo el tráfico Telnet (TCP puerto 23) hacia 10.0.0.5 desde cualquier origen, y permite todo lo demás

C) Permite solo el tráfico Telnet (TCP puerto 23) hacia 10.0.0.5 desde cualquier origen, y bloquea todo lo demás

D) Bloquea todo el tráfico excepto Telnet (TCP puerto 23)

<details>
<summary>Respuesta</summary>
✅ Correcta: B) Bloquea solo el tráfico Telnet (TCP puerto 23) hacia 10.0.0.5 desde cualquier origen, y permite todo lo demás

💡 Explicación: La primera regla deniega TCP puerto 23 (Telnet) desde cualquier origen (any) hacia el host 10.0.0.5. La segunda regla permite todo el resto del tráfico IP (any a any). Sin la segunda regla, el deny implícito al final de la ACL bloquearía todo lo demás. Las reglas se evalúan en orden: primero se comprueba la coincidencia con Telnet, y si no coincide, se aplica el permit general.
</details>

---

**Pregunta 13. [Multiple Choice — Single Answer]**

En el contexto de fortaleza de contraseñas, ¿cuál es el factor más importante una vez incluida una variación mínima de caracteres?

A) El uso de exactamente 3 símbolos especiales

B) La longitud de la contraseña

C) Cambiar la contraseña cada 24 horas

D) Usar solo números para facilitar la memorización

<details>
<summary>Respuesta</summary>
✅ Correcta: B) La longitud de la contraseña

💡 Explicación: La fortaleza de una contraseña se mide en entropy bits. Una vez incluido un mínimo de variación (mayúsculas, símbolos, números), la longitud es el factor más importante. Un password de 15 caracteres con poca variación es más seguro que uno de 10 con mucha variación. Se recomienda un mínimo de 8 caracteres, nunca reutilizar contraseñas, y usar password managers.
</details>

---

**Pregunta 14. [Multiple Choice — Single Answer]**

¿Qué principio de seguridad establece que nunca se debe depender de una sola línea de defensa, sino que el atacante debe atravesar múltiples capas defensivas con vulnerabilidades diferentes?

A) Zero trust

B) Shift left

C) Defense in depth

D) Single sign-on

<details>
<summary>Respuesta</summary>
✅ Correcta: C) Defense in depth

💡 Explicación: Defense in depth establece que múltiples capas de defensa (segmentación, 2FA para la red, 2FA para la aplicación, ACLs, monitorización, logging) deben proteger los recursos. Cada capa tiene vulnerabilidades diferentes, de modo que un atacante que supere una capa aún debe enfrentarse a las demás. Zero trust (A) elimina la confianza implícita en cualquier usuario/dispositivo. Shift left (B) integra seguridad desde el diseño.
</details>

---

**Pregunta 15. [Multiple Choice — Single Answer]**

¿Cuáles son las tres mejoras que WPA introdujo sobre WEP?

A) Cifrado AES, autenticación RADIUS y firewall integrado

B) Claves de 256 bits, MIC en cada paquete y autenticación de usuarios/hosts

C) Soporte para IPv6, eliminación de SSID y contraseñas de 32 caracteres obligatorias

D) Eliminación de contraseñas, autenticación biométrica y cifrado cuántico

<details>
<summary>Respuesta</summary>
✅ Correcta: B) Claves de 256 bits, MIC en cada paquete, y autenticación de usuarios/hosts

💡 Explicación: WPA (2003) introdujo tres mejoras fundamentales sobre WEP: (1) claves de 256 bits (frente a 64/128 de WEP), (2) un message integrity code (MIC) en cada paquete para detectar manipulación, y (3) autenticación de usuarios y hosts, no solo cifrado. Estas mejoras hicieron WPA significativamente más seguro que WEP.
</details>

---

**Pregunta 16. [Multiple Choice — Single Answer]**

Los protocolos seguros como HTTPS y TLS combinan dos tipos de cifrado. ¿Cómo se utilizan en la práctica?

A) Solo cifrado simétrico para todo el proceso

B) Solo cifrado asimétrico para todo el proceso

C) Cifrado asimétrico para intercambiar una clave de sesión, y cifrado simétrico para cifrar el flujo de datos

D) Cifrado simétrico para intercambiar claves, y cifrado asimétrico para cifrar los datos

<details>
<summary>Respuesta</summary>
✅ Correcta: C) Cifrado asimétrico para intercambiar una clave de sesión, y cifrado simétrico para cifrar el flujo de datos
💡 Explicación: Los protocolos reales combinan ambos tipos: usan criptografía asimétrica (par de claves pública/privada, más lenta pero no requiere compartir secreto) para intercambiar una clave de sesión de forma segura, y después usan criptografía simétrica (una sola clave compartida, más rápida) para cifrar el flujo de datos de forma eficiente.
</details>

---

**Pregunta 17. [Multiple Choice — Choose Two]**

¿Cuáles de las siguientes son características del cifrado asimétrico? (Elige dos)

A) Utiliza un par de claves: pública (publicada) y privada (secreta)

B) Usa una sola clave compartida entre emisor y receptor

C) No requiere compartir un secreto previo para establecer comunicación segura

D) Es más rápido que el cifrado simétrico y se usa para cifrar grandes volúmenes de datos

<details>
<summary>Respuesta</summary>
✅ Correcta: A) y C)

💡 Explicación: El cifrado asimétrico usa un par de claves — pública y privada (A). Lo cifrado con una solo se descifra con la otra, lo que elimina la necesidad de compartir un secreto previo (C). Es más lento y computacionalmente costoso que el simétrico (D es falsa), por lo que se usa para bloques pequeños como el intercambio de claves de sesión. La opción B describe el cifrado simétrico.
</details>

---

**Pregunta 18. [Multiple Choice — Choose Two]**
¿Cuáles de las siguientes son formas comunes de implementar 2FA (Two-Factor Authentication)? (Elige dos)

A) Token rotativo que genera un código cada ~60 segundos, sincronizado con el servidor
B) Usar dos contraseñas diferentes en el mismo formulario de login
C) Push notification que el usuario debe aprobar en su dispositivo móvil
D) Introducir el mismo PIN dos veces para confirmación

<respuesta>
✅ Correcta: A) y C)
💡 Explicación: Las formas comunes de 2FA son: código SMS (vulnerable a clonación de SIM), token rotativo de app/hardware que genera códigos cada ~60 segundos (A), y push notification en el móvil que requiere aprobación del usuario (C). 2FA requiere combinar factores de categorías diferentes (algo que sabes + algo que tienes). Usar dos contraseñas (B) o el mismo PIN dos veces (D) sigue siendo solo un factor ("algo que sabes").
</respuesta>

---

**Pregunta 19. [Multiple Choice — Choose Two]**
¿Cuáles de las siguientes son diferencias entre un DDoS directo (burner) y un DDoS por reflexión? (Elige dos)

A) En el directo, los dispositivos del botnet envían tráfico con sus IPs reales, quedando expuestos ("quemados")
B) En el directo, las IPs de los dispositivos están falsificadas (spoofed)
C) En el de reflexión, el botnet envía tráfico con la IP falsificada de la víctima a servidores legítimos que amplifican la respuesta
D) En el de reflexión, los dispositivos del botnet quedan expuestos y deben ser reemplazados

<respuesta>
✅ Correcta: A) y C)
💡 Explicación: En el DDoS directo, el botnet envía tráfico con IPs reales → los dispositivos quedan expuestos/"quemados" (A), sin spoofing. En el de reflexión, el botnet falsifica la IP origen (la IP de la víctima) y envía consultas a servidores legítimos (DNS) que responden con paquetes grandes hacia la víctima, amplificando el ataque (C). El de reflexión no "quema" el botnet porque las IPs reales nunca se exponen.
</respuesta>

---

**Pregunta 20. [Multiple Choice — Choose Two]**
Un administrador de red quiere proteger el correo electrónico corporativo contra suplantación de identidad del remitente. ¿Cuáles de los siguientes mecanismos debería implementar? (Elige dos)

A) DKIM — el servidor emisor firma los campos del email con su clave privada, y el receptor verifica con la clave pública publicada en DNS
B) PoE — alimentar los servidores de correo directamente por el cable Ethernet
C) SPF — registro DNS que lista las IPs autorizadas para enviar correo desde el dominio
D) NAT — traducir las direcciones IP del servidor de correo

<respuesta>
✅ Correcta: A) y C)
💡 Explicación: DKIM verifica la integridad del email firmando campos (from, to, body, subject) con la clave privada del servidor emisor (A). SPF publica un registro DNS con las IPs autorizadas para enviar correo del dominio, descartando emails de IPs no autorizadas (C). Juntos, con DMARC como política combinada, son la defensa estándar contra suplantación de email. PoE y NAT no tienen relación con seguridad de correo.
</respuesta>

---

**Pregunta 21. [Multiple Choice — Choose Two]**
¿Cuáles de las siguientes son buenas prácticas para la seguridad de una red Wi-Fi doméstica? (Elige dos)

A) Cambiar siempre el SSID y la contraseña por defecto de fábrica
B) Deshabilitar todo cifrado para mejorar la velocidad de conexión
C) Usar WPA-PSK como mínimo; WPA2 o WPA3 es preferible
D) Mantener el SSID y contraseña de fábrica para facilitar la reconexión de dispositivos

<respuesta>
✅ Correcta: A) y C)
💡 Explicación: Las buenas prácticas incluyen: cambiar siempre el SSID y contraseña por defecto (A) para evitar que atacantes conozcan las credenciales de fábrica, y usar siempre cifrado con WPA-PSK como mínimo (C) — sin cifrado, cualquiera puede capturar los datos (wardriving). Deshabilitar el cifrado (B) y mantener credenciales de fábrica (D) son prácticas peligrosas que exponen la red.
</respuesta>

---

**Pregunta 22. [Multiple Choice — Choose Two]**
¿Cuáles de los siguientes son ejemplos de ataques supply chain documentados? (Elige dos)

A) Un atacante accedió a la red de Target a través del proveedor de HVAC (climatización)
B) Un usuario olvidó su contraseña y fue bloqueado del sistema
C) SolarWinds distribuyó una actualización de software que contenía código malicioso a miles de organizaciones
D) Un switch perdió su tabla MAC tras un reinicio rutinario

<respuesta>
✅ Correcta: A) y C)
💡 Explicación: Los supply chain attacks entran a través de proveedores o software de terceros. Target fue comprometido vía su proveedor de HVAC (A). SolarWinds distribuyó una actualización de código infectado que afectó a miles de organizaciones (C). Microsoft Exchange Server (backdoor) es otro ejemplo documentado. Las opciones B y D son incidentes operativos normales, no ataques.
</respuesta>

---

**Pregunta 23. [Drag and Drop]**
Arrastra cada pilar de la tríada CIA a su definición correcta.

**Elementos a arrastrar:**
- Confidentiality
- Integrity
- Availability

**Categorías destino:**
- Proteger la información del acceso por partes no autorizadas
- Confianza en que los datos no han sido modificados durante almacenamiento o transmisión
- Capacidad de los usuarios de acceder a los recursos y datos que necesitan para trabajar

<respuesta>
✅ Correcta:
- Confidentiality → Proteger la información del acceso por partes no autorizadas
- Integrity → Confianza en que los datos no han sido modificados durante almacenamiento o transmisión
- Availability → Capacidad de los usuarios de acceder a los recursos y datos que necesitan para trabajar
💡 Explicación: Los tres pilares de CIA cubren aspectos complementarios de la seguridad. Confidentiality protege el acceso (cifrado, control de acceso). Integrity asegura que los datos no se alteran (hashes, cifrado). Availability garantiza que los recursos estén disponibles (resiliencia, redundancia frente a DDoS).
</respuesta>

---

**Pregunta 24. [Drag and Drop]**
Arrastra cada fase de AAA a su función.

**Elementos a arrastrar:**
- Authentication
- Authorization
- Accounting

**Categorías destino:**
- Verificar la identidad del usuario mediante credenciales
- Verificar los permisos del usuario para acceder a un recurso específico
- Registrar qué hace el usuario: qué datos envía, recibe, a qué accede y cuándo

<respuesta>
✅ Correcta:
- Authentication → Verificar la identidad del usuario mediante credenciales
- Authorization → Verificar los permisos del usuario para acceder a un recurso específico
- Accounting → Registrar qué hace el usuario: qué datos envía, recibe, a qué accede y cuándo
💡 Explicación: Las tres fases de AAA son secuenciales: primero se autentica (¿quién eres?), luego se autoriza (¿qué puedes hacer?), y finalmente se registra toda la actividad (¿qué hiciste?). En un escenario típico, el router intercepta la solicitud, el servidor AAA autentica, el router evalúa el token contra políticas de autorización, y registra todo el tráfico.
</respuesta>

---

**Pregunta 25. [Drag and Drop]**
Arrastra cada tipo de ataque a su descripción.

**Elementos a arrastrar:**
- Phishing
- Spam
- MITM
- Ransomware

**Categorías destino:**
- Correo personalizado que imita organizaciones de confianza para obtener credenciales
- Correo masivo no personalizado enviado a muchas personas (publicidad, estafas)
- Atacante entre dos partes que descifra y re-cifra tráfico transparentemente
- Malware que cifra los datos del usuario y exige pago para entregar la clave de descifrado

<respuesta>
✅ Correcta:
- Phishing → Correo personalizado que imita organizaciones de confianza para obtener credenciales
- Spam → Correo masivo no personalizado enviado a muchas personas (publicidad, estafas)
- MITM → Atacante entre dos partes que descifra y re-cifra tráfico transparentemente
- Ransomware → Malware que cifra los datos del usuario y exige pago para entregar la clave de descifrado
💡 Explicación: La diferencia clave entre spam y phishing es la personalización: spam es masivo e indiscriminado; phishing está diseñado para un destinatario específico. MITM intercepta comunicaciones sin que las partes lo noten. Ransomware es un subtipo de malware enfocado en extorsión directa mediante cifrado de datos.
</respuesta>

---

**Pregunta 26. [Drag and Drop]**
Arrastra cada protocolo de seguridad Wi-Fi a su estado actual y característica principal.

**Elementos a arrastrar:**
- WEP
- WPA
- WPA2
- WPA3

**Categorías destino:**
- Retirado en 2004, nunca usar; claves de 64/128 bits
- 2003; introdujo claves 256-bit, MIC e integridad; superado por WPA2/WPA3
- 2004; cifrado AES más robusto; ampliamente desplegado como estándar
- 2018; el más seguro; protección contra ataques offline de diccionario

<respuesta>
✅ Correcta:
- WEP → Retirado en 2004, nunca usar; claves de 64/128 bits
- WPA → 2003; introdujo claves 256-bit, MIC e integridad; superado por WPA2/WPA3
- WPA2 → 2004; cifrado AES más robusto; ampliamente desplegado como estándar
- WPA3 → 2018; el más seguro; protección contra ataques offline de diccionario
💡 Explicación: La evolución de seguridad Wi-Fi va de WEP (inseguro, retirado) → WPA (mejora significativa) → WPA2 (estándar durante años) → WPA3 (recomendado actual). Cada versión aumenta la seguridad del cifrado y la autenticación. WEP nunca es una respuesta correcta como opción de seguridad.
</respuesta>

---

**Pregunta 27. [Drag and Drop]**
Arrastra cada factor de autenticación a su categoría.

**Elementos a arrastrar:**
- Contraseña o PIN
- Teléfono móvil con app de autenticación
- Huella dactilar
- Hardware token USB

**Categorías destino:**
- Something you know (algo que sabes)
- Something you have (algo que tienes)
- Something you are (algo que eres)

<respuesta>
✅ Correcta:
- Contraseña o PIN → Something you know
- Teléfono móvil con app de autenticación → Something you have
- Huella dactilar → Something you are
- Hardware token USB → Something you have
💡 Explicación: Los factores se agrupan en tres categorías: conocimiento (contraseñas, PINs), posesión (dispositivos físicos como teléfonos, tokens USB, tarjetas) y biométricos (huella, iris, reconocimiento facial). MFA combina factores de categorías diferentes. Usar dos contraseñas sigue siendo un solo factor (know), no MFA.
</respuesta>

---

**Pregunta 28. [Hotspot]**
*Descripción: Se muestra la siguiente tabla de reglas ACL aplicada a la interfaz de entrada de un router:*

```
access-list 110 permit tcp 192.168.1.0 0.0.0.255 any eq 443
access-list 110 permit tcp 192.168.1.0 0.0.0.255 any eq 80
access-list 110 deny tcp any any eq 23
[deny implícito al final]
```

Un host con IP 192.168.1.50 intenta establecer una conexión Telnet (TCP puerto 23) hacia un servidor externo. **Señala qué regla se aplicará y qué acción se tomará.**

A) La regla 1 (permit TCP 443) — se permite la conexión
B) La regla 2 (permit TCP 80) — se permite la conexión
C) La regla 3 (deny TCP 23) — se bloquea la conexión Telnet
D) El deny implícito al final — se bloquea porque no hay regla permit para Telnet

<respuesta>
✅ Correcta: C) La regla 3 (deny TCP 23) — se bloquea la conexión Telnet
💡 Explicación: Las reglas ACL se evalúan en orden. La regla 1 no coincide (el puerto destino es 443, no 23). La regla 2 tampoco (puerto 80). La regla 3 coincide: deny TCP desde cualquier origen (any) hacia cualquier destino (any) en puerto 23. El paquete Telnet es bloqueado explícitamente. Aunque el deny implícito al final también lo bloquearía, la regla 3 explícita se aplica primero.
</respuesta>

---

**Pregunta 29. [Hotspot]**
*Descripción: Se muestra una tabla con cuatro escenarios de red Wi-Fi. Se pide identificar cuál es la configuración más segura para una red corporativa.*

| Escenario | Protocolo | Modo | Servidor externo |
|-----------|-----------|------|-----------------|
| **A** | WEP | — | No |
| **B** | WPA2 | Personal (PSK) | No |
| **C** | WPA2 | Enterprise | Sí (RADIUS) |
| **D** | WPA | Personal (PSK) | No |

**Señala el escenario que ofrece la configuración más segura para un entorno corporativo.**

<respuesta>
✅ Correcta: Escenario C — WPA2 Enterprise con servidor RADIUS
💡 Explicación: Para un entorno corporativo, WPA2 Enterprise con RADIUS (C) es la opción más segura: utiliza WPA2 (cifrado AES robusto) con modo Enterprise, donde cada usuario tiene credenciales individuales proporcionadas por un servidor RADIUS externo. El atacante no puede derivar la clave inicial. WEP (A) está retirado. WPA2-PSK (B) usa clave compartida (menos seguro que Enterprise). WPA-PSK (D) es más antiguo y menos seguro que WPA2.
</respuesta>

---

**Pregunta 30. [Hotspot]**
*Descripción: Se muestra un diagrama del proceso de filtrado stateful de un firewall con las siguientes etapas:*

| Etapa | Evento |
|-------|--------|
| **1** | Host interno A envía TCP SYN hacia servidor externo C |
| **2** | El firewall B anota la conexión y abre un "agujero" temporal |
| **3** | C responde con SYN-ACK → el firewall lo permite |
| **4** | A envía ACK → conexión TCP establecida |
| **5** | Host externo D (no solicitado) envía TCP SYN hacia A |

**Señala la etapa 5. ¿Qué acción toma el firewall B cuando el host externo D intenta iniciar una conexión no solicitada hacia A?**

A) Permite el SYN de D porque es tráfico TCP válido
B) Permite el SYN de D porque la conexión con C ya está establecida
C) Descarta el SYN de D porque no existe estado previo de una conexión iniciada por A hacia D
D) Reenvía el SYN de D al servidor AAA para autenticación

<respuesta>
✅ Correcta: C) Descarta el SYN de D porque no existe estado previo de una conexión iniciada por A hacia D
💡 Explicación: El filtrado stateful rastrea el estado de cada conexión TCP. El "agujero" temporal abierto en la etapa 2 solo permite tráfico del servidor C (con quien A inició la conversación). Cuando D intenta iniciar una conexión nueva hacia A, el firewall no encuentra estado previo — A nunca envió un SYN a D — y descarta el paquete. Cada conexión tiene su propio estado independiente. Esto es el "espejo unidireccional": permite respuestas de conexiones iniciadas desde dentro, bloquea todo lo demás desde fuera.
</respuesta>

---

✅ 30 preguntas del Dominio 6 completadas.

📊 **Desglose por objetivo:**

| Objetivo | Tema | Preguntas | Total |
|----------|------|-----------|:-----:|
| **6.1** | Firewalls: ACL, stateful, contextual, defense in depth | 1, 5, 12, 14, 28, 30 | **6** |
| **6.2** | CIA, AAA, MFA, cifrado, certificados, contraseñas, amenazas | 2, 3, 6, 7, 8, 10, 11, 13, 16, 17, 18, 19, 20, 22, 23, 24, 25, 27 | **18** |
| **6.3** | Seguridad Wi-Fi: WPA/WPA2/WPA3, Personal vs. Enterprise | 4, 9, 15, 21, 26, 29 | **6** |
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
| Fácil (40%) | **12** | 2, 4, 5, 6, 7, 8, 11, 13, 23, 24, 26, 27 |
| Medio (40%) | **12** | 1, 3, 9, 12, 14, 15, 16, 18, 21, 25, 29, 30 |
| Difícil (20%) | **6** | 10, 17, 19, 20, 22, 28 |

🔥 **Preguntas de escenario de amenaza real: 6**
→ P3 (phishing personalizado), P7 (ransomware en empresa), P10 (DDoS reflexión DNS), P12 (ACL bloqueando Telnet), P22 (supply chain Target/SolarWinds), P28 (ACL evaluada en orden)
