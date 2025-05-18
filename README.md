# ActividadTunomatico

## ✅ Descripción General del Sistema
Este proyecto corresponde al modelado arquitectónico completo de un Sistema de Gestión de Turnos Digitales, orientado a optimizar la asignación y atención de turnos en entornos con alta demanda de servicios.
El enfoque del proyecto se basa en buenas prácticas de diseño orientado a objetos, con la aplicación de patrones de diseño reconocidos, para garantizar una arquitectura robusta, escalable y mantenible.
El sistema contempla la transición integral desde los requerimientos funcionales hasta la arquitectura física del software, incluyendo:
- Definición de casos de uso representativos del flujo operativo del sistema.
- Diseño lógico mediante diagramas de clases con patrones de diseño aplicados (como Singleton, Prototype y Adapter).
- Distribución clara de responsabilidades entre capas del sistema (presentación, lógica y persistencia).
---
## 🔍 Objetivos del Modelado
- Modelar integralmente un sistema de gestión de turnos digitales, desde los requerimientos funcionales hasta su arquitectura física.
- Aplicar patrones de diseño orientado a objetos en el diseño lógico, asegurando coherencia con la arquitectura de implementación.
- Fortalecer el pensamiento arquitectónico mediante el uso de diagramas UML (casos de uso, clases, componentes e implementación).
---
## 🔹 1. Diagrama de Casos de Uso UML
![Image](https://github.com/user-attachments/assets/ac59cc2e-f20c-4ea6-9c65-8fc74f47dd74)

### Descripción general
El análisis funcional del sistema Tunomático permitió identificar los actores principales y sus interacciones clave con el sistema, Asimismo, se incorporaron relaciones del tipo <<extend>> para representar acciones opcionales que complementan procesos base, favoreciendo una mayor flexibilidad y modularidad.

### Actores identificados:
- **User**: Puede registrarse, iniciar sesión, registrar turno, cancelar turno y consultar turnos.
- **Administrador**: Tiene acceso a la consulta de turnos y puede extender dicha consulta con la visualización de reportes.
- **Sistema**: Actor externo encargado de emitir notificaciones de turnos de forma automática.

### Cados de uso destacados y relaciones aplicadas:
- **Registrarse**: Permite al usuario crear una cuenta en el sistema.
- **Iniciar Sesión**:Autentica al usuario para acceder a las funcionalidades del sistema.
- **Registrar Turno**: El usuario puede solicitar un nuevo turno en el sistema.
- **Cancelar Turno**: Permite anular un turno previamente asignado al usuario.
- **Consultar Turno**: Funcionalidad central para revisar información de turnos registrador por parte del usuario o el administrador.
- `<<extend>>` **Ver reporte de turnos**: El administrador puede, de forma opcional, acceder a un reporte detallado asociado a los turnos consultados.
- **Notificar Turno**: Proceso automático gestionado por el sistema, que emite recordatorios o confirmaciones de turnos a los usuarios.

### Justificación de las relaciones aplicadas
- Se empleó la relación `<<extend>>` en el caso Consultar Turno, ya que la generación de un reporte detallado no es obligatorio en todos los flujos, sino una funcionalidad opcional especialmente útil para el rol de administrador.
- La separación de responsabilidades entre usuarios, administradores y el sistema asegura una arquitectura clara, reutilizable y fácil de mantener.
- Se reforzó la claridad de los flujos mediante la identificación precisa de actores y la incorporación de relaciones opcionales, cumpliendo con los principios de diseño orientado a objetos. 

### Relación destacada:
**Notificar Turno** representa una interacción automática gestionada por el sistema, que agrega valor al proceso de atención mediante el envío de notificaciones a los usuarios, asegurando recordatorios proactivos y disminuyendo ausencias en la atención.

## 🔹 2. Diagrama de Clases UML con Patrones Aplicados
![imagen](https://github.com/user-attachments/assets/86766c8e-d585-4b55-b3c2-e7122f68b902)

## 🧩 Justificación Arquitectónica y Patrones Aplicados

###Selección de patrones
La arquitectura del sistema Tunomático fue diseñada considerando la reutilización, mantenibilidad y extensibilidad. La selección de los patrones de diseño responde a desafíos clave como la gestión centralizada, la necesidad de clonación eficiente de objetos y la integración con servicios externos de notificación.

### **1. Singleton (`GestiónDeTurnos`)**
#### Justificación:
Se implementó el patrón Singleton en la clase GestiónDeTurnos para garantizar que exista una única instancia responsable de la administración de los turnos del sistema. Esto permite centralizar la lógica de registro, cancelación y consulta, asegurando coherencia y control global sobre las operaciones críticas.

### Intención arquitectónica:
- Centralizar la lógica de negocio de turnos en una única instancia.
- Evitar múltiples puntos de manipulación de los datos de turnos.
- Facilitar futuras integraciones sin comprometer la consistencia del sistema.

---

### **2. Prototype (`Turno`)**
#### Justificación:
Dado que los turnos pueden compartir múltiples atributos y es común que se generen en grandes volúmenes, se aplicó el patrón Prototype en la clase llamada Turno. Este permite clonar turnos base, facilitando la generación de nuevos objetos sin repetir procesos costosos de inicialización.

#### Intención arquitectónica:
- Permitir la creación eficiente de nuevos turnos a partir de plantillas.
- Aumentar la velocidad de procesamiento en escenarios con múltiples usuarios solicitando turnos simultáneamente.
- Reducir la duplicación de código al generar instancias repetitivas.

---

### **3. Adapter (`AdaptarComunicador`)**

#### Justificación:
El sistema requiere notificar a los usuarios sobre eventos relacionados con sus turnos. Para lograr esto, se integró con una API externa (ApiNotificaciones). El patrón Adapter, implementado mediante la clase AdaptarComunicador, permite traducir la interfaz interna Comunicador a la interfaz externa de la API, desacoplando así el núcleo del sistema de dependencias externas.

#### Intención arquitectónica:
- Facilitar la comunicación con servicios de terceros sin afectar la lógica central.
- Posibilitar el reemplazo de la API de notificaciones en el futuro sin refactorizaciones significativas.
- Promover el principio de inversión de dependencias, alineado con buenas prácticas SOLID.

---

### **4. Interface (`Comunicador`)**

#### Justificación:
Se definió la interfaz Comunicador como punto de abstracción para la funcionalidad de notificación. Esto permite aplicar el principio de programación orientada a interfaces, y posibilita la integración de otros canales de notificación (SMS, correo, etc.) sin alterar el sistema base.

#### Intención arquitectónica:
- Promover la extensibilidad del sistema de notificaciones.
- Separar las dependencias concretas de la lógica de negocio.
- Permitir pruebas unitarias mediante mocks del Comunicador.

---


## 🔹 3. Diagrama de Implementación UML
![Image](https://github.com/user-attachments/assets/0f8a349e-3fb5-4a23-b698-3e7df5148c8e)

### Despliegue Físico y decisiones técnicas:
- **Nodos físicos diferenciados** para reforzar seguridad, escalabilidad y disponibilidad:
El sistema se despliega en múltiples nodos claramente separados:
- El Cliente (Nodo lógico o dispositivo del usuario) accede a través de una interfaz web.
- El servidor Web centraliza la lógica de negocio.
- La Base de Datos se aloja en un nodo dedicado para almacenamiento persistente de cuentas y turnos.
- La API de Notificaciones representa un servicio externo independiente al que se accede mediante un adaptador, garantizando bajo acoplamiento.
Separación clara de responsabilidades entre servidores de aplicaciones, lógica de negocio, integración de servicios y base de datos:
- El Controlador Principal gestiona las solicitudes del cliente.
- El AdministradorTurnos (Singleton) regula el acceso concurrente y las operaciones sobre turnos.
- El Servicio de Validación de Cuentas actúa como punto de entrada para autenticación.
- Las bases de datos (BD Cuentas y BD Turnos) se mantienen aisladas del resto del sistema, reforzando la seguridad.

---


## 🧩 Reflexiones Finales del Modelado
Este ejercicio refleja una aproximación arquitectónica donde:
- Cada patrón fue seleccionado según necesidades específicas del sistema Tunomático.
- La transición entre caso de uso ➡ Diagrama de clases ➡ implementación permitió mantener una trazabilidad clara desde el análisis funcional hasta la infraestructura física, garantizando que las decisiones técnicas respondan a necesidades reales del sistema.
- La modularización y aplicación de patrones permitieron diseñar un sistema robusto, flexible, mantenible y alineado con buenas prácticas de ingeniería de software.

Este repositorio busca servir como referencia formal para futuros trabajos de modelado arquitectónico, mostrando los estándares esperados en entornos profesionales de desarrollo.

---




