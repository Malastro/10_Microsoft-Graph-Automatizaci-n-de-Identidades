# Lab10: Microsoft Graph & Automatización de Identidades

## 1. Descripción del proyecto

La que se avecina — Temporada 2, Episodio 20: «Un método ilícito».

En este episodio, Maxi recurre a un método poco ortodoxo para conseguir que en el bar Henry & Max puedan ver los partidos de fútbol utilizando una señal de televisión de pago de Antonio Recio. La operación se lleva a cabo al margen de los procedimientos establecidos y sin autorización.

En Mirador de Montepinar S.L. se ha detectado un problema de naturaleza similar, aunque trasladado al ámbito de la seguridad informática. Algunos procesos de administración de identidades dependen de credenciales personales de administradores o de secretos almacenados directamente en scripts. Esto supone un riesgo para la seguridad, dificulta la trazabilidad de las operaciones y puede provocar accesos excesivos o no controlados.

Enrique Pastor plantea una alternativa: dejar de utilizar identidades personales para ejecutar tareas automatizadas y establecer identidades de aplicación independientes, con autenticación mediante certificados digitales y permisos específicos.

A partir de esta propuesta, la comunidad decide implantar una solución basada en Microsoft Graph API y PowerShell que permita consultar información de usuarios, auditar identidades y ejecutar acciones administrativas controladas.

El laboratorio desarrollará dos Service Principals independientes: uno destinado a tareas de auditoría y otro dedicado a determinadas acciones de remediación. Ambos utilizarán certificados digitales y permisos de aplicación ajustados a sus funciones.

La solución incorporará controles de acceso, validaciones, gestión de errores y mecanismos de trazabilidad para demostrar cómo automatizar operaciones IAM sin depender de credenciales personales ni conceder privilegios innecesarios.


## 2. Objetivos del proyecto

- Comprender los fundamentos de PowerShell y su aplicación en la administración de identidades.
- Aprender a utilizar Microsoft Graph API para consultar y gestionar recursos de Microsoft Entra ID.
- Desarrollar scripts de PowerShell para automatizar tareas de auditoría de usuarios.
- Comprender las diferencias entre aplicaciones, Service Principals e identidades de usuario.
- Implementar autenticación App-Only mediante certificados digitales y el flujo OAuth 2.0 Client Credentials.
- Configurar dos Service Principals independientes con permisos de aplicación específicos.
- Aplicar el principio de mínimo privilegio mediante la separación de funciones de auditoría y remediación.
- Analizar información de identidades y actividad de inicio de sesión, teniendo en cuenta los requisitos de licencia de Microsoft Entra ID.
- Implementar controles para ejecutar acciones administrativas de forma explícita y segura.
- Utilizar mecanismos de gestión de errores, registro de operaciones y validación de resultados.
- Comprobar mediante pruebas negativas que cada identidad de aplicación está limitada a los permisos que necesita.
- Documentar la arquitectura, las decisiones técnicas y los resultados obtenidos.
  

## 3. Arquitectura del proyecto

La solución se construirá sobre Microsoft Entra ID, Microsoft Graph API y PowerShell. La arquitectura estará basada en dos identidades de aplicación independientes, cada una con permisos específicos y certificados digitales propios.

### 3.1. Componentes principales

**1. Microsoft Entra ID**

Será el directorio central donde se encuentran las identidades de Mirador de Montepinar S.L. Desde aquí se administrarán los registros de aplicaciones, los Service Principals, los certificados públicos y los permisos de Microsoft Graph.

**2. Microsoft Graph API**

Actuará como interfaz de comunicación entre los scripts de PowerShell y los recursos de Microsoft Entra ID. Permitirá consultar información de usuarios y ejecutar operaciones administrativas autorizadas.

**3. PowerShell 7**

Será el entorno utilizado para desarrollar y ejecutar los scripts de auditoría y remediación mediante el SDK de Microsoft Graph.

**4. Certificados digitales**

Se utilizarán para autenticar las aplicaciones mediante el flujo OAuth 2.0 Client Credentials. Cada identidad de aplicación tendrá su propio certificado, evitando depender de contraseñas personales o secretos almacenados directamente en los scripts.

### 3.2. Identidades de aplicación

La arquitectura contará con dos Service Principals:

**SP-Montepinar-Audit**

Identidad destinada exclusivamente a tareas de consulta y auditoría.

Permisos previstos:
- `User.Read.All` (Application): consultar perfiles de usuarios.
- `AuditLog.Read.All` (Application): consultar información de auditoría e inicios de sesión cuando sea necesario.

**SP-Montepinar-Remediation**

Identidad destinada a ejecutar acciones administrativas controladas.

Permiso previsto:
- `User.RevokeSessions.All` (Application): revocar las sesiones de inicio de sesión de usuarios autorizados.

La separación evita que la identidad utilizada para consultar información disponga de permisos de remediación, y que la identidad de remediación tenga acceso innecesario a los perfiles de todos los usuarios.

### 3.3. Modelo de autenticación

Se utilizará autenticación App-Only mediante certificados digitales.

El proceso será el siguiente:

1. PowerShell inicia la conexión con Microsoft Graph utilizando el registro de aplicación correspondiente.
2. La aplicación demuestra su identidad mediante una aserción firmada con su certificado privado.
3. Microsoft Entra ID valida la autenticación y emite un token de acceso.
4. Microsoft Graph comprueba los permisos de aplicación incluidos en el token.
5. Se ejecuta únicamente la operación autorizada.

Las claves privadas permanecerán en el almacén de certificados local. Solo se registrará en Entra ID el certificado público correspondiente.

### 3.4. Separación de responsabilidades

La solución tendrá dos flujos de trabajo independientes:

- **Auditoría:** consulta de usuarios, análisis de información de identidad y generación de informes.
- **Remediación:** revocación controlada de sesiones de usuarios expresamente autorizados.

La remediación incorporará validaciones, confirmación de operaciones y gestión de errores. No se permitirá ejecutar acciones masivas indiscriminadas.

### 3.5. Seguridad y trazabilidad

Se aplicarán los siguientes controles:

- Principio de mínimo privilegio.
- Separación de identidades y certificados.
- Autenticación mediante certificados en lugar de secretos de cliente.
- Restricción de las acciones de remediación a usuarios autorizados.
- Pruebas negativas para comprobar que los permisos no concedidos son rechazados.
- Registro de resultados y errores.
- Verificación de las operaciones mediante los registros disponibles en Microsoft Entra ID.

### 3.6. Arquitectura lógica

PowerShell 7 será el punto de ejecución de los scripts y se comunicará con Microsoft Graph mediante HTTPS.

La identidad `SP-Montepinar-Audit` gestionará las consultas, mientras que `SP-Montepinar-Remediation` se utilizará exclusivamente para las operaciones de revocación de sesiones.

Ambas identidades tendrán certificados y permisos independientes, con consentimiento administrativo concedido en Microsoft Entra ID.

## 4. Fases de implementación

## 5. Conclusiones

## 6. Tecnologías empleadas 

## 7. Futuras mejoras 
