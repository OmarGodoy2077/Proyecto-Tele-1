# Matriz de trazabilidad D → R → C → E → I

**Propósito**: dar cumplimiento a la exigencia de §1.4 del enunciado —
*"cada debilidad detectada en la Fase 1 debe estar cubierta por al menos una medida concreta en
la Fase 2, un procedimiento de continuidad en la Fase 3 y —cuando aplique— un rubro de
inversión en la Fase 4."*

Esta tabla es el **instrumento de verificación** de esa cadena. Se actualiza al cerrar cada fase.

**Última actualización**: 2026-09-07

---

## Convención de identificadores

| Prefijo | Significado | Fase | Fuente |
|---|---|---|---|
| `D-nn` | Debilidad del caso | Insumo | Enunciado §2.4 |
| `R-nn` | Riesgo de la matriz de riesgos | 1 | Matriz de riesgos del grupo |
| `C-nn` | Control / medida del Plan de Seguridad | 2 | Plan de Seguridad §6 |
| `E-nn` | Escenario de desastre del DRP | 3 | DRP §4 y §7 |
| `I-nn` | Rubro de inversión (CAPEX/OPEX) | 4 | Plan de adquisición §7.2–7.4 |

---

## Estado global de la cadena

| Métrica | Valor |
|---|---|
| Debilidades del caso (§2.4) | 17 |
| Con riesgo asignado en Fase 1 | **17 de 17 (100 %)** — Fase 1 revisada 2026-09-07 |
| Con control asignado en Fase 2 | 0 de 17 (0 %) |
| Con procedimiento en Fase 3 | 0 de 17 (0 %) |
| Con rubro de inversión en Fase 4 | 0 de 17 (0 %) |
| **Cadena completa D→R→C→E→I** | **0 de 17 (0 %)** |

---

## Matriz principal

Los `R-nn` reflejan la matriz de riesgos de la **Fase 1 revisada (2026-09-07)**.
Las columnas C, E e I se llenan conforme avancen las fases.

| ID | Debilidad (§2.4) | Fase 1 — Riesgo | Fase 2 — Control | Fase 3 — Escenario | Fase 4 — Inversión |
|---|---|---|---|---|---|
| **D-01** | 3 apps en DMZ sin WAF / Honeypot / Anti-DDoS / DNS Protection | `R-01` Compromiso de la BD interna por explotación de las apps web de la DMZ (**CRÍTICO**, 5×5=25) | *pendiente* | `E-04` | `I-` WAF, Anti-DDoS, DNS Security, Honeypot |
| **D-02** | Firewall perimetral único sin HA | `R-02` Caída total de conectividad de Casa Matriz y aislamiento de la Planta (**CRÍTICO**, 4×5=20) | *pendiente* | `E-02` | `I-` NGFW en clúster HA |
| **D-03** | VPN IPsec >6 años, IKEv1 + 3DES/SHA-1, sin respaldo | `R-08` Interceptación o descifrado del tráfico entre sedes (**ALTO**, 4×3=12) | *pendiente* | `E-03` | `I-` SD-WAN / reemplazo VPN a IKEv2/AES-256 |
| **D-04** | ISP único, sin redundancia ni balanceo | `R-02` (compartido con D-02) | *pendiente* | `E-08` | `I-` Segundo ISP |
| **D-05** | Sin 2FA/MFA en VPN, correo, dominio, consolas | `R-03` (facilitador de propagación), `R-07` Suplantación de identidad / phishing (**ALTO**, 4×4=16) | *pendiente* | `E-04`, `E-05` | `I-` MFA/2FA |
| **D-06** | Cuentas administrativas compartidas; política de contraseñas débil | `R-03` Propagación de malware/ransomware (**CRÍTICO**, 5×4=20) — como facilitador de movimiento lateral y acceso no auditable | *pendiente* | `E-04`, `E-05` | `I-` MFA + PAM |
| **D-07** | Red plana /16 sin VLAN ni ACL | `R-03` Propagación masiva de malware/ransomware (**CRÍTICO**, 5×4=20) | *pendiente* | `E-05` | `I-` Segmentación VLAN + switching |
| **D-08** | WiFi con clave WPA2-Personal única compartida | `R-03` (vector de entrada por dispositivo de visitante en red plana) | *pendiente* | `E-05` | `I-` WLAN segmentada 802.1X |
| **D-09** | Sin NAC | `R-03` (cualquier dispositivo conectado alcanza los recursos internos) | *pendiente* | `E-05` | `I-` NAC 802.1X |
| **D-10** | SO desactualizados (WS2012R2, Win7/8.1), sin gestión de parches | `R-03` (superficie de explotación sin parche) y `R-05` Pérdida irrecuperable de datos (**ALTO**, 3×5=15) | *pendiente* | `E-05` | `I-` Renovación SO + gestor de parches |
| **D-11** | Antivirus de firmas, sin EDR, sin inventario de activos | `R-03` (sin capacidad de detección ni contención en endpoint) | *pendiente* | `E-05` | `I-` EDR + inventario |
| **D-12** | Sala sin control biométrico/tarjeta, CCTV parcial, sin monitoreo ambiental | `R-10` Acceso físico no controlado y daño ambiental no detectado (**ALTO**, 3×4=12) | *pendiente* | `E-01` | `I-` Control de acceso + CCTV + sensores |
| **D-13** | UPS de solo 15 min, sin planta eléctrica | `R-09` Apagado abrupto y daño de equipos del datacenter (**ALTO**, 3×4=12) | *pendiente* | `E-01` | `I-` UPS ampliado + planta |
| **D-14** | Respaldos en cinta local, sin offsite, sin inmutabilidad, sin pruebas | `R-05` Pérdida irrecuperable de datos ante desastre físico o ransomware (**ALTO**, 3×5=15) | *pendiente* | `E-01`, `E-05`, `E-06` | `I-` Plataforma de respaldo 3-2-1 |
| **D-15** | Sin SPF/DKIM/DMARC; sin programa de concientización | `R-07` Suplantación de identidad / phishing (**ALTO**, 4×4=16) | *pendiente* | `E-05` | `I-` Concientización + filtrado de correo |
| **D-16** | Sin SIEM, sin gestión de vulnerabilidades, sin IRP, sin CSIRT/SOC | `R-04` Ceguera operativa ante incidentes (**CRÍTICO**, 5×4=20) | *pendiente* | Todos los escenarios | `I-` SIEM + NDR + talento humano SOC |
| **D-17** | Accesos remotos permanentes de proveedores, sin monitoreo ni cláusulas | `R-06` Acceso no monitoreado y persistente de proveedores externos (**ALTO**, 4×4=16) | *pendiente* | `E-04` | `I-` PAM / gestión de acceso de terceros |

> **Cambio de numeración respecto a la matriz de riesgos de la versión anterior de la Fase 1:**
> el riesgo de VPN pasó de `R-05` a **`R-08`** y de MEDIO a **ALTO** (regla P×I §2.3);
> "Pérdida irrecuperable de datos" pasó de `R-04` a **`R-05`**; "Ceguera operativa ante
> incidentes" pasó de `R-08` a **`R-04`**. Se agregaron **`R-09`** (energía / D-13) y
> **`R-10`** (físico y ambiental / D-12). Detalle en
> [`fase1-hallazgos-auditoria.md`](fase1-hallazgos-auditoria.md) §0.

---

## Brechas de cobertura de la Fase 1

### ✅ Resueltas en la revisión del 2026-09-07

Las 17 debilidades tienen ahora al menos un riesgo asociado (ver §2.5 del entregable de la
Fase 1). Las brechas que registraba la auditoría del 2026-09-05 se cerraron así:

| ID | Brecha anterior | Cómo se cerró |
|---|---|---|
| **D-06** | Sin riesgo propio | Vinculada explícitamente a `R-03` como facilitador de movimiento lateral y de acceso administrativo no auditable |
| **D-08** | Sin cobertura | Ítem de checklist 4.3 (WiFi Enterprise) + `R-03` como vector de entrada |
| **D-09** | Sin cobertura | Ítem 4.2 (NAC) + `R-03` |
| **D-10** | Cobertura parcial | Ítems 5.1, 5.2, 5.5 + `R-03` y `R-05` |
| **D-11** | Sin cobertura | Ítems 5.3 (EDR) y 5.4 (inventario) + `R-03` |
| **D-12** | Sin cobertura | Ítems 6.1–6.3 (acceso físico, CCTV, ambiental) + **`R-10`** nuevo |
| **D-13** | Cobertura parcial | Ítem 6.4 + **`R-09`** nuevo (antes se mezclaba con la pérdida de datos) |

---

## Verificación por correspondencias obligatorias del enunciado (§5.2)

El enunciado fija **nueve correspondencias literales** entre debilidad y sección del Plan de
Seguridad. Estas son de cumplimiento verificable y **no admiten interpretación**:

| # | Debilidad | Sección obligatoria de la Fase 2 | Estado |
|---|---|---|---|
| 1 | D-01 — DMZ sin WAF/Honeypot/Anti-DDoS/DNS | Seguridad en redes — control de publicación de servicios y protección de apps web | `[ ]` |
| 2 | D-02 — Firewall sin HA | Seguridad de operaciones — continuidad de servicios críticos de red (enlazado al DRP) | `[ ]` |
| 3 | D-03 — VPN antigua sobre red pública | Seguridad en redes — comunicaciones entre sedes | `[ ]` |
| 4 | D-05 — Sin 2FA en accesos internos | Identificación, autenticación y control de acceso | `[ ]` |
| 5 | D-07 — Red plana sin segmentación | Seguridad en redes — segmentación y control de acceso a la red | `[ ]` |
| 6 | D-12 — Datacenter sin protección perimetral física | Seguridad física y ambiental | `[ ]` |
| 7 | D-10 — SO desactualizados | Clasificación y control de bienes / Seguridad de operaciones (parches) | `[ ]` |
| 8 | D-17 — Accesos permanentes de proveedores | Gestión del personal y terceros | `[ ]` |
| 9 | D-16 — Sin SIEM ni plan de respuesta | Gestión de incidentes de seguridad | `[ ]` |

---

## Cobertura inversa: escenarios del DRP → debilidades

Verificación de que los 8 escenarios obligatorios de §6.3 tengan raíz en el diagnóstico:

| ID | Escenario (§6.3) | Debilidades que lo hacen probable o grave |
|---|---|---|
| `E-01` | No disponibilidad del centro de datos | D-12 (sin monitoreo ambiental), D-13 (UPS 15 min), D-14 (respaldos en el mismo cuarto) |
| `E-02` | Falla o compromiso del firewall perimetral único | D-02 (sin HA), D-04 (ISP único) |
| `E-03` | Caída del enlace VPN entre sedes | D-03 (sin enlace de respaldo ni SD-WAN) |
| `E-04` | Incidente en la DMZ con movimiento lateral | D-01 (sin WAF), D-07 (red plana), D-17 (accesos de terceros), D-05 (sin MFA) |
| `E-05` | Ransomware en servidores de archivos y/o ERP | D-07, D-10, D-11, D-14, D-15 |
| `E-06` | Pérdida o corrupción de respaldos | D-14 (sin offsite, sin inmutabilidad, sin pruebas) |
| `E-07` | Sismos, tormentas tropicales, inundaciones (contexto GT) | D-12, D-13, D-14 (sitio único sin alterno) |
| `E-08` | Interrupción prolongada del ISP único | D-04 (proveedor único, sin SLA) |

---

## Registro de cambios

| Fecha | Cambio |
|---|---|
| 2026-09-05 | Creación de la matriz; mapeo de la Fase 1 entregada; detección de 4 debilidades sin cobertura y 2 con cobertura parcial |
| 2026-09-07 | Remapeo a la Fase 1 revisada: riesgos renumerados a `R-01…R-10`, VPN reclasificada a ALTO, nuevos `R-09` (energía/D-13) y `R-10` (físico/D-12). Cobertura de debilidades con riesgo: 13/17 → **17/17**. Actualizado el estado global y las correspondencias E-nn |
