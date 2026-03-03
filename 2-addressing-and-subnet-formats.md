# Dominio 2: Addressing and Subnet Formats

## Resumen ejecutivo

Este dominio abarca el sistema de direccionamiento IP que hace posible la comunicación en redes. Cubre las diferencias entre direcciones públicas y privadas, el funcionamiento de NAT, el cálculo de subredes IPv4 con notación CIDR y máscaras de subred, los dominios de broadcast, y el formato y tipos de direcciones IPv6. Es un dominio muy práctico: el examen incluye preguntas de cálculo y de identificación de rangos.

---

## Conceptos clave

### 2.1 — Direcciones privadas vs. públicas

🔑 *Analogía:* Las direcciones privadas son como extensiones telefónicas internas de una empresa — funcionan dentro del edificio, pero para llamar fuera necesitas pasar por la centralita (NAT) que presenta un número público.

#### Clases de direcciones IPv4 (históricas)

Antes de CIDR (1993), las direcciones IPv4 se dividían en clases según el primer octeto. Aunque las clases ya no se usan para enrutamiento, siguen siendo relevantes para entender rangos y el examen las menciona explícitamente.

| Clase | Rango primer octeto | Prefijo por defecto | Bits de red | Bits de host | N.º de redes | N.º de hosts por red |
|-------|---------------------|---------------------|-------------|--------------|-------------|---------------------|
| **A** | 0 – 127 | /8 | 8 | 24 | 128 | ~16,7 millones |
| **B** | 128 – 191 | /16 | 16 | 16 | 16.384 | ~65.534 |
| **C** | 192 – 223 | /24 | 24 | 8 | ~2,1 millones | 254 |
| **D** | 224 – 239 | N/A | N/A | N/A | Multicast | N/A |
| **E** | 240 – 255 | N/A | N/A | N/A | Experimental/Reservado | N/A |

En 1993 estas clases fueron reemplazadas por **CIDR (Classless Inter-Domain Routing)**, que permite dividir el espacio de direcciones con cualquier longitud de prefijo, no solo /8, /16 o /24.

#### Direcciones privadas IPv4

Tres rangos están reservados para uso privado. No son enrutables en Internet público; cualquier organización puede usarlos internamente sin coordinación.

| Rango privado | Prefijo CIDR | Clase equivalente | Nº de direcciones |
|---------------|-------------|-------------------|-------------------|
| **10.0.0.0** – 10.255.255.255 | 10.0.0.0/8 | Clase A completa | ~16,7 millones |
| **172.16.0.0** – 172.31.255.255 | 172.16.0.0/12 | 16 redes de Clase B | ~1 millón |
| **192.168.0.0** – 192.168.255.255 | 192.168.0.0/16 | 256 redes de Clase C | ~65.534 |

#### Direcciones públicas

Las direcciones públicas son **globalmente enrutables** en Internet. Se obtienen a través de:

1. **IANA** (Internet Assigned Numbers Authority) → controla la distribución global.
2. **RIRs** (Regional Internet Registries) → asignan bloques por región geográfica: AFRINIC (África), ARIN (Norteamérica), APNIC (Asia-Pacífico), LACNIC (Latinoamérica/Caribe), RIPE (Europa/Asia Central).
3. **ISPs** → la forma más habitual: el proveedor de Internet asigna direcciones al contratar el servicio.

Obtener direcciones IPv4 públicas nuevas es prácticamente imposible hoy — la mayoría de RIRs han agotado su espacio libre.

#### Direcciones reservadas importantes

| Dirección / Rango | Propósito |
|--------------------|-----------|
| **0.0.0.0/8** | "Esta red" — usado por hosts al arrancar antes de obtener IP |
| **127.0.0.0/8** | Loopback — paquetes no salen del host (127.0.0.1 es la más usada) |
| **169.254.0.0/16** | Link-local — autoasignada cuando DHCP falla (APIPA) |
| **224.0.0.0/4** | Multicast (Clase D) |
| **255.255.255.255** | Broadcast limitado — todos los hosts del segmento local |

#### NAT (Network Address Translation)

NAT permite que múltiples dispositivos con direcciones privadas compartan una o pocas direcciones públicas para acceder a Internet. Fue diseñado para extender la vida útil del espacio IPv4.

**Funcionamiento básico:**

1. El host interno (por ejemplo, 192.168.1.10) envía un paquete hacia Internet con su IP privada como origen y un puerto efímero (por ejemplo, 49170).
2. El dispositivo NAT (normalmente el router) **reemplaza** la dirección origen privada por su dirección pública (por ejemplo, 203.0.113.1) y **puede modificar el puerto** origen para distinguir entre hosts internos.
3. Cuando la respuesta llega, el NAT consulta su **tabla de traducciones** para saber a qué host interno y puerto reenviar el paquete.

**NAT vs. PAT:** NAT traduce solo direcciones IP (una IP pública por host). **PAT (Port Address Translation)** traduce direcciones IP *y* puertos, permitiendo que múltiples hosts compartan una sola IP pública. En la práctica, la mayoría de implementaciones son PAT, pero el término "NAT" se usa para ambas.

**¿Por qué importa?** NAT rompe el modelo end-to-end de Internet (las direcciones embebidas dentro de los datos de aplicación no coinciden con las del header), lo que puede causar problemas con ciertos protocolos. Sin embargo, es omnipresente en redes actuales.

---

### 2.2 — Direcciones IPv4 y formatos de subred

🔑 *Analogía:* Una dirección IPv4 es como una dirección postal con dos partes: el nombre de la calle (prefijo de red) identifica el barrio, y el número de portal (parte de host) identifica la casa concreta dentro de ese barrio. La máscara de subred es la regla que dice dónde termina el nombre de calle y empieza el número de portal.

#### Estructura de una dirección IPv4

Una dirección IPv4 tiene **32 bits**, representados como cuatro octetos en notación decimal separados por puntos (ej: 192.168.1.100). Se divide en dos partes:

- **Prefijo (network portion):** Identifica la red o subred. Todos los hosts del mismo segmento comparten el mismo prefijo.
- **Parte de host (subnet/host portion):** Identifica al host individual dentro de esa red.

La longitud del prefijo se indica con **notación CIDR** (slash notation): un `/` seguido del número de bits dedicados al prefijo. Ejemplo: `10.1.1.0/24` → los primeros 24 bits son el prefijo; los 8 restantes son para hosts.

#### Máscara de subred (Subnet Mask)

La máscara de subred es una representación alternativa de la longitud del prefijo. Es un valor de 32 bits donde los **1s representan la parte de red** y los **0s representan la parte de host**.

| Prefijo CIDR | Máscara de subred | Bits de host | Hosts utilizables* |
|-------------|-------------------|--------------|-------------------|
| /8 | 255.0.0.0 | 24 | 16.777.214 |
| /16 | 255.255.0.0 | 16 | 65.534 |
| /24 | 255.255.255.0 | 8 | 254 |
| /25 | 255.255.255.128 | 7 | 126 |
| /26 | 255.255.255.192 | 6 | 62 |
| /27 | 255.255.255.224 | 5 | 30 |
| /28 | 255.255.255.240 | 4 | 14 |
| /29 | 255.255.255.248 | 3 | 6 |
| /30 | 255.255.255.252 | 2 | 2 |

*\*Hosts utilizables = 2^(bits de host) − 2 (se restan la dirección de red y la de broadcast).*

**Para encontrar el prefijo (ID de red)** a partir de una dirección y su máscara, se aplica una operación lógica **AND** bit a bit entre la dirección y la máscara. El resultado es la dirección de red.

#### Dominio de broadcast

Un **broadcast domain** (dominio de broadcast) es el conjunto de todos los dispositivos que reciben una trama de broadcast enviada por cualquiera de ellos. Equivale a un segmento de red o VLAN.

- Todos los hosts **con el mismo prefijo y longitud de prefijo** pertenecen al mismo broadcast domain.
- Los **routers** separan broadcast domains (no reenvían broadcasts).
- Los **switches** no separan broadcast domains (reenvían broadcasts a todos los puertos).

**Direcciones de broadcast en una subred:**

- **Dirección de red** (todos los bits de host a 0): primera dirección de la subred. Técnicamente también es broadcast, pero casi nunca se usa como tal.
- **Dirección de broadcast** (todos los bits de host a 1): última dirección de la subred. Es la que se usa en la práctica.

#### Método rápido de cálculo: Skip Chart

A continuación, se presenta un método eficiente para calcular direcciones de red y broadcast sin convertir a binario. El concepto clave es el **"skip"** (salto): el intervalo en el que se repiten las subredes.

**Tabla de skips para el cuarto octeto** (los más frecuentes en examen):

| Prefijo | Skip | Nº subredes en el octeto | Hosts por subred |
|---------|------|--------------------------|------------------|
| /25 | 128 | 2 | 126 |
| /26 | 64 | 4 | 62 |
| /27 | 32 | 8 | 30 |
| /28 | 16 | 16 | 14 |
| /29 | 8 | 32 | 6 |
| /30 | 4 | 64 | 2 |

**Ejemplo paso a paso:** Dada la dirección **198.51.100.70/26**:

1. El prefijo es /26 → el skip es **64** y trabajamos en el **cuarto octeto**.
2. Dividimos 70 ÷ 64 = **1** (ignoramos el resto).
3. Multiplicamos 1 × 64 = **64** → Dirección de red: **198.51.100.64**
4. Sumamos el skip y restamos 1: 64 + 64 − 1 = **127** → Broadcast: **198.51.100.127**
5. Rango de hosts utilizables: **198.51.100.65** a **198.51.100.126** (62 hosts).

**Cómo calcular el skip sin memorizar la tabla:**

1. Dividir la longitud del prefijo entre 8 (parte entera + 1 = octeto de trabajo).
2. Multiplicar el octeto × 8 y restar del prefijo → bits consumidos en ese octeto.
3. Restar ese valor de 8 y elevar 2 a esa potencia → skip.

Para /26: 26 ÷ 8 = 3, octeto 4. 4 × 8 = 32. 32 − 26 = 6. 2^6 = **64** (skip).

#### Ejemplo con prefijo fuera de los límites de octeto

Dada **10.128.192.0/18**:

- /18 → trabajamos en el **tercer octeto**, skip = 2^(24−18) = 2^6 = **64**.
- 192 ÷ 64 = 3. 3 × 64 = **192** → Dirección de red: **10.128.192.0**
- 192 + 64 − 1 = **255** → Broadcast: **10.128.255.255** (los octetos posteriores al de trabajo van a 255 en el broadcast).

---

### 2.3 — Direcciones IPv6 y formatos de prefijo

🔑 *Analogía:* Si IPv4 es un código postal de 10 dígitos que se agotó, IPv6 es como pasar a un código postal de 32 dígitos hexadecimales — tan grande que puede asignar una dirección única a cada grano de arena del planeta.

#### Formato de dirección IPv6

- **128 bits** de longitud (frente a los 32 de IPv4).
- Se representa como **8 grupos de 4 dígitos hexadecimales** separados por dos puntos. Cada grupo (a veces llamado **quartet**) representa 16 bits (2 octetos).
- Ejemplo completo: `2001:0db8:03e8:0000:0000:0000:0100:0001`

**Reglas de simplificación:**

1. **Se eliminan los ceros iniciales** de cada quartet: `0db8` → `db8`, `0000` → `0`.
2. **Una única cadena consecutiva de quartets todo-ceros** se reemplaza por `::` (solo una vez por dirección): `2001:db8:3e8:0:0:0:100:1` → `2001:db8:3e8::100:1`

**Prefijo IPv6:** Funciona igual que en IPv4 — la notación CIDR indica cuántos bits pertenecen al prefijo. Ejemplo: `2001:db8:3e8::/48` → los primeros 48 bits son el prefijo.

#### Tipos de direcciones IPv6

| Tipo | Prefijo / Rango | Alcance | Descripción |
|------|-----------------|---------|-------------|
| **Global Unicast** | `2000::/3` (empieza por 2 o 3) | Internet global | Equivalente a las IPs públicas en IPv4. Enrutables globalmente. |
| **Link-Local** | `fe80::/10` | Solo el enlace local | Se genera automáticamente en cada interfaz. No atraviesa routers. Obligatoria en toda interfaz IPv6. |
| **Unique Local (ULA)** | `fc00::/7` (empieza por fc o fd) | Organización interna | Equivalente funcional de las direcciones privadas IPv4. No enrutable en Internet. |
| **Multicast** | `ff00::/8` (empieza por ff) | Variable (según scope) | Reemplaza al broadcast de IPv4. No existe broadcast en IPv6. |
| **Loopback** | `::1/128` | Solo el host | Equivalente a 127.0.0.1 en IPv4. |
| **Unspecified** | `::/128` | N/A | Equivalente a 0.0.0.0 en IPv4. Usada antes de obtener dirección. |

**Dato clave para el examen:** IPv6 **no tiene broadcast**. Toda comunicación "a todos" se realiza mediante **multicast** (dirección que comienza por `ff`).

#### Longitudes de prefijo comunes en IPv6

| Prefijo | Uso típico |
|---------|------------|
| /128 | Dirección de host individual o enlace punto a punto entre routers |
| /64 | Subred estándar asignada a un segmento de red (la más habitual) |
| /48 | Bloque típico asignado a una organización (contiene 65.536 subredes /64) |
| /32 | Bloque asignado por RIRs a ISPs |

En la práctica, los prefijos que más encontrarás están entre **/48 y /64**. Los hosts individuales siempre reciben un **/64**.

#### Cómo se obtiene una dirección IPv6

**Link-Local (automática):**

1. Se toma la dirección MAC (EUI-48) de la interfaz.
2. Se invierte el bit U/L (7º bit del primer octeto).
3. Se insertan los bytes `FF:FE` en el centro → se obtiene un identificador EUI-64.
4. Se combina con el prefijo `fe80::/64`.
5. Se ejecuta **DAD (Duplicate Address Detection)** para asegurar unicidad.

Ejemplo: MAC `00:00:00:11:22:33` → Link-local: `fe80::200:ff:fe11:2233/64`

**Global Unicast (SLAAC o DHCPv6):**

- **SLAAC (Stateless Address Autoconfiguration):** El host envía un **Router Solicitation (RS)**, recibe un **Router Advertisement (RA)** con el prefijo de la red, y combina ese prefijo con su identificador EUI-64 para formar la dirección global. El router que envió el RA se convierte en el **default gateway**.
- **DHCPv6:** Similar a DHCP en IPv4. El servidor asigna la dirección completa. Puede funcionar como stateful (asigna todo) o stateless (solo proporciona DNS y otros parámetros; la dirección se obtiene por SLAAC).

**Nota sobre privacidad:** SLAAC revela la MAC del dispositivo en los últimos 64 bits de la dirección, lo que permite rastrear a un usuario aunque cambie de red. Para mitigar esto, muchos sistemas operativos generan **direcciones temporales aleatorias** en lugar de usar el EUI-64.

#### Subnetting en IPv6

El subnetting en IPv6 sigue la misma lógica que en IPv4 pero con rangos más amplios. Ejemplo: dado un bloque `2001:db8:3e8::/48`:

- Se puede dividir en 2 subredes /49: `2001:db8:3e8::/49` y `2001:db8:3e8:8000::/49`
- Se puede dividir en 4 subredes /50: `2001:db8:3e8::/50`, `2001:db8:3e8:4000::/50`, `2001:db8:3e8:8000::/50` y `2001:db8:3e8:c000::/50`

El método del skip funciona igual: para /50, el skip en el cuarto quartet es `4000` (hex), así que las subredes van de 4000 en 4000: 0000, 4000, 8000, C000.

La primera y última dirección de cada subred IPv6 son, al igual que en IPv4, direcciones de broadcast (aunque en IPv6 el concepto se materializa como multicast).

---

## 🎯 Puntos críticos para el examen

- **Rangos privados IPv4:** Memorizar los tres rangos exactos (10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16). Saber que NO son enrutables en Internet sin NAT.
- **Clases IPv4:** Saber los rangos del primer octeto para Clase A (0-127), B (128-191) y C (192-223). Aunque CIDR reemplazó las clases, el examen pregunta por ellas.
- **NAT/PAT:** NAT traduce direcciones; PAT traduce direcciones y puertos. PAT permite que múltiples hosts compartan una sola IP pública. En la práctica, ambos términos se usan indistintamente.
- **Notación CIDR:** /24 = 255.255.255.0, /25 = 255.255.255.128, /26 = 255.255.255.192, /27 = 255.255.255.224. Poder convertir entre prefijo CIDR y máscara decimal.
- **Cálculo de subredes:** Dados una IP y un prefijo, saber encontrar la dirección de red, el broadcast y el rango de hosts válidos usando el método del skip.
- **Broadcast domain:** Todos los hosts con el mismo prefijo están en el mismo broadcast domain. Los routers separan broadcast domains; los switches no.
- **IPv6 link-local:** Siempre empieza por `fe80::`, se genera automáticamente, no atraviesa routers. Es obligatoria en toda interfaz IPv6.
- **IPv6 global unicast:** Empieza por `2` o `3` (rango `2000::/3`). Es el equivalente a una IP pública IPv4.
- **IPv6 no tiene broadcast:** Usa multicast (prefijo `ff`) en su lugar. Esto es una pregunta típica de examen.
- **Prefijo /64:** Es la longitud de prefijo estándar para un segmento de red IPv6. Los hosts siempre reciben un /64.

---

## Mini-resumen

- Las **direcciones privadas** IPv4 (10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16) son para uso interno; las **públicas** son enrutables en Internet y se obtienen a través de IANA → RIR → ISP. **NAT** permite que redes privadas accedan a Internet compartiendo IPs públicas.
- Una dirección IPv4 de 32 bits se divide en **prefijo** (red) y **parte de host** mediante la **longitud de prefijo CIDR** o la **máscara de subred**. La primera dirección de la subred es la dirección de red y la última es el **broadcast**; ninguna es asignable a hosts.
- El **método del skip** permite calcular rápidamente redes y broadcasts: dividir el valor del octeto entre el skip, multiplicar de vuelta para obtener la red, y sumar skip−1 para obtener el broadcast.
- IPv6 usa **128 bits** con notación hexadecimal. Los tipos clave son: **global unicast** (2000::/3 — pública), **link-local** (fe80::/10 — automática, solo enlace), **unique local** (fc00::/7 — privada), y **multicast** (ff00::/8 — reemplaza al broadcast). Los hosts reciben siempre un prefijo **/64**, y las organizaciones típicamente un **/48**.
- IPv6 obtiene direcciones automáticamente via **SLAAC** (Router Solicitation → Router Advertisement + EUI-64) o **DHCPv6**, y resuelve la privacidad con direcciones temporales aleatorias.
