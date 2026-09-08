---
**Universidad Mariano Gálvez de Guatemala** — Facultad de Ingeniería en Sistemas de Información
**Campus:** Jutiapa · **Curso:** Telecomunicaciones (Área de Especialidad) · **Unidad integradora:** Seguridad de Redes
**Docente:** Ing. Juan Daniel Ramos Martínez · **Ciclo:** Segundo Semestre 2026
**Proyecto No. 01 — Fase 1: Diagnóstico de riesgos tecnológicos**
**Caso de estudio:** TransAgro del Oriente, S.A.
**Integrantes:** _(completar)_ · **Fecha de entrega:** _(completar)_
---

# Fase 1: Diagnóstico de riesgos tecnológicos

## Caso de Estudio: TransAgro del Oriente, S.A.

---

## 1. Checklist de Seguridad Informática Adaptado

Con el propósito de fortalecer la postura de ciberseguridad de la organización, se presenta el
instrumento de auditoría que fue diseñado y adaptado tomando como referencia los controles
**CIS Critical Security Controls v8.1** (Center for Internet Security, 2024) y los dominios del
Anexo A de la norma **ISO/IEC 27001:2022** (Organización Internacional de Normalización, 2022),
enfocándose específicamente en las debilidades tecnológicas de la infraestructura actual de
TransAgro del Oriente, S.A. Se tomó además como base el modelo de referencia entregado por el
curso ("Check List — Seguridad Informática y Sistemas"), ampliándolo para cubrir los dominios
propios de este caso.

El checklist cubre los **9 dominios mínimos** exigidos por la guía del proyecto (§4.2), con un
total de **36 aspectos de verificación** alineados a las 17 debilidades descritas en el caso de
estudio (§2.4). Para efectos de trazabilidad entre fases, cada pregunta declara la
**debilidad del caso (D-nn)** que ayuda a diagnosticar.

### 1.1 Nivel de aplicación adoptado (CIS Controls v8.1)

Las salvaguardas de CIS Controls v8.1 se organizan en tres **Grupos de Implementación** (IG1,
IG2, IG3). Para TransAgro del Oriente, S.A. se adopta el **Grupo de Implementación 2 (IG2)**
como nivel objetivo de la auditoría, por las siguientes razones:

- La organización tiene **~480 colaboradores** y dos sedes, un tamaño que supera el alcance de
  IG1 ("higiene cibernética esencial", pensado para organizaciones pequeñas con TI limitada).
- Custodia **datos de terceros**: información de clientes mayoristas, facturación de proveedores
  agrícolas y datos de ubicación GPS de la flotilla tercerizados a un SaaS externo.
- Opera **tecnología de operación (OT)**: controladores lógicos programables (PLC) y cámaras IP
  en la planta de Chiquimula, cuyo compromiso tiene impacto físico y de continuidad.
- No requiere el nivel IG3 (defensa frente a adversarios especializados con capacidad de
  ataque dirigido y persistente), que excede el perfil de riesgo de una agroindustria regional.

La justificación de este nivel se sostiene en la guía de grupos de implementación de CIS
(Center for Internet Security, 2024).

### 1.2 Supuestos adoptados

El caso de estudio no detalla todos los aspectos que evalúa el checklist. Cuando fue necesario,
se adoptaron los siguientes supuestos razonables:

| ID | Supuesto | Justificación |
|---|---|---|
| S-01 | Nivel de aplicación del checklist: **CIS Controls v8.1, Grupo de Implementación 2 (IG2)**. | Ver §1.1. |
| S-02 | Umbral de referencia para la retención de grabación de CCTV del centro de datos: **30 días** (ítem 6.2). | Práctica habitual para investigación de incidentes físicos; se usa solo como criterio de la pregunta, no como hallazgo. |
| S-03 | Configuración criptográfica destino de la VPN entre sedes: **IKEv2 + AES-256-GCM + SHA-2**, grupo Diffie-Hellman 19/20 y Perfect Forward Secrecy habilitado (control de R-08). | Derivada de RFC 9395, del retiro de SHA-1 (NIST, 2022) y de NIST SP 800-131A Rev. 2; el caso no especifica el grupo DH ni el PFS actuales. |
| S-04 | Criterio de tratamiento por nivel de riesgo (§2.3): CRÍTICO = acción inmediata con escalamiento a Gerencia General; ALTO ≤ 3 meses; MEDIO ≤ 12 meses; BAJO = aceptar y monitorear. | El enunciado exige clasificar en Bajo/Medio/Alto/Crítico pero no fija los plazos de tratamiento. |

### 1.3 Escala de las columnas de respuesta

| Valor | Significado |
|---|---|
| **SÍ** | El control existe y opera de forma efectiva. |
| **NO** | El control no existe, o existe de forma tan deficiente que no cumple su objetivo. |
| **N-A** | El control no aplica al alcance tecnológico actual de TransAgro. |

Las observaciones documentan el hallazgo concreto que sustenta cada respuesta.

---

### Dominio 1: Seguridad Perimetral y DMZ

| # | Pregunta de verificación | D-nn | Ref. (CIS v8.1 / ISO 27001:2022) | SÍ / NO / N-A | Observaciones del hallazgo |
|---|---|---|---|---|---|
| **1.1** | ¿Existe una separación física o lógica de zona desmilitarizada (DMZ) respecto a Internet y a la red interna? | D-01 | CIS 12.2 / A.8.22 | **SÍ** | El firewall perimetral sí implementa tres zonas (Internet / DMZ / red interna); la deficiencia está en la ausencia de controles adicionales, no en la existencia de la DMZ. |
| **1.2** | ¿Existe un Web Application Firewall (WAF) protegiendo las aplicaciones web publicadas? | D-01 | CIS 13.10 / A.8.26 | **NO** | El Portal de Clientes, el Portal de Proveedores y el Sistema de Rastreo de Flotilla operan en la DMZ sin filtrado en capa de aplicación. |
| **1.3** | ¿Se cuenta con protección Anti-DDoS (volumétrica y de capa de aplicación) en el perímetro? | D-01 | CIS 13.10 / A.8.20 | **NO** | No existe mitigación de denegación de servicio; un ataque volumétrico contra un solo enlace ISP dejaría sin servicio a ambas sedes. |
| **1.4** | ¿Existe filtrado DNS (DNS Firewall) que bloquee dominios maliciosos y de phishing? | D-01 | CIS 9.2 / A.8.20 | **NO** | La resolución DNS no cuenta con protección; usuarios e infraestructura pueden consultar dominios maliciosos sin restricción. |
| **1.5** | ¿La DMZ está segmentada respecto a la red interna con reglas de firewall estrictas y sin acceso directo a bases de datos internas? | D-01 | CIS 12.2 / A.8.22 | **NO** | Las tres aplicaciones comparten el mismo segmento de DMZ y el mismo servidor de base de datos backend; el Portal de Clientes tiene conexión directa a la BD del ERP interno, sin capa de servicios intermedia. |
| **1.6** | ¿Existe una solución de engaño (Honeypot / Deception) para detección temprana de intrusos en el perímetro? | D-01 | CIS 13.11 / A.8.16 | **NO** | No hay ningún mecanismo de detección temprana ni señuelos en la DMZ ni en la red interna. |
| **1.7** | ¿El firewall perimetral opera bajo una arquitectura de Alta Disponibilidad (clúster HA)? | D-02 | CIS 12.2 / A.8.14 | **NO** | Se identificó un equipo único, que representa un solo punto de falla (SPOF) para todo el tráfico de la Casa Matriz. |

---

### Dominio 2: Comunicaciones

| # | Pregunta de verificación | D-nn | Ref. (CIS v8.1 / ISO 27001:2022) | SÍ / NO / N-A | Observaciones del hallazgo |
|---|---|---|---|---|---|
| **2.1** | ¿Existe un túnel VPN sitio a sitio cifrado entre las dos sedes? | D-03 | CIS 3.10 / A.8.24 | **SÍ** | Existe una VPN IPsec sitio a sitio Jutiapa↔Chiquimula sobre Internet público; el hallazgo es sobre su vigencia criptográfica, no sobre su existencia. |
| **2.2** | ¿El túnel VPN sitio a sitio utiliza protocolos y algoritmos vigentes (IKEv2, AES-256, SHA-2)? | D-03 | CIS 3.10 / A.8.24 | **NO** | La VPN utiliza IKEv1, 3DES y SHA-1. IKEv1 fue formalmente deprecado por el IETF (RFC 9395, 2023); SHA-1 fue retirado por NIST (2022) y 3DES está en calendario de retiro (NIST SP 800-131A Rev. 2). |
| **2.3** | ¿La conectividad a Internet cuenta con enlaces redundantes de proveedores distintos y balanceo o failover? | D-04 | CIS 12.2 / A.8.14 | **NO** | Existe un único proveedor (ISP) para toda la conectividad de ambas sedes, sin acuerdos de nivel de servicio (SLA) documentados. |
| **2.4** | ¿Existe un enlace de respaldo o solución SD-WAN para la comunicación entre sedes ante caída del túnel principal? | D-03 | CIS 12.2 / A.5.29 | **NO** | El túnel VPN es el único camino entre sedes; su caída aísla por completo a la planta de Chiquimula del ERP y los servicios centrales. |

---

### Dominio 3: Identidad y Control de Acceso

| # | Pregunta de verificación | D-nn | Ref. (CIS v8.1 / ISO 27001:2022) | SÍ / NO / N-A | Observaciones del hallazgo |
|---|---|---|---|---|---|
| **3.1** | ¿Se implementa Autenticación Multifactor (MFA/2FA) para accesos críticos (VPN, correo, dominio interno, consolas de administración)? | D-05 | CIS 6.3, 6.4, 6.5 / A.8.5 | **NO** | No hay MFA para VPN, correo corporativo, dominio interno ni consolas de administración de servidores. |
| **3.2** | ¿Existe una política formal de contraseñas con requisitos de complejidad y expiración periódica? | D-06 | CIS 5.2 / A.5.17 | **NO** | No hay política de complejidad ni rotación de contraseñas. |
| **3.3** | ¿Las cuentas administrativas son individuales, nominadas y con principio de mínimo privilegio? | D-06 | CIS 5.4, 6.8 / A.8.2 | **NO** | Las cuentas administrativas son compartidas entre el personal de TI; no es posible auditar quién realizó una acción administrativa específica. |
| **3.4** | ¿Se realiza revisión periódica documentada de accesos y privilegios de usuarios, con baja oportuna de cuentas? | D-06 | CIS 5.1, 5.3, 6.2 / A.5.18 | **NO** | No existe un proceso documentado de recertificación de accesos ni de baja oportuna de cuentas de personal que causa baja. |

---

### Dominio 4: Red Interna

| # | Pregunta de verificación | D-nn | Ref. (CIS v8.1 / ISO 27001:2022) | SÍ / NO / N-A | Observaciones del hallazgo |
|---|---|---|---|---|---|
| **4.1** | ¿La red interna está segmentada de forma lógica (VLAN) aislando servidores, usuarios y dispositivos críticos, con ACL entre segmentos? | D-07 | CIS 12.2, 12.4 / A.8.22 | **NO** | Es una red plana (subred /16) donde convergen estaciones de trabajo, servidores (ERP, correo, archivos), impresoras, cámaras IP y controladores industriales (PLC), sin ACL entre ellos. |
| **4.2** | ¿Existe una solución NAC (Network Access Control) que valide el cumplimiento del dispositivo antes de otorgar acceso a la red? | D-09 | CIS 13.9 / A.8.20 | **NO** | Cualquier dispositivo conectado físicamente a un punto de red obtiene automáticamente una dirección IP y acceso a los recursos internos. |
| **4.3** | ¿La red inalámbrica corporativa cuenta con SSID segregado para invitados, portal cautivo y autenticación empresarial (WPA2/WPA3-Enterprise, 802.1X)? | D-08 | CIS 12.6, 15.4 / A.8.20 | **NO** | Existe una sola clave WPA2-Personal compartida por todo el personal y los visitantes; no hay red de invitados aislada ni portal cautivo. |
| **4.4** | ¿Los dispositivos IoT/OT (cámaras IP, PLC de planta) están aislados en segmentos de red dedicados con reglas de comunicación explícitas? | D-07 | CIS 12.1, 12.4 / A.8.22 | **NO** | Los controladores industriales y las cámaras comparten la misma subred que las estaciones de trabajo de los usuarios. |

---

### Dominio 5: Endpoints y Sistemas

| # | Pregunta de verificación | D-nn | Ref. (CIS v8.1 / ISO 27001:2022) | SÍ / NO / N-A | Observaciones del hallazgo |
|---|---|---|---|---|---|
| **5.1** | ¿Los sistemas operativos de servidores y estaciones mantienen soporte vigente del fabricante? | D-10 | CIS 2.2 / A.8.19 | **NO** | Se operan servidores con Windows Server 2012 R2 (fin de soporte extendido: 10 de octubre de 2023) y estaciones con Windows 7 (14 de enero de 2020) y 8.1 (10 de enero de 2023), sin soporte del fabricante. |
| **5.2** | ¿Existe gestión centralizada de parches para sistemas operativos y aplicaciones? | D-10 | CIS 7.3, 7.4 / A.8.8 | **NO** | No hay WSUS ni gestor de actualizaciones; los parches se aplican de forma manual e inconsistente. |
| **5.3** | ¿Se cuenta con una solución EDR (detección y respuesta en endpoint) en servidores y estaciones? | D-11 | CIS 10.1, 10.7 / A.8.7 | **NO** | Solo existe antivirus tradicional basado en firmas, desactualizado en varias estaciones; no hay EDR. |
| **5.4** | ¿Existe un inventario confiable y centralizado de activos de hardware y software? | D-11 | CIS 1.1, 2.1 / A.5.9 | **NO** | No hay inventario centralizado ni confiable de activos; no es posible determinar con certeza qué equipos están conectados a la red. |
| **5.5** | ¿Los discos de estaciones de trabajo y servidores cuentan con cifrado (BitLocker / equivalente)? | D-10 | CIS 3.6 / A.8.24 | **NO** | No se ha implementado cifrado de disco en los endpoints; la información queda expuesta ante robo o extravío físico del equipo. |

---

### Dominio 6: Datacenter y Seguridad Física

| # | Pregunta de verificación | D-nn | Ref. (CIS v8.1 / ISO 27001:2022) | SÍ / NO / N-A | Observaciones del hallazgo |
|---|---|---|---|---|---|
| **6.1** | ¿El centro de datos cuenta con control de acceso biométrico o por tarjeta, con bitácora de ingresos? | D-12 | CIS 1.1 / A.7.2, A.7.3 | **NO** | Solo existe una llave física compartida; no hay registro de quién ingresa ni cuándo. |
| **6.2** | ¿Existe videovigilancia (CCTV) del centro de datos con cobertura completa y retención mínima de 30 días? | D-12 | — / A.7.4 | **NO** | La cobertura de CCTV es parcial y no se cuenta con un sistema de grabación con retención adecuada. |
| **6.3** | ¿Se cuenta con monitoreo ambiental (temperatura, humedad, fuga de agua) con alertas automáticas? | D-12 | — / A.7.8 | **NO** | No existen sensores ambientales ni alertas automáticas al personal de TI. |
| **6.4** | ¿La UPS tiene autonomía suficiente para un apagado ordenado y existe planta eléctrica de respaldo? | D-13 | — / A.7.11 | **NO** | El respaldo energético (UPS) es de solo 15 minutos; no existe planta eléctrica de respaldo. |

---

### Dominio 7: Datos y Continuidad

| # | Pregunta de verificación | D-nn | Ref. (CIS v8.1 / ISO 27001:2022) | SÍ / NO / N-A | Observaciones del hallazgo |
|---|---|---|---|---|---|
| **7.1** | ¿Se ejecutan respaldos periódicos de los sistemas y datos críticos? | D-14 | CIS 11.2 / A.8.13 | **SÍ** | Sí se realizan respaldos en cinta local; el hallazgo es sobre su resguardo, verificación y modelo, no sobre su ejecución. |
| **7.2** | ¿El almacenamiento de copias de seguridad cumple el principio fuera de sitio (offsite) y el modelo 3-2-1? | D-14 | CIS 11.4 / A.8.13 | **NO** | Los respaldos se realizan en cinta local y se resguardan dentro del mismo cuarto de servidores que aloja la producción; no hay copia externa. |
| **7.3** | ¿Se realizan pruebas periódicas y documentadas de restauración de respaldos? | D-14 | CIS 11.5 / A.8.13 | **NO** | No existe un calendario documentado de pruebas de restauración ni validación de integridad de las copias. |
| **7.4** | ¿Los respaldos cuentan con cifrado, copia inmutable contra ransomware y política de retención documentada? | D-14 | CIS 11.3 / A.8.13, A.8.24 | **NO** | No hay política formal de retención, ni cifrado de respaldos, ni copia inmutable. |

---

### Dominio 8: Monitoreo y Respuesta a Incidentes

| # | Pregunta de verificación | D-nn | Ref. (CIS v8.1 / ISO 27001:2022) | SÍ / NO / N-A | Observaciones del hallazgo |
|---|---|---|---|---|---|
| **8.1** | ¿Existe centralización y correlación de logs (SIEM) de los sistemas y dispositivos de seguridad? | D-16 | CIS 8.9, 8.11 / A.8.15, A.8.16 | **NO** | No se cuenta con SIEM; los eventos de seguridad no se recolectan ni se correlacionan de forma centralizada. |
| **8.2** | ¿Se realizan escaneos periódicos de vulnerabilidades y pruebas de penetración? | D-16 | CIS 7.1, 7.5, 7.6 / A.8.8 | **NO** | No existe gestión de vulnerabilidades ni pruebas de penetración programadas. |
| **8.3** | ¿Existe un plan formal y documentado de respuesta a incidentes de seguridad? | D-16 | CIS 17.4 / A.5.24, A.5.26 | **NO** | No hay un plan de respuesta a incidentes; la reacción ante un evento sería improvisada. |
| **8.4** | ¿Existe un responsable o equipo designado (CSIRT/SOC, interno o tercerizado) para detección y respuesta? | D-16 | CIS 17.1 / A.5.24 | **NO** | No hay personal dedicado a seguridad; estas funciones recaen de manera informal en los administradores de sistemas. |

---

### Dominio 9: Personal y Proveedores

| # | Pregunta de verificación | D-nn | Ref. (CIS v8.1 / ISO 27001:2022) | SÍ / NO / N-A | Observaciones del hallazgo |
|---|---|---|---|---|---|
| **9.1** | ¿Existe un programa formal y documentado de concientización en ciberseguridad para todo el personal? | D-15 | CIS 14.1, 14.2 / A.6.3 | **NO** | No hay programa de capacitación ni concientización; el usuario es el eslabón más expuesto ante phishing. |
| **9.2** | ¿El dominio de correo corporativo cuenta con registros SPF, DKIM y DMARC configurados? | D-15 | CIS 9.5 / A.8.24 | **NO** | El dominio de correo no publica SPF, DKIM ni DMARC, lo que facilita la suplantación del dominio de la empresa. |
| **9.3** | ¿Los accesos remotos de proveedores externos son temporales y se revocan al finalizar la actividad? | D-17 | CIS 6.1, 6.2 / A.5.19 | **NO** | Los proveedores externos cuentan con accesos remotos permanentes, sin cuentas temporales ni revocación. |
| **9.4** | ¿Cada proveedor cuenta con credenciales individuales y nominadas, con rotación periódica? | D-17 | CIS 5.2, 6.1 / A.5.19 | **NO** | Se utilizan credenciales compartidas y no rotadas (el consultor del ERP mantiene credenciales sin rotar desde su asignación inicial). |
| **9.5** | ¿Se monitorean y registran las sesiones de acceso remoto de terceros? | D-17 | CIS 8.5, 13.5 / A.5.20 | **NO** | No existe monitoreo ni registro de las sesiones de acceso de proveedores externos. |
| **9.6** | ¿Los contratos con proveedores incluyen cláusulas de seguridad de la información, SLA y acuerdos de confidencialidad (NDA)? | D-17 | CIS 15.4 / A.5.20, A.5.21 | **NO** | No se han identificado cláusulas contractuales de seguridad ni acuerdos de confidencialidad vigentes; el integrador que instaló firewall y VPN tiene contrato de soporte no vigente y el ISP no tiene SLA documentado. |

---

## 2. Matriz de Riesgos Tecnológicos

Los riesgos detectados se priorizaron con una escala cualitativa que evalúa la
**probabilidad de ocurrencia (1-5)** y el **impacto potencial (1-5)** sobre la
confidencialidad, integridad y disponibilidad de la información de la empresa. Cada riesgo
declara su trazabilidad hacia las debilidades del caso (D-nn), el ítem del checklist que lo
origina y el control propuesto para la Fase 2.

### 2.1 Escala de probabilidad

| Valor | Nivel | Criterio |
|---|---|---|
| **1** | Muy baja | Evento improbable; requiere una combinación excepcional de condiciones. Sin antecedentes en el sector. |
| **2** | Baja | Podría ocurrir en algún momento, pero no se esperaría en el horizonte de un año. |
| **3** | Media | Es plausible que ocurra dentro de los próximos 12 meses. |
| **4** | Alta | Es esperable que ocurra en los próximos 12 meses dado el estado actual de los controles. |
| **5** | Muy alta | Ya está ocurriendo, o su ocurrencia en el corto plazo es casi segura por la ausencia total de controles. |

### 2.2 Escala de impacto

| Valor | Nivel | Criterio |
|---|---|---|
| **1** | Insignificante | Afectación mínima; sin interrupción del servicio ni pérdida de datos. |
| **2** | Menor | Interrupción breve de un servicio no crítico; sin impacto en clientes ni cumplimiento. |
| **3** | Moderado | Interrupción de un servicio relevante por horas, o exposición limitada de datos internos. |
| **4** | Mayor | Interrupción de operaciones críticas por uno o varios días, o fuga de datos de terceros; impacto reputacional y contractual. |
| **5** | Catastrófico | Paralización de la operación, pérdida irrecuperable de datos o compromiso total del ERP; impacto económico y legal grave, riesgo de continuidad del negocio. |

### 2.3 Regla de conversión Probabilidad × Impacto → Nivel de riesgo

| Nivel | Rango P×I | Criterio de tratamiento |
|---|---|---|
| **CRÍTICO** | 20 – 25 | Mitigación inmediata; escalamiento a Gerencia General. |
| **ALTO** | 12 – 19 | Mitigación planificada en el corto plazo (≤ 3 meses). |
| **MEDIO** | 6 – 11 | Mitigación programada (≤ 12 meses). |
| **BAJO** | 1 – 5 | Aceptar y monitorear. |

### 2.4 Matriz

| R-nn | Riesgo identificado | Debilidades (D-nn) | Ítem(s) del checklist | Activo / proceso afectado | Prob. | Impacto | Nivel | Control propuesto (Fase 2) |
|---|---|---|---|---|---|---|---|---|
| **R-01** | Compromiso de la base de datos interna por explotación de las aplicaciones web de la DMZ | D-01 | 1.2, 1.3, 1.5, 1.6 | Portales web, BD del ERP, red interna | 5 | 5 | **CRÍTICO** (25) | C: WAF gestionado, capa de servicios intermedia entre portales y BD, segmentación estricta de la DMZ, hardening de aplicaciones y pentesting periódico. |
| **R-02** | Caída total de la conectividad de la Casa Matriz y aislamiento de la Planta por fallo del equipo de borde | D-02, D-04 | 1.7, 2.3 | Firewall perimetral, enlace a Internet, enlace entre sedes | 4 | 5 | **CRÍTICO** (20) | C: clúster de firewalls en alta disponibilidad, segundo enlace ISP con failover y SLA documentado. |
| **R-03** | Propagación masiva de malware / ransomware por ausencia de segmentación en la red interna | D-07, D-08, D-09, D-10, D-11 | 4.1, 4.2, 4.3, 4.4, 5.1, 5.3 | Red interna, servidores de archivos y ERP, PLC de planta | 5 | 4 | **CRÍTICO** (20) | C: segmentación en VLAN por función con ACL, NAC, WiFi Enterprise con red de invitados aislada, EDR, renovación de sistemas operativos sin soporte y plan de respuesta a incidentes. |
| **R-04** | Ceguera operativa ante incidentes de seguridad por ausencia de SIEM y de plan de respuesta | D-16 | 8.1, 8.2, 8.3, 8.4 | Toda la infraestructura | 5 | 4 | **CRÍTICO** (20) | C: SIEM con correlación de logs, gestión de vulnerabilidades, plan formal de respuesta a incidentes y equipo designado (CSIRT/SOC interno, tercerizado o mixto). |
| **R-05** | Pérdida irrecuperable de datos ante desastre físico o ransomware por respaldos sin copia externa ni pruebas | D-14 | 7.2, 7.3, 7.4 | Servidores de producción, respaldos en cinta local | 3 | 5 | **ALTO** (15) | C: plataforma de respaldo con modelo 3-2-1, copia offsite / en nube, copia inmutable, cifrado y pruebas de restauración calendarizadas. |
| **R-06** | Acceso no monitoreado y persistente de proveedores externos al ERP y a la red interna | D-17 | 9.3, 9.4, 9.5, 9.6 | ERP, red interna, datos de terceros | 4 | 4 | **ALTO** (16) | C: cuentas temporales e individuales por proveedor, mínimo privilegio, grabación y auditoría de sesiones remotas y cláusulas contractuales de seguridad. |
| **R-07** | Suplantación de identidad y compromiso de credenciales por phishing y ausencia de MFA | D-05, D-15 | 3.1, 9.1, 9.2 | Correo corporativo, credenciales de dominio y VPN | 4 | 4 | **ALTO** (16) | C: MFA en VPN, correo y consolas; registros SPF, DKIM y DMARC; programa de concientización y simulacros de phishing. |
| **R-08** | Interceptación o descifrado del tráfico entre sedes por criptografía obsoleta en la VPN | D-03 | 2.1, 2.2, 2.4 | Tráfico Jutiapa↔Chiquimula | 4 | 3 | **ALTO** (12) | C: reemplazo de la VPN por IKEv2/IPsec con AES-256-GCM y SHA-2; evaluación de SD-WAN con enlace de respaldo. |
| **R-09** | Apagado abrupto y daño de equipos del centro de datos por autonomía energética insuficiente | D-13 | 6.4 | Servidores, almacenamiento, equipos de red del datacenter | 3 | 4 | **ALTO** (12) | C: ampliación de la autonomía de UPS para apagado ordenado y planta eléctrica de respaldo con transferencia automática. |
| **R-10** | Acceso físico no controlado y daño ambiental no detectado en el centro de datos | D-12 | 6.1, 6.2, 6.3 | Centro de datos de la Casa Matriz | 3 | 4 | **ALTO** (12) | C: control de acceso por tarjeta/biométrico con bitácora, CCTV con retención de 30 días y monitoreo ambiental con alertas. |

> **Nota sobre R-08:** con la regla de conversión declarada en §2.3 (ALTO = 12 – 19), el
> riesgo de la VPN (4 × 3 = 12) se clasifica como **ALTO**. Se corrige así la calificación
> para mantener coherencia aritmética con el resto de la matriz.

### 2.5 Cobertura de las 17 debilidades del caso

| Debilidad | Riesgo(s) que la representan |
|---|---|
| D-01 | R-01 |
| D-02 | R-02 |
| D-03 | R-08 |
| D-04 | R-02 |
| D-05 | R-03, R-07 |
| D-06 | R-03 (cuentas compartidas como facilitador de propagación y de acceso no auditable) |
| D-07 | R-03 |
| D-08 | R-03 |
| D-09 | R-03 |
| D-10 | R-03, R-05 |
| D-11 | R-03 |
| D-12 | R-10 |
| D-13 | R-09 |
| D-14 | R-05 |
| D-15 | R-07 |
| D-16 | R-04 |
| D-17 | R-06 |

---

## 3. Conclusión Ejecutiva

**Dirigida a la Dirección y Gerencia General de TransAgro del Oriente, S.A.**

A partir del diagnóstico tecnológico realizado con estándares internacionales de auditoría
(CIS Critical Security Controls v8.1 e ISO/IEC 27001:2022), el equipo de analistas concluye que
TransAgro del Oriente, S.A. enfrenta vulnerabilidades sistémicas derivadas del crecimiento no
planificado de su infraestructura durante más de diez años. La operación carece de una
arquitectura de seguridad formal, lo que genera niveles de riesgo inaceptables para la
continuidad del negocio.

De los diez riesgos priorizados en la matriz, **los cinco de mayor calificación
Probabilidad × Impacto**, y que requieren atención inmediata de la Gerencia, son:

1. **Exposición directa de la información del ERP a través de las aplicaciones web (R-01,
   crítico, 25).** La publicación de los portales de clientes y proveedores en la DMZ sin
   inspección de capa de aplicación (WAF, Anti-DDoS, filtrado DNS), sumada a que el Portal de
   Clientes se conecta directamente a la base de datos del ERP sin una capa de servicios
   intermedia, permite que un atacante transite desde la web pública hasta los registros
   financieros y operativos internos.

2. **Propagación masiva de malware o ransomware por la red plana (R-03, crítico, 20).** La
   ausencia de segmentación en la red interna (subred /16), unida a la falta de NAC y a una red
   WiFi con una sola clave compartida con visitantes, implica que un incidente en una sola
   computadora —o en el equipo de un visitante— puede alcanzar sin obstáculos los servidores
   del ERP y de archivos, y los controladores industriales (PLC) de las líneas de
   procesamiento en Chiquimula.

3. **Ceguera operativa ante incidentes (R-04, crítico, 20).** No existe un SIEM que centralice
   y correlacione registros, ni un plan formal de respuesta a incidentes, ni un responsable
   designado. Un ataque puede permanecer sin detección durante días o semanas, ampliando su
   alcance y su costo de recuperación.

4. **Punto único de falla en el borde de la red (R-02, crítico, 20).** Toda la conectividad
   externa de la Casa Matriz depende de un único firewall y un solo enlace de Internet. Una
   falla de hardware en ese nodo aislaría la sede principal y desconectaría de inmediato a la
   Planta de Procesamiento de Chiquimula, que depende del túnel VPN sobre ese mismo enlace.

5. **Imposibilidad de recuperación ante desastre o ransomware (R-05, alto, 15).** Los
   respaldos se almacenan en cinta dentro de la misma sala que aloja los servidores de
   producción, sin copia externa, sin copia inmutable y sin pruebas de restauración. Un
   incendio, una inundación o un cifrado malicioso destruiría simultáneamente los datos de
   producción y su única copia.

Los cinco riesgos comparten una causa raíz común: la falta de una arquitectura de seguridad
diseñada, y no meramente heredada. Las Fases 2, 3 y 4 de este proyecto desarrollan,
respectivamente, los controles, los procedimientos de continuidad y la inversión necesaria
para cerrarlos, manteniendo la trazabilidad D-nn → R-nn → C-nn → E-nn → I-nn.

---

## 4. Referencias

Barker, E., & Roginsky, A. (2019). *Transitioning the use of cryptographic algorithms and key
lengths* (NIST Special Publication 800-131A Rev. 2). National Institute of Standards and
Technology. https://doi.org/10.6028/NIST.SP.800-131Ar2

Center for Internet Security. (2024). *CIS Critical Security Controls version 8.1*.
https://www.cisecurity.org/controls/v8-1

Center for Internet Security. (2024). *Guide to implementation groups (IG): CIS Critical
Security Controls v8.1*.
https://www.cisecurity.org/insights/white-papers/guide-implementation-groups-ig-cis-critical-security-controls-v8-1

Microsoft. (2023). *Windows Server 2012 and 2012 R2 reaching end of support*. Microsoft
Lifecycle.
https://learn.microsoft.com/en-us/lifecycle/announcements/windows-server-2012-r2-end-of-support

Microsoft. (2022). *Windows 7 — Microsoft Lifecycle*.
https://learn.microsoft.com/en-us/lifecycle/products/windows-7

Microsoft. (2022). *Windows 8.1 — Microsoft Lifecycle*.
https://learn.microsoft.com/en-us/lifecycle/products/windows-81

National Institute of Standards and Technology. (2022, 15 de diciembre). *NIST retires SHA-1
cryptographic algorithm*.
https://www.nist.gov/news-events/news/2022/12/nist-retires-sha-1-cryptographic-algorithm

National Institute of Standards and Technology. (2024). *The NIST Cybersecurity Framework
(CSF) 2.0* (NIST CSWP 29). U.S. Department of Commerce.
https://doi.org/10.6028/NIST.CSWP.29

Open Worldwide Application Security Project. (2025). *OWASP Top 10:2025*.
https://owasp.org/Top10/2025/

Organización Internacional de Normalización. (2022). *ISO/IEC 27001:2022 — Information
security, cybersecurity and privacy protection — Information security management systems —
Requirements*. https://www.iso.org/standard/27001

Smyslov, V., & Hoffman, P. (2023). *Deprecation of the Internet Key Exchange version 1
(IKEv1) protocol and obsoleted algorithms* (RFC 9395). Internet Engineering Task Force.
https://doi.org/10.17487/RFC9395
