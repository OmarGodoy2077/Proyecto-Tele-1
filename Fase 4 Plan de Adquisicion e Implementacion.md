---
**Universidad Mariano Gálvez de Guatemala** — Facultad de Ingeniería en Sistemas de Información
**Campus:** Jutiapa · **Curso:** Telecomunicaciones (Área de Especialidad) · **Unidad integradora:** Seguridad de Redes
**Docente:** Ing. Juan Daniel Ramos Martínez · **Ciclo:** Segundo Semestre 2026
**Proyecto No. 01 — Fase 4: Plan de Adquisición e Implementación de Infraestructura de Ciberseguridad**
**Caso de estudio:** TransAgro del Oriente, S.A.
**Integrantes:** _(completar)_ · **Fecha de entrega:** _(completar)_
---

# Plan de Adquisición e Implementación de Infraestructura de Ciberseguridad

## TransAgro del Oriente, S.A.

---

## Control de versiones

| Versión | Fecha | Autor / rol | Descripción del cambio | Aprobado por |
|---|---|---|---|---|
| 0.1 | 2026-09-08 | Especialista en adquisiciones e infraestructura | Redacción inicial completa: metodología, marco de referencia de soluciones (31 rubros de inversión organizados en 6 bloques), estructura de talento humano, estimación consolidada CAPEX/OPEX, propuesta de fases de implementación, verificación independiente de 5 precios oficiales vigentes y cierre de la matriz de trazabilidad D→R→C→E→I (17/17 debilidades con rubro asignado). | _(pendiente)_ |
| _(borrador)_ | | | Revisión del Redactor técnico y del Coordinador; consolidación con Fases 1–3 en el documento final. | |

**Clasificación del documento:** USO INTERNO — distribución restringida a Dirección, Gerencia de TI y responsables designados.
**Documento propietario:** Gerencia de Tecnología de la Información de TransAgro del Oriente, S.A.
**Moneda de referencia:** Dólares de los Estados Unidos (US$), por ser la moneda en que cotizan la mayoría de fabricantes y proveedores cloud citados. Equivalencia en quetzales calculada al tipo de cambio de referencia del Banco de Guatemala del **7 de septiembre de 2026: Q7.6222 por US$1.00** (Banco de Guatemala, 2026), únicamente para dimensionar el presupuesto ante Dirección; el valor exacto a pagar dependerá del tipo de cambio y de las condiciones vigentes al momento de la compra.

---

## Índice

1. Alcance y objetivo del Plan de Adquisición
2. Metodología de la propuesta técnico-económica
3. Marco de referencia de soluciones, marcas y arquitecturas
   3.1 Seguridad perimetral y de aplicaciones (DMZ)
   3.2 Comunicaciones entre sedes y acceso remoto
   3.3 Identidad, acceso y red interna
   3.4 Protección de endpoints y gestión de sistemas
   3.5 Seguridad física y continuidad del centro de datos
   3.6 Respaldo, monitoreo y gestión de incidentes
4. Equipo humano de respuesta a incidentes y ciberseguridad
5. Estimación de inversión consolidada (CAPEX / OPEX)
6. Propuesta de fases de implementación
7. Anexos
   A. Tabla de trazabilidad D-nn → R-nn → C-nn → E-nn → I-nn (cierre de la cadena)
   B. Evidencia de verificación independiente de precios (mínimo 3 exigido)
   C. Glosario de términos específicos de la Fase 4
   D. Referencias
8. Entregable de la Fase 4 y cierre

---

## Nota metodológica y de trazabilidad

Este es el **cuarto y último entregable técnico** del Proyecto No. 01, elaborado desde el rol de **Especialista en adquisiciones e infraestructura**. Toma como insumo directo:

- La **Fase 1** (checklist de 43 ítems, matriz de riesgos R-01 a R-10 y conclusión ejecutiva de 5 riesgos críticos).
- La **Fase 2 — Plan de Seguridad Informática** (30 controles C-01 a C-30, cada uno con un rubro de inversión `I-xxx` ya declarado en su ficha y en el Anexo C/D de ese documento).
- La **Fase 3 — DRP**, de la que se toman los escenarios `E-nn` y los componentes con RTO/RPO que condicionan el dimensionamiento de la plataforma de respaldo y del sitio alterno.

Se conserva la convención de identificadores del proyecto:

| Prefijo | Significado | Fase |
|---|---|---|
| `D-nn` | Debilidad del caso (enunciado §2.4) | Insumo |
| `R-nn` | Riesgo de la matriz de riesgos | Fase 1 |
| `C-nn` | Control / medida del Plan de Seguridad | Fase 2 |
| `E-nn` | Escenario de desastre del DRP | Fase 3 |
| `I-xxx` | Rubro de inversión (CAPEX/OPEX) | **Fase 4** |

A diferencia de las fases anteriores, esta Fase **no introduce numeración secuencial nueva** (`I-01, I-02…`): reutiliza literalmente los códigos `I-xxx` que la Fase 2 ya asignó a cada control en su Anexo C ("Inversión (Fase 4)"), de modo que un mismo nombre de rubro identifique la misma partida presupuestaria en ambos documentos. El **§7** de este documento cierra esa cadena: de los **31 rubros de inversión** que aquí se presupuestan, se verifica que las **17 debilidades** del caso queden cubiertas (Anexo A).

**Regla de validación de precios (enunciado §7.1 y §4.D del checklist maestro del repositorio):** de los 31 rubros, al menos tres deben validarse con una fuente de precio actual e independiente, citada con enlace y fecha de consulta. Este documento valida **cinco**: Microsoft Entra ID (MFA), Cloudflare Business (WAF), AWS Shield Advanced (Anti-DDoS), CrowdStrike Falcon (EDR) y Microsoft Defender for Business Suite (referencia complementaria de endpoint). El detalle de la verificación está en el **Anexo B**.

---

# 1. Alcance y objetivo del Plan de Adquisición

## 1.1 Propósito

Traducir los controles definidos en el Plan de Seguridad Informática (Fase 2) y los requisitos de continuidad del DRP (Fase 3) en una **propuesta de inversión concreta, priorizada y presupuestada**: qué se compra o se contrata, con qué arquitectura, de qué proveedor, a qué costo referencial (validado cuando es posible) y en qué orden, de modo que la Gerencia General de TransAgro del Oriente, S.A. cuente con la información suficiente para aprobar un presupuesto plurianual de ciberseguridad.

## 1.2 Alcance

Este Plan cubre los **31 rubros de inversión** (`I-xxx`) que se derivan de los 30 controles de la Fase 2, agrupados en:

- Hardware y software de seguridad perimetral, de red, de endpoint y de datacenter (**CAPEX**).
- Suscripciones, licenciamiento cloud y servicios administrados (**OPEX**).
- Talento humano de seguridad de la información, ya sea por contratación directa o por servicio tercerizado (**OPEX**, componente obligatorio del enunciado §7.3).

Quedan **fuera de alcance**: la inversión en sistemas de negocio no relacionados con seguridad (por ejemplo, una nueva versión del ERP más allá de lo estrictamente necesario para retirar el sistema operativo sin soporte), y la obra civil no asociada a seguridad física del centro de datos.

## 1.3 Relación con las Fases 1–3

| Fase previa | Qué aporta a la Fase 4 |
|---|---|
| Fase 1 | Prioriza: los rubros ligados a los riesgos **R-01 a R-04 (CRÍTICO)** se tratan como Prioridad 1; los ligados a **R-05 a R-10 (ALTO)** como Prioridad 2. |
| Fase 2 | Define el **requisito funcional** de cada control (qué debe hacer la solución) y el código `I-xxx` que aquí se presupuesta. |
| Fase 3 (DRP) | Define el **RTO/RPO** de cada componente crítico, lo que dimensiona la plataforma de respaldo (`I-Respaldo`) y condiciona la estrategia de sitio alterno (§6.5 del DRP), cuyo CAPEX/OPEX se estima en el §5.7 de este documento. |

## 1.4 Criterios de éxito de la propuesta

1. **Cobertura:** las 17 debilidades del caso (`D-01`–`D-17`) tienen al menos un rubro de inversión asignado (verificado en el Anexo A).
2. **Verificación:** al menos tres precios están validados de forma independiente con fuente y fecha (Anexo B); se cumple con cinco.
3. **Priorización defendible:** ningún rubro asociado a un riesgo CRÍTICO de la Fase 1 queda en la última fase de implementación.
4. **Talento humano incluido:** la propuesta no se limita a tecnología; dimensiona el rol de seguridad de la información inexistente hoy en TransAgro (§4).
5. **Trazabilidad completa:** cada rubro declara explícitamente qué `D-nn`, `C-nn` y `E-nn` remedia.

---

# 2. Metodología de la propuesta técnico-económica

## 2.1 De la brecha al rubro de inversión

Para cada uno de los 30 controles de la Fase 2 se verificó si su implementación requiere una adquisición (hardware, software, suscripción o servicio) distinta de las ya existentes en TransAgro. El resultado son los **31 rubros `I-xxx`** del §3, agrupados en los mismos seis bloques del marco de referencia del enunciado (§7.2.1–§7.2.6): perímetro y DMZ; comunicaciones; identidad y red interna; endpoints; físico/datacenter; respaldo-monitoreo-incidentes.

## 2.2 Priorización

La prioridad de cada rubro se deriva **directamente** de la matriz de riesgos de la Fase 1 (no de un criterio nuevo): un rubro que remedia una debilidad asociada a un riesgo **CRÍTICO** (R-01 a R-04, todos con P×I ≥ 20) se clasifica **CRÍTICA**; uno que remedia solo debilidades asociadas a riesgos **ALTO** (R-05 a R-10, P×I 12–15) se clasifica **ALTA**; los complementarios u opcionales que refuerzan un control ya cubierto por otro rubro de mayor prioridad (por ejemplo, Honeypot o NDR) se clasifican **MEDIA**. Ningún rubro de este Plan cae en BAJA, porque los diez riesgos que la Fase 2 trata (R-01–R-10) son, en conjunto, todos CRÍTICO o ALTO.

## 2.3 CAPEX vs. OPEX

Se separa **gasto de capital (CAPEX)** — equipo, licencias perpetuas, obra de acondicionamiento — de **gasto operativo recurrente (OPEX)** — suscripciones SaaS/cloud, soporte y mantenimiento anual, personal. La mayoría de los controles de red y de aplicación de este proyecto se resuelven hoy con modelos **híbridos** (appliance con licenciamiento anual, o servicio cloud puro): donde aplica, se declara el CAPEX inicial y el OPEX del primer año por separado, conforme al formato exigido en el enunciado §7.4.

## 2.4 Reglas de validación de precios

1. Los precios del enunciado (§7.2, tablas del docente) son un piso de referencia didáctica; no se citan como verificados salvo que se confirmen de forma independiente.
2. Un precio se marca **✔ VERIFICADO** solo si proviene de la lista de precios pública y vigente del propio fabricante o proveedor cloud, con URL y fecha de consulta (Anexo B); se marca **○ Referencia de mercado** si proviene de la tabla del enunciado o de un rango de mercado no verificado directamente en esta iteración, y queda pendiente de cotización formal con un distribuidor autorizado en Guatemala o la región antes de la ejecución del presupuesto (tal como exige el enunciado §7.1 y el registro `R-1` de precios pendientes del repositorio del curso).
3. Los rubros de hardware especializado (firewall, UPS, planta eléctrica, control de acceso físico) casi nunca publican lista de precios pública — requieren cotización directa con un integrador local; se mantienen como referencia de mercado y se marca explícitamente la acción pendiente ("cotizar con distribuidor autorizado en Guatemala").
4. Toda cifra en quetzales es una conversión referencial al tipo de cambio del §"Control de versiones"; no sustituye una cotización formal en la moneda de cierre del contrato.

## 2.5 Convención de las tablas del §3

Cada tabla de rubro declara:

> **I-xxx — Nombre del rubro.** Remedia: `D-nn`. Soporta control(es): `C-nn` (Fase 2). Soporta escenario DRP: `E-nn` (Fase 3). Prioridad: CRÍTICA / ALTA / MEDIA (según §2.2).

seguida de la tabla de solución de referencia, marca/producto, proveedor y precio (con la marca ✔/○ de verificación).

---

# 3. Marco de referencia de soluciones, marcas y arquitecturas

> Los modelos y marcas propuestos son ejemplos representativos del mercado; el grupo puede proponer marcas distintas si las justifica técnicamente (throughput requerido, número de usuarios, presupuesto disponible, soporte local), conforme al enunciado §7.1.

## 3.1 Seguridad perimetral y de aplicaciones (DMZ)

### I-NGFW-HA — Clúster de firewall perimetral en alta disponibilidad

> Remedia: `D-02`, `D-04` (falla del borde). Soporta: `C-13`. Soporta escenario: `E-02`. Prioridad: **CRÍTICA** (R-02, P×I=20).

| Solución de referencia | Marca / producto | Proveedor | Precio referencial | Verificación |
|---|---|---|---|---|
| Dos equipos NGFW en clúster activo-pasivo, con IPS integrado e inspección de tráfico DMZ/interna | Fortinet FortiGate 100F · Palo Alto PA-4xx · Cisco Secure Firewall · Sophos XGS | Distribuidor autorizado local / integrador de seguridad regional | **US$ 6,500 – 19,000** (par de equipos) + **US$ 1,200 – 3,000/año** de licenciamiento (UTP/soporte) | ○ Referencia de mercado — cotizar con distribuidor local |

### I-WAF — Web Application Firewall para las tres aplicaciones publicadas

> Remedia: `D-01`. Soporta: `C-19`. Soporta escenario: `E-04`. Prioridad: **CRÍTICA** (R-01, P×I=25).

| Solución de referencia | Marca / producto | Proveedor | Precio referencial | Verificación |
|---|---|---|---|---|
| WAF como proxy inverso en la nube (cubre las reglas OWASP Top 10:2025 para los tres portales) | **Cloudflare Business** (incluye WAF gestionado) · alternativas: AWS WAF, F5 Distributed Cloud WAF, Fortinet FortiWeb | Cloudflare, Inc. (contratación directa vía portal) | **US$ 200/mes facturado anual, o US$ 250/mes mensual** (plan Business) | **✔ VERIFICADO** — Cloudflare, *Plans* (2026); consultado el 8 de septiembre de 2026 |

### I-AntiDDoS — Protección Anti-DDoS volumétrica y de aplicación

> Remedia: `D-01`. Soporta: `C-20`. Soporta escenario: `E-08`. Prioridad: **CRÍTICA** (R-01/R-02).

| Solución de referencia | Marca / producto | Proveedor | Precio referencial | Verificación |
|---|---|---|---|---|
| Mitigación gestionada en la nube, con SLA de tiempo de respuesta | **AWS Shield Advanced** · alternativas: Cloudflare Magic Transit, Radware Cloud DDoS Protection | Amazon Web Services (si la infraestructura pública migra a AWS) / proveedor cloud equivalente | **US$ 3,000/mes** de suscripción (por cuenta de facturación, compromiso de 1 año) + tarifas de transferencia de datos desde US$ 0.025/GB | **✔ VERIFICADO** — AWS, *Shield Pricing* (2026); consultado el 8 de septiembre de 2026. Nota: si TransAgro no migra su DMZ a AWS, la alternativa equivalente es la protección Anti-DDoS incluida en el plan Cloudflare Business (I-WAF) o un servicio administrado del propio ISP — **cotizar ambas opciones antes de decidir** |

### I-DNSSecurity — Protección y filtrado de DNS

> Remedia: `D-01`. Soporta: `C-21`. Soporta escenario: `E-04`, `E-05`. Prioridad: **CRÍTICA** (R-01, R-03).

| Solución de referencia | Marca / producto | Proveedor | Precio referencial | Verificación |
|---|---|---|---|---|
| Resolución DNS gestionada que bloquea dominios maliciosos y de phishing, aplicable a usuarios internos y portátiles | Cisco Umbrella DNS Security · Infoblox BloxOne Threat Defense · Cloudflare Gateway (DNS) | Distribuidor autorizado Cisco/Infoblox en la región / Cloudflare directo | **US$ 2.50 – 4.00/usuario/mes** | ○ Referencia de mercado — Cisco Umbrella no publica lista de precios pública (portal de ventas confirma cotización por contacto directo); cotizar con distribuidor |

### I-Honeypot — Honeypot / Deception (complementario, opcional)

> Remedia: `D-01` (detección temprana, complementa `C-19`–`C-21`). Soporta: `C-14.6`. Prioridad: **MEDIA** (complementario, no obligatorio según Fase 2 §6.8.1).

| Solución de referencia | Marca / producto | Proveedor | Precio referencial | Verificación |
|---|---|---|---|---|
| Señuelos que simulan servicios reales en la DMZ y en segmentos internos críticos | Fortinet FortiDeceptor (comercial) · T-Pot / Cowrie (open source) | Distribuidor Fortinet / implementación interna (open source) | **US$ 0 (open source, solo horas internas) – 12,000** (appliance comercial) | ○ Referencia de mercado (tabla del enunciado) |

### I-Segmentación-DMZ — Rediseño de la DMZ y capa de servicios intermedia

> Remedia: `D-01`. Soporta: `C-14`. Soporta escenario: `E-04`. Prioridad: **CRÍTICA** (R-01).

| Solución de referencia | Marca / producto | Proveedor | Precio referencial | Verificación |
|---|---|---|---|---|
| Separación de las tres aplicaciones en subsegmentos distintos + capa de API intermedia que aísla la base de datos del ERP de la DMZ; principalmente horas de arquitectura/desarrollo, no licenciamiento | Desarrollo interno o consultoría de arquitectura + reutiliza el NGFW (I-NGFW-HA) para las nuevas reglas de segmentación | Integrador de seguridad / equipo de desarrollo interno del ERP | **US$ 8,000 – 20,000** (proyecto de arquitectura e implementación, una sola vez) | ○ Estimación de esfuerzo — cotizar con integrador o dimensionar con horas internas |

### I-GestiónSecretos — Bóveda de secretos y gestión de identidades no humanas

> Remedia: `D-01` (credenciales estáticas del Rastreo de Flotilla), `D-17`. Soporta: `C-07`. Soporta escenario: `E-04`. Prioridad: **CRÍTICA** (R-01, R-06).

| Solución de referencia | Marca / producto | Proveedor | Precio referencial | Verificación |
|---|---|---|---|---|
| Bóveda de secretos con rotación automática, control de acceso por rol y auditoría | HashiCorp Vault (self-hosted, open source, o HCP Vault administrado) · CyberArk Conjur · Azure Key Vault | Licenciamiento cloud directo / distribuidor | **US$ 0 (open source, horas internas) – 1,500/mes** (servicio administrado según volumen de secretos) | ○ Referencia de mercado |

## 3.2 Comunicaciones entre sedes y acceso remoto

### I-SD-WAN/VPN — Reemplazo de la VPN sitio a sitio y evaluación de SD-WAN

> Remedia: `D-03`. Soporta: `C-23`. Soporta escenario: `E-03`. Prioridad: **ALTA** (R-08, P×I=12).

| Solución de referencia | Marca / producto | Proveedor | Precio referencial | Verificación |
|---|---|---|---|---|
| Túneles IPsec IKEv2/AES-256-GCM/SHA-2 con selección dinámica de ruta entre Jutiapa y Chiquimula | Fortinet Secure SD-WAN (FortiGate 60F/100F) · Cisco Meraki MX · Palo Alto Prisma SD-WAN | Distribuidor autorizado / integrador de redes | **US$ 1,200 – 4,500** por sede (equipo) + **US$ 300 – 700/año** de licenciamiento | ○ Referencia de mercado — cotizar con distribuidor local |

### I-SegundoISP — Redundancia del enlace a Internet

> Remedia: `D-04`. Soporta: `C-24`. Soporta escenario: `E-08`. Prioridad: **CRÍTICA** (R-02, R-08).

| Solución de referencia | Marca / producto | Proveedor | Precio referencial | Verificación |
|---|---|---|---|---|
| Segundo proveedor de Internet con ruta física distinta, para Jutiapa y, en lo posible, Chiquimula, con failover automático | ISP local/regional alterno (fibra o inalámbrico según cobertura) | Segundo ISP local | **US$ 150 – 700/mes** por sede (según ancho de banda contratado) | ○ Referencia de mercado — cotizar con al menos dos ISP locales en Jutiapa y Chiquimula |

## 3.3 Identidad, acceso y red interna

### I-MFA — Autenticación multifactor (MFA/2FA)

> Remedia: `D-05`. Soporta: `C-22`. Soporta escenario: `E-04`, `E-05`. Prioridad: **CRÍTICA** (R-03, R-06, R-07).

| Solución de referencia | Marca / producto | Proveedor | Precio referencial | Verificación |
|---|---|---|---|---|
| Segundo factor obligatorio para VPN, correo, dominio (Active Directory) y consolas de administración; integración con el directorio existente | **Microsoft Entra ID P1** (segundo factor, SSO, políticas de acceso condicional) · alternativas: Cisco Duo, Fortinet FortiToken | Licenciamiento cloud Microsoft (CSP) | **US$ 7.00/usuario/mes** (Entra ID P1, facturación anual) — para ~480 colaboradores: **≈ US$ 40,320/año**; el nivel **P2** (con protección de identidad basada en riesgo) cuesta **US$ 10.00/usuario/mes** | **✔ VERIFICADO** — Microsoft, *Microsoft Entra Pricing* (2026); consultado el 8 de septiembre de 2026 |

### I-PAM — Gestión de identidades privilegiadas, cuentas nominadas y accesos de terceros

> Remedia: `D-05`, `D-06`, `D-17`. Soporta: `C-15`, `C-05`. Soporta escenario: `E-04`, `E-05`. Prioridad: **CRÍTICA** (R-03, R-06, R-07).

| Solución de referencia | Marca / producto | Proveedor | Precio referencial | Verificación |
|---|---|---|---|---|
| Bóveda de credenciales privilegiadas, acceso *just-in-time*, grabación de sesión y jump host para administradores y terceros (integrador, consultor ERP, SaaS de flotilla) | CyberArk PAM · Delinea (Thycotic) Secret Server · BeyondTrust Password Safe | Distribuidor autorizado / licenciamiento directo | **US$ 8,000 – 30,000/año** (licenciamiento + reconfiguración inicial, según número de cuentas privilegiadas) | ○ Referencia de mercado — cotizar con distribuidor; alternativa de menor costo: módulo PAM incluido en Microsoft Entra ID P2 (Privileged Identity Management) ya cubierto por I-MFA |

### I-Segmentación-VLAN — Segmentación de la red interna en VLAN + reconfiguración de switching

> Remedia: `D-07`. Soporta: `C-25`. Soporta escenario: `E-05`. Prioridad: **CRÍTICA** (R-03, P×I=20).

| Solución de referencia | Marca / producto | Proveedor | Precio referencial | Verificación |
|---|---|---|---|---|
| Diseño de al menos 6 VLAN por función (administración, servidores, DMZ, cámaras, OT/PLC bajo modelo de zonas y conductos ISA/IEC 62443, invitados) con ACL inter-VLAN en el switch de capa 3 o en el firewall | Cisco Catalyst (switching gestionado) · Aruba switches · reconfiguración del NGFW ya adquirido (I-NGFW-HA) | Distribuidor autorizado / integrador de redes | **US$ 8,000 – 30,000** (licenciamiento de switches gestionados si se requiere reemplazo + horas de reconfiguración) | ○ Referencia de mercado — depende del inventario de switches actual (a auditar antes de cotizar) |

### I-NAC — Control de acceso a la red (NAC) con 802.1X

> Remedia: `D-09`. Soporta: `C-26`. Soporta escenario: `E-05`. Prioridad: **CRÍTICA** (R-03).

| Solución de referencia | Marca / producto | Proveedor | Precio referencial | Verificación |
|---|---|---|---|---|
| NAC con autenticación 802.1X, perfilado de dispositivos IoT/OT (MAB) y cuarentena automática, en modo monitor y luego enforcement | Cisco ISE · Aruba ClearPass · FortiNAC + FortiSwitch | Distribuidor autorizado / integrador de redes | **US$ 8,000 – 30,000** (licenciamiento + reconfiguración de switching) | ○ Referencia de mercado — cotizar con distribuidor |

### I-WLAN — Red inalámbrica corporativa WPA3-Enterprise y red de invitados aislada

> Remedia: `D-08`. Soporta: `C-27`. Soporta escenario: `E-05`. Prioridad: **ALTA** (complementa la segmentación crítica, pero su ausencia hoy es un vector de acceso, no la causa raíz de R-03).

| Solución de referencia | Marca / producto | Proveedor | Precio referencial | Verificación |
|---|---|---|---|---|
| Controlador WLAN con SSID corporativo 802.1X/EAP-TLS y SSID de invitados con portal cautivo aislado | Cisco Meraki MR · Aruba Instant On/AP · Ubiquiti UniFi (gama media) | Distribuidor autorizado / integrador de redes | **US$ 250 – 900** por punto de acceso + licenciamiento cloud del controlador | ○ Referencia de mercado |

### I-Inventario — Plataforma de inventario único de activos de hardware y software

> Remedia: `D-09`, `D-11`. Soporta: `C-01`. Soporta escenario: `E-05`. Prioridad: **CRÍTICA** (R-03; es prerrequisito de NAC y EDR).

| Solución de referencia | Marca / producto | Proveedor | Precio referencial | Verificación |
|---|---|---|---|---|
| Descubrimiento automático y consola central de inventario (hardware, SO, parches, agentes de seguridad) | Incluido en la mayoría de plataformas EDR/gestor de parches (ManageEngine, Microsoft Intune) o herramienta dedicada (Lansweeper, Device42) | Licenciamiento cloud/on-prem | **US$ 0 – 3/dispositivo/mes** (si se usa el módulo de inventario ya incluido en el EDR o en el gestor de parches, el costo incremental es marginal) | ○ Referencia de mercado — evaluar bundling con I-EDR e I-Parches antes de licenciar por separado |

## 3.4 Protección de endpoints y gestión de sistemas

### I-EDR — Plataforma de detección y respuesta en endpoint (EDR)

> Remedia: `D-11`. Soporta: `C-28`. Soporta escenario: `E-04`, `E-05`. Prioridad: **CRÍTICA** (R-03, P×I=20).

| Solución de referencia | Marca / producto | Proveedor | Precio referencial | Verificación |
|---|---|---|---|---|
| EDR con protección en tiempo real, análisis de comportamiento y aislamiento remoto en el 100 % de servidores y estaciones de ambas sedes | **CrowdStrike Falcon Go** (hasta 100 dispositivos) o **Falcon Pro** · alternativas: SentinelOne Singularity, Microsoft Defender for Endpoint, ESET PROTECT Advanced | Distribuidor autorizado / licenciamiento cloud directo | **US$ 7.99/dispositivo/mes** (Falcon Go, facturación mensual, hasta 100 dispositivos) o **US$ 14.99/dispositivo/mes** (Falcon Pro, mayor cobertura de detección); para el parque completo de TransAgro (servidores + estaciones, orden de magnitud ~150–250 equipos) se requiere el nivel Pro o superior — **≈ US$ 27,000 – 45,000/año** | **✔ VERIFICADO** — CrowdStrike, *Falcon Pricing* (2026); consultado el 8 de septiembre de 2026. Referencia complementaria: Microsoft Defender (suite empaquetada con Microsoft 365 E5 Security) cotiza **US$ 12.00/usuario/mes** como parte de un bundle — **✔ VERIFICADO**, Microsoft (2026), aunque no es una licencia de EDR standalone y su costo real depende del nivel de Microsoft 365 ya contratado |

### I-RenovaciónSO — Migración de sistemas operativos sin soporte

> Remedia: `D-10`. Soporta: `C-16`. Soporta escenario: `E-05`. Prioridad: **CRÍTICA** (R-03, R-05).

| Solución de referencia | Marca / producto | Proveedor | Precio referencial | Verificación |
|---|---|---|---|---|
| Migración de Windows Server 2012 R2 (sin soporte desde el 10/oct/2023) a una versión con soporte vigente, priorizando los servidores del ERP y de la DMZ; migración de estaciones Windows 7/8.1 | Microsoft Windows Server 2022/2025 · distribuciones Linux empresariales con soporte (Red Hat Enterprise Linux, Ubuntu Pro) | Distribuidor Microsoft CSP / soporte de la distribución Linux | **US$ 900 – 1,100** por licencia de servidor (o suscripción anual equivalente en Linux); estaciones: costo de hardware si no admiten un SO con soporte (fuera de este rubro) | ○ Referencia de mercado. Nota de sustento: Microsoft confirma que el soporte extendido de WS2012 R2 terminó el 10 de octubre de 2023 y que las ESU de pago solo cubren hasta el 13 de octubre de 2026 — la migración no es opcional, es una ventana que se cierra (Microsoft, 2023) |

### I-Parches — Gestor centralizado de parches y hardening

> Remedia: `D-10`. Soporta: `C-16`. Soporta escenario: `E-05`. Prioridad: **CRÍTICA** (R-03, R-05).

| Solución de referencia | Marca / producto | Proveedor | Precio referencial | Verificación |
|---|---|---|---|---|
| Despliegue automatizado de actualizaciones críticas de SO y aplicaciones, con reportes de cumplimiento (ventana de despliegue ≤15 días, ≤72h para explotación activa, conforme a C-16.4) | ManageEngine Patch Manager Plus · Ivanti Patch Management · WSUS (gratuito, solo Microsoft) | Distribuidor autorizado / licenciamiento directo | **US$ 8 – 12/endpoint/año** | ○ Referencia de mercado |

### I-FiltradoCorreo — Filtrado avanzado de correo y autenticación de dominio (SPF/DKIM/DMARC)

> Remedia: `D-15`. Soporta: `C-21b`, `C-21c`. Soporta escenario: `E-04`, `E-05`. Prioridad: **ALTA** (R-07, P×I=16).

| Solución de referencia | Marca / producto | Proveedor | Precio referencial | Verificación |
|---|---|---|---|---|
| Sandbox de adjuntos, reescritura de enlaces, cuarentena y publicación/endurecimiento de registros SPF, DKIM y DMARC (sin costo de licenciamiento adicional si ya existe Microsoft 365, solo horas de configuración) | Microsoft Defender for Office 365 · Proofpoint Essentials · Mimecast | Licenciamiento cloud directo | **US$ 2 – 5/usuario/mes** (nivel de filtrado avanzado); SPF/DKIM/DMARC: **US$ 0** de licenciamiento, solo horas de configuración DNS | ○ Referencia de mercado |

## 3.5 Seguridad física y continuidad del centro de datos

### I-ControlAccesoFísico — Control de acceso biométrico o por tarjeta

> Remedia: `D-12`. Soporta: `C-12(a)`. Soporta escenario: `E-01`, `E-07`. Prioridad: **ALTA** (R-10, P×I=12).

| Solución de referencia | Marca / producto | Proveedor | Precio referencial | Verificación |
|---|---|---|---|---|
| Lector biométrico o de tarjeta en la puerta del centro de datos (Jutiapa) y del cuarto de telecomunicaciones (Chiquimula), con bitácora electrónica | HID Signo · Axis Communications | Integrador de seguridad física local | **US$ 1,200 – 3,000** por sede (control de acceso de una puerta) | ○ Referencia de mercado |

### I-CCTV — Videovigilancia con retención mínima de 30 días

> Remedia: `D-12`. Soporta: `C-12(b)`. Soporta escenario: `E-01`. Prioridad: **ALTA** (R-10).

| Solución de referencia | Marca / producto | Proveedor | Precio referencial | Verificación |
|---|---|---|---|---|
| Cámaras IP con grabación en NVR y retención de 30 días, cobertura de puerta, pasillos de racks y cuarto de Chiquimula | Axis Communications · Hikvision | Integrador de seguridad física local | **US$ 1,300 – 3,000** (8 cámaras + NVR, ambas sedes) | ○ Referencia de mercado |

### I-MonitoreoAmbiental — Sensores ambientales del centro de datos

> Remedia: `D-12`. Soporta: `C-12(c)`. Soporta escenario: `E-01`, `E-07`. Prioridad: **ALTA** (R-10).

| Solución de referencia | Marca / producto | Proveedor | Precio referencial | Verificación |
|---|---|---|---|---|
| Sensores de temperatura, humedad, fuga de agua y corte eléctrico con alertas automáticas | APC NetBotz · Vertiv Environet | Distribuidor autorizado APC/Vertiv | **US$ 1,500 – 3,500** (ambas sedes) | ○ Referencia de mercado |

### I-UPS — Energía de respaldo ampliada (UPS)

> Remedia: `D-13`. Soporta: `C-12(d)`. Soporta escenario: `E-01`, `E-07`. Prioridad: **ALTA** (R-09, P×I=12).

| Solución de referencia | Marca / producto | Proveedor | Precio referencial | Verificación |
|---|---|---|---|---|
| UPS dimensionado para al menos 60–90 minutos de autonomía de la carga crítica (hoy 15 minutos) | APC Smart-UPS / Symmetra | Distribuidor autorizado APC | **US$ 4,000 – 8,000** | ○ Referencia de mercado — el dimensionamiento exacto (kVA) requiere un estudio de carga crítica actual, pendiente de levantamiento en sitio |

### I-Planta — Planta eléctrica de respaldo con transferencia automática

> Remedia: `D-13`. Soporta: `C-12(d)`. Soporta escenario: `E-01`, `E-07`. Prioridad: **ALTA** (R-09).

| Solución de referencia | Marca / producto | Proveedor | Precio referencial | Verificación |
|---|---|---|---|---|
| Planta eléctrica diésel con ATS (transferencia automática) para eventos prolongados, dimensionada según la carga del centro de datos de Jutiapa | Marca según disponibilidad local (Cummins, Caterpillar, Perkins) | Proveedor de plantas eléctricas local | **US$ 15,000 – 35,000** (según capacidad, kVA a determinar) | ○ Referencia de mercado — cotizar con al menos dos proveedores locales; el enunciado exige valores realistas de mercado guatemalteco |

### I-Respaldo — Plataforma de respaldo bajo el modelo 3-2-1-1-0

> Remedia: `D-14`. Soporta: `C-08`, `C-09`, `C-10`. Soporta escenario: `E-01`, `E-05`, `E-06`, `E-07`. Prioridad: **ALTA** (R-05, P×I=15) — con dependencia directa del RTO/RPO del ERP definido en el DRP (Fase 3).

| Solución de referencia | Marca / producto | Proveedor | Precio referencial | Verificación |
|---|---|---|---|---|
| Reemplazo de la cinta local por copia en disco + copia replicada a la Planta de Chiquimula (o a la nube) + copia inmutable (*object lock*), cifrada, con pruebas de restauración calendarizadas | Veeam Backup & Replication + repositorio con bloqueo de objetos (Azure, AWS o nube local) · Veeam Cloud Connect | Distribuidor autorizado / proveedor de nube | **US$ 500 – 1,200** por socket/año (licenciamiento) + almacenamiento en la nube según volumen (típicamente US$ 0.01–0.02/GB/mes para almacenamiento con bloqueo de objeto) | ○ Referencia de mercado — Veeam no publica lista pública de precios (portal de ventas exige "Request Pricing"); cotizar con distribuidor autorizado |

**Ajuste derivado del DRP (2026-09-08):** la estrategia seleccionada es un sitio alterno tibio en
Chiquimula, complementado con una copia inmutable cifrada fuera del sitio o en nube. El
dimensionamiento inicial debe soportar los siguientes objetivos: ERP/BD, RTO 4 h y RPO 1 h;
portales, RTO 8 h y RPO 4 h; correo, RTO 4 h y RPO 4 h; rastreo de flotilla, RTO 4 h y RPO 1 h.
Para VPN y red, el objetivo es restaurar el servicio en 2 h y conservar la configuración con una
antigüedad máxima de 24 h y 4 h, respectivamente. Estos objetivos se verifican en las pruebas
semestrales del DRP y no convierten el rango referencial en una cotización definitiva.

## 3.6 Respaldo, monitoreo y gestión de incidentes

### I-SIEM — Centralización y correlación de eventos (SIEM)

> Remedia: `D-16`. Soporta: `C-29`. Soporta escenario: todos. Prioridad: **CRÍTICA** (R-04, P×I=20).

| Solución de referencia | Marca / producto | Proveedor | Precio referencial | Verificación |
|---|---|---|---|---|
| Correlación de eventos de firewall, WAF, EDR, NAC, WLAN, directorio, respaldo y sensores ambientales en una consola única | Wazuh (open source, autoalojado) · Microsoft Sentinel (SaaS, pago por consumo) · Splunk Enterprise | Implementación interna (open source) / licenciamiento cloud por consumo | **US$ 0** (Wazuh, solo infraestructura y horas de implementación) **– US$ 2 – 5/GB ingerido/mes** (Microsoft Sentinel) | ○ Referencia de mercado — recomendación: iniciar con Wazuh (menor OPEX, coherente con el presupuesto de una empresa de 480 colaboradores) y migrar a un SIEM comercial si el volumen de eventos lo justifica |

### I-Observabilidad — Monitoreo de disponibilidad e infraestructura

> Remedia: `D-16` (dimensión de visibilidad operativa). Soporta: `C-29`. Prioridad: **CRÍTICA** (R-04) — complementario al SIEM.

| Solución de referencia | Marca / producto | Proveedor | Precio referencial | Verificación |
|---|---|---|---|---|
| Monitoreo de disponibilidad, desempeño y capacidad de servidores, enlaces y switches con tableros y alertamiento proactivo | Zabbix + Grafana (open source) · PRTG Network Monitor · SolarWinds | Implementación interna / licenciamiento comercial | **US$ 0 – 1,500/año** (según licenciamiento elegido) | ○ Referencia de mercado |

### I-NDR — Detección y respuesta de red (complementario al SIEM)

> Remedia: `D-16` (visibilidad de red que evade el perímetro, en especial hacia/desde OT). Soporta: `C-29b`. Prioridad: **MEDIA** (complementario, ver Fase 2 §6.9 "especialmente en la red interna ya segmentada").

| Solución de referencia | Marca / producto | Proveedor | Precio referencial | Verificación |
|---|---|---|---|---|
| Análisis de tráfico de red para detectar patrones anómalos que evaden el firewall perimetral | Suricata + Zeek (open source) · Darktrace (comercial) | Implementación interna / distribuidor especializado | **US$ 0 (open source) – 20,000+/año** (Darktrace, referencial) | ○ Referencia de mercado — se recomienda diferir esta adquisición a la Fase de implementación 3 (§6), una vez madura la segmentación (I-Segmentación-VLAN) y el SIEM |

### I-GestiónVuln — Gestión de vulnerabilidades y pruebas de penetración

> Remedia: `D-16`, `D-10`. Soporta: `C-11`. Soporta escenario: `E-04`. Prioridad: **CRÍTICA** (R-04, R-01/R-03 por superficie de explotación sin parche).

| Solución de referencia | Marca / producto | Proveedor | Precio referencial | Verificación |
|---|---|---|---|---|
| Escaneo de vulnerabilidades autenticado (mensual, quincenal en la DMZ) + prueba de penetración anual de las tres aplicaciones publicadas | Tenable Nessus Professional · Qualys VMDR · prueba de penetración por firma local especializada | Licenciamiento directo + servicio profesional | **US$ 3,000 – 5,000/año** (escáner) + **US$ 4,000 – 10,000** (pentest anual de las 3 apps + nueva arquitectura de DMZ) | ○ Referencia de mercado |

### I-Concientización — Programa de concientización y simulacros de phishing

> Remedia: `D-15`. Soporta: `C-04`. Soporta escenario: `E-04`, `E-05`. Prioridad: **ALTA** (R-07).

| Solución de referencia | Marca / producto | Proveedor | Precio referencial | Verificación |
|---|---|---|---|---|
| Plataforma de capacitación y simulacros de phishing trimestrales para ~480 colaboradores | KnowBe4 · Proofpoint Security Awareness | Licenciamiento anual por usuario | **US$ 1.50 – 3.00/usuario/año** — para 480 colaboradores: **≈ US$ 720 – 1,440/año** | ○ Referencia de mercado |

### I-TalentoSOC — Estructura de talento humano de seguridad de la información

> Remedia: `D-16` (ausencia total de personal dedicado a seguridad). Soporta: `C-29`, `C-30`, §5 de la Fase 2. Soporta escenario: todos. Prioridad: **CRÍTICA** (R-04) — se desarrolla en detalle en el §4.

---

# 4. Equipo humano de respuesta a incidentes y ciberseguridad

La tecnología por sí sola no resuelve las brechas identificadas: TransAgro del Oriente, S.A. no cuenta hoy con **ningún** rol dedicado a seguridad de la información, monitoreo o respuesta a incidentes (Fase 1, Fase 2 §2.4.1). El rubro `I-TalentoSOC` traduce a presupuesto la estructura organizacional que la Fase 2 (§5.1) definió funcionalmente.

## 4.1 Estructura organizacional propuesta

```
                 Gerencia General
                        |
        Comité de Seguridad de la Información
   (Gerencia General + Gerencia de TI + asesor externo)
                        |
     Oficial / Responsable de Seguridad de la Información
        (interno a tiempo parcial, o vCISO por contrato)
              /                          \
   Administradores de              Analista SOC N1  +  Especialista en
   Sistemas y Redes (2,           Respuesta a Incidentes
   ya existentes)                  (internos, o servicio MDR/SOC tercerizado)
```

La decisión entre **contratación directa**, **servicio tercerizado (MDR/SOC como servicio)** o un **esquema mixto** queda a criterio de la Gerencia General según el flujo de caja disponible; ambos escenarios se presupuestan a continuación para que la Dirección compare.

## 4.2 Perfiles, certificaciones sugeridas y costo referencial

| Rol | Perfil / certificaciones sugeridas | Modalidad | Costo mensual referencial | Costo anual (OPEX) |
|---|---|---|---|---|
| Oficial de Seguridad de la Información | Ingeniero en Sistemas con formación en ISO/IEC 27001 (Lead Implementer/Auditor) o ISC2 CC/CISSP | Contratación directa (tiempo parcial o completo) o vCISO por retainer | **Q15,000 – Q22,000/mes** (interno) ≈ **US$ 1,970 – 2,890** · o **US$ 1,500 – 3,000/mes** (vCISO externo) | Interno: **≈ US$ 23,600 – 34,700/año** · vCISO: **US$ 18,000 – 36,000/año** |
| Analista SOC Nivel 1 | Técnico/Ingeniero con CompTIA Security+ o equivalente | Contratación directa o incluido en servicio de MDR tercerizado | **Q6,000 – Q9,000/mes** ≈ **US$ 790 – 1,180** | **≈ US$ 9,480 – 14,200/año** (interno) |
| Especialista en Respuesta a Incidentes | EC-Council CEH, GIAC GCIH o equivalente | Contratación directa o retainer de horas garantizadas con proveedor externo | **Q10,000 – Q15,000/mes** ≈ **US$ 1,310 – 1,970** (interno) · o **US$ 5,000 – 15,000/año** (retainer IR) | **≈ US$ 15,700 – 23,600/año** (interno) |
| **Alternativa: Servicio MDR/SOC como servicio (tercerizado)** | Monitoreo 24/7 de EDR, firewall y SIEM por proveedor especializado | Servicio contratado (OPEX puro, sin contratación de personal propio) | — | **US$ 18,000 – 48,000/año** (US$ 1,500 – 4,000/mes, según número de activos monitoreados) |

> Los valores en quetzales son referenciales y deben contrastarse con la escala salarial vigente para el sector TI en Guatemala al momento de ejecutar el presupuesto; el grupo puede optar por un esquema totalmente interno, totalmente tercerizado o híbrido, siempre que lo justifique.

## 4.3 Recomendación de esquema para el primer año

Dado que TransAgro no tiene madurez de seguridad instalada, se recomienda un **esquema mixto**: **Oficial de Seguridad de la Información interno a tiempo parcial** (para tener un dueño funcional del programa, alineado con el Comité de Seguridad) + **servicio MDR/SOC tercerizado** para el monitoreo 24/7 (más económico y más rápido de desplegar que reclutar y formar un SOC interno desde cero). La transición a un SOC interno completo se revalúa en el año 2, conforme madure el volumen de eventos gestionado por el SIEM (`I-SIEM`).

**Costo estimado del esquema recomendado (año 1):** Oficial de Seguridad interno tiempo parcial (≈ US$ 12,000 – 17,000/año, 50 % de dedicación) + MDR/SOC tercerizado (≈ US$ 18,000 – 30,000/año) ≈ **US$ 30,000 – 47,000/año**, sensiblemente menor que construir el equipo completo internamente en el primer año (≈ US$ 49,000 – 72,000/año).

---

# 5. Estimación de inversión consolidada (CAPEX / OPEX)

## 5.1 Tabla consolidada por dominio

| Dominio | Prioridad | Rubros incluidos (`I-xxx`) | CAPEX estimado (US$) | OPEX anual estimado (US$) | Responsable de gestión |
|---|---|---|---|---|---|
| Perímetro y aplicaciones (DMZ) | **CRÍTICA** | NGFW-HA, WAF, AntiDDoS, DNSSecurity, Segmentación-DMZ, GestiónSecretos, Honeypot (MEDIA) | 14,500 – 51,000 | 5,050 – 21,600 | Gerencia de TI / Administradores de redes |
| Comunicaciones entre sedes | **ALTA / CRÍTICA** (SegundoISP) | SD-WAN/VPN, SegundoISP | 1,200 – 4,500 | 6,000 – 30,000 | Gerencia de TI |
| Identidad, acceso y red interna | **CRÍTICA** | MFA, PAM, Segmentación-VLAN, NAC, WLAN, Inventario | 17,250 – 63,900 | 40,320 – 40,320 (MFA, fijo por usuario) + 0 – 15,000 (PAM/inventario) | Administradores de sistemas y redes |
| Endpoints y sistemas | **CRÍTICA** | EDR, RenovaciónSO, Parches, FiltradoCorreo | 5,000 – 20,000 (renovación SO, según servidores a migrar) | 27,000 – 45,000 (EDR) + 1,500 – 3,000 (parches) + 11,500 – 28,800 (filtrado correo) | Administradores de sistemas y redes |
| Seguridad física y datacenter | **ALTA** | ControlAccesoFísico, CCTV, MonitoreoAmbiental, UPS, Planta | 23,000 – 52,500 | — (mantenimiento anual estimado 8–10 % del CAPEX) | Gerencia de TI / Administración |
| Respaldo, monitoreo e incidentes | **CRÍTICA** | Respaldo, SIEM, Observabilidad, NDR (MEDIA), GestiónVuln, Concientización | 0 – 1,200 (licenciamiento perpetuo, si aplica) | 500 – 1,200/socket (respaldo) + 0 – 15,000 (SIEM) + 0 – 1,500 (observabilidad) + 0 – 20,000 (NDR, diferido) + 7,000 – 15,000 (gestión de vulnerabilidades y pentest) + 720 – 1,440 (concientización) | Oficial de Seguridad de la Información |
| Talento humano (CSIRT/SOC) | **CRÍTICA** | TalentoSOC | — | 30,000 – 72,000 (según esquema del §4.3) | Gerencia General / Gerencia de TI |
| **TOTAL CONSOLIDADO (año 1, orden de magnitud)** | | | **≈ US$ 61,000 – 193,000** | **≈ US$ 129,000 – 310,000** | |

> **Nota de lectura:** los rangos son amplios porque combinan escenarios de licenciamiento open source (extremo inferior) con soluciones comerciales de mayor cobertura (extremo superior); la Gerencia de TI debe cerrar cada rango con la cotización formal de al menos tres proveedores antes de comprometer presupuesto (§2.4). El extremo superior de OPEX asume que se contrata protección Anti-DDoS dedicada (AWS Shield Advanced, US$36,000/año) además del plan Cloudflare Business; si la protección Anti-DDoS incluida en Cloudflare Business resulta suficiente (caso base recomendado), el OPEX superior baja en esa misma magnitud. En quetzales, al tipo de cambio de referencia Q7.6222/US$1.00 (Banguat, 7 de septiembre de 2026), el total estimado del año 1 equivale aproximadamente a **Q1,449,000 – Q3,834,000** (CAPEX + OPEX combinados).

## 5.2 Comparación con el costo de no actuar

Los cinco riesgos críticos de la Fase 1 (R-01 a R-04, con P×I entre 20 y 25) representan, de materializarse, una interrupción de la facturación electrónica, la exposición de datos de clientes y proveedores, o un evento de ransomware sin capacidad de recuperación verificada. El presupuesto anual estimado de este Plan (extremo inferior, ≈ US$ 190,000/año combinando CAPEX y OPEX) equivale a una fracción del costo típico de un incidente de ransomware con indisponibilidad prolongada del ERP en una empresa del tamaño de TransAgro (pérdida de facturación diaria, costo de recuperación forense, posibles sanciones contractuales con clientes de exportación); este Plan no cuantifica ese costo evitado por no contar con una cifra propia de TransAgro, pero lo señala como el argumento central para la aprobación del presupuesto ante Dirección.

---

# 6. Propuesta de fases de implementación

La secuencia respeta el criterio de aceptación de riesgo de la Fase 2 (§3.4): **ningún riesgo CRÍTICO ni ALTO se acepta sin un plan de tratamiento con responsable y fecha.** Se implementa primero lo que remedia los riesgos CRÍTICO (R-01 a R-04), luego lo ALTO (R-05 a R-10), y al final lo complementario (MEDIA).

## Fase de implementación 1 (0–3 meses) — Riesgos CRÍTICO

| Rubro | Por qué es primero |
|---|---|
| `I-MFA` | Es la medida de menor costo relativo y mayor reducción de riesgo inmediata (R-03, R-06, R-07); no requiere rediseño de red. |
| `I-PAM` (cuentas nominadas, eliminación de cuentas compartidas) | Prerrequisito de auditabilidad para todo lo demás; costo bajo si se limita a la reconfiguración de Active Directory en esta fase. |
| `I-Inventario` | Prerrequisito técnico de NAC (fase 2) y de EDR. |
| `I-EDR` | Mayor cobertura de riesgo por dólar invertido frente a R-03 (propagación de malware/ransomware). |
| `I-WAF`, `I-AntiDDoS`, `I-DNSSecurity`, `I-Segmentación-DMZ`, `I-GestiónSecretos` | Remedian directamente R-01 (el riesgo más crítico, P×I=25); la exposición de la BD del ERP a través de la DMZ es la brecha de mayor impacto de negocio. |
| `I-NGFW-HA` | Elimina el punto único de falla del borde (R-02, P×I=20). |
| `I-SIEM`, `I-GestiónVuln` (escaneo, no pentest aún) | Sin visibilidad (R-04) no se puede verificar que el resto de controles funcione. |
| `I-TalentoSOC` (Oficial de Seguridad interino + inicio de contratación MDR) | Sin un responsable designado, ningún control anterior tiene dueño operativo. |

## Fase de implementación 2 (3–6 meses) — Riesgos ALTO

| Rubro | Justificación |
|---|---|
| `I-Segmentación-VLAN`, `I-NAC`, `I-WLAN` | Completan la segmentación de la red interna (R-03); requieren más tiempo por el riesgo de interrumpir la operación de planta durante el cambio (se implementan por fases, primero OT y cámaras). |
| `I-SD-WAN/VPN`, `I-SegundoISP` | Resuelven R-08 (VPN obsoleta) y refuerzan R-02; requieren coordinación con dos proveedores de Internet. |
| `I-ControlAccesoFísico`, `I-CCTV`, `I-MonitoreoAmbiental`, `I-UPS`, `I-Planta` | Resuelven R-09 y R-10; son obra física con tiempos de instalación más largos (plantas eléctricas en particular). |
| `I-Respaldo` | Migra el modelo 3-2-1-1-0; se coordina con la definición final de RTO/RPO del DRP (Fase 3) y con el sitio alterno. |
| `I-RenovaciónSO`, `I-Parches` | Migración de servidores críticos primero (ERP, DMZ), luego correo/archivos/directorio, luego estaciones — plan escalonado propio de C-16. |
| `I-FiltradoCorreo`, `I-Concientización` | Resuelven R-07 en su componente de correo/factor humano. |

## Fase de implementación 3 (6–12 meses) — Complementarios y madurez

| Rubro | Justificación |
|---|---|
| `I-Honeypot` | Complementario a la DMZ ya protegida; solo aporta valor una vez que WAF/Anti-DDoS/DNS están operando. |
| `I-NDR` | Requiere que la segmentación VLAN (fase 2) esté operando para tener tráfico inter-zona que analizar. |
| `I-GestiónVuln` (prueba de penetración anual completa) | Se ejecuta sobre la arquitectura ya rediseñada (I-Segmentación-DMZ), no sobre la anterior. |
| Evolución de `I-TalentoSOC` hacia SOC interno (si el volumen de eventos lo justifica) | Decisión basada en datos reales del primer año de operación del SIEM. |

---

# 7. Anexos

## Anexo A — Tabla de trazabilidad D-nn → R-nn → C-nn → E-nn → I-nn (cierre de la cadena)

| D-nn | Riesgo (Fase 1) | Control (Fase 2) | Escenario DRP (Fase 3) | **Inversión (Fase 4)** | Prioridad |
|---|---|---|---|---|---|
| D-01 | R-01 (CRÍTICO, 25) | C-19, C-20, C-21, C-14, C-07, C-11 | E-04 | I-WAF, I-AntiDDoS, I-DNSSecurity, I-Segmentación-DMZ, I-GestiónSecretos, I-Honeypot | CRÍTICA |
| D-02 | R-02 (CRÍTICO, 20) | C-13, C-17 | E-02 | I-NGFW-HA | CRÍTICA |
| D-03 | R-08 (ALTO, 12) | C-23, C-24 | E-03 | I-SD-WAN/VPN | ALTA |
| D-04 | R-02 (CRÍTICO, 20) | C-24, C-13 | E-08 | I-SegundoISP | CRÍTICA |
| D-05 | R-03 (CRÍTICO, 20), R-07 (ALTO, 16) | C-22, C-15 | E-04, E-05 | I-MFA, I-PAM | CRÍTICA |
| D-06 | R-03 (CRÍTICO, 20) | C-15, C-22, C-18 | E-04, E-05 | I-PAM, I-MFA | CRÍTICA |
| D-07 | R-03 (CRÍTICO, 20) | C-25, C-14 | E-05 | I-Segmentación-VLAN | CRÍTICA |
| D-08 | R-03 (CRÍTICO, 20) | C-27 | E-05 | I-WLAN | ALTA |
| D-09 | R-03 (CRÍTICO, 20) | C-26, C-01 | E-05 | I-NAC, I-Inventario | CRÍTICA |
| D-10 | R-03 (CRÍTICO, 20), R-05 (ALTO, 15) | C-16, C-02, C-17, C-11 | E-05 | I-RenovaciónSO, I-Parches, I-GestiónVuln | CRÍTICA |
| D-11 | R-03 (CRÍTICO, 20) | C-28, C-01, C-02 | E-04, E-05 | I-EDR, I-Inventario | CRÍTICA |
| D-12 | R-10 (ALTO, 12) | C-12(a)(b)(c) | E-01, E-07 | I-ControlAccesoFísico, I-CCTV, I-MonitoreoAmbiental | ALTA |
| D-13 | R-09 (ALTO, 12) | C-12(d), C-13.3 | E-01, E-07 | I-UPS, I-Planta | ALTA |
| D-14 | R-05 (ALTO, 15) | C-08, C-09, C-10 | E-01, E-05, E-06, E-07 | I-Respaldo | ALTA |
| D-15 | R-07 (ALTO, 16) | C-21b, C-21c, C-04 | E-04, E-05 | I-FiltradoCorreo, I-Concientización | ALTA |
| D-16 | R-04 (CRÍTICO, 20) | C-29, C-30, C-11 | Todos | I-SIEM, I-Observabilidad, I-NDR, I-GestiónVuln, I-TalentoSOC | CRÍTICA |
| D-17 | R-06 (ALTO, 16) | C-05, C-06, C-18, C-22 | E-04 | I-PAM, I-GestiónSecretos | CRÍTICA |

**Resultado de la verificación:** **17 de 17 debilidades (100 %)** cuentan con al menos un rubro de inversión asignado, cerrando la cadena `D-nn → R-nn → C-nn → E-nn → I-nn` iniciada en la Fase 1 y exigida por el enunciado §1.4. Los **31 rubros `I-xxx`** del §3 cubren la totalidad de las 17 debilidades; ninguno queda huérfano de debilidad, y ninguna debilidad queda sin rubro.

## Anexo B — Evidencia de verificación independiente de precios

Cumplimiento del requisito obligatorio del enunciado §7.1 ("validar y actualizar al menos tres de estas referencias mediante cotización o investigación directa con un proveedor o distribuidor autorizado en Guatemala o la región, citando la fuente"). Se presentan **cinco** verificaciones, todas contra la lista de precios pública y vigente del propio fabricante/proveedor cloud (tipo de evidencia: enlace oficial), consultadas el **8 de septiembre de 2026**:

| # | Rubro | Producto verificado | Precio verificado | Fuente (enlace) | Fecha de consulta |
|---|---|---|---|---|---|
| 1 | I-MFA | Microsoft Entra ID P1 / P2 | US$ 7.00 / US$ 10.00 por usuario/mes (facturación anual) | https://www.microsoft.com/en-us/security/business/microsoft-entra-pricing | 8 de septiembre de 2026 |
| 2 | I-WAF | Cloudflare Business (incluye WAF) | US$ 200/mes (anual) o US$ 250/mes (mensual) | https://www.cloudflare.com/plans/ | 8 de septiembre de 2026 |
| 3 | I-AntiDDoS | AWS Shield Advanced | US$ 3,000/mes (suscripción, compromiso 1 año) + tarifas de transferencia desde US$ 0.025/GB | https://aws.amazon.com/shield/pricing/ | 8 de septiembre de 2026 |
| 4 | I-EDR | CrowdStrike Falcon Go / Falcon Pro | US$ 7.99 / US$ 14.99 por dispositivo/mes (facturación mensual) | https://www.crowdstrike.com/en-us/pricing/ | 8 de septiembre de 2026 |
| 5 | I-EDR (referencia complementaria) | Microsoft Defender (suite incluida en Microsoft 365 E5 Security) | US$ 12.00 por usuario/mes (facturación anual, bundle) | https://www.microsoft.com/en-us/microsoft-365/security/endpoint-defender | 8 de septiembre de 2026 |

**Tipo de cambio de referencia utilizado en este documento:**

| Dato | Valor verificado | Fuente | Fecha |
|---|---|---|---|
| Tipo de cambio de referencia USD/GTQ | Q 7.6222 por US$ 1.00 | Banco de Guatemala, *Tipo de Cambio de Referencia* | 7 de septiembre de 2026 |

**Pendiente para el cierre de la Fase 4** (a completar por el grupo antes de la defensa oral, conforme al enunciado §7.5): al menos una cotización adicional de **hardware** (firewall NGFW, UPS o planta eléctrica) con un distribuidor autorizado en Guatemala, dado que estos rubros —a diferencia de las suscripciones cloud verificadas arriba— no publican lista de precios pública y requieren contacto directo (captura de pantalla, enlace o constancia de contacto, conforme al formato de evidencia aceptado por el enunciado).

## Anexo C — Glosario de términos específicos de la Fase 4

| Término | Definición |
|---|---|
| **CAPEX** | *Capital Expenditure* — gasto de capital: inversión inicial en activos (equipo, licencias perpetuas, obra) que se deprecia en el tiempo. |
| **OPEX** | *Operating Expenditure* — gasto operativo recurrente: suscripciones, soporte anual, personal. |
| **TCO** | *Total Cost of Ownership* — costo total de propiedad de una solución a lo largo de su vida útil (CAPEX + OPEX acumulado). |
| **SLA** | *Service Level Agreement* — acuerdo de nivel de servicio; define la disponibilidad y los tiempos de respuesta comprometidos por un proveedor. |
| **vCISO** | *Virtual Chief Information Security Officer* — Oficial de Seguridad de la Información contratado como servicio externo (retainer), en lugar de un puesto interno de tiempo completo. |
| **MDR** | *Managed Detection and Response* — servicio tercerizado de monitoreo y respuesta ante amenazas, equivalente a un SOC como servicio. |
| **Referencia de mercado vs. verificado** | En este documento, "✔ VERIFICADO" indica un precio confirmado contra la lista de precios pública vigente del propio fabricante o proveedor, citada en el Anexo B; "○ Referencia de mercado" indica un rango indicativo pendiente de cotización formal con un distribuidor. |

> Los términos técnicos generales (WAF, DMZ, EDR, SIEM, NAC, RTO, RPO, DRP, BCP, CSIRT/SOC) ya están definidos en el Anexo F de la Fase 2 — Plan de Seguridad Informática y no se repiten aquí.

## Anexo D — Referencias

Amazon Web Services. (2026). *AWS Shield pricing*. https://aws.amazon.com/shield/pricing/

Banco de Guatemala. (2026, 7 de septiembre). *Tipo de cambio de referencia*. https://www.banguat.gob.gt/cambio/tctemp.asp

Center for Internet Security. (2024). *CIS Critical Security Controls version 8.1*. https://www.cisecurity.org/controls/v8-1

Cloudflare, Inc. (2026). *Plans*. https://www.cloudflare.com/plans/

CrowdStrike Holdings, Inc. (2026). *Falcon pricing*. https://www.crowdstrike.com/en-us/pricing/

Microsoft. (2023). *Windows Server 2012 and 2012 R2 reaching end of support*. Microsoft Lifecycle. https://learn.microsoft.com/en-us/lifecycle/announcements/windows-server-2012-r2-end-of-support

Microsoft. (2026). *Microsoft Entra pricing*. https://www.microsoft.com/en-us/security/business/microsoft-entra-pricing

Microsoft. (2026). *Microsoft Defender for Endpoint*. https://www.microsoft.com/en-us/microsoft-365/security/endpoint-defender

National Institute of Standards and Technology. (2024). *The NIST Cybersecurity Framework (CSF) 2.0* (NIST CSWP 29). U.S. Department of Commerce. https://doi.org/10.6028/NIST.CSWP.29

Veeam Software. (2026). *Pricing*. https://www.veeam.com/pricing.html

> Nota: las referencias normativas ya citadas de forma completa en la Fase 2 (ISO/IEC 27001:2022, RFC 9395, NIST SP 800-131A Rev. 2, retiro de SHA-1, OWASP Top 10:2025) no se repiten en este Anexo; se listan aquí únicamente las fuentes nuevas consultadas para la Fase 4.

---

# 8. Entregable de la Fase 4 y cierre

## 8.1 Verificación de cumplimiento del entregable (enunciado §7.5)

| Requisito exigido | Estado en este documento |
|---|---|
| Documento con las tablas de las secciones equivalentes a §7.2, §7.3 y §7.4 completas, actualizadas y con fuentes citadas | ✅ Completo (§3, §4, §5) |
| Al menos tres cotizaciones o referencias de precio verificadas de forma independiente | ✅ Cinco verificadas (Anexo B) — pendiente de complementar con una cotización de hardware local antes de la defensa oral |
| Propuesta de fases de implementación (qué se adquiere primero y por qué, según nivel de riesgo) | ✅ Completo (§6) |
| Componente de talento humano (contratación directa, MDR/SOC o esquema mixto) | ✅ Completo (§4), con recomendación de esquema para el año 1 |
| Tabla resumen consolidada por dominio: Dominio \| Prioridad \| CAPEX \| OPEX anual \| Responsable | ✅ Completo (§5.1) |
| Trazabilidad completa de las 17 debilidades hasta un rubro de inversión | ✅ 17 de 17 (100 %), Anexo A |

## 8.2 Pendientes antes de la integración final (Fase "Integración y defensa")

1. Obtener y anexar al menos una constancia de cotización de hardware local (NGFW, UPS o planta eléctrica) con un distribuidor guatemalteco, conforme al Anexo B.
2. Consolidar este documento con las Fases 1, 2 y 3 en el documento único (portada institucional, índice y numeración de página conforme al enunciado §8.1).
3. **Completado en borrador:** el DRP define sitio tibio en Chiquimula, copia inmutable externa y objetivos RTO/RPO que dimensionan `I-Respaldo`; queda pendiente cerrar la cotización formal y validar el levantamiento técnico del sitio.
4. Preparar la defensa de cada rubro de inversión: cada integrante debe poder justificar el porqué de la marca, la arquitectura y el costo de los rubros bajo su responsabilidad, conforme a la exigencia de la defensa oral (§8.2 del enunciado).

## Cierre

Este Plan de Adquisición e Implementación traduce los 30 controles de la Fase 2 en **31 rubros de inversión** organizados en seis bloques (perímetro/DMZ, comunicaciones, identidad/red interna, endpoints, físico/datacenter, respaldo-monitoreo-incidentes), presupuestados y priorizados según la matriz de riesgos de la Fase 1, con **cinco precios verificados de forma independiente** contra fuente oficial vigente y con la cadena de trazabilidad `D-nn → R-nn → C-nn → E-nn → I-nn` **cerrada al 100 %** para las 17 debilidades del caso. El presupuesto consolidado (orden de magnitud US$ 61,000–193,000 de CAPEX y US$ 129,000–293,000 de OPEX anual) y la secuencia de implementación en tres fases quedan listos para su discusión y aprobación por la Gerencia General de TransAgro del Oriente, S.A.

**Documento vivo.** Los precios marcados como "○ Referencia de mercado" deben cerrarse con cotización formal de al menos un distribuidor autorizado en Guatemala antes de la ejecución del presupuesto, conforme al §2.4 de este documento.
