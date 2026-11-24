# 🛡️ Protege la navegación de tu hogar con DNS públicos

> **Una configuración sencilla puede añadir una capa de protección para todos los dispositivos de tu casa, sin instalar software en cada uno.**
>
> Esta guía explica cómo elegir y configurar DNS públicos con bloqueo de dominios maliciosos, anuncios o contenido para adultos, según las necesidades de tu familia.

## 📌 Contenido

- [¿Qué es un DNS y por qué importa?](#-qué-es-un-dns-y-por-qué-importa)
- [Comparativa de DNS públicos](#-comparativa-de-dns-públicos)
- [¿Cuál deberías elegir?](#-cuál-deberías-elegir)
- [Configura el DNS en tu router](#-configura-el-dns-en-tu-router)
- [Configura el DNS en Windows](#-configura-el-dns-en-windows)
- [Configura el DNS en Android](#-configura-el-dns-en-android)
- [Configura el DNS en iPhone y iPad (iOS/iPadOS)](#-configura-el-dns-en-iphone-y-ipad-iosipados)
- [DNS cifrado: DoH y DoT](#-dns-cifrado-doh-y-dot)
- [Comprueba que funciona](#-comprueba-que-funciona)
- [Prueba el bloqueo de anuncios y rastreadores](#-prueba-el-bloqueo-de-anuncios-y-rastreadores)
- [Buenas prácticas y limitaciones](#-buenas-prácticas-y-limitaciones)
- [Fuentes oficiales](#-fuentes-oficiales)

## 🌐 ¿Qué es un DNS y por qué importa?

El **Sistema de Nombres de Dominio (DNS)** traduce nombres fáciles de recordar, como `example.com`, en direcciones IP que utilizan los equipos para conectarse a Internet.

```text
📱 Tu dispositivo
       │
       │  ¿Cuál es la IP de example.com?
       ▼
🛡️ Servidor DNS seleccionado
       │
       ├── Dominio permitido → Responde con su IP
       │
       └── Dominio bloqueado → Impide o altera su resolución DNS
```

Un servicio DNS con filtrado puede ayudar a **reducir el acceso a dominios conocidos por distribuir malware, phishing o contenido no deseado**. También existen resolutores que se enfocan en la resolución DNS y **no aplican filtrado de contenido**.

**Importante:** el DNS es una *capa adicional de protección*, no reemplaza un antivirus, un firewall, las actualizaciones ni una navegación responsable.

## 📊 Comparativa de DNS públicos

Todas las direcciones siguientes son **IPv4** y se han contrastado con la documentación oficial de los proveedores.

| Proveedor | Modalidad | DNS primario | DNS secundario | Función principal |
|---|---|---|---|---|
| **AdGuard DNS** | Predeterminado | `94.140.14.14` | `94.140.15.15` | Bloqueo de anuncios y rastreadores |
| **AdGuard DNS** | Protección familiar | `94.140.14.15` | `94.140.15.16` | Anuncios, rastreadores y contenido para adultos |
| **Cloudflare** | Estándar | `1.1.1.1` | `1.0.0.1` | DNS sin filtrado de contenido |
| **Cloudflare** | Seguridad | `1.1.1.2` | `1.0.0.2` | Bloqueo de dominios asociados con malware/phishing |
| **Cloudflare** | Familias | `1.1.1.3` | `1.0.0.3` | Malware/phishing y contenido para adultos |
| **Google Public DNS** | Estándar | `8.8.8.8` | `8.8.4.4` | DNS sin filtrado familiar integrado |
| **OpenDNS** | Estándar | `208.67.222.222` | `208.67.220.220` | Resolución DNS estándar |
| **OpenDNS** | FamilyShield | `208.67.222.123` | `208.67.220.123` | Filtrado predefinido de sitios para adultos |

> ⚠️ **No combines** un DNS familiar como `1.1.1.3` con otro sin filtrado como `8.8.8.8` pensando que el segundo solo se consultará cuando el primero falle. Según el dispositivo, los resolutores pueden usarse de distintas formas y el filtrado puede quedar inconsistente. Usa el par correspondiente a **la misma modalidad**.

## 🎯 ¿Cuál deberías elegir?

| Tu prioridad | Opción sugerida |
|---|---|
| Reducir el riesgo de navegar a dominios maliciosos | **Cloudflare Seguridad** (`1.1.1.2` / `1.0.0.2`) |
| Protección familiar y bloqueo de sitios para adultos | **Cloudflare Familias** (`1.1.1.3` / `1.0.0.3`) |
| Reducir anuncios y rastreadores | **AdGuard predeterminado** (`94.140.14.14` / `94.140.15.15`) |
| Anuncios, rastreadores y control familiar | **AdGuard Protección familiar** (`94.140.14.15` / `94.140.15.16`) |
| Filtrado familiar simple | **OpenDNS FamilyShield** (`208.67.222.123` / `208.67.220.123`) |
| Solo cambiar el resolutor DNS, sin filtros predefinidos | **Cloudflare estándar o Google Public DNS** |

**Para un hogar con niños**, empieza evaluando Cloudflare Familias o AdGuard Protección familiar. Si la prioridad es bloquear publicidad, AdGuard predeterminado suele encajar mejor. Ningún DNS tiene una cobertura perfecta de amenazas o de categorías.

## 🛜 Configura el DNS en tu router

Es la opción más práctica para aplicar el DNS a la mayoría de los dispositivos que usan tu Wi-Fi o red cableada, **siempre que acepten el DNS entregado por el router**.

1. Conéctate a tu red doméstica.
2. Abre la dirección de administración de tu router. En muchos modelos es `192.168.1.1` o `192.168.0.1`, pero puede ser otra.
3. Inicia sesión con tus credenciales de administración.
4. Busca un menú como **Internet**, **WAN**, **LAN**, **DHCP** o **DNS**.
5. Anota los valores DNS actuales antes de cambiarlos.
6. Configura los campos **DNS primario** y **DNS secundario** con el par elegido. Si el router separa el DNS de la conexión WAN del que anuncia por DHCP a tus equipos, revisa ambos ajustes y la documentación del fabricante.
7. Guarda la configuración. Si es necesario, renueva la conexión Wi-Fi o reinicia los dispositivos.

**Ejemplo: Cloudflare Familias**

```text
DNS primario:    1.1.1.3
DNS secundario:  1.0.0.3
```

> Algunos routers de proveedores de Internet no permiten editar el DNS. En ese caso, puedes configurarlo dispositivo por dispositivo o utilizar un router propio compatible. Cambiar el DNS en el router **no obliga** a todas las aplicaciones a usarlo: un navegador, una VPN o un teléfono pueden tener su propia configuración.

## 💻 Configura el DNS en Windows

### Windows 11

1. Abre **Configuración → Red e Internet**.
2. Selecciona tu conexión **Wi-Fi** o **Ethernet** y entra en sus propiedades.
3. Localiza **Asignación de servidor DNS** y selecciona **Editar**.
4. Selecciona **Manual**, activa **IPv4** e introduce el DNS primario y el secundario.
5. Si el proveedor y Windows lo admiten, configura **DNS sobre HTTPS (DoH)** para cifrar las consultas.
6. Guarda los cambios.

> No confundas **Asignación de DNS** con **Asignación de IP**: no necesitas cambiar tu dirección IP para utilizar DNS públicos.

## 🤖 Configura el DNS en Android

### Android 9 o posterior: DNS privado

1. Abre **Ajustes → Red e Internet → DNS privado** (el nombre varía por fabricante).
2. Elige **Nombre de host del proveedor de DNS privado**.
3. Introduce **uno de estos nombres de host**, no una dirección IP:

| Servicio | Hostname para DNS privado |
|---|---|
| AdGuard: anuncios y rastreadores | `dns.adguard-dns.com` |
| AdGuard: protección familiar | `family.adguard-dns.com` |
| Cloudflare: estándar | `one.one.one.one` |
| Cloudflare: malware/phishing | `security.cloudflare-dns.com` |
| Cloudflare: familias | `family.cloudflare-dns.com` |
| Google Public DNS | `dns.google` |

4. Guarda. Android utiliza **DNS over TLS (DoT)** para esta modalidad y, normalmente, aplica el ajuste a Wi-Fi y datos móviles.

## 🍎 Configura el DNS en iPhone y iPad (iOS/iPadOS)

### Opción 1: configuración manual para una red Wi-Fi

1. Entra en **Ajustes → Wi-Fi**.
2. Toca el botón de información **ⓘ** junto a tu red.
3. Abre **Configurar DNS → Manual**.
4. Elimina las entradas anteriores, si corresponde, y agrega las dos IP del servicio seleccionado.
5. Guarda los cambios.

**Nota:** esta configuración manual corresponde solo a la red Wi-Fi seleccionada; no establece por sí sola un DNS personalizado para todas las redes ni para los datos móviles. Introducir IPs manualmente en Wi-Fi tampoco implica que las consultas estén cifradas.

### Opción 2: DNS cifrado (DoH/DoT) mediante perfil de configuración

En iOS 14 y posteriores, los perfiles de configuración pueden definir un resolutor DNS cifrado para el dispositivo. Esta es una alternativa para usar el mismo proveedor en Wi-Fi y datos móviles, siempre que la red, las restricciones del sistema y las aplicaciones lo permitan.

1. Selecciona un proveedor que ofrezca **perfil DNS para iOS/iPadOS** (por ejemplo, [AdGuard DNS público](https://adguard-dns.io/es/public-dns.html)).
2. Desde su **sitio oficial**, selecciona la modalidad deseada (estándar o familiar) y genera o descarga el perfil para iOS/macOS. Comprueba que corresponda al servicio elegido.
3. En tu iPhone o iPad, abre el perfil descargado y sigue las indicaciones del sistema. En general, entra en **Ajustes → Perfil descargado** o **Ajustes → General → VPN y gestión de dispositivos**, según la versión de iOS.
4. Revisa el nombre, el origen y los permisos del perfil antes de instalarlo; no instales perfiles obtenidos de fuentes desconocidas.
5. Una vez instalado, comprueba su funcionamiento tanto en Wi-Fi como en datos móviles mediante las páginas de prueba del proveedor.

> **Precaución:** las VPN, las aplicaciones con su propio DNS, las redes que bloquean el acceso al resolutor y algunas políticas de administración del dispositivo pueden modificar o impedir este comportamiento. Para revertirlo, elimina el perfil desde **VPN y gestión de dispositivos**, si tu dispositivo permite hacerlo.

### Opción 3: aplicación oficial con protección DNS

Una aplicación del proveedor compatible con iOS puede gestionar DNS cifrado y facilitar el cambio de perfiles. Consulta la documentación oficial, por ejemplo [AdGuard para iOS](https://adguard.com/kb/es/adguard-for-ios/features/dns-protection/). Ten en cuenta que algunas aplicaciones usan una configuración VPN local para dirigir el tráfico DNS, lo cual puede interferir con otra VPN.

**¿Qué opción elegir?** Para proteger únicamente tu Wi-Fi de casa, la **opción 1** suele ser suficiente. Si quieres aplicar DNS cifrado al cambiar entre Wi-Fi y datos móviles, evalúa la **opción 2** o **3** y verifica que el filtrado siga activo.

## 🔐 DNS cifrado: DoH y DoT

El DNS clásico suele transmitirse sin cifrar. Los protocolos siguientes protegen **el transporte de las consultas DNS** entre tu dispositivo y el resolutor:

- **DNS over HTTPS (DoH):** usa HTTPS.
- **DNS over TLS (DoT):** usa TLS, normalmente en el puerto 853.

Algunos endpoints oficiales de **DoH** son:

| Perfil | URL DoH |
|---|---|
| AdGuard predeterminado | `https://dns.adguard-dns.com/dns-query` |
| AdGuard familiar | `https://family.adguard-dns.com/dns-query` |
| Cloudflare estándar | `https://cloudflare-dns.com/dns-query` |
| Cloudflare seguridad | `https://security.cloudflare-dns.com/dns-query` |
| Cloudflare familias | `https://family.cloudflare-dns.com/dns-query` |
| Google Public DNS | `https://dns.google/dns-query` |

> 🔎 **DNS cifrado no es una VPN**: no oculta por completo los sitios que visitas, ni protege contra todo tipo de seguimiento. El proveedor DNS que elijas seguirá procesando tus consultas.

### IPv6 también importa

Si tu conexión utiliza IPv6, verifica la configuración de los resolutores IPv6. Por ejemplo, **Cloudflare Familias** ofrece:

```text
IPv6 primario:    2606:4700:4700::1113
IPv6 secundario:  2606:4700:4700::1003
```

Si mantienes IPv6 activo con DNS no filtrados, algunos dispositivos podrían resolver dominios fuera de la política que configuraste solo para IPv4.

## ✅ Comprueba que funciona

**En Windows**, abre PowerShell o Símbolo del sistema y ejecuta:

```powershell
nslookup example.com
```

Observa el campo **Servidor / Server** y su dirección para identificar qué resolutor DNS utiliza la prueba. También puedes inspeccionar tus DNS configurados:

```powershell
Get-DnsClientServerAddress
```

Para vaciar la caché local tras el cambio:

```powershell
ipconfig /flushdns
```

**Comprobaciones adicionales:**

- Visita [Cloudflare 1.1.1.1 Help](https://one.one.one.one/help/) si elegiste Cloudflare; sus resultados deben interpretarse en función del servicio y método que hayas configurado. Para **Cloudflare Familias**, Cloudflare proporciona dominios de prueba seguros: [malware.testcategory.com](https://malware.testcategory.com/) (bloqueo de malware) y [nudity.testcategory.com](https://nudity.testcategory.com/) (bloqueo de contenido adulto).
- Si elegiste OpenDNS, utiliza su [página de prueba](https://welcome.opendns.com/).
- Comprueba que el filtrado realmente se aplique con las herramientas de prueba oficiales del proveedor; no es necesario visitar páginas maliciosas reales.

> `nslookup` confirma el comportamiento de esa consulta y puede mostrar el servidor configurado, **pero no demuestra por sí solo** que todo el tráfico de las aplicaciones esté filtrado ni que DNS esté cifrado.

## 🧪 Prueba el bloqueo de anuncios y rastreadores

Después de configurar tu DNS, visita **[Ad Blocker Test — Turtlecute](https://adblock.turtlecute.org/)** para comprobar desde el navegador si tu configuración está bloqueando determinados anuncios, rastreadores y solicitudes a dominios publicitarios.

**Cómo realizar la prueba:**

1. Conecta el equipo o teléfono a la red donde configuraste el DNS (o activa el DNS privado del dispositivo).
2. Abre **https://adblock.turtlecute.org/** en tu navegador, con JavaScript habilitado.
3. Examina el resultado en las categorías **Host**, **Cosmetic Filter** y **Ad Scripts Loading**.
4. Si quieres comparar, repite la prueba con y sin tu bloqueador de navegador, sin modificar innecesariamente la configuración de seguridad de tu red.

| Categoría | ¿Qué comprueba? | ¿Un DNS público con filtrado puede bloquearlo? |
|---|---|---|
| **Host** | Solicitudes a dominios asociados a anuncios, analítica y rastreadores | **Sí, cuando esos dominios están incluidos en sus reglas** |
| **Cosmetic Filter** | Ocultación visual de espacios publicitarios en la página | **No**; requiere filtrado en el navegador |
| **Ad Scripts Loading** | Bloqueo de scripts y recursos publicitarios en la página | **No necesariamente**; depende de un bloqueador a nivel del navegador |

> ⚠️ **No busques necesariamente un 100 %.** Un DNS como AdGuard DNS puede bloquear dominios sin eliminar elementos visuales o scripts que se sirven desde dominios permitidos. Cloudflare estándar y Google Public DNS no son bloqueadores de anuncios; Cloudflare Familias se enfoca en malware y contenido adulto, no en publicidad general. **Una puntuación baja no demuestra, por sí sola, que la protección contra malware o phishing esté desactivada.** El resultado también puede verse afectado por extensiones, VPN, listas de filtrado y características del navegador.

Esta es una herramienta de terceros para una **prueba orientativa del bloqueo de anuncios y rastreadores**, no una auditoría integral de seguridad ni una verificación del cifrado DNS. Para validar el proveedor y la política DNS, utiliza también las comprobaciones oficiales indicadas en la sección anterior.

## 🔒 Buenas prácticas y limitaciones

1. **Mantén actualizado el router** y cambia su contraseña administrativa predeterminada.
2. **Utiliza WPA2-AES o WPA3** en Wi-Fi, con una contraseña robusta.
3. **Desactiva WPS** si no lo necesitas y crea una red separada para invitados o dispositivos IoT cuando sea posible.
4. **Revisa DNS por IPv4 e IPv6**, no solo una de las dos familias.
5. **Comprueba DNS privados, DoH del navegador y VPN**: pueden sustituir el DNS entregado por el router y evitar el filtro configurado.
6. **No mezcles resolutores filtrados y sin filtrar** en el mismo perfil.
7. **Complementa DNS con otras medidas**: actualizaciones automáticas, MFA, gestor de contraseñas, bloqueadores locales apropiados y controles parentales en cada dispositivo.
8. **Considera la privacidad**: el operador del DNS recibe consultas de resolución; revisa su política de registros y privacidad.

### Lo que un DNS filtrado **no** puede garantizar

- No detecta todas las páginas nuevas de phishing o malware.
- No analiza el contenido de archivos descargados ni sustituye un antivirus.
- No bloquea de forma confiable contenido específico dentro de un dominio permitido.
- No impide todas las conexiones directas por IP o las aplicaciones que usen otros mecanismos de resolución.
- No sustituye controles parentales a nivel de dispositivo ni una conversación sobre hábitos digitales seguros.

## 📚 Fuentes oficiales

- [AdGuard DNS: servidores públicos y métodos de configuración](https://adguard-dns.io/es/public-dns.html)
- [Cloudflare: direcciones IP de los resolutores](https://developers.cloudflare.com/1.1.1.1/ip-addresses/)
- [Cloudflare: configuración en routers](https://developers.cloudflare.com/1.1.1.1/setup/router/)
- [Cloudflare: configuración en Android](https://developers.cloudflare.com/1.1.1.1/setup/android/)
- [Google Public DNS](https://developers.google.com/speed/public-dns/docs/using)
- [OpenDNS: guía oficial](https://www.opendns.com/setupguide/)
- [Cisco: OpenDNS FamilyShield](https://www.cisco.com/c/en/us/support/docs/security/umbrella/225803-understand-opendns-familyshield.html)
- [Microsoft: configuración de DNS en Windows](https://support.microsoft.com/en-us/windows/experience/connectivity-networking/essential-network-settings-and-tasks-in-windows)
- [Apple: configuración de DNS cifrado mediante perfiles](https://developer.apple.com/documentation/devicemanagement/dnssettings)
- [AdGuard: DNS público y perfil para iOS/macOS](https://adguard-dns.io/es/public-dns.html)
- [AdGuard: protección DNS en iOS](https://adguard.com/kb/es/adguard-for-ios/features/dns-protection/)

---

### 🤝 Comparte esta guía

Si te resultó útil, dale una ⭐ al repositorio y compártelo con alguien que quiera mejorar la seguridad de su red doméstica.

**La ciberseguridad también empieza en casa.** 🏠🔐

*Contenido educativo. Los servicios y sus políticas de filtrado pueden cambiar; consulta la documentación oficial antes de implementar configuraciones críticas.*
