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

## 3. Arquitectura 

## 4. Fases de implementación

## 5. Conclusiones

## 6. Tecnologías empleadas 

## 7. Futuras mejoras 
