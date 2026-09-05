## UNIVERSIDAD MARIANO GÁLVEZ DE GUATEMALA

Facultad de Ingeniería en Sistemas de Información

Campus Jutiapa

## PROYECTO No.01 DE CURSO

Seguridad de Redes: Diagnóstico de Riesgos, Plan de Seguridad Informática,

Plan de Recuperación ante Desastres y Plan de Adquisición de Infraestructura de

Ciberseguridad

Curso: Telecomunicaciones — Área de Especialidad, último semestre

Unidad temática integradora: Seguridad de Redes Docente: Ing. Juan Daniel Ramos Martínez

Segundo Semestre 2026

Guía del proyecto — Documento para el estudiante


## Contenido


## 1. Presentación y objetivos del proyecto

## 1.1 Justificación

Durante las semanas correspondientes a la unidad de Seguridad de Redes se abordaron los fundamentos de protección perimetral, control de acceso, continuidad de las comunicaciones y buenas prácticas de gestión de riesgos en infraestructuras de telecomunicaciones. El presente proyecto integra esos contenidos en un ejercicio profesional completo: partiendo de un caso de estudio con debilidades tecnológicas deliberadamente introducidas, cada grupo deberá diagnosticar los riesgos, documentar un plan de seguridad informática, elaborar un plan de recuperación ante desastres y proponer una inversión técnico-económica realista para remediar las brechas identificadas.

Este ejercicio simula el flujo de trabajo real de un consultor o responsable de seguridad de la información: identificar, priorizar, planificar y presentar una propuesta ante la dirección de una organización, insumo directamente aplicable al ejercicio profesional del futuro Ingeniero en Sistemas.

## 1.2 Objetivo general

Aplicar los conceptos de seguridad de redes, gestión de riesgos y continuidad operativa mediante el análisis de un caso empresarial realista, produciendo un conjunto de documentos técnicos profesionales (checklist de seguridad, plan de seguridad informática, plan de recuperación ante desastres y plan de adquisición de infraestructura) que respondan de manera integral a las vulnerabilidades identificadas.

## 1.3 Objetivos específicos / competencias a desarrollar

- Identificar y clasificar riesgos tecnológicos en una infraestructura de red mediante instrumentos de diagnóstico (checklist de auditoría).

- Diseñar controles de seguridad en las capas de red, aplicación y perímetro (firewall, WAF, DDoS, DNS, segmentación, autenticación) alineados a buenas prácticas internacionales (ISO/IEC 27001, NIST CSF).

- Redactar políticas y procedimientos de seguridad informática aplicables a los procesos reales de una organización (personal, operaciones, proveedores, activos).

- Elaborar un Plan de Recuperación ante Desastres (DRP) con roles, escenarios, tiempos de recuperación (RTO/RPO) y procedimientos de contingencia.

- Formular una propuesta técnico-económica de adquisición de hardware, software y talento humano especializado en respuesta a incidentes.

- Fortalecer competencias de trabajo colaborativo, comunicación técnica escrita y defensa oral de propuestas ante una audiencia no necesariamente técnica (dirección/gerencia).

## 1.4 Metodología de trabajo


El proyecto se desarrolla en cuatro fases secuenciales y acumulativas (diagnóstico, plan de seguridad, DRP y plan de adquisición), cada una con un entregable parcial que retroalimenta a la siguiente. El grupo debe mantener trazabilidad: cada debilidad detectada en la Fase 1 debe estar cubierta por al menos una medida concreta en la Fase 2, un procedimiento de continuidad en la Fase 3, y —cuando aplique— un rubro de inversión en la Fase 4. El detalle de la organización de grupos y el cronograma se describe en la sección 3.

Nota metodológica: se recomienda al estudiante utilizar herramientas de investigación asistida (buscadores especializados, documentación de fabricantes, marcos de referencia como ISO/IEC 27001, NIST CSF, COBIT y CIS Controls) citando siempre la fuente consultada.

## 2. Caso de estudio: TransAgro del Oriente, S.A.

El siguiente caso es de carácter ficticio y ha sido diseñado con fines exclusivamente académicos. Cualquier semejanza con organizaciones reales es coincidencia. El caso deberá tomarse como insumo único y obligatorio para el desarrollo de las cuatro fases del proyecto; ningún grupo debe modificar los hechos aquí descritos, aunque sí puede —y debe— documentar supuestos razonables cuando el caso no detalle un aspecto específico (por ejemplo, modelos exactos de equipo o número de licencias), dejando constancia expresa del supuesto adoptado.

## 2.1 Perfil de la organización

TransAgro del Oriente, S.A. es una empresa guatemalteca dedicada al acopio, procesamiento y comercialización de granos básicos y productos agroindustriales, con operaciones en la región oriental del país. Cuenta con aproximadamente 480 colaboradores distribuidos en dos sedes:

- Casa Matriz (Jutiapa): oficinas administrativas, finanzas, ventas, atención a clientes y el centro de datos principal (18 servidores físicos y virtualizados).

- Planta de Procesamiento (Chiquimula): operaciones de acopio, procesamiento industrial, control de calidad y logística de despacho, con un cuarto de telecomunicaciones local que aloja controladores de planta, cámaras de videovigilancia y estaciones de trabajo administrativas.

La empresa exporta parte de su producción hacia mercados centroamericanos y depende de sistemas de información para la gestión de pedidos, facturación electrónica, trazabilidad de la cadena de frío/transporte y comunicación con proveedores agrícolas de la región.

## 2.2 Infraestructura tecnológica actual

La infraestructura fue implementada de forma incremental durante más de una década, sin un rediseño integral ni una arquitectura de seguridad formalmente documentada. A grandes rasgos:

- Un router de borde conectado a un único ISP, seguido de un firewall perimetral (equipo único, sin alta disponibilidad) que separa Internet, la DMZ y la red interna.

- Una DMZ donde se publican tres aplicaciones web de cara al público (ver 2.3), alojadas en servidores con sistema operativo desactualizado.


- Un enlace VPN sitio a sitio hacia la Planta de Procesamiento en Chiquimula, establecido sobre la red pública de Internet con equipos y configuración de más de seis años de antigüedad.

- Una red interna plana (sin VLAN) que interconecta estaciones de trabajo, servidores de aplicación (ERP, correo, archivos), impresoras de red, cámaras IP y, en la planta, controladores industriales (PLC) de las líneas de procesamiento.

- Un centro de datos ubicado en la Casa Matriz, con controles físicos y ambientales limitados (ver categoría “Datacenter y físico” en la tabla 2.4).

- Un esquema de respaldo local en cinta, sin política formal de retención ni copia externa.

Se recomienda a cada grupo elaborar, como parte del diagnóstico, un diagrama de topología (físico y lógico) que represente gráficamente esta descripción, útil tanto para el checklist como para el plan de seguridad y el DRP.

## 2.3 Aplicaciones y servicios publicados en la DMZ

| Aplicación | Función de negocio | Observación técnica |
| --- | --- | --- |
| Portal de Clientes | Ingreso y seguimiento de pedidos de granos y derivados por parte de clientes mayoristas. | Aplicación web (framework desactualizado) con conexión directa a la base de datos interna del ERP, sin capa de servicios intermedia. |
| Portal de Proveedores | Registro de facturación electrónica y programación de entregas de proveedores agrícolas. | Permite carga de archivos (comprobantes) sin validación robusta de tipo/contenido; sin WAF que filtre inyecciones o cargas maliciosas. |
| Sistema de Rastreo de Flotilla | Consulta de ubicación GPS y estado de la flotilla de transporte en tiempo real. | Integración vía API con proveedor SaaS externo mediante credenciales estáticas embebidas en el código. |

Las tres aplicaciones comparten el mismo segmento de DMZ y el mismo servidor de base de datos backend, lo que implica que el compromiso de cualquiera de ellas representa una amenaza directa para las demás y, potencialmente, para la red interna.

## 2.4 Debilidades de seguridad identificadas

La siguiente tabla resume —sin pretender ser exhaustiva— las debilidades tecnológicas que la organización presenta actualmente. Cada grupo debe validarlas, ampliarlas si detecta riesgos adicionales derivados de estas condiciones, y priorizarlas en la Fase 1.

| Categoría | Debilidad identificada |
| --- | --- |
| Perímetro y DMZ | Tres aplicaciones web publicadas en la DMZ (Portal de Clientes, Portal de Proveedores y Sistema de Rastreo de Flotilla) sin ningún control en la capa de aplicación: sin WAF, sin Honeypot/Deception, sin protección Anti-DDoS y sin protección/filtrado DNS (DNS Firewall). |
| Perímetro y DMZ | Firewall perimetral único (sin clúster de alta disponibilidad); un solo punto de falla para la totalidad del tráfico entrante y saliente de la Casa Matriz. |


| Comunicaciones | Enlace entre la Casa Matriz (Jutiapa) y la Planta de Procesamiento (Chiquimula) mediante un túnel VPN IPsec configurado hace más de seis años sobre Internet público, con IKEv1 y algoritmos de cifrado 3DES/SHA-1 ya obsoletos; sin enlace de respaldo ni SD-WAN. |
| --- | --- |
| Comunicaciones | Conexión a Internet mediante un único proveedor (ISP), sin redundancia de enlace ni balanceo de carga. |
| Identidad y acceso | No existe segundo factor de autenticación (2FA/MFA) para el acceso a la VPN, el correo corporativo, el dominio interno ni las consolas de administración de servidores. |
| Identidad y acceso | Cuentas administrativas compartidas entre el personal de TI; política de contraseñas sin requisitos de complejidad ni expiración periódica. |
| Red interna | Red plana sin segmentación por VLAN: estaciones de usuario, servidores, impresoras, cámaras IP y controladores de planta comparten la misma subred (/16) sin listas de control de acceso entre segmentos. |
| Red interna | Red inalámbrica corporativa con una sola clave WPA2-Personal compartida por todo el personal y visitantes; no existe red de invitados aislada ni portal cautivo. |
| Red interna | Sin solución NAC (Network Access Control): cualquier dispositivo conectado físicamente a un punto de red obtiene automáticamente una dirección IP y acceso a los recursos internos. |
| Endpoint y sistemas | Sistemas operativos desactualizados: servidores con Windows Server 2012 R2 sin soporte extendido y estaciones de trabajo con Windows 7/8.1; sin gestión centralizada de parches (WSUS/gestor de actualizaciones). |
| Endpoint y sistemas | Antivirus tradicional basado en firmas, desactualizado en varias estaciones; ausencia de EDR (Endpoint Detection & Response) y de un inventario confiable de activos de TI. |
| Datacenter y físico | Sala de servidores sin control de acceso biométrico o por tarjeta (solo llave física compartida), cobertura parcial de CCTV y sin monitoreo ambiental de temperatura, humedad o corte eléctrico. |
| Datacenter y físico | UPS de respaldo dimensionado únicamente para 15 minutos de autonomía; sin planta eléctrica de respaldo. |
| Datos y continuidad | Respaldos realizados en cinta local, almacenados en el mismo cuarto de servidores, sin copia fuera de sitio (offsite) ni copia inmutable; sin pruebas periódicas de restauración. |
| Correo y usuarios | Dominio de correo sin registros SPF, DKIM ni DMARC configurados, con alta exposición a suplantación de identidad (phishing/spoofing); sin programa formal de concientización en ciberseguridad para el personal. |
| Monitoreo y respuesta | Ausencia de SIEM o cualquier mecanismo de centralización y correlación de bitácoras (logs); sin gestión de vulnerabilidades ni pruebas de penetración periódicas; sin plan de respuesta a incidentes documentado ni CSIRT/SOC. |
| Terceros / proveedores | Accesos remotos permanentes otorgados a proveedores externos (soporte del ERP, integrador de red, aplicación SaaS de rastreo GPS) sin monitoreo, sin cuentas temporales y sin cláusulas contractuales de seguridad de la información. |

## 2.5 Personal de TI y proveedores actuales

## Personal interno de Tecnología


- 1 Gerente de Tecnología de la Información (reporta a Gerencia General).

- 2 Administradores de sistemas y redes (Casa Matriz).

- 1 Técnico de soporte en sitio (Planta de Procesamiento, Chiquimula).

- No existe personal dedicado a seguridad de la información, monitoreo o respuesta a incidentes; estas funciones —cuando se realizan— recaen de manera informal en los administradores de sistemas.

## Proveedores externos relevantes

- Proveedor de enlace de Internet (ISP) para ambas sedes, sin acuerdo de nivel de servicio (SLA) de disponibilidad documentado.

- Integrador que instaló el firewall perimetral y el enlace VPN hace más de seis años; el contrato de soporte y actualización no se encuentra vigente.

- Proveedor de la aplicación SaaS de rastreo de flotilla (terceriza el almacenamiento de datos de ubicación de la operación logística).

- Proveedor de nómina electrónica en la nube, con acceso remoto periódico a los sistemas administrativos.

- Consultor externo eventual para mantenimiento del ERP, con acceso remoto permanente y credenciales que no han sido rotadas.

## 3. Organización del trabajo en grupos

## 3.1 Conformación de grupos

El curso, con 25 estudiantes, se organizará en tres grupos de trabajo (dos grupos de 8 integrantes y un grupo de 9 integrantes, o la distribución que el docente determine el día de la asignación). Los tres grupos analizan el mismo caso de estudio (TransAgro del Oriente, S.A.) y producen, cada uno, el conjunto completo de entregables (diagnóstico, plan de seguridad, DRP y plan de adquisición). Esta redundancia es intencional: permite comparar enfoques, fomenta la discusión técnica en la defensa oral y evita que el proyecto dependa de la interpretación de un único equipo.

El docente podrá, a su criterio, asignar énfasis distintos a cada grupo (por ejemplo, Grupo 1 con mayor peso en perímetro/DMZ, Grupo 2 en red interna e identidad, Grupo 3 en continuidad de negocio y adquisiciones) sin que ello exima a ningún grupo de entregar los cuatro documentos completos.

## 3.2 Roles sugeridos dentro de cada grupo

Se recomienda que cada grupo distribuya internamente responsabilidades similares a las de un equipo de consultoría real. Sugerencia de roles (ajustable según el número de integrantes):

| Rol | Responsabilidad principal |
| --- | --- |
| Líder de proyecto / Coordinador | Coordina avances, controla el cronograma interno y consolida los documentos finales. |
| Analista de riesgos | Lidera la Fase 1: adaptación del checklist, aplicación al caso y matriz de riesgos. |


| Especialista en seguridad perimetral y de aplicaciones | Diseña los controles de DMZ, WAF, anti-DDoS, protección DNS y arquitectura de firewall en alta disponibilidad. |
| --- | --- |
| Especialista en redes internas e identidad | Diseña la segmentación (VLAN/NAC), la estrategia de autenticación (MFA/2FA) y la política de contraseñas. |
| Especialista en continuidad de negocio | Lidera la Fase 3 (DRP): escenarios, RTO/RPO, roles y árbol de llamadas. |
| Especialista en adquisiciones e infraestructura | Lidera la Fase 4: selección de soluciones, marcas, arquitecturas, proveedores y presupuesto. |
| Redactor técnico / Editor | Unifica formato, redacción y coherencia de los cuatro documentos finales. |

## 3.3 Fases y entregables del proyecto

| Fase | Nombre | Entregable principal |
| --- | --- | --- |
| 1 | Diagnóstico de riesgos tecnológicos | Checklist de seguridad informática adaptado y aplicado al caso, con matriz de riesgos priorizada. |
| 2 | Plan de Seguridad Informática | Documento formal de Plan de Seguridad Informática aplicado a TransAgro del Oriente, S.A. |
| 3 | Plan de Recuperación ante Desastres (DRP) | Documento formal de DRP, con roles, escenarios y procedimientos de recuperación. |
| 4 | Plan de adquisición e implementación | Propuesta técnico-económica de hardware, software y equipo humano de respuesta a incidentes. |
| Final | Integración y defensa | Documento consolidado (portada única, los cuatro planes anexados) y presentación oral de 20-25 minutos por grupo. |

## 3.4 Cronograma sugerido

El siguiente cronograma referencial distribuye el proyecto en seis semanas efectivas de trabajo. El docente ajustará las fechas exactas al calendario académico vigente.

| Semana | Actividad |
| --- | --- |
|   | Entrega del caso de estudio, conformación de grupos, distribución de roles y selección/adaptación del checklist de seguridad informática. |
|   | Aplicación del checklist al caso, elaboración de la matriz de riesgos y entrega de la Fase 1. |
| 1 | Elaboración del Plan de Seguridad Informática (secciones de alcance, caracterización, políticas y responsabilidades). |
|   | Elaboración de medidas y procedimientos del Plan de Seguridad Informática; entrega de la Fase 2. Inicio del DRP (alcance, RTO/RPO, roles). |
|   | Finalización y entrega del DRP (Fase 3). Elaboración del plan de adquisición: selección de soluciones, marcas y arquitecturas. |
| 2 | Finalización del plan de adquisición y presupuesto (Fase 4), integración del documento final y ensayo de la defensa oral. |
|   | Presentación y defensa oral de cada grupo ante el docente (y, de ser posible, un panel invitado). |


## 4. Fase 1 — Diagnóstico de riesgos tecnológicos

## 4.1 Elaboración/adaptación del checklist de seguridad informática

Se ha compartido con el curso un modelo de referencia (“Check List - Seguridad Informática y Sistemas”) que cubre los dominios de seguridad física, seguridad lógica, sala de servidores y seguridad en red WiFi mediante preguntas de verificación (SÍ / NO / N-A) con espacio para observaciones. Cada grupo deberá investigar al menos un checklist adicional (por ejemplo, basado en CIS Controls v8, ISO/IEC 27001 Anexo A, o NIST Cybersecurity Framework) y adaptar/ampliar el modelo entregado para que cubra explícitamente los dominios propios de este caso: seguridad perimetral y de aplicaciones (DMZ), continuidad de comunicaciones (VPN/enlaces), identidad y acceso (2FA/MFA), segmentación de red, gestión de parches, protección de endpoints, respaldo y monitoreo/gestión de incidentes.

El resultado de esta fase no es simplemente llenar el formato original: es producir un checklist propio, adaptado al caso, documentado con su fuente de referencia, que sirva como instrumento de auditoría reutilizable.

## 4.2 Dominios mínimos a evaluar

| Dominio | Aspectos mínimos a verificar |
| --- | --- |
| Seguridad perimetral y DMZ | Presencia de WAF, protección Anti-DDoS, protección/filtrado DNS, segmentación de la DMZ respecto a la red interna, arquitectura de firewall (single point of failure vs. alta disponibilidad). |
| Comunicaciones | Vigencia y robustez criptográfica de VPN sitio a sitio, redundancia de enlaces (ISP/SD-WAN), cifrado de tráfico entre sedes. |
| Identidad y control de acceso | Existencia de MFA/2FA, política de contraseñas, gestión de cuentas privilegiadas, revisión periódica de accesos. |
| Red interna | Segmentación VLAN, control de acceso a red (NAC), seguridad de la red inalámbrica, aislamiento de dispositivos IoT/OT. |
| Endpoints y sistemas | Vigencia de sistemas operativos, gestión centralizada de parches, protección antimalware/EDR, cifrado de discos. |
| Datacenter y seguridad física | Control de acceso físico, videovigilancia, monitoreo ambiental, energía de respaldo (UPS/planta eléctrica). |
| Datos y continuidad | Política y prueba de respaldos, copia fuera de sitio, cifrado de respaldos, retención documentada. |
| Monitoreo y respuesta a incidentes | Centralización de logs (SIEM), gestión de vulnerabilidades, existencia de un plan de respuesta a incidentes y de un responsable designado. |
| Personal y proveedores | Concientización y capacitación del personal, gestión de accesos de terceros, cláusulas de seguridad en contratos. |

## 4.3 Matriz de riesgos

Con base en los hallazgos del checklist, el grupo deberá construir una matriz de riesgos que priorice cada debilidad según su probabilidad de ocurrencia y el impacto potencial sobre la confidencialidad,


integridad y disponibilidad de la información. Se sugiere una escala cualitativa de 1 a 5 para cada eje (probabilidad × impacto), clasificando el riesgo resultante en Bajo, Medio, Alto o Crítico, y justificando brevemente la calificación otorgada a cada riesgo relevante.

Ejemplo de estructura de la matriz: Riesgo | Activo/Proceso afectado | Probabilidad (1-5) | Impacto (1-5) | Nivel de riesgo | Control propuesto (referenciado a la Fase 2).

## 4.4 Entregable de la Fase 1

- Checklist adaptado (formato propio, con fuente de referencia citada).

- Checklist aplicado al caso de TransAgro del Oriente, S.A., con las columnas SÍ/NO/N-A y observaciones debidamente completadas.

- Matriz de riesgos priorizada.

- Conclusión ejecutiva de una página con los cinco riesgos más críticos identificados.


## 5. Fase 2 — Plan de Seguridad Informática

Se ha compartido con el curso una plantilla de referencia (“Plan de Seguridad Informática”) con la estructura estándar utilizada institucionalmente para este tipo de documento. El grupo deberá adoptar esa estructura y completarla —sin dejar secciones en corchetes o sin desarrollar— con contenido específico y realista para TransAgro del Oriente, S.A.

## 5.1 Estructura obligatoria del documento

- 1. Alcance del Plan de Seguridad Informática.

- 2. Caracterización del sistema informático (bienes, redes, aplicaciones, servicios, personal, edificaciones).

- 3. Resultados del análisis de riesgo (retomando la Fase 1).

- 4. Políticas de seguridad informática (normas generales de obligatorio cumplimiento).

- 5. Responsabilidades (por rol: dirección, gerencia de TI, administradores, usuarios).

- 6. Medidas y procedimientos, desagregados como mínimo en:

- Clasificación y control de los bienes informáticos.

- Gestión del personal (selección, capacitación, altas y bajas de acceso).

- Seguridad física y ambiental (datacenter, control de acceso, energía).

- Seguridad de operaciones (gestión de cambios, mantenimiento, introducción de nuevos sistemas).

- Identificación, autenticación y control de acceso (incluyendo MFA/2FA).

- Seguridad ante programas malignos (antivirus/EDR).

- Respaldo de la información (política, pruebas de restauración).

- Seguridad en redes (segmentación, VPN, WAF, Anti-DDoS, DNS, NAC).

- Gestión de incidentes de seguridad (procedimientos de respuesta por tipo de incidente).

- 7. Anexos (listado nominal de usuarios, registros, control de cambios).

## 5.2 Consideraciones específicas para TransAgro del Oriente, S.A.

Cada medida propuesta debe responder de forma explícita a una o más debilidades descritas en la sección 2.4 del caso de estudio. A manera de guía —no de solución cerrada— se sugiere que el grupo dé tratamiento formal, como mínimo, a los siguientes puntos dentro de las Medidas y procedimientos:

| Debilidad del caso | Debe quedar reflejada en la política/procedimiento de… |
| --- | --- |
| DMZ sin WAF/Honeypot/Anti- DDoS/DNS Protection | Seguridad en redes — control de publicación de servicios y protección de aplicaciones web. |
| Firewall sin alta disponibilidad | Seguridad de operaciones — continuidad de servicios críticos de red (enlazado también con el DRP). |
| VPN antigua sobre red pública | Seguridad en redes — comunicaciones entre sedes. |


| Sin 2FA en accesos internos | Identificación, autenticación y control de acceso. |
| --- | --- |
| Red plana sin segmentación | Seguridad en redes — segmentación y control de acceso a la red. |
| Datacenter sin protección perimetral física | Seguridad física y ambiental. |
| Sistemas operativos desactualizados | Clasificación y control de bienes informáticos / Seguridad de operaciones (gestión de parches). |
| Accesos permanentes de proveedores | Gestión del personal y terceros — control de acceso de proveedores externos. |
| Sin SIEM ni plan de respuesta a incidentes | Gestión de incidentes de seguridad. |

## 5.3 Entregable de la Fase 2

- Documento “Plan de Seguridad Informática — TransAgro del Oriente, S.A.” completo, siguiendo la estructura de 5.1, con portada institucional (logo UMG) y control de versiones.

- Tabla de trazabilidad riesgo → política/medida (puede integrarse como anexo).

## 6. Fase 3 — Plan de Recuperación ante Desastres (DRP)

Se han compartido con el curso dos referencias complementarias: la “Guía Plan de Recuperación ante Desastres” (con enfoque en roles, escenarios de desastre y actividades detalladas de recuperación técnica) y la “Plantilla DRP” de la Dirección General de Cómputo y de Tecnologías de Información y Comunicación (con enfoque en comité de crisis, equipos de recuperación/pruebas y procedimientos por tipo de desastre físico). El grupo deberá combinar lo mejor de ambos modelos en un solo documento coherente aplicado a TransAgro del Oriente, S.A.

## 6.1 Estructura obligatoria del documento

- 1. Información general (objetivo, responsable, alcance).

- 2. Condiciones generales y supuestos del plan.

- 3. Comité de Crisis, Equipo de Recuperación y Equipo de Pruebas (integrantes por rol, no por nombre, y responsabilidades antes / durante / después del evento).

- 4. Escenarios de desastre contemplados (ver 6.3).

- 5. Tabla de componentes críticos con RTO y RPO (ver 6.2).

- 6. Árbol de llamadas y procedimientos de notificación, evaluación y activación del DRP.

- 7. Procedimientos de recuperación y contingencia por escenario (paso a paso, con responsable por actividad).

- 8. Centro de control / sitio alterno de operaciones.

- 9. Actividades de manejo de crisis y comunicación (principios: informar rápida y periódicamente, decir la verdad, emitir reportes exactos; audiencias a considerar).

- 10. Actividades de mantenimiento y prueba del DRP (periodicidad, responsables).


- 11. Distribución del documento y control de cambios.

## 6.2 Alcance y componentes críticos (RTO/RPO)

El grupo deberá definir, con criterio propio y justificado, el Tiempo de Interrupción Tolerable (RTO) y el Punto de Recuperación Objetivo (RPO) para cada componente crítico de TransAgro del Oriente, S.A. A modo de referencia, se sugiere una tabla con al menos los siguientes componentes:

| Componente / Servicio | RTO sugerido | RPO sugerido |
| --- | --- | --- |
| ERP / Base de datos transaccional | A definir por el grupo (justificar) | A definir por el grupo (justificar) |
| Portal de Clientes / Portal de Proveedores | A definir por el grupo (justificar) | A definir por el grupo (justificar) |
| Correo electrónico corporativo | A definir por el grupo (justificar) | A definir por el grupo (justificar) |
| Enlace VPN entre sedes | A definir por el grupo (justificar) | A definir por el grupo (justificar) |
| Sistema de Rastreo de Flotilla | A definir por el grupo (justificar) | A definir por el grupo (justificar) |
| Infraestructura de red (firewall, switch core) | A definir por el grupo (justificar) | A definir por el grupo (justificar) |

*Deliberadamente se deja este ejercicio abierto: el estudiante debe fundamentar cada valor de RTO/RPO en el impacto de negocio del componente, no copiar valores de un ejemplo genérico.*

## 6.3 Escenarios de desastre a contemplar

- No disponibilidad del centro de datos (incendio, inundación, falla del sistema de aire acondicionado, falla prolongada del suministro eléctrico).

- Falla o compromiso del firewall perimetral único (al no existir alta disponibilidad, cualquier falla de hardware deja sin conectividad a Internet a toda la Casa Matriz).

- Caída del enlace VPN entre Casa Matriz y Planta de Procesamiento.

- Incidente de ciberseguridad en la DMZ (compromiso de una o más aplicaciones web, con posible movimiento lateral hacia la base de datos interna).

- Incidente de tipo ransomware con cifrado de servidores de archivos y/o del ERP.

- Pérdida o corrupción de respaldos (dado que actualmente se almacenan en el mismo sitio del centro de datos).

- Eventos propios del contexto guatemalteco: sismos/terremotos, tormentas tropicales e inundaciones estacionales en la región oriental.

- Interrupción prolongada del proveedor único de Internet.

## 6.4 Roles, árbol de llamadas y comité de crisis

El grupo deberá construir un árbol de llamadas propio (similar en concepto al ilustrado en la Guía DRP compartida), partiendo de quién detecta o reporta el incidente (usuario, personal de planta, sistema de monitoreo) hasta el Gerente de Tecnología de la Información y, cuando corresponda, la Gerencia


General. Debe definirse explícitamente qué rol tiene autoridad para activar formalmente el DRP y bajo qué criterios (por ejemplo, cuando la solución en sitio exceda un umbral de horas definido por el grupo).

## 6.5 Centro de operaciones alterno / sitio de contingencia

Dado que TransAgro del Oriente, S.A. no dispone actualmente de un centro de datos alterno, el grupo deberá proponer y justificar una estrategia de contingencia viable: por ejemplo, un sitio alterno frío/tibio/caliente, replicación hacia un proveedor de nube pública para los sistemas críticos, o un acuerdo de reciprocidad entre la Casa Matriz y la Planta de Procesamiento. Esta decisión debe conectarse con el presupuesto propuesto en la Fase 4.

## 6.6 Entregable de la Fase 3

- Documento “Plan de Recuperación ante Desastres — TransAgro del Oriente, S.A.” completo, con portada institucional (logo UMG) y control de versiones.

- Tabla de RTO/RPO justificada.

- Al menos tres escenarios de la sección 6.3 desarrollados con procedimiento de recuperación paso a paso.


## 7. Fase 4 — Plan de adquisición e implementación de infraestructura de ciberseguridad

## 7.1 Metodología de la propuesta técnico-económica

Cada grupo debe traducir las brechas identificadas en la Fase 1 y las políticas definidas en la Fase 2 en una propuesta concreta de inversión: qué se compra o contrata, con qué arquitectura, de qué proveedor y a qué costo referencial, ordenada por prioridad (crítico / alto / medio) y separando, cuando corresponda, la inversión inicial (CAPEX) del costo operativo recurrente (OPEX: suscripciones, licenciamiento, soporte y personal).

Las marcas, modelos y precios que se listan a continuación son referencias de mercado con fines exclusivamente didácticos; los valores cambian con el tiempo, el tipo de cambio y las condiciones comerciales de cada proveedor. Se exige a cada grupo validar y actualizar al menos tres de estas referencias mediante cotización o investigación directa con un proveedor o distribuidor autorizado en Guatemala o la región, citando la fuente.

El grupo es libre de proponer marcas distintas a las aquí listadas siempre que justifique técnicamente la elección (throughput requerido, número de usuarios, presupuesto disponible, soporte local, etc.).

## 7.2 Marco de referencia de soluciones, marcas y arquitecturas

*7.2.1 Seguridad perimetral y de aplicaciones (DMZ)*

| Rubro | Solución / arquitectura de referencia | Ejemplos de marca / producto | Proveedor referencial | Precio referencial |
| --- | --- | --- | --- | --- |
| Firewall perimetral en alta disponibilidad (NGFW) | Clúster activo-pasivo de dos equipos con sincronización de sesión (HA), inspección de tráfico con IPS integrado, en el borde entre Internet, DMZ y red interna. | Fortinet FortiGate (serie 60F/100F) · Palo Alto Networks PA-4xx · Sophos XGS · Cisco Secure Firewall | Distribuidor autorizado local / integrador de seguridad regional | US$ 6,000 – 18,000 (par de equipos + licenciamiento anual) |
| WAF (Web Application Firewall) | Protección en capa de aplicación (OWASP Top 10) para las tres aplicaciones publicadas; puede desplegarse como servicio en la nube (reverse proxy) o como appliance físico/virtual en la DMZ. | Cloudflare WAF (Business/Enterprise) · AWS WAF · F5 Distributed Cloud WAF · Fortinet FortiWeb | Proveedor cloud / integrador de seguridad | US$ 250 – 3,000 /mes (según tráfico y plan) |
| Protección Anti- DDoS | Mitigación volumétrica y de capa de aplicación mediante proveedor especializado (scrubbing en la nube) o suscripción del propio ISP/CDN. | Cloudflare (Pro/Business/Magic Transit) · Radware Cloud DDoS Protection · AWS Shield Advanced | Proveedor cloud / ISP con servicio administrado | US$ 200 – 3,000 /mes (según nivel de servicio) |
| Protección / filtrado DNS (DNS Security) | Resolución DNS protegida que bloquea dominios maliciosos y de phishing conocidos, aplicable tanto a los usuarios internos como a la infraestructura publicada. | Cisco Umbrella DNS Security · Infoblox BloxOne Threat Defense · Cloudflare Gateway (DNS) | Distribuidor autorizado Cisco/Infoblox en la región | US$ 2.50 – 4.00 /usuario/mes |
| Honeypot / Deception | Señuelos que simulan servicios reales para detectar intentos de reconocimiento y movimiento lateral de forma temprana, dentro | Fortinet FortiDeceptor (comercial) · T-Pot / Cowrie (open source, requiere horas de administración) | Distribuidor Fortinet / implementación interna (open source) | US$ 0 (open source, solo horas internas) – 12,000 (appliance comercial) |


de la DMZ y en segmentos internos críticos.

## 7.2.2 Comunicaciones entre sedes y acceso remoto

| Rubro | Solución / arquitectura de referencia | Ejemplos de marca / producto | Proveedor referencial | Precio referencial |
| --- | --- | --- | --- | --- |
| Reemplazo de VPN sitio a sitio / SD- WAN | Túneles IPsec con IKEv2 y cifrado AES-256/SHA-2 vigente, con posibilidad de doble enlace (ISP primario + respaldo LTE/otro ISP) y selección dinámica de ruta. | Fortinet Secure SD-WAN (FortiGate 60F/100F) · Cisco Meraki MX · Palo Alto Prisma SD-WAN | Distribuidor autorizado / integrador de redes | US$ 1,200 – 4,500 por sede (equipo) + US$ 300 – 700 /año licenciamiento |
| Redundancia de enlace a Internet | Segundo proveedor de Internet independiente (ruta física distinta) con balanceo/failover automático en el firewall o SD-WAN. | Segundo ISP local (fibra/inalámbrico) según cobertura en Jutiapa y Chiquimula | ISP local regional | US$ 150 – 600 /mes (según ancho de banda) |

## 7.2.3 Identidad, acceso y red interna

| Rubro | Solución / arquitectura de referencia | Ejemplos de marca / producto | Proveedor referencial | Precio referencial |
| --- | --- | --- | --- | --- |
| Autenticación multifactor (MFA/2FA) | Segundo factor obligatorio para VPN, correo, dominio (Active Directory) y consolas de administración; integración con el directorio existente. | Microsoft Entra ID P1 · Cisco Duo · Fortinet FortiToken | Licenciamiento cloud (Microsoft CSP) / distribuidor Cisco | US$ 3 – 9 /usuario/mes |
| Control de acceso a la red (NAC) y segmentación VLAN | Autenticación 802.1X por puerto/switch, cuarentena automática de dispositivos no conformes y perfilado de dispositivos IoT/OT; rediseño de la red en VLAN por función (usuarios, servidores, VoIP, cámaras, planta/OT, invitados). | Cisco ISE + switches Catalyst · Aruba ClearPass + switches Aruba · FortiNAC + FortiSwitch | Distribuidor autorizado / integrador de redes | US$ 8,000 – 30,000 (licenciamiento + reconfiguración de switching) |
| Red inalámbrica corporativa segmentada | Controlador WLAN con SSID independiente para invitados (portal cautivo, aislado de la red interna) y SSID corporativo con autenticación 802.1X (WPA2/WPA3-Enterprise). | Cisco Meraki MR · Aruba Instant On/AP · Ubiquiti UniFi (gama media) | Distribuidor autorizado / integrador de redes | US$ 250 – 900 por punto de acceso + licenciamiento cloud |

## 7.2.4 Protección de endpoints y gestión de sistemas

| Rubro | Solución / arquitectura de referencia | Ejemplos de marca / producto | Proveedor referencial | Precio referencial |
| --- | --- | --- | --- | --- |
| EDR (Endpoint Detection & Response) | Reemplazo del antivirus tradicional por una plataforma de detección y respuesta con telemetría centralizada, aislamiento remoto de equipos comprometidos y análisis de comportamiento. | CrowdStrike Falcon · SentinelOne Singularity · Microsoft Defender for Endpoint · ESET PROTECT Advanced | Distribuidor autorizado / licenciamiento cloud directo | US$ 5 – 12 /endpoint/mes |
| Gestión centralizada de parches | Despliegue automatizado de actualizaciones críticas de sistema operativo y aplicaciones, con reportes de cumplimiento. | ManageEngine Patch Manager Plus · Ivanti Patch Management · WSUS (gratuito, solo Microsoft) | Distribuidor autorizado / licenciamiento directo | US$ 8 – 12 /endpoint/año |


Microsoft Windows Server 2022/2025 · distribuciones Linux empresariales con soporte (Red Hat Enterprise Linux, Ubuntu Pro)

Migración de Windows Server 2012 R2 (fuera de soporte) a una versión con soporte vigente, priorizando los servidores que sostienen el ERP y las aplicaciones de la DMZ.

US\$ 900 – 1,100 por licencia de servidor (o suscripción anual Linux)

Distribuidor Microsoft CSP / soporte de la distribución Linux

Renovación de sistemas operativos de servidor

## 7.2.5 Seguridad física y continuidad del centro de datos

| Rubro | Solución / arquitectura de referencia | Ejemplos de marca / producto | Proveedor referencial | Precio referencial |
| --- | --- | --- | --- | --- |
| Control de acceso físico y videovigilancia | Lector biométrico o de tarjeta en la puerta del centro de datos con bitácora de acceso, complementado con cámaras IP con grabación en NVR y retención mínima de 30 días. | HID Signo (control de acceso) · Axis Communications / Hikvision (CCTV) | Integrador de seguridad física local | US$ 2,500 – 6,000 (control de acceso + CCTV de 8 cámaras) |
| Monitoreo ambiental del centro de datos | Sensores de temperatura, humedad, fuga de agua y corte eléctrico con alertas automáticas al personal de TI. | APC NetBotz · Vertiv Environet | Distribuidor autorizado APC/Vertiv | US$ 1,500 – 3,500 |
| Energía de respaldo (UPS ampliado / planta eléctrica) | UPS dimensionado para al menos 60-90 minutos de autonomía de la carga crítica, más planta eléctrica de respaldo para eventos prolongados. | APC Smart-UPS / Symmetra · plantas eléctricas diésel (marca según disponibilidad local) | Distribuidor autorizado APC / proveedor de plantas eléctricas | US$ 4,000 – 8,000 (UPS) + US$ 15,000 – 35,000 (planta eléctrica, según capacidad) |

## 7.2.6 Respaldo, monitoreo y gestión de incidentes

| Rubro | Solución / arquitectura de referencia | Ejemplos de marca / producto | Proveedor referencial | Precio referencial |
| --- | --- | --- | --- | --- |
| Plataforma de respaldo con copia inmutable y fuera de sitio | Reemplazo de la cinta local por un esquema 3-2-1 (tres copias, dos medios distintos, una fuera de sitio), con repositorio inmutable y replicación hacia la nube o hacia la Planta de Procesamiento. | Veeam Backup & Replication + repositorio con bloqueo de objetos (object lock) · Veeam Cloud Connect | Distribuidor autorizado / proveedor de nube (Azure, AWS, o nube local) | US$ 500 – 1,200 por socket/año (licenciamiento) + almacenamiento en la nube según volumen |
| SIEM / centralización de logs | Correlación de eventos de firewall, servidores, EDR y aplicaciones en una consola única, con reglas de alerta para los escenarios definidos en el DRP. | Wazuh (open source, autoalojado) · Microsoft Sentinel (SaaS, pago por consumo) · Splunk Enterprise | Implementación interna (open source) / licenciamiento cloud | US$ 0 (Wazuh, solo infraestructura) – US$ 2 – 5 /GB ingerido/mes (Sentinel) |
| Observabilidad y monitoreo de infraestructura | Monitoreo de disponibilidad, desempeño y capacidad de servidores, enlaces y switches, con tableros y alertamiento proactivo. | Zabbix + Grafana (open source) · PRTG Network Monitor · SolarWinds | Implementación interna (open source) / licenciamiento comercial | US$ 0 – 1,500 /año (según licenciamiento elegido) |
| Detección y respuesta de red (NDR) / IDS-IPS complementario | Análisis de tráfico de red para detectar patrones anómalos que evadan el firewall perimetral, útil especialmente en la red interna ya segmentada. | Suricata + Zeek (open source) · Darktrace (comercial, mayor costo) | Implementación interna (open source) / distribuidor especializado | US$ 0 (open source) – 20,000+ /año (Darktrace, referencial) |

## 7.3 Equipo humano de respuesta a incidentes y observabilidad


La tecnología por sí sola no resuelve las brechas identificadas: TransAgro del Oriente, S.A. no cuenta actualmente con ningún rol dedicado a seguridad de la información. El plan de adquisición debe incluir, por tanto, una propuesta de fortalecimiento del talento humano, ya sea mediante contratación directa, tercerización de un servicio administrado (MDR/SOC como servicio), o un esquema mixto.

## 7.3.1 Estructura organizacional propuesta

- Gerencia General

- Comité de Seguridad de la Información (Gerencia General, Gerencia de TI y, cuando aplique, un asesor externo)

- Oficial / Responsable de Seguridad de la Información (interno o vCISO por contrato)

- Analista SOC Nivel 1 — monitoreo continuo de alertas

- Especialista en Respuesta a Incidentes (Incident Responder) — investigación y contención

- Coordinación permanente con los Administradores de Sistemas y Redes ya existentes en la organización

## 7.3.2 Perfiles, certificaciones sugeridas y presupuesto referencial

| Rol | Perfil / certificaciones sugeridas | Modalidad | Costo mensual referencial |
| --- | --- | --- | --- |
| Oficial de Seguridad de la Información | Ingeniero en Sistemas con formación en ISO/IEC 27001 (Lead Implementer/Auditor) o ISC2 CC/CISSP | Contratación directa (tiempo parcial o completo) o servicio de vCISO por retainer | Q15,000 – Q22,000/mes (interno) o US$ 1,500 – 3,000/mes (vCISO externo) |
| Analista SOC Nivel 1 | Técnico/Ingeniero con CompTIA Security+ o equivalente | Contratación directa o incluido en servicio de MDR tercerizado | Q6,000 – Q9,000/mes (interno) |
| Especialista en Respuesta a Incidentes | EC-Council CEH, GIAC GCIH o equivalente | Contratación directa o retainer de horas garantizadas con proveedor externo | Q10,000 – Q15,000/mes (interno) o US$ 5,000 – 15,000/año (retainer IR) |
| Servicio MDR / SOC como servicio (alternativa tercerizada) | Monitoreo 24/7 de EDR, firewall y SIEM por proveedor especializado | Servicio contratado (OPEX puro, sin contratación de personal propio) | US$ 1,500 – 4,000/mes (según número de activos monitoreados) |

Los valores salariales son referenciales y deben contrastarse con la escala salarial vigente para el sector TI en Guatemala al momento de elaborar la propuesta final; el grupo puede optar por un esquema totalmente interno, totalmente tercerizado o híbrido, siempre que lo justifique.

## 7.4 Estimación de inversión consolidada

Como cierre de la Fase 4, cada grupo debe presentar una tabla resumen que consolide la inversión inicial (CAPEX) y el costo operativo anual recurrente (OPEX), agrupada por dominio, priorizada según la criticidad establecida en la matriz de riesgos de la Fase 1. Se sugiere el siguiente formato mínimo:

| Dominio | Prioridad | CAPEX estimado | OPEX anual estimado | Responsable de gestión |
| --- | --- | --- | --- | --- |


| Perímetro y aplicaciones (DMZ) | Crítica | A completar por el grupo | A completar por el grupo | A completar por el grupo |
| --- | --- | --- | --- | --- |
| Comunicaciones entre sedes | Alta | A completar por el grupo | A completar por el grupo | A completar por el grupo |
| Identidad, acceso y red interna Alta |   | A completar por el grupo | A completar por el grupo | A completar por el grupo |
| Endpoints y sistemas | Media | A completar por el grupo | A completar por el grupo | A completar por el grupo |
| Seguridad física y datacenter | Alta | A completar por el grupo | A completar por el grupo | A completar por el grupo |
| Respaldo, monitoreo y respuesta a incidentes | Crítica | A completar por el grupo | A completar por el grupo | A completar por el grupo |
| Talento humano (CSIRT/SOC) Crítica |   | — | A completar por el grupo | A completar por el grupo |
| TOTAL CONSOLIDADO |   | A completar por el grupo | A completar por el grupo |   |

## 7.5 Entregable de la Fase 4

- Documento “Plan de Adquisición e Implementación de Infraestructura de Ciberseguridad — TransAgro del Oriente, S.A.”, con las tablas de las secciones 7.2, 7.3 y 7.4 completas, actualizadas y con fuentes citadas.

- Al menos tres cotizaciones o referencias de precio verificadas de forma independiente por el grupo (captura de pantalla, enlace o constancia de contacto con un distribuidor/proveedor).

- Propuesta de fases de implementación (qué se adquiere primero y por qué, en función del nivel de riesgo).


## 8. Entregables finales y formato de presentación

## 8.1 Documentos a entregar

- Documento consolidado en formato Word (.docx) y PDF, con portada institucional única (logo UMG, nombre del curso, integrantes del grupo, docente y fecha), que incluya como capítulos o anexos los cuatro planes: Diagnóstico/Checklist (Fase 1), Plan de Seguridad Informática (Fase 2), Plan de Recuperación ante Desastres (Fase 3) y Plan de Adquisición e Implementación (Fase 4).

- Presentación de diapositivas (PowerPoint) de apoyo para la defensa oral, con un máximo de 20 diapositivas, orientada a una audiencia de dirección/gerencia (lenguaje claro, evitando saturar de texto técnico).

- Diagrama de topología de red actual y topología propuesta (debe elaborarse en Cisco Packet Tracer).

## 8.2 Presentación oral / defensa técnica

- Duración: 20 a 25 minutos por grupo, más 10 minutos de preguntas.

- Todos los integrantes deben participar activamente en la exposición, en correspondencia con el rol que desempeñaron durante el proyecto (sección 3.2).

- Se espera que el grupo sea capaz de justificar cada decisión técnica y cada rubro de inversión ante preguntas del docente, simulando la defensa de una propuesta ante la dirección de una empresa.

## 8.3 Normas de formato

- Papel tamaño carta, márgenes de 1 pulgada, fuente Calibri o Arial 11 puntos, interlineado 1.15.

- Portada, índice, numeración de página y encabezado institucional en todos los documentos.

- Todas las tablas, diagramas y cifras deben estar debidamente tituladas y, cuando provengan de una fuente externa, citadas conforme al formato indicado por el docente (APA 7ª edición u otro que se establezca en clase).

- Se prohíbe copiar literalmente el contenido de las plantillas de referencia sin adaptarlo al caso; el uso de herramientas de inteligencia artificial como apoyo de redacción o investigación es permitido siempre que el contenido final sea revisado, comprendido y defendido por el propio grupo.


## 9. Rúbrica de evaluación

| Criterio | Puntos | Descripción |
| --- | --- | --- |
| Fase 1 — Diagnóstico de riesgos | 20 | Calidad y pertinencia del checklist adaptado; exhaustividad en la aplicación al caso; rigor y priorización de la matriz de riesgos. |
| Fase 2 — Plan de Seguridad Informática | 20 | Cumplimiento de la estructura obligatoria; trazabilidad entre riesgo y política/medida; nivel de detalle y aplicabilidad al caso. |
| Fase 3 — Plan de Recuperación ante Desastres | 20 | Definición justificada de RTO/RPO; cobertura de escenarios relevantes; claridad de roles y procedimientos de recuperación. |
| Fase 4 — Plan de adquisición e implementación | 20 | Pertinencia técnica de las soluciones propuestas; realismo del presupuesto; inclusión del componente de talento humano; verificación de al menos tres cotizaciones. |
| Integración, redacción y formato | 10 | Coherencia entre los cuatro documentos; cumplimiento de las normas de formato; calidad de la redacción técnica. |
| Defensa oral | 10 | Dominio técnico, claridad expositiva, participación equitativa del grupo y calidad de las respuestas a preguntas. |
| TOTAL | 100 |   |

El docente podrá ajustar la ponderación anterior conforme a la distribución de puntos vigente en el reglamento de evaluación del curso, manteniendo la proporción relativa entre fases.

## 10. Glosario de términos

| Término | Definición |
| --- | --- |
| WAF | Web Application Firewall: control de seguridad que filtra, monitorea y bloquea tráfico HTTP/HTTPS malicioso hacia una aplicación web. |
| DMZ | Zona Desmilitarizada: segmento de red aislado donde se publican servicios accesibles desde Internet, separado de la red interna. |
| DDoS | Denegación de Servicio Distribuida: ataque que satura los recursos de un sistema o enlace mediante múltiples orígenes simultáneos. |
| MFA / 2FA | Autenticación Multifactor / de Doble Factor: exige dos o más evidencias independientes de identidad para autenticar a un usuario. |
| NAC | Network Access Control: control de acceso a la red que valida el cumplimiento de un dispositivo antes de otorgarle conectividad. |


| EDR | Endpoint Detection and Response: plataforma de detección y respuesta ante amenazas en estaciones de trabajo y servidores. |
| --- | --- |
| SIEM | Security Information and Event Management: sistema de centralización y correlación de eventos de seguridad de múltiples fuentes. |
| RTO | Recovery Time Objective: tiempo máximo tolerable de interrupción de un proceso o sistema tras un desastre. |
| RPO | Recovery Point Objective: cantidad máxima tolerable de datos que se puede perder, medida en tiempo, tras un desastre. |
| DRP | Disaster Recovery Plan: plan de recuperación ante desastres, enfocado en restaurar la plataforma tecnológica. |
| BCP | Business Continuity Plan: plan de continuidad de negocio, de alcance más amplio que el DRP, que integra procesos no solo tecnológicos. |
| CSIRT / SOC | Equipo de respuesta a incidentes de seguridad informática / Centro de operaciones de seguridad, responsable de la detección, análisis y respuesta ante incidentes. |
| CAPEX / OPEX | Gasto de capital (inversión inicial) y gasto operativo (costo recurrente), respectivamente. |

## 11. Referencias y fuentes sugeridas

- ISO/IEC 27001:2022 — Sistemas de Gestión de Seguridad de la Información.

- NIST Cybersecurity Framework (CSF) 2.0 — National Institute of Standards and Technology.

- CIS Controls v8 — Center for Internet Security.

- NIST SP 800-34 — Contingency Planning Guide for Federal Information Systems.

- OWASP Top 10 — Open Worldwide Application Security Project.

- Documentación oficial de fabricantes: Fortinet, Cisco, Palo Alto Networks, Microsoft, Cloudflare, Veeam, entre otros mencionados en la sección 7.

- Plantillas institucionales compartidas por el docente para este proyecto (ver Anexo).

## Anexo — Plantillas de apoyo entregadas por el docente

Como insumo de referencia para el desarrollo de los cuatro entregables, el docente ha compartido los siguientes documentos, cuya estructura debe adaptarse —no copiarse literalmente— al caso de TransAgro del Oriente, S.A.:

- Checklist – Seguridad Informática y Sistemas (modelo de auditoría con dominios de seguridad física, lógica, sala de servidores y red WiFi).

- Guía Plan de Recuperación ante Desastres (enfoque en roles, escenarios de desastre y procedimientos técnicos detallados de recuperación).

- Plan de Seguridad Informática (plantilla con la estructura estándar de alcance, caracterización, análisis de riesgo, políticas, responsabilidades y medidas/procedimientos).


- Plantilla DRP – Dirección General de Cómputo y de Tecnologías de Información y Comunicación (enfoque en Comité de Crisis, Equipo de Recuperación y Equipo de Pruebas, y procedimientos por tipo de desastre físico).

Página 23 de 23
