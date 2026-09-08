# CLAUDE.md — Memoria del Proyecto

> Memoria de contexto para agentes de IA y para el equipo humano.
> **Este archivo es la fuente de verdad sobre QUÉ pide el proyecto.**
> Ante cualquier duda, la autoridad final es [`00-guia/Proyecto No.md`](00-guia/Proyecto%20No.md) (enunciado del docente).

---

## 1. Identificación

| Campo | Valor |
|---|---|
| Universidad | Universidad Mariano Gálvez de Guatemala |
| Facultad | Ingeniería en Sistemas de Información |
| Campus | Jutiapa |
| Curso | Telecomunicaciones — Área de Especialidad, último semestre |
| Unidad integradora | Seguridad de Redes |
| Docente | Ing. Juan Daniel Ramos Martínez |
| Ciclo | Segundo Semestre 2026 |
| Proyecto | No. 01 de curso |
| Caso de estudio | TransAgro del Oriente, S.A. (ficticio, obligatorio, **no modificable**) |

---

## 2. Qué se entrega (4 fases + integración)

| Fase | Nombre | Entregable principal | Puntos |
|---|---|---|---|
| 1 | Diagnóstico de riesgos tecnológicos | Checklist adaptado + aplicado + matriz de riesgos + conclusión ejecutiva | 20 |
| 2 | Plan de Seguridad Informática | Documento formal (estructura obligatoria de 7 secciones) | 20 |
| 3 | Plan de Recuperación ante Desastres | DRP formal (estructura obligatoria de 11 secciones) | 20 |
| 4 | Plan de adquisición e implementación | Propuesta técnico-económica CAPEX/OPEX + 3 cotizaciones verificadas | 20 |
| — | Integración, redacción y formato | Coherencia entre los 4 documentos + normas de formato | 10 |
| — | Defensa oral | 20–25 min + 10 min preguntas, participación de **todos** | 10 |
| | | **TOTAL** | **100** |

---

## 3. El caso: TransAgro del Oriente, S.A.

### 3.1 Perfil
Empresa guatemalteca de acopio, procesamiento y comercialización de granos básicos y
productos agroindustriales, región oriental. **~480 colaboradores**, **2 sedes**:

- **Casa Matriz (Jutiapa)** — administración, finanzas, ventas, atención a clientes.
  Centro de datos principal: **18 servidores** físicos y virtualizados.
- **Planta de Procesamiento (Chiquimula)** — acopio, procesamiento industrial, control de
  calidad, logística. Cuarto de telecomunicaciones local con controladores de planta (PLC),
  cámaras de videovigilancia y estaciones administrativas.

Exporta a mercados centroamericanos. Depende de TI para pedidos, facturación electrónica,
trazabilidad de cadena de frío/transporte y comunicación con proveedores agrícolas.

### 3.2 Infraestructura actual (implementada de forma incremental >10 años, sin arquitectura formal)
- Router de borde → **un solo ISP** → **firewall perimetral único (sin HA)** que separa
  Internet / DMZ / red interna.
- **DMZ** con 3 aplicaciones web públicas sobre SO desactualizado.
- **VPN sitio a sitio** Jutiapa↔Chiquimula sobre Internet público, equipos y configuración
  de **más de 6 años**.
- **Red interna plana, sin VLAN**: estaciones, servidores (ERP, correo, archivos),
  impresoras, cámaras IP y PLC comparten la **misma subred /16**.
- Centro de datos en Casa Matriz con controles físicos y ambientales limitados.
- **Respaldo local en cinta**, sin política de retención ni copia externa.

### 3.3 Aplicaciones publicadas en la DMZ

| Aplicación | Función de negocio | Debilidad técnica |
|---|---|---|
| Portal de Clientes | Ingreso y seguimiento de pedidos de granos y derivados (clientes mayoristas) | Framework desactualizado; **conexión directa a la BD interna del ERP**, sin capa de servicios intermedia |
| Portal de Proveedores | Facturación electrónica y programación de entregas de proveedores agrícolas | **Carga de archivos sin validación** robusta de tipo/contenido; sin WAF |
| Sistema de Rastreo de Flotilla | Consulta GPS y estado de flotilla en tiempo real | Integración API con SaaS externo mediante **credenciales estáticas embebidas en el código** |

> Las tres comparten **el mismo segmento de DMZ y el mismo servidor de BD backend**:
> comprometer una amenaza a las demás y, potencialmente, a la red interna.

### 3.4 Las 17 debilidades del caso (sección 2.4 del enunciado) — **IDs canónicos del repo**

Usar SIEMPRE estos identificadores para trazabilidad entre las 4 fases.

| ID | Categoría | Debilidad |
|---|---|---|
| **D-01** | Perímetro y DMZ | 3 apps web en DMZ sin control de capa de aplicación: sin WAF, sin Honeypot/Deception, sin Anti-DDoS, sin protección/filtrado DNS |
| **D-02** | Perímetro y DMZ | Firewall perimetral único (sin clúster HA); punto único de falla de todo el tráfico de Casa Matriz |
| **D-03** | Comunicaciones | VPN IPsec Jutiapa↔Chiquimula de >6 años sobre Internet público, con **IKEv1 y 3DES/SHA-1**; sin enlace de respaldo ni SD-WAN |
| **D-04** | Comunicaciones | **Un solo ISP**, sin redundancia de enlace ni balanceo de carga |
| **D-05** | Identidad y acceso | **Sin 2FA/MFA** en VPN, correo corporativo, dominio interno ni consolas de administración |
| **D-06** | Identidad y acceso | **Cuentas administrativas compartidas**; política de contraseñas sin complejidad ni expiración |
| **D-07** | Red interna | **Red plana sin VLAN**: usuarios, servidores, impresoras, cámaras IP y PLC en la misma subred /16, sin ACL entre segmentos |
| **D-08** | Red interna | WiFi corporativa con **una sola clave WPA2-Personal** compartida con personal y visitantes; sin red de invitados aislada ni portal cautivo |
| **D-09** | Red interna | **Sin NAC**: cualquier dispositivo conectado a un punto de red obtiene IP y acceso a recursos internos |
| **D-10** | Endpoint y sistemas | SO desactualizados: **Windows Server 2012 R2** sin soporte extendido, estaciones **Windows 7/8.1**; sin gestión centralizada de parches |
| **D-11** | Endpoint y sistemas | Antivirus de firmas desactualizado; **sin EDR** y **sin inventario confiable de activos** |
| **D-12** | Datacenter y físico | Sala de servidores **sin control biométrico/tarjeta** (solo llave física compartida), CCTV parcial, **sin monitoreo ambiental** |
| **D-13** | Datacenter y físico | **UPS de solo 15 minutos**; sin planta eléctrica de respaldo |
| **D-14** | Datos y continuidad | Respaldos en **cinta local en el mismo cuarto de servidores**; sin copia offsite, sin copia inmutable, **sin pruebas de restauración** |
| **D-15** | Correo y usuarios | Dominio de correo **sin SPF, DKIM ni DMARC**; **sin programa de concientización** en ciberseguridad |
| **D-16** | Monitoreo y respuesta | **Sin SIEM** ni correlación de logs; sin gestión de vulnerabilidades ni pentesting; **sin plan de respuesta a incidentes** ni CSIRT/SOC |
| **D-17** | Terceros / proveedores | **Accesos remotos permanentes** a proveedores externos, sin monitoreo, sin cuentas temporales, **sin cláusulas contractuales** de seguridad |

### 3.5 Personal de TI actual
- 1 Gerente de TI (reporta a Gerencia General)
- 2 Administradores de sistemas y redes (Casa Matriz)
- 1 Técnico de soporte en sitio (Planta, Chiquimula)
- **Cero personal dedicado a seguridad de la información, monitoreo o respuesta a incidentes**

### 3.6 Proveedores externos
- ISP para ambas sedes, **sin SLA documentado**
- Integrador que instaló firewall y VPN hace >6 años, **contrato de soporte no vigente**
- SaaS de rastreo de flotilla (terceriza datos de ubicación)
- Nómina electrónica en la nube, con acceso remoto periódico
- Consultor externo del ERP, **acceso remoto permanente con credenciales no rotadas**

---

## 4. Regla de oro: TRAZABILIDAD

> Cada debilidad de la Fase 1 debe estar cubierta por **al menos una medida concreta en la
> Fase 2**, **un procedimiento de continuidad en la Fase 3** y —cuando aplique— **un rubro de
> inversión en la Fase 4**.

Convención de IDs del repositorio:

| Prefijo | Significado | Fase | Ejemplo |
|---|---|---|---|
| `D-nn` | Debilidad del caso (sección 2.4) | Insumo | `D-03` |
| `R-nn` | Riesgo de la matriz de riesgos | 1 | `R-05` |
| `C-nn` | Control / medida del Plan de Seguridad | 2 | `C-12` |
| `E-nn` | Escenario de desastre del DRP | 3 | `E-04` |
| `I-nn` | Rubro de inversión (CAPEX/OPEX) | 4 | `I-07` |

La cadena completa se registra en [`auditoria/matriz-trazabilidad.md`](auditoria/matriz-trazabilidad.md).

---

## 5. Requisitos NO negociables (fuente de descuentos si se incumplen)

### 5.1 Fase 1 — Diagnóstico
- Checklist **propio y adaptado**, no el modelo del docente llenado.
- Investigar y citar **al menos un checklist adicional** (CIS Controls v8, ISO/IEC 27001
  Anexo A o NIST CSF) y documentar la fuente.
- Columnas obligatorias: **SÍ / NO / N-A + Observaciones**.
- Cubrir **los 9 dominios mínimos** de la sección 4.2 (ver §6 abajo).
- Matriz de riesgos: **Probabilidad (1-5) × Impacto (1-5)** → Bajo/Medio/Alto/Crítico,
  **con justificación** de cada calificación.
- Estructura de la matriz sugerida: Riesgo | Activo/Proceso afectado | Probabilidad | Impacto
  | Nivel de riesgo | Control propuesto (referenciado a Fase 2).
- **Conclusión ejecutiva de UNA página con los CINCO riesgos más críticos** (exactamente 5).

### 5.2 Fase 2 — Plan de Seguridad Informática
Estructura obligatoria, **sin secciones en corchetes ni sin desarrollar**:
1. Alcance del Plan de Seguridad Informática
2. Caracterización del sistema informático (bienes, redes, aplicaciones, servicios, personal, edificaciones)
3. Resultados del análisis de riesgo (retomando la Fase 1)
4. Políticas de seguridad informática (normas generales de obligatorio cumplimiento)
5. Responsabilidades (por rol: dirección, gerencia de TI, administradores, usuarios)
6. Medidas y procedimientos, **desagregados como mínimo en 9 bloques**:
   1. Clasificación y control de los bienes informáticos
   2. Gestión del personal (selección, capacitación, altas y bajas de acceso)
   3. Seguridad física y ambiental (datacenter, control de acceso, energía)
   4. Seguridad de operaciones (gestión de cambios, mantenimiento, nuevos sistemas)
   5. Identificación, autenticación y control de acceso (incluyendo MFA/2FA)
   6. Seguridad ante programas malignos (antivirus/EDR)
   7. Respaldo de la información (política, pruebas de restauración)
   8. Seguridad en redes (segmentación, VPN, WAF, Anti-DDoS, DNS, NAC)
   9. Gestión de incidentes de seguridad (procedimientos de respuesta por tipo)
7. Anexos (listado nominal de usuarios, registros, control de cambios)

**Además**: portada institucional (logo UMG), control de versiones y **tabla de trazabilidad
riesgo → política/medida**.

### 5.3 Fase 3 — DRP
Estructura obligatoria de **11 secciones**:
1. Información general (objetivo, responsable, alcance)
2. Condiciones generales y supuestos del plan
3. Comité de Crisis, Equipo de Recuperación y Equipo de Pruebas (**por rol, no por nombre**;
   responsabilidades antes / durante / después)
4. Escenarios de desastre contemplados
5. Tabla de componentes críticos con RTO y RPO
6. Árbol de llamadas y procedimientos de notificación, evaluación y activación del DRP
7. Procedimientos de recuperación y contingencia por escenario (paso a paso, con responsable por actividad)
8. Centro de control / sitio alterno de operaciones
9. Actividades de manejo de crisis y comunicación
10. Actividades de mantenimiento y prueba del DRP (periodicidad, responsables)
11. Distribución del documento y control de cambios

**Componentes que deben tener RTO/RPO justificado** (mínimo): ERP/BD transaccional; Portal de
Clientes / Portal de Proveedores; Correo corporativo; Enlace VPN entre sedes; Sistema de
Rastreo de Flotilla; Infraestructura de red (firewall, switch core).

**Los 8 escenarios de la sección 6.3** (mínimo **3 desarrollados paso a paso**):
1. No disponibilidad del centro de datos (incendio, inundación, falla de A/C, corte eléctrico prolongado)
2. Falla o compromiso del firewall perimetral único
3. Caída del enlace VPN entre sedes
4. Incidente de ciberseguridad en la DMZ (con movimiento lateral hacia la BD interna)
5. Ransomware con cifrado de servidores de archivos y/o ERP
6. Pérdida o corrupción de respaldos
7. Eventos del contexto guatemalteco: sismos, tormentas tropicales, inundaciones estacionales
8. Interrupción prolongada del ISP único

**Debe definirse explícitamente** qué rol tiene autoridad para activar el DRP y bajo qué criterios.

**Sitio alterno**: TransAgro NO tiene datacenter alterno. Hay que **proponer y justificar** una
estrategia (frío/tibio/caliente, nube pública, o reciprocidad Casa Matriz↔Planta) y
**conectarla con el presupuesto de la Fase 4**.

### 5.4 Fase 4 — Plan de adquisición
- Propuesta ordenada **por prioridad** (crítico / alto / medio), separando **CAPEX** de **OPEX**.
- **Obligatorio: validar y actualizar al menos TRES referencias de precio** mediante cotización
  o investigación directa con proveedor/distribuidor autorizado en Guatemala o la región,
  **citando la fuente** (captura de pantalla, enlace o constancia de contacto).
- Marcas distintas a las del enunciado son válidas **si se justifica técnicamente**
  (throughput, número de usuarios, presupuesto, soporte local).
- **Debe incluir componente de talento humano** (contratación directa, MDR/SOC tercerizado o mixto).
- Tabla resumen consolidada por dominio: Dominio | Prioridad | CAPEX | OPEX anual | Responsable.
- **Propuesta de fases de implementación** (qué se adquiere primero y por qué, según nivel de riesgo).

### 5.5 Entrega final
- Documento consolidado en **Word (.docx) Y PDF**, portada institucional única
  (logo UMG, curso, integrantes, docente, fecha), con los 4 planes como capítulos/anexos.
- **Presentación PowerPoint, máximo 20 diapositivas**, orientada a dirección/gerencia.
- **Diagrama de topología actual y propuesta — obligatoriamente en Cisco Packet Tracer.**
- Formato: carta, márgenes 1", **Calibri o Arial 11 pt**, interlineado **1.15**.
- Portada, índice, numeración de página y encabezado institucional en todos los documentos.
- Tablas, diagramas y cifras **tituladas y citadas** (APA 7ª ed. salvo indicación del docente).
- Prohibido copiar literalmente las plantillas de referencia. IA permitida como apoyo
  **siempre que el contenido final sea revisado, comprendido y defendido por el grupo**.

---

## 6. Los 9 dominios mínimos del checklist (Fase 1, sección 4.2)

| # | Dominio | Aspectos mínimos a verificar |
|---|---|---|
| 1 | Seguridad perimetral y DMZ | WAF, Anti-DDoS, protección/filtrado DNS, segmentación DMZ↔interna, arquitectura de firewall (SPOF vs HA) |
| 2 | Comunicaciones | Vigencia y robustez criptográfica de VPN sitio a sitio, redundancia de enlaces (ISP/SD-WAN), cifrado entre sedes |
| 3 | Identidad y control de acceso | MFA/2FA, política de contraseñas, gestión de cuentas privilegiadas, revisión periódica de accesos |
| 4 | Red interna | Segmentación VLAN, NAC, seguridad inalámbrica, aislamiento IoT/OT |
| 5 | Endpoints y sistemas | Vigencia de SO, gestión centralizada de parches, antimalware/EDR, cifrado de discos |
| 6 | Datacenter y seguridad física | Control de acceso físico, videovigilancia, monitoreo ambiental, energía de respaldo (UPS/planta) |
| 7 | Datos y continuidad | Política y prueba de respaldos, copia offsite, cifrado de respaldos, retención documentada |
| 8 | Monitoreo y respuesta a incidentes | Centralización de logs (SIEM), gestión de vulnerabilidades, plan de respuesta a incidentes y responsable designado |
| 9 | Personal y proveedores | Concientización y capacitación, gestión de accesos de terceros, cláusulas de seguridad en contratos |

---

## 7. Roles del grupo

| Rol | Responsabilidad |
|---|---|
| Líder de proyecto / Coordinador | Coordina avances, cronograma interno, consolida documentos finales |
| Analista de riesgos | Lidera Fase 1: adaptación del checklist, aplicación y matriz de riesgos |
| Especialista en seguridad perimetral y de aplicaciones | Controles de DMZ, WAF, anti-DDoS, protección DNS, firewall en HA |
| Especialista en redes internas e identidad | Segmentación VLAN/NAC, MFA/2FA, política de contraseñas |
| Especialista en continuidad de negocio | Lidera Fase 3 (DRP): escenarios, RTO/RPO, roles, árbol de llamadas |
| Especialista en adquisiciones e infraestructura | Lidera Fase 4: soluciones, marcas, arquitecturas, proveedores, presupuesto |
| Redactor técnico / Editor | Unifica formato, redacción y coherencia de los 4 documentos |

### Rol del propietario de este repositorio
**Fase 2 — Especialista en seguridad perimetral/DMZ y en redes internas e identidad**,
más **auditor de calidad transversal**: verificar que las fases 1, 3 y 4 de los compañeros
cumplan exactamente lo exigido en el enunciado, usando
[`auditoria/CHECKLIST-CUMPLIMIENTO.md`](auditoria/CHECKLIST-CUMPLIMIENTO.md).

---

## 8. Estructura del repositorio

```
.
├── CLAUDE.md                        ← este archivo (memoria del proyecto)
├── README.md                        ← guía de uso del repo para el grupo
├── 00-guia/
│   └── Proyecto No.md               ← enunciado del docente (INMUTABLE)
├── 01-fase1-diagnostico/
│   └── Fase 1 Proyecto Tele 1.md    ← entregable del grupo
├── 02-fase2-plan-seguridad/
├── 03-fase3-drp/
├── 04-fase4-adquisicion/
├── 05-entrega-final/
├── auditoria/
│   ├── CHECKLIST-CUMPLIMIENTO.md    ← checklist paralelo maestro (marcar avance aquí)
│   ├── matriz-trazabilidad.md       ← D-nn → R-nn → C-nn → E-nn → I-nn
│   └── fase1-hallazgos-auditoria.md ← gaps detectados en la Fase 1 entregada
└── referencias/
    └── fuentes-oficiales.md         ← fuentes citables verificadas, con fecha de consulta
```

---

## 9. Datos técnicos verificados (usar en los documentos, con cita)

Fechas y estados confirmados contra fuente oficial — detalle y URLs en
[`referencias/fuentes-oficiales.md`](referencias/fuentes-oficiales.md).

| Dato | Valor verificado | Relevancia |
|---|---|---|
| Windows Server 2012 R2 | Fin de soporte extendido: **10 de octubre de 2023** | D-10 |
| Windows 8.1 | Fin de soporte: **10 de enero de 2023** | D-10 |
| Windows 7 | Fin de soporte extendido: **14 de enero de 2020** | D-10 |
| IKEv1 | **Deprecado formalmente por IETF RFC 9395 (2023)**; RFC 2407/2408/2409 pasaron a *Historic* | D-03 |
| SHA-1 | NIST lo retira; prohibido en aplicaciones nuevas, eliminación total al **31 dic 2030** | D-03 |
| 3DES / TDEA | NIST SP 800-131A Rev. 2 establece calendario de retiro del TDEA | D-03 |
| ISO/IEC 27001:2022 Anexo A | **93 controles** en **4 temas**: organizacionales (37), personas (8), físicos (14), tecnológicos (34) | Marco Fase 1-2 |
| NIST CSF 2.0 | **6 funciones**: Govern, Identify, Protect, Detect, Respond, Recover | Marco Fase 1-2 |
| CIS Controls v8.1 | **18 controles**, **153 salvaguardas**, 3 grupos de implementación (IG1=56, IG2=+74, IG3=+23) | Marco Fase 1 |

> **Nota de dimensionamiento**: para IG (Implementation Group) de CIS, TransAgro con ~480
> colaboradores, datos de terceros (clientes, proveedores, ubicación GPS) y operación OT
> corresponde razonablemente a **IG2**. Justificar esta elección en el documento.

---

## 10. Supuestos documentados

El enunciado permite —y exige— documentar supuestos razonables cuando el caso no detalle un
aspecto. **Todo supuesto adoptado debe registrarse aquí y en el documento donde se use.**

| ID | Supuesto | Justificación | Fase donde se usa |
|---|---|---|---|
| S-01 | Nivel de aplicación del checklist = **CIS Controls v8.1 IG2** | ~480 colaboradores, custodia de datos de terceros (clientes, proveedores, GPS de flotilla) y operación OT (PLC). Supera IG1; no requiere IG3. Sustento: guía de grupos de implementación de CIS (2024) | Fase 1 (§1.1 del entregable); marco para Fases 2 y 4 |
| S-02 | Umbral de referencia para retención de CCTV del datacenter = **30 días** | El caso no fija un valor; 30 días es la práctica habitual para investigación de incidentes físicos y es el mínimo que suelen exigir marcos de cumplimiento. Se usa solo como criterio de la pregunta de auditoría, no como hallazgo | Fase 1 (checklist ítem 6.2) |
| S-03 | Config. destino de la VPN entre sedes: **IKEv2 + AES-256-GCM + SHA-2**, grupo DH 19/20, PFS habilitado | Derivado de RFC 9395, retiro de SHA-1 (NIST 2022) y NIST SP 800-131A Rev. 2. El caso no especifica grupo DH ni PFS actuales | Fase 1 (ítem 2.2, control de R-08); se detalla en Fase 2 y Fase 4 |
| S-04 | Escala de tratamiento por nivel de riesgo: CRÍTICO = acción inmediata + escalamiento; ALTO ≤ 3 meses; MEDIO ≤ 12 meses; BAJO aceptar y monitorear | El enunciado pide clasificar en Bajo/Medio/Alto/Crítico pero no fija plazos de tratamiento; se adopta una convención estándar y defendible | Fase 1 (§2.3 del entregable); coherencia con priorización de Fase 4 |

---

## 11. Reglas de trabajo para agentes de IA en este repo

1. **No inventar datos del caso.** Los hechos de TransAgro son solo los de la sección 2 del
   enunciado. Lo que no esté ahí es un **supuesto** y va a la tabla §10.
2. **No modificar** `00-guia/Proyecto No.md`. Es el enunciado original.
3. **Citar siempre la fuente** de cualquier dato técnico, precio o marco normativo, con fecha
   de consulta. Preferir fuente oficial del fabricante o del organismo normativo.
4. **Mantener trazabilidad**: cualquier control nuevo debe declarar a qué `D-nn` responde.
5. **Actualizar** `auditoria/CHECKLIST-CUMPLIMIENTO.md` al completar cualquier ítem.
6. **No copiar literalmente** las plantillas de referencia del docente: adaptar al caso.
7. Los precios del enunciado son **referenciales y didácticos**; para la Fase 4 hay que
   verificarlos contra fuente actual y citar.
8. Escribir en **español de Guatemala**, registro técnico profesional, evitando anglicismos
   innecesarios (pero conservando los términos técnicos estándar: WAF, DMZ, EDR, SIEM…).
