# Proyecto No. 01 — Seguridad de Redes
### TransAgro del Oriente, S.A.

Universidad Mariano Gálvez de Guatemala · Facultad de Ingeniería en Sistemas de Información
Campus Jutiapa · Curso: Telecomunicaciones · Segundo Semestre 2026
Docente: Ing. Juan Daniel Ramos Martínez

---

## Qué es este repositorio

Espacio de trabajo compartido del grupo para las **cuatro fases** del proyecto, con control de
versiones y un mecanismo de verificación de cumplimiento contra el enunciado del docente.

---

## Por dónde empezar

| Si eres… | Lee primero |
|---|---|
| **Nuevo en el proyecto** | [`CLAUDE.md`](CLAUDE.md) — resumen completo del caso y de lo que se exige |
| **Responsable de una fase** | [`auditoria/CHECKLIST-CUMPLIMIENTO.md`](auditoria/CHECKLIST-CUMPLIMIENTO.md) — tu lista de tareas verificables |
| **Redactando un documento** | [`referencias/fuentes-oficiales.md`](referencias/fuentes-oficiales.md) — citas ya verificadas, listas para usar |
| **Revisando el trabajo de otro** | [`auditoria/matriz-trazabilidad.md`](auditoria/matriz-trazabilidad.md) — verifica que la cadena D→R→C→E→I esté completa |

---

## Estructura

```
├── CLAUDE.md                          Memoria del proyecto: el caso, los requisitos, las reglas
├── README.md                          Este archivo
│
├── 00-guia/
│   └── Proyecto No.md                 ⚠️ Enunciado del docente — NO MODIFICAR
│
├── 01-fase1-diagnostico/              Fase 1 — Checklist + matriz de riesgos     (20 pts)
├── 02-fase2-plan-seguridad/           Fase 2 — Plan de Seguridad Informática     (20 pts)
├── 03-fase3-drp/                      Fase 3 — Plan de Recuperación ante Desastres (20 pts)
├── 04-fase4-adquisicion/              Fase 4 — Plan de adquisición e implementación (20 pts)
├── 05-entrega-final/                  Documento consolidado, PPT y diagramas
│
├── auditoria/
│   ├── CHECKLIST-CUMPLIMIENTO.md      ✅ Checklist maestro — marcar avance aquí
│   ├── matriz-trazabilidad.md         🔗 Cadena D→R→C→E→I
│   └── fase1-hallazgos-auditoria.md   🔍 Brechas detectadas en la Fase 1
│
└── referencias/
    └── fuentes-oficiales.md           📚 Fuentes verificadas con cita APA 7
```

---

## Estado actual

| Fase | Responsable | Estado | Cumplimiento |
|---|---|---|---|
| Fase 1 — Diagnóstico | *(asignar)* | Entregada, **con brechas** | ~28 % |
| Fase 2 — Plan de Seguridad | Sergio Godoy | No iniciada | 0 % |
| Fase 3 — DRP | *(asignar)* | No iniciada | 0 % |
| Fase 4 — Adquisición | *(asignar)* | No iniciada | 0 % |
| Entrega final | *(asignar)* | No iniciada | 0 % |

> 📋 Detalle en [`auditoria/CHECKLIST-CUMPLIMIENTO.md`](auditoria/CHECKLIST-CUMPLIMIENTO.md)

### Atención inmediata — Fase 1

Cinco correcciones de **menos de 2 horas en total** que suben el cumplimiento de ~28 % a ~55 %:

1. La conclusión ejecutiva lista **6 riesgos**; el enunciado pide **exactamente 5**
2. Corregir ortografía: "TransA**g**ro" (aparece como "TransAro") y "Fase **1**" (aparece "Fase l")
3. Publicar las escalas de probabilidad e impacto y la regla P×I → nivel de riesgo
4. Agregar sección de referencias en APA 7 — las fuentes ya están verificadas en el repo
5. Añadir IDs de trazabilidad a la columna "Control propuesto (Fase 2)"

Después, lo de fondo: **ampliar el checklist de 10 a 60–80 ítems** para cubrir los 9 dominios
obligatorios, y cubrir las 4 debilidades sin diagnóstico (WiFi, NAC, EDR, acceso físico).

> 🔍 Detalle completo en [`auditoria/fase1-hallazgos-auditoria.md`](auditoria/fase1-hallazgos-auditoria.md)

---

## Reglas de trabajo

### La regla que más pesa: trazabilidad

El enunciado (§1.4) exige que **cada debilidad del caso** esté cubierta por:
- al menos **una medida** en la Fase 2,
- **un procedimiento** de continuidad en la Fase 3,
- y —cuando aplique— **un rubro de inversión** en la Fase 4.

Por eso usamos identificadores. Al escribir cualquier control, escenario o rubro, **declara a
qué debilidad responde**:

```
D-nn  Debilidad del caso (§2.4)     →  las 17 están listadas en CLAUDE.md §3.4
R-nn  Riesgo (Fase 1)
C-nn  Control / medida (Fase 2)
E-nn  Escenario de desastre (Fase 3)
I-nn  Rubro de inversión (Fase 4)
```

Ejemplo: *"**C-08** Segmentación de la red en VLAN por función — responde a **D-07** y **D-09**;
mitiga **R-03**; soporta **E-05**; requiere **I-09**."*

### Otras reglas

1. **No modificar** `00-guia/Proyecto No.md`. Es el enunciado original.
2. **No inventar datos del caso.** Los hechos de TransAgro son solo los de §2 del enunciado.
   Lo que no esté ahí es un **supuesto** y se registra en `CLAUDE.md` §10.
3. **Citar todo dato técnico o precio** con fuente y fecha de consulta.
4. **Actualizar el checklist** al completar cualquier ítem.
5. **No copiar literalmente** las plantillas del docente — hay que adaptarlas al caso (§8.3).
6. Escribir en español, registro técnico profesional.

---

## Formato de los entregables (§8.3) — no negociable

- Papel **carta**, márgenes de **1 pulgada**
- Fuente **Calibri o Arial 11 pt**, interlineado **1.15**
- Portada, índice, numeración de página y encabezado institucional en **todos** los documentos
- Portada institucional con **logo UMG**
- Citas en **APA 7ª edición**
- Entrega final en **Word (.docx) y PDF**
- Presentación PowerPoint de **máximo 20 diapositivas**
- Diagramas de topología (actual y propuesta) **obligatoriamente en Cisco Packet Tracer**

---

## Flujo de trabajo con Git

```bash
# Antes de empezar a trabajar, traer los cambios de los demás
git pull

# Trabajar en tu fase, luego:
git add .
git commit -m "fase2: agrega políticas de seguridad en redes (C-01 a C-06)"
git push
```

**Convención de mensajes de commit**: `fase<n>: <qué cambió>`

Ejemplos:
```
fase1: corrige conclusión ejecutiva a 5 riesgos (H-04)
fase2: agrega bloque de identificación y control de acceso
fase3: define RTO/RPO de ERP y portales con justificación
fase4: verifica precio de Cloudflare WAF (cotización 1 de 3)
auditoria: actualiza checklist tras revisión de Fase 3
```

---

## Rúbrica (§9)

| Criterio | Puntos |
|---|---|
| Fase 1 — Diagnóstico de riesgos | 20 |
| Fase 2 — Plan de Seguridad Informática | 20 |
| Fase 3 — Plan de Recuperación ante Desastres | 20 |
| Fase 4 — Plan de adquisición e implementación | 20 |
| Integración, redacción y formato | 10 |
| Defensa oral | 10 |
| **TOTAL** | **100** |

---

## Nota sobre el uso de IA

El enunciado (§8.3) permite usar herramientas de IA como apoyo de redacción e investigación,
**siempre que el contenido final sea revisado, comprendido y defendido por el propio grupo**.

En la defensa oral (§8.2) cada integrante debe poder **justificar cada decisión técnica y cada
rubro de inversión**. Lo que no entiendas, no lo entregues.
