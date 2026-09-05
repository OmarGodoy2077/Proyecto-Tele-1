Fase 1: Diagnóstico de riesgos tecnológicos Caso de Estudio: TransAgro del Oriente, S.A.

## Checklist de Seguridad Informática Adaptado

Con el propósito de fortalecer la postura de ciberseguridad se describe el

instrumentó de auditoria que ha sido diseñado y adaptado tomando como

referencia los controles CIS Controls v8 y los dominios de la norma ISO/IEC

27001, enfocándose específicamente en las debilidades tecnologías de la

infraestructura actual de TransAro del Oriente, S.A.

| DOMINIO | PREGUNTA DE SÍ / NO / N-A OBSERVACIONES VERIFICACIÓN DEL HALLAZGO |
| --- | --- |
| PERÍMETRO Y DMZ PERÍMETRO Y DMZ COMUNICACIONES COMUNICACIONES | ¿Existe un Web NO Las aplicaciones Application Firewall (Portal de (WAF) protegiendo Clientes, las aplicaciones Proveedores y web publicadas? Rastreo) operan en la DMZ sin filtrado en capa de aplicación. ¿El firewall NO Se identificó un perimetral opera equipo único, bajo una representando arquitectura de un solo punto de Alta falla para el Disponibilidad tráfico de la (Clúster HA)? Casa Matriz. ¿El túnel VPN sitio NO La VPN sobre a sitio utiliza internet público algoritmos de utiliza IKEv1, cifrado vigentes 3DES y SHA-1, los (ej. AES-256)? cuales son algoritmos criptográficos obsoletos. ¿La NO Existe un único conectividad a proveedor (ISP) |


| IDENTIDAD Y ACCESO RED INTERNA ENDPOINTS Y SISTEMAS DATACENTER (FÍSICO) DATOS Y CONTINUIDAD | Fase l Internet cuenta para toda la con enlaces conectividad, redundantes y sin acuerdos de balanceo de nivel de servicio carga? (SLA) documentados. ¿Se implementa NO No hay MFA Autenticación para VPN, Multifactor correo, dominio (MFA/2FA) para interno ni el acceso a consolas de sistemas críticos? administración. ¿La red está NO Es una red plana segmentada de (subred /16) forma lógica donde (VLANs) aislando convergen servicios y estaciones de usuarios? trabajo, servidores, cámaras IP y controladores industriales. ¿Los sistemas NO Se operan operativos servidores con mantienen Windows Server actualizaciones y 2012 R2 y soporte vigente clientes con por el Windows 7/8.1, fabricante? sin gestión de parches. ¿El centro de NO El respaldo datos posee energético (UPS) controles es de solo 15 ambientales y minutos, sin autonomía planta eléctrica energética ni monitoreo de prolongada? temperatura. ¿El NO Los respaldos se almacenamiento realizan en cinta de copias de local y se |
| --- | --- |


## Fase l

| MONITOREO Y RESPUESTA A INCIDENTES | seguridad resguardan cumple con el dentro del principio fuera mismo cuarto de sitio (offsite)? de servidores. ¿Existe NO No se cuenta centralización de con un SIEM ni logs (SIEM) o un con un plan plan de formal de respuesta a respuesta a incidentes? incidentes; los eventos de seguridad no se correlacionan ni se monitorean de forma centralizada, retrasando la detección de ataques. |
| --- | --- |


## Matriz de Riesgos Tecnológicos

Los riesgos detectados se han priorizado utilizando una escala cualitativa para evaluar la Probabilidad de

ocurrencia (1-5) y el Impacto potencial (1-5) sobre la confidencialidad, integridad y disponibilidad de la

información de la empresa.

| RIESGO IDENTIFICADO | TRAZABILIDAD ACTIVO / (HALLAZGO DEL JUSTIFICACIÓN DEL JUSTIFICACIÓN NIVEL CONTROL PROB. IMPACT PROCESO CHECKLIST / PUNTAJE DEL PUNTAJE DE PROPUESTO (1-5) O (1-5) AFECTADO CONTROL DE (PROBABILIDAD) (IMPACTO) RIESGO (FASE 2) REFERENCIA) |
| --- | --- |
| COMPROMISO DE BASES DE DATOS POR VULNERABILIDADES WEB CAÍDA TOTAL OPERATIVA POR FALLO DE EQUIPO DE BORDE PROPAGACIÓN MASIVA DE | Implementar Las aplicaciones Un ataque exitoso WAF, aplicar están publicadas compromete Checklist hardening a las en la DMZ sin WAF, datos financieros, Portal de Dominio "Perímetro aplicaciones, expuestas de de clientes y del Clientes, Portal y DMZ" (¿Existe segmentar DMZ 5 forma constante a 5 ERP, afectando CRÍTICO de Proveedores, WAF?) → CIS del backend y ataques confidencialidad, ERP interno. Control 16 / ISO realizar pruebas automatizados integridad y 27001 A.8.26. de pentesting (SQLi, XSS) desde continuidad del periódicas. internet. negocio. Implementar El firewall Una falla aislaría clúster de Checklist Dominios perimetral es un totalmente la firewalls en Alta "Perímetro y DMZ" equipo único sin Conectividad a Casa Matriz y Disponibilidad, (Clúster HA) y Clúster HA y Internet Casa desconectaría la contratar un "Comunicaciones" depende de un Matriz, VPN a 4 5 Planta de CRÍTICO segundo (enlaces solo ISP sin SLA, Planta Chiquimula, enlace de redundantes) → elevando la Chiquimula. deteniendo la Internet con CIS Control 12 / ISO probabilidad de operación balanceo/failov 27001 A.8.14. una falla no completa. er y definir SLA planificada. documentado. Red corporativa, Checklist Dominios La red es plana Puede detener la Segmentar la 5 4 CRÍTICO servidores "Red Interna" (subred /16, sin producción red por VLANs, |


## Fase l

| MALWARE/RANSOMW ARE PÉRDIDA IRRECUPERABLE DE DATOS POR DESASTRE FÍSICO INTERCEPCIÓN DE DATOS SENSIBLES EN TRÁNSITO ACCESO NO MONITOREADO DE PROVEEDORES EXTERNOS | principales, (VLANs) y VLANs) y coexiste industrial y cifrar actualizar o controladores "Endpoints y con sistemas información reemplazar de planta (PLC). Sistemas" (SO sin operativos crítica del sistemas soporte) → CIS obsoletos y sin negocio, aunque operativos Controls 4 y 12 / parches (Windows con posibilidad obsoletos, ISO 27001 A.8.22. 7/8.1, Server 2012 de contención implementar R2), facilitando el parcial si se actúa EDR/antivirus movimiento lateral. a tiempo. centralizado y un plan de respuesta a incidentes. Implementar Checklist Dominios El riesgo de un La empresa respaldo fuera "Datos y siniestro físico perdería de forma de sitio (offsite) Continuidad" (incendio, total e o en la nube, Servidores del (backup offsite) y inundación) no es irrecuperable su adoptar la ERP, cintas de "Datacenter diario, pero es real información 3 5 ALTO política 3-2-1 de respaldo locales (Físico)" dado que los operativa y backups y en Casa Matriz. (autonomía respaldos están en financiera ante un realizar pruebas energética) → CIS el mismo cuarto desastre físico o de restauración Control 11 / ISO que los servidores un ataque de periódicas. 27001 A.8.13. de producción. ransomware. Migrar la VPN a La VPN sitio a sitio Expone IKEv2/IPsec con Checklist Dominio utiliza IKEv1, 3DES y información cifrado AES-256 Información de "Comunicaciones" SHA-1, algoritmos operativa y de y SHA-2, producción y (cifrado VPN AES- criptográficamente facturación en actualizando el 4 3 MEDIO facturación que 256) → CIS Control rotos y vulnerables tránsito, aunque equipo de viaja por la VPN. 3 / ISO 27001 a técnicas de no compromete borde si es necesario para A.8.24. interceptación directamente los conocidas. sistemas internos. soportarlo. Checklist Los proveedores Un acceso de Establecer ERP interno, red Dominio "Personal externos cuentan terceros cuentas interna, y Proveedores" con accesos comprometido individuales y información de (accesos 4 permanentes y/o 4 puede derivar en ALTO temporales clientes y temporales y compartidos, sin fuga, para proveedores. monitoreados) → cuentas manipulación o proveedores, CIS Control 6 / ISO individuales ni eliminación de aplicar principio |
| --- | --- |


## Fase l

| SUPLANTACIÓN DE IDENTIDAD (PHISHING) CEGUERA OPERATIVA ANTE INCIDENTES | 27001 A.5.19– monitoreo de su información de mínimo A.5.22. actividad. crítica del ERP. privilegio y monitorear/aud itar sus accesos. Configurar SPF/DKIM/DMA Derivado del RC, habilitar No existen registros Puede derivar en análisis del caso, MFA en el Correo SPF/DKIM/DMARC robo de correo vinculado al corporativo, ni programas de credenciales, dominio "Identidad corporativo, credenciales de concientización, lo fraude financiero y Acceso" (falta de 4 4 ALTO capacitar usuarios, que facilita el o servir como MFA/controles de periódicament información envío de correos puerta de correo) → CIS e al personal y confidencial. falsificados y entrada para Control 14 / ISO reforzar el creíbles. ransomware. 27001 A.6.3. filtrado antispam. Implementar un SIEM o No existe SIEM, Retrasa la Checklist Dominio centralización centralización de detección y "Monitoreo y de logs, definir Toda la logs ni gestión de respuesta ante Respuesta a un Plan de infraestructura vulnerabilidades, ataques, Incidentes" (SIEM / Respuesta a tecnológica 5 por lo que los 4 incrementando su CRÍTICO plan de respuesta) Incidentes (IRP) (red, servidores, eventos de alcance y el → CIS Controls 8 y y establecer aplicaciones). seguridad no se tiempo de 17 / ISO 27001 escaneos detectan de forma exposición de la A.8.15–A.8.16. periódicos de oportuna. empresa. vulnerabilidade s. |
| --- | --- |


## Dirección y Gerencia General de TransAgro del Oriente, S.A.

A partir del diagnóstico tecnológico realizado mediante estándares internacionales de auditoría, el equipo de analistas concluye que TransAgro

del Oriente, S.A. enfrenta vulnerabilidades sistémicas críticas derivadas del

crecimiento no planificado de su infraestructura. Actualmente, la operación

carece de una arquitectura de seguridad formal, lo que genera niveles de

riesgo inaceptables para la continuidad del negocio.

Los hallazgos más críticos que requieren la atención inmediata de la

gerencia son:

- Exposición directa de la información financiera y operativa: La publicación de aplicaciones web (portales de clientes y proveedores) en la DMZ sin mecanismos de inspección (WAF) expone la base de datos central a ataques externos. Al no existir una separación adecuada, un ciberdelincuente puede transitar desde la web pública hasta los registros internos del ERP.

- Riesgo de paralización por un punto único de falla: Toda la conectividad externa de la Casa Matriz depende de un único firewall y un solo enlace de Internet. Una falla de hardware en este nodo aislaría a la sede principal y desconectaría inmediatamente la Planta de Procesamiento en Chiquimula.

- Vulnerabilidad ante infecciones de rápida propagación: La ausencia de segmentación en la red interna (/16) significa que un incidente menor en una computadora de escritorio puede propagarse libremente hacia los servidores vitales y los controladores industriales (PLC) de las líneas de procesamiento.


- Imposibilidad de recuperación efectiva: Almacenar los respaldos en cinta dentro de la misma sala que aloja los servidores de producción anula cualquier capacidad de recuperación ante un desastre físico (incendio, inundación) o un ataque avanzado de secuestro de datos.

- Ausencia total de detección y respuesta ante incidentes: no existe un SIEM ni un plan formal de respuesta a incidentes, lo que significa que un ataque puede pasar desapercibido durante días o semanas, incrementando su alcance y el daño potencial.

- Accesos de terceros sin control: los proveedores externos cuentan con accesos permanentes y compartidos al ERP y otros sistemas, sin monitoreo ni cuentas individuales, lo que representa una puerta de entrada adicional difícil de rastrear en caso de incidente.
