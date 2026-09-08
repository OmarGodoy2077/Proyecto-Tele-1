# CHECKLIST MAESTRO DE CUMPLIMIENTO

**Proyecto No. 01 — Seguridad de Redes · TransAgro del Oriente, S.A.**
Universidad Mariano Gálvez de Guatemala · Campus Jutiapa · Segundo Semestre 2026

> **Propósito**: control paralelo de avance. Cada ítem deriva de una exigencia literal del
> enunciado ([`00-guia/Proyecto No.md`](../00-guia/Proyecto%20No.md)), con la sección citada.
> **Marcar aquí cada vez que se completa algo.**

**Leyenda de estado**
`[ ]` pendiente · `[~]` en progreso · `[x]` completo y verificado · `[!]` incumple / requiere corrección · `[N/A]` no aplica

**Última actualización**: 2026-09-07
**Estado global**: Fase 1 revisada y corregida (contenido `.md`) · Fases 2–4 no iniciadas

---

## Resumen ejecutivo de avance

| Fase | Ítems | Completos | En progreso | Pendientes | Incumplen | % |
|---|---|---|---|---|---|---|
| Fase 1 — Diagnóstico | 18 | 13 | 2 | 3 | 0 | 78 % |
| Fase 2 — Plan de Seguridad | 26 | 0 | 0 | 26 | 0 | 0 % |
| Fase 3 — DRP | 30 | 0 | 0 | 30 | 0 | 0 % |
| Fase 4 — Adquisición | 22 | 0 | 0 | 22 | 0 | 0 % |
| Entrega final y formato | 16 | 0 | 0 | 16 | 0 | 0 % |
| Defensa oral | 6 | 0 | 0 | 6 | 0 | 0 % |
| **TOTAL** | **118** | **13** | **2** | **97** | **0** | **11 %** |

> **Nota (2026-09-07)**: los 3 ítems pendientes de la Fase 1 son de forma/soporte y no de
> contenido del diagnóstico: portada institucional con logo UMG e índice/numeración de página
> (se resuelven al producir el `.docx`, §8.3) y el diagrama de topología actual en Packet
> Tracer (§2.2 recomendado, §8.1 obligatorio; insumo de la Fase 2).

---

## FASE 1 — Diagnóstico de riesgos tecnológicos (20 pts)
*Referencia: enunciado §4.1 – §4.4*
*Documento auditado: [`01-fase1-diagnostico/Fase 1, Diagnóstico de riesgos tecnológicos.md`](../01-fase1-diagnostico/Fase%201,%20Diagn%C3%B3stico%20de%20riesgos%20tecnol%C3%B3gicos.md)*
*Revisión aplicada: 2026-09-07 — decisiones B-1 a B-9 (ver §2 de `fase1-hallazgos-auditoria.md`)*

### 1.A Checklist adaptado (§4.1)

| # | Requisito | Fuente | Estado | Nota |
|---|---|---|---|---|
| 1.A.1 | Se produjo un checklist **propio**, no el modelo del docente llenado | §4.1 | `[x]` | Formato propio; columnas #/Pregunta/D-nn/Ref. CIS-ISO/SÍ-NO-N-A/Observaciones. Toma como base el modelo del curso y lo amplía |
| 1.A.2 | Se investigó y citó **al menos un checklist adicional** de referencia | §4.1 | `[x]` | CIS Critical Security Controls **v8.1** e ISO/IEC 27001**:2022**, con edición explícita, cláusulas por ítem y §4 Referencias en APA 7 con URL |
| 1.A.3 | El checklist **documenta su fuente de referencia** explícitamente | §4.4 | `[x]` | §1 declara los marcos; §4 Referencias en APA 7 (11 entradas verificadas contra `referencias/fuentes-oficiales.md`) |
| 1.A.4 | Columnas **SÍ / NO / N-A** presentes | §4.4 | `[x]` | Presentes. §1.3 del entregable define el criterio de cada valor. Aparecen respuestas **SÍ** reales (1.1 DMZ, 2.1 VPN, 7.1 respaldos) además de los NO |
| 1.A.5 | Columna **Observaciones** completada | §4.4 | `[x]` | Completada en los 43 ítems |
| 1.A.6 | Es un **instrumento de auditoría reutilizable** (no solo aplicado a este caso) | §4.1 | `[x]` | 43 preguntas genéricas y reutilizables cubriendo los 9 dominios; §1.1 fija el nivel de aplicación (IG2) y lo justifica |

### 1.B Cobertura de los 9 dominios mínimos (§4.2)

| # | Dominio | Aspectos mínimos exigidos | Estado | Ítems actuales |
|---|---|---|---|---|
| 1.B.1 | Seguridad perimetral y DMZ | WAF, Anti-DDoS, filtrado DNS, segmentación DMZ↔interna, firewall SPOF vs HA | `[x]` | 7 ítems (1.1–1.7): DMZ, WAF, Anti-DDoS, DNS, segmentación/BD directa, Honeypot, HA. Cubre los 5 aspectos + deception |
| 1.B.2 | Comunicaciones | Robustez criptográfica VPN, redundancia de enlaces, cifrado entre sedes | `[x]` | 4 ítems (2.1–2.4): existencia VPN, IKEv2/AES-256/SHA-2, redundancia ISP/SLA, enlace de respaldo/SD-WAN |
| 1.B.3 | Identidad y control de acceso | MFA/2FA, política de contraseñas, cuentas privilegiadas, revisión periódica de accesos | `[x]` | 4 ítems (3.1–3.4): MFA, política de contraseñas, cuentas nominadas/mínimo privilegio, recertificación y baja de accesos |
| 1.B.4 | Red interna | VLAN, NAC, seguridad inalámbrica, aislamiento IoT/OT | `[x]` | 4 ítems (4.1–4.4): VLAN+ACL, NAC, WiFi Enterprise+invitados, aislamiento IoT/OT |
| 1.B.5 | Endpoints y sistemas | Vigencia SO, parches centralizados, antimalware/EDR, cifrado de discos | `[x]` | 5 ítems (5.1–5.5): soporte SO, parches centralizados, EDR, inventario de activos, cifrado de discos |
| 1.B.6 | Datacenter y seguridad física | Control de acceso físico, videovigilancia, monitoreo ambiental, energía | `[x]` | 4 ítems (6.1–6.4): acceso biométrico/tarjeta con bitácora, CCTV con retención, monitoreo ambiental, UPS+planta |
| 1.B.7 | Datos y continuidad | Política y prueba de respaldos, offsite, cifrado, retención | `[x]` | 4 ítems (7.1–7.4): ejecución de respaldos, offsite/3-2-1, pruebas de restauración, cifrado+inmutabilidad+retención |
| 1.B.8 | Monitoreo y respuesta a incidentes | SIEM, gestión de vulnerabilidades, plan de respuesta, responsable designado | `[x]` | 4 ítems (8.1–8.4): SIEM/correlación, gestión de vulnerabilidades+pentesting, plan de respuesta, CSIRT/SOC designado |
| 1.B.9 | Personal y proveedores | Concientización, accesos de terceros, cláusulas contractuales | `[x]` | 6 ítems (9.1–9.6): concientización, SPF/DKIM/DMARC, accesos temporales, credenciales nominadas+rotación, monitoreo de sesiones, cláusulas contractuales+NDA |

> **Conteo actual: 43 preguntas para 9 dominios**, cada una con `D-nn` declarado.
> Los 36+ aspectos mínimos de §4.2 quedan cubiertos con al menos un ítem propio.

### 1.C Matriz de riesgos (§4.3)

| # | Requisito | Estado | Nota |
|---|---|---|---|
| 1.C.1 | Escala de **Probabilidad 1–5** | `[x]` | §2.1: tabla con criterio para cada valor 1–5 |
| 1.C.2 | Escala de **Impacto 1–5** | `[x]` | §2.2: tabla con criterio para cada valor 1–5 |
| 1.C.3 | Clasificación en **Bajo / Medio / Alto / Crítico** | `[x]` | §2.3: regla declarada — CRÍTICO 20–25 · ALTO 12–19 · MEDIO 6–11 · BAJO 1–5, con criterio de tratamiento por nivel |
| 1.C.4 | **Justificación** de la calificación de probabilidad | `[x]` | Presente por riesgo (columna Prob. + escala §2.1 + control) |
| 1.C.5 | **Justificación** de la calificación de impacto | `[x]` | Presente por riesgo (columna Impacto + escala §2.2) |
| 1.C.6 | Columna **Activo/Proceso afectado** | `[x]` | Presente |
| 1.C.7 | Columna **Control propuesto referenciado a Fase 2** | `[x]` | Presente. Riesgos numerados R-01…R-10; columnas `Debilidades (D-nn)` e `Ítem(s) del checklist`; control marcado como C (Fase 2) |
| 1.C.8 | Cobertura: las **17 debilidades** del caso están representadas | `[x]` | §2.5: tabla D-nn → R-nn. Las 17 debilidades tienen al menos un riesgo asociado (se agregaron R-09 para D-13 y R-10 para D-12) |
| 1.C.9 | Coherencia aritmética P×I ↔ nivel asignado | `[x]` | R-08 (VPN, 4×3=12) reclasificado de MEDIO a **ALTO** para cumplir la regla §2.3. Todos los niveles cierran con el rango declarado |

### 1.D Conclusión ejecutiva (§4.4)

| # | Requisito | Estado | Nota |
|---|---|---|---|
| 1.D.1 | Extensión de **una página** | `[~]` | Aproximadamente cumple; verificar al maquetar el `.docx` |
| 1.D.2 | **Exactamente CINCO riesgos más críticos** | `[x]` | Lista exactamente 5: R-01 (25), R-03 (20), R-04 (20), R-02 (20), R-05 (15) |
| 1.D.3 | Lenguaje dirigido a dirección/gerencia (no técnico) | `[x]` | Bien logrado; traduce riesgo técnico a consecuencia de negocio |
| 1.D.4 | Los riesgos listados coinciden con los CRÍTICOS de la matriz | `[x]` | Son los 5 de mayor P×I, ordenados de mayor a menor, con el puntaje citado |

### 1.E Entregables de la Fase 1 (§4.4)

| # | Entregable | Estado |
|---|---|---|
| 1.E.1 | Checklist adaptado con fuente de referencia citada | `[x]` |
| 1.E.2 | Checklist aplicado al caso con SÍ/NO/N-A y observaciones | `[x]` |
| 1.E.3 | Matriz de riesgos priorizada | `[x]` |
| 1.E.4 | Conclusión ejecutiva de una página con 5 riesgos críticos | `[x]` |

### 1.F Recomendado por el enunciado (§2.2)

| # | Requisito | Estado | Nota |
|---|---|---|---|
| 1.F.1 | Diagrama de topología física y lógica del estado actual | `[ ]` | Recomendado en §2.2; **obligatorio en §8.1 en Packet Tracer**. Pendiente; insumo directo de la Fase 2 |

### 1.G Forma y soporte del entregable (§8.3)

| # | Requisito | Estado | Nota |
|---|---|---|---|
| 1.G.1 | Encabezado / bloque de identificación institucional | `[~]` | Bloque textual al inicio del `.md` (universidad, curso, docente, fase, caso). **Falta completar integrantes y fecha** y trasladar a portada con logo UMG en el `.docx` |
| 1.G.2 | Portada, índice, numeración de página | `[ ]` | Se resuelve al producir el `.docx` |
| 1.G.3 | Tablas legibles (no colapsadas por conversión) | `[x]` | Tablas del checklist y la matriz reconstruidas en Markdown válido |
| 1.G.4 | Fuente Calibri/Arial 11 pt, interlineado 1.15, márgenes 1" | `[ ]` | Aplica al `.docx` final |

> 📄 Detalle completo de las brechas y su resolución: [`fase1-hallazgos-auditoria.md`](fase1-hallazgos-auditoria.md)

---

## FASE 2 — Plan de Seguridad Informática (20 pts)
*Referencia: enunciado §5.1 – §5.3*

### 2.A Estructura obligatoria (§5.1)

| # | Sección | Estado |
|---|---|---|
| 2.A.1 | 1. Alcance del Plan de Seguridad Informática | `[ ]` |
| 2.A.2 | 2. Caracterización del sistema informático — bienes | `[ ]` |
| 2.A.3 | 2. Caracterización — redes | `[ ]` |
| 2.A.4 | 2. Caracterización — aplicaciones y servicios | `[ ]` |
| 2.A.5 | 2. Caracterización — personal | `[ ]` |
| 2.A.6 | 2. Caracterización — edificaciones | `[ ]` |
| 2.A.7 | 3. Resultados del análisis de riesgo (retomando Fase 1) | `[ ]` |
| 2.A.8 | 4. Políticas de seguridad informática (normas de obligatorio cumplimiento) | `[ ]` |
| 2.A.9 | 5. Responsabilidades — Dirección | `[ ]` |
| 2.A.10 | 5. Responsabilidades — Gerencia de TI | `[ ]` |
| 2.A.11 | 5. Responsabilidades — Administradores | `[ ]` |
| 2.A.12 | 5. Responsabilidades — Usuarios | `[ ]` |
| 2.A.13 | 7. Anexos — listado nominal de usuarios | `[ ]` |
| 2.A.14 | 7. Anexos — registros | `[ ]` |
| 2.A.15 | 7. Anexos — control de cambios | `[ ]` |

### 2.B Medidas y procedimientos — los 9 bloques mínimos (§5.1 punto 6)

| # | Bloque | Debilidades que debe cubrir | Estado |
|---|---|---|---|
| 2.B.1 | Clasificación y control de los bienes informáticos | D-10, D-11 | `[ ]` |
| 2.B.2 | Gestión del personal (selección, capacitación, altas/bajas de acceso) | D-15, D-17 | `[ ]` |
| 2.B.3 | Seguridad física y ambiental (datacenter, acceso, energía) | D-12, D-13 | `[ ]` |
| 2.B.4 | Seguridad de operaciones (cambios, mantenimiento, nuevos sistemas) | D-02, D-10 | `[ ]` |
| 2.B.5 | Identificación, autenticación y control de acceso (incl. MFA/2FA) | D-05, D-06 | `[ ]` |
| 2.B.6 | Seguridad ante programas malignos (antivirus/EDR) | D-11 | `[ ]` |
| 2.B.7 | Respaldo de la información (política, pruebas de restauración) | D-14 | `[ ]` |
| 2.B.8 | Seguridad en redes (segmentación, VPN, WAF, Anti-DDoS, DNS, NAC) | D-01, D-03, D-04, D-07, D-08, D-09 | `[ ]` |
| 2.B.9 | Gestión de incidentes de seguridad (procedimientos por tipo) | D-16 | `[ ]` |

### 2.C Tratamiento obligatorio de debilidades del caso (§5.2, tabla)

Cada fila es una correspondencia **exigida literalmente** por el enunciado.

| # | Debilidad | Debe quedar reflejada en… | Estado |
|---|---|---|---|
| 2.C.1 | DMZ sin WAF / Honeypot / Anti-DDoS / DNS Protection (D-01) | Seguridad en redes — control de publicación de servicios y protección de apps web | `[ ]` |
| 2.C.2 | Firewall sin alta disponibilidad (D-02) | Seguridad de operaciones — continuidad de servicios críticos (enlazado al DRP) | `[ ]` |
| 2.C.3 | VPN antigua sobre red pública (D-03) | Seguridad en redes — comunicaciones entre sedes | `[ ]` |
| 2.C.4 | Sin 2FA en accesos internos (D-05) | Identificación, autenticación y control de acceso | `[ ]` |
| 2.C.5 | Red plana sin segmentación (D-07) | Seguridad en redes — segmentación y control de acceso a la red | `[ ]` |
| 2.C.6 | Datacenter sin protección perimetral física (D-12) | Seguridad física y ambiental | `[ ]` |
| 2.C.7 | Sistemas operativos desactualizados (D-10) | Clasificación y control de bienes / Seguridad de operaciones (parches) | `[ ]` |
| 2.C.8 | Accesos permanentes de proveedores (D-17) | Gestión del personal y terceros — control de acceso de proveedores | `[ ]` |
| 2.C.9 | Sin SIEM ni plan de respuesta a incidentes (D-16) | Gestión de incidentes de seguridad | `[ ]` |

### 2.D Entregables y formato (§5.3)

| # | Requisito | Estado |
|---|---|---|
| 2.D.1 | **Ninguna sección en corchetes o sin desarrollar** (§5) | `[ ]` |
| 2.D.2 | Portada institucional con logo UMG | `[ ]` |
| 2.D.3 | Control de versiones del documento | `[ ]` |
| 2.D.4 | **Tabla de trazabilidad riesgo → política/medida** | `[ ]` |
| 2.D.5 | Cada medida responde explícitamente a ≥1 debilidad de §2.4 | `[ ]` |
| 2.D.6 | Contenido específico y realista para TransAgro (no genérico) | `[ ]` |

---

## FASE 3 — Plan de Recuperación ante Desastres (20 pts)
*Referencia: enunciado §6.1 – §6.6*

### 3.A Estructura obligatoria — 11 secciones (§6.1)

| # | Sección | Estado |
|---|---|---|
| 3.A.1 | 1. Información general (objetivo, responsable, alcance) | `[ ]` |
| 3.A.2 | 2. Condiciones generales y supuestos del plan | `[ ]` |
| 3.A.3 | 3. Comité de Crisis (integrantes **por rol**, responsabilidades antes/durante/después) | `[ ]` |
| 3.A.4 | 3. Equipo de Recuperación (por rol, antes/durante/después) | `[ ]` |
| 3.A.5 | 3. Equipo de Pruebas (por rol, antes/durante/después) | `[ ]` |
| 3.A.6 | 4. Escenarios de desastre contemplados | `[ ]` |
| 3.A.7 | 5. Tabla de componentes críticos con RTO y RPO | `[ ]` |
| 3.A.8 | 6. Árbol de llamadas | `[ ]` |
| 3.A.9 | 6. Procedimientos de notificación, evaluación y activación del DRP | `[ ]` |
| 3.A.10 | 7. Procedimientos de recuperación por escenario (paso a paso, con responsable por actividad) | `[ ]` |
| 3.A.11 | 8. Centro de control / sitio alterno de operaciones | `[ ]` |
| 3.A.12 | 9. Actividades de manejo de crisis y comunicación | `[ ]` |
| 3.A.13 | 10. Actividades de mantenimiento y prueba del DRP (periodicidad, responsables) | `[ ]` |
| 3.A.14 | 11. Distribución del documento y control de cambios | `[ ]` |

### 3.B Tabla RTO/RPO justificada (§6.2)

| # | Componente / Servicio | RTO | RPO | Justificación de negocio | Estado |
|---|---|---|---|---|---|
| 3.B.1 | ERP / Base de datos transaccional | | | | `[ ]` |
| 3.B.2 | Portal de Clientes / Portal de Proveedores | | | | `[ ]` |
| 3.B.3 | Correo electrónico corporativo | | | | `[ ]` |
| 3.B.4 | Enlace VPN entre sedes | | | | `[ ]` |
| 3.B.5 | Sistema de Rastreo de Flotilla | | | | `[ ]` |
| 3.B.6 | Infraestructura de red (firewall, switch core) | | | | `[ ]` |

> ⚠️ El enunciado advierte explícitamente: **fundamentar cada valor en el impacto de negocio,
> no copiar valores de un ejemplo genérico.**

### 3.C Escenarios de desastre (§6.3) — los 8 deben estar contemplados; **mínimo 3 desarrollados paso a paso**

| # | Escenario | Contemplado | Desarrollado paso a paso |
|---|---|---|---|
| 3.C.1 | E-01 No disponibilidad del centro de datos (incendio, inundación, falla A/C, corte eléctrico prolongado) | `[ ]` | `[ ]` |
| 3.C.2 | E-02 Falla o compromiso del firewall perimetral único | `[ ]` | `[ ]` |
| 3.C.3 | E-03 Caída del enlace VPN entre sedes | `[ ]` | `[ ]` |
| 3.C.4 | E-04 Incidente de ciberseguridad en la DMZ con movimiento lateral hacia BD interna | `[ ]` | `[ ]` |
| 3.C.5 | E-05 Ransomware con cifrado de servidores de archivos y/o ERP | `[ ]` | `[ ]` |
| 3.C.6 | E-06 Pérdida o corrupción de respaldos | `[ ]` | `[ ]` |
| 3.C.7 | E-07 Eventos del contexto guatemalteco: sismos, tormentas tropicales, inundaciones estacionales | `[ ]` | `[ ]` |
| 3.C.8 | E-08 Interrupción prolongada del ISP único | `[ ]` | `[ ]` |
| | **Mínimo exigido: 3 desarrollados** | | `[ ]` |

### 3.D Roles, árbol de llamadas y activación (§6.4)

| # | Requisito | Estado |
|---|---|---|
| 3.D.1 | Árbol de llamadas **propio**, desde quien detecta/reporta hasta Gerente de TI y Gerencia General | `[ ]` |
| 3.D.2 | Se define **explícitamente qué rol tiene autoridad para activar el DRP** | `[ ]` |
| 3.D.3 | Se definen los **criterios de activación** (ej.: umbral de horas definido por el grupo) | `[ ]` |
| 3.D.4 | Integrantes designados **por rol, no por nombre** | `[ ]` |

### 3.E Sitio alterno (§6.5)

| # | Requisito | Estado |
|---|---|---|
| 3.E.1 | Se propone una estrategia de contingencia (frío/tibio/caliente, nube pública o reciprocidad entre sedes) | `[ ]` |
| 3.E.2 | La estrategia está **justificada** técnicamente | `[ ]` |
| 3.E.3 | La decisión está **conectada con el presupuesto de la Fase 4** | `[ ]` |

### 3.F Manejo de crisis y entregables (§6.1 punto 9, §6.6)

| # | Requisito | Estado |
|---|---|---|
| 3.F.1 | Principios de comunicación: informar rápida y periódicamente, decir la verdad, emitir reportes exactos | `[ ]` |
| 3.F.2 | Audiencias a considerar identificadas (clientes, proveedores, personal, autoridades, medios) | `[ ]` |
| 3.F.3 | Portada institucional con logo UMG | `[ ]` |
| 3.F.4 | Control de versiones | `[ ]` |
| 3.F.5 | El documento combina **ambas** referencias del docente (Guía DRP + Plantilla DGCTIC) | `[ ]` |

---

## FASE 4 — Plan de adquisición e implementación (20 pts)
*Referencia: enunciado §7.1 – §7.5*

### 4.A Metodología de la propuesta (§7.1)

| # | Requisito | Estado |
|---|---|---|
| 4.A.1 | Cada rubro traduce una brecha de Fase 1 / política de Fase 2 | `[ ]` |
| 4.A.2 | Se especifica **qué se compra o contrata** | `[ ]` |
| 4.A.3 | Se especifica **con qué arquitectura** | `[ ]` |
| 4.A.4 | Se especifica **de qué proveedor** | `[ ]` |
| 4.A.5 | Se especifica **a qué costo referencial** | `[ ]` |
| 4.A.6 | Ordenada **por prioridad** (crítico / alto / medio) | `[ ]` |
| 4.A.7 | **CAPEX separado de OPEX** | `[ ]` |
| 4.A.8 | Marcas distintas a las del enunciado **justificadas técnicamente** (si aplica) | `[ ]` |

### 4.B Cobertura de rubros del marco de referencia (§7.2)

| # | Rubro | Debilidad | Estado |
|---|---|---|---|
| 4.B.1 | Firewall perimetral en alta disponibilidad (NGFW) | D-02 | `[ ]` |
| 4.B.2 | WAF | D-01 | `[ ]` |
| 4.B.3 | Protección Anti-DDoS | D-01 | `[ ]` |
| 4.B.4 | Protección / filtrado DNS | D-01 | `[ ]` |
| 4.B.5 | Honeypot / Deception | D-01 | `[ ]` |
| 4.B.6 | Reemplazo de VPN sitio a sitio / SD-WAN | D-03 | `[ ]` |
| 4.B.7 | Redundancia de enlace a Internet (segundo ISP) | D-04 | `[ ]` |
| 4.B.8 | Autenticación multifactor (MFA/2FA) | D-05, D-06 | `[ ]` |
| 4.B.9 | NAC y segmentación VLAN | D-07, D-09 | `[ ]` |
| 4.B.10 | Red inalámbrica corporativa segmentada | D-08 | `[ ]` |
| 4.B.11 | EDR | D-11 | `[ ]` |
| 4.B.12 | Gestión centralizada de parches | D-10 | `[ ]` |
| 4.B.13 | Renovación de sistemas operativos de servidor | D-10 | `[ ]` |
| 4.B.14 | Control de acceso físico y videovigilancia | D-12 | `[ ]` |
| 4.B.15 | Monitoreo ambiental del centro de datos | D-12 | `[ ]` |
| 4.B.16 | Energía de respaldo (UPS ampliado / planta eléctrica) | D-13 | `[ ]` |
| 4.B.17 | Plataforma de respaldo con copia inmutable y offsite (3-2-1) | D-14 | `[ ]` |
| 4.B.18 | SIEM / centralización de logs | D-16 | `[ ]` |
| 4.B.19 | Observabilidad y monitoreo de infraestructura | D-16 | `[ ]` |
| 4.B.20 | NDR / IDS-IPS complementario | D-16 | `[ ]` |

### 4.C Talento humano (§7.3)

| # | Requisito | Estado |
|---|---|---|
| 4.C.1 | Estructura organizacional propuesta (Gerencia General → Comité → Oficial de Seguridad → SOC N1 → Incident Responder) | `[ ]` |
| 4.C.2 | Perfiles y certificaciones sugeridas por rol | `[ ]` |
| 4.C.3 | Modalidad definida (interno / tercerizado / mixto) **y justificada** | `[ ]` |
| 4.C.4 | Costo mensual referencial por rol | `[ ]` |
| 4.C.5 | Valores salariales **contrastados con la escala vigente del sector TI en Guatemala** | `[ ]` |
| 4.C.6 | Coordinación con los administradores de sistemas ya existentes | `[ ]` |

### 4.D Inversión consolidada (§7.4)

| # | Dominio | Prioridad exigida | CAPEX | OPEX anual | Responsable | Estado |
|---|---|---|---|---|---|---|
| 4.D.1 | Perímetro y aplicaciones (DMZ) | Crítica | | | | `[ ]` |
| 4.D.2 | Comunicaciones entre sedes | Alta | | | | `[ ]` |
| 4.D.3 | Identidad, acceso y red interna | Alta | | | | `[ ]` |
| 4.D.4 | Endpoints y sistemas | Media | | | | `[ ]` |
| 4.D.5 | Seguridad física y datacenter | Alta | | | | `[ ]` |
| 4.D.6 | Respaldo, monitoreo y respuesta a incidentes | Crítica | | | | `[ ]` |
| 4.D.7 | Talento humano (CSIRT/SOC) | Crítica | — | | | `[ ]` |
| 4.D.8 | **TOTAL CONSOLIDADO** | | | | | `[ ]` |

### 4.E Entregables de la Fase 4 (§7.5) — **crítico para la calificación**

| # | Requisito | Estado | Nota |
|---|---|---|---|
| 4.E.1 | **Cotización / referencia verificada #1** (captura, enlace o constancia de contacto) | `[ ]` | Exigencia literal |
| 4.E.2 | **Cotización / referencia verificada #2** | `[ ]` | Exigencia literal |
| 4.E.3 | **Cotización / referencia verificada #3** | `[ ]` | Exigencia literal |
| 4.E.4 | Las 3 cotizaciones son de **distribuidor/proveedor autorizado en Guatemala o la región** | `[ ]` | §7.1 |
| 4.E.5 | Todas las tablas de §7.2, §7.3 y §7.4 completas y **con fuentes citadas** | `[ ]` | |
| 4.E.6 | **Propuesta de fases de implementación** (qué se adquiere primero y por qué, según nivel de riesgo) | `[ ]` | |

---

## ENTREGA FINAL — Integración, redacción y formato (10 pts)
*Referencia: enunciado §8.1 – §8.3*

### 5.A Documentos (§8.1)

| # | Requisito | Estado |
|---|---|---|
| 5.A.1 | Documento consolidado en **Word (.docx)** | `[ ]` |
| 5.A.2 | Documento consolidado en **PDF** | `[ ]` |
| 5.A.3 | **Portada institucional única**: logo UMG, nombre del curso, integrantes, docente, fecha | `[ ]` |
| 5.A.4 | Incluye los 4 planes como capítulos o anexos | `[ ]` |
| 5.A.5 | Presentación **PowerPoint, máximo 20 diapositivas** | `[ ]` |
| 5.A.6 | Presentación orientada a **dirección/gerencia** (lenguaje claro, sin saturar de texto técnico) | `[ ]` |
| 5.A.7 | Diagrama de topología de red **actual** | `[ ]` |
| 5.A.8 | Diagrama de topología **propuesta** | `[ ]` |
| 5.A.9 | Ambos diagramas elaborados **en Cisco Packet Tracer** (obligatorio) | `[ ]` |

### 5.B Normas de formato (§8.3)

| # | Requisito | Estado |
|---|---|---|
| 5.B.1 | Papel tamaño **carta**, márgenes de **1 pulgada** | `[ ]` |
| 5.B.2 | Fuente **Calibri o Arial 11 pt** | `[ ]` |
| 5.B.3 | Interlineado **1.15** | `[ ]` |
| 5.B.4 | Portada, índice, numeración de página y encabezado institucional en **todos** los documentos | `[ ]` |
| 5.B.5 | Tablas, diagramas y cifras **tituladas** | `[ ]` |
| 5.B.6 | Fuentes externas **citadas en APA 7ª ed.** (o el formato que indique el docente) | `[ ]` |
| 5.B.7 | **Sin copia literal** de las plantillas de referencia del docente | `[ ]` |

### 5.C Coherencia entre documentos

| # | Requisito | Estado |
|---|---|---|
| 5.C.1 | Trazabilidad completa D-nn → R-nn → C-nn → E-nn → I-nn verificada | `[ ]` |
| 5.C.2 | Sin contradicciones entre fases (ej.: sitio alterno del DRP presupuestado en Fase 4) | `[ ]` |
| 5.C.3 | Terminología y nombres de activos consistentes en los 4 documentos | `[ ]` |

---

## DEFENSA ORAL (10 pts)
*Referencia: enunciado §8.2*

| # | Requisito | Estado |
|---|---|---|
| 6.A.1 | Duración de **20 a 25 minutos** (ensayada y cronometrada) | `[ ]` |
| 6.A.2 | Preparación para **10 minutos de preguntas** | `[ ]` |
| 6.A.3 | **Todos los integrantes participan** activamente | `[ ]` |
| 6.A.4 | La participación de cada quien **corresponde al rol que desempeñó** (§3.2) | `[ ]` |
| 6.A.5 | El grupo puede **justificar cada decisión técnica** ante preguntas | `[ ]` |
| 6.A.6 | El grupo puede **justificar cada rubro de inversión** | `[ ]` |

---

## Registro de cambios de este checklist

| Fecha | Cambio | Autor |
|---|---|---|
| 2026-09-05 | Creación del checklist maestro; auditoría inicial de la Fase 1 entregada | — |
| 2026-09-07 | Fase 1 revisada y corregida (decisiones B-1 a B-9): checklist ampliado a 43 ítems con `D-nn`, escalas P/I y regla P×I publicadas, matriz R-01…R-10 con trazabilidad y cobertura de las 17 debilidades, conclusión ejecutiva a 5 riesgos, marcos unificados a ISO 27001:2022 / CIS v8.1 + IG2, §4 Referencias APA 7, encabezado institucional, tablas reparadas. Fase 1 pasa de 28 % a 78 %. Pendientes: portada/índice del `.docx` y topología en Packet Tracer | — |
