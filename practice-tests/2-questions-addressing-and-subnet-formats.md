## Dominio 2: Addressing and Subnet Formats (30 preguntas)

---

**Pregunta 1. [Multiple Choice — Single Answer]**

¿Cuál de los siguientes rangos de direcciones IPv4 está reservado para uso privado y NO es enrutable en Internet?

A) 172.32.0.0 – 172.47.255.255

B) 192.168.0.0 – 192.168.255.255

C) 169.254.0.0 – 169.254.255.255

D) 224.0.0.0 – 239.255.255.255

<details>
<summary>Respuesta</summary>
✅ Correcta: B) 192.168.0.0 – 192.168.255.255

💡 Explicación: Los tres rangos privados IPv4 son: 10.0.0.0/8, 172.16.0.0/12 (172.16.0.0 – 172.31.255.255) y 192.168.0.0/16. La opción A empieza en 172.32, que está fuera del rango privado (que llega solo hasta 172.31). La opción C (169.254) es link-local/APIPA, no privada. La opción D (224.0.0.0) es multicast (Clase D).
</details>

---

**Pregunta 2. [Multiple Choice — Single Answer]**

Una dirección IPv4 cuyo primer octeto es 150 pertenece históricamente a la Clase:

A) A

B) B

C) C

D) D

<details>
<summary>Respuesta</summary>
✅ Correcta: B) B

💡 Explicación: La Clase B abarca el rango de primer octeto 128–191. El valor 150 cae dentro de ese rango. Clase A es 0–127, Clase C es 192–223 y Clase D es 224–239 (multicast).
</details>

---

**Pregunta 3. [Multiple Choice — Single Answer]**

¿Cuál es la diferencia principal entre NAT y PAT?

A) NAT funciona en capa 2 y PAT funciona en capa 3

B) NAT traduce solo direcciones IP, mientras que PAT traduce direcciones IP y puertos

C) PAT traduce solo direcciones IP, mientras que NAT traduce direcciones IP y puertos

D) NAT modifica las direcciones MAC y PAT modifica las direcciones IP

<details>
<summary>Respuesta</summary>
✅ Correcta: B) NAT traduce solo direcciones IP, mientras que PAT traduce direcciones IP y puertos, permitiendo que múltiples hosts compartan una sola IP pública

💡 Explicación: NAT traduce solo direcciones (una IP pública por host interno). PAT (Port Address Translation) traduce tanto direcciones como puertos, lo que permite que muchos hosts internos compartan una sola IP pública. En la práctica, la mayoría de implementaciones son PAT, aunque se use el término "NAT" de forma genérica.
</details>

---

**Pregunta 4. [Multiple Choice — Single Answer]**

Un host arranca y no consigue contactar con ningún servidor DHCP. Se autoasigna una dirección del rango 169.254.x.x. ¿Cómo se denomina este tipo de dirección?

A) Dirección de loopback

B) Dirección multicast

C) Dirección link-local (APIPA)

D) Dirección privada de Clase A

<details>
<summary>Respuesta</summary>
✅ Correcta: C) Dirección link-local (APIPA)

💡 Explicación: El rango 169.254.0.0/16 es link-local, también conocido como APIPA (Automatic Private IP Addressing). Se autoasigna cuando DHCP falla. Loopback es 127.0.0.0/8, multicast es 224.0.0.0/4, y las direcciones privadas de Clase A son 10.0.0.0/8.
</details>

---

**Pregunta 5. [Multiple Choice — Single Answer]**

¿Cuál es la dirección IPv4 de loopback más utilizada, cuyos paquetes nunca salen del propio host?

A) 0.0.0.0

B) 127.0.0.1

C) 169.254.1.1

D) 255.255.255.255

<details>
<summary>Respuesta</summary>
✅ Correcta: B) 127.0.0.1

💡 Explicación: 127.0.0.1 es la dirección de loopback más usada (todo el rango 127.0.0.0/8 es loopback). Los paquetes enviados a esta dirección no salen del host. 0.0.0.0 representa "esta red" (usado al arrancar), 169.254.x.x es link-local/APIPA, y 255.255.255.255 es broadcast limitado.
</details>

---

**Pregunta 6. [Multiple Choice — Single Answer]**

¿Cuál es la máscara de subred equivalente al prefijo CIDR /25?

A) 255.255.255.0

B) 255.255.255.128

C) 255.255.255.192

D) 255.255.255.224

<details>
<summary>Respuesta</summary>
✅ Correcta: B) 255.255.255.128

💡 Explicación: Un prefijo /25 significa que los primeros 25 bits son 1s en la máscara. Los primeros 24 bits forman 255.255.255, y el bit 25 activa el bit más significativo del cuarto octeto (valor 128), resultando en 255.255.255.128. La opción A es /24, C es /26, y D es /27.
</details>

---

**Pregunta 7. [Multiple Choice — Single Answer]**

Dada la dirección **192.168.10.130/25**, ¿cuál es la dirección de red de la subred a la que pertenece este host?

A) 192.168.10.0

B) 192.168.10.64

C) 192.168.10.128

D) 192.168.10.192

<details>
<summary>Respuesta</summary>
✅ Correcta: C) 192.168.10.128

💡 Explicación: Para /25, el skip es 128 (2^7) y trabajamos en el cuarto octeto. Dividimos el valor del octeto entre el skip: 130 ÷ 128 = 1 (ignoramos el resto). Multiplicamos: 1 × 128 = 128. La dirección de red es 192.168.10.128. La siguiente subred empezaría en 192.168.10.256, que no existe, así que el broadcast es 192.168.10.255.
</details>

---

**Pregunta 8. [Multiple Choice — Single Answer]**

Dada la dirección **172.16.5.100/27**, ¿cuál es la dirección de broadcast de su subred?

A) 172.16.5.63

B) 172.16.5.127

C) 172.16.5.128

D) 172.16.5.255

<details>
<summary>Respuesta</summary>
✅ Correcta: B) 172.16.5.127

💡 Explicación: Para /27, el skip es 32 (2^5). Dividimos: 100 ÷ 32 = 3 (ignoramos el resto). Dirección de red: 3 × 32 = 96 → 172.16.5.96. Broadcast: 96 + 32 − 1 = 127 → 172.16.5.127. El rango de hosts utilizables es 172.16.5.97 a 172.16.5.126 (30 hosts).
</details>

---

**Pregunta 9. [Multiple Choice — Single Answer]**

¿Cuántos hosts utilizables (asignables a dispositivos) tiene una subred con prefijo /29?

A) 2

B) 6

C) 8

D) 14

<details>
<summary>Respuesta</summary>
✅ Correcta: B) 6
  
💡 Explicación: Con /29 hay 32 − 29 = 3 bits de host. El número total de direcciones es 2^3 = 8, pero se restan 2 (la dirección de red y la de broadcast), dejando 6 hosts utilizables. Esta es una subred típica para enlaces punto a punto con varios dispositivos.
</details>

---

**Pregunta 10. [Multiple Choice — Single Answer]**

¿Qué tipo de dispositivo separa dominios de broadcast, impidiendo que las tramas de broadcast se propaguen entre segmentos de red?

A) Hub

B) Switch

C) Router

D) Access Point

<details>
<summary>Respuesta</summary>
✅ Correcta: C) Router

💡 Explicación: Los routers operan en capa 3 y no reenvían broadcasts entre interfaces, por lo que separan dominios de broadcast. Los switches reenvían broadcasts a todos sus puertos, manteniéndolos dentro del mismo dominio. Los hubs también reenvían todo. Un Access Point proporciona conectividad inalámbrica sin separar dominios de broadcast.
</details>

---

**Pregunta 11. [Multiple Choice — Single Answer]**

Dada la dirección **10.128.200.0/18**, ¿cuál es la dirección de broadcast de esta subred?

A) 10.128.207.255

B) 10.128.255.255

C) 10.128.223.255

D) 10.129.255.255

<details>
<summary>Respuesta</summary>
✅ Correcta: B) 10.128.255.255

💡 Explicación: Para /18, el octeto de trabajo es el tercero. Skip = 2^(24−18) = 2^6 = 64. Dividimos: 200 ÷ 64 = 3 (ignoramos resto). Red: 3 × 64 = 192 → 10.128.192.0. Broadcast: 192 + 64 − 1 = 255, y los octetos posteriores al de trabajo van a 255 → 10.128.255.255. El host 10.128.200.0 pertenece a la subred que va de 10.128.192.0 a 10.128.255.255.
</details>

---

**Pregunta 12. [Multiple Choice — Single Answer]**

Un administrador necesita crear subredes con un prefijo /28 en el cuarto octeto. ¿Cuál es el valor del skip (intervalo entre subredes)?

A) 8

B) 16

C) 32

D) 64

<details>
<summary>Respuesta</summary>
✅ Correcta: B) 16

💡 Explicación: Para calcular el skip: los bits de host en el cuarto octeto son 32 − 28 = 4. El skip es 2^4 = 16. Esto significa que las subredes se suceden de 16 en 16: .0, .16, .32, .48, .64, etc. Cada subred /28 tiene 14 hosts utilizables.
</details>

---

**Pregunta 13. [Multiple Choice — Single Answer]**

¿Cuántos bits de longitud tiene una dirección IPv6?

A) 32

B) 48

C) 64

D) 128

<details>
<summary>Respuesta</summary>
✅ Correcta: D) 128

💡 Explicación: Una dirección IPv6 tiene 128 bits (frente a los 32 de IPv4). Se representa como 8 grupos de 4 dígitos hexadecimales separados por dos puntos. Cada grupo (quartet) representa 16 bits. 48 bits es la longitud de una dirección MAC y 64 es la parte de host estándar en IPv6, pero la dirección completa es de 128 bits.
</details>

---

**Pregunta 14. [Multiple Choice — Single Answer]**

¿Qué prefijo identifica una dirección IPv6 link-local, que se genera automáticamente en cada interfaz y no atraviesa routers?

A) 2001::/16

B) fe80::/10

C) ff00::/8

D) fc00::/7

<details>
<summary>Respuesta</summary>
✅ Correcta: B) fe80::/10

💡 Explicación: Las direcciones link-local IPv6 usan el prefijo fe80::/10 y se generan automáticamente en toda interfaz IPv6. No atraviesan routers (solo tienen alcance en el enlace local). 2001:: es un prefijo de global unicast, ff00::/8 es multicast, y fc00::/7 es unique local (ULA, equivalente a privadas IPv4).
</details>

---

**Pregunta 15. [Multiple Choice — Single Answer]**

Una dirección IPv6 que empieza por `2001:` pertenece al tipo Global Unicast. ¿Cuál es el rango de prefijo que define este tipo de direcciones?

A) fe80::/10

B) ff00::/8

C) 2000::/3

D) fc00::/7

<details>
<summary>Respuesta</summary>
✅ Correcta: C) 2000::/3

💡 Explicación: Las direcciones Global Unicast IPv6 se definen por el prefijo 2000::/3, lo que significa que comienzan por los dígitos 2 o 3 (binario 001x). Son el equivalente a las direcciones públicas IPv4, globalmente enrutables. fe80::/10 es link-local, ff00::/8 es multicast, y fc00::/7 es unique local.
</details>

---

**Pregunta 16. [Multiple Choice — Single Answer]**

¿Cuál es la forma simplificada correcta de la dirección IPv6 `2001:0db8:0000:0000:0000:0000:0100:0001`?

A) 2001:db8::100:1

B) 2001:db8:0:0:0:0:100:1

C) 2001:db8:::100:1

D) Tanto A como B son correctas

<details>
<summary>Respuesta</summary>
✅ Correcta: D) Tanto A como B son correctas

💡 Explicación: Primero se eliminan los ceros iniciales de cada quartet: 0db8→db8, 0000→0, 0100→100, 0001→1, dando 2001:db8:0:0:0:0:100:1 (opción B, válida). Luego, una cadena consecutiva de quartets todo-ceros se puede reemplazar por :: (solo una vez), dando 2001:db8::100:1 (opción A, también válida). La opción C usa ::: que es sintaxis inválida. Ambas representaciones A y B son correctas.
</details>

---

**Pregunta 17. [Multiple Choice — Choose Two]**

¿Cuáles de las siguientes direcciones IPv4 pertenecen a rangos privados? (Elige dos)

A) 10.255.1.100

B) 172.32.10.5

C) 192.168.100.50

D) 169.254.10.1

<details>
<summary>Respuesta</summary>
✅ Correcta: A) 10.255.1.100 y C) 192.168.100.50

💡 Explicación: Los tres rangos privados son 10.0.0.0/8, 172.16.0.0/12 (172.16.0.0–172.31.255.255) y 192.168.0.0/16. La opción A (10.255.1.100) está en 10.0.0.0/8 y la C (192.168.100.50) está en 192.168.0.0/16. La opción B (172.32.10.5) está fuera del rango privado (que llega solo hasta 172.31.x.x). La opción D (169.254.x.x) es link-local/APIPA, no privada.
</details>

---

**Pregunta 18. [Multiple Choice — Choose Two]**

¿Cuáles de las siguientes afirmaciones describen correctamente el funcionamiento de NAT? (Elige dos)

A) El dispositivo NAT reemplaza la dirección IP origen privada del paquete por su dirección IP pública antes de enviarlo a Internet

B) NAT opera en la capa 2 del modelo OSI modificando las direcciones MAC y consultando su tabla de traducciones para reenviar el paquete

C) Cuando llega una respuesta de Internet, el NAT consulta su tabla de traducciones para reenviar el paquete al host interno correcto

D) NAT fue diseñado exclusivamente para IPv6

<details>
<summary>Respuesta</summary>
✅ Correcta: A) y C)

💡 Explicación: NAT reemplaza la IP privada origen por la pública al salir hacia Internet (A), y cuando la respuesta vuelve, consulta su tabla de traducciones para saber a qué host interno y puerto reenviarla (C). NAT opera en capa 3 (no capa 2), y fue diseñado para extender la vida útil del espacio IPv4, no para IPv6.
</details>

---

**Pregunta 19. [Multiple Choice — Choose Two]**

Dada la subred **10.0.5.0/24**, ¿cuáles de las siguientes direcciones NO son asignables a hosts? (Elige dos)

A) 10.0.5.0

B) 10.0.5.1

C) 10.0.5.254

D) 10.0.5.255

<details>
<summary>Respuesta</summary>
✅ Correcta: A) 10.0.5.0 y D) 10.0.5.255

💡 Explicación: En una subred /24, la primera dirección (todos los bits de host a 0) es la dirección de red: 10.0.5.0. La última dirección (todos los bits de host a 1) es la dirección de broadcast: 10.0.5.255. Ninguna de las dos es asignable a hosts. 10.0.5.1 y 10.0.5.254 son el primer y último host utilizable, respectivamente.
</details>

---

**Pregunta 20. [Multiple Choice — Choose Two]**

¿Cuáles de las siguientes afirmaciones sobre dominios de broadcast son correctas? (Elige dos)

A) Todos los hosts con el mismo prefijo y longitud de prefijo pertenecen al mismo broadcast domain

B) Un switch separa dominios de broadcast al reenviar tramas de forma selectiva

C) Un router separa dominios de broadcast porque no reenvía tramas de broadcast entre sus interfaces

D) Un hub crea un dominio de broadcast independiente en cada uno de sus puertos

<details>
<summary>Respuesta</summary>
✅ Correcta: A) y C)

💡 Explicación: Un broadcast domain incluye todos los dispositivos que comparten el mismo prefijo y longitud de prefijo (A). Los routers separan broadcast domains al no reenviar broadcasts entre interfaces (C). Los switches NO separan broadcast domains (reenvían broadcasts a todos los puertos), así que B es falsa. Los hubs tampoco crean dominios independientes; reenvían todo a todos los puertos, así que D es falsa.
</details>

---

**Pregunta 21. [Multiple Choice — Choose Two]**

¿Cuáles de las siguientes son características de las direcciones IPv6 link-local? (Elige dos)

A) Se generan automáticamente en cada interfaz IPv6 y son obligatorias

B) Son enrutables globalmente en Internet, como las Global Unicast

C) Utilizan el prefijo fe80::/10

D) Reemplazan la necesidad de direcciones Global Unicast para comunicación entre sitios remotos

<details>
<summary>Respuesta</summary>
✅ Correcta: A) y C)

💡 Explicación: Las direcciones link-local se generan automáticamente en toda interfaz IPv6 (obligatorias) y usan el prefijo fe80::/10. No son enrutables más allá del enlace local (no atraviesan routers), por lo que B es falsa. No reemplazan a las Global Unicast para comunicación remota (D); cada tipo tiene su propósito específico.
</details>

---

**Pregunta 22. [Multiple Choice — Choose Two]**

¿Cuáles de las siguientes son diferencias entre IPv6 e IPv4? (Elige dos)

A) IPv6 utiliza 128 bits de longitud en sus direcciones, frente a los 32 bits de IPv4

B) IPv6 utiliza broadcast para comunicarse con todos los hosts de un segmento, igual que IPv4

C) IPv6 no tiene broadcast; toda comunicación "a todos" se realiza mediante multicast

D) IPv6 usa 4 octetos decimales separados por puntos, igual que IPv4

<details>
<summary>Respuesta</summary>
✅ Correcta: A) y C)

💡 Explicación: IPv6 usa 128 bits (A), frente a los 32 de IPv4. Además, IPv6 elimina el concepto de broadcast y lo sustituye por multicast con direcciones que empiezan por ff (C). IPv6 NO usa broadcast (B es falsa) y se representa con 8 quartets hexadecimales separados por dos puntos, no con octetos decimales (D es falsa).
</details>

---

**Pregunta 23. [Drag and Drop]**

Arrastra cada clase de dirección IPv4 al rango de primer octeto que le corresponde.

**Elementos a arrastrar:**
- Clase A
- Clase B
- Clase C
- Clase D

**Categorías destino:**
- 0 – 127
- 128 – 191
- 192 – 223
- 224 – 239

<details>
<summary>Respuesta</summary>
✅ Correcta:

- Clase A → 0 – 127

- Clase B → 128 – 191

- Clase C → 192 – 223

- Clase D → 224 – 239

💡 Explicación: Las clases IPv4 se definen por el primer octeto. Clase A (0–127) tiene prefijo /8 por defecto con ~16,7M hosts por red. Clase B (128–191) tiene /16 con ~65K hosts. Clase C (192–223) tiene /24 con 254 hosts. Clase D (224–239) se reserva para multicast.
</details>

---

**Pregunta 24. [Drag and Drop]**

Clasifica cada dirección IPv4 como Privada, Reservada o Pública.

**Elementos a arrastrar:**
- 10.50.1.200
- 203.0.113.45
- 127.0.0.1
- 172.20.5.10

**Categorías destino:**
- Privada
- Pública
- Reservada

<details>
<summary>Respuesta</summary>
✅ Correcta:

- 10.50.1.200 → Privada (rango 10.0.0.0/8)

- 203.0.113.45 → Pública (no pertenece a ningún rango privado ni reservado conocido)

- 127.0.0.1 → Reservada (loopback, rango 127.0.0.0/8)

- 172.20.5.10 → Privada (rango 172.16.0.0/12, que va de 172.16.0.0 a 172.31.255.255)

💡 Explicación: 10.x.x.x y 172.16–31.x.x son rangos privados. 127.x.x.x es loopback (reservado). 203.0.113.45 no pertenece a ningún rango privado o reservado, por lo que es pública.
</details>

---

**Pregunta 25. [Drag and Drop]**

Arrastra cada prefijo CIDR a su máscara de subred equivalente.

**Elementos a arrastrar:**
- /24
- /26
- /27
- /30

**Categorías destino:**
- 255.255.255.0
- 255.255.255.192
- 255.255.255.224
- 255.255.255.252

<details>
<summary>Respuesta</summary>
✅ Correcta:

- /24 → 255.255.255.0 (8 bits de host)

- /26 → 255.255.255.192 (6 bits de host)

- /27 → 255.255.255.224 (5 bits de host)

- /30 → 255.255.255.252 (2 bits de host)

💡 Explicación: La máscara se construye con N bits a 1 (parte de red) seguidos de bits a 0 (parte de host). /24 = 24 bits a 1 → cuarto octeto todo 0s = .0. /26 = 26 bits a 1 → 2 bits a 1 en el cuarto octeto = 128+64 = .192. /27 = 3 bits a 1 = 128+64+32 = .224. /30 = 6 bits a 1 = 252.
</details>

---

**Pregunta 26. [Drag and Drop]**

Arrastra cada tipo de dirección IPv6 a su prefijo correspondiente.

**Elementos a arrastrar:**
- Global Unicast
- Link-Local
- Unique Local (ULA)
- Multicast

**Categorías destino:**
- 2000::/3 (empieza por 2 o 3)
- fe80::/10
- fc00::/7 (empieza por fc o fd)
- ff00::/8 (empieza por ff)

<details>
<summary>Respuesta</summary>
✅ Correcta:

- Global Unicast → 2000::/3 (empieza por 2 o 3)

- Link-Local → fe80::/10

- Unique Local (ULA) → fc00::/7 (empieza por fc o fd)

- Multicast → ff00::/8 (empieza por ff)

💡 Explicación: Global Unicast (2000::/3) equivale a IPs públicas IPv4. Link-Local (fe80::/10) se genera automáticamente y no sale del enlace. Unique Local (fc00::/7) equivale a las privadas IPv4. Multicast (ff00::/8) reemplaza al broadcast de IPv4, que no existe en IPv6.
</details>

---

**Pregunta 27. [Drag and Drop]**

Arrastra cada longitud de prefijo IPv6 a su uso típico.

**Elementos a arrastrar:**
- /48
- /64
- /128

**Categorías destino:**
- Bloque típico asignado a una organización (contiene 65.536 subredes /64)
- Subred estándar asignada a un segmento de red (la más habitual para hosts)
- Dirección de host individual o enlace punto a punto entre routers

<details>
<summary>Respuesta</summary>
✅ Correcta:

- /48 → Bloque típico asignado a una organización (contiene 65.536 subredes /64)

- /64 → Subred estándar asignada a un segmento de red (la más habitual para hosts)

- /128 → Dirección de host individual o enlace punto a punto entre routers

💡 Explicación: La jerarquía típica en IPv6 es: los RIRs asignan /32 a ISPs, las organizaciones reciben /48, cada segmento de red usa un /64 (la longitud estándar que reciben los hosts), y /128 identifica un host individual o un enlace punto a punto.
</details>

---

**Pregunta 28. [Hotspot]**

Se muestra una tabla con cuatro direcciones IP. Un administrador necesita identificar cuál pertenece a la subred **10.0.1.0/24**.

| Fila | Dirección IP |
|------|-------------|
| **A** | 10.0.0.200 |
| **B** | 10.0.1.50 |
| **C** | 10.0.2.1 |
| **D** | 10.1.1.1 |

**Señala la fila que contiene una dirección perteneciente a la subred 10.0.1.0/24.**

<details>
<summary>Respuesta</summary>
✅ Correcta: Fila B — 10.0.1.50

💡 Explicación: Con prefijo /24, los primeros 3 octetos definen la red: 10.0.1.x. Solo la dirección 10.0.1.50 (fila B) comparte el prefijo 10.0.1 con la subred indicada. La fila A tiene prefijo 10.0.0, la C tiene 10.0.2, y la D tiene 10.1.1 — todas pertenecen a subredes /24 diferentes.
</details>

---

**Pregunta 29. [Hotspot]**

Se muestra una tabla con datos de la subred a la que pertenece el host **192.168.1.200/26**. Se pide identificar la dirección de broadcast.

| Fila | Dato de subred | Valor |
|------|---------------|-------|
| **A** | Dirección de red | 192.168.1.192 |
| **B** | Primer host utilizable | 192.168.1.193 |
| **C** | Último host utilizable | 192.168.1.254 |
| **D** | Dirección de broadcast | ¿? |

**Señala la fila D e indica cuál es la dirección de broadcast de esta subred.**

A) 192.168.1.224

B) 192.168.1.240

C) 192.168.1.255

D) 192.168.1.256

<details>
<summary>Respuesta</summary>
✅ Correcta: C) 192.168.1.255

💡 Explicación: Para /26, el skip es 64. La dirección de red es 192.168.1.192 (ya dada en la tabla). Broadcast = 192 + 64 − 1 = 255 → 192.168.1.255. El rango de hosts va de .193 a .254 (62 hosts utilizables). La opción D (256) es inválida como octeto, la A (.224) y la B (.240) no corresponden al cálculo correcto.
</details>

---

**Pregunta 30. [Hotspot]**

Se muestra una tabla con cuatro direcciones IPv6. Se pide identificar cuál es una dirección Unique Local (equivalente funcional de las privadas IPv4).

| Fila | Dirección IPv6 |
|------|---------------|
| **A** | 2001:db8:1::100 |
| **B** | fe80::1 |
| **C** | fd00:abcd:1234::1 |
| **D** | ff02::1 |

**Señala la fila que contiene una dirección Unique Local (ULA).**

<details>
<summary>Respuesta</summary>
✅ Correcta: Fila C — fd00:abcd:1234::1

💡 Explicación: Las direcciones Unique Local usan el prefijo fc00::/7, lo que significa que empiezan por fc o fd. La dirección fd00:abcd:1234::1 (fila C) comienza por fd, así que es ULA. La fila A (2001:) es Global Unicast, la fila B (fe80::) es Link-Local, y la fila D (ff02::) es Multicast.
</details>

---

✅ 30 preguntas del Dominio 2 completadas.

📊 **Desglose por objetivo:**

| Objetivo | Tema | Preguntas | Total |
|----------|------|-----------|:-----:|
| **2.1** | Direcciones privadas/públicas, clases, NAT, reservadas | 1, 2, 3, 4, 5, 17, 18, 23, 24 | **9** |
| **2.2** | IPv4: CIDR, máscaras, broadcast domain, cálculo de subredes | 6, 7, 8, 9, 10, 11, 12, 19, 20, 25, 28, 29 | **12** |
| **2.3** | IPv6: tipos de direcciones, formato de prefijo, simplificación | 13, 14, 15, 16, 21, 22, 26, 27, 30 | **9** |
| | | **TOTAL** | **30** |

📋 **Desglose por tipo de pregunta:**

| Tipo | Cantidad | Preguntas |
|------|:--------:|-----------|
| Multiple Choice (1 respuesta) | **16** | 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16 |
| Multiple Choice (Choose Two) | **6** | 17, 18, 19, 20, 21, 22 |
| Drag and Drop | **5** | 23, 24, 25, 26, 27 |
| Hotspot | **3** | 28, 29, 30 |

🔢 **Preguntas con cálculo real de subred o identificación de rango: 10**
→ Preguntas 7, 8, 9, 11, 12, 17, 19, 24, 28, 29

🌐 **Preguntas sobre IPv6: 9**
→ Preguntas 13, 14, 15, 16, 21, 22, 26, 27, 30

🎯 **Desglose por dificultad:**

| Nivel | Cantidad | Preguntas |
|-------|:--------:|-----------|
| Fácil (40%) | **12** | 1, 2, 5, 6, 9, 10, 13, 14, 19, 23, 25, 28 |
| Medio (40%) | **12** | 3, 4, 7, 8, 12, 15, 17, 18, 21, 24, 26, 30 |
| Difícil (20%) | **6** | 11, 16, 20, 22, 27, 29 |
