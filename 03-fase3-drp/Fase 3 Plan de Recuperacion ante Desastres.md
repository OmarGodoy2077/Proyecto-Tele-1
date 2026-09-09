# Plan de Recuperación ante Desastres

## TransAgro del Oriente, S.A.

<p align="center">
  <img src="./Captura%20de%20pantalla%202026-09-08%20194039.png" alt="Logo de la Universidad Mariano Gálvez de Guatemala" width="180">
</p>

**Ruta del logo:** `Proyecto Telecomunicaciones\03-fase3-drp\Captura de pantalla 2026-09-08`

**Universidad Mariano Gálvez de Guatemala — Facultad de Ingeniería en Sistemas de Información**  
**Campus:** Jutiapa · **Curso:** Telecomunicaciones — Área de Especialidad  
**Unidad integradora:** Seguridad de Redes · **Docente:** Ing. Juan Daniel Ramos Martínez  
**Proyecto No. 01 — Segundo Semestre 2026**  
**Integrantes:** _(completar)_ · **Fecha de entrega:** _(completar)_

**Clasificación:** Uso interno — distribución restringida a Dirección, Gerencia de TI y roles de recuperación  
**Responsable del documento:** Especialista en continuidad de negocio, bajo aprobación de la Gerencia de TI  
**Versión:** 0.1 — 8 de septiembre de 2026

## Control de versiones

| Versión | Fecha | Autor / rol | Descripción | Aprobado por |
|---|---|---|---|---|
| 0.1 | 2026-09-08 | Especialista en continuidad de negocio | Redacción inicial del DRP: alcance, supuestos, roles, ocho escenarios, RTO/RPO, sitio alterno tibio y procedimientos de recuperación. | _(pendiente)_ |
| _(siguiente)_ | | | Resultado de pruebas, cambios de arquitectura y aprobación formal. | |

## 1. Información general

### 1.1 Objetivo

Establecer la autoridad, los criterios y los procedimientos para responder, contener y recuperar los servicios tecnológicos críticos de TransAgro del Oriente, S.A. después de una interrupción, desastre físico, falla de infraestructura o incidente de ciberseguridad.

El plan busca reducir el tiempo de indisponibilidad y la pérdida de datos dentro de los objetivos RTO/RPO definidos en la sección 5. Su alcance es tecnológico; la continuidad comercial, financiera y logística debe coordinarse con la Gerencia General y las áreas de negocio.

La estructura aplica el enfoque de planificación de contingencia de NIST SP 800-34 Rev. 1, que relaciona requisitos de recuperación, prioridades, estrategias y procedimientos técnicos (National Institute of Standards and Technology [NIST], 2010). Para incidentes de ciberseguridad se adopta el ciclo de preparación, detección, respuesta y recuperación alineado con NIST SP 800-61 Rev. 3 (NIST, 2025).

### 1.2 Responsable y autoridad

El **Gerente de Tecnología de la Información** es el responsable operativo del DRP y tiene autoridad para activarlo formalmente cuando se cumpla cualquiera de los criterios de la sección 6.3. Si no está disponible, el administrador de sistemas y redes de mayor antigüedad puede activar las medidas inmediatas de contención y notificar al Gerente de TI o a la Gerencia General.

La **Gerencia General** conserva la autoridad para aprobar decisiones de negocio extraordinarias, comunicación externa sensible, contratación urgente y operación prolongada en el sitio alterno. La autoridad técnica para activar la recuperación no debe esperar una aprobación administrativa cuando exista riesgo para la vida, pérdida acelerada de datos o indisponibilidad de un servicio crítico.

### 1.3 Alcance

El DRP cubre:

- Casa Matriz en Jutiapa, Planta de Procesamiento en Chiquimula y sus interconexiones.
- Firewall perimetral, enlaces ISP, VPN sitio a sitio, switches, VLAN, NAC y WiFi.
- ERP y base de datos transaccional, portales de clientes y proveedores, correo corporativo y sistema de rastreo de flotilla.
- Servidores, almacenamiento, respaldos, Active Directory, EDR, SIEM y servicios de administración.
- Aplicaciones de la DMZ, BD backend, integraciones SaaS y accesos de terceros.
- Comunicación con colaboradores, proveedores, clientes, autoridades y proveedores tecnológicos.

No sustituye un plan de evacuación, seguridad ocupacional, continuidad financiera ni un plan de crisis corporativo. Cuando un evento afecte personas o instalaciones, la seguridad humana tiene prioridad sobre la recuperación tecnológica.

### 1.4 Relación con las fases anteriores y posteriores

El DRP toma como insumos la [Fase 1 — Diagnóstico de riesgos](../01-fase1-diagnostico/Fase%201,%20Diagnóstico%20de%20riesgos%20tecnológicos.md), los controles disponibles de la [Fase 2 — Redes internas e identidad](../02-fase2-plan-seguridad/fase2-RedesInternas.md) y los rubros presupuestarios de la [Fase 4 — Adquisición](../04-fase4-adquisicion/Fase%204%20Plan%20de%20Adquisicion%20e%20Implementacion.md).

La Fase 3 convierte los riesgos en escenarios `E-nn`, define RTO/RPO y establece qué inversiones de la Fase 4 son necesarias para que la recuperación sea posible. Los valores de esta versión son objetivos de diseño y deben validarse mediante pruebas, inventario y cotizaciones antes de la aprobación final.

## 2. Condiciones generales y supuestos del plan

### 2.1 Condiciones conocidas

- TransAgro depende de ERP, facturación electrónica, pedidos, trazabilidad de transporte, correo y comunicaciones entre sedes.
- La infraestructura actual tiene un firewall sin alta disponibilidad, un solo ISP, una VPN antigua, red plana, sistemas operativos sin soporte y respaldos locales en cinta.
- No existe actualmente un datacenter alterno, un SOC/CSIRT dedicado ni un plan de respuesta a incidentes aprobado.
- La Planta de Chiquimula dispone de un cuarto de telecomunicaciones y controles de planta, pero el caso no confirma que tenga capacidad de datacenter alterno.
- Los accesos de proveedores, el SaaS de rastreo y el proveedor de nómina deben participar en pruebas y recuperación según sus contratos.

### 2.2 Supuestos adoptados

| ID | Supuesto | Uso y validación requerida |
|---|---|---|
| S-DRP-01 | Se habilitará un sitio alterno **tibio** en Chiquimula para recuperar servicios prioritarios, sin asumir que actualmente existe capacidad de datacenter. | Requiere levantamiento de carga, espacio, climatización, energía, seguridad física y conectividad antes de contratarlo. |
| S-DRP-02 | Se conservará una copia inmutable y cifrada fuera del cuarto de servidores, en nube u otro repositorio con control de acceso separado. | Debe implementarse con `I-Respaldo`, probarse y documentarse la retención. |
| S-DRP-03 | La replicación de datos hacia Chiquimula o la nube se dimensionará para alcanzar RPO de una hora para ERP/BD y rastreo. | Requiere `I-SD-WAN/VPN`, segundo ISP y monitoreo de transferencia. |
| S-DRP-04 | Los RTO/RPO de la sección 5 son objetivos de servicio, no garantías de disponibilidad mientras no se implementen los controles de Fases 2 y 4. | Se revisarán después de cada prueba y cambio importante. |
| S-DRP-05 | Los roles se designan por función, no por nombre, y la Gerencia de TI mantendrá la lista de contactos vigente en el Anexo A. | El Coordinador debe actualizarla trimestralmente. |
| S-DRP-06 | El proveedor de correo, SaaS de rastreo, ISP, MDR/SOC y soporte del ERP entregarán contactos de emergencia y compromisos de atención. | Debe incorporarse al contrato o SLA y probarse al menos una vez al año. |
| S-DRP-07 | La información de clientes, proveedores, empleados y ubicación GPS se tratará como información sensible y se restaurará con controles de acceso y registro. | Validar con Gerencia, Legal y contratos aplicables antes de una recuperación real. |

### 2.3 Principios de recuperación

1. Proteger personas y detener riesgos físicos antes de manipular equipos.
2. Preservar evidencia en incidentes de seguridad; no formatear, reiniciar ni restaurar un equipo comprometido sin autorización del responsable de respuesta.
3. Recuperar primero red, identidad, respaldos y servicios que habilitan otros sistemas.
4. Restaurar desde copias verificadas y limpias, no desde sistemas que todavía presenten indicadores de compromiso.
5. Registrar cada decisión, hora, responsable, evidencia y resultado.
6. Comunicar hechos confirmados, sin especulación, con una sola fuente autorizada.
7. Volver a la operación normal solo después de validar integridad, seguridad, monitoreo y aceptación del propietario del proceso.

## 3. Organización de crisis, recuperación y pruebas

### 3.1 Comité de Crisis

| Rol | Antes del evento | Durante el evento | Después del evento |
|---|---|---|---|
| Gerencia General | Aprobar prioridades, presupuesto y nivel de riesgo aceptable. | Autorizar decisiones extraordinarias, comunicaciones externas y operación prolongada en contingencia. | Aprobar el retorno a operación normal y el informe ejecutivo. |
| Gerente de TI | Mantener el DRP, recursos, contratos y criterios de activación. | Dirigir la activación, priorizar servicios y reportar estado al Comité. | Presidir la revisión posterior y aprobar acciones correctivas. |
| Responsable de Operaciones / Planta | Identificar procesos mínimos de producción, logística y calidad. | Confirmar impacto operativo y aceptar procedimientos manuales o alternos. | Validar que producción y logística hayan recuperado sus servicios. |
| Responsable financiero/administrativo | Mantener prioridades de facturación, pagos y obligaciones. | Evaluar impacto económico, compras urgentes y continuidad de facturación. | Documentar costos, pérdidas evitadas y reclamaciones. |
| Responsable de comunicaciones | Preparar mensajes y canales aprobados. | Emitir comunicados autorizados a personal, clientes, proveedores y medios. | Consolidar el comunicado de cierre y lecciones aprendidas. |
| Asesor legal/privacidad, cuando aplique | Mantener criterios de notificación contractual y regulatoria. | Evaluar exposición de datos, obligaciones de aviso y preservación legal. | Revisar contratos, notificaciones y medidas correctivas. |

### 3.2 Equipo de Recuperación

| Rol | Antes | Durante | Después |
|---|---|---|---|
| Líder técnico de recuperación — Gerente de TI | Mantener procedimientos, prioridades y proveedores. | Coordinar tareas, tiempos, evidencias y escalamiento. | Confirmar cierre técnico y actualizar el DRP. |
| Administradores de sistemas y redes | Mantener inventario, configuraciones, respaldos y accesos. | Recuperar identidad, servidores, red, firewall, VPN y aplicaciones. | Validar parches, hardening, monitoreo y documentación. |
| Técnico de soporte de Planta | Verificar energía, conectividad, equipos locales y condiciones de seguridad. | Ejecutar actividades en Chiquimula y reportar estado físico/operativo. | Confirmar normalización de la Planta y controles pendientes. |
| Responsable de seguridad / MDR-SOC | Mantener detecciones, contactos y procedimientos de incidentes. | Clasificar, contener, investigar y autorizar la limpieza de sistemas comprometidos. | Elaborar informe forense, indicadores y mejoras. |
| Propietario del ERP / proveedor autorizado | Mantener procedimiento de restauración y dependencias. | Validar BD, integridad transaccional y operación funcional del ERP. | Aceptar la recuperación y corregir defectos de la aplicación. |
| Proveedor de nube, respaldo, ISP o SaaS | Mantener contactos y SLA. | Ejecutar soporte contratado, restauración, failover o escalamiento. | Entregar informe de servicio y acciones preventivas. |

### 3.3 Equipo de Pruebas

| Rol | Responsabilidad |
|---|---|
| Coordinador de pruebas | Aprobar alcance, escenario, criterios de éxito y reglas de seguridad. |
| Representante de auditoría/calidad | Verificar evidencias, tiempos, trazabilidad y cumplimiento del DRP. |
| Administrador de sistemas y redes | Ejecutar restauraciones, conmutaciones y validaciones técnicas. |
| Representante de negocio | Probar pedidos, facturación, proveedores, logística y comunicación. |
| Responsable de seguridad/MDR-SOC | Incluir escenarios de compromiso, aislamiento y preservación de evidencia. |
| Proveedor involucrado | Participar cuando el servicio sea SaaS, nube, ISP, ERP o respaldo administrado. |

Ninguna prueba debe modificar producción sin ventana aprobada, respaldo verificado, plan de reversión y autorización del Gerente de TI.

### 3.4 Autoridad de activación

| Nivel | Criterio | Autoridad | Acción |
|---|---|---|---|
| P1 — desastre mayor | Riesgo para personas/instalación; pérdida del datacenter; ransomware extendido; pérdida de ERP/BD; o indisponibilidad prevista mayor que el RTO. | Gerente de TI, o administrador senior si está incomunicado; notificación inmediata a Gerencia General. | Activar formalmente el DRP, reunir Comité y pasar a sitio alterno si corresponde. |
| P2 — interrupción crítica | Firewall, VPN, ISP o portal fuera de servicio y sin solución estimada dentro del RTO; compromiso limitado de DMZ. | Gerente de TI. | Activar el procedimiento del escenario, escalar a proveedores y decidir si se requiere Comité. |
| P3 — incidente controlable | Falla aislada con solución dentro del RTO y sin impacto significativo a procesos críticos. | Administrador responsable. | Aplicar operación normal, registrar evento y notificar al Gerente de TI. |

## 4. Escenarios de desastre contemplados

| ID | Escenario | Riesgo relacionado | Debilidades raíz | Prioridad | Procedimiento principal |
|---|---|---|---|---|---|
| E-01 | No disponibilidad del centro de datos por incendio, inundación, falla de A/C o corte eléctrico prolongado. | R-05, R-09, R-10 | D-12, D-13, D-14 | Crítica/Alta | Evacuación, aislamiento, evaluación, activación de sitio tibio y restauración priorizada. |
| E-02 | Falla o compromiso del firewall perimetral único. | R-02 | D-02, D-04 | Crítica | Failover al NGFW HA cuando exista; si no, reemplazo controlado y reglas mínimas. |
| E-03 | Caída del enlace VPN entre sedes. | R-08 | D-03 | Alta | Diagnóstico, enlace alterno, túnel IKEv2 y operación temporal aislada. |
| E-04 | Incidente en la DMZ con movimiento lateral hacia la BD interna. | R-01, R-04, R-06, R-07 | D-01, D-05, D-07, D-17 | Crítica | Aislamiento, preservación de evidencia, erradicación, restauración limpia y revisión de accesos. |
| E-05 | Ransomware con cifrado de servidores de archivos y/o ERP. | R-03, R-04, R-05 | D-06, D-07, D-08, D-09, D-10, D-11, D-14, D-15 | Crítica | Aislamiento, análisis, recuperación desde copia inmutable, validación y retorno gradual. |
| E-06 | Pérdida o corrupción de respaldos. | R-05 | D-14 | Alta | Congelar eliminaciones, preservar copias alternativas, validar integridad y recuperar del nivel más confiable. |
| E-07 | Sismo, tormenta tropical o inundación estacional en la región oriental. | R-05, R-09, R-10 | D-12, D-13, D-14 | Alta | Seguridad humana, evaluación de sedes, activación del sitio alterno y operación degradada. |
| E-08 | Interrupción prolongada del ISP único. | R-02 | D-04 | Crítica | Conmutar segundo ISP/LTE contratado, priorizar tráfico y escalar al proveedor. |

## 5. Componentes críticos, RTO y RPO

Los objetivos siguientes se fijan por impacto de negocio, dependencia entre servicios y capacidad de recuperación propuesta. RTO significa el tiempo máximo objetivo para restablecer el servicio; RPO representa la antigüedad máxima aceptable de los datos recuperados. Los objetivos serán válidos después de implementar y probar los controles relacionados.

| Componente | RTO objetivo | RPO objetivo | Justificación de negocio | Dependencias / inversión |
|---|---:|---:|---|---|
| ERP y base de datos transaccional | 4 horas | 1 hora | Sostiene pedidos, facturación, inventario, proveedores y trazabilidad. Una indisponibilidad mayor afecta ventas y operación de ambas sedes. | Identidad, red, almacenamiento, `I-Respaldo`, `I-SIEM`, `I-Segmentación-VLAN`. |
| Portal de Clientes y Portal de Proveedores | 8 horas | 4 horas | Son importantes para pedidos y recepción documental, pero se puede usar un canal manual temporal mientras se restaura el servicio. | DMZ, WAF, capa de servicios, ERP/BD, `I-WAF`, `I-Segmentación-DMZ`. |
| Correo corporativo | 4 horas | 4 horas | Es el canal de coordinación interna y con terceros; la pérdida de algunos mensajes puede mitigarse con colas y canales alternos. | Identidad, MFA, proveedor de correo, `I-MFA`, `I-FiltradoCorreo`. |
| Enlace VPN entre sedes | 2 horas | N/A para datos; 24 h para la última configuración respaldada | Sin VPN se pierde la operación integrada entre Jutiapa y Chiquimula. El RPO se expresa como antigüedad máxima de la configuración, no como pérdida de transacciones. | NGFW, ISP alterno, `I-SD-WAN/VPN`, `I-SegundoISP`. |
| Sistema de Rastreo de Flotilla | 4 horas | 1 hora, sujeto al SaaS | La operación logística y la trazabilidad de transporte requieren ubicación reciente; el histórico puede depender del proveedor SaaS. | API/SaaS, secretos rotados, conectividad, `I-GestiónSecretos`, `I-SIEM`. |
| Infraestructura de red: firewall y switch core | 2 horas | 4 horas para configuración | Es prerrequisito para recuperar cualquier otro servicio. La alta disponibilidad reduce el RTO efectivo después de la implementación. | NGFW HA, configuración versionada, `I-NGFW-HA`, `I-Segmentación-VLAN`, `I-UPS`. |

### 5.1 Regla de prioridad de recuperación

1. Seguridad de personas, energía, climatización y acceso físico.
2. Conectividad de gestión, firewall, switch core, DNS, identidad y VPN.
3. Repositorios de respaldo y plataforma de virtualización/almacenamiento.
4. ERP/BD transaccional.
5. Correo y portales de clientes/proveedores.
6. Rastreo de flotilla e integraciones no esenciales.
7. Sistemas secundarios, reportes y servicios de conveniencia.

## 6. Árbol de llamadas, notificación y activación

### 6.1 Árbol de llamadas

```text
Quien detecta el evento
(usuario, soporte, planta, monitoreo o proveedor)
        │
        ▼
Administrador de sistemas y redes / Técnico de Planta
        │  registra hora, servicio afectado y evidencia inicial
        ▼
Gerente de TI
        │
        ├── Incidente P3: asigna técnico, registra y cierra
        │
        ├── Incidente P2: notifica al proveedor correspondiente
        │                 y convoca soporte técnico ampliado
        │
        └── Incidente P1: activa DRP y convoca Comité de Crisis
                         │
                         ├── Gerencia General
                         ├── Operaciones / Planta
                         ├── Finanzas / Administración
                         ├── Comunicaciones / Legal
                         ├── MDR-SOC, ERP, ISP, nube y respaldo
                         └── Clientes/proveedores/autoridades, según impacto
```

### 6.2 Procedimiento de notificación

1. El detector informa por el canal primario de incidentes; si no está disponible, utiliza teléfono y luego un canal alterno previamente aprobado.
2. El receptor registra fecha, hora, persona, sede, servicio, síntomas, acciones realizadas y riesgo para personas.
3. El administrador de turno notifica al Gerente de TI dentro de 15 minutos para un posible P1/P2.
4. El Gerente de TI clasifica el evento, asigna responsable, abre bitácora y determina si se preserva evidencia.
5. Para P1, convoca al Comité de Crisis y a los equipos técnicos; la primera notificación ejecutiva debe emitirse dentro de 30 minutos.
6. El responsable de comunicaciones mantiene reportes periódicos con hora de próxima actualización, aunque no existan nuevos datos.

### 6.3 Criterios y procedimiento de activación

Se activa formalmente el DRP cuando se cumple al menos una de estas condiciones:

- El datacenter no es seguro, no es accesible o no puede sostener servicios críticos.
- El ERP/BD, la red central o la conectividad entre sedes estarán fuera del RTO objetivo.
- Existe ransomware, compromiso de DMZ con indicios de movimiento lateral o pérdida de control administrativo.
- El respaldo primario está destruido, cifrado, corrupto o no puede restaurarse.
- Un evento físico o del ISP afecta la operación de ambas sedes o amenaza con prolongarse.

El Gerente de TI documenta la hora de activación, escenario, nivel, servicios afectados, estrategia seleccionada, responsables, criterios de escalamiento y autorización de retorno. Si el evento involucra seguridad de personas, la activación técnica se realiza después de la coordinación de emergencia correspondiente.

## 7. Procedimientos de recuperación y contingencia por escenario

### 7.1 Acciones comunes para cualquier escenario

| Actividad | Responsable | Evidencia / criterio de salida |
|---|---|---|
| Proteger personas y detener exposición física | Operaciones / Técnico de Planta | Área segura y autorización para ingresar. |
| Abrir bitácora y clasificar P1/P2/P3 | Gerente de TI / administrador | Ticket o registro con hora, impacto y responsable. |
| Identificar servicios, sedes, activos y datos afectados | Equipo de Recuperación | Lista de alcance y dependencias. |
| Preservar logs, memoria, imágenes o configuraciones cuando sea incidente de seguridad | Responsable de seguridad/MDR-SOC | Evidencia almacenada con integridad y cadena de custodia. |
| Contener sin destruir evidencia | Administradores / seguridad | Segmento, cuenta o sistema aislado; decisión registrada. |
| Seleccionar recuperación primaria, sitio tibio o nube | Gerente de TI / Comité | Estrategia y RTO/RPO aceptados. |
| Ejecutar restauración y pruebas funcionales | Equipo de Recuperación / propietario del servicio | Evidencia de restauración y aceptación del propietario. |
| Comunicar estado y cerrar | Comunicaciones / Gerente de TI | Informe, lecciones aprendidas y acciones correctivas. |

### 7.2 E-01 — No disponibilidad del centro de datos

| Paso | Actividad | Responsable |
|---:|---|---|
| 1 | Activar seguridad física, evacuar si corresponde y solicitar evaluación de instalaciones, energía, agua, humo y climatización. | Operaciones / Gerencia General |
| 2 | Declarar P1 si la sala no es segura o el servicio no podrá restablecerse dentro del RTO. | Gerente de TI |
| 3 | Desconectar energía o red solo cuando sea necesario para evitar daño adicional; no ingresar sin autorización. | Técnico de Planta / proveedor físico |
| 4 | Confirmar último respaldo verificable, estado de la copia inmutable y conectividad con Chiquimula/nube. | Administradores / responsable de respaldo |
| 5 | Preparar el sitio tibio de Chiquimula: energía, conectividad, firewall, switching, almacenamiento y control de acceso temporal. | Administradores / Técnico de Planta |
| 6 | Restaurar primero gestión, identidad, DNS, firewall/VPN y plataforma de respaldo. | Administradores de sistemas y redes |
| 7 | Restaurar ERP/BD con la copia más reciente dentro del RPO y ejecutar validación de integridad. | Administrador de BD / proveedor ERP |
| 8 | Restaurar correo, portales y rastreo según la prioridad de la sección 5.1. | Equipo de Recuperación / proveedores |
| 9 | Validar transacciones de prueba, accesos MFA, segmentación, logs y operación de los propietarios de negocio. | Propietarios de servicio / seguridad |
| 10 | Comunicar operación degradada, registrar tiempos y decidir si se mantiene el sitio alterno o se retorna. | Comité de Crisis |

**Criterio de recuperación:** ERP/BD opera con transacción de prueba aceptada, respaldos nuevos funcionando, monitoreo activo y aprobación de Operaciones y Finanzas.

### 7.3 E-02 — Falla o compromiso del firewall perimetral único

| Paso | Actividad | Responsable |
|---:|---|---|
| 1 | Confirmar si es falla eléctrica, de hardware, configuración o compromiso; preservar logs. | Administrador de redes / seguridad |
| 2 | Aislar el equipo comprometido y bloquear cambios no autorizados. | Administrador de redes |
| 3 | Si existe NGFW HA, conmutar al miembro sano y verificar reglas mínimas, VPN, DMZ y salida a Internet. | Administrador de redes |
| 4 | Si aún no existe HA, activar equipo de reemplazo o configuración de contingencia aprobada. | Gerente de TI / proveedor |
| 5 | Validar conectividad desde usuarios, Planta, portales y proveedores autorizados; no abrir reglas amplias para acelerar. | Administradores / seguridad |
| 6 | Revisar indicadores de compromiso y rotar credenciales si el equipo fue administrado por terceros. | Responsable de seguridad |
| 7 | Documentar causa, configuración restaurada y acciones para eliminar el punto único de falla. | Gerente de TI |

### 7.4 E-03 — Caída de la VPN entre sedes

| Paso | Actividad | Responsable |
|---:|---|---|
| 1 | Confirmar alcance: ISP, equipo local, túnel, rutas o autenticación. | Administrador de redes |
| 2 | Revisar logs, disponibilidad de ambos extremos y cambios recientes. | Administrador de redes |
| 3 | Activar segundo ISP/SD-WAN o enlace alterno, si está disponible. | Administrador de redes / ISP |
| 4 | Levantar túnel IKEv2/IPsec con parámetros aprobados; no reactivar IKEv1/3DES/SHA-1. | Administrador de redes |
| 5 | Mantener operación local de la Planta con procedimientos manuales si la restauración supera dos horas. | Operaciones / Técnico de Planta |
| 6 | Probar rutas, DNS, ERP, autenticación y registro de transacciones antes de cerrar. | Administradores / propietarios |

### 7.5 E-04 — Incidente en la DMZ con movimiento lateral hacia la BD

| Paso | Actividad | Responsable |
|---:|---|---|
| 1 | Clasificar P1, activar al responsable de seguridad/MDR-SOC y preservar logs del firewall, WAF, servidores y BD. | Gerente de TI / seguridad |
| 2 | Bloquear temporalmente la publicación afectada y aislar el servidor comprometido de la DMZ. | Administrador de redes |
| 3 | Restringir tráfico DMZ→interna a lo indispensable; bloquear conexión directa a BD si no está justificada. | Administrador de redes |
| 4 | Suspender o limitar cuentas de proveedores y rotar secretos de APIs; conservar evidencia de sesiones. | Administrador de sistemas / seguridad |
| 5 | Determinar alcance: aplicación, sistema operativo, BD, credenciales, datos y movimiento lateral. | MDR-SOC / proveedor aplicativo |
| 6 | Notificar al Comité de Crisis y evaluar obligaciones contractuales o de privacidad. | Gerente de TI / Legal |
| 7 | Tomar imágenes y exportar logs antes de reconstruir, cuando sea técnicamente posible. | MDR-SOC / proveedor forense |
| 8 | Reconstruir el servicio desde una imagen limpia y código verificado; parchear y cambiar secretos. | Proveedor ERP/aplicativo / administradores |
| 9 | Restaurar datos solo desde copia validada; comprobar que no haya persistencia en la BD interna. | Administrador de BD / seguridad |
| 10 | Aplicar WAF, segmentación, ACL y reglas de mínimo privilegio; validar con pruebas de seguridad. | Administrador de redes / seguridad |
| 11 | Habilitar publicación gradual y monitoreo reforzado por al menos 24 horas. | Gerente de TI / MDR-SOC |
| 12 | Emitir informe de causa raíz, datos afectados, controles pendientes y aceptación del propietario del portal. | Responsable de seguridad / Comité |

**Criterio de recuperación:** no existen indicadores activos, los secretos fueron rotados, la BD está validada, la comunicación DMZ→interna está restringida y el propietario del servicio acepta la operación.

### 7.6 E-05 — Ransomware en archivos y/o ERP

| Paso | Actividad | Responsable |
|---:|---|---|
| 1 | Activar P1 y aislar inmediatamente equipos, servidores o VLAN afectadas; retirar conectividad WiFi si es necesario. | Administradores / Técnico de Planta |
| 2 | No pagar, no borrar evidencia y no restaurar sobre sistemas comprometidos sin aprobación técnica. | Comité / seguridad |
| 3 | Determinar alcance inicial, paciente cero, cuentas utilizadas, servidores cifrados y respaldos accesibles. | MDR-SOC / administradores |
| 4 | Deshabilitar cuentas comprometidas, sesiones de proveedores y mecanismos de propagación; preservar logs. | Administrador de sistemas |
| 5 | Proteger y verificar la copia inmutable, fuera del sitio y cualquier medio desconectado. | Responsable de respaldo |
| 6 | Notificar al Comité, proveedor MDR/SOC, proveedor ERP, aseguradora y asesor legal cuando corresponda. | Gerente de TI / Legal |
| 7 | Crear imágenes o muestras forenses de equipos representativos antes de limpiar. | MDR-SOC / proveedor forense |
| 8 | Reconstruir primero identidad, red, administración y plataforma de respaldo en entorno limpio. | Administradores de sistemas y redes |
| 9 | Restaurar ERP/BD a un punto anterior al compromiso, verificar integridad y reconciliar transacciones manuales. | Administrador de BD / proveedor ERP / Finanzas |
| 10 | Restaurar archivos y estaciones por prioridad, con EDR, parches, MFA y segmentación antes de conectarlas. | Administradores / seguridad |
| 11 | Mantener los sistemas recuperados aislados hasta completar escaneo, revisión de cuentas y validación de logs. | MDR-SOC |
| 12 | Validar procesos de pedidos, facturación, proveedores, inventario, rastreo y comunicación. | Propietarios de negocio |
| 13 | Reabrir conectividad gradualmente y monitorear por 72 horas; conservar imágenes y evidencias. | Gerente de TI / seguridad |
| 14 | Documentar causa raíz, pérdida de datos, controles fallidos y plan de remediación. | Comité de Crisis |

**Criterio de recuperación:** no hay cifrado activo ni cuentas comprometidas, los sistemas están parcheados y protegidos, la restauración fue verificada y los propietarios aceptaron los datos recuperados.

### 7.7 E-06 — Pérdida o corrupción de respaldos

| Paso | Actividad | Responsable |
|---:|---|---|
| 1 | Suspender tareas de retención/eliminación y proteger todos los medios restantes. | Responsable de respaldo |
| 2 | Determinar si la corrupción afecta cinta, repositorio, catálogo, nube o credenciales. | Administradores / seguridad |
| 3 | Verificar copia inmutable, réplica en Chiquimula, copia desconectada y respaldos de aplicaciones. | Equipo de Recuperación |
| 4 | No confiar en un respaldo hasta completar una restauración de prueba y verificación de integridad. | Administrador de BD / propietario |
| 5 | Recuperar el servicio crítico desde la copia más antigua que cumpla el RPO disponible. | Gerente de TI / equipo técnico |
| 6 | Notificar pérdida de datos potencial y evaluar continuidad manual con el Comité. | Gerencia / Legal |
| 7 | Rehacer la política 3-2-1-1-0, credenciales, retención y pruebas antes de cerrar. | Gerente de TI |

### 7.8 E-07 — Sismo, tormenta tropical o inundación

| Paso | Actividad | Responsable |
|---:|---|---|
| 1 | Priorizar evacuación, primeros auxilios y comunicación con autoridades; no exponer personal para recuperar equipos. | Operaciones / Gerencia General |
| 2 | Evaluar si Jutiapa, Chiquimula o ambas sedes son accesibles y seguras. | Operaciones / Técnico de Planta |
| 3 | Activar P1 si la sede principal no puede operar o hay daño ambiental/energético prolongado. | Gerente de TI |
| 4 | Habilitar sitio tibio y copia en nube si la sede alterna también está afectada. | Equipo de Recuperación |
| 5 | Recuperar conectividad, identidad, respaldos y ERP conforme a la prioridad de la sección 5.1. | Administradores |
| 6 | Mantener operación degradada y registrar transacciones manuales para reconciliación posterior. | Operaciones / Finanzas |
| 7 | Revisar acceso físico, CCTV, humedad, temperatura, UPS y planta antes de reocupar el datacenter. | Técnico de Planta / proveedor físico |
| 8 | Documentar daño, gastos, decisiones y mejoras de resiliencia geográfica. | Comité de Crisis |

### 7.9 E-08 — Interrupción prolongada del ISP único

| Paso | Actividad | Responsable |
|---:|---|---|
| 1 | Confirmar la interrupción con el ISP, registrar número de ticket y solicitar ETA/SLA. | Administrador de redes |
| 2 | Conmutar al segundo ISP o enlace inalámbrico/LTE contratado, priorizando VPN, ERP, correo y gestión. | Administrador de redes |
| 3 | Aplicar políticas de ancho de banda y suspender tráfico no esencial. | Administrador de redes |
| 4 | Validar WAF, portales, VPN, autenticación MFA, DNS y comunicación con la Planta. | Administradores / seguridad |
| 5 | Informar a usuarios y proveedores sobre operación degradada; registrar servicios no disponibles. | Comunicaciones / Gerente de TI |
| 6 | Cerrar solo después de confirmar estabilidad, rutas, monitoreo y análisis de causa con el ISP. | Gerente de TI |

## 8. Centro de control y sitio alterno de operaciones

### 8.1 Estrategia seleccionada

Se propone un **sitio alterno tibio en la Planta de Procesamiento de Chiquimula**, complementado con una **copia inmutable cifrada fuera del sitio o en nube**. La estrategia no afirma que el cuarto de telecomunicaciones actual ya sea un datacenter: requiere acondicionamiento y validación.

El sitio tibio tendrá capacidad preparada para recibir o restaurar los componentes prioritarios, pero no necesariamente todos los servicios simultáneamente. Esta decisión equilibra el costo y la urgencia: una alternativa caliente sería más rápida, pero exigiría duplicar buena parte de los 18 servidores y servicios; una alternativa fría no cumpliría los RTO de ERP, red y VPN.

### 8.2 Arquitectura de contingencia

| Capa | Operación normal | Contingencia | Rubro relacionado |
|---|---|---|---|
| Conectividad | ISP primario y VPN entre sedes. | Segundo ISP/SD-WAN, failover y túneles IKEv2. | `I-SD-WAN/VPN`, `I-SegundoISP`. |
| Perímetro | Firewall perimetral en Jutiapa. | NGFW HA o equipo de contingencia con reglas mínimas aprobadas. | `I-NGFW-HA`. |
| Datos | ERP/BD y servicios en Jutiapa. | Réplica/restauración priorizada en Chiquimula; copia inmutable en nube. | `I-Respaldo`. |
| Aplicaciones | Portales en DMZ y servicios internos. | Publicación gradual desde entorno limpio y segmentado. | `I-WAF`, `I-Segmentación-DMZ`. |
| Energía/físico | Datacenter principal. | UPS ampliado, planta, control físico y sensores en las áreas utilizadas. | `I-UPS`, `I-Planta`, `I-ControlAccesoFísico`, `I-MonitoreoAmbiental`. |
| Detección | Logs dispersos y sin SOC actual. | SIEM, observabilidad y MDR/SOC con acceso a ambas sedes. | `I-SIEM`, `I-Observabilidad`, `I-TalentoSOC`. |

### 8.3 Condiciones mínimas para declarar operativo el sitio tibio

- Área físicamente separada de riesgos previsibles de la operación industrial, con acceso autorizado.
- Capacidad eléctrica, UPS, climatización, detección de agua/humo y conectividad suficiente.
- Switches, firewall, VLAN, ACL y administración separadas de los PLC y cámaras.
- Credenciales de emergencia almacenadas en una bóveda y con MFA; cuentas nominadas y temporales.
- Procedimiento probado para restaurar ERP/BD, correo, VPN y portales.
- Copia inmutable accesible aun si las credenciales o la red de Jutiapa están comprometidas.
- Contratos con ISP, nube, respaldo, ERP y MDR/SOC con contactos de emergencia.

### 8.4 Decisión si ambas sedes están afectadas

Si Jutiapa y Chiquimula no son utilizables, el Gerente de TI activa la restauración desde la copia inmutable hacia la nube o un proveedor de infraestructura contratado. La operación se limita inicialmente a ERP/BD, identidad, correo y servicios de coordinación; los portales se habilitan después de completar validaciones de seguridad.

## 9. Manejo de crisis y comunicación

### 9.1 Principios

- Informar rápido, periódicamente y con hechos confirmados.
- Mantener una sola línea de comunicación externa autorizada.
- No divulgar detalles técnicos que faciliten el ataque ni atribuir causas sin evidencia.
- Separar la comunicación operativa, ejecutiva, contractual y pública.
- Conservar una bitácora de mensajes, destinatarios, hora y responsable.
- Coordinar con Legal/Privacidad las notificaciones por exposición de información.

### 9.2 Audiencias y mensajes

| Audiencia | Responsable | Contenido mínimo |
|---|---|---|
| Gerencia General y Comité | Gerente de TI | Impacto, nivel, servicios afectados, RTO/RPO, decisiones requeridas y próxima actualización. |
| Colaboradores | Comunicaciones / TI | Qué servicios usar, qué no conectar, canales alternos y cómo reportar síntomas. |
| Clientes | Comunicaciones / Comercial | Disponibilidad de pedidos, facturación y canales temporales; sin especulación técnica. |
| Proveedores agrícolas y logísticos | Operaciones / Compras | Procedimiento manual, recepción de documentos y estado del rastreo. |
| Proveedores tecnológicos | Gerente de TI | Alcance técnico, evidencia disponible, SLA solicitado y autorización de acceso. |
| Autoridades, aseguradora o asesoría legal | Gerencia / Legal | Hechos confirmados, impacto, medidas tomadas y documentación requerida. |
| Medios o público | Vocero autorizado | Mensaje aprobado por Gerencia General y Legal. |

La guía de CISA recomienda mantener un plan de respuesta y comunicaciones, aislar sistemas afectados, preservar evidencia y probar regularmente los respaldos durante un incidente de ransomware (Cybersecurity and Infrastructure Security Agency [CISA] et al., 2023). Estas prácticas se incorporan en E-04, E-05 y E-06.

## 10. Mantenimiento y pruebas del DRP

| Actividad | Periodicidad | Responsable | Evidencia / criterio de éxito |
|---|---|---|---|
| Revisión de contactos y árbol de llamadas | Trimestral y después de cada cambio de personal | Coordinador / Gerente de TI | Lista aprobada y prueba de contacto. |
| Revisión de inventario, dependencias y propietarios | Trimestral | Administradores / propietarios de servicio | Inventario versionado. |
| Restauración de una muestra de archivos y una VM no productiva | Mensual | Responsable de respaldo | Restauración íntegra dentro del tiempo definido. |
| Prueba de copia inmutable y acceso de emergencia | Trimestral | Administrador de respaldos / seguridad | Hash/integridad, permisos y bitácora. |
| Ejercicio de mesa para ransomware o DMZ | Trimestral | Comité / MDR-SOC | Decisiones, tiempos y brechas documentadas. |
| Prueba de VPN/ISP alterno y árbol de activación | Semestral | Administrador de redes / ISP | Túnel operativo y failover probado sin pérdida no autorizada. |
| Prueba de recuperación de ERP/BD en sitio tibio | Semestral | Equipo de Recuperación / ERP | RTO/RPO medidos y aceptación de Finanzas/Operaciones. |
| Ejercicio integral de sitio alterno | Anual | Equipo de Pruebas / Comité | Informe con objetivos alcanzados, fallas y plan de remediación. |
| Revisión extraordinaria | Después de incidente, cambio mayor o nueva aplicación | Gerente de TI | Nueva versión del DRP y aprobación. |

### 10.1 Criterios de aprobación de una prueba

Una prueba se considera satisfactoria cuando: el equipo fue notificado dentro del tiempo objetivo; la copia utilizada fue identificada y verificada; el servicio se restauró dentro del RTO; la pérdida de datos no superó el RPO; se validaron controles de acceso y monitoreo; el propietario del proceso aceptó el resultado; y las fallas tienen responsable y fecha de corrección.

## 11. Distribución del documento y control de cambios

### 11.1 Distribución

El documento completo se entrega de forma controlada al Gerente de TI, Gerencia General, Comité de Crisis, Equipo de Recuperación, Equipo de Pruebas, responsable de seguridad/MDR-SOC y proveedores que necesiten ejecutar una actividad. Las copias impresas o digitales deben tener versión y fecha; no se deben conservar copias obsoletas en sitios operativos.

Los anexos con contactos, credenciales de emergencia, diagramas detallados o información de proveedores se distribuyen por separado y con acceso restringido. Las credenciales nunca deben escribirse en este documento.

### 11.2 Control de cambios

| Cambio | Responsable de proponer | Revisión | Aprobación |
|---|---|---|---|
| Modificación de RTO/RPO | Propietario del proceso / Gerente de TI | Comité de Crisis y Finanzas/Operaciones | Gerencia General para cambios de prioridad o costo |
| Nuevo sistema o dependencia | Propietario de aplicación / Administradores | Responsable de seguridad y Equipo de Pruebas | Gerente de TI |
| Cambio de sitio alterno o proveedor | Gerente de TI / Adquisiciones | Seguridad, Operaciones, Legal y proveedor | Gerencia General |
| Cambio posterior a incidente o prueba | Coordinador del DRP | Comité de Crisis | Gerente de TI; Gerencia General cuando afecte continuidad corporativa |

Toda modificación debe registrar versión, fecha, descripción, motivo, secciones afectadas, autor, revisor, aprobador y fecha de la próxima prueba.

## Anexo A — Árbol de llamadas y registro de contactos

La versión operativa debe completar la siguiente tabla sin publicar nombres ni teléfonos en documentos de distribución amplia:

| Rol | Titular / suplente | Canal primario | Canal alterno | Tiempo objetivo de respuesta | Última prueba |
|---|---|---|---|---:|---|
| Gerente de TI | _(completar)_ | _(completar)_ | _(completar)_ | 15 min | _(fecha)_ |
| Administrador de sistemas | _(completar)_ | _(completar)_ | _(completar)_ | 15 min | _(fecha)_ |
| Administrador de redes | _(completar)_ | _(completar)_ | _(completar)_ | 15 min | _(fecha)_ |
| Técnico de Planta | _(completar)_ | _(completar)_ | _(completar)_ | 15 min | _(fecha)_ |
| Responsable de seguridad/MDR-SOC | _(completar)_ | _(completar)_ | _(completar)_ | 30 min | _(fecha)_ |
| Proveedor ERP | _(completar)_ | _(completar)_ | _(completar)_ | SLA | _(fecha)_ |
| ISP primario/alterno | _(completar)_ | _(completar)_ | _(completar)_ | SLA | _(fecha)_ |
| Proveedor de respaldo/nube | _(completar)_ | _(completar)_ | _(completar)_ | SLA | _(fecha)_ |

## Anexo B — Trazabilidad de escenarios

| Escenario | Debilidades | Riesgos | Control o medida relacionada | Inversión relacionada |
|---|---|---|---|---|
| `E-01` | `D-12`, `D-13`, `D-14` | `R-05`, `R-09`, `R-10` | Seguridad física, energía y respaldos | `I-ControlAccesoFísico`, `I-MonitoreoAmbiental`, `I-UPS`, `I-Planta`, `I-Respaldo` |
| `E-02` | `D-02`, `D-04` | `R-02` | Firewall HA y redundancia de ISP | `I-NGFW-HA`, `I-SegundoISP` |
| `E-03` | `D-03` | `R-08` | VPN IKEv2/SD-WAN | `I-SD-WAN/VPN` |
| `E-04` | `D-01`, `D-05`, `D-07`, `D-17` | `R-01`, `R-04`, `R-06`, `R-07` | WAF, DMZ segmentada, MFA, PAM, SIEM | `I-WAF`, `I-Segmentación-DMZ`, `I-MFA`, `I-PAM`, `I-SIEM` |
| `E-05` | `D-06`, `D-07`, `D-08`, `D-09`, `D-10`, `D-11`, `D-14`, `D-15` | `R-03`, `R-04`, `R-05`, `R-07` | Segmentación, NAC, EDR, parches, respaldos y concientización | `I-Segmentación-VLAN`, `I-NAC`, `I-EDR`, `I-Parches`, `I-Respaldo`, `I-Concientización` |
| `E-06` | `D-14` | `R-05` | Copias 3-2-1-1-0 y pruebas de restauración | `I-Respaldo` |
| `E-07` | `D-12`, `D-13`, `D-14` | `R-05`, `R-09`, `R-10` | Sitio tibio, energía, sensores y copia externa | `I-UPS`, `I-Planta`, `I-Respaldo` |
| `E-08` | `D-04` | `R-02` | Segundo ISP y conmutación | `I-SegundoISP` |

## Referencias

Cybersecurity and Infrastructure Security Agency, Federal Bureau of Investigation, National Security Agency, & Multi-State Information Sharing and Analysis Center. (2023). *#StopRansomware guide*. https://www.cisa.gov/resources-tools/resources/stopransomware-guide

National Institute of Standards and Technology. (2010). *Contingency planning guide for federal information systems* (Special Publication 800-34 Rev. 1). https://csrc.nist.gov/pubs/sp/800/34/r1/upd1/final

National Institute of Standards and Technology. (2024). *The NIST Cybersecurity Framework (CSF) 2.0* (NIST CSWP 29). https://doi.org/10.6028/NIST.CSWP.29

National Institute of Standards and Technology. (2025). *Incident response recommendations and considerations for cybersecurity risk management: A CSF 2.0 community profile* (Special Publication 800-61 Rev. 3). https://csrc.nist.gov/pubs/sp/800/61/r3/final

## Nota de aplicación

Este DRP es un documento académico aplicado al caso ficticio de TransAgro. Los datos no definidos por el enunciado —capacidad exacta del sitio alterno, número de equipos, proveedores, contactos, kVA, licencias y SLA— son supuestos de diseño y deben validarse antes de ejecutar una contratación o una recuperación real.
