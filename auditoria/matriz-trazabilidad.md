# Matriz de trazabilidad D → R → C → E → I

**Propósito**: dar cumplimiento a la exigencia de §1.4 del enunciado —
*"cada debilidad detectada en la Fase 1 debe estar cubierta por al menos una medida concreta en
la Fase 2, un procedimiento de continuidad en la Fase 3 y —cuando aplique— un rubro de
inversión en la Fase 4."*

Esta tabla es el **instrumento de verificación** de esa cadena. Se actualiza al cerrar cada fase.

**Última actualización**: 2026-09-05

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
| Con riesgo asignado en Fase 1 | 13 de 17 (**76 %**) |
| Con control asignado en Fase 2 | 0 de 17 (0 %) |
| Con procedimiento en Fase 3 | 0 de 17 (0 %) |
| Con rubro de inversión en Fase 4 | 0 de 17 (0 %) |
| **Cadena completa D→R→C→E→I** | **0 de 17 (0 %)** |

---

## Matriz principal

Los `R-nn` reflejan la matriz de riesgos **tal como fue entregada** en la Fase 1.
Las columnas C, E e I se llenan conforme avancen las fases.

| ID | Debilidad (§2.4) | Fase 1 — Riesgo | Fase 2 — Control | Fase 3 — Escenario | Fase 4 — Inversión |
|---|---|---|---|---|---|
| **D-01** | 3 apps en DMZ sin WAF / Honeypot / Anti-DDoS / DNS Protection | `R-01` Compromiso de BD por vulnerabilidades web (**CRÍTICO**, 5×5) | *pendiente* | `E-04` | `I-` WAF, Anti-DDoS, DNS Security, Honeypot |
| **D-02** | Firewall perimetral único sin HA | `R-02` Caída total operativa por fallo de equipo de borde (**CRÍTICO**, 4×5) | *pendiente* | `E-02` | `I-` NGFW en clúster HA |
| **D-03** | VPN IPsec >6 años, IKEv1 + 3DES/SHA-1, sin respaldo | `R-05` Interceptación de datos en tránsito (MEDIO, 4×3) | *pendiente* | `E-03` | `I-` SD-WAN / reemplazo VPN |
| **D-04** | ISP único, sin redundancia ni balanceo | `R-02` (compartido con D-02) | *pendiente* | `E-08` | `I-` Segundo ISP |
| **D-05** | Sin 2FA/MFA en VPN, correo, dominio, consolas | `R-07` Suplantación de identidad / phishing (ALTO, 4×4) — *parcial* | *pendiente* | `E-04`, `E-05` | `I-` MFA/2FA |
| **D-06** | Cuentas administrativas compartidas; política de contraseñas débil | ⚠️ **sin riesgo propio** | *pendiente* | | `I-` MFA + PAM |
| **D-07** | Red plana /16 sin VLAN ni ACL | `R-03` Propagación masiva de malware/ransomware (**CRÍTICO**, 5×4) | *pendiente* | `E-05` | `I-` Segmentación VLAN + switching |
| **D-08** | WiFi con clave WPA2-Personal única compartida | ❌ **SIN COBERTURA** | *pendiente* | | `I-` WLAN segmentada 802.1X |
| **D-09** | Sin NAC | ❌ **SIN COBERTURA** | *pendiente* | | `I-` NAC 802.1X |
| **D-10** | SO desactualizados (WS2012R2, Win7/8.1), sin gestión de parches | `R-03` (mencionado dentro del riesgo de red plana) | *pendiente* | `E-05` | `I-` Renovación SO + gestor de parches |
| **D-11** | Antivirus de firmas, sin EDR, sin inventario de activos | ❌ **SIN COBERTURA** | *pendiente* | `E-05` | `I-` EDR + inventario |
| **D-12** | Sala sin control biométrico/tarjeta, CCTV parcial, sin monitoreo ambiental | ❌ **SIN COBERTURA** *(el checklist pregunta pero solo evalúa el UPS)* | *pendiente* | `E-01` | `I-` Control de acceso + CCTV + sensores |
| **D-13** | UPS de solo 15 min, sin planta eléctrica | `R-04` Pérdida irrecuperable de datos por desastre físico (ALTO, 3×5) — *parcial* | *pendiente* | `E-01` | `I-` UPS ampliado + planta |
| **D-14** | Respaldos en cinta local, sin offsite, sin inmutabilidad, sin pruebas | `R-04` Pérdida irrecuperable de datos por desastre físico (ALTO, 3×5) | *pendiente* | `E-01`, `E-05`, `E-06` | `I-` Plataforma de respaldo 3-2-1 |
| **D-15** | Sin SPF/DKIM/DMARC; sin programa de concientización | `R-07` Suplantación de identidad / phishing (ALTO, 4×4) | *pendiente* | `E-05` | `I-` Concientización + filtrado de correo |
| **D-16** | Sin SIEM, sin gestión de vulnerabilidades, sin IRP, sin CSIRT/SOC | `R-08` Ceguera operativa ante incidentes (**CRÍTICO**, 5×4) | *pendiente* | Todos los escenarios | `I-` SIEM + NDR + talento humano SOC |
| **D-17** | Accesos remotos permanentes de proveedores, sin monitoreo ni cláusulas | `R-06` Acceso no monitoreado de proveedores externos (ALTO, 4×4) | *pendiente* | `E-04` | `I-` PAM / gestión de acceso de terceros |

---

## Brechas de cobertura detectadas en Fase 1

### ❌ Sin riesgo asignado (4 debilidades)

| ID | Debilidad | Consecuencia si no se corrige |
|---|---|---|
| **D-08** | WiFi WPA2-Personal compartida con visitantes | La Fase 2 no tendrá de dónde derivar la medida de WLAN corporativa 802.1X con SSID de invitados aislado — y §5.1 punto 6.8 exige tratarla |
| **D-09** | Sin NAC | Igual: la Fase 2 debe cubrir NAC explícitamente (§5.1 punto 6.8) y la Fase 4 tiene un rubro dedicado (§7.2.3) |
| **D-11** | Sin EDR ni inventario de activos | §5.1 punto 6.6 exige un bloque de "seguridad ante programas malignos (antivirus/EDR)"; sin riesgo previo, la medida queda sin fundamento |
| **D-12** | Control de acceso físico y CCTV del datacenter | §5.2 lo lista como correspondencia obligatoria ("Datacenter sin protección perimetral física → Seguridad física y ambiental") |

### ⚠️ Con cobertura parcial (2 debilidades)

| ID | Debilidad | Situación |
|---|---|---|
| **D-06** | Cuentas administrativas compartidas y política de contraseñas | Absorbida implícitamente en el riesgo de phishing, pero es un vector distinto: el abuso de credenciales privilegiadas compartidas impide la trazabilidad de acciones administrativas. Merece riesgo propio |
| **D-10** | SO desactualizados | Aparece como agravante dentro del riesgo de red plana, no como riesgo independiente. Windows Server 2012 R2 sin soporte desde el 10-oct-2023 justifica un riesgo propio de explotación de vulnerabilidades sin parche disponible |

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
