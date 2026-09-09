# Fuentes oficiales verificadas

**Propósito**: repositorio único de referencias citables para los cuatro entregables.
Todas las entradas fueron **verificadas contra la fuente primaria** en la fecha indicada.

**Regla del repositorio**: ningún dato técnico, precio ni marco normativo entra a un
entregable sin una entrada correspondiente en este archivo.

**Formato de cita**: APA 7ª edición (§8.3 del enunciado).
**Fecha de verificación general**: 5 de septiembre de 2026.

---

## 1. Marcos normativos y de control

### 1.1 ISO/IEC 27001:2022

**Dato verificado**: el Anexo A de la edición 2022 contiene **93 controles** organizados en
**4 temas**: organizacionales (37), personas (8), físicos (14) y tecnológicos (34). La edición
anterior (2013) tenía 114 controles en 14 categorías. La revisión incorpora **11 controles
nuevos**, fusiona 24 y revisa 58.

> ⚠️ **Crítico para la Fase 1**: la numeración tipo `A.8.26` que usa el entregable actual
> corresponde a la **edición 2022**. Debe declararse la edición explícitamente, porque en la
> edición 2013 esa numeración no existe.

- Organización Internacional de Normalización. (2022). *ISO/IEC 27001:2022 — Information security, cybersecurity and privacy protection — Information security management systems — Requirements*. https://www.iso.org/standard/27001

Controles del Anexo A más citados en este proyecto:

| Control | Título | Debilidad asociada |
|---|---|---|
| A.5.15 | Control de acceso | D-05, D-06 |
| A.5.17 | Información de autenticación | D-05, D-06 |
| A.5.19 – A.5.22 | Seguridad de la información en relaciones con proveedores | D-17 |
| A.6.3 | Concientización, educación y capacitación | D-15 |
| A.7.1 – A.7.4 | Perímetros y controles de acceso físico, monitoreo | D-12 |
| A.7.11 | Servicios de suministro (energía) | D-13 |
| A.8.7 | Protección contra malware | D-11 |
| A.8.8 | Gestión de vulnerabilidades técnicas | D-10, D-16 |
| A.8.13 | Respaldo de la información | D-14 |
| A.8.15 – A.8.16 | Registro de eventos y actividades de monitoreo | D-16 |
| A.8.20 – A.8.22 | Seguridad de redes, servicios de red y segregación de redes | D-01, D-07 |
| A.8.24 | Uso de criptografía | D-03 |
| A.8.26 | Requisitos de seguridad de aplicaciones | D-01 |

### 1.2 NIST Cybersecurity Framework 2.0

**Dato verificado**: CSF 2.0 se organiza en **6 funciones** — Govern (GV), Identify (ID),
Protect (PR), Detect (DE), Respond (RS) y Recover (RC). La función **Govern es nueva** en la
versión 2.0; CSF 1.1 tenía solo cinco. Publicado en febrero de 2024.

- National Institute of Standards and Technology. (2024). *The NIST Cybersecurity Framework (CSF) 2.0* (NIST CSWP 29). U.S. Department of Commerce. https://doi.org/10.6028/NIST.CSWP.29
- PDF directo: https://nvlpubs.nist.gov/nistpubs/CSWP/NIST.CSWP.29.pdf

### 1.3 CIS Critical Security Controls v8.1

**Dato verificado**: **18 controles** y **153 salvaguardas**, distribuidas en 3 grupos de
implementación: **IG1 = 56** salvaguardas ("higiene cibernética esencial"), **IG2 = +74**
(acumulado 130), **IG3 = +23** (acumulado 153). La v8 redujo de 20 a 18 controles y renombró
"sub-controles" a "salvaguardas".

> **Justificación para TransAgro**: con ~480 colaboradores, custodia de datos de terceros
> (clientes, proveedores, ubicación GPS de flotilla) y operación OT (PLC de planta), la
> organización corresponde razonablemente a **IG2**. Esta elección debe justificarse en el
> documento.

- Center for Internet Security. (2024). *CIS Critical Security Controls version 8.1*. https://www.cisecurity.org/controls/v8-1
- Guía de grupos de implementación: https://www.cisecurity.org/insights/white-papers/guide-implementation-groups-ig-cis-critical-security-controls-v8-1
- Navegador interactivo de controles: https://www.cisecurity.org/controls/cis-controls-navigator

### 1.4 NIST SP 800-34 Rev. 1 — Planificación de contingencia

Referencia central para la **Fase 3 (DRP)**: define la metodología de análisis de impacto al
negocio (BIA), la determinación de RTO/RPO y las estrategias de sitio alterno
(frío / tibio / caliente / espejo).

- Swanson, M., Bowen, P., Phillips, A. W., Gallup, D., & Lynes, D. (2010). *Contingency planning guide for federal information systems* (NIST SP 800-34 Rev. 1). National Institute of Standards and Technology. https://doi.org/10.6028/NIST.SP.800-34r1

### 1.5 NIST SP 800-61 Rev. 3 — Manejo de incidentes

Base para el bloque de **gestión de incidentes** de la Fase 2 (§5.1 punto 6.9) y para los
procedimientos de respuesta del DRP.

- National Institute of Standards and Technology. (2025). *Incident response recommendations and considerations for cybersecurity risk management* (NIST SP 800-61r3). https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-61r3.pdf

### 1.5b NIST SP 800-207 — Zero Trust Architecture

Principio rector de la **segmentación de la Fase 2 (C-25)**: el acceso a un recurso se concede
por identidad, necesidad y postura del dispositivo, no por su ubicación en la red. Elimina la
confianza implícita de la red plana. Consultado el 7 de septiembre de 2026.

- Rose, S., Borchert, O., Mitchell, S., & Connelly, S. (2020). *Zero Trust Architecture* (NIST SP 800-207). National Institute of Standards and Technology. https://doi.org/10.6028/NIST.SP.800-207

### 1.5c NIST SP 800-63B-4 — Digital Identity Guidelines (autenticación)

Base de la **política de contraseñas y MFA de la Fase 2 (C-22, P-05)**: longitud sobre
complejidad, verificación contra listas de contraseñas comprometidas, sin expiración forzada
periódica cuando hay MFA y detección de compromiso. Consultado el 7 de septiembre de 2026.

- National Institute of Standards and Technology. (2024). *Digital identity guidelines: Authentication and authenticator management* (NIST SP 800-63B-4). https://pages.nist.gov/800-63-4/sp800-63b.html

### 1.5d CISA — Implementing Phishing-Resistant MFA

Sustento de exigir **MFA resistente a phishing (FIDO2/WebAuthn o PKI)** para cuentas
privilegiadas y de administración en la Fase 2 (C-22, P-04); SMS solo como último recurso.
Consultado el 7 de septiembre de 2026.

- Cybersecurity and Infrastructure Security Agency. (2022). *Implementing phishing-resistant MFA* (fact sheet). U.S. Department of Homeland Security. https://www.cisa.gov/sites/default/files/publications/fact-sheet-implementing-phishing-resistant-mfa-508.pdf

### 1.5e Veeam — Modelo de respaldo 3-2-1-1-0

Sustento del **modelo de respaldo de la Fase 2 (C-08, P-11)**: 3 copias, 2 medios, 1 offsite,
1 copia inmutable/aislada (air-gapped) y 0 errores verificados por prueba. Extiende el clásico
3-2-1 frente al ransomware que ataca los respaldos. Consultado el 7 de septiembre de 2026.

- Veeam Software. (2024). *The 3-2-1 backup rule and the modern 3-2-1-1-0 approach*. https://www.veeam.com/blog/321-backup-rule.html

### 1.5f ISA/IEC 62443 y modelo Purdue — segmentación de la red OT

Sustento del aislamiento de los **PLC de la Planta en una zona dedicada con conductos
controlados** (Fase 2, C-25). El 96 % de los incidentes OT se originan en la red IT (Dragos,
2025), por lo que la segmentación IT/OT es de los controles de mayor impacto. Consultado el 7
de septiembre de 2026.

- International Society of Automation. (s. f.). *ISA/IEC 62443 series of standards*. https://www.isa.org/standards-and-publications/isa-standards/isa-iec-62443-series-of-standards
- SentinelOne. (2025). *What is the Purdue model? Definition, levels and best practices*. https://www.sentinelone.com/cybersecurity-101/cybersecurity/what-is-the-purdue-model/

### 1.5g WPA3-Enterprise, 802.1X y Wi-Fi de invitados

Sustento de la **WLAN corporativa de la Fase 2 (C-27)**: SSID corporativo WPA3-Enterprise con
802.1X (preferible EAP-TLS por certificado y RADIUS sobre TLS/RadSec) y SSID de invitados
aislado con portal cautivo, aislamiento de clientes y credenciales temporales; WPA3-Enhanced
Open (OWE) como alternativa para invitados. Consultado el 7 de septiembre de 2026.

- a7.de. (2025). *Enterprise WLAN security: WPA3, 802.1X and secure guest Wi-Fi*. https://a7.de/en/blog/enterprise-wlan-security-wpa3-8021x-and-secure-guest-wi-fi/

### 1.6 OWASP Top 10

**Dato verificado**: existen dos ediciones relevantes. La **2025 es la versión vigente**; la
2021 sigue siendo ampliamente citada y es la que menciona el enunciado del docente de forma
genérica.

> **Recomendación**: citar la edición **2025** como vigente y mencionar la 2021 por continuidad,
> ya que gran parte de la documentación de fabricantes de WAF todavía referencia la 2021.

**OWASP Top 10:2025** — categorías:

| ID | Categoría |
|---|---|
| A01 | Broken Access Control |
| A02 | Security Misconfiguration |
| A03 | Software Supply Chain Failures |
| A04 | Cryptographic Failures |
| A05 | Injection |
| A06 | Insecure Design |
| A07 | Authentication Failures |
| A08 | Software or Data Integrity Failures |
| A09 | Security Logging and Alerting Failures |
| A10 | Mishandling of Exceptional Conditions |

- Open Worldwide Application Security Project. (2025). *OWASP Top 10:2025*. https://owasp.org/Top10/2025/
- Open Worldwide Application Security Project. (2021). *OWASP Top 10:2021*. https://owasp.org/Top10/2021/

**Aplicación al caso**: las debilidades de las apps de la DMZ (D-01) mapean directamente a
**A05 Injection** (Portal de Proveedores sin validación de carga de archivos), **A01 Broken
Access Control** (Portal de Clientes con conexión directa a la BD del ERP) y **A02 Security
Misconfiguration** / **A07 Authentication Failures** (credenciales estáticas embebidas en el
código del Sistema de Rastreo).

---

## 2. Ciclo de vida de productos Microsoft — sustento de D-10

Fuente: portal oficial Microsoft Lifecycle. Fechas mostradas en zona horaria del Pacífico (PT).

| Producto | Fin de soporte general | Fin de soporte extendido | Estado |
|---|---|---|---|
| **Windows Server 2012 R2** | 9 oct 2018 | **10 de octubre de 2023** | Sin soporte. ESU disponible hasta el **13 de octubre de 2026** (de pago, renovable anualmente) |
| **Windows 8.1** | 9 ene 2018 | **10 de enero de 2023** | Sin soporte. **Sin programa ESU** para consumidores |
| **Windows 7** | 13 ene 2015 | **14 de enero de 2020** | Sin soporte. ESU finalizó el **10 de enero de 2023** |

> **Uso en el proyecto**: estos son los datos duros que convierten D-10 de una afirmación
> general ("sistemas desactualizados") en un hallazgo con severidad cuantificable: los
> servidores del ERP y las estaciones de trabajo llevan **entre 3 y 6 años sin recibir parches
> de seguridad**, lo que significa que toda vulnerabilidad publicada desde entonces permanece
> explotable sin remedio disponible.

- Microsoft. (2023). *Windows Server 2012 and 2012 R2 reaching end of support*. Microsoft Lifecycle. https://learn.microsoft.com/en-us/lifecycle/announcements/windows-server-2012-r2-end-of-support
- Microsoft. (2022). *Windows 8.1 — Microsoft Lifecycle*. https://learn.microsoft.com/en-us/lifecycle/products/windows-81
- Microsoft. (2022). *Windows 7 — Microsoft Lifecycle*. https://learn.microsoft.com/en-us/lifecycle/products/windows-7
- Microsoft. (2023). *Overview of Extended Security Updates for Windows Server 2012 and 2012 R2*. https://learn.microsoft.com/en-us/windows-server/get-started/extended-security-updates-overview

---

## 3. Obsolescencia criptográfica — sustento de D-03

### 3.1 IKEv1 está formalmente deprecado

**Dato verificado**: el IETF publicó en **abril de 2023** el RFC 9395, que **deprecia IKEv1** y
mueve los RFC 2407, 2408 y 2409 a estado **Historic**. IANA cerró los registros
"Internet Key Exchange (IKE) Attributes" y "Magic Numbers for ISAKMP Protocol", agregando la
nota: *"All registries listed below have been closed. See RFC 9395."*

> Esto es **más fuerte que decir "obsoleto"**: significa que el protocolo que sostiene la VPN
> entre Jutiapa y Chiquimula ya no es un estándar vigente de Internet, y que su registro de
> parámetros está cerrado a nuevas asignaciones.

- Smyslov, V., & Hoffman, P. (2023). *Deprecation of the Internet Key Exchange version 1 (IKEv1) protocol and obsoleted algorithms* (RFC 9395). Internet Engineering Task Force. https://doi.org/10.17487/RFC9395
- Texto completo: https://www.rfc-editor.org/rfc/rfc9395.html

### 3.2 SHA-1 está retirado

**Dato verificado**: NIST anunció en diciembre de 2022 el retiro de SHA-1. La eliminación total
está fijada al **31 de diciembre de 2030**, fecha en la que se publicará FIPS 180-5 removiendo
la especificación. Los ataques de colisión demostrados en la práctica son la causa.

Cita textual de NIST: *"We recommend that anyone relying on SHA-1 for security migrate to
SHA-2 or SHA-3 as soon as possible"* (Chris Celi, científico de cómputo de NIST).

- National Institute of Standards and Technology. (2022, 15 de diciembre). *NIST retires SHA-1 cryptographic algorithm*. https://www.nist.gov/news-events/news/2022/12/nist-retires-sha-1-cryptographic-algorithm
- National Institute of Standards and Technology. (2022). *NIST transitioning away from SHA-1 for all applications*. CSRC. https://csrc.nist.gov/news/2022/nist-transitioning-away-from-sha-1-for-all-apps

### 3.3 3DES / TDEA en retiro

**Dato verificado**: NIST SP 800-131A Rev. 2 establece la estrategia y el calendario de retiro
del Triple Data Encryption Algorithm (TDEA). El documento define la transición hacia AES-128,
AES-192 y AES-256, y hacia la familia SHA-2.

- Barker, E., & Roginsky, A. (2019). *Transitioning the use of cryptographic algorithms and key lengths* (NIST SP 800-131A Rev. 2). National Institute of Standards and Technology. https://doi.org/10.6028/NIST.SP.800-131Ar2
- PDF directo: https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-131Ar2.pdf

> Existe un **borrador de la Rev. 3** (SP 800-131A Rev. 3 ipd) en consulta pública:
> https://csrc.nist.gov/pubs/sp/800/131/a/r3/ipd

### 3.4 Configuración objetivo para el reemplazo de la VPN (Fase 2 / Fase 4)

Derivado de las tres fuentes anteriores, la configuración destino que debe proponerse:

| Parámetro | Estado actual (D-03) | Estado objetivo | Sustento |
|---|---|---|---|
| Protocolo de intercambio de claves | IKEv1 | **IKEv2** | RFC 9395 |
| Cifrado | 3DES | **AES-256-GCM** | NIST SP 800-131A Rev. 2 |
| Integridad / hash | SHA-1 | **SHA-256 o superior (SHA-2)** | NIST SHA-1 retirement |
| Grupo Diffie-Hellman | *(no especificado en el caso — supuesto)* | **Grupo 19/20 (ECDH P-256/P-384) o superior** | NIST SP 800-131A Rev. 2 |
| Perfect Forward Secrecy | *(no especificado — supuesto)* | **Habilitado** | Buena práctica |

> ⚠️ Las filas marcadas como supuesto deben registrarse en la tabla §10 de `CLAUDE.md`.

---

## 4. Pendientes de verificación — Fase 4

El enunciado §7.1 exige **validar y actualizar al menos tres referencias de precio** mediante
cotización o investigación directa con un proveedor o distribuidor autorizado en Guatemala o la
región, **citando la fuente**.

Esta sección se llena al ejecutar la Fase 4.

| # | Rubro | Fuente de precio | Fecha de consulta | Tipo de evidencia | Estado |
|---|---|---|---|---|---|
| 1 | *(pendiente)* | | | | `[ ]` |
| 2 | *(pendiente)* | | | | `[ ]` |
| 3 | *(pendiente)* | | | | `[ ]` |

**Tipos de evidencia aceptados** (§7.5): captura de pantalla, enlace, o constancia de contacto
con un distribuidor/proveedor.

**Nota metodológica**: los precios con lista pública verificable (Cloudflare, Microsoft 365 /
Entra ID, AWS, Cisco Umbrella) son los más fáciles de citar con enlace y fecha. Los rubros de
hardware (FortiGate, switches, UPS, planta eléctrica) generalmente requieren contacto con
distribuidor local, porque no publican lista.

---

## 5. Contexto guatemalteco — pendiente para el escenario E-07

El DRP debe contemplar "eventos propios del contexto guatemalteco: sismos/terremotos, tormentas
tropicales e inundaciones estacionales en la región oriental" (§6.3).

Fuentes institucionales a consultar al desarrollar E-07:

| Institución | Utilidad | Sitio |
|---|---|---|
| INSIVUMEH | Datos sísmicos e hidrometeorológicos, temporada de lluvias | https://insivumeh.gob.gt |
| CONRED | Coordinadora Nacional para la Reducción de Desastres; protocolos y mapas de amenaza | https://conred.gob.gt |

> **Pendiente**: verificar estas fuentes al desarrollar la Fase 3. No se han consultado aún.

---

## 6. Documentación de fabricantes — Fase 4

A consultar al justificar cada solución propuesta (§7.2). No verificadas aún.

| Fabricante | Producto relevante | Rubro |
|---|---|---|
| Fortinet | FortiGate 60F/100F, FortiWeb, FortiNAC, FortiDeceptor | Firewall HA, WAF, NAC, Honeypot |
| Cisco | Secure Firewall, Meraki MX, ISE, Umbrella, Duo | Firewall, SD-WAN, NAC, DNS, MFA |
| Palo Alto Networks | PA-4xx, Prisma SD-WAN | Firewall HA, SD-WAN |
| Microsoft | Entra ID P1, Defender for Endpoint, Sentinel, Windows Server 2022/2025 | MFA, EDR, SIEM, renovación SO |
| Cloudflare | WAF, Magic Transit, Gateway | WAF, Anti-DDoS, DNS |
| Veeam | Backup & Replication, Cloud Connect | Respaldo 3-2-1 inmutable |
| APC / Vertiv | Smart-UPS, Symmetra, NetBotz, Environet | Energía y monitoreo ambiental |
| Wazuh | Wazuh (open source) | SIEM |

---

## Registro de cambios

| Fecha | Cambio |
|---|---|
| 2026-09-05 | Creación. Verificadas: ISO 27001:2022, NIST CSF 2.0, CIS v8.1, ciclo de vida Microsoft (WS2012R2, Win7, Win8.1), RFC 9395, retiro de SHA-1, NIST SP 800-131A Rev. 2, OWASP Top 10 2021/2025 |
| 2026-09-07 | Agregadas para la Fase 2: NIST SP 800-207 (Zero Trust), NIST SP 800-63B-4 (autenticación), CISA phishing-resistant MFA, Veeam 3-2-1-1-0, ISA/IEC 62443 + modelo Purdue (OT), WPA3-Enterprise/802.1X. Consultadas el 7 de septiembre de 2026 |
