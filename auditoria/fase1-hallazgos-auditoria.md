# Auditoría de la Fase 1 entregada — Informe de brechas

**Documento auditado (auditoría original)**: `01-fase1-diagnostico/Fase 1 Proyecto Tele 1.md` (versión de 10 ítems, ya reemplazada)
**Documento vigente**: [`01-fase1-diagnostico/Fase 1, Diagnóstico de riesgos tecnológicos.md`](../01-fase1-diagnostico/Fase%201,%20Diagn%C3%B3stico%20de%20riesgos%20tecnol%C3%B3gicos.md)
**Criterio de auditoría**: enunciado §4.1–§4.4 y rúbrica §9 (Fase 1 = 20 puntos)
**Fecha auditoría original**: 2026-09-05 · **Fecha revisión**: 2026-09-07
**Alcance**: verificación de cumplimiento

---

## 0. Estado de resolución (2026-09-07)

La auditoría original (§1–§5 de este documento) evaluó una versión anterior del entregable
—"Fase 1 Proyecto Tele 1.md", 10 ítems de checklist—. Esa versión fue **reemplazada** por
"Fase 1, Diagnóstico de riesgos tecnológicos.md". Sobre ese documento vigente se aplicaron las
decisiones B-1 a B-9 (ver §6). Correspondencia con los hallazgos originales:

| Hallazgo original | Tema | Estado | Cómo se resolvió |
|---|---|---|---|
| **H-01** | Checklist de 10 ítems para ~36 aspectos | ✅ Resuelto | Ampliado a **43 ítems**, 4–7 por dominio, cada aspecto de §4.2 con ítem propio |
| **H-02** | Dominio "Personal y proveedores" ausente | ✅ Resuelto | Dominio 9 con 6 ítems (9.1–9.6), incluye SPF/DKIM/DMARC y cláusulas contractuales |
| **H-03** | D-08, D-09, D-11, D-12 sin cobertura | ✅ Resuelto | 4.3 (WiFi/D-08), 4.2 (NAC/D-09), 5.3–5.4 (EDR e inventario/D-11), 6.1–6.3 (físico y ambiental/D-12); R-03, R-10 en la matriz |
| **H-04** | Conclusión ejecutiva con 6 (luego 8) riesgos | ✅ Resuelto | Exactamente **5**, los de mayor P×I: R-01(25), R-03(20), R-04(20), R-02(20), R-05(15) |
| **H-05** | Regla P×I → nivel no declarada + inconsistencia VPN | ✅ Resuelto | §2.1–§2.3: escalas de P e I y regla **CRÍTICO 20-25 / ALTO 12-19 / MEDIO 6-11 / BAJO 1-5**. R-08 (VPN, 12) reclasificado a **ALTO** |
| **H-06** | Referencias mencionadas pero no citadas | ✅ Resuelto | §4 Referencias en APA 7 (11 entradas); edición declarada: ISO/IEC 27001**:2022**, CIS Controls **v8.1** |
| **H-07** | Columna de control sin IDs de trazabilidad | ✅ Resuelto | Checklist con columna `D-nn`; matriz con `R-01…R-10`, `Debilidades (D-nn)`, `Ítem(s) del checklist`; §2.5 mapeo D→R de las 17 debilidades |
| **H-08** | Ortografía; "TransAro"; "Fase l" en encabezado | ✅ Resuelto | Texto reescrito; nombre correcto "TransAgro"; bloque de identificación institucional al inicio |
| **H-09** | Checklist 100 % "NO" | ✅ Resuelto | Respuestas **SÍ** reales en 1.1 (DMZ), 2.1 (VPN), 7.1 (respaldos), con observación "existe pero…"; §1.2 define el criterio de cada valor |
| **H-10** | Sin diagrama de topología | ⬜ Pendiente | No es entregable formal de Fase 1 (§4.4). Obligatorio en §8.1 (Packet Tracer); insumo de la Fase 2 |
| **H-11** | Tablas Markdown colapsadas por conversión | ✅ Resuelto | Checklist y matriz reconstruidos en Markdown válido |
| **H-12** | Falta encabezado institucional | 🔶 Parcial | Bloque textual de identificación agregado al `.md`. Falta completar integrantes/fecha y trasladar a portada con logo UMG e índice en el `.docx` |

**Extra no señalado en la auditoría original y también corregido:**

- **B-6** — El Dominio 3 citaba numeración ISO 2013 (`A.9.2`, `A.9.4`). Toda la numeración ISO
  del documento se unificó a la edición **2022** (control de acceso → A.5.15–A.5.18, A.8.2–A.8.5;
  proveedores → A.5.19–A.5.21; físico → A.7.2–A.7.11; malware → A.8.7).
- **B-6** — Se declara "CIS Controls **v8.1**" (antes "v8") y se agrega **§1.1** justificando el
  grupo de implementación **IG2** para TransAgro (~480 colaboradores, datos de terceros, OT).
- **B-10** — Se agregaron **R-09** (autonomía energética / D-13) y **R-10** (acceso físico y
  ambiental / D-12) para que las 17 debilidades tengan riesgo asociado.

**Estimación de cumplimiento tras la revisión: ~78 %** (contenido del diagnóstico completo;
pendiente solo portada/índice del `.docx` y topología en Packet Tracer). Ver
[`CHECKLIST-CUMPLIMIENTO.md`](CHECKLIST-CUMPLIMIENTO.md) §Fase 1.

---

> ⚠️ **Lo que sigue (§1–§5) es la auditoría original del 2026-09-05**, conservada como
> registro histórico. Se refiere a la versión de 10 ítems ya reemplazada. Para el estado
> actual, ver §0 arriba.

---

## 1. Veredicto

El entregable **tiene una base conceptual correcta** —el enfoque, la redacción ejecutiva y la
lógica de riesgo son sólidos— pero **no cumple la cobertura exigida** por §4.2 ni la
especificación literal de §4.4.

| Componente | Peso relativo | Estado | Riesgo de pérdida de puntos |
|---|---|---|---|
| Checklist adaptado | Alto | Incompleto | **Alto** |
| Aplicación al caso | Alto | Parcial | **Alto** |
| Matriz de riesgos | Alto | Buena, con defectos formales | Medio |
| Conclusión ejecutiva | Medio | Incumple especificación numérica | Medio |

**Estimación de cumplimiento actual: ~28 %** de los ítems verificables de la Fase 1.

---

## 2. Hallazgos por severidad

### 🔴 CRÍTICO

#### H-01 — El checklist cubre 10 ítems para 9 dominios y ~36 aspectos mínimos

El enunciado §4.2 fija **9 dominios** y, dentro de cada uno, una lista de **aspectos mínimos a
verificar**. Sumados dan aproximadamente **36 aspectos**. El entregable tiene **10 preguntas**.

Cobertura real por dominio:

| Dominio (§4.2) | Aspectos exigidos | Cubiertos | Faltantes |
|---|---|---|---|
| 1. Seguridad perimetral y DMZ | WAF · Anti-DDoS · filtrado DNS · segmentación DMZ↔interna · firewall SPOF/HA | 2 | **Anti-DDoS, filtrado DNS, segmentación DMZ** |
| 2. Comunicaciones | robustez cripto VPN · redundancia de enlaces · cifrado entre sedes | 2 | Cifrado entre sedes (tratado indirectamente) |
| 3. Identidad y control de acceso | MFA/2FA · política de contraseñas · cuentas privilegiadas · revisión periódica de accesos | 1 | **Política de contraseñas, cuentas privilegiadas, revisión de accesos** |
| 4. Red interna | VLAN · NAC · seguridad inalámbrica · aislamiento IoT/OT | 1 | **NAC, WiFi, aislamiento OT** |
| 5. Endpoints y sistemas | vigencia SO · parches centralizados · antimalware/EDR · cifrado de discos | 1 | **EDR, inventario de activos, cifrado de discos** |
| 6. Datacenter y físico | control de acceso físico · videovigilancia · monitoreo ambiental · energía | 1 | **Acceso físico, CCTV, monitoreo ambiental** |
| 7. Datos y continuidad | política y prueba de respaldos · offsite · cifrado de respaldos · retención | 1 | **Pruebas de restauración, cifrado/inmutabilidad, retención** |
| 8. Monitoreo y respuesta | SIEM · gestión de vulnerabilidades · plan de respuesta · responsable designado | 1 | **Gestión de vulnerabilidades/pentesting, responsable designado** |
| 9. Personal y proveedores | concientización · accesos de terceros · cláusulas contractuales | **0** | **El dominio completo** |

**Impacto**: la rúbrica evalúa "exhaustividad en la aplicación al caso". Con 10 de ~36 aspectos,
este criterio se cumple parcialmente.

**Corrección**: ampliar el checklist a **60–80 ítems**. La regla práctica es 5–10 preguntas por
dominio, de modo que cada aspecto mínimo de §4.2 tenga al menos una pregunta propia.

---

#### H-02 — El dominio "Personal y proveedores" no existe en el checklist

Es uno de los **9 dominios obligatorios** de §4.2. En el entregable aparece únicamente como
riesgo en la matriz ("Acceso no monitoreado de proveedores externos"), pero **sin ningún ítem
de verificación que lo respalde**.

Esto rompe la lógica del instrumento: la matriz de riesgos debe derivarse del checklist
(§4.3, "con base en los hallazgos del checklist"). Un riesgo sin hallazgo que lo origine es
un riesgo sin evidencia de auditoría.

**Corrección**: agregar un bloque de dominio con al menos estas preguntas:
- ¿Existe un programa formal y documentado de concientización en ciberseguridad? *(D-15)*
- ¿Los accesos remotos de proveedores son temporales y se revocan al finalizar la actividad? *(D-17)*
- ¿Cada proveedor cuenta con credenciales individuales y nominadas? *(D-17)*
- ¿Se monitorean y registran las sesiones de acceso de terceros? *(D-17)*
- ¿Los contratos con proveedores incluyen cláusulas de seguridad de la información y NDA? *(D-17)*
- ¿Se rotan las credenciales entregadas a consultores externos? *(D-17)*

---

#### H-03 — Cuatro debilidades del caso no tienen cobertura en ningún entregable

El enunciado §2.4 lista 17 debilidades y §1.4 exige trazabilidad. Estas quedaron fuera tanto
del checklist como de la matriz:

| ID | Debilidad no cubierta | Dónde debía aparecer |
|---|---|---|
| **D-08** | WiFi corporativa con una sola clave WPA2-Personal compartida con personal y visitantes; sin red de invitados ni portal cautivo | Checklist dominio 4 + matriz |
| **D-09** | Sin NAC: cualquier dispositivo conectado obtiene IP y acceso a recursos internos | Checklist dominio 4 + matriz |
| **D-11** | Antivirus de firmas desactualizado, sin EDR y sin inventario confiable de activos | Checklist dominio 5 + matriz |
| **D-12** | Sala de servidores sin control biométrico/tarjeta, CCTV parcial, sin monitoreo ambiental | Checklist dominio 6 + matriz |

Nota sobre D-12: el checklist sí pregunta por controles ambientales, pero la observación
responde solo sobre el UPS (que es D-13). **El control de acceso físico y la videovigilancia
quedan sin evaluar.**

**Impacto**: si estas debilidades no se diagnostican en la Fase 1, la Fase 2 no tendrá de dónde
derivar las medidas de NAC, WiFi Enterprise, EDR y seguridad física — y se rompe la cadena de
trazabilidad que el enunciado exige explícitamente.

---

#### H-04 — La conclusión ejecutiva lista SEIS riesgos; el enunciado pide CINCO

§4.4 dice literalmente: *"Conclusión ejecutiva de una página con los **cinco** riesgos más
críticos identificados."*

El documento presenta seis viñetas:
1. Exposición directa de la información financiera y operativa (DMZ sin WAF)
2. Riesgo de paralización por punto único de falla
3. Vulnerabilidad ante infecciones de rápida propagación (red plana)
4. Imposibilidad de recuperación efectiva (respaldos)
5. Ausencia total de detección y respuesta ante incidentes
6. **Accesos de terceros sin control** ← excedente

Además, hay una **inconsistencia con la matriz**: el riesgo #6 está calificado **ALTO** (4×4),
no CRÍTICO, mientras que "Suplantación de identidad (phishing)" también es ALTO y no aparece.
El criterio de selección no es evidente.

**Corrección**: dejar exactamente cinco, y que sean **los cinco de mayor puntaje P×I de la
matriz**, ordenados de mayor a menor. Con los puntajes actuales:

| Orden | Riesgo | P×I | Nivel |
|---|---|---|---|
| 1 | Compromiso de bases de datos por vulnerabilidades web | 5×5 = **25** | CRÍTICO |
| 2 | Propagación masiva de malware/ransomware (red plana) | 5×4 = **20** | CRÍTICO |
| 3 | Ceguera operativa ante incidentes (sin SIEM/IRP) | 5×4 = **20** | CRÍTICO |
| 4 | Caída total operativa por fallo de equipo de borde | 4×5 = **20** | CRÍTICO |
| 5 | Pérdida irrecuperable de datos por desastre físico | 3×5 = **15** | ALTO |

Los cuatro CRÍTICOS entran por definición; el quinto lugar se disputa entre "Pérdida
irrecuperable de datos" (15), "Accesos de proveedores" (16) y "Phishing" (16).
**Esto obliga a resolver primero H-05.**

---

### 🟠 ALTO

#### H-05 — No se declara la regla de conversión P×I → nivel de riesgo, y hay una inconsistencia

La matriz asigna niveles (Crítico/Alto/Medio) sin publicar **la escala que los produce**. Sin
esa regla, la calificación no es auditable ni defendible ante el docente. Y al reconstruirla,
aparece una contradicción:

| Riesgo | P | I | P×I | Nivel asignado | ¿Consistente? |
|---|---|---|---|---|---|
| Compromiso de BD por vulnerabilidades web | 5 | 5 | 25 | CRÍTICO | ✔ |
| Caída total por fallo de equipo de borde | 4 | 5 | 20 | CRÍTICO | ✔ |
| Propagación masiva de malware/ransomware | 5 | 4 | 20 | CRÍTICO | ✔ |
| Ceguera operativa ante incidentes | 5 | 4 | 20 | CRÍTICO | ✔ |
| Acceso no monitoreado de proveedores | 4 | 4 | 16 | ALTO | ✔ |
| Suplantación de identidad (phishing) | 4 | 4 | 16 | ALTO | ✔ |
| Pérdida irrecuperable de datos por desastre físico | 3 | 5 | 15 | ALTO | ✔ |
| **Interceptación de datos en tránsito (VPN)** | **4** | **3** | **12** | **MEDIO** | ⚠ frontera sin regla |

Los siete primeros son consistentes con un corte del tipo *Crítico ≥ 20 · Alto 12–19 ·
Medio 6–11 · Bajo ≤ 5*… pero con **ese** corte, el riesgo de VPN (12) sería **ALTO**, no MEDIO.
Con un corte alternativo *Alto 15–19 · Medio 10–14*, el 12 sí es MEDIO y todo cierra.

**No es que el número esté mal: es que sin la regla publicada, la clasificación queda expuesta
a que el docente aplique la suya y encuentre inconsistencia.**

**Corrección**: agregar antes de la matriz una tabla de criterio, por ejemplo:

| Nivel | Rango P×I | Criterio de tratamiento |
|---|---|---|
| CRÍTICO | 20 – 25 | Mitigación inmediata; escalamiento a Gerencia General |
| ALTO | 15 – 19 | Mitigación planificada en el corto plazo (≤ 3 meses) |
| MEDIO | 8 – 14 | Mitigación programada (≤ 12 meses) |
| BAJO | 1 – 7 | Aceptar y monitorear |

Y acompañarla con las **escalas de probabilidad e impacto** (qué significa 1, 2, 3, 4 y 5 en
cada eje), que tampoco están declaradas.

---

#### H-06 — Las referencias normativas se mencionan pero no se citan

El texto invoca "CIS Controls v8", "ISO/IEC 27001 A.8.26", "CIS Control 16", etc. Eso es
correcto y valioso, pero:

- **No se declara la edición** de ISO/IEC 27001 (¿2013 o 2022?). Importa: la numeración
  `A.8.26` corresponde a la **edición 2022**, cuyo Anexo A tiene 93 controles en 4 temas. Si el
  documento no lo dice, no se puede verificar.
- **No hay lista de referencias** ni bibliografía al final del entregable.
- §4.4 exige el checklist "con **fuente de referencia citada**"; §8.3 exige citación en
  **APA 7ª edición**.

**Corrección**: agregar una sección de referencias. Ver
[`referencias/fuentes-oficiales.md`](../referencias/fuentes-oficiales.md), que ya trae las
entradas verificadas y listas para copiar.

---

#### H-07 — La columna "Control propuesto (Fase 2)" no tiene identificadores de trazabilidad

La matriz sí propone controles, lo cual es correcto. Pero los enuncia en prosa, sin un ID que
permita seguirlos hacia la Fase 2. El enunciado §1.4 exige que *"cada debilidad detectada en la
Fase 1 esté cubierta por al menos una medida concreta en la Fase 2"* — y eso se verifica con
identificadores, no con párrafos.

**Corrección**: adoptar la convención de IDs del repositorio (`D-nn` → `R-nn` → `C-nn`),
documentada en [`CLAUDE.md §4`](../CLAUDE.md) y operativa en
[`matriz-trazabilidad.md`](matriz-trazabilidad.md).

---

### 🟡 MEDIO

#### H-08 — Errores de redacción y ortografía

| Ubicación | Error | Corrección |
|---|---|---|
| Párrafo introductorio | "el **instrumentó** de auditoria" | "el **instrumento** de auditoría" |
| Párrafo introductorio | "auditoria" (sin tilde) | "auditoría" |
| Párrafo introductorio | "debilidades **tecnologías**" | "debilidades **tecnológicas**" |
| Párrafo introductorio | "**TransAro** del Oriente" | "**TransAgro** del Oriente" |
| Encabezado de páginas | "Fase **l**" (ele minúscula) | "Fase **1**" |

El nombre mal escrito de la empresa y el "Fase l" recurrente son los más visibles: aparecen en
encabezado de página, es decir, en cada hoja del documento.

---

#### H-09 — Todas las respuestas del checklist son "NO"

Las 10 preguntas se responden NO. Es coherente con el caso —está diseñado con debilidades
deliberadas— pero un instrumento de auditoría **con 100 % de respuestas negativas y ninguna
N-A no demuestra que las columnas SÍ y N-A tengan uso real**.

Al ampliar el checklist (H-01) esto se resuelve solo, porque aparecen ítems donde:
- La respuesta es **SÍ**: existe firewall perimetral, existe DMZ separada de la red interna,
  existe VPN entre sedes, existe UPS, existe CCTV (parcial), se realizan respaldos.
- La respuesta es **N-A**: por ejemplo, controles específicos de nube pública, que TransAgro
  no utiliza salvo el SaaS de rastreo.

Eso hace el instrumento más creíble y demuestra criterio de auditor.

---

#### H-10 — Ausencia del diagrama de topología

§2.2 lo recomienda como parte del diagnóstico ("útil tanto para el checklist como para el plan
de seguridad y el DRP") y **§8.1 lo hace obligatorio en Cisco Packet Tracer**, tanto de la
topología actual como de la propuesta.

No es formalmente un entregable de la Fase 1 según §4.4, pero conviene levantar la **topología
actual** ahora: es insumo directo de la Fase 2 (diseño de VLAN y segmentación) y de la Fase 3
(escenarios de desastre).

---

### 🔵 BAJO / FORMA

#### H-11 — El formato de tabla no sobrevivió la conversión a Markdown

En el archivo `.md`, las tablas del checklist y de la matriz están colapsadas: varias columnas
quedaron fusionadas en una sola celda, con el texto entremezclado. El contenido está completo,
pero es ilegible como tabla.

Esto es un artefacto de la conversión desde Word y **probablemente no afecta el documento
original** que se entregará. Conviene confirmarlo, porque si el docente recibe el `.docx` con
las tablas así, sí pesa en el criterio de formato (10 pts).

#### H-12 — Falta encabezado institucional en el entregable parcial

§8.3 exige "portada, índice, numeración de página y encabezado institucional en **todos** los
documentos". Aplica también a los entregables de fase, no solo al consolidado final.

---

## 3. Plan de corrección priorizado

Ordenado por relación impacto/esfuerzo:

| Prioridad | Hallazgo | Acción | Esfuerzo |
|---|---|---|---|
| 1 | H-04 | Dejar exactamente 5 riesgos en la conclusión ejecutiva | 10 min |
| 2 | H-08 | Corregir ortografía, "TransAgro" y "Fase 1" en encabezado | 15 min |
| 3 | H-05 | Publicar escalas de P e I y la regla de conversión P×I → nivel | 30 min |
| 4 | H-06 | Agregar sección de referencias en APA 7 (fuentes ya verificadas) | 30 min |
| 5 | H-07 | Añadir columna de ID de trazabilidad (D-nn / R-nn / C-nn) | 30 min |
| 6 | H-02, H-03 | Agregar dominio "Personal y proveedores" y cubrir D-08, D-09, D-11, D-12 | 2 h |
| 7 | H-01 | Ampliar el checklist a 60–80 ítems cubriendo los 36 aspectos de §4.2 | 4–6 h |
| 8 | H-09 | Verificar que aparezcan respuestas SÍ y N-A al ampliar | incluido en 7 |
| 9 | H-10 | Levantar topología actual en Packet Tracer | 3 h |
| 10 | H-11, H-12 | Verificar formato del .docx y agregar encabezado institucional | 1 h |

**Ruta rápida**: los primeros cinco hallazgos se corrigen en **menos de 2 horas** y elevan el
cumplimiento de ~28 % a ~55 % sin reescribir el contenido sustantivo.

---

## 4. Lo que está bien hecho

Conviene decirlo con la misma precisión, porque **no debe tocarse al corregir**:

1. **La conclusión ejecutiva está bien escrita para su audiencia.** Traduce riesgo técnico a
   consecuencia de negocio sin jerga: *"un ciberdelincuente puede transitar desde la web
   pública hasta los registros internos del ERP"* es exactamente el registro que pide §8.2.
2. **El encadenamiento causal de los riesgos es correcto.** Que el compromiso de la DMZ derive
   en acceso al ERP no es una suposición: es consecuencia directa del hecho del caso de que las
   apps tienen conexión directa a la BD interna sin capa de servicios.
3. **El mapeo a CIS Controls e ISO 27001 es pertinente.** Los controles invocados corresponden
   razonablemente a cada hallazgo. Solo falta citarlos formalmente (H-06).
4. **La justificación separada de probabilidad e impacto** es metodológicamente correcta y es
   justo lo que §4.3 pide al exigir "justificando brevemente la calificación otorgada".
5. **La identificación de los cuatro riesgos críticos es acertada** y coincide con lo que un
   análisis independiente produce sobre este caso.

---

## 5. Estado de verificación

Este informe audita el documento **tal como está en el repositorio** a la fecha indicada.
Los hallazgos H-11 (formato de tablas) y H-12 (encabezado institucional) requieren
**verificar contra el archivo Word original**, que no está en el repositorio — es posible que
ya estén resueltos ahí.

Los hallazgos H-01 a H-10 son verificables directamente sobre el contenido y no dependen del
formato de origen.

---

## 6. Registro de cambios

| Fecha | Cambio |
|---|---|
| 2026-09-05 | Auditoría inicial de la Fase 1 entregada (versión de 10 ítems). Hallazgos H-01 a H-12 |
| 2026-09-07 | Revisión de la Fase 1 sobre el documento vigente. Decisiones B-1 a B-10 aplicadas. H-01 a H-09 y H-11 resueltos; H-12 parcial; H-10 pendiente. Estado de resolución en §0. Cumplimiento Fase 1: 28 % → ~78 % |
