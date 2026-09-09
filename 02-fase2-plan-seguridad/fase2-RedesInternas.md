# CONTENIDO PARA EL ROL 4 - FASE 2

## 4. Políticas de Seguridad Informática (Extractos para Redes e Identidad)

### 4.X. Política de Identidad, Autenticación y Control de Acceso
1. **Autenticación Multifactor (MFA):** Es obligatorio el uso de MFA para todo acceso remoto (VPN), acceso a correo corporativo, consolas de administración de servidores y el dominio interno. *[Mitiga D-05, R-07]*
2. **Gestión de Contraseñas:** Las contraseñas deben cumplir con los lineamientos del NIST SP 800-63B (mínimo 8 caracteres, sin requisitos de complejidad arbitrarios que obliguen a rotaciones frecuentes, pero con bloqueo ante intentos fallidos y verificación contra listas de contraseñas filtradas). *[Mitiga D-06]*
3. **Acceso de Terceros:** Todo proveedor externo deberá contar con una cuenta individual, nominada y temporal, revocada automáticamente al finalizar su actividad. Queda estrictamente prohibido el uso de credenciales compartidas. *[Mitiga D-17, R-06]*

### 4.Y. Política de Segmentación y Seguridad de Red
1. **Segmentación Lógica:** La red de TransAgro del Oriente, S.A. deberá operar bajo un modelo de "Confianza Cero" (Zero Trust) mediante VLANs estrictas, aislando por completo la red de Tecnología de Operación (OT/ PLCs) de la red corporativa. *[Mitiga D-07, R-03]*
2. **Control de Acceso a la Red (NAC):** Ningún dispositivo podrá obtener conectividad IP en la red cableada o inalámbrica corporativa sin antes autenticarse mediante 802.1X y cumplir con las políticas de postura de seguridad. *[Mitiga D-09, R-03]*

## 5. Responsabilidades
1. **Gerente de Tecnología de la Información:** Aprobar la política de segmentación de red y el presupuesto para la adquisición de la solución NAC y licencias MFA. Autorizar los accesos excepcionales de proveedores externos.
2. **Administradores de Sistemas y Redes (Casa Matriz y Chiquimula):** Configurar y mantener las VLANs en los switches de acceso y distribución. Gestionar las políticas de autenticación 802.1X en el controlador de dominio. Auditar mensualmente los logs de acceso de proveedores externos.
3. **Usuarios Finales:** Proteger sus credenciales, no compartir tokens de MFA y reportar inmediatamente la pérdida de dispositivos o credenciales. Conectarse únicamente a la red WiFi corporativa autenticada.

## 6. Medidas y Procedimientos

### 6.5. Identificación, autenticación y control de acceso

#### Procedimiento 6.5.1: Implementación de Autenticación Multifactor (MFA)
1. **Objetivo:** Mitigar el riesgo de suplantación de identidad y robo de credenciales (R-07).
2. **Alcance:** VPN, Correo Corporativo (Microsoft 365 / Exchange), Dominio (Active Directory) y consolas de administración.
3. **Descripción:** Se implementará MFA basado en *push notifications* o tokens TOTP (ej. Microsoft Authenticator o Cisco Duo). Para el acceso administrativo a servidores y firewalls, se exigirá MFA físico (llave de seguridad FIDO2) o certificado digital.
4. **Trazabilidad:** Da cumplimiento directo a la debilidad D-05 y mitiga el riesgo R-07.

#### Procedimiento 6.5.2: Gestión de Accesos de Proveedores Externos
1. **Objetivo:** Eliminar los accesos permanentes y compartidos de terceros (R-06).
2. **Descripción:**
   1. Se crearán cuentas individuales en el directorio activo para cada proveedor (ej. `prov_erp_juanperez`).
   2. Se implementará un sistema de *Privileged Access Management* (PAM) o, en su defecto, un portal de acceso remoto que grabe las sesiones.
   3. Las cuentas se configurarán con fecha de expiración automática.
   4. Se aplicará el principio de mínimo privilegio, restringiendo el acceso solo a los módulos del ERP o servidores estrictamente necesarios.
3. **Trazabilidad:** Da cumplimiento directo a la debilidad D-17 y mitiga el riesgo R-06.

### 6.8. Seguridad en redes

#### Procedimiento 6.8.1: Rediseño y Segmentación de Red por VLANs
1. **Objetivo:** Detener el movimiento lateral de malware y aislar los activos críticos (R-03).
2. **Descripción:** Se eliminará la red plana (/16) actual. Se implementará el siguiente esquema de VLANs en los switches de la Casa Matriz (Jutiapa) y la Planta (Chiquimula), aplicando Listas de Control de Acceso (ACLs) en el firewall o switch de capa 3 para restringir el tráfico entre ellas:

| ID VLAN | Nombre | Descripción | Restricciones de Acceso (ACL) |
| :--- | :--- | :--- | :--- |
| **10** | VLAN-ADMIN | Estaciones de trabajo administrativas y finanzas. | Acceso a Internet y VLAN-Servidores (puertos específicos). |
| **20** | VLAN-SERVERS | Servidores ERP, Correo, Archivos, AD. | Solo recibe tráfico de VLAN-ADMIN y VLAN-DMZ (puertos 443/80). |
| **30** | VLAN-OT | Controladores industriales (PLC), SCADA (Planta Chiquimula). | Aislamiento total. Solo comunicación con VLAN-SERVERS (puertos industriales específicos). Sin acceso a Internet. |
| **40** | VLAN-CCTV | Cámaras IP y NVR. | Solo comunicación con el NVR y estaciones de seguridad. |
| **50** | VLAN-VOICE | Telefonía IP (si aplica). | Tráfico priorizado (QoS). |
| **99** | VLAN-GUEST | Red de invitados y dispositivos personales. | Aislamiento total. Solo acceso a Internet. Sin acceso a ninguna VLAN interna. |

3. **Trazabilidad:** Da cumplimiento directo a la debilidad D-07 y mitiga el riesgo R-03.

#### Procedimiento 6.8.2: Implementación de Control de Acceso a la Red (NAC)
1. **Objetivo:** Evitar que dispositivos no autorizados o infectados se conecten a la red (R-03).
2. **Descripción:** Se desplegará una solución NAC (ej. Cisco ISE, FortiNAC o Aruba ClearPass) configurada en modo *Monitor* inicialmente y luego en modo *Enforcement*.
   1. **Autenticación 802.1X:** Los puertos de los switches y la red WiFi corporativa requerirán autenticación de usuario/dispositivo contra el Active Directory.
   2. **Evaluación de Postura:** Antes de otorgar acceso, el NAC verificará que el equipo tenga el antivirus/EDR activo y el sistema operativo parcheado. Si no cumple, se le asignará a una *VLAN de Cuarentena* para remediación.
   3. **Perfilado de Dispositivos:** Los dispositivos que no soporten 802.1X (ej. impresoras, cámaras IP, PLCs) serán autenticados mediante *MAC Authentication Bypass (MAB)* y restringidos estrictamente a su VLAN correspondiente.
3. **Trazabilidad:** Da cumplimiento directo a la debilidad D-09 y mitiga el riesgo R-03.

#### Procedimiento 6.8.3: Seguridad en Redes Inalámbricas (WiFi)
1. **Objetivo:** Eliminar el riesgo de la clave WPA2-Personal compartida (R-03).
2. **Descripción:**
   1. **SSID Corporativo (TransAgro-Secure):** Configurado con WPA3-Enterprise (o WPA2-Enterprise), autenticación 802.1X contra el directorio activo. Cada usuario se conecta con sus credenciales personales.
   2. **SSID Invitados (TransAgro-Guest):** Red completamente aislada (VLAN 99), con portal cautivo que acepte términos y condiciones. Acceso exclusivo a Internet, con limitación de ancho de banda.
3. **Trazabilidad:** Da cumplimiento directo a la debilidad D-08 y mitiga el riesgo R-03.

---

## Anexo X: Tabla de Trazabilidad (Redes Internas e Identidad)
*(Esta tabla es obligatoria según el ítem 2.D.4 del Checklist Maestro. Agrégala al final de tu sección o en el anexo general del documento).*

| Debilidad (Fase 1) | Riesgo (Fase 1) | Política / Medida Implementada (Fase 2) |
| :--- | :--- | :--- |
| **D-05:** Sin 2FA en accesos internos. | **R-07:** Suplantación de identidad. | Procedimiento 6.5.1: Implementación de MFA en VPN, correo y consolas. |
| **D-06:** Cuentas compartidas y sin política de contraseñas. | **R-03, R-07:** Propagación malware / Phishing. | Política 4.X y Proc. 6.5.1: Gestión de contraseñas NIST y cuentas nominadas. |
| **D-07:** Red plana sin segmentación. | **R-03:** Propagación masiva de malware. | Procedimiento 6.8.1: Rediseño de red por VLANs (especialmente aislamiento OT). |
| **D-08:** WiFi con clave compartida. | **R-03:** Propagación masiva de malware. | Procedimiento 6.8.3: WPA3-Enterprise y SSID de invitados aislado. |
| **D-09:** Sin solución NAC. | **R-03:** Propagación masiva de malware. | Procedimiento 6.8.2: Implementación de NAC con 802.1X y evaluación de postura. |
| **D-17:** Accesos permanentes de proveedores. | **R-06:** Acceso no monitoreado de terceros. | Procedimiento 6.5.2: Cuentas temporales, individuales y auditoría de sesiones. |

---

