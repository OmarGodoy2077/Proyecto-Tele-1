---
**Universidad Mariano Gálvez de Guatemala** — Facultad de Ingeniería en Sistemas de Información
**Campus:** Jutiapa · **Curso:** Telecomunicaciones (Área de Especialidad) · **Unidad integradora:** Seguridad de Redes
**Docente:** Ing. Juan Daniel Ramos Martínez · **Ciclo:** Segundo Semestre 2026
**Proyecto No. 01 — Fase 2: Plan de Seguridad Informática**
**Caso de estudio:** TransAgro del Oriente, S.A.
**Integrantes:** _(completar)_ · **Fecha de entrega:** _(completar)_
---

# Plan de Seguridad Informática

## TransAgro del Oriente, S.A.

---

## Control de versiones

| Versión | Fecha | Autor / rol | Descripción del cambio | Aprobado por |
|---|---|---|---|---|
| 0.1 | 2026-09-07 | Especialista en seguridad perimetral/DMZ y redes internas e identidad | Redacción inicial completa: alcance, caracterización, análisis de riesgo (retomando Fase 1), políticas, responsabilidades, 9 bloques de medidas y procedimientos, anexos y tabla de trazabilidad riesgo → control. | _(pendiente)_ |
| 0.2 | 2026-09-07 | Revisión técnica de redes y seguridad | Maduración del entregable: catálogo C-01…C-30 completo (C-07 y C-28), referencias primarias reforzadas, precisión del ciclo de respuesta a incidentes y del ciclo de soporte de Windows Server 2012 R2. | _(pendiente)_ |
| _(borrador)_ | | | Revisión del Redactor técnico y del Coordinador; consolidación con Fases 3 y 4. | |

**Clasificación del documento:** USO INTERNO — distribución restringida a Dirección, Gerencia de TI y responsables designados.
**Periodicidad de revisión:** anual, o ante cambio mayor de infraestructura, incidente grave o hallazgo de auditoría.
**Documento propietario:** Gerencia de Tecnología de la Información de TransAgro del Oriente, S.A.

---

## Índice

1. Alcance del Plan de Seguridad Informática
2. Caracterización del sistema informático
   2.1 Bienes informáticos
   2.2 Redes y comunicaciones
   2.3 Aplicaciones y servicios
   2.4 Personal
   2.5 Edificaciones e instalaciones
3. Resultados del análisis de riesgo (retomando la Fase 1)
4. Políticas de seguridad informática
5. Responsabilidades por rol
6. Medidas y procedimientos
   6.1 Clasificación y control de los bienes informáticos
   6.2 Gestión del personal
   6.3 Seguridad física y ambiental
   6.4 Seguridad de operaciones
   6.5 Identificación, autenticación y control de acceso
   6.6 Seguridad ante programas malignos
   6.7 Respaldo de la información
   6.8 Seguridad en redes
   6.9 Gestión de incidentes de seguridad
7. Anexos
   A. Listado nominal de usuarios y cuentas (plantilla)
   B. Registros y formularios de control
   C. Tabla de trazabilidad Debilidad → Riesgo → Control (D-nn → R-nn → C-nn)
   D. Catálogo de controles del Plan (C-01 a C-30)
   E. Mapa de control a los marcos de referencia (ISO/IEC 27001:2022, CIS v8.1, NIST CSF 2.0)
   F. Glosario
   G. Referencias

---

## Nota metodológica y de trazabilidad

Este Plan es el segundo entregable del Proyecto No. 01. Toma como insumo directo la **Fase 1 — Diagnóstico de riesgos tecnológicos** (checklist de 43 ítems sobre 9 dominios, matriz de riesgos R-01 a R-10 y conclusión ejecutiva de 5 riesgos críticos) y prepara los insumos de la Fase 3 (DRP) y de la Fase 4 (Plan de adquisición).

Se conserva la convención de identificadores del repositorio:

| Prefijo | Significado | Fase |
|---|---|---|
| `D-nn` | Debilidad del caso (enunciado §2.4) | Insumo |
| `R-nn` | Riesgo de la matriz de riesgos | Fase 1 |
| `C-nn` | Control / medida de este Plan de Seguridad | **Fase 2** |
| `E-nn` | Escenario de desastre del DRP | Fase 3 |
| `I-nn` | Rubro de inversión (CAPEX/OPEX) | Fase 4 |

**Regla de oro (enunciado §1.4):** cada una de las 17 debilidades del caso queda cubierta por **al menos un control concreto** de este Plan. La verificación completa está en el **Anexo C**.

Los controles se numeran **C-01 a C-30** y se agrupan en los 9 bloques obligatorios de medidas y procedimientos (§6). Cada control declara: la(s) debilidad(es) `D-nn` que remedia, el/los riesgo(s) `R-nn` que mitiga, el escenario `E-nn` del DRP que soporta y el rubro `I-nn` de inversión que requiere (referencia hacia la Fase 4, aún por numerar en detalle).

Todo dato técnico, fecha de obsolescencia y marco normativo citado en este documento está verificado contra fuente primaria en `referencias/fuentes-oficiales.md` y se lista en el **Anexo G**.

---

# 1. Alcance del Plan de Seguridad Informática

## 1.1 Propósito

Establecer el conjunto de políticas, responsabilidades, medidas y procedimientos de obligatorio cumplimiento que rigen la protección de la información y de la infraestructura tecnológica de **TransAgro del Oriente, S.A.**, con el fin de:

- Preservar la **confidencialidad, la integridad y la disponibilidad** de la información de la empresa, de sus clientes mayoristas, de sus proveedores agrícolas y de los datos de operación logística.
- Reducir a un nivel aceptable los riesgos identificados en la Fase 1, priorizando los cinco riesgos críticos de la conclusión ejecutiva (R-01, R-02, R-03, R-04 y R-05).
- Dotar a la organización de una **arquitectura de seguridad diseñada**, y no meramente heredada del crecimiento incremental de más de una década.
- Servir de base para el Plan de Recuperación ante Desastres (Fase 3) y para el Plan de Adquisición e Implementación (Fase 4).

## 1.2 Alcance organizacional

El Plan aplica a:

- Las **dos sedes** de la empresa: Casa Matriz (Jutiapa) y Planta de Procesamiento (Chiquimula).
- Los **~480 colaboradores**, sin excepción de nivel jerárquico, incluido el personal de Dirección y Gerencia.
- Todo el **personal externo** con acceso a los sistemas o a la red de TransAgro: proveedor de enlace de Internet (ISP), integrador de red, proveedor SaaS de rastreo de flotilla, proveedor de nómina electrónica en la nube y consultor externo del ERP.
- Visitantes y personal temporal mientras se encuentren dentro de las instalaciones o utilicen recursos de red de la empresa.

## 1.3 Alcance tecnológico

Quedan cubiertos por este Plan:

| Categoría | Elementos incluidos |
|---|---|
| Servidores | 18 servidores físicos y virtualizados de la Casa Matriz (ERP, base de datos, correo, archivos, servicios de dominio, servidores de la DMZ) y los servidores/estaciones de la Planta. |
| Aplicaciones publicadas | Portal de Clientes, Portal de Proveedores y Sistema de Rastreo de Flotilla (DMZ). |
| Aplicaciones internas | ERP y su base de datos transaccional, correo corporativo, servicios de archivos, servicios de directorio. |
| Redes y comunicaciones | Router de borde, firewall perimetral, DMZ, red interna (LAN), red inalámbrica corporativa, enlace VPN sitio a sitio Jutiapa↔Chiquimula, enlace a Internet. |
| Endpoints | Estaciones de trabajo administrativas de ambas sedes, equipos portátiles, impresoras de red. |
| Tecnología de operación (OT) | Controladores lógicos programables (PLC) de las líneas de procesamiento y cámaras IP de videovigilancia de la Planta. |
| Datos | Información de clientes y proveedores, facturación electrónica, datos financieros y contables del ERP, datos de ubicación GPS de la flotilla, datos de nómina, bitácoras y registros de seguridad. |
| Instalaciones | Centro de datos de la Casa Matriz, cuarto de telecomunicaciones de la Planta, áreas de trabajo y puntos de red. |
| Servicios de terceros | SaaS de rastreo de flotilla, nómina electrónica en la nube, servicios de soporte remoto de proveedores. |

## 1.4 Exclusiones

- Este Plan **no** es un plan de continuidad de negocio (BCP) completo; los aspectos no tecnológicos de la continuidad (recursos humanos, logística física, cadena de suministro agrícola) se abordan solo en lo que dependen de los sistemas de información.
- Los **procedimientos de recuperación paso a paso** ante desastre se desarrollan en la Fase 3 (DRP); este Plan los referencia y establece los prerrequisitos (por ejemplo, la política de respaldo y la arquitectura de alta disponibilidad).
- La **selección de marcas, modelos y precios** de las soluciones se desarrolla en la Fase 4; aquí se definen los requisitos funcionales que esas soluciones deben cumplir.
- Seguridad del producto agroindustrial, inocuidad alimentaria y cumplimiento fitosanitario, salvo los sistemas de trazabilidad que los soportan.

## 1.5 Marco de referencia adoptado

El Plan se alinea a:

- **ISO/IEC 27001:2022**, Anexo A — 93 controles en 4 temas (organizacionales, personas, físicos, tecnológicos). Se usa como taxonomía principal de control (Organización Internacional de Normalización, 2022).
- **CIS Critical Security Controls v8.1** — 18 controles, 153 salvaguardas. Nivel objetivo: **Grupo de Implementación 2 (IG2)**, coherente con el supuesto S-01 de la Fase 1: ~480 colaboradores, custodia de datos de terceros y operación OT (Center for Internet Security, 2024).
- **NIST Cybersecurity Framework 2.0** — 6 funciones: Gobernar, Identificar, Proteger, Detectar, Responder, Recuperar. Se usa para organizar el discurso ante Dirección (National Institute of Standards and Technology, 2024).
- **NIST SP 800-61 Rev. 3** — recomendaciones de respuesta a incidentes, base del bloque §6.9 (National Institute of Standards and Technology, 2025).
- **OWASP Top 10:2025** — base del control de protección de aplicaciones web de la DMZ (Open Worldwide Application Security Project, 2025).
- **NIST SP 800-207 (Zero Trust Architecture)** — principio rector de la segmentación: el acceso se concede por necesidad al recurso y verificación de identidad y postura, no por ubicación en la red (National Institute of Standards and Technology, 2020).
- **ISA/IEC 62443** — modelo de zonas y conductos para la segmentación de la red OT de la Planta.

## 1.6 Vigencia y aprobación

Este Plan entra en vigor a partir de su aprobación por la **Gerencia General** y es de **obligatorio cumplimiento**. Su incumplimiento se trata conforme al régimen disciplinario laboral vigente y, para terceros, conforme a las cláusulas contractuales de seguridad de la información (ver §6.2 y §6.8). Se revisa **al menos una vez al año** y cada vez que ocurra un cambio significativo de infraestructura, un incidente grave o un hallazgo de auditoría que lo amerite.

---

# 2. Caracterización del sistema informático

Esta sección describe el estado **actual** de la plataforma tecnológica de TransAgro del Oriente, S.A., tomado del enunciado (§2) y de la Fase 1. Es la línea base sobre la que operan los controles del §6. Donde el caso no detalla un aspecto, se aplica un supuesto documentado (S-01 a S-08; los cuatro primeros provienen de la Fase 1).

## 2.1 Bienes informáticos

### 2.1.1 Servidores

| Ubicación | Cantidad | Función principal | Sistema operativo (estado actual) | Criticidad |
|---|---|---|---|---|
| Casa Matriz (Jutiapa) — centro de datos | 18 físicos y virtualizados (agregado) | ERP y base de datos transaccional; servidor de correo corporativo; servidor de archivos; servicios de directorio y DNS internos; servidores de virtualización; servidores de la DMZ (portales y base de datos backend). | Predominantemente **Windows Server 2012 R2**. El soporte extendido general terminó el **10 de octubre de 2023**; las ESU, si fueron adquiridas o se usa Azure, solo constituyen una excepción temporal hasta octubre de 2026 y no sustituyen la migración (Microsoft, 2026). | ALTA — sostienen pedidos, facturación electrónica y trazabilidad. |
| Planta de Procesamiento (Chiquimula) — cuarto de telecomunicaciones | No detallado (supuesto S-05: 2–3 servidores/estaciones administrativas locales) | Estaciones administrativas de planta; concentración local de cámaras IP; interfaz con PLC. | Windows Server / Windows de escritorio desactualizados. | MEDIA-ALTA — soporta control de calidad y despacho. |

> **Supuesto S-05:** el caso indica que la Planta tiene "estaciones de trabajo administrativas" y un "cuarto de telecomunicaciones local" pero no detalla su número ni sistema operativo. Se asume una dotación menor equivalente a 2–3 equipos administrativos y ningún servidor de aplicaciones crítico local (el ERP se consume desde Jutiapa por la VPN). Registrar en `CLAUDE.md` §10.

### 2.1.2 Estaciones de trabajo y equipos de usuario

| Elemento | Descripción (estado actual) |
|---|---|
| Estaciones administrativas | Parque mixto; una parte con **Windows 7** (fin de soporte extendido: 14 de enero de 2020) y **Windows 8.1** (fin de soporte: 10 de enero de 2023). Sin gestión centralizada de parches. Sin cifrado de disco. Antivirus tradicional basado en firmas, desactualizado en varias máquinas. Sin EDR. |
| Equipos portátiles | Supuesto S-06: existen equipos portátiles de personal de ventas y de gerencia; se asume el mismo estado de configuración que las estaciones fijas. |
| Impresoras de red | Conectadas a la misma subred plana /16 que servidores y estaciones. |
| Inventario de activos | **No existe** un inventario centralizado y confiable de hardware y software. |

> **Supuesto S-06:** el caso no menciona equipos portátiles explícitamente pero describe personal de ventas y gerencia; se asume su existencia con el mismo perfil de configuración. Registrar en `CLAUDE.md` §10.

### 2.1.3 Tecnología de operación (OT) e IoT

| Elemento | Descripción (estado actual) |
|---|---|
| Controladores lógicos programables (PLC) | En las líneas de procesamiento de la Planta de Chiquimula. Comparten la misma subred /16 que las estaciones de usuario, sin ACL entre segmentos. Su compromiso o indisponibilidad detiene el procesamiento industrial. |
| Cámaras IP de videovigilancia | En la Planta (y parcialmente en la Casa Matriz). También en la red plana. |

### 2.1.4 Software y licenciamiento

| Elemento | Descripción (estado actual) |
|---|---|
| ERP | Aplicación central de negocio con base de datos transaccional. Versión del framework y del motor de base de datos no detallada (supuesto S-07: motor de base de datos y sistema operativo host dentro de la ventana de obsolescencia descrita en D-10). |
| Aplicaciones de la DMZ | Portal de Clientes (framework desactualizado), Portal de Proveedores (carga de archivos sin validación robusta), Sistema de Rastreo de Flotilla (credenciales estáticas embebidas en el código). |
| Sistemas operativos | Ver §2.1.1 y §2.1.2. |
| Herramientas de seguridad | Antivirus de firmas. **No hay** WAF, EDR, SIEM, NAC, gestor de parches ni gestor de identidades privilegiadas. |

> **Supuesto S-07:** ante la ausencia de detalle sobre el motor de base de datos del ERP, se asume que corre sobre un sistema operativo dentro de la ventana de obsolescencia de D-10 y que su versión requiere evaluación de soporte en la Fase 4. Registrar en `CLAUDE.md` §10.

## 2.2 Redes y comunicaciones

### 2.2.1 Topología lógica actual (descripción)

```
                    Internet
                       |
                [ Router de borde ]
                       |
              ( ISP ÚNICO - sin redundancia )
                       |
        [ FIREWALL PERIMETRAL ÚNICO - sin HA ]
             /            |             \
        Zona DMZ      Red interna     Túnel VPN sitio a sitio
            |          (LAN plana)     (IPsec IKEv1 / 3DES / SHA-1,
   +--------+--------+   subred /16     > 6 años, sin respaldo)
   | Portal Clientes |   sin VLAN           |
   | Portal Provee.  |   sin ACL      [ Planta Chiquimula ]
   | Rastreo Flotilla|      |          cuarto de telecom.
   +--------+--------+      |          - PLC de líneas
            |               |          - cámaras IP
   [ BD backend compartida ]|          - estaciones admin.
   (misma que consume el   -+- estaciones de usuario
    Portal de Clientes         - servidores ERP / correo / archivos
    directo, sin capa de       - impresoras de red
    servicios intermedia)      - cámaras IP
                               - (todo en la misma subred /16)
```

> El **diagrama de topología actual en Cisco Packet Tracer** (obligatorio, enunciado §8.1) es insumo compartido de la Fase 1 (§2.2) y de esta Fase 2. Este Plan usa la descripción textual anterior como referencia; el diagrama gráfico se adjunta en el documento consolidado (Fase final).

### 2.2.2 Componentes de red — estado actual

| Componente | Estado actual | Debilidad asociada |
|---|---|---|
| Enlace a Internet | Un único proveedor (ISP), sin SLA documentado, sin redundancia ni balanceo. | D-04 |
| Router de borde | Equipo único. | D-04 |
| Firewall perimetral | Equipo único, sin clúster de alta disponibilidad. Separa Internet / DMZ / red interna. Sin IPS documentado, sin filtrado DNS, sin protección de capa de aplicación. | D-02 |
| DMZ | Un solo segmento para las tres aplicaciones web públicas y su base de datos backend compartida. Sistemas operativos desactualizados. Sin WAF, sin Anti-DDoS, sin Honeypot/Deception, sin filtrado DNS. | D-01 |
| Red interna (LAN) | **Plana**, una sola subred /16 sin VLAN. Convergen estaciones, servidores, impresoras, cámaras IP y PLC. Sin ACL entre tipos de dispositivo. | D-07, D-09 |
| Red inalámbrica corporativa | Una sola clave **WPA2-Personal** (PSK) compartida por todo el personal y los visitantes. Sin SSID de invitados aislado, sin portal cautivo, sin 802.1X. | D-08 |
| Control de acceso a la red (NAC) | Inexistente. Cualquier dispositivo conectado a un punto de red obtiene IP y acceso a los recursos internos. | D-09 |
| VPN sitio a sitio Jutiapa↔Chiquimula | Túnel IPsec sobre Internet público, con más de 6 años de antigüedad. **IKEv1**, cifrado **3DES**, integridad **SHA-1**. Sin enlace de respaldo ni SD-WAN. IKEv1 fue deprecado formalmente por el IETF en el RFC 9395 (2023); SHA-1 fue retirado por NIST (2022); 3DES está en calendario de retiro (NIST SP 800-131A Rev. 2). | D-03 |
| Segmentación DMZ ↔ interna | El firewall implementa las tres zonas, pero la aplicación de la DMZ tiene **conexión directa a la base de datos del ERP interno**, sin capa de servicios intermedia. | D-01 |

### 2.2.3 Direccionamiento y servicios de red

| Servicio | Estado actual (supuesto S-08 donde el caso no detalla) |
|---|---|
| Direccionamiento IPv4 | Subred privada única /16 en la red interna (dato del caso). Asignación por DHCP sin control de admisión. |
| DNS | Resolución interna por servidor de dominio; resolución externa sin filtrado de dominios maliciosos ni de phishing. |
| Servicios de directorio | Dominio interno de Active Directory (supuesto S-08, coherente con la mención de "dominio interno" en D-05). Cuentas administrativas compartidas; política de contraseñas sin complejidad ni expiración. |
| Correo | Dominio de correo corporativo **sin SPF, sin DKIM y sin DMARC**. Alta exposición a suplantación del dominio. |
| NTP, registro de eventos | Sin sincronización horaria centralizada verificada y sin recolección centralizada de bitácoras (no hay SIEM). |

> **Supuesto S-08:** el caso menciona "dominio interno" y "consolas de administración de servidores"; se asume Active Directory como servicio de directorio y autenticación. Registrar en `CLAUDE.md` §10.

## 2.3 Aplicaciones y servicios

### 2.3.1 Aplicaciones publicadas en la DMZ

| Aplicación | Función de negocio | Debilidad técnica (del caso) | Mapeo OWASP Top 10:2025 |
|---|---|---|---|
| **Portal de Clientes** | Ingreso y seguimiento de pedidos de granos y derivados por clientes mayoristas. | Framework desactualizado; **conexión directa a la base de datos interna del ERP**, sin capa de servicios intermedia. | A01 Broken Access Control; A06 Insecure Design; A02 Security Misconfiguration. |
| **Portal de Proveedores** | Facturación electrónica y programación de entregas de proveedores agrícolas. | **Carga de archivos sin validación** robusta de tipo/contenido; sin WAF. | A05 Injection; A03 Software Supply Chain Failures; A08 Software or Data Integrity Failures. |
| **Sistema de Rastreo de Flotilla** | Consulta de ubicación GPS y estado de la flotilla en tiempo real. | Integración por API con un SaaS externo mediante **credenciales estáticas embebidas en el código**. | A04 Cryptographic Failures; A07 Authentication Failures; A02 Security Misconfiguration. |

Las tres aplicaciones comparten **el mismo segmento de DMZ y el mismo servidor de base de datos backend**: comprometer una es una amenaza directa a las otras dos y, potencialmente, a la red interna.

### 2.3.2 Aplicaciones y servicios internos

| Servicio | Descripción | Criticidad de negocio |
|---|---|---|
| ERP y base de datos transaccional | Núcleo de pedidos, facturación electrónica, inventario, finanzas y contabilidad. | **CRÍTICA.** Su indisponibilidad detiene la facturación y la toma de pedidos. |
| Correo corporativo | Comunicación con clientes, proveedores y autoridades; vehículo de facturación electrónica y de notificaciones. | ALTA. |
| Servicios de archivos | Documentación operativa, contratos, registros de calidad y trazabilidad. | ALTA. |
| Servicios de directorio y autenticación (AD) | Autenticación de usuarios y equipos, políticas de grupo. | **CRÍTICA** (habilitador transversal). |
| Trazabilidad de cadena de frío / transporte | Depende del Sistema de Rastreo de Flotilla y del ERP. | ALTA (contractual con clientes de exportación). |

### 2.3.3 Servicios de terceros

| Proveedor | Servicio | Modo de acceso actual | Debilidad |
|---|---|---|---|
| ISP | Enlace de Internet de ambas sedes | Enlace permanente, sin SLA documentado. | D-04, D-17 |
| Integrador de red | Instaló firewall y VPN hace más de 6 años | Contrato de soporte **no vigente**. | D-17 |
| SaaS de rastreo de flotilla | Almacena datos de ubicación de la flotilla | API con credenciales estáticas embebidas en el código del sistema publicado. | D-01, D-17 |
| Nómina electrónica en la nube | Procesamiento de nómina | Acceso remoto **periódico** a los sistemas administrativos. | D-17 |
| Consultor externo del ERP | Mantenimiento del ERP | Acceso remoto **permanente** con credenciales **no rotadas**. | D-17 |

## 2.4 Personal

### 2.4.1 Personal interno de Tecnología de la Información

| Rol | Cantidad | Sede | Funciones |
|---|---|---|---|
| Gerente de Tecnología de la Información | 1 | Casa Matriz | Reporta a Gerencia General. Dirección del área, presupuesto, proveedores, decisiones de arquitectura. |
| Administrador de sistemas y redes | 2 | Casa Matriz | Operación de servidores, red, respaldos, soporte de segundo nivel. Asumen de forma informal las funciones de seguridad. |
| Técnico de soporte en sitio | 1 | Planta (Chiquimula) | Soporte de primer nivel, estaciones, impresoras, cámaras, coordinación con líneas de planta. |

**No existe** personal dedicado a seguridad de la información, monitoreo o respuesta a incidentes. Esta brecha de talento humano se trata en el §5, en el §6.9 y, en su dimensión de inversión, en la Fase 4 (estructura de Comité de Seguridad, Oficial de Seguridad de la Información, Analista SOC N1, Especialista en Respuesta a Incidentes, o servicio MDR/SOC tercerizado).

### 2.4.2 Personal usuario

~480 colaboradores en total, distribuidos en administración, finanzas, ventas, atención a clientes (Casa Matriz), acopio, procesamiento, control de calidad y logística (Planta). **No existe** un programa formal de concientización en ciberseguridad. El usuario es el eslabón más expuesto ante phishing (agravado por la ausencia de SPF/DKIM/DMARC).

### 2.4.3 Personal externo con acceso

Los cinco proveedores de §2.3.3, más personal temporal y visitantes que hoy comparten la clave WiFi única.

## 2.5 Edificaciones e instalaciones

| Instalación | Descripción | Controles físicos actuales | Debilidad |
|---|---|---|---|
| Centro de datos — Casa Matriz (Jutiapa) | Aloja los 18 servidores, almacenamiento, equipos de red de core y perímetro, y las **cintas de respaldo** (en el mismo cuarto que la producción). | **Llave física compartida** (sin biométrico ni tarjeta, sin bitácora de ingreso). CCTV de cobertura parcial, sin retención adecuada. **Sin monitoreo ambiental** (temperatura, humedad, fuga de agua, corte eléctrico). **UPS de 15 minutos** de autonomía. **Sin planta eléctrica** de respaldo. | D-12, D-13, D-14 |
| Cuarto de telecomunicaciones — Planta (Chiquimula) | Aloja el equipo terminal de la VPN, el switch local, la concentración de cámaras IP y la interfaz con PLC. | Supuesto S-09: controles físicos limitados equivalentes o inferiores a los de la Casa Matriz. | D-12 |
| Áreas de trabajo y puntos de red | Oficinas administrativas de ambas sedes. | Puntos de red activos sin control de admisión (NAC). Cualquier persona con acceso físico a una oficina puede conectar un dispositivo. | D-09 |

> **Supuesto S-09:** el caso no describe los controles físicos del cuarto de telecomunicaciones de la Planta; se asume que son limitados. Registrar en `CLAUDE.md` §10.

---

# 3. Resultados del análisis de riesgo (retomando la Fase 1)

## 3.1 Método aplicado en la Fase 1

La Fase 1 aplicó un checklist propio de **43 ítems** sobre los **9 dominios mínimos** del enunciado (§4.2), tomando como referencia CIS Controls v8.1 (nivel IG2) e ISO/IEC 27001:2022. De los hallazgos se construyó una matriz de riesgos con escala cualitativa de **probabilidad (1–5) × impacto (1–5)** y la regla de conversión:

| Nivel | Rango P×I | Criterio de tratamiento (supuesto S-04) |
|---|---|---|
| CRÍTICO | 20 – 25 | Mitigación inmediata; escalamiento a Gerencia General. |
| ALTO | 12 – 19 | Mitigación planificada de corto plazo (≤ 3 meses). |
| MEDIO | 6 – 11 | Mitigación programada (≤ 12 meses). |
| BAJO | 1 – 5 | Aceptar y monitorear. |

## 3.2 Matriz de riesgos priorizada (resumen de la Fase 1)

| R-nn | Riesgo | D-nn | Prob. | Impacto | P×I | Nivel | Controles de este Plan |
|---|---|---|---|---|---|---|---|
| **R-01** | Compromiso de la base de datos interna por explotación de las aplicaciones web de la DMZ | D-01 | 5 | 5 | 25 | **CRÍTICO** | C-19, C-20, C-21, C-22, C-14 |
| **R-02** | Caída total de la conectividad de la Casa Matriz y aislamiento de la Planta por fallo del equipo de borde | D-02, D-04 | 4 | 5 | 20 | **CRÍTICO** | C-13, C-23, C-24 |
| **R-03** | Propagación masiva de malware / ransomware por ausencia de segmentación en la red interna | D-05, D-06, D-07, D-08, D-09, D-10, D-11 | 5 | 4 | 20 | **CRÍTICO** | C-15, C-16, C-25, C-26, C-27, C-28, C-01, C-02, C-17, C-18 |
| **R-04** | Ceguera operativa ante incidentes de seguridad por ausencia de SIEM y de plan de respuesta | D-16 | 5 | 4 | 20 | **CRÍTICO** | C-29, C-30, C-11, C-12 |
| **R-05** | Pérdida irrecuperable de datos ante desastre físico o ransomware por respaldos sin copia externa ni pruebas | D-14 | 3 | 5 | 15 | **ALTO** | C-08, C-09, C-10 |
| **R-06** | Acceso no monitoreado y persistente de proveedores externos al ERP y a la red interna | D-17 | 4 | 4 | 16 | **ALTO** | C-05, C-06, C-07, C-18 |
| **R-07** | Suplantación de identidad y compromiso de credenciales por phishing y ausencia de MFA | D-05, D-15 | 4 | 4 | 16 | **ALTO** | C-15, C-03, C-04, C-22 |
| **R-08** | Interceptación o descifrado del tráfico entre sedes por criptografía obsoleta en la VPN | D-03 | 4 | 3 | 12 | **ALTO** | C-23, C-24 |
| **R-09** | Apagado abrupto y daño de equipos del centro de datos por autonomía energética insuficiente | D-13 | 3 | 4 | 12 | **ALTO** | C-12 (b), C-13 |
| **R-10** | Acceso físico no controlado y daño ambiental no detectado en el centro de datos | D-12 | 3 | 4 | 12 | **ALTO** | C-12 (a), C-12 (c) |

> Nota: la numeración de controles C-nn se define en el §6 y se cataloga en el Anexo D. Un mismo control puede mitigar varios riesgos y un mismo riesgo puede requerir varios controles.

## 3.3 Los cinco riesgos críticos y su tratamiento en este Plan

De la conclusión ejecutiva de la Fase 1, los cinco riesgos que la Dirección debe atender de inmediato, y la respuesta de este Plan:

| # | Riesgo (Fase 1) | Causa raíz | Respuesta de la Fase 2 |
|---|---|---|---|
| 1 | **R-01 (25)** — Exposición directa de la información del ERP a través de las apps web | Portales en DMZ sin inspección de capa de aplicación; Portal de Clientes conectado directo a la BD del ERP. | §6.8: WAF gestionado (C-19), Anti-DDoS (C-20), filtrado DNS (C-21), rediseño de la DMZ con capa de servicios intermedia y segmentación estricta (C-14, C-22); §6.4: gestión de cambios y hardening antes de publicar (C-17). |
| 2 | **R-03 (20)** — Propagación masiva de malware/ransomware por red plana | Red /16 sin VLAN ni ACL; sin NAC; WiFi con clave única compartida con visitantes; SO sin soporte; sin EDR. | §6.8: segmentación en VLAN por función con ACL y modelo Zero Trust / IEC 62443 para OT (C-25), NAC 802.1X (C-26), WLAN WPA3-Enterprise con SSID de invitados aislado (C-27); §6.6: EDR (C-15); §6.4: renovación de SO sin soporte (C-16). |
| 3 | **R-04 (20)** — Ceguera operativa ante incidentes | Sin SIEM, sin plan de respuesta, sin responsable designado. | §6.9: SIEM y correlación de logs (C-29), plan formal de respuesta a incidentes por tipo (C-30), gestión de vulnerabilidades y pentesting (C-11); §5: designación de responsable de seguridad y Comité. |
| 4 | **R-02 (20)** — Punto único de falla en el borde de la red | Un solo firewall y un solo enlace ISP; VPN sobre ese mismo enlace. | §6.4: continuidad de servicios críticos de red — clúster de firewalls en alta disponibilidad (C-13); §6.8: segundo enlace ISP con failover y SLA (C-24), SD-WAN para la ruta entre sedes (C-23). |
| 5 | **R-05 (15)** — Imposibilidad de recuperación ante desastre o ransomware | Respaldos en cinta en la misma sala que la producción; sin copia externa, sin inmutabilidad, sin pruebas. | §6.7: política de respaldo bajo el modelo 3-2-1-1-0 con copia offsite y copia inmutable (C-08), calendario de pruebas de restauración (C-09), cifrado y retención documentada (C-10). |

## 3.4 Apetito de riesgo y criterio de aceptación

La Gerencia General de TransAgro adopta el siguiente criterio:

- **No se aceptan** riesgos de nivel CRÍTICO ni ALTO sin un plan de tratamiento con responsable y fecha.
- Los riesgos de nivel MEDIO se tratan dentro de los 12 meses o se aceptan formalmente por escrito por la Gerencia de TI con visto bueno del Comité de Seguridad.
- Los riesgos de nivel BAJO se aceptan y se monitorean; se revalúan en la revisión anual del Plan.
- Todo riesgo **aceptado** queda registrado en el **Registro de riesgos aceptados** (Anexo B, formato R-6) con fecha, justificación de negocio, responsable y fecha de revaluación.

---

# 4. Políticas de seguridad informática

Normas generales de **obligatorio cumplimiento** para todo el personal interno y externo dentro del alcance (§1.2). Cada política es de nivel directivo; su implementación operativa está en el §6. El incumplimiento se trata según §1.6.

## P-01. Política general de seguridad de la información

TransAgro del Oriente, S.A. protege la confidencialidad, la integridad y la disponibilidad de su información y de la que le confían clientes y proveedores. La seguridad de la información es responsabilidad de todos los colaboradores y una condición del uso de los recursos tecnológicos de la empresa. La Gerencia General respalda este Plan, asigna los recursos para ejecutarlo y exige su cumplimiento.

## P-02. Política de clasificación y manejo de la información

Toda información de la empresa se clasifica en una de cuatro categorías: **Pública, Uso interno, Confidencial y Restringida**. El manejo, almacenamiento, transmisión, retención y destrucción de la información se realiza conforme a su clasificación (§6.1). Los datos de clientes, de proveedores, financieros del ERP y de ubicación de la flotilla son, como mínimo, **Confidenciales**.

## P-03. Política de control de acceso

El acceso a los sistemas y a la información se concede bajo los principios de **mínimo privilegio** y **necesidad de conocer**, mediante **cuentas individuales y nominadas**. Quedan prohibidas las cuentas compartidas. El acceso a recursos críticos exige **autenticación multifactor**. Los accesos se revisan formalmente al menos cada seis meses y se revocan de inmediato al cesar la necesidad (§6.5).

## P-04. Política de autenticación multifactor (MFA/2FA)

Es obligatorio el segundo factor de autenticación para: VPN y acceso remoto, correo corporativo, dominio interno, consolas de administración de servidores y de red, acceso a la plataforma del ERP con perfiles administrativos, y todo acceso de proveedores externos. Para cuentas privilegiadas y accesos de administración se exige **MFA resistente a phishing** (FIDO2/WebAuthn o certificados), conforme a la guía de CISA (Cybersecurity and Infrastructure Security Agency, 2022) y a NIST SP 800-63B (§6.5).

## P-05. Política de contraseñas y credenciales

Las contraseñas cumplen los requisitos de longitud y resistencia definidos en el §6.5, se almacenan solo de forma protegida y nunca se comparten ni se embeben en código fuente ni en archivos de configuración en texto claro. Las credenciales de servicio y de integración se custodian en una **bóveda de secretos** y se rotan periódicamente. Las credenciales estáticas del Sistema de Rastreo de Flotilla se eliminan del código y se migran a la bóveda antes de cualquier otra intervención sobre esa aplicación.

## P-06. Política de uso aceptable de los recursos tecnológicos

Los equipos, la red, el correo y los servicios de TransAgro se usan para fines relacionados con el trabajo. Queda prohibido: instalar software no autorizado, desactivar controles de seguridad (antivirus/EDR, cifrado, firewall de host), conectar dispositivos personales a la red corporativa sin autorización, y extraer información confidencial fuera de los medios autorizados. El usuario acepta esta política al recibir sus credenciales.

## P-07. Política de seguridad en redes y segmentación

La red se diseña y opera segmentada por función y por nivel de confianza. La comunicación entre segmentos se permite solo de forma explícita (denegación por defecto). Los dispositivos de operación (PLC) y las cámaras IP se aíslan en zonas dedicadas conforme al modelo de zonas y conductos de ISA/IEC 62443. Ningún servicio se publica a Internet sin pasar por el proceso de control de publicación (§6.8) y sin protección de capa de aplicación (WAF).

## P-08. Política de comunicaciones seguras y criptografía

Todo tráfico que atraviese una red no confiable (Internet, enlaces entre sedes) se cifra con algoritmos vigentes: **IKEv2, AES-256-GCM y SHA-2 (SHA-256 o superior)**, grupo Diffie-Hellman 19/20 o superior y Perfect Forward Secrecy habilitado (supuesto S-03). Quedan prohibidos IKEv1, 3DES, DES, RC4, MD5 y SHA-1 para cualquier uso nuevo o renovado, conforme al RFC 9395 (Smyslov & Hoffman, 2023), al retiro de SHA-1 por NIST (2022) y a NIST SP 800-131A Rev. 2 (Barker & Roginsky, 2019).

## P-09. Política de protección de endpoints y contra programas malignos

Todo servidor y estación de trabajo cuenta con una solución de **detección y respuesta en endpoint (EDR)** administrada centralmente, con protección en tiempo real, aislamiento remoto y telemetría enviada al SIEM. El antivirus de solo firmas se retira. Ningún equipo sin EDR y sin parches al día se conecta a la red corporativa (se valida por NAC).

## P-10. Política de gestión de vulnerabilidades y parches

Los sistemas operativos y las aplicaciones se mantienen con soporte vigente del fabricante y con los parches de seguridad aplicados según los plazos del §6.4. Los sistemas fuera de soporte (Windows Server 2012 R2, Windows 7, Windows 8.1) se migran o se aíslan con controles compensatorios documentados y aprobados. Se ejecutan escaneos de vulnerabilidades al menos mensuales y una prueba de penetración anual de las aplicaciones publicadas.

## P-11. Política de respaldo y recuperación de la información

La información crítica se respalda bajo el modelo **3-2-1-1-0**: tres copias, en dos medios distintos, una fuera de sitio, una copia **inmutable o aislada (air-gapped)** y **cero errores** verificados mediante pruebas periódicas de restauración (Veeam, 2024). Los respaldos se cifran. La política de retención se documenta y se aprueba. Este Plan fija los prerrequisitos; los procedimientos de recuperación se desarrollan en el DRP (Fase 3).

## P-12. Política de gestión de incidentes de seguridad

Todo colaborador reporta de inmediato cualquier evento sospechoso al canal definido (§6.9). La empresa mantiene un **plan de respuesta a incidentes** documentado, con roles, procedimientos por tipo de incidente y un responsable designado. Los incidentes se registran, se clasifican por severidad, se contienen, se erradican, se recuperan y se someten a lección aprendida, conforme a NIST SP 800-61 Rev. 3 (National Institute of Standards and Technology, 2025).

## P-13. Política de seguridad física y ambiental

El acceso al centro de datos y a los cuartos de telecomunicaciones se controla por medio de identificación individual (tarjeta o biométrico) con bitácora, se videovigila con retención mínima de 30 días (supuesto S-02) y se monitorea ambientalmente con alertas automáticas. La energía de la carga crítica se respalda con UPS de autonomía suficiente para un apagado ordenado y con planta eléctrica para eventos prolongados.

## P-14. Política de gestión de terceros y proveedores

Ningún tercero accede a los sistemas de TransAgro sin: un contrato con **cláusulas de seguridad de la información y acuerdo de confidencialidad (NDA)**, cuentas **individuales, nominadas y temporales** con fecha de expiración, **MFA**, mínimo privilegio, y **registro y monitoreo de sus sesiones**. Los accesos remotos permanentes existentes (consultor del ERP, integrador de red, SaaS de rastreo) se convierten a este esquema o se revocan.

## P-15. Política de gestión del personal

La seguridad de la información se integra al ciclo de vida del empleo: verificación previa proporcional al puesto, acuerdo de confidencialidad en la contratación, capacitación de inducción, **programa continuo de concientización** con simulacros de phishing, y un procedimiento de baja que revoca todos los accesos el mismo día del cese (§6.2).

## P-16. Política de cumplimiento, auditoría y excepciones

El cumplimiento de este Plan se audita al menos una vez al año. Toda excepción a una política debe solicitarse por escrito, justificarse por necesidad de negocio, definir controles compensatorios, tener fecha de vencimiento y ser aprobada por la Gerencia de TI con visto bueno del Comité de Seguridad. Las excepciones se registran en el Anexo B (formato R-7).

---

# 5. Responsabilidades por rol

La seguridad de la información se estructura en tres líneas: quien **decide y aprueba** (Dirección y Comité), quien **diseña, opera y verifica** (Gerencia de TI, administradores y el rol de seguridad), y quien **cumple en el día a día** (usuarios y terceros).

## 5.1 Estructura de gobierno propuesta

```
                 Gerencia General
                        |
        Comité de Seguridad de la Información
   (Gerencia General + Gerencia de TI + asesor externo
      + Oficial de Seguridad de la Información)
                        |
     Oficial / Responsable de Seguridad de la Información
        (interno a tiempo parcial o vCISO por contrato)
              /                          \
   Administradores de              Analista SOC N1  +  Especialista en
   Sistemas y Redes (2)            Respuesta a Incidentes
   Técnico de soporte (1)          (internos, o servicio MDR/SOC tercerizado)
```

> La creación de los roles de seguridad y su modalidad (interna, tercerizada o mixta) se dimensiona económicamente en la Fase 4. Este Plan los define funcionalmente y establece que su ausencia actual es una brecha de tratamiento inmediato asociada a R-04.

## 5.2 Dirección / Gerencia General

| Responsabilidad | Detalle |
|---|---|
| Aprobar el Plan y sus políticas | Firmar la versión vigente; exigir su cumplimiento en toda la organización. |
| Asignar recursos | Aprobar el presupuesto de la Fase 4 (CAPEX y OPEX) y el plan de contratación o tercerización del equipo de seguridad. |
| Presidir el Comité de Seguridad | Convocar al menos trimestralmente; conocer el estado de los riesgos críticos y altos. |
| Autoridad de aceptación de riesgo | Aceptar formalmente, por escrito, los riesgos residuales que no se traten. |
| Respaldo en incidentes graves | Autorizar comunicación externa, contacto con autoridades y activación del DRP cuando el criterio lo exija (Fase 3). |
| Tono desde la cima | Cumplir personalmente las políticas (MFA, clasificación, uso aceptable) como ejemplo. |

## 5.3 Comité de Seguridad de la Información

| Responsabilidad | Detalle |
|---|---|
| Dirección estratégica | Revisar y priorizar el tratamiento de riesgos; aprobar el plan anual de seguridad y sus métricas. |
| Aprobar políticas y excepciones | Dar visto bueno a nuevas políticas, a cambios mayores y a las excepciones (P-16). |
| Supervisar el avance | Dar seguimiento a la implementación de los controles C-01 a C-30 y a los hallazgos de auditoría. |
| Coordinar áreas | Alinear seguridad con operaciones de planta, finanzas, ventas y recursos humanos. |
| Revisión post-incidente | Conocer los informes de incidentes graves y aprobar las acciones correctivas. |

## 5.4 Gerencia de Tecnología de la Información

| Responsabilidad | Detalle |
|---|---|
| Propietario del Plan | Mantener, actualizar y distribuir el Plan; convocar su revisión anual. |
| Diseño de la arquitectura de seguridad | Aprobar el diseño de segmentación, la arquitectura de alta disponibilidad, el rediseño de la DMZ y la configuración objetivo de la VPN. |
| Gestión de proveedores de seguridad | Contratar y supervisar al integrador, al proveedor de WAF/Anti-DDoS/DNS, al MDR/SOC y a los servicios de nube; exigir SLA y cláusulas de seguridad. |
| Gestión de vulnerabilidades y cambios | Presidir el Comité de Cambios; aprobar ventanas de mantenimiento y excepciones técnicas temporales. |
| Reporte a Dirección | Presentar al Comité el estado de los riesgos, el avance de controles y las métricas (§6.9.7). |
| Designar al responsable de seguridad | Nombrar al Oficial de Seguridad de la Información (o contratar el vCISO) y dotarlo de autoridad funcional. |

## 5.5 Oficial / Responsable de Seguridad de la Información

| Responsabilidad | Detalle |
|---|---|
| Operación del programa de seguridad | Ejecutar el plan anual; mantener el registro de riesgos y la matriz de trazabilidad D→R→C. |
| Gestión de incidentes | Coordinar la respuesta a incidentes (§6.9); ser el punto de contacto del CSIRT/SOC. |
| Concientización | Diseñar y medir el programa de concientización y los simulacros de phishing. |
| Cumplimiento y auditoría | Preparar y acompañar las auditorías; verificar el cierre de hallazgos. |
| Revisión de accesos | Coordinar la recertificación semestral de accesos y la revisión de cuentas privilegiadas y de terceros. |
| Métricas | Reportar mensualmente los indicadores de seguridad a la Gerencia de TI. |

## 5.6 Administradores de Sistemas y Redes / Técnico de soporte

| Responsabilidad | Detalle |
|---|---|
| Implementar y operar los controles técnicos | Segmentación, NAC, firewalls, VPN, EDR, gestor de parches, bóveda de secretos, plataforma de respaldo, SIEM (recolección). |
| Aplicar parches y hardening | Cumplir los plazos de P-10; aplicar líneas base de configuración; documentar excepciones. |
| Gestión de cuentas | Crear, modificar y dar de baja cuentas conforme a las solicitudes autorizadas; no crear cuentas compartidas. |
| Respaldos | Ejecutar y verificar los respaldos; participar en las pruebas de restauración calendarizadas. |
| Primer nivel de respuesta | Detectar, contener y escalar incidentes según el §6.9; preservar evidencia. |
| Registro de cambios | Documentar todo cambio en el sistema de gestión de cambios. |
| Terminante | No usar las cuentas administrativas compartidas actuales una vez creadas las nominadas; reportar cualquier presión para hacerlo. |

## 5.7 Usuarios (todo el personal)

| Responsabilidad | Detalle |
|---|---|
| Cumplir las políticas | Uso aceptable (P-06), contraseñas (P-05), MFA (P-04), clasificación de la información (P-02). |
| Proteger sus credenciales | No compartirlas, no anotarlas a la vista, no reutilizarlas fuera del trabajo. |
| Reportar | Informar de inmediato correos sospechosos, comportamientos anómalos del equipo, pérdida o robo de dispositivos, y cualquier incidente. |
| Participar en la concientización | Completar la capacitación anual y atender los resultados de los simulacros de phishing. |
| Manejo de dispositivos | No conectar dispositivos no autorizados; bloquear la sesión al ausentarse; no desactivar el EDR ni el cifrado. |

## 5.8 Terceros y proveedores

| Responsabilidad | Detalle |
|---|---|
| Aceptar y cumplir las cláusulas de seguridad | Firmar el anexo de seguridad de la información y el NDA antes de cualquier acceso. |
| Usar accesos nominados y temporales | Un usuario por persona, con MFA, con fecha de expiración; nunca credenciales compartidas ni embebidas. |
| Someterse a monitoreo | Aceptar el registro y la grabación de sus sesiones de acceso remoto. |
| Notificar incidentes | Informar a TransAgro dentro de las 24 horas de cualquier incidente que pueda afectar su información o sus sistemas. |
| Mínimo privilegio y ventana de trabajo | Acceder solo a lo autorizado y solo durante la ventana acordada. |

## 5.9 Recursos Humanos

| Responsabilidad | Detalle |
|---|---|
| Ciclo de vida del empleo | Ejecutar la verificación previa, la firma de acuerdos de confidencialidad y la inducción de seguridad. |
| Notificación de altas y bajas | Comunicar a TI las altas, cambios de puesto y bajas **el mismo día**, para el aprovisionamiento y la revocación de accesos. |
| Apoyo al régimen disciplinario | Tramitar las sanciones por incumplimiento conforme al reglamento interno. |

---

# 6. Medidas y procedimientos

Los controles se agrupan en los **9 bloques obligatorios** del enunciado (§5.1 punto 6). Cada control (C-nn) declara su trazabilidad. El detalle económico de cada solución se desarrolla en la Fase 4; aquí se fija el **requisito funcional y el procedimiento**.

Notación de cada ficha de control:

> **C-nn — Nombre.** Remedia: `D-nn`. Mitiga: `R-nn`. Soporta (DRP): `E-nn`. Requiere inversión: `I-nn` (Fase 4). Marco: ISO 27001:2022 / CIS v8.1 / NIST CSF 2.0.

---

## 6.1 Clasificación y control de los bienes informáticos

Cubre **D-10** y **D-11**. Responde a la exigencia del enunciado §5.2 ("Sistemas operativos desactualizados → Clasificación y control de bienes informáticos").

### C-01 — Inventario único y confiable de activos de hardware y software

> Remedia: D-11. Mitiga: R-03. Soporta: E-05. Requiere: I-EDR/inventario. Marco: A.5.9 / CIS 1.1, 2.1 / ID.AM.

**Procedimiento.**
1. Desplegar una herramienta de descubrimiento e inventario que registre, para cada activo: identificador, tipo, ubicación (sede/sala), responsable, sistema operativo y versión, aplicaciones instaladas, estado de soporte, estado de parche, presencia de EDR y de cifrado, y segmento de red asignado.
2. Realizar un descubrimiento inicial en ambas sedes y conciliar contra los registros contables de activos.
3. Marcar todo activo no reconocido para investigación; ningún activo desconocido permanece conectado a la red (se articula con el NAC, C-26).
4. Actualización automática diaria; revisión de conciliación mensual por un administrador; auditoría semestral por el Oficial de Seguridad.
5. El inventario es la fuente de verdad para la gestión de parches (C-16), la respuesta a incidentes (§6.9) y el DRP (componentes críticos).

**Registro asociado:** R-1 Inventario de activos (Anexo B).

### C-02 — Clasificación de activos y de la información

> Remedia: D-11 (y habilita P-02). Mitiga: R-03, R-01. Marco: A.5.9–A.5.13 / CIS 3.1, 3.2, 3.7 / ID.AM-05.

**Procedimiento.**
1. Clasificar cada activo por criticidad de negocio en **Alta / Media / Baja**, según su impacto en pedidos, facturación electrónica y trazabilidad.
2. Clasificar la información en **Pública / Uso interno / Confidencial / Restringida** (P-02). Etiquetar repositorios y bases de datos; los datos del ERP, de clientes, de proveedores y de ubicación de la flotilla son mínimo Confidenciales.
3. Definir, por clasificación, las reglas de almacenamiento, transmisión (cifrado obligatorio para Confidencial y Restringida fuera de la red interna), copia, retención y destrucción segura.
4. Los activos de criticidad Alta se priorizan en la segmentación (C-25), la alta disponibilidad (C-13), el respaldo (C-08) y el monitoreo (C-29).

**Registro asociado:** R-1 (columna de clasificación); R-2 Catálogo de sistemas de información críticos.

### C-16 — Gestión del ciclo de vida y soporte de sistemas operativos y software

> Remedia: D-10. Mitiga: R-03, R-05. Soporta: E-05. Requiere: I-RenovaciónSO, I-Parches. Marco: A.8.8, A.8.19 / CIS 2.2, 2.3, 7.3, 7.4 / PR.PS-01, PR.PS-02.

**Situación actual.** Windows Server 2012 R2 sin soporte extendido desde el 10 de octubre de 2023; estaciones con Windows 7 (fin de soporte 14 de enero de 2020) y Windows 8.1 (10 de enero de 2023). Toda vulnerabilidad publicada desde esas fechas permanece explotable sin remedio del fabricante (Microsoft, 2022; 2023).

**Procedimiento.**
1. A partir del inventario (C-01), levantar la lista completa de sistemas fuera de soporte y clasificarlos por criticidad y exposición.
2. **Plan de migración priorizado** (se detalla y presupuesta en la Fase 4):
   a. Prioridad 1: servidores que sostienen el ERP y la base de datos backend de la DMZ → migrar a una versión con soporte vigente (Windows Server 2022/2025 o Linux empresarial con soporte).
   b. Prioridad 2: servidores de correo, archivos y directorio.
   c. Prioridad 3: estaciones de trabajo → migrar a un sistema operativo con soporte; reemplazar el hardware que no lo admita.
3. **Controles compensatorios** para todo sistema que no pueda migrarse dentro del plazo: aislamiento en un segmento restringido con ACL de denegación por defecto (C-25), sin acceso a Internet, con EDR (C-15), con reglas específicas en el WAF/IPS y con monitoreo reforzado en el SIEM. Cada excepción se documenta y aprueba (P-16).
4. **Gestión de parches centralizada:** desplegar un gestor de parches para sistema operativo y aplicaciones de terceros; ventana de despliegue de parches críticos ≤ 15 días naturales desde su publicación (≤ 72 horas para vulnerabilidades explotadas activamente), previa validación en un grupo piloto. Reporte mensual de cumplimiento de parcheo al Comité.
5. **Líneas base de configuración (hardening):** adoptar guías CIS Benchmarks para servidores, estaciones y dispositivos de red; verificar el cumplimiento con escaneo periódico.

**Registro asociado:** R-3 Estado de soporte y parcheo; R-7 Excepciones aprobadas.

---

## 6.2 Gestión del personal

Cubre **D-15** y **D-17** en su dimensión de personas y terceros. Responde a §5.2 ("Accesos permanentes de proveedores → Gestión del personal y terceros").

### C-03 — Seguridad en el ciclo de vida del empleo

> Remedia: D-15 (factor humano), habilita P-03. Mitiga: R-07, R-03. Marco: A.6.1–A.6.5 / CIS 6.1, 6.2 / PR.AA, GV.RR.

**Procedimiento.**
1. **Selección:** verificación de antecedentes proporcional al puesto (referencias laborales; verificación reforzada para puestos con acceso a datos Restringidos, finanzas o administración de sistemas).
2. **Contratación:** firma de acuerdo de confidencialidad y de aceptación del uso aceptable (P-06) antes de entregar credenciales; inducción de seguridad en la primera semana.
3. **Altas de acceso:** RR. HH. notifica a TI el mismo día; TI aprovisiona con base en un **perfil de acceso por puesto** (mínimo privilegio); toda excepción la aprueba la jefatura y el Oficial de Seguridad.
4. **Cambios de puesto:** se revocan los accesos del puesto anterior y se aprovisionan los del nuevo (no se acumulan privilegios).
5. **Bajas:** RR. HH. notifica el cese; TI revoca **todos** los accesos (dominio, correo, VPN, ERP, aplicaciones, físico) el mismo día; se recupera el equipo; se deshabilita y luego se elimina la cuenta según la retención definida.
6. Registro de cada alta, cambio y baja con fecha, responsable y evidencia.

**Registro asociado:** R-4 Altas/bajas/cambios de acceso.

### C-04 — Programa continuo de concientización en ciberseguridad

> Remedia: D-15. Mitiga: R-07. Soporta: E-04, E-05. Requiere: I-Concientización. Marco: A.6.3 / CIS 14.1–14.9 / PR.AT.

**Procedimiento.**
1. Capacitación de **inducción** obligatoria para todo ingreso y **refuerzo anual** para toda la plantilla (~480 personas), con registro de asistencia y evaluación mínima aprobatoria.
2. Contenidos mínimos: reconocimiento de phishing y de fraude de facturación (relevante por la operación con proveedores), manejo de información confidencial, uso de MFA y de la bóveda de contraseñas, reporte de incidentes, y seguridad en planta (no conectar dispositivos a la red OT).
3. **Simulacros de phishing** trimestrales; a quien falle se le asigna refuerzo dirigido; se mide la tasa de clic y de reporte como indicador (§6.9.7). No se usa con fin punitivo salvo reincidencia deliberada.
4. Campañas breves mensuales (cartel, correo, píldora formativa) alineadas a amenazas vigentes.
5. Formación específica para el personal de TI (hardening, respuesta a incidentes) y para roles de finanzas (verificación de cambios de cuenta bancaria de proveedores por doble canal).

**Registro asociado:** R-5 Capacitación y simulacros.

### C-05 — Alta, control y baja de accesos de terceros y proveedores

> Remedia: D-17. Mitiga: R-06. Soporta: E-04. Requiere: I-PAM/GestiónTerceros. Marco: A.5.19–A.5.22 / CIS 6.1, 6.2, 6.7 / GV.SC, PR.AA-05.

**Situación actual.** Cinco proveedores con acceso; el consultor del ERP con acceso remoto **permanente** y credenciales **no rotadas**; el integrador con contrato de soporte no vigente; el ISP sin SLA.

**Procedimiento.**
1. **Registro de terceros:** inventario de todos los proveedores con acceso, alcance, sistemas, tipo de acceso, contrato vigente, cláusulas de seguridad y NDA, y contacto responsable.
2. **Conversión del acceso permanente a bajo demanda:** cada proveedor recibe cuentas **individuales y nominadas**, con **MFA**, **fecha de expiración** y activación por solicitud (ventana de trabajo). Se elimina toda credencial compartida o embebida.
3. **Consultor del ERP:** revocar de inmediato el acceso permanente; recrear como acceso bajo demanda a través del portal de acceso privilegiado; rotar toda credencial que haya conocido; restringir a los objetos del ERP que su trabajo requiere.
4. **Acceso mediante jump host / portal de acceso privilegiado:** los terceros entran por un punto único controlado que aplica MFA, mínimo privilegio, **grabación de sesión** y registro; sin conexión directa a servidores desde Internet.
5. **Revisión trimestral** de todos los accesos de terceros; revocación inmediata al terminar el servicio o el contrato.
6. **Cierre contractual:** ningún proveedor opera sin contrato vigente con cláusulas de seguridad, SLA y NDA (C-06).

**Registro asociado:** R-8 Registro de accesos de terceros; R-9 Sesiones remotas de terceros.

### C-06 — Cláusulas de seguridad, SLA y NDA en contratos con terceros

> Remedia: D-17. Mitiga: R-06. Marco: A.5.20, A.5.21, A.5.22 / CIS 15.1–15.6 / GV.SC-06, GV.SC-07.

**Procedimiento.**
1. Definir un **anexo contractual de seguridad de la información** estándar que incluya: obligaciones de confidencialidad, requisitos de acceso (nominado, temporal, MFA, monitoreo), notificación de incidentes en ≤ 24 h, derecho de auditoría, requisitos de subcontratación, y penalizaciones por incumplimiento.
2. Incorporar el anexo a **todo contrato nuevo** y a la **renovación** de los existentes; para el ISP, exigir un **SLA de disponibilidad** con penalización; para el integrador, regularizar o sustituir el contrato de soporte.
3. Para el **SaaS de rastreo de flotilla:** exigir evidencia de controles del proveedor (certificación o cuestionario de seguridad), definir el tratamiento de los datos de ubicación (clasificados Confidenciales), y sustituir las credenciales estáticas embebidas por un mecanismo seguro (token en bóveda, C-07 y C-22).
4. Revisión anual del cumplimiento de las cláusulas por el Oficial de Seguridad y la Gerencia de TI.

**Registro asociado:** R-10 Contratos y cláusulas de seguridad de terceros.

### C-07 — Gestión de identidades no humanas y secretos de integración

> Remedia: D-01, D-17. Mitiga: R-01, R-06. Soporta: E-04. Requiere: I-GestiónSecretos. Marco: A.5.16, A.5.17, A.8.4 / CIS 5.4, 6.8 / PR.AA, PR.DS.

**Situación actual.** El Sistema de Rastreo de Flotilla usa credenciales estáticas embebidas en el código para integrarse con su proveedor SaaS; además, no existe evidencia de un inventario ni de una rotación formal de cuentas de servicio.

**Procedimiento.**
1. Inventariar cada cuenta de servicio, token, certificado, clave API y secreto de integración: propietario de negocio y técnico, sistema, privilegios, fecha de vencimiento y dependencia.
2. Retirar secretos del código fuente, archivos de configuración, scripts y bitácoras; almacenarlos únicamente en una **bóveda de secretos** con cifrado, control de acceso por rol, MFA para administradores y auditoría de lectura o modificación.
3. Aplicar mínimo privilegio, credenciales distintas por ambiente (desarrollo, pruebas y producción), caducidad y rotación documentada; revocar de inmediato secretos expuestos o vinculados a un proveedor cuyo contrato finalice.
4. Para la API de rastreo, migrar a un mecanismo de corta vigencia o certificado cuando el proveedor lo soporte; si no, mantener el token en bóveda y rotarlo según el contrato y ante cualquier sospecha de exposición.
5. Prohibir cuentas de servicio interactivas y su uso por personas. Las excepciones requieren aprobación del Oficial de Seguridad y fecha de vencimiento.

**Registro asociado:** R-18 Inventario de secretos en bóveda; R-8 Registro de accesos de terceros.

---

## 6.3 Seguridad física y ambiental

Cubre **D-12** y **D-13**. Responde a §5.2 ("Datacenter sin protección perimetral física → Seguridad física y ambiental").

### C-12 — Protección física y ambiental del centro de datos y de los cuartos de telecomunicaciones

> Remedia: D-12, D-13. Mitiga: R-10, R-09. Soporta: E-01, E-07. Requiere: I-ControlAccesoFísico, I-CCTV, I-MonitoreoAmbiental, I-UPS, I-Planta. Marco: A.7.1–A.7.4, A.7.8, A.7.11 / CIS 1.1 / PR.IR-02, PR.AA-06.

**Procedimiento.**

**(a) Control de acceso físico.**
1. Instalar control de acceso por **tarjeta o biométrico** en la puerta del centro de datos (Casa Matriz) y del cuarto de telecomunicaciones (Planta), con **bitácora electrónica** de cada ingreso y egreso (persona, fecha, hora).
2. Autorización de acceso por lista nominal aprobada por la Gerencia de TI; revisión semestral.
3. Acceso de terceros solo acompañado y con registro manual adicional (formato R-11).
4. Retirar el esquema de llave física compartida una vez operativo el nuevo control (conservar una llave de emergencia en caja sellada con registro de apertura).

**(b) Videovigilancia (CCTV).**
5. Cobertura completa de la puerta, los pasillos de racks y la entrada del cuarto de la Planta.
6. Grabación en NVR con **retención mínima de 30 días** (supuesto S-02); acceso a las grabaciones restringido y registrado.
7. Sincronización horaria de las cámaras con la fuente NTP central para correlación con el SIEM.

**(c) Monitoreo ambiental.**
8. Sensores de **temperatura, humedad, fuga de agua y estado del suministro eléctrico** en el centro de datos y en el cuarto de la Planta.
9. Alertas automáticas (correo y mensajería) al personal de TI y al Oficial de Seguridad ante umbrales fuera de rango; prueba mensual de las alertas.
10. Integración de los eventos ambientales al SIEM (C-29) y al procedimiento de activación del DRP (Fase 3).

**(d) Energía de respaldo.**
11. Dimensionar el **UPS** para una autonomía suficiente para un apagado ordenado de la carga crítica y para cubrir el arranque de la planta (referencia de diseño: 60–90 minutos de la carga crítica; el valor exacto y el equipo se definen en la Fase 4).
12. Instalar **planta eléctrica** de respaldo con transferencia automática (ATS) para eventos prolongados; contrato de mantenimiento y prueba con carga mensual.
13. Procedimiento de apagado ordenado automatizado si la autonomía del UPS se agota antes de estabilizarse la planta.

**Registros asociados:** R-11 Bitácora de acceso físico; R-12 Pruebas de UPS/planta y de alertas ambientales.

---

## 6.4 Seguridad de operaciones

Cubre **D-02** (continuidad de servicios críticos de red, enlazado al DRP) y **D-10** (gestión de cambios y parches; el parcheo se detalla en C-16). Responde a §5.2 ("Firewall sin alta disponibilidad → Seguridad de operaciones").

### C-13 — Alta disponibilidad de los servicios críticos de red

> Remedia: D-02. Mitiga: R-02, R-09 (por dependencia energética del borde). Soporta: E-01, E-02. Requiere: I-NGFW-HA. Marco: A.8.14 / CIS 12.2 / PR.IR-03, RC.RP.

**Situación actual.** Un único firewall perimetral, sin clúster; su fallo de hardware aísla toda la Casa Matriz y, con ella, a la Planta (que depende de la VPN sobre el mismo borde).

**Procedimiento.**
1. Sustituir el firewall único por un **clúster de dos NGFW en alta disponibilidad activo-pasivo** con sincronización de estado de sesión, en el borde entre Internet, DMZ y red interna.
2. Habilitar **IPS** integrado, control de aplicaciones e inspección TLS donde sea legalmente admisible y técnicamente viable.
3. Alimentar cada nodo del clúster desde una fase eléctrica distinta y ambas por UPS (articula con C-12(d)).
4. **Gestión de configuración del firewall:** repositorio de reglas versionado, revisión de cambios por el Comité de Cambios (C-17), respaldo diario de la configuración, y revisión semestral de la base de reglas para eliminar reglas obsoletas o permisivas.
5. **Prueba de conmutación (failover)** planificada semestral, documentada; es también un caso de prueba del DRP (E-02).
6. Monitoreo del estado del clúster en el SIEM (C-29) con alerta ante conmutación o pérdida de un nodo.

**Registro asociado:** R-13 Cambios y pruebas de la infraestructura de red.

### C-17 — Gestión de cambios

> Remedia: D-10 (introducción controlada de sistemas), habilita P-10. Mitiga: R-01, R-03. Soporta: E-04, E-05. Marco: A.8.32 / CIS 4.2 / PR.PS-01, ID.RA.

**Procedimiento.**
1. Todo cambio en producción (servidores, red, firewall, aplicaciones publicadas, reglas de WAF, políticas de NAC) se solicita en un **formulario de cambio** con: descripción, motivo, análisis de riesgo e impacto, plan de implementación, plan de reversión y ventana propuesta.
2. **Comité de Cambios** (Gerencia de TI, administradores, Oficial de Seguridad) clasifica el cambio (estándar / normal / urgente) y lo aprueba o rechaza.
3. Los cambios se ejecutan en **ventana de mantenimiento** comunicada; los cambios estándar preaprobados siguen un procedimiento documentado.
4. **Cambios de emergencia:** se ejecutan con autorización verbal de la Gerencia de TI y se documentan dentro de las 24 horas siguientes.
5. Registro del resultado (éxito / reversión) y actualización del inventario y de la documentación.
6. Prohibido publicar o modificar un servicio en la DMZ sin: revisión de seguridad, prueba de la protección WAF (C-19) y verificación del hardening (C-16.5).

**Registro asociado:** R-13; R-14 Bitácora de cambios de aplicaciones.

### C-18 — Segregación de funciones y de ambientes; endurecimiento operativo

> Remedia: D-06 (cuentas y acciones administrativas), D-17 (operación de terceros). Mitiga: R-03, R-06. Marco: A.5.3, A.8.31 / CIS 4.1, 4.7 / PR.PS, PR.AA.

**Procedimiento.**
1. Separar los ambientes de **desarrollo, pruebas y producción** de las aplicaciones (en especial las de la DMZ); los datos de producción no se copian a pruebas sin anonimizar.
2. Ninguna persona aprueba y ejecuta sola un cambio crítico (segregación de funciones); las acciones administrativas se realizan con cuentas nominadas (C-15) y quedan registradas.
3. Deshabilitar servicios, puertos y cuentas por defecto no utilizados en todos los sistemas; retirar software innecesario.
4. Sincronización horaria (NTP) centralizada y obligatoria en todos los activos para la fiabilidad de las bitácoras.
5. Documentar los procedimientos operativos estándar (respaldo, restauración, alta/baja de usuario, publicación de servicio, respuesta a incidente) y mantenerlos accesibles al personal autorizado.

**Registro asociado:** R-15 Procedimientos operativos estándar (índice y versión).

---

## 6.5 Identificación, autenticación y control de acceso

Cubre **D-05** y **D-06**. Responde a §5.2 ("Sin 2FA en accesos internos → Identificación, autenticación y control de acceso").

### C-15 — Cuentas nominadas, mínimo privilegio y gestión de identidades privilegiadas

> Remedia: D-06, D-05. Mitiga: R-03, R-07, R-06. Soporta: E-04, E-05. Requiere: I-MFA, I-PAM. Marco: A.5.15–A.5.18, A.8.2 / CIS 5.1–5.6, 6.1, 6.2, 6.8 / PR.AA-01, PR.AA-05.

**Situación actual.** Cuentas administrativas compartidas entre el personal de TI; imposible auditar quién hizo qué.

**Procedimiento.**
1. **Eliminar las cuentas administrativas compartidas.** Crear una cuenta administrativa **nominada** por cada administrador, separada de su cuenta de usuario normal (cuenta de trabajo vs. cuenta de administración).
2. **Mínimo privilegio:** asignar privilegios por rol y por necesidad; ningún usuario estándar tiene derechos de administrador local en su estación.
3. **Gestión de accesos privilegiados (PAM):** las credenciales de administración y de servicio se custodian en una **bóveda**; el acceso privilegiado se solicita, se aprueba, es **temporal (just-in-time)**, con **grabación de sesión** y rotación automática de la credencial tras el uso.
4. **Cuentas de servicio y de integración:** nominadas a un sistema, sin interactividad, con contraseña larga y rotada, custodiadas en la bóveda; **nunca embebidas en código** (aplica de inmediato al Sistema de Rastreo de Flotilla, C-07).
5. **Revisión de accesos:** recertificación **semestral** de todos los accesos por las jefaturas; revisión **trimestral** de las cuentas privilegiadas y de terceros; baja inmediata de cuentas sin uso 90 días o de personal que causó baja.
6. Registro centralizado de eventos de autenticación y de uso privilegiado en el SIEM (C-29).

**Registro asociado:** R-16 Cuentas privilegiadas; R-4 Altas/bajas.

### C-22 — Autenticación multifactor (MFA)

> Remedia: D-05. Mitiga: R-03, R-07, R-06. Soporta: E-04, E-05. Requiere: I-MFA. Marco: A.5.17, A.8.5 / CIS 6.3, 6.4, 6.5 / PR.AA-02, PR.AA-03.

**Procedimiento.**
1. **Activar MFA obligatorio** para: VPN y acceso remoto, correo corporativo (incluido webmail), inicio de sesión en el dominio para cuentas privilegiadas, consolas de administración de servidores y de red, plataforma del ERP con perfiles administrativos, y todos los accesos de terceros.
2. **MFA resistente a phishing** (FIDO2/WebAuthn con llave de seguridad, o certificado en dispositivo gestionado) para cuentas privilegiadas y de administración; para el resto de usuarios se admite aplicación de autenticación (TOTP/push con verificación de número), evitando SMS salvo como último recurso (Cybersecurity and Infrastructure Security Agency, 2022).
3. **Contraseñas** (P-05): longitud mínima 14 caracteres para usuarios y 20 para cuentas privilegiadas y de servicio; verificación contra listas de contraseñas comprometidas; sin expiración forzada periódica si hay MFA y detección de compromiso, conforme a NIST SP 800-63B; bloqueo temporal tras intentos fallidos.
4. **Single Sign-On (SSO)** contra el directorio para las aplicaciones que lo admitan, de modo que la baja de una identidad revoque el acceso en todas. La gestión de cuentas de servicio, tokens y secretos de aplicación se realiza bajo C-07.

**Registro asociado:** R-17 Cobertura de MFA por sistema.

---

## 6.6 Seguridad ante programas malignos

Cubre **D-11**. Responde a §5.1 punto 6 ("Seguridad ante programas malignos (antivirus/EDR)").

### C-28 — Plataforma de detección y respuesta en endpoint (EDR)

> Remedia: D-11. Mitiga: R-03. Soporta: E-05, E-04. Requiere: I-EDR. Marco: A.8.7 / CIS 10.1–10.7 / PR.PS-05, DE.CM-01.

**Situación actual.** Antivirus de solo firmas, desactualizado en varias estaciones; sin EDR; sin capacidad de contención.

**Procedimiento.**
1. Desplegar **EDR** en el 100 % de servidores y estaciones (ambas sedes), administrado desde una consola central en la nube o en sitio.
2. Configuración: protección en tiempo real, análisis de comportamiento, prevención de ejecución de scripts y de macros no firmadas, control de dispositivos USB, y **aislamiento remoto** del equipo comprometido con un clic.
3. Retirar el antivirus de solo firmas tras verificar la cobertura del EDR (evitar conflictos de dos agentes).
4. **Telemetría al SIEM** (C-29): alertas de EDR correlacionadas con eventos de red, identidad y correo.
5. Política de respuesta: ante detección de alta severidad, aislamiento automático del host y notificación al canal de incidentes (§6.9).
6. Revisión mensual de detecciones, exclusiones y estado de los agentes; ningún host productivo sin agente activo (se valida por NAC, C-26, y por el inventario, C-01).
7. Para los sistemas fuera de soporte que no admitan el agente moderno: aislamiento reforzado (C-16.3) y monitoreo por red (NDR, C-29b).

**Registro asociado:** R-19 Estado de despliegue y detecciones de EDR.

### C-21b — Protección del correo contra malware y phishing (complemento de §6.8)

> Remedia: D-15. Mitiga: R-07. Soporta: E-05. Requiere: I-FiltradoCorreo. Marco: A.8.7, A.8.23 / CIS 9.6, 9.7 / PR.PS-05, DE.CM-09.

**Procedimiento.**
1. Habilitar filtrado avanzado de correo: análisis de adjuntos en entorno aislado (sandbox), reescritura y análisis de enlaces en el momento del clic, y detección de suplantación del dominio propio y de dominios similares.
2. Cuarentena de correo sospechoso con liberación controlada; botón de "reportar phishing" en el cliente de correo, integrado con el flujo de incidentes.
3. Publicar y endurecer **SPF, DKIM y DMARC** (C-21c) para reducir la suplantación del dominio de TransAgro.

**Registro asociado:** R-5 (integración con simulacros); R-20 Métricas de correo bloqueado.

---

## 6.7 Respaldo de la información

Cubre **D-14**. Responde a §5.1 punto 6 ("Respaldo de la información (política, pruebas de restauración)").

### C-08 — Plataforma y modelo de respaldo 3-2-1-1-0

> Remedia: D-14. Mitiga: R-05. Soporta: E-01, E-05, E-06, E-07. Requiere: I-Respaldo. Marco: A.8.13 / CIS 11.1–11.5 / PR.DS-11, RC.RP.

**Situación actual.** Respaldos en **cinta local** guardados en el **mismo cuarto** que los servidores de producción; sin copia externa, sin copia inmutable, sin pruebas de restauración.

**Procedimiento.**
1. Adoptar el modelo **3-2-1-1-0** como regla operativa: **3** copias de los datos, en **2** medios distintos, **1** copia **fuera de sitio**, **1** copia **inmutable o aislada (air-gapped)**, y **0** errores verificados por prueba. CISA respalda mantener copias cifradas, desconectadas o inmutables y probar regularmente su disponibilidad e integridad (Cybersecurity and Infrastructure Security Agency, 2023).
2. **Arquitectura objetivo (se presupuesta en la Fase 4):**
   a. Copia primaria en disco en el centro de datos (restauración rápida).
   b. Copia secundaria replicada a la **Planta de Chiquimula** (otro sitio físico) o a un repositorio en la nube.
   c. Copia **inmutable** mediante bloqueo de objeto (object lock) en almacenamiento en la nube o en un repositorio endurecido, fuera del dominio de administración de producción (una credencial comprometida de TI no puede borrarla).
3. Alcance mínimo: base de datos del ERP, servidores de archivos, servidor de correo, configuración de servidores y de dispositivos de red, servidores de la DMZ, y la configuración del directorio.
4. Frecuencia alineada al RPO que fije el DRP (Fase 3); como referencia de diseño de este Plan: respaldo de la base de datos del ERP al menos cada 4 horas y respaldo diario del resto.
5. Retirar progresivamente la cinta local; si se conserva por transición, sacarla del cuarto de servidores a una ubicación con control ambiental y de acceso.

**Registro asociado:** R-21 Ejecución y estado de respaldos.

### C-09 — Pruebas de restauración calendarizadas

> Remedia: D-14. Mitiga: R-05. Soporta: E-05, E-06. Marco: A.8.13 / CIS 11.5 / RC.RP-01, ID.IM-02.

**Procedimiento.**
1. **Calendario anual** de pruebas de restauración con responsables asignados:
   - Restauración de archivos puntuales: mensual.
   - Restauración de la base de datos del ERP a un entorno aislado: trimestral, con verificación de integridad y de arranque de la aplicación.
   - Restauración completa de un servidor crítico (bare-metal / máquina virtual): semestral.
   - Ejercicio conjunto con el DRP (Fase 3): anual.
2. Cada prueba mide el **tiempo real de restauración** y lo compara con el RTO objetivo; las desviaciones generan acción correctiva.
3. La verificación automática de recuperabilidad de la plataforma (arranque y prueba de la copia) se ejecuta tras cada ciclo de respaldo (el "0" del modelo 3-2-1-1-0).
4. Resultados reportados al Comité de Seguridad y archivados como evidencia de auditoría.

**Registro asociado:** R-22 Resultados de pruebas de restauración.

### C-10 — Cifrado, retención y protección de los respaldos

> Remedia: D-14. Mitiga: R-05. Marco: A.8.13, A.8.24 / CIS 11.3 / PR.DS-10, PR.DS-11.

**Procedimiento.**
1. **Cifrado** de los respaldos en tránsito y en reposo; las claves se custodian por separado de los datos y del dominio de administración de producción.
2. **Política de retención documentada y aprobada** por clasificación y por tipo de sistema; como referencia: respaldos diarios 30 días, semanales 3 meses, mensuales 12 meses, anuales según requisito legal y contable de Guatemala (a confirmar con el área legal/contable).
3. Control de acceso a la consola de respaldo con cuentas nominadas y MFA (C-15, C-22); las acciones de borrado requieren doble aprobación.
4. Monitoreo en el SIEM de los eventos de la plataforma de respaldo (fallos, borrados, cambios de política).

**Registro asociado:** R-23 Política de retención vigente.

---

## 6.8 Seguridad en redes

Cubre **D-01, D-03, D-04, D-07, D-08, D-09**. Responde a tres correspondencias literales del §5.2: DMZ sin WAF/Honeypot/Anti-DDoS/DNS → control de publicación de servicios y protección de apps web; VPN antigua → comunicaciones entre sedes; red plana → segmentación y control de acceso a la red.

### C-25 — Segmentación de la red en zonas por función y por nivel de confianza

> Remedia: D-07, D-09. Mitiga: R-03. Soporta: E-04, E-05. Requiere: I-Segmentación, I-Switching. Marco: A.8.22, A.8.20 / CIS 12.2, 12.4 / PR.IR-01, PR.AA-05.

**Situación actual.** Red plana /16 sin VLAN; estaciones, servidores, impresoras, cámaras IP y PLC en la misma subred sin ACL.

**Procedimiento.**
1. **Diseño de segmentación** en VLAN y subredes por función, con denegación por defecto entre segmentos y reglas explícitas de comunicación:
   - Usuarios administrativos (por área si aplica).
   - Servidores de aplicación interna (ERP, correo, archivos, directorio).
   - Servidores de gestión / administración (consolas, PAM, SIEM).
   - DMZ de servicios publicados (rediseñada, C-14).
   - Impresión y periféricos.
   - **Cámaras IP / videovigilancia** (segmento aislado, sin salida a Internet salvo lo estrictamente necesario).
   - **OT / PLC de planta:** zona dedicada conforme al modelo de **zonas y conductos de ISA/IEC 62443**; comunicación con el resto de la red solo a través de un "conducto" controlado (firewall industrial o reglas específicas), sin acceso directo desde usuarios ni desde Internet. La separación IT/OT y el filtrado explícito de los flujos reducen la exposición y el movimiento lateral (Cybersecurity and Infrastructure Security Agency, 2022).
   - Invitados (aislada, solo Internet; ver C-27).
   - Gestión de dispositivos de red (out-of-band).
2. **Principio Zero Trust** (NIST SP 800-207): el acceso entre zonas se concede por identidad, necesidad y postura del dispositivo, no por pertenecer a la red interna; se evita la confianza implícita de la red plana actual.
3. **Microsegmentación** de los servidores más críticos (ERP y base de datos) para limitar el movimiento lateral incluso dentro de la zona de servidores.
4. **Implementación por fases** para no interrumpir la operación: primero aislar OT y cámaras (mayor riesgo físico), luego separar servidores de usuarios, luego microsegmentar el ERP.
5. Todas las reglas inter-VLAN se documentan, se versionan y se revisan semestralmente (C-13.4).

**Registro asociado:** R-24 Matriz de segmentación y reglas inter-zona.

### C-26 — Control de acceso a la red (NAC) con 802.1X

> Remedia: D-09. Mitiga: R-03. Soporta: E-05. Requiere: I-NAC. Marco: A.8.20 / CIS 13.9 / PR.AA-05, DE.CM-07.

**Situación actual.** Sin NAC; cualquier dispositivo conectado a un punto de red obtiene IP y acceso.

**Procedimiento.**
1. Desplegar **NAC con autenticación 802.1X** por puerto en el switching cableado y en la WLAN corporativa.
2. **Política de admisión:** solo se otorga acceso a la VLAN correspondiente si el dispositivo se autentica (certificado de máquina para equipos gestionados; credenciales para casos definidos) **y** cumple la postura mínima (EDR activo, parches al día, cifrado activo).
3. **Perfilado** de dispositivos que no hacen 802.1X (impresoras, cámaras, PLC): identificación por características y asignación estática a su VLAN aislada; cualquier desviación genera alerta.
4. **Cuarentena automática** de los dispositivos no conformes o desconocidos en una VLAN de remediación sin acceso a recursos internos.
5. Modo de despliegue: primero **monitor (sin bloquear)** para inventariar y ajustar, luego **enforcement**.
6. Eventos de NAC enviados al SIEM (C-29).

**Registro asociado:** R-25 Eventos de admisión y cuarentena NAC.

### C-27 — Red inalámbrica corporativa segmentada (WPA3-Enterprise) y red de invitados aislada

> Remedia: D-08. Mitiga: R-03. Soporta: E-05. Requiere: I-WLAN. Marco: A.8.20, A.8.22 / CIS 12.6, 15.4 / PR.AA-05, PR.IR-01.

**Situación actual.** Una sola clave WPA2-Personal compartida por personal y visitantes; sin SSID de invitados aislado; sin portal cautivo.

**Procedimiento.**
1. **SSID corporativo** con **WPA3-Enterprise (802.1X)** contra el directorio; preferir autenticación por **certificado (EAP-TLS)** para admitir solo equipos gestionados. El diseño debe validar compatibilidad de clientes y puntos de acceso antes de retirar WPA2-Enterprise durante la migración.
2. **SSID de invitados** completamente **aislado** de la red interna (solo Internet), con **portal cautivo**, credenciales temporales o self-service con caducidad, límite de ancho de banda y **aislamiento de clientes** (client isolation). Como alternativa moderna, WPA3-Enhanced Open (OWE) para cifrar la sesión de invitado sin contraseña compartida.
3. Retirar la clave WPA2-Personal única una vez migrados los equipos corporativos.
4. **WIPS** (detección de puntos de acceso no autorizados) activo; alerta ante rogue AP.
5. Los puntos de acceso se gestionan de forma centralizada; su tráfico de gestión va por la VLAN de administración.

**Registro asociado:** R-26 SSID, políticas WLAN y credenciales de invitado emitidas.

### C-19 — Web Application Firewall (WAF) para las aplicaciones publicadas

> Remedia: D-01. Mitiga: R-01. Soporta: E-04. Requiere: I-WAF. Marco: A.8.26, A.8.20, A.8.23 / CIS 13.10 / PR.PS-01, DE.CM-01.

**Situación actual.** Portal de Clientes, Portal de Proveedores y Sistema de Rastreo de Flotilla en la DMZ **sin filtrado de capa de aplicación**.

**Procedimiento.**
1. Publicar las tres aplicaciones **detrás de un WAF** (servicio en la nube como proxy inverso, o appliance virtual en la DMZ; la elección se justifica en la Fase 4).
2. Conjunto de reglas base contra **OWASP Top 10:2025** (inyección, control de acceso roto, mala configuración, fallos criptográficos, entre otros) (Open Worldwide Application Security Project, 2025).
3. Reglas específicas por aplicación:
   - Portal de Proveedores: **validación estricta de carga de archivos** (tipo real por contenido, tamaño, análisis antimalware, almacenamiento fuera de la raíz web, nombres saneados).
   - Portal de Clientes: limitación de tasa, protección contra abuso de autenticación y contra enumeración; bloqueo de patrones de inyección hacia la base de datos.
   - Rastreo de Flotilla: control de los endpoints de API expuestos; ocultar cabeceras y mensajes de error que revelen tecnología.
4. Despliegue inicial en modo **detección**, ajuste de falsos positivos, y paso a **bloqueo** en un plazo definido.
5. Registro del WAF integrado al SIEM (C-29); alertas por ataques sostenidos.
6. Ningún servicio nuevo se publica sin WAF (P-07, C-17).

**Registro asociado:** R-27 Reglas WAF y eventos bloqueados.

### C-20 — Protección Anti-DDoS

> Remedia: D-01. Mitiga: R-01, R-02 (disponibilidad del enlace). Soporta: E-08. Requiere: I-AntiDDoS. Marco: A.8.20, A.8.6 / CIS 13.10 / PR.IR-04, DE.CM-01.

**Procedimiento.**
1. Contratar mitigación **volumétrica y de capa de aplicación** mediante un proveedor especializado (scrubbing en la nube) o servicio administrado del ISP/CDN.
2. Proteger los nombres públicos de las tres aplicaciones y los registros del correo saliente.
3. Definir umbrales y perfiles de tráfico normal; alertas al canal de incidentes ante activación de mitigación.
4. Runbook de DDoS en el plan de respuesta a incidentes (§6.9) y en el DRP (E-08): contactos del proveedor, procedimiento de conmutación y comunicación a clientes.
5. Prueba anual coordinada con el proveedor.

**Registro asociado:** R-28 Eventos de mitigación DDoS.

### C-21 — Protección y filtrado de DNS

> Remedia: D-01. Mitiga: R-01, R-03, R-07. Soporta: E-04, E-05. Requiere: I-DNSSecurity. Marco: A.8.20 / CIS 9.2 / PR.PS, DE.CM-09.

**Procedimiento.**
1. Dirigir la resolución DNS de **usuarios e infraestructura** a un servicio de **DNS seguro** que bloquee dominios maliciosos, de phishing, de mando y control y de reciente registro.
2. Aplicar la política tanto en la red interna como en los equipos portátiles fuera de la oficina (agente o perfil).
3. Registrar y enviar al SIEM las consultas bloqueadas; investigar picos o consultas a dominios de C2.
4. Endurecer los servidores DNS internos (consultas recursivas restringidas, protección contra envenenamiento de caché).

**Registro asociado:** R-29 Consultas DNS bloqueadas.

### C-14 — Rediseño de la DMZ y capa de servicios intermedia hacia el ERP

> Remedia: D-01. Mitiga: R-01. Soporta: E-04. Requiere: I-WAF, I-Segmentación. Marco: A.8.22, A.8.26 / CIS 12.2 / PR.IR-01, PR.PS-01.

**Situación actual.** Las tres aplicaciones comparten segmento y base de datos backend; el Portal de Clientes se conecta **directamente a la base de datos del ERP interno**, sin capa de servicios.

**Procedimiento.**
1. **Separar las tres aplicaciones** en subsegmentos de DMZ distintos, sin visibilidad de red entre ellas salvo lo necesario.
2. Introducir una **capa de servicios (API) intermedia** en un segmento propio entre la DMZ y la red interna: los portales consumen la API, y solo la API —con credenciales de servicio en bóveda (C-22) y consultas parametrizadas— accede a la base de datos, que **deja de ser alcanzable desde la DMZ**.
3. La base de datos del ERP solo acepta conexiones desde la capa de servicios y desde la red de administración; se retira toda regla que permita a la DMZ llegar a la base de datos.
4. **Endurecer** los servidores de la DMZ (C-16.5), retirar servicios innecesarios y actualizar/rehospedar el framework desactualizado del Portal de Clientes.
5. Revisión de seguridad y prueba de intrusión de la nueva arquitectura antes de pasar a producción (C-11).
6. Opción de **Honeypot/Deception** (señuelos que simulan servicios reales) en la DMZ y en segmentos internos críticos para detección temprana de reconocimiento y movimiento lateral; su adquisición se valora en la Fase 4.

**Registro asociado:** R-14; R-24.

### C-23 — Reemplazo de la VPN sitio a sitio y evaluación de SD-WAN

> Remedia: D-03. Mitiga: R-08. Soporta: E-03. Requiere: I-SD-WAN/VPN. Marco: A.8.24, A.8.21 / CIS 3.10, 12.7 / PR.DS-02, PR.IR-01.

**Situación actual.** Túnel IPsec de más de 6 años con **IKEv1 / 3DES / SHA-1**, sin enlace de respaldo.

**Procedimiento.**
1. Sustituir la configuración por la **configuración objetivo (supuesto S-03):** **IKEv2**, cifrado **AES-256-GCM**, integridad **SHA-256 o superior**, grupo Diffie-Hellman **19/20 o superior**, **PFS habilitado**. Prohibidos IKEv1, 3DES y SHA-1 (RFC 9395; NIST, 2022; NIST SP 800-131A Rev. 2).
2. Renovar los equipos terminales de VPN si el hardware actual no soporta la configuración objetivo (se dimensiona en la Fase 4).
3. **Evaluar SD-WAN** para: seleccionar dinámicamente la mejor ruta, usar un **enlace de respaldo** (segundo ISP o enlace celular) y cifrar de extremo a extremo entre sedes.
4. Autenticación del túnel por **certificados** (no por clave precompartida) donde el equipo lo permita.
5. Monitoreo del estado del túnel en el SIEM; alerta ante caída y conmutación.
6. Prueba de conmutación al enlace de respaldo semestral (caso de prueba de E-03 en el DRP).

**Registro asociado:** R-13; R-30 Configuración criptográfica vigente de la VPN.

### C-24 — Redundancia del enlace a Internet

> Remedia: D-04. Mitiga: R-02, R-08. Soporta: E-08. Requiere: I-SegundoISP. Marco: A.8.14 / CIS 12.2 / PR.IR-03, RC.RP.

**Procedimiento.**
1. Contratar un **segundo proveedor de Internet** con **ruta física distinta** para la Casa Matriz y, en lo posible, para la Planta.
2. Configurar **failover/balanceo** automático en el clúster de firewalls o en el SD-WAN (C-13, C-23).
3. Exigir **SLA de disponibilidad** con penalización a ambos proveedores (C-06).
4. Documentar el procedimiento de conmutación y los contactos en el DRP (E-08).
5. Prueba de failover semestral.

**Registro asociado:** R-13; R-10 (SLA de proveedores).

---

## 6.9 Gestión de incidentes de seguridad

Cubre **D-16**. Responde a la correspondencia literal del §5.2 ("Sin SIEM ni plan de respuesta a incidentes → Gestión de incidentes de seguridad"). Se basa en NIST SP 800-61 Rev. 3 (National Institute of Standards and Technology, 2025).

### C-29 — Centralización y correlación de eventos (SIEM) y monitoreo

> Remedia: D-16. Mitiga: R-04. Soporta: todos los escenarios del DRP. Requiere: I-SIEM, I-Observabilidad. Marco: A.8.15, A.8.16 / CIS 8.1–8.12 / DE.CM, DE.AE.

**Procedimiento.**
1. Desplegar una **plataforma SIEM** que recolecte, normalice y correlacione eventos de: firewalls y clúster HA, WAF, Anti-DDoS, DNS seguro, NAC, WLAN/WIPS, EDR, servidores y directorio, plataforma de respaldo, sensores ambientales, y accesos privilegiados y de terceros.
2. **Fuentes y retención:** definir el catálogo de fuentes obligatorias; retención en línea mínima 90 días y archivado 12 meses (a ajustar con requisitos legales).
3. **Casos de uso de detección** iniciales, alineados a los escenarios del DRP: fuerza bruta y viaje imposible de autenticación; ejecución sospechosa en endpoint; conexión de la DMZ hacia la base de datos (debe ser cero tras C-14); tráfico de un PLC hacia Internet; conmutación del firewall o del enlace; borrado o fallo de respaldos; consultas DNS a C2; picos de tráfico (DDoS).
4. **Sincronización horaria** (NTP) obligatoria en todas las fuentes (C-18.4).
5. **NDR / IDS-IPS complementario (C-29b):** análisis del tráfico de la red interna ya segmentada para detectar patrones que evadan el perímetro (especialmente hacia/desde OT y servidores críticos).
6. **Observabilidad de infraestructura:** monitoreo de disponibilidad y capacidad de servidores, enlaces y switches, con tableros y alertas proactivas.
7. **Operación:** el SIEM lo opera el Analista SOC N1 (interno o MDR tercerizado); alertas de severidad alta escalan de inmediato al Especialista en Respuesta a Incidentes y al Oficial de Seguridad.

**Registro asociado:** R-31 Catálogo de fuentes y casos de uso del SIEM; R-32 Bitácora de alertas.

### C-30 — Plan de respuesta a incidentes de seguridad

> Remedia: D-16. Mitiga: R-04. Soporta: E-02, E-03, E-04, E-05, E-06, E-08. Requiere: I-TalentoSOC. Marco: A.5.24–A.5.28 / CIS 17.1–17.9 / RS, RC.

**Procedimiento.**

**6.9.1 Alcance y ciclo.** NIST SP 800-61r3 integra la respuesta a incidentes en las seis funciones de NIST CSF 2.0 (Gobernar, Identificar, Proteger, Detectar, Responder y Recuperar), en lugar de prescribir el ciclo lineal de la revisión 2. Para operar el Plan, TransAgro adopta el flujo interno **preparación; detección y análisis; contención; erradicación; recuperación; actividad post-incidente**, con mejora continua y evidencias en cada etapa (National Institute of Standards and Technology, 2025).

**6.9.2 Roles.** Coordinador del incidente (Oficial de Seguridad o su suplente); equipo técnico (administradores, SOC N1, Incident Responder); apoyo (RR. HH., Legal, Comunicación); autoridad de decisión (Gerencia de TI; Gerencia General para incidentes graves). Los roles se designan **por función, no por nombre** (coherente con el DRP).

**6.9.3 Clasificación por severidad.**

| Severidad | Criterio | Ejemplos | Tiempo objetivo de primera respuesta |
|---|---|---|---|
| **Crítica** | Afecta un servicio crítico (ERP, correo, enlace entre sedes) o hay compromiso confirmado de datos Confidenciales/Restringidos, ransomware activo o intrusión con movimiento lateral. | Cifrado de servidores; compromiso de la BD del ERP desde la DMZ; caída del clúster de firewalls. | ≤ 15 minutos; activación del DRP según criterio (Fase 3). |
| **Alta** | Compromiso de un endpoint o cuenta sin propagación confirmada; intento de intrusión con indicios de éxito parcial. | EDR aísla una estación con troyano; phishing con credenciales entregadas. | ≤ 1 hora. |
| **Media** | Evento contenido por los controles; sin impacto en servicio ni datos. | WAF bloquea un ataque sostenido; malware bloqueado en correo. | ≤ 8 horas. |
| **Baja** | Anomalía menor o falso positivo con seguimiento. | Consulta DNS bloqueada aislada. | ≤ 2 días hábiles. |

**6.9.4 Detección y reporte.** Canales: alertas del SIEM/EDR; **buzón y número únicos de reporte** para el personal; botón de "reportar phishing". Todo colaborador está obligado a reportar (P-12). El SOC N1 hace el triaje inicial y abre el **registro del incidente** (R-33).

**6.9.5 Runbooks por tipo de incidente** (procedimiento paso a paso; se coordinan con los escenarios del DRP):

- **Phishing / compromiso de credenciales (→ E-04):** confirmar; deshabilitar la cuenta y revocar sesiones/tokens; forzar restablecimiento con MFA; revisar reglas de reenvío y accesos recientes; buscar el mismo correo en otros buzones y purgar; bloquear remitente/dominio y URL en el filtro de correo y en el DNS; lección aprendida y refuerzo de concientización.
- **Endpoint comprometido / malware (→ E-05):** aislar el host con el EDR; identificar el paciente cero y el vector; buscar indicadores en el resto del parque (EDR + SIEM); erradicar o reimaginar el equipo; restaurar datos desde respaldo limpio (C-08); reincorporar tras verificación; revisar por qué evadió los controles.
- **Ransomware (→ E-05):** declarar incidente crítico; **aislar** los segmentos afectados (apoyado en la segmentación C-25); no apagar en frío los equipos si se necesita evidencia de memoria; identificar la variante y el alcance; **no pagar**; recuperar desde la copia **inmutable** (C-08) al último punto limpio; reconstruir identidades y credenciales; endurecer y monitorear; informe a Dirección y, si aplica, a autoridades y afectados; activar el DRP (Fase 3).
- **Intrusión en la DMZ con movimiento lateral (→ E-04):** contener la aplicación afectada (aislarla o sacarla de servicio tras el WAF); verificar que la base de datos del ERP no fue alcanzable (post-C-14); revisar la capa de servicios y sus credenciales; rotar secretos; análisis forense de los servidores de la DMZ; restaurar desde imagen limpia; revisión de código y prueba de intrusión antes de reponer el servicio.
- **Falla o compromiso del firewall perimetral (→ E-02):** confirmar el estado del clúster; conmutar al nodo sano; si ambos fallan, seguir el procedimiento del DRP (equipo de reemplazo / configuración respaldada C-13.4); validar reglas al reponer.
- **Caída del enlace VPN entre sedes (→ E-03):** verificar enlaces; conmutar al enlace/ruta de respaldo (C-23, C-24); operar la Planta en modo degradado según el DRP; restablecer y validar criptografía (C-23.1).
- **DDoS (→ E-08):** activar la mitigación con el proveedor (C-20); comunicar a clientes; conmutar enlace si aplica; análisis posterior de perfil de ataque.
- **Acceso indebido de un tercero (→ relacionado con R-06):** revocar la cuenta del proveedor; revisar la grabación de su sesión (C-05.4); alcance del acceso; notificación contractual (C-06); ajuste del privilegio.

**6.9.6 Contención, erradicación, recuperación y evidencia.** Preservar evidencia (imágenes, memoria, bitácoras del SIEM) con cadena de custodia; contener sin destruir evidencia salvo riesgo mayor; erradicar la causa raíz; recuperar desde fuentes verificadas limpias; validar antes de reponer en producción.

**6.9.7 Actividad post-incidente y métricas.** Reunión de lección aprendida dentro de los 5 días hábiles; informe con línea de tiempo, causa raíz, impacto y acciones correctivas con responsable y fecha; actualización de controles, runbooks y concientización. **Indicadores reportados mensualmente al Comité:** número de incidentes por severidad, tiempo medio de detección (MTTD), tiempo medio de respuesta (MTTR), % de endpoints con EDR, % de sistemas con parche al día, cobertura de MFA, tasa de clic y de reporte en simulacros de phishing, % de respaldos con prueba de restauración exitosa, disponibilidad de los servicios críticos.

**6.9.8 Relación con el DRP.** Cuando un incidente supere el umbral de severidad o el tiempo de solución en sitio que defina la Fase 3, el Oficial de Seguridad o la Gerencia de TI **escala al procedimiento de activación del DRP**. Este Plan mantiene los prerrequisitos (respaldo, alta disponibilidad, segmentación, monitoreo); el DRP define la recuperación paso a paso y el sitio alterno.

### C-11 — Gestión de vulnerabilidades y pruebas de penetración

> Remedia: D-16, D-10. Mitiga: R-04, R-01. Soporta: E-04. Requiere: I-GestiónVuln. Marco: A.8.8 / CIS 7.1, 7.5, 7.6, 7.7 / ID.RA-01, DE.CM-08.

**Procedimiento.**
1. **Escaneo de vulnerabilidades** autenticado al menos **mensual** de servidores, estaciones y dispositivos de red, y **quincenal** de los servidores de la DMZ.
2. Priorización por severidad y exposición (CVSS + explotación activa + criticidad del activo); plazos de remediación alineados a P-10 (C-16.4).
3. **Prueba de penetración anual** de las tres aplicaciones publicadas y de la nueva arquitectura de DMZ (C-14); prueba dirigida tras cambios mayores.
4. Seguimiento de hallazgos hasta el cierre; reporte trimestral al Comité de Seguridad.
5. Suscripción a fuentes de amenazas y a los avisos de los fabricantes de la plataforma para actuar ante vulnerabilidades críticas fuera de ciclo.

**Registro asociado:** R-34 Hallazgos de vulnerabilidades y su estado; R-35 Informes de pentesting.

---

# 7. Anexos

## Anexo A — Listado nominal de usuarios y cuentas (plantilla)

> Se completa por la Gerencia de TI con los datos reales al implementar el Plan. Aquí se define la estructura obligatoria del registro.

### A.1 Usuarios de dominio

| ID de cuenta | Nombre completo | Puesto / área | Sede | Perfil de acceso (rol) | MFA | Fecha de alta | Última recertificación | Estado |
|---|---|---|---|---|---|---|---|---|
| _(ejemplo)_ jperez | _(nominal)_ | Ventas | Jutiapa | Perfil-Ventas | Sí | | | Activo |

### A.2 Cuentas privilegiadas / administrativas (nominadas)

| ID de cuenta admin. | Titular (nominal) | Ámbito (sistemas) | Tipo de MFA | En bóveda PAM | Fecha de alta | Última revisión | Estado |
|---|---|---|---|---|---|---|---|

### A.3 Cuentas de servicio y de integración

| ID de cuenta | Sistema propietario | Uso | Ubicación del secreto (bóveda) | Rotación | Responsable | Estado |
|---|---|---|---|---|---|---|

### A.4 Cuentas de terceros y proveedores

| Proveedor | Persona (nominal) | Sistemas autorizados | Ventana de acceso | Expiración | MFA | Sesión grabada | Contrato/NDA vigente | Estado |
|---|---|---|---|---|---|---|---|---|

## Anexo B — Registros y formularios de control

Registros mínimos que genera y conserva el Plan (evidencia para auditoría). El Oficial de Seguridad mantiene el índice y la ubicación de cada uno.

| Código | Registro / formulario | Responsable | Frecuencia de actualización | Control(es) que lo generan |
|---|---|---|---|---|
| R-1 | Inventario de activos de hardware y software | Administradores | Automática diaria; conciliación mensual | C-01, C-02 |
| R-2 | Catálogo de sistemas de información críticos y su clasificación | Oficial de Seguridad | Semestral | C-02 |
| R-3 | Estado de soporte y de parcheo de sistemas | Administradores | Mensual | C-16 |
| R-4 | Altas, bajas y cambios de acceso | Administradores / RR. HH. | Por evento | C-03, C-15 |
| R-5 | Capacitación y simulacros de phishing | Oficial de Seguridad | Por campaña / trimestral | C-04, C-21b |
| R-6 | Registro de riesgos aceptados | Gerencia de TI | Por evento; revisión anual | §3.4 |
| R-7 | Excepciones de política aprobadas | Gerencia de TI / Comité | Por evento | P-16, C-16 |
| R-8 | Registro de accesos de terceros | Oficial de Seguridad | Trimestral | C-05 |
| R-9 | Grabaciones y bitácoras de sesiones remotas de terceros | Administradores | Por sesión | C-05 |
| R-10 | Contratos con cláusulas de seguridad, SLA y NDA de terceros | Gerencia de TI / Legal | Anual | C-06, C-24 |
| R-11 | Bitácora de acceso físico al centro de datos y cuartos de telecom. | Administradores | Por evento | C-12(a) |
| R-12 | Pruebas de UPS/planta eléctrica y de alertas ambientales | Administradores | Mensual | C-12(c)(d) |
| R-13 | Cambios y pruebas de la infraestructura de red | Administradores | Por evento; failover semestral | C-13, C-17, C-23, C-24 |
| R-14 | Bitácora de cambios de aplicaciones | Gerencia de TI | Por evento | C-17, C-14 |
| R-15 | Índice y versión de los procedimientos operativos estándar | Oficial de Seguridad | Semestral | C-18 |
| R-16 | Inventario de cuentas privilegiadas | Oficial de Seguridad | Trimestral | C-15 |
| R-17 | Cobertura de MFA por sistema | Administradores | Trimestral | C-22 |
| R-18 | Inventario de secretos en bóveda | Administradores | Mensual | C-07 |
| R-19 | Estado de despliegue y detecciones de EDR | Administradores / SOC | Mensual | C-28 |
| R-20 | Métricas de correo bloqueado | Administradores | Mensual | C-21b |
| R-21 | Ejecución y estado de respaldos | Administradores | Diaria | C-08 |
| R-22 | Resultados de pruebas de restauración | Administradores | Según calendario C-09 | C-09 |
| R-23 | Política de retención de respaldos vigente | Gerencia de TI / Legal | Anual | C-10 |
| R-24 | Matriz de segmentación y reglas inter-zona | Administradores | Semestral | C-25, C-14 |
| R-25 | Eventos de admisión y cuarentena NAC | SOC | Continuo | C-26 |
| R-26 | SSID, políticas WLAN y credenciales de invitado emitidas | Administradores | Por evento | C-27 |
| R-27 | Reglas WAF y eventos bloqueados | SOC | Continuo; revisión mensual | C-19 |
| R-28 | Eventos de mitigación DDoS | SOC | Por evento | C-20 |
| R-29 | Consultas DNS bloqueadas | SOC | Continuo | C-21 |
| R-30 | Configuración criptográfica vigente de la VPN | Administradores | Por cambio | C-23 |
| R-31 | Catálogo de fuentes y casos de uso del SIEM | Oficial de Seguridad | Trimestral | C-29 |
| R-32 | Bitácora de alertas del SIEM | SOC | Continuo | C-29 |
| R-33 | Registro de incidentes de seguridad | Oficial de Seguridad | Por incidente | C-30 |
| R-34 | Hallazgos de vulnerabilidades y su estado | Administradores | Mensual | C-11 |
| R-35 | Informes de pruebas de penetración | Oficial de Seguridad | Anual / por cambio mayor | C-11 |
| R-36 | Control de versiones y distribución de este Plan | Gerencia de TI | Por versión | §Control de versiones |

## Anexo C — Tabla de trazabilidad Debilidad → Riesgo → Control (D-nn → R-nn → C-nn)

Verificación de la regla de oro (§1.4): **las 17 debilidades del caso quedan cubiertas por al menos un control de este Plan**. La columna "Escenario DRP" y "Inversión" se cierran en las Fases 3 y 4.

| D-nn | Debilidad (enunciado §2.4) | Riesgo(s) Fase 1 | **Control(es) Fase 2** | Bloque §6 | Escenario DRP (Fase 3) | Inversión (Fase 4) |
|---|---|---|---|---|---|---|
| **D-01** | 3 apps en DMZ sin WAF / Honeypot / Anti-DDoS / DNS Protection; y BD del ERP directamente expuesta | R-01 | **C-19** WAF, **C-20** Anti-DDoS, **C-21** filtrado DNS, **C-14** rediseño DMZ + capa de servicios (+ Honeypot opcional), **C-07** gestión de secretos, **C-11** pentesting | §6.8, §6.2, §6.9 | E-04 | I-WAF, I-AntiDDoS, I-DNSSecurity, I-Segmentación, I-Honeypot, I-GestiónSecretos |
| **D-02** | Firewall perimetral único sin HA | R-02 | **C-13** clúster NGFW en alta disponibilidad, **C-17** gestión de cambios de la base de reglas | §6.4 | E-02 | I-NGFW-HA |
| **D-03** | VPN IPsec >6 años, IKEv1 + 3DES/SHA-1, sin respaldo | R-08 | **C-23** reemplazo a IKEv2/AES-256-GCM/SHA-2 + SD-WAN, **C-24** enlace de respaldo | §6.8 | E-03 | I-SD-WAN/VPN, I-SegundoISP |
| **D-04** | ISP único, sin redundancia ni balanceo | R-02 | **C-24** segundo ISP con failover y SLA, **C-13** failover en el clúster | §6.8, §6.4 | E-08 | I-SegundoISP |
| **D-05** | Sin 2FA/MFA en VPN, correo, dominio, consolas | R-03, R-07 | **C-22** MFA obligatorio (resistente a phishing para privilegios), **C-15** cuentas nominadas y PAM | §6.5 | E-04, E-05 | I-MFA, I-PAM |
| **D-06** | Cuentas administrativas compartidas; política de contraseñas débil | R-03 | **C-15** eliminación de cuentas compartidas, mínimo privilegio, PAM, recertificación; **C-22** política de contraseñas; **C-18** segregación de funciones | §6.5, §6.4 | E-04, E-05 | I-PAM, I-MFA |
| **D-07** | Red plana /16 sin VLAN ni ACL | R-03 | **C-25** segmentación por zonas (Zero Trust / IEC 62443 para OT), **C-14** (DMZ), microsegmentación del ERP | §6.8 | E-05 | I-Segmentación, I-Switching |
| **D-08** | WiFi con clave WPA2-Personal única compartida | R-03 | **C-27** WPA3-Enterprise 802.1X + SSID de invitados aislado con portal cautivo | §6.8 | E-05 | I-WLAN |
| **D-09** | Sin NAC | R-03 | **C-26** NAC con 802.1X y postura del dispositivo; **C-01** inventario | §6.8, §6.1 | E-05 | I-NAC |
| **D-10** | SO desactualizados (WS2012R2, Win7/8.1), sin gestión de parches | R-03, R-05 | **C-16** migración de SO sin soporte + gestor de parches + hardening; **C-02** clasificación; **C-17** cambios; **C-11** gestión de vulnerabilidades | §6.1, §6.4, §6.9 | E-05 | I-RenovaciónSO, I-Parches |
| **D-11** | Antivirus de firmas, sin EDR, sin inventario de activos | R-03 | **C-28** EDR en el 100 % de servidores y estaciones; **C-01** inventario único; **C-02** clasificación | §6.6, §6.1 | E-04, E-05 | I-EDR, I-Inventario |
| **D-12** | Sala sin control biométrico/tarjeta, CCTV parcial, sin monitoreo ambiental | R-10 | **C-12(a)** control de acceso con bitácora, **C-12(b)** CCTV con retención de 30 días, **C-12(c)** monitoreo ambiental con alertas | §6.3 | E-01, E-07 | I-ControlAccesoFísico, I-CCTV, I-MonitoreoAmbiental |
| **D-13** | UPS de solo 15 min, sin planta eléctrica | R-09 | **C-12(d)** UPS dimensionado + planta eléctrica con ATS; **C-13.3** alimentación redundante del borde | §6.3, §6.4 | E-01, E-07 | I-UPS, I-Planta |
| **D-14** | Respaldos en cinta local, sin offsite, sin inmutabilidad, sin pruebas | R-05 | **C-08** modelo 3-2-1-1-0 con copia offsite e inmutable, **C-09** pruebas de restauración calendarizadas, **C-10** cifrado y retención | §6.7 | E-01, E-05, E-06, E-07 | I-Respaldo |
| **D-15** | Sin SPF/DKIM/DMARC; sin programa de concientización | R-07 | **C-21c** SPF/DKIM/DMARC (en C-21b), **C-21b** filtrado avanzado de correo, **C-04** programa de concientización con simulacros | §6.6, §6.2 | E-04, E-05 | I-FiltradoCorreo, I-Concientización |
| **D-16** | Sin SIEM, sin gestión de vulnerabilidades, sin IRP, sin CSIRT/SOC | R-04 | **C-29** SIEM + NDR + observabilidad, **C-30** plan de respuesta a incidentes por tipo, **C-11** gestión de vulnerabilidades y pentesting; §5 designación del Oficial de Seguridad y Comité | §6.9 | Todos | I-SIEM, I-Observabilidad, I-NDR, I-TalentoSOC |
| **D-17** | Accesos remotos permanentes de proveedores, sin monitoreo ni cláusulas | R-06 | **C-05** cuentas nominadas y temporales + jump host con grabación, **C-06** cláusulas de seguridad/SLA/NDA, **C-18** segregación, **C-22** MFA de terceros | §6.2, §6.5, §6.4 | E-04 | I-PAM/GestiónTerceros |

**Resultado de la verificación:** 17 de 17 debilidades con al menos un control asignado (**100 %**).

## Anexo D — Catálogo de controles del Plan (C-01 a C-30)

| C-nn | Nombre | Bloque §6 | Debilidades | Riesgos |
|---|---|---|---|---|
| C-01 | Inventario único y confiable de activos | 6.1 | D-11 | R-03 |
| C-02 | Clasificación de activos y de la información | 6.1 | D-11 | R-03, R-01 |
| C-03 | Seguridad en el ciclo de vida del empleo | 6.2 | D-15 | R-07, R-03 |
| C-04 | Programa continuo de concientización | 6.2 | D-15 | R-07 |
| C-05 | Alta, control y baja de accesos de terceros | 6.2 | D-17 | R-06 |
| C-06 | Cláusulas de seguridad, SLA y NDA en contratos | 6.2 | D-17 | R-06 |
| C-07 | Gestión de identidades no humanas y secretos de integración | 6.2 | D-17, D-01 | R-06, R-01 |
| C-08 | Plataforma y modelo de respaldo 3-2-1-1-0 | 6.7 | D-14 | R-05 |
| C-09 | Pruebas de restauración calendarizadas | 6.7 | D-14 | R-05 |
| C-10 | Cifrado, retención y protección de respaldos | 6.7 | D-14 | R-05 |
| C-11 | Gestión de vulnerabilidades y pruebas de penetración | 6.9 | D-16, D-10 | R-04, R-01 |
| C-12 | Protección física y ambiental del datacenter (a acceso, b CCTV, c ambiental, d energía) | 6.3 | D-12, D-13 | R-10, R-09 |
| C-13 | Alta disponibilidad de los servicios críticos de red | 6.4 | D-02 | R-02, R-09 |
| C-14 | Rediseño de la DMZ y capa de servicios intermedia | 6.8 | D-01 | R-01 |
| C-15 | Cuentas nominadas, mínimo privilegio y PAM | 6.5 | D-06, D-05 | R-03, R-07, R-06 |
| C-28 | Plataforma EDR | 6.6 | D-11 | R-03 |
| C-16 | Ciclo de vida y soporte de SO y software; parches; hardening | 6.1 | D-10 | R-03, R-05 |
| C-17 | Gestión de cambios | 6.4 | D-10 | R-01, R-03 |
| C-18 | Segregación de funciones y de ambientes; endurecimiento operativo | 6.4 | D-06, D-17 | R-03, R-06 |
| C-19 | Web Application Firewall (WAF) | 6.8 | D-01 | R-01 |
| C-20 | Protección Anti-DDoS | 6.8 | D-01 | R-01, R-02 |
| C-21 | Protección y filtrado de DNS | 6.8 | D-01 | R-01, R-03, R-07 |
| C-21b | Protección del correo contra malware y phishing (incl. C-21c SPF/DKIM/DMARC) | 6.6 | D-15 | R-07 |
| C-22 | Autenticación multifactor (MFA) | 6.5 | D-05 | R-03, R-07, R-06 |
| C-23 | Reemplazo de la VPN sitio a sitio y SD-WAN | 6.8 | D-03 | R-08 |
| C-24 | Redundancia del enlace a Internet | 6.8 | D-04 | R-02, R-08 |
| C-25 | Segmentación de la red en zonas (Zero Trust / IEC 62443) | 6.8 | D-07, D-09 | R-03 |
| C-26 | Control de acceso a la red (NAC) con 802.1X | 6.8 | D-09 | R-03 |
| C-27 | WLAN corporativa WPA3-Enterprise y red de invitados aislada | 6.8 | D-08 | R-03 |
| C-29 | SIEM, correlación de eventos, NDR y observabilidad (incl. C-29b NDR) | 6.9 | D-16 | R-04 |
| C-30 | Plan de respuesta a incidentes de seguridad | 6.9 | D-16 | R-04 |

> Los controles principales se numeran de `C-01` a `C-30`. Los identificadores `C-21b/c` y `C-29b` son subcontroles funcionales de protección de correo y monitoreo de red, respectivamente.

## Anexo E — Mapa de control a los marcos de referencia

| Bloque §6 | Controles | ISO/IEC 27001:2022 (Anexo A) | CIS Controls v8.1 | NIST CSF 2.0 |
|---|---|---|---|---|
| 6.1 Bienes informáticos | C-01, C-02, C-16 | A.5.9–A.5.13, A.8.8, A.8.19 | 1, 2, 3, 7 | ID.AM, PR.PS |
| 6.2 Gestión del personal | C-03, C-04, C-05, C-06, C-07 | A.6.1–A.6.6, A.5.16–A.5.22, A.8.4 | 5, 6, 14, 15 | PR.AT, GV.SC, PR.AA, PR.DS |
| 6.3 Seguridad física y ambiental | C-12 | A.7.1–A.7.4, A.7.8, A.7.11 | 1 | PR.IR, PR.AA-06 |
| 6.4 Seguridad de operaciones | C-13, C-17, C-18 | A.8.14, A.8.32, A.5.3, A.8.31 | 4, 12 | PR.PS, PR.IR-03, ID.RA |
| 6.5 Identidad y control de acceso | C-15, C-22 | A.5.15–A.5.18, A.8.2, A.8.5, A.8.24 | 5, 6, 16 | PR.AA |
| 6.6 Programas malignos | C-28, C-21b/c | A.8.7, A.8.23 | 9, 10 | PR.PS-05, DE.CM |
| 6.7 Respaldo | C-08, C-09, C-10 | A.8.13, A.8.24 | 11 | PR.DS-11, RC.RP |
| 6.8 Seguridad en redes | C-14, C-19, C-20, C-21, C-23, C-24, C-25, C-26, C-27 | A.8.20–A.8.26, A.8.14, A.8.6 | 9, 12, 13 | PR.IR, PR.AA-05, DE.CM |
| 6.9 Gestión de incidentes | C-11, C-29, C-30 | A.5.24–A.5.28, A.8.8, A.8.15, A.8.16 | 7, 8, 17 | DE, RS, RC |

## Anexo F — Glosario

| Término | Definición |
|---|---|
| **Air-gapped** | Copia de datos físicamente o lógicamente desconectada de la red, inalcanzable por un atacante que comprometa la producción. |
| **Anti-DDoS** | Conjunto de servicios que absorben o filtran el tráfico de un ataque de denegación de servicio distribuido antes de que agote los recursos del objetivo. |
| **DMZ** | Zona desmilitarizada: segmento de red aislado donde se publican servicios accesibles desde Internet, separado de la red interna. |
| **EDR** | Endpoint Detection and Response: plataforma de detección y respuesta ante amenazas en estaciones y servidores, con telemetría central y capacidad de aislamiento. |
| **Failover** | Conmutación automática a un componente de respaldo cuando el primario falla. |
| **FIDO2 / WebAuthn** | Estándar de autenticación fuerte resistente a phishing basado en criptografía de clave pública, ligado al dominio del servicio. |
| **Hardening** | Endurecimiento de la configuración de un sistema retirando servicios, cuentas y permisos innecesarios y aplicando una línea base segura. |
| **IEC 62443 (zonas y conductos)** | Marco de seguridad para sistemas de automatización industrial: agrupa activos con requisitos de seguridad homogéneos en "zonas" y controla la comunicación entre ellas por "conductos". |
| **IKEv2 / IPsec** | Protocolos de establecimiento de túnel y cifrado de red; IKEv2 sustituye a IKEv1, deprecado por el IETF (RFC 9395). |
| **Jump host / portal de acceso privilegiado** | Punto único y controlado por el que un administrador o un tercero accede a los sistemas, con MFA, mínimo privilegio y grabación de sesión. |
| **MFA / 2FA** | Autenticación multifactor: exige dos o más evidencias independientes de identidad. |
| **NAC** | Network Access Control: valida la identidad y la postura de un dispositivo antes de concederle acceso a la red (802.1X). |
| **NDR** | Network Detection and Response: análisis del tráfico de red para detectar comportamiento malicioso que evade el perímetro. |
| **PAM** | Privileged Access Management: custodia, aprobación temporal y auditoría del uso de credenciales privilegiadas. |
| **PLC** | Controlador lógico programable: computador industrial que gobierna una línea de procesamiento. |
| **RPO** | Recovery Point Objective: máxima pérdida de datos tolerable, medida en tiempo. |
| **RTO** | Recovery Time Objective: máximo tiempo tolerable de interrupción de un servicio. |
| **SD-WAN** | Red de área amplia definida por software: selecciona dinámicamente la mejor ruta entre varios enlaces y cifra el tráfico entre sedes. |
| **SIEM** | Security Information and Event Management: centraliza y correlaciona eventos de seguridad de múltiples fuentes. |
| **SPF / DKIM / DMARC** | Mecanismos de autenticación del correo que permiten al receptor verificar que un mensaje proviene realmente del dominio declarado y aplicar una política ante la suplantación. |
| **WAF** | Web Application Firewall: filtra y bloquea tráfico HTTP/HTTPS malicioso dirigido a una aplicación web (OWASP Top 10). |
| **WPA3-Enterprise** | Modo de seguridad inalámbrica con autenticación individual 802.1X contra un servidor, en lugar de una clave compartida. |
| **Zero Trust (NIST SP 800-207)** | Modelo en el que ningún usuario o dispositivo es confiable por su ubicación en la red; cada acceso se autentica, autoriza y evalúa por postura. |

## Anexo G — Referencias

Barker, E., & Roginsky, A. (2019). *Transitioning the use of cryptographic algorithms and key lengths* (NIST Special Publication 800-131A Rev. 2). National Institute of Standards and Technology. https://doi.org/10.6028/NIST.SP.800-131Ar2

Center for Internet Security. (2024). *CIS Critical Security Controls version 8.1*. https://www.cisecurity.org/controls/v8-1

Center for Internet Security. (2024). *Guide to implementation groups (IG): CIS Critical Security Controls v8.1*. https://www.cisecurity.org/insights/white-papers/guide-implementation-groups-ig-cis-critical-security-controls-v8-1

Cybersecurity and Infrastructure Security Agency. (2022). *Implementing phishing-resistant MFA* (fact sheet). U.S. Department of Homeland Security. https://www.cisa.gov/sites/default/files/publications/fact-sheet-implementing-phishing-resistant-mfa-508.pdf

Cybersecurity and Infrastructure Security Agency. (2022). *Layering network security through segmentation* [Infografía]. U.S. Department of Homeland Security. https://www.cisa.gov/sites/default/files/2023-01/layering-network-security-segmentation_infographic_508_0.pdf

Cybersecurity and Infrastructure Security Agency. (2023). *#StopRansomware guide*. U.S. Department of Homeland Security. https://www.cisa.gov/stopransomware/ransomware-guide

Microsoft. (2022). *Windows 7 — Microsoft Lifecycle*. https://learn.microsoft.com/en-us/lifecycle/products/windows-7

Microsoft. (2022). *Windows 8.1 — Microsoft Lifecycle*. https://learn.microsoft.com/en-us/lifecycle/products/windows-81

Microsoft. (2026). *Windows Server 2012 R2 — Microsoft Lifecycle*. Recuperado el 7 de septiembre de 2026, de https://learn.microsoft.com/en-us/lifecycle/products/windows-server-2012-r2

National Institute of Standards and Technology. (2020). *Zero Trust Architecture* (NIST Special Publication 800-207). U.S. Department of Commerce. https://doi.org/10.6028/NIST.SP.800-207

National Institute of Standards and Technology. (2022, 15 de diciembre). *NIST retires SHA-1 cryptographic algorithm*. https://www.nist.gov/news-events/news/2022/12/nist-retires-sha-1-cryptographic-algorithm

National Institute of Standards and Technology. (2024). *The NIST Cybersecurity Framework (CSF) 2.0* (NIST CSWP 29). U.S. Department of Commerce. https://doi.org/10.6028/NIST.CSWP.29

National Institute of Standards and Technology. (2024). *Digital identity guidelines: Authentication and authenticator management* (NIST Special Publication 800-63B-4). https://pages.nist.gov/800-63-4/sp800-63b.html

National Institute of Standards and Technology. (2025). *Incident response recommendations and considerations for cybersecurity risk management* (NIST Special Publication 800-61 Rev. 3). https://doi.org/10.6028/NIST.SP.800-61r3

Open Worldwide Application Security Project. (2025). *OWASP Top 10:2025*. https://owasp.org/Top10/2025/

Organización Internacional de Normalización. (2022). *ISO/IEC 27001:2022 — Information security, cybersecurity and privacy protection — Information security management systems — Requirements*. https://www.iso.org/standard/27001

Smyslov, V., & Hoffman, P. (2023). *Deprecation of the Internet Key Exchange version 1 (IKEv1) protocol and obsoleted algorithms* (RFC 9395). Internet Engineering Task Force. https://doi.org/10.17487/RFC9395

---

## Cierre

Este Plan de Seguridad Informática traduce las 17 debilidades del diagnóstico (Fase 1) en **30 controles** organizados en los 9 bloques obligatorios de medidas y procedimientos, con trazabilidad completa `D-nn → R-nn → C-nn` (Anexo C) y con las 9 correspondencias literales del enunciado §5.2 satisfechas. Sus prerrequisitos alimentan el Plan de Recuperación ante Desastres (Fase 3) —a través de los escenarios `E-nn` referenciados en cada control— y su materialización económica se dimensiona en el Plan de Adquisición e Implementación (Fase 4), a través de los rubros `I-nn`.

**Documento vivo.** Se revisa al menos anualmente y ante todo cambio mayor de infraestructura, incidente grave o hallazgo de auditoría, conforme al §1.6 y al control de versiones.
