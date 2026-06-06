# Capítulo IV: Solution Software Design

## 4.1. Strategic-Level Domain-Driven Design.

### 4.1.1. Design-Level EventStorming.

El Strategic-Level Domain-Driven Design constituye la base fundamental para el desarrollo de la aplicación Clair. Este enfoque nos permite identificar y definir los límites de los contextos de dominio, establecer las relaciónes entre ellos y crear una arquitectura de software sólida que soporte los objetivos del negocio.
En esta fase estratégica, nos enfocamos en:

- Comprensión profunda del dominio: Identificación de los procesos de negocio críticos

- Definición de bounded contexts: Establecimiento de límites claros entre diferentes áreas funciónales

- Modelado de relaciónes: Definición de cómo interactúan los diferentes contextos

- Arquitectura de alto nivel: Diseño de la estructura general del sistema

#### 4.1.1.1 Candidate Context Discovery.

En esta etapa se desarrolló el Design-Level EventStorming, tomando como insumo el *Big Picture*, el *Ubiquitous Language* y los artefactos previamente definidos (*commands*, *policies* y *read models*).

El objetivo fue descender desde una comprensión general del negocio hacia un nivel de diseño técnico, permitiendo modelar el comportamiento del sistema con mayor precisión.

Se modelaron los 12 flujos principales de Clair, estructurados bajo la siguiente secuencia:

$$
\text{Actor} \rightarrow \text{Command} \rightarrow \text{Constraint} \rightarrow \text{Domain Event} \rightarrow \text{Policy} \rightarrow \text{Command} \rightarrow \text{Domain Event} \rightarrow \text{Read Model}
$$

Adicionalmente, se identificaron:
- Sistemas externos relevantes dentro de los flujos 
- *Hotspots* o zonas de alta complejidad y riesgo 

Como resultado, el equipo transitó de una fase de entendimiento del negocio (*“qué ocurre”*) hacia una definición clara del comportamiento del sistema (*“cómo debe implementarse”*), estableciendo límites, responsabilidades y reglas explícitas para su desarrollo.

El **Candidate Context Discovery** corresponde al proceso de identificación de fronteras de dominio candidatas (*Bounded Contexts*) a partir de patrones de lenguaje, reglas de negocio, responsabilidades y niveles de acoplamiento observados en los eventos del sistema.

En esta actividad, el equipo agrupó comportamientos que comparten un propósito común y consistencia interna, evitando la coexistencia de capacidades que evolucionan a ritmos distintos dentro de un mismo contexto. Este enfoque permite preservar la coherencia del modelo y reducir fricciones en la evolución del sistema.

Como resultado, se definieron los siguientes bounded context:

- **IAM (Identity \& Access Management)** 
- **Billing** 
- **Device \& Space Management** 
- **Air Quality Evaluation** 
- **Alerting \& Response** 
- **Analytics \& Reporting** 

Esta partición permite:
- Una asignación más clara de *ownership* por dominio 
- Reducir la ambigüedad en la conversación técnico-funciónal 
- Mejorar la trazabilidad entre decisiones de negocio y diseño de software 

En paralelo, se definieron doce flujos principales *end-to-end*, representando los recorridos críticos del sistema:

**Leyenda de Elementos**

<p align="center">
 <img src="https://i.imgur.com/nqINlqg.png" width="500">
</p>
**1. User Registration and Access Activation**

Este flujo gestiona la creación de nuevas identidades en la plataforma. El sistema captura los datos del aspirante, valida los requisitos de seguridad y activa el acceso tras confirmar la identidad.

<p align="center">
 <img src="https://i.imgur.com/3MbRs9Z.png" width="700">
</p>
**2. Login and Session Start**

Describe el proceso de validación de credenciales para usuarios existentes. Una vez autenticado, el sistema inicia una sesión segura y otorga los permisos necesarios según el rol asignado (**Home User** o **Facility Admin**).

<p align="center">
 <img src="https://i.imgur.com/jvEigtT.png" width="700">
</p>
**3. Trial and Subscription Lifecycle**

Gestiona el estado de la cuenta del usuario, desde la activación del período de prueba de 30 días hasta la transición a planes suscritos, controlando el acceso a las funciónes premium del ecosistema.

<p align="center">
 <img src="https://i.imgur.com/7wSa5xs.png" width="700">
</p>
**4. Checkout and Payment Outcome**

Representa el flujo financiero donde se procesan las transacciones de suscripción. El sistema valida el método de pago y confirma el resultado de la operación para actualizar el nivel de servicio del cliente.

<p align="center">
 <img src="https://i.imgur.com/1dgJLHX.png" width="700">
</p>
**5. Facility and Space Setup**

Flujo orientado principalmente al Facility Admin para la estructuración lógica de sus establecimientos. Permite segmentar el local en zonas específicas para una monitorización más precisa y organizada.

<p align="center">
 <img src="https://i.imgur.com/PopJW9Q.png" width="700">
</p>
**6. Device Onboarding**

Es el proceso técnico de vinculación de hardware. Incluye la lectura del código único del sensor Clair y su registro en la base de datos de la plataforma para comenzar la transmisión de datos.

<p align="center">
 <img src="https://i.imgur.com/FDUiEL9.png" width="700">
</p>
**7. Threshold Management**

Permite a los usuarios definir los parámetros de seguridad para $CO_2$ y partículas. Este flujo establece los límites que el motor de reglas utilizará para evaluar la calidad del aire de forma personalizada.

<p align="center">
 <img src="https://i.imgur.com/dEGlvX9.png" width="700">
</p>
**8. Telemetry Ingestion and Validation**

Gestiona la recepción de datos y valida su integridad. Incluye almacenamiento local (Offline) cuando se pierde la conexión, permitiendo la sincronización automática por lotes al restablecerse el internet para evitar brechas en el historial de calidad del aire.

<p align="center">
 <img src="https://i.imgur.com/R7wW3kx.png" width="700">
</p>
**9. Air Quality Evaluation**

Es el motor de procesamiento donde la telemetría se compara contra los umbrales configurados. Este flujo determina el estado ambiental en tiempo real (Seguro, Advertencia o Crítico).

<p align="center">
 <img src="https://i.imgur.com/qkJ8oVo.png" width="700">
</p>
**10. Critical Alert Management**

Flujo de respuesta inmediata ante picos de contaminación. Se encarga de la generación y envío de notificaciones *push* y alertas visuales cuando el aire representa un riesgo para la salud.

<p align="center">
 <img src="https://i.imgur.com/TTe7xX5.png" width="700">
</p>
**11. Corrective Action Orchestration**

Gestiona la ejecución de comandos hacia los actuadores. Este flujo coordina la apertura de ventanas o el encendido de extractores de forma autónoma según las reglas de automatización configuradas.

<p align="center">
 <img src="https://i.imgur.com/ffAxj7b.png" width="700">
</p>
**12. Reporting and Insights**

 Proceso de síntesis de datos históricos. Transforma la telemetría acumulada en reportes semanales de salud y visualizaciones de tendencias para la toma de decisiones informadas.

<p align="center">
 <img src="https://i.imgur.com/RzEd1me.png" width="700">
</p>

Cada flujo fue modelado de manera independiente y detallada, utilizando *post-its* atómicos (sin combinación de elementos), lo que asegura que cada evento, comando, regla y reacción se mantenga explícito y alineado con el *Ubiquitous Language* del dominio.

El tablero completo del Candidate Context Discovery puede visualizarse en el siguiente enlace: https://bit.ly/3QwYkAS

#### 4.1.1.2 Domain Message Flows Modeling.

El Domain Message Flows Modeling mapea cómo los mensajes (eventos, comandos) fluyen entre los diferentes bounded contexts identificados. Este modelado es crucial para entender las dependencias y patrones de comunicación del sistema.

**User Registration and Access Activation**

<p align="center">
<img src="../assets/domain-message-flows/DMF1.jpg" alt="c4-container" width="700">
</p>

Esta vista muestra el workflow para el registro y activación de usuarios, destacando cómo el sistema IAM (Identity and Access Management) centraliza la seguridad y la gestión de sesiónes. El proceso asegura el desacoplamiento de responsabilidades: la Website actúa como interfaz de captura, el IAM valida la identidad y el ciclo de vida de la cuenta, mientras que el Email Service gestiona la comunicación externa de forma independiente. Finalmente, el uso de tokens y la persistencia en el Internal Storage garantizan que solo los usuarios verificados obtengan acceso.

**Login and Session Start**

<p align="center">
<img src="../assets/domain-message-flows/DMF2.jpg" alt="c4-container" width="700">
</p>

Esta vista detalla el proceso de Login e Inicio de Sesión, ilustrando cómo el sistema organiza la autenticación y la autorización mediante un componente central de IAM. El flujo comienza cuando el usuario proporciona sus credenciales a través de la Website, la cual delega la validación y la asignación de permisos por rol al IAM para garantizar un control de acceso seguro y centralizado. Una vez autenticado, el estado de la sesión se persiste en el Internal Storage, permitiendo que el usuario consulte servicios especializados como la Air Quality Evaluation en tiempo real, cuyas interacciones son registradas por el módulo de Analytics & Reporting para auditoría y análisis posterior.

**Trial Subscription Lifecycle**

<p align="center">
<img src="../assets/domain-message-flows/DMF3.jpg" alt="c4-container" width="700">
</p>

Esta vista describe el ciclo de vida de una Suscripción de Prueba, mostrando cómo se gestiona la elegibilidad y activación mediante un servicio centralizado de Billing. El flujo comienza cuando el Home User solicita iniciar una prueba a través de la Website, la cual se encarga de validar la elegibilidad del usuario antes de procesar la solicitud con el módulo de facturación. Una vez que el servicio de Billing confirma el inicio de la suscripción, se genera un registro con el ID de suscripción y la fecha de expiración, información que se persiste finalmente en el Internal Storage para asegurar que el acceso temporal del usuario quede correctamente documentado y administrado.

**Paid Subscription Lifecycle**

<p align="center">
<img src="../assets/domain-message-flows/DMF4.jpg" alt="c4-container" width="700">
</p>
Esta vista describe el Ciclo de Vida de la Suscripción de Pago, detallando los procesos de actualización y cancelación de servicios por parte del usuario. El flujo se inicia en la Website, que actúa como intermediaria para enviar solicitudes de cambio de plan o desactivación hacia el módulo de Billing. Para cambios de plan, el sistema coordina el procesamiento del pago a través de un Payment Gateway externo; una vez confirmado, o en caso de una desactivación, se actualiza el registro correspondiente en el Internal Storage para reflejar el nuevo estado de la suscripción y el ciclo de facturación actual del usuario.

**Checkout and Payment Outcome**

<p align="center">
<img src="../assets/domain-message-flows/DMF5.jpg" alt="c4-container" width="700">
</p>

Esta vista describe el proceso de Checkout y Resultado de Pago, ilustrando cómo la plataforma integra la validación de identidad con la ejecución de servicios en tiempo real. El flujo inicia cuando el usuario se autentica a través de la Website, la cual coordina con el IAM para validar credenciales y obtener permisos específicos de rol que se persisten en el Internal Storage. Una vez establecida la sesión, el sistema permite la consulta de estados mediante la Air Quality Evaluation, cuyos resultados y tipos de consulta son registrados por el módulo de Analytics & Reporting para garantizar la trazabilidad y el análisis de cada transacción completada.

**Facility and Space Setup**

<p align="center">
<img src="../assets/domain-message-flows/DMF6.jpg" alt="c4-container" width="700">
</p>
Esta vista detalla el proceso de Configuración de Instalaciones y Espacios, ilustrando cómo el sistema gestiona la creación de infraestructura bajo un esquema de control de acceso centralizado. El flujo comienza cuando el Facility Admin solicita la creación de una instalación a través de la Website, la cual coordina con el IAM para validar el rol administrativo y los límites de creación permitidos. Una vez autorizado, el módulo de Facility Management registra la instalación y permite la configuración de espacios específicos (interiores o exteriores), verificando siempre su existencia previa antes de persistir los detalles finales en el Internal Storage para asegurar una administración organizada y auditable.

**Initial Device Setup**

<p align="center">
<img src="../assets/domain-message-flows/DMF7.jpg" alt="c4-container" width="700">
</p>
Esta vista describe el proceso de Configuración Inicial del Dispositivo, ilustrando cómo se vincula el hardware con la cuenta del usuario de forma segura. El flujo comienza cuando el Home User solicita el emparejamiento a través de la Website, la cual se comunica con el módulo de Device & Space Management para validar la propiedad y disponibilidad del modelo mediante su número de serie. Una vez que el dispositivo es reconocido y vinculado con éxito, el sistema confirma el registro y persiste los datos de la asociación en el Internal Storage, garantizando que el equipo esté listo para su monitoreo y gestión dentro del entorno del usuario.

**Device Location Setup**

<p align="center">
<img src="../assets/domain-message-flows/DMF8.jpg" alt="c4-container" width="700">
</p>
Esta vista detalla el proceso de Configuración de la Ubicación del Dispositivo, donde se asigna un equipo específico a un entorno previamente definido. El flujo inicia cuando el usuario solicita la asignación a través de la Website, la cual interactúa con el módulo de Facility Management para verificar la disponibilidad y validez del espacio seleccionado. Una vez confirmada la ubicación, el servicio de Device Management procesa los detalles de la instalación y notas adicionales, persistiendo el registro final con su respectiva marca de tiempo en el Internal Storage para asegurar la trazabilidad geográfica del hardware.

**Threshold Management**

<p align="center">
<img src="../assets/domain-message-flows/DMF9.jpg" alt="c4-container" width="700">
</p>

Esta vista describe el proceso de Gestión de Umbrales, donde se definen los límites de alerta para sensores de CO2, PM y temperatura. El flujo comienza cuando el usuario solicita un cambio de umbral a través de la Website, la cual coordina con el IAM para autorizar la operación según el rol y espacio asignado. Una vez validado, el servicio de Air Quality Evaluation actualiza los límites del espacio y evalúa posibles brechas en tiempo real mediante su lógica interna, persistiendo los nuevos umbrales y marcas de tiempo en el Internal Storage para el monitoreo continuo de la calidad del aire.

**Telemetry Ingestion**

<p align="center">
<img src="../assets/domain-message-flows/DMF10.jpg" alt="c4-container" width="700">
</p>
Esta vista describe el proceso de Ingesta de Telemetría, describiendo cómo el sistema procesa los datos enviados por los sensores en tiempo real. El flujo comienza cuando el Sensor Device envía un lote de lecturas al módulo de Device & Space Management, el cual actúa como receptor central para organizar y persistir los datos de las métricas. Posteriormente, esta información se distribuye hacia el componente de Analytics & Reporting para su almacenamiento histórico en series de tiempo dentro del Internal Storage, y simultáneamente hacia la Air Quality Evaluation, donde se evalúa la calidad del aire actual para activar respuestas inmediatas basadas en las lecturas recibidas.

**Telemetry Validation**

<p align="center">
<img src="../assets/domain-message-flows/DMF11.jpg" alt="c4-container" width="700">
</p>
Esta vista describe el proceso de Validación de Telemetría, donde el sistema asegura la integridad de los datos recibidos antes de su procesamiento. El flujo inicia en el módulo de Device & Space Management, que utiliza su lógica interna para validar el estado del dispositivo y la firma del payload. Si la lectura es válida, los datos limpios se envían a la Air Quality Evaluation para su análisis; de lo contrario, la lectura es rechazada y se registra el error en el Internal Storage para auditoría, garantizando que solo información confiable afecte las evaluaciones de calidad del aire.

**Offline Reading Synchronization**

<p align="center">
<img src="../assets/domain-message-flows/DMF12.jpg" alt="c4-container" width="700">
</p>
Esta vista describe el proceso de Sincronización de Lecturas Offline, ilustrando cómo el sistema recupera la continuidad de los datos tras un periodo de desconexión del hardware. El flujo inicia cuando el Sensor Device recupera la conectividad y envía un lote de lecturas almacenadas localmente al módulo de Device & Space Management, el cual confirma la recepción del paquete de datos. Finalmente, el sistema procesa el lote para integrar la telemetría histórica en el Internal Storage, garantizando que el registro de métricas esté completo y sincronizado con la marca de tiempo correspondiente para evitar vacíos en el análisis de la calidad del aire.

**Alerting & Response to Air Quality Evaluation**

<p align="center">
<img src="../assets/domain-message-flows/DMF13.jpg" alt="c4-container" width="700">
</p>
Esta vista ilustra el flujo de Alertas y Respuesta ante la Evaluación de Calidad del Aire, describiendo la reacción del sistema ante la detección de niveles críticos de CO2, PM o temperatura. El proceso se activa cuando el módulo de Air Quality Evaluation detecta un incumplimiento de umbrales, notificando al componente de Alerting & Response, el cual consulta al IAM para obtener las preferencias de contacto y canales de notificación del usuario. Finalmente, se despacha una notificación de emergencia de alta prioridad y se registra el evento en el Internal Storage, permitiendo una respuesta inmediata tanto a través de la lógica interna del sistema como mediante alertas directas a los administradores responsables.

**Critical Alert Generation & Notification**

<p align="center">
<img src="../assets/domain-message-flows/DMF14.jpg" alt="c4-container" width="700">
</p>
Esta vista describe el proceso de Generación y Notificación de Alertas Críticas, ilustrando la respuesta automatizada del sistema ante eventos de alta severidad en la calidad del aire. El flujo se activa cuando el módulo de Air Quality Evaluation detecta una violación de umbral crítica, lo que dispara en el componente de Alerting & Response la creación de una alerta con estado "abierto" y su respectiva persistencia en el Internal Storage. Simultáneamente, se coordina el envío de una notificación por correo electrónico a través de un Email Provider externo, registrando el ID de entrega y la marca de tiempo para asegurar que los usuarios responsables reciban información inmediata sobre el estado del espacio monitoreado.

**Alert Acknowledgement & Tracking**

<p align="center">
<img src="../assets/domain-message-flows/DMF15.jpg" alt="c4-container" width="700">
</p>
Esta vista ilustra el proceso de Reconocimiento y Seguimiento de Alertas, describiendo cómo el sistema gestiona la respuesta humana ante incidentes detectados. El flujo se activa cuando un usuario reconoce una alerta a través de la interfaz, lo que dispara en el componente de Alerting & Response el cambio de estado de la alerta a "en progreso", persistiendo esta actualización en el Internal Storage para asegurar la trazabilidad de la atención. Finalmente, el sistema interactúa con la lógica interna para actualizar el tablero de alertas activas del usuario, garantizando que el equipo responsable tenga una visibilidad en tiempo real de los eventos pendientes y aquellos que ya están siendo gestionados.

**Corrective Action & Resolution**

<p align="center">
<img src="../assets/domain-message-flows/DMF16.jpg" alt="c4-container" width="700">
</p>
Esta vista ilustra el proceso de Acción Correctiva y Resolución, describiendo cómo el sistema y el usuario colaboran para cerrar incidentes de calidad del aire. El flujo comienza cuando el sistema envía un recordatorio de acción correctiva basado en el tiempo transcurrido, procesado por el módulo de Alerting & Response. Una vez que el usuario ejecuta y registra la resolución con sus respectivas notas, el sistema actualiza el estado de la alerta a "cerrado" en el Internal Storage y sincroniza el centro de notificaciones a través de la lógica interna, garantizando que el ciclo del incidente finalice de manera documentada y auditable.

**Automatic Corrective Action Execution**

<p align="center">
<img src="../assets/domain-message-flows/DMF17.jpg" alt="c4-container" width="700">
</p>
Esta vista detalla el proceso de Ejecución Automática de Acciones Correctivas, ilustrando cómo el sistema responde de forma autónoma ante brechas críticas en la calidad del aire. El flujo se activa cuando el sistema detecta un nivel de CO2 persistente, lo que dispara en el componente de Alerting & Response una orden de ventilación de alta prioridad enviada directamente a los Smart Devices para abrir las ventanas inteligentes. Finalmente, una vez ejecutada la acción, el sistema confirma la apertura de los dispositivos y persiste el registro de la ejecución en el Internal Storage, garantizando una mitigación inmediata del riesgo sin necesidad de intervención manual.

**Manual Corrective Action Selection**

<p align="center">
<img src="../assets/domain-message-flows/DMF18.jpg" alt="c4-container" width="700">
</p>
Esta vista detalla el proceso de Selección Manual de Acción Correctiva, ilustrando cómo el usuario puede intervenir directamente para mitigar problemas de calidad del aire. El flujo inicia cuando el User selecciona un tipo de acción específica a través del componente de Alerting & Response, el cual valida la coherencia de la solicitud con el estado actual del entorno mediante su lógica interna. Una vez confirmada la validez y registrado el comando con un indicador de anulación manual en el Internal Storage, el sistema procede a la ejecución inmediata sobre los Smart Devices, asegurando que la respuesta del sistema se adapte a las necesidades puntuales detectadas por el operador.

**Corrective Action Recording & Timeline**

<p align="center">
<img src="../assets/domain-message-flows/DMF19.jpg" alt="c4-container" width="700">
</p>
Esta vista ilustra el proceso de Registro y Cronología de Acciones Correctivas, detallando cómo el sistema documenta cada intervención para mantener un historial preciso de mitigación. El flujo comienza en el módulo de Alerting & Response, que inicia el registro de la acción capturando métricas iniciales y marcas de tiempo en el Internal Storage. Una vez finalizada la intervención, se procesan los datos del cierre, lo que permite al sistema actualizar la línea de tiempo de acciones correctivas dentro del almacenamiento interno, garantizando que cada evento sea auditable y contribuya al análisis de efectividad de las respuestas ante incidentes.

**Automated Data Aggregation & Digest Generation**

<p align="center">
<img src="../assets/domain-message-flows/DMF20.jpg" alt="c4-container" width="700">
</p>
Esta vista describe el proceso de Agregación Automática de Datos y Generación de Resúmenes, ilustrando cómo el sistema transforma la telemetría histórica en información accionable para el usuario. El flujo se activa cuando el sistema solicita la agregación de datos de las últimas 24 horas al módulo de Analytics & Reporting, el cual consulta las reglas de agregación mediante la lógica interna para procesar la información almacenada en el Internal Storage. Finalmente, el sistema genera un resumen diario personalizado por dispositivo y notifica su disponibilidad a través del Notifications Center, asegurando que el usuario tenga acceso a un análisis consolidado de la calidad del aire sin necesidad de revisar lecturas individuales.

**Strategic Insight Identification**

<p align="center">
<img src="../assets/domain-message-flows/DMF21.jpg" alt="c4-container" width="700">
</p>
Esta vista describe el proceso de Identificación de Insights Estratégicos, ilustrando cómo el sistema utiliza el análisis de datos para optimizar el bienestar en los espacios monitoreados. El flujo comienza cuando el sistema solicita identificar la mejor hora de ventilación al módulo de Analytics & Reporting, el cual procesa métricas de rendimiento almacenadas en el Internal Storage. Una vez identificada la hora óptima con un alto puntaje de confianza, el componente utiliza la lógica interna para generar una recomendación específica de ventilación para el espacio, permitiendo una gestión proactiva y eficiente de la calidad del aire basada en patrones históricos de los últimos 7 días.

**On-Demand Historical Reporting & Access Control**

<p align="center">
<img src="../assets/domain-message-flows/DMF22.jpg" alt="c4-container" width="700">
</p>
Esta vista describe el proceso de Reportes Históricos bajo Demanda y Control de Acceso, detallando cómo el sistema restringe o permite la visualización de tendencias según el plan del usuario. El flujo inicia cuando el usuario solicita una vista de tendencias mensuales al módulo de Analytics & Reporting, el cual coordina con la Internal Logic para verificar los permisos de visibilidad y límites del plan actual. Si el acceso es autorizado, se genera el reporte y se notifica al usuario a través del Notifications Center; de lo contrario, la previsualización se bloquea indicando que se ha alcanzado el límite del plan gratuito, garantizando así la integridad del modelo de suscripción mientras se recuperan los datos del Internal Storage.

El tablero completo del Domain Message Flows Modeling. puede visualizarse en el siguiente enlace: https://bit.ly/3QwYkAS

#### 4.1.1.3 Bounded Context Canvases.

A continuación se presentan los Context Canvases de los contextos de Clair, donde se describen sus responsabilidades, relaciónes, eventos clave, reglas de negocio, etc.

**IAM (Identity \& Access Management)**

El **Bounded Context Canvas** del módulo **Air Quality Monitoring** define el núcleo operativo de Clair, estableciendo los límites de responsabilidad para el procesamiento de datos ambientales.

- **Propósito:** Monitorear y evaluar la calidad del aire en tiempo real para generar alertas y ejecutar respuestas automáticas.
- **Capacidades:** Incluye la ingesta de telemetría, el monitoreo del estado de los sensores y la evaluación de niveles de contaminantes basados en umbrales de seguridad.
- **Interacciones (Inbound/Outbound):** Recibe datos de los dispositivos y configuraciónes del contexto de *Space Management*, mientras envía eventos críticos al contexto de *Alerting & Response* para la mitigación de riesgos.
- **Eventos de Dominio:** Los eventos clave incluyen `Air Quality Measured`, `Safety Threshold Exceeded` y `Sensor Connection Lost`, los cuales disparan la lógica de automatización del sistema.

<img src="../assets/context-canvases/cc-iam.jpg" alt="cc-iam" width="800">

**Billing**

Este canvas gestiona el flujo financiero y el modelo de monetización de la plataforma, asegurando la sostenibilidad del servicio.

- **Propósito:** Administrar el ciclo de vida de los pagos, planes de suscripción y la facturación de los servicios premium de Clair.
- **Capacidades:** Procesamiento de pagos (Checkout), gestión de niveles de suscripción (Freemium/Paid) y emisión de comprobantes fiscales electrónicos.
- **Interacciones clave:** Informa al contexto de *Identity & Access Management* sobre el estado de pago del usuario para habilitar o restringir el acceso a funciónalidades avanzadas.
- **Eventos de Dominio:** Los hitos críticos incluyen `Payment Processed`, `Subscription Tier Upgraded` e `Invoice Issued`, los cuales garantizan la transparencia financiera y la continuidad del servicio para los clientes.

<img src="../assets/context-canvases/cc-billing.jpg" alt="cc-billing" width="800">

**Device \& Space Management**

Este canvas define la estructura organizativa de la solución, encargándose de la gestión del hardware y la jerarquización de los entornos físicos monitoreados.

- **Propósito:** Administrar el inventario de dispositivos y la configuración de los espacios (establecimientos y zonas) para contextualizar los datos ambientales.
- **Capacidades:** Incluye el registro de dispositivos (**Device Onboarding**), la gestión de estados del sensor y la creación de una jerarquía de espacios que permite asignar sensores a áreas específicas (ej. "Área de Cocina" o "Sala de Espera").
- **Interacciones Clave:** Actúa como proveedor de estructura para el contexto de *Air Quality Monitoring* y recibe directrices de permisos desde el contexto de *Identity & Access Management*.
- **Eventos de Dominio:** Los hitos fundamentales son `Device Registered`, `Space Configured` y `Device Status Updated`, los cuales aseguran que cada lectura de aire esté correctamente vinculada a un punto geográfico y a un responsable administrativo.

<img src="../assets/context-canvases/cc-device.jpg" alt="cc-device-space" width="800">

**Air Quality Evaluation**

Este canvas representa el motor de inteligencia del sistema, encargado de procesar la telemetría bruta para determinar el estado de salubridad del entorno.

- **Propósito:** Analizar y validar los datos provenientes de los sensores para identificar desviaciones en la calidad del aire respecto a los estándares de salud.
- **Capacidades:** Incluye la ingesta de telemetría, la validación de la integridad de los datos y el motor de evaluación que compara las lecturas con los umbrales de $CO_2$ y material particulado (PM2.5).
- **Interacciones Clave:** Recibe el flujo de datos constante de los dispositivos y, al detectar niveles críticos, notifica al contexto de *Alerting & Response* para iniciar acciones de mitigación.
- **Eventos de Dominio:** Los hitos clave son `Telemetry Validated`, `Air Quality Evaluated` y `Health Threshold Breached`, los cuales activan la lógica reactiva y preventiva de la plataforma.

<img src="../assets/context-canvases/cc-quality.jpg" alt="cc-aq" width="800">

**Alerting \& Response**

Este canvas define la capacidad reactiva y de mitigación del sistema, transformando los eventos de riesgo en acciones correctivas inmediatas.

- **Propósito:** Orquestar la comunicación de alertas críticas y ejecutar de forma autónoma las acciones necesarias para restaurar la calidad del aire.
- **Capacidades:** Gestión de notificaciones automáticas (push/email) y control de actuadores inteligentes, permitiendo la activación de sistemas de ventilación o purificación sin intervención manual.
- **Interacciones Clave:** Depende de los eventos de "umbral excedido" provenientes de *Air Quality Evaluation* y consulta los canales de comunicación preferidos del usuario en el contexto de *Identity & Access Management*.
- **Eventos de Dominio:** Los hitos fundamentales incluyen `Alert Triggered`, `Corrective Action Initiated` y `Notification Delivered`, garantizando una respuesta inmediata ante cualquier anomalía ambiental detectada.

<img src="../assets/context-canvases/cc-alerting.jpg" alt="cc-alerting" width="800">

**Analytics \& Reporting**

Este canvas se enfoca en la síntesis y transformación de datos históricos para facilitar la toma de decisiones basada en evidencia.

- **Propósito:** Proporcionar una visión retrospectiva y estratégica de la calidad del aire mediante el análisis de tendencias y la generación de informes detallados.
- **Capacidades:** Incluye la visualización de datos históricos, la generación de reportes semanales de salud y la creación de resúmenes analíticos que permiten identificar patrones de contaminación recurrentes.
- **Interacciones Clave:** Consume la telemetría validada del contexto de *Air Quality Evaluation* y utiliza la estructura de zonas definida en *Device & Space Management* para organizar la información.
- **Eventos de Dominio:** Los hitos principales incluyen `Historical Data Summarized`, `Weekly Insight Generated` y `Report Exported`, permitiendo a los usuarios evaluar la efectividad de sus medidas de ventilación a lo largo del tiempo.

<img src="../assets/context-canvases/cc-analytics.jpg" alt="cc-analytics" width="800">

**Notifications**

Este canvas define la capacidad reactiva del sistema, encargándose de transformar los eventos críticos en acciones de mitigación tangibles.

- **Propósito:** Gestionar la comunicación de alertas a los usuarios y coordinar la respuesta automática de los actuadores ante riesgos ambientales.
- **Capacidades:** Orquestación de notificaciones (push/email) y ejecución de comandos hacia hardware inteligente (extractores, purificadores y ventanas).
- **Interacciones clave:** Depende de los eventos de "umbral excedido" provenientes de *Air Quality Monitoring* y consulta las preferencias de contacto del contexto de *Identity & Access Management*.
- **Eventos de Dominio:** Los hitos principales son `Notification Sent`, `Corrective Action Executed` y `Action Outcome Logged`, asegurando la trazabilidad de cada intervención del sistema.

<img src="../assets/context-canvases/cc-notifications.jpg" alt="cc-notifications" width="800">

**Embedded App**

Este canvas define la lógica del software que reside directamente en el hardware, actuando como el puente físico entre el entorno y la nube de Clair.

- **Propósito:** Gestionar la operación local del sensor, garantizando la captura precisa de datos y la comunicación estable con el ecosistema digital.
- **Capacidades:** Controla la lectura de los sensores de $CO_2$ y PM2.5, la gestión de la conectividad Wi-Fi, el almacenamiento local (*Offline Logging*) durante fallos de red y la señalización visual mediante indicadores LED.
- **Interacciones Clave:** Envía el flujo de telemetría bruta al contexto de *Air Quality Evaluation* y recibe señales de configuración o comandos de actualización desde la plataforma central.
- **Eventos de Dominio:** Los hitos críticos incluyen `Physical Reading Captured`, `Connectivity Status Changed` y `Local Buffer Synced`, los cuales aseguran que ninguna medición se pierda a pesar de las fluctuaciones en la infraestructura de red.

<img src="../assets/context-canvases/cc-embedded.jpg" alt="cc-embedded" width="800">

**Edge Station**

Este canvas describe el componente de infraestructura local que actúa como concentrador y gestor de datos en el sitio donde se encuentran los sensores.

- **Propósito:** Optimizar el flujo de información entre los dispositivos periféricos y la nube, garantizando la resiliencia operativa y el procesamiento ligero en el borde (*Edge Computing*).
- **Capacidades:** Gestión de la red local de sensores, orquestación de la transmisión de datos hacia la plataforma central y mantenimiento de la persistencia temporal de lecturas ante cortes de energía o internet.
- **Interacciones Clave:** Se comunica directamente con la **Embedded App** de los sensores para recolectar telemetría y sirve como enlace para el contexto de **Air Quality Evaluation** en la nube.
- **Eventos de Dominio:** Los hitos principales incluyen `Gateway Connection Established`, `Data Batch Forwarded` y `Node Status Heartbeat`, asegurando que la infraestructura física del establecimiento se mantenga estable y supervisada.

<img src="../assets/context-canvases/cc-edge.jpg" alt="cc-edge" width="800">

El tablero completo del Bounded Context Canvases. puede visualizarse en el siguiente enlace: https://bit.ly/3QwYkAS

### 4.1.2. Context Mapping.

El **Context Mapping** (Mapa de Contextos) es una herramienta estratégica de Domain-Driven Design (DDD) que define visual y conceptualmente cómo interactúan los diferentes *Bounded Contexts* (Contextos Acotados) de la solución Clair. Nos permite identificar los límites de responsabilidades, el tipo de relación técnica y organizativa entre los equipos, y cómo fluye la información a través del sistema.

Para la elaboración de nuestros mapas de contextos, el equipo realizó sesiones de debate técnico analizando la información de los Bounded Contexts y el EventStorming. Durante este proceso, evaluamos el diseño técnico respondiendo a preguntas estratégicas para analizar alternativas de acoplamiento y cohesión:
*   **¿Qué pasaría si aislamos las capacidades principales (core capabilities) y movemos las otras a un contexto aparte?** Evaluamos separar el motor de evaluación de calidad del aire (`Evaluation`) del procesamiento de alertas físicas (`Alerting`). Decidimos mantenerlos separados para que el motor de evaluación sea puramente analítico y el de alertas sea reactivo/operativo, evitando sobrecargar un solo módulo.
*   **¿Qué pasaría si creamos un servicio compartido (Shared Service) o Shared Kernel para reducir la duplicación?** Consideramos duplicar las entidades de usuario en cada subsistema para darles total independencia. Sin embargo, para no ensuciar la base de datos con información redundante de perfiles y sesiones, decidimos implementar un `Shared Kernel` y un módulo `IAM` como proveedor Upstream general. Esto centraliza la autenticación pero usa Capas Anticorrupción (ACL) en los consumidores para mitigar el acoplamiento.
*   **¿Qué pasaría si movemos la capacidad de notificaciones dentro de Alerting?** Analizamos fusionar `Notifications` con `Alerting`. No obstante, determinamos que `Notifications` debe ser un contexto genérico que pueda servir a otros módulos en el futuro (como facturación o marketing), por lo que lo mantuvimos independiente y consumiendo eventos de alerta a través de un canal intermedio.

**Discusión de alternativas:** Evaluamos una alternativa monolítica donde todos los contextos compartían la misma base de datos sin ACLs (patrón Shared Database), lo cual agilizaba el desarrollo inicial pero creaba un fuerte acoplamiento. Al final, optamos por la aproximación actual basada en Upstream/Downstream con ACLs y Shared Kernels delimitados por plataforma (Web, Mobile, Edge). Esta aproximación garantiza la máxima independencia de despliegue para cada producto de la solución Clair y protege la integridad de los modelos de dominio individuales.

Para entender las relaciones descritas en los diagramas, se utilizan los siguientes patrones estándar:
*   **Upstream (U) / Downstream (D):** Define la dirección de la dependencia. El contexto *Upstream* (U) es el proveedor y el *Downstream* (D) es el cliente. Si el Upstream cambia, el Downstream se ve afectado.
*   **ACL (Anti-Corruption Layer / Capa Anticorrupción):** Una capa de traducción implementada por el Downstream para evitar que el modelo de datos del Upstream contamine o ensucie su propio modelo de dominio.
*   **Shared Kernel (SK) / Núcleo Compartido:** Un conjunto de código, bases de datos o librerías que dos o más contextos comparten de mutuo acuerdo. Cualquier cambio en el Shared Kernel requiere la coordinación de ambos equipos.

A continuación se detallan las relaciones y el flujo de diseño para cada producto de la solución:

#### 4.1.2.1. Context Mapping - Web services (Backend).

El backend es el motor central de la solución Clair, donde se orquestan los procesos de negocio más complejos.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/context-mapping/backend/backend-context-mapping/context-mapping.svg" alt="Context Mapping - Web Services" width="800">
</p>

**Análisis Detallado de Relaciones:**

1.  **El rol de Device como Proveedor Central (Upstream -> Downstream con ACL):**
    *   `Device` provee información a `Alerting`, `Analytics`, `Evaluation` y `Notifications`.
    *   **¿Por qué con ACL?** Cada uno de estos contextos de negocio consume datos del sensor, pero tiene su propio modelo conceptual (por ejemplo, `Evaluation` se enfoca en umbrales de salud, mientras que `Analytics` se enfoca en series de tiempo históricas). Las ACL aseguran que un cambio en la estructura interna de los dispositivos no rompa estos módulos individuales.
2.  **Gestión de Suscripciones y Facturación (Billing):**
    *   `Billing` es *Upstream* de `Device` y `Analytics`. Esto controla qué dispositivos se pueden activar o qué cantidad de reportes históricos se pueden generar según el plan del usuario (gratuito o de pago).
3.  **Seguridad y Acceso (IAM):**
    *   `IAM` provee datos de identidad a `Billing` (para asociar pagos a usuarios) y a `Notifications` (para obtener correos y tokens de notificación).
4.  **Shared Kernel (SK):**
    *   Todos los contextos del backend (`IAM`, `Device`, `Alerting`, `Analytics`, `Billing`, `Evaluation`, `Notifications`) comparten un `Shared Kernel` que contiene las clases base del dominio, eventos de integración comunes y utilidades de infraestructura transversal.

#### 4.1.2.2. Context Mapping - Web application (Frontend).

Representa la aplicación web desarrollada en Angular, encargada de la visualización y administración para los usuarios administradores del sistema (Facility Admins).

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/context-mapping/frontend/frontend-context-mapping/context-mapping.svg" alt="Context Mapping - Web Application" width="800">
</p>

**Análisis Detallado de Relaciones:**

1.  **Módulos de Negocio en la Interfaz (Upstream -> Downstream con ACL):**
    *   `Device` expone sus datos a `Alerting` y `Analytics` a nivel de UI a través de servicios de frontend dedicados con traductores propios (ACL) para estructurar componentes visuales independientes.
    *   `Evaluation` alimenta visualmente a `Analytics` (por ejemplo, mostrando gráficas de alertas cruzadas con el estado del aire).
2.  **IAM como Eje Transversal en el Cliente:**
    *   `IAM` es *Upstream* directo de `Analytics`, `Billing` y el `Shared Kernel` del frontend. La sesión activa del usuario y sus permisos de rol (Guardas de Angular) determinan qué partes de la interfaz y qué componentes compartidos se renderizan.
3.  **Shared Kernel en Frontend:**
    *   `Alerting`, `Analytics`, `Device` e `IAM` interactúan con el `Shared Kernel` (que aloja layouts comunes, componentes visuales reutilizables como botones y selectores, y configuraciones de interceptores HTTP).

#### 4.1.2.3. Context Mapping - Mobile application.

Corresponde a la aplicación móvil desarrollada en Flutter, diseñada para el usuario final (Home User) para consultar la calidad del aire en tiempo real y recibir alertas inmediatas.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/context-mapping/mobile/mobile-context-mapping/context-mapping.svg" alt="Context Mapping - Mobile Application" width="800">
</p>

**Análisis Detallado de Relaciones:**

1.  **Dependencias en Dispositivos Móviles (Upstream -> Downstream con ACL):**
    *   `Alerts` y `Analytics` actúan como *Upstream* de `Devices` con ACL. En la aplicación móvil, los listados de dispositivos se enriquecen dinámicamente con alertas y resúmenes analíticos rápidos.
    *   `Devices` provee información directamente al módulo de `Evaluation` para mostrar estados del aire en tiempo real usando ACL para mapear los colores de advertencia específicos del UI.
2.  **Infraestructura Base Compartida (Core Infrastructure y Shared Kernel):**
    *   Existe un contexto de **Core Infrastructure** que funciona como el Shared Kernel a bajo nivel técnico para todos los módulos (IAM, Devices, Alerts, Analytics, Evaluation, Notifications y Shared). Contiene el cliente HTTP de Flutter, base de datos local (SQLite/Hive) y configuraciones del dispositivo móvil.
    *   El **Shared Kernel (Shared)** provee componentes visuales nativos de Flutter (Widgets, loaders, diálogos) comunes para la mayoría de los módulos.

#### 4.1.2.4. Context Mapping - Edge services.

Corresponde a la estación Edge de Clair desarrollada en Flask/Python, encargada del procesamiento intermedio en local, controlando los sensores físicos y actuadores antes de enviar la información a la nube.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/context-mapping/edge/edge-context-mapping/context-mapping.svg" alt="Context Mapping - Edge Services" width="800">
</p>

**Análisis Detallado de Relaciones:**

1.  **IAM local como Consumidor de Seguridad (Upstream -> Downstream con ACL):**
    *   En este entorno offline o de borde, los contextos de `Device` (el hardware del hub), `Alerting` (las reglas de activación del relé físico) y `Provisioning` (la vinculación del hardware al Edge) actúan como *Upstream* de `IAM`.
    *   **¿Por qué esta dirección?** El IAM local necesita validar y autenticar las peticiones internas de estos componentes de hardware para garantizar que ningún dispositivo no autorizado tome el control del Edge o de los actuadores (ventanas, extractores). Se utiliza ACL para aislar las librerías criptográficas de seguridad del negocio del hardware.
2.  **Shared Kernel en Edge:**
    *   `IAM`, `Device`, `Alerting` y `Provisioning` comparten un `Shared Kernel` ligero que incluye los modelos de comunicación de sockets, serialización JSON nativa y middlewares de logging del sistema operativo local.

### 4.1.3. Software Architecture.


#### 4.1.3.1. Software Architecture System Landscape Diagram.

El diagrama de **System Landscape** (Panorama del Sistema) proporciona una vista de alto nivel de todo el ecosistema de software de Vanana. A diferencia de un diagrama de contexto tradicional enfocado en un solo sistema, este diagrama representa un mapa global donde todos los sistemas de software (internos y externos) y los usuarios se muestran como pares (*peers*) dentro del entorno organizacional.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/c4/landscape/VananaSystemLandscape-dark.svg" alt="Vanana System Landscape Diagram" width="850">
</p>

**Descripción Detallada del Ecosistema:**

1.  **Usuarios y Actores del Sistema:**
    *   **Facility Admin (Administrador de Instalaciones):** Es el operador responsable de gestionar múltiples espacios y monitorear los sensores de calidad del aire en establecimientos comerciales. Interactúa directamente con la plataforma Vanana, autenticándose a través de redes sociales (Google) y administrando sus planes de pago en Stripe.
    *   **Home User (Usuario del Hogar):** Es el cliente residencial que monitorea la calidad del aire de su hogar. Al igual que el administrador, hace uso del login social (Google) y gestiona su suscripción premium en Stripe.

2.  **Sistemas Internos de Vanana:**
    *   **Vanana Platform:** Es el núcleo tecnológico centralizado que recibe, procesa y expone la información de telemetría, administrando los flujos de automatización de actuadores en base a los umbrales de contaminación.
    *   **Clair Hardware:** Comprende el conjunto físico de sensores IOT (capturadores de telemetría de $CO_2$, material particulado PM2.5 y temperatura) y actuadores (ventanas inteligentes, extractores) instalados en los espacios de los usuarios.

3.  **Sistemas Externos Integrados (Pares de Servicios):**
    *   **Google OAuth2:** Servicio externo utilizado por la plataforma para proveer autenticación federada, segura y ágil mediante OpenID Connect.
    *   **Stripe:** Pasarela externa encargada del procesamiento financiero de suscripciones y facturas electrónicas de los clientes.
    *   **Resend:** Plataforma externa de entrega de correos electrónicos transaccionales (como reportes semanales e informes de salud).
    *   **OneSignal:** Proveedor externo que gestiona el envío de notificaciones push a los dispositivos móviles de los usuarios en tiempo real ante alertas críticas de calidad del aire.

Este diagrama demuestra que la plataforma de Vanana no opera de forma aislada, sino que colabora dinámicamente con una suite de servicios especializados para ofrecer resiliencia, escalabilidad y una experiencia de usuario integral.

#### 4.1.3.2. Software Architecture Context Level Diagrams.

El diagrama de contexto de sistema (System Context Diagram) representa el nivel de abstracción más alto de la arquitectura C4 para la plataforma **Vanana**. Este modelo delimita las fronteras del sistema de software principal, identificando sus interacciones directas con los actores y con los sistemas externos integrados en el ecosistema.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/c4/context/VananaContext-dark.svg" alt="Vanana System Context Diagram" width="850">
</p>

Las interacciones clave representadas en el diagrama de contexto son las siguientes:

*   **Actores del Sistema:**
    *   **Home User y Facility Admin:** Interactúan directamente con la plataforma para la monitorización ambiental de sus respectivos entornos (hogares y locales comerciales). Ambos perfiles delegan la autenticación de sus credenciales al sistema externo de **Google** y la gestión de planes y transacciones monetarias al servicio de **Stripe**.
*   **Dispositivos de Hardware (Clair Hardware):**
    *   Los sensores y actuadores físicos establecen una comunicación bidireccional con la plataforma central, transmitiendo datos de telemetría de calidad del aire (CO2, material particulado y temperatura) y ejecutando comandos automáticos de ventilación en respuesta a las evaluaciones ambientales.
*   **Servicios Externos de Soporte:**
    *   **Google OAuth2:** Provee el servicio de autenticación federada y validación de identidad.
    *   **Stripe:** Administra los flujos de cobro, procesamiento de pagos y el ciclo de vida de las suscripciones.
    *   **OneSignal:** Recibe peticiones de la plataforma para despachar notificaciones push a los dispositivos móviles de los usuarios.
    *   **Resend:** Gestiona el envío de correos electrónicos transaccionales con alertas críticas y reportes de analítica periódica.


#### 4.1.3.3. Software Architecture Container Level Diagrams.

El **Container Diagram** (Diagrama de Contenedores) representa el Nivel 2 del modelo C4. Este diagrama detalla la composición interna de **Vanana Platform**, ilustrando cómo se distribuyen las responsabilidades del sistema entre los diferentes componentes ejecutables (aplicaciones web, móviles, bases de datos, brokers de mensajería y firmware embebido), especificando las tecnologías seleccionadas y los protocolos de comunicación utilizados.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/c4/containers/VananaContainers-dark.svg" alt="Vanana Containers Diagram" width="850">
</p>

**Descripción de Contenedores y Decisiones Tecnológicas:**

*   **Aplicaciones Cliente (Frontend):**
    *   **Landing Page (HTML / CSS / JavaScript):** Sitio web estático público que presenta la propuesta de valor de la plataforma.
    *   **Single Page Application (SPA - Angular):** Aplicación web autenticada que permite a los administradores de instalaciones (Facility Admins) configurar espacios físicos, definir umbrales de alerta y visualizar paneles analíticos de calidad de aire en tiempo real.
    *   **Mobile App (Flutter):** Aplicación móvil multiplataforma orientada al usuario del hogar (Home User) para el monitoreo ágil y la recepción de notificaciones de alerta inmediata.
*   **Capa de Servicios de Backend:**
    *   **API Gateway (Spring Cloud Gateway / Java):** Punto único de entrada al backend encargado de la seguridad perimetral, balanceo de carga y enrutamiento de peticiones.
    *   **Platform API (Spring Boot / Java 25):** Núcleo de servicios empresariales que implementa las reglas de negocio críticas, incluyendo IAM, gestión de locales, e ingesta y evaluación de telemetría.
*   **Capa de Mensajería y Desacoplamiento:**
    *   **Kafka Message Broker (Apache Kafka):** Broker de mensajería asíncrono que desacopla la ingesta masiva de datos en el Edge del procesamiento interno de la plataforma, garantizando tolerancia a fallos y alta escalabilidad.
*   **Bases de Datos de la Plataforma:**
    *   **Platform PostgreSQL Database:** Almacenamiento relacional principal para entidades transaccionales (instalaciones, dispositivos asociados, históricos y preferencias).
    *   **Platform Redis Database:** Almacenamiento clave-valor en memoria utilizado para la gestión rápida de sesiones activas, tokens de seguridad temporales y control de tasas de peticiones (rate limiting).
*   **Capa IoT (Edge y Dispositivos Embebidos):**
    *   **Clair Embedded Application (Firmware Embebido):** Corre directamente sobre el microcontrolador físico del sensor. Mide los niveles ambientales y transmite los payloads localmente.
    *   **Clair Edge Station Application (Flask / Python):** Estación local que actúa como pasarela (Gateway local) para coordinar múltiples sensores Clair. Almacena temporalmente los datos en una **Edge SQLite Database** para garantizar la continuidad operativa ante pérdidas de conexión a Internet (sincronización offline).

**Protocolos y Mecanismos de Comunicación:**

*   **REST/HTTPS (JSON):** Utilizado para la comunicación síncrona entre las aplicaciones de cliente (Angular, Flutter, Edge Station) y el backend a través del API Gateway.
*   **Kafka Wire Protocol (TCP):** Utilizado para el envío asíncrono de lotes de telemetría desde la estación Edge hacia el broker de mensajería en la nube.
*   **JDBC/SQL:** Conexión nativa de base de datos para la persistencia transaccional entre Spring Boot y PostgreSQL.
*   **Redis Protocol (RESP):** Utilizado para operaciones de caché de baja latencia.

#### 4.1.3.4. Software Architecture Deployment Diagrams.

El **Deployment Diagram** (Diagrama de Despliegue) ilustra la distribución de las instancias de software y bases de datos sobre la infraestructura física y virtual correspondiente al entorno de **Desarrollo (Development)**. Este modelo permite identificar la topología de red, los entornos de ejecución y los límites de la infraestructura del sistema.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/c4/deploy/Development-dark.svg" alt="Vanana Development Deployment Diagram" width="850">
</p>

**Descripción de Nodos de Despliegue e Infraestructura:**

*   **Vanana Cloud (Entorno Linux / Docker):**
    Representa la nube privada de desarrollo montada sobre servidores Linux ejecutando contenedores Docker para aislar y escalar los servicios:
    *   **Backend Container:** Aloja la máquina virtual de Java (JVM Eclipse Temurin - JDK 25) ejecutando la instancia de la aplicación `Platform API`. Dentro de este nodo también se despliegan de forma independiente los contenedores del `API Gateway` y del broker de mensajería asíncrona `Kafka Message Broker`.
    *   **Database Server Container:** Contenedor Docker dedicado al motor de base de datos relacional `PostgreSQL 16` que corre la instancia de base de datos `PostgreSQL Database`.
    *   **Redis Container:** Contenedor Docker dedicado al motor en memoria `Redis` para la caché activa.
*   **Vercel (Static Website Hosting):**
    Servicio PaaS externo en la nube que aloja de manera redundante las aplicaciones de cliente frontend:
    *   **Landing Page Container:** Aloja el servidor web estático para la Landing Page pública.
    *   **Web App Container:** Aloja el empaquetado Angular que sirve la `Single Page Application (SPA)`.
*   **Mobile Device (Android / iOS):**
    Representa los dispositivos físicos móviles de los usuarios que ejecutan el contenedor cliente de la `Mobile App` en Flutter.
*   **Edge Station (Physical Hardware):**
    Representa la estación o puerta de enlace local física (por ejemplo, una Raspberry Pi) configurada en los establecimientos para coordinar los sensores y correr localmente la aplicación de Python/Flask.
*   **Embedded Device (Physical Hardware):**
    Representa el hardware del microcontrolador físico Clair que corre el firmware compilado en C++ (`Embedded App`).
*   **External Services (Servicios SaaS de terceros):**
    Nodo lógico externo que agrupa los servicios en la nube de terceros: `Google OAuth2` para identidades, `Stripe` para pagos, `OneSignal` para mensajería push, y `Resend` para entrega de correos electrónicos.

**Flujos y Protocolos de Comunicación en el Despliegue:**

*   **REST/HTTPS (JSON):** Utilizado entre los navegadores de clientes, dispositivos móviles y el API Gateway en la nube.
*   **OneSignal SDK:** Utilizado para coordinar las llamadas de notificaciones móviles directamente desde la plataforma y las aplicaciones móviles.
*   **Kafka Wire Protocol (TCP):** Utilizado para el envío asíncrono y bidireccional de streams de telemetría y comandos entre la estación Edge física y el contenedor de Kafka en la nube.
*   **GPIO/I2C:** Interfaz física de bajo nivel utilizada por el microcontrolador embebido para recopilar lecturas directas del hardware del sensor de aire.

## 4.2. Tactical-Level Domain-Driven Design - Web Services

En esta sección se detalla el diseño táctico basado en Domain-Driven Design (DDD) para el contenedor central de servicios web de la plataforma Vanana (Platform API). El backend se construye sobre una arquitectura modular estructurada por Bounded Contexts independientes, lo que permite que cada área de negocio mantenga su consistencia y evolucione sin afectar directamente a los demás componentes del sistema.

**Arquitectura de Componentes de la API del Backend (Platform API)**

El contenedor **Platform API** (desarrollado en Spring Boot y Java 25) agrupa de forma modular los contextos acotados de IAM, Billing, Device & Space Management, Air Quality Evaluation, Alerting & Response, Analytics y Notifications. El siguiente diagrama de componentes a nivel de contenedor muestra la descomposición general de la API, detallando cómo interactúan estos bloques estructurales principales y cómo se delegan las responsabilidades:

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/c4/containers/backend/components/PlatformApiComponents-dark.svg" alt="Platform API General Component Diagram" width="850">
</p>

A nivel de diseño táctico, cada uno de los contextos acotados dentro del backend sigue una arquitectura limpia (Clean Architecture) dividida en cuatro capas bien definidas:
1.  **Interfaces/Presentation Layer:** Compuesto por controladores REST que exponen los endpoints públicos y adaptadores de entrada encargados de recibir peticiones externas y serializarlas.
2.  **Application Layer:** Contiene los servicios de aplicación, casos de uso del sistema, y la lógica de enrutamiento y orquestación de comandos y consultas (*Commands/Queries*).
3.  **Domain Layer:** Representa el núcleo del sistema, libre de dependencias tecnológicas. Contiene las entidades base, agregados (*Aggregates*), objetos de valor (*Value Objects*), servicios de dominio e interfaces de repositorios (puertos).
4.  **Infrastructure Layer:** Implementa los adaptadores de salida necesarios para la persistencia de datos (conectando a PostgreSQL o Redis), la comunicación externa con APIs de terceros (Stripe, Google, Resend) y el encolamiento de eventos de integración en Kafka.

La comunicación interna entre contextos acotados dentro de la misma API se realiza de manera desacoplada a través de fachadas lógicas (*Facades*), o mediante la publicación y consumo asíncrono de eventos de integración a través del bus de datos de Apache Kafka, evitando el acoplamiento directo de base de datos.

### 4.2.1. Bounded Context: Identity & Access (IAM)

El contexto acotado de **Identity & Access Management (IAM)** gestiona el registro de nuevos usuarios, la autenticación segura, el control de acceso basado en roles y el inicio de sesión federado (Google OAuth2). Asegura que los recursos de la plataforma Vanana estén protegidos y que solo los usuarios autorizados puedan interactuar con los sensores y actuadores.

**Diccionario de Clases del Contexto IAM**

A continuación, se detallan las clases principales identificadas para este contexto, clasificadas por capa de arquitectura:

| Nombre de la Clase | Capa | Propósito / Responsabilidad | Atributos Principales | Métodos Clave | Relaciones de Asociación / Dependencia |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **User** | Dominio | Representa la entidad de usuario en la plataforma. Actúa como raíz de agregado (*Aggregate Root*). | `id` (UUID), `email` (EmailAddress), `password` (Password), `status` (UserStatus), `googleUserId` (GoogleUserId) | `confirm()`, `linkGoogleAccount(googleUserId)` | Contiene `EmailAddress` y `Password`. |
| **TokenSession** | Dominio | Representa una sesión activa de JWT emitida para un usuario específico. | `jti` (TokenJti), `userId` (UserId), `refreshToken` (String), `tokenType` (TokenType), `expiresAt` (Instant) | `invalidate()` | Contiene `UserId`. |
| **RegistrationSession** | Dominio | Entidad temporal que mantiene el estado de registro de un usuario pendiente de confirmación. | `id` (RegistrationSessionId), `email` (EmailAddress), `password` (Password), `verificationCode` (VerificationCode), `expiresAt` (Instant) | *N/A* | Contiene `EmailAddress`, `Password` y `VerificationCode`. |
| **EmailAddress** | Dominio | Objeto de Valor (*Value Object*) que encapsula la lógica de validación del correo electrónico. | `value` (String) | *N/A* | Composición en `User` y `RegistrationSession`. |
| **Password** | Dominio | Objeto de Valor que maneja el hash encriptado de la contraseña. | `encryptedValue` (String) | *N/A* | Composición en `User` y `RegistrationSession`. |
| **VerificationCode** | Dominio | Objeto de Valor que representa el código de 6 dígitos enviado por email. | `value` (String) | *N/A* | Composición en `RegistrationSession`. |
| **UserRepository** | Dominio | Interfaz (Puerto) que define los métodos de persistencia del Agregado `User`. | *N/A* | `save()`, `findById()`, `findByEmail()`, `findByGoogleUserId()` | Utilizado por `UserCommandServiceImpl` e `UserQueryServiceImpl`. |
| **TokenSessionRepository** | Dominio | Interfaz (Puerto) para gestionar el ciclo de vida de persistencia rápida de `TokenSession`. | *N/A* | `save()`, `findByJti()`, `deleteByJti()` | Utilizado por `TokenCommandServiceImpl` y `TokenQueryServiceImpl`. |
| **GoogleTokenVerifier** | Dominio | Interfaz (Servicio de Dominio) para verificar tokens de identidad emitidos por Google. | *N/A* | `verify(idToken)` | Utilizado por `GoogleAuthenticationCommandServiceImpl`. |
| **AuthenticationController** | Interfaz | Controlador REST de entrada para flujos de autenticación local. | `userCommandService`, `tokenCommandService` | `signUp()`, `confirmSignUp()`, `signIn()`, `refreshToken()`, `signOut()` | Depende de `UserCommandServiceImpl` y `TokenCommandServiceImpl`. |
| **GoogleOAuthController** | Interfaz | Controlador REST para manejar la redirección y el callback de Google OAuth2. | `googleOAuthStateManager`, `googleOAuthCallbackApplicationService` | `redirectToGoogle()`, `handleCallback()` | Depende de `GoogleOAuthCallbackApplicationService`. |
| **UserCommandServiceImpl** | Aplicación | Servicio de aplicación que orquesta el registro inicial y la confirmación mediante código. | `userRepository`, `registrationSessionRepository`, `asyncNotificationService` | `handle(InitiateRegistrationCommand)`, `handle(ConfirmRegistrationCommand)` | Usa `UserRepository`, `RegistrationSessionRepository` y `AsyncNotificationService`. |
| **TokenCommandServiceImpl** | Aplicación | Servicio de aplicación para la creación, rotación e invalidación de tokens JWT. | `tokenSessionRepository`, `userRepository`, `jwtTokenEncoder` | `handle(CreateTokenSessionCommand)`, `handle(RotateRefreshTokenCommand)`, `handle(InvalidateTokenSessionCommand)` | Usa `TokenSessionRepository`, `UserRepository` y `JwtTokenEncoder`. |
| **JpaUserRepository** | Infraestructura | Adaptador concreto de persistencia relacional que interactúa con PostgreSQL mediante JPA. | *N/A* | `findByEmail()`, `existsByEmail()` | Implementa `UserRepository`. |
| **RedisTokenSessionRepository** | Infraestructura | Adaptador concreto para almacenar y verificar sesiones de tokens de forma rápida en caché Redis. | `redisTemplate`, `objectMapper` | `save()`, `findByJti()`, `deleteByJti()`, `revokeAllTokensForUser()` | Implementa `TokenSessionRepository`. |

#### 4.2.1.1. Domain Layer

La capa de dominio de IAM contiene las reglas fundamentales de negocio independientes de cualquier infraestructura. Define las entidades críticas del ciclo de vida de usuario y las abstracciones de persistencia (puertos).

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/iam-bc/domain-layer.svg" alt="IAM Domain Layer Class Diagram" width="750">
</p>

*   **Entities y Aggregates:** `User` actúa como la raíz de agregado que mantiene la identidad de la persona y sus vinculaciones externas (como Google). `TokenSession` es la entidad que administra la sesión del usuario a nivel de tokens JWT, permitiendo su revocación inmediata (`invalidate()`). `RegistrationSession` resguarda de manera temporal la contraseña encriptada y el código de verificación del flujo de registro.
*   **Value Objects:** `EmailAddress`, `Password` y `VerificationCode` encapsulan las restricciones estructurales y aseguran la validez y encapsulamiento de los datos del dominio desde el momento de su instanciación.
*   **Ports (Interfaces):** `UserRepository`, `TokenSessionRepository` y `RegistrationSessionRepository` definen las operaciones lógicas de almacenamiento sin depender de tecnologías específicas como JPA o Redis.

#### 4.2.1.2. Interface Layer

La capa de interfaz expone las API REST del contexto acotado, traduciendo las peticiones JSON HTTP externas en comandos de aplicación fuertemente tipados.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/iam-bc/interfaces-layer.svg" alt="IAM Interface Layer Class Diagram" width="750">
</p>

*   **AuthenticationController:** Expone endpoints HTTP estándar para el registro local (`signUp`), confirmación vía código por correo (`confirmSignUp`), inicio de sesión (`signIn`), renovación de tokens (`refreshToken`) y cierre de sesión (`signOut`).
*   **GoogleOAuthController:** Administra el flujo federado de OpenID Connect. Redirecciona al usuario al servidor de autorización de Google y recibe el código de autorización en el endpoint de callback para autenticar la sesión.
*   **UserController:** Controlador simple que recupera los datos del perfil del usuario autenticado en base a la sesión de seguridad actual.

#### 4.2.1.3. Application Layer

Esta capa actúa como el orquestador principal del contexto acotado. Implementa los casos de uso definidos del sistema, interactuando con las interfaces de dominio y coordinando el flujo de las transacciones sin contener lógica de negocio directa.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/iam-bc/application-layer.svg" alt="IAM Application Layer Class Diagram" width="750">
</p>

*   **Command Handlers:** `UserCommandServiceImpl` implementa la lógica para iniciar el registro enviando un código de confirmación asíncrono (`InitiateRegistrationCommand`) y para validar el código y persistir definitivamente al usuario en el sistema (`ConfirmRegistrationCommand`).
*   **TokenCommandServiceImpl:** Orquesta las transacciones relacionadas con la sesión de tokens, controlando la persistencia de las firmas de tokens de refresco y su rotación segura para mitigar ataques de replay.
*   **GoogleOAuthCallbackApplicationService:** Orquesta el flujo de inicio de sesión social. Convierte el código de Google en un perfil de usuario verificado y delega la creación de tokens en el servicio de tokens de la aplicación.
*   **AsyncNotificationService (Port):** Interfaz que permite al servicio de aplicación delegar el envío de correos electrónicos a un sistema de mensajería asíncrono o un proveedor de correo externo sin acoplarse directamente a este.

#### 4.2.1.4. Infrastructure Layer

La capa de infraestructura implementa las interfaces de dominio (puertos) y provee los adaptadores concretos para interactuar con bases de datos relacionales, almacenamiento en memoria cache Redis, servicios OAuth2 y generadores de tokens criptográficos.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/iam-bc/infrastructure-layer.svg" alt="IAM Infrastructure Layer Class Diagram" width="750">
</p>

*   **Adaptadores de Persistencia:** `JpaUserRepository` utiliza Spring Data JPA y Hibernate para persistir usuarios en la base de datos central PostgreSQL. Para las sesiones de tokens y registro temporal de alta volatilidad, `RedisTokenSessionRepository` y `RedisRegistrationSessionRepository` encapsulan el acceso mediante `StringRedisTemplate`, configurando tiempos de expiración automáticos (TTL).
*   **GoogleTokenVerifierImpl:** Adaptador que consume las librerías cliente de Google para validar de forma criptográfica la autenticidad del ID Token recibido durante el flujo de OAuth2.
*   **JwtTokenEncoder:** Clase de infraestructura encargada de firmar algoritmos criptográficos HMAC-SHA256 para generar los Access Tokens (de corta duración) y Refresh Tokens (de larga duración).

#### 4.2.1.5. Bounded Context Software Architecture Component Level Diagrams

Dentro del contenedor **Platform API**, el contexto acotado de **IAM** se organiza internamente siguiendo el patrón de arquitectura hexagonal estructurada en las cuatro capas tácticas (Interfaces, Application, Domain e Infrastructure).

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/c4/containers/backend/components/contexts/IamLayers-dark.svg" alt="IAM Layer Components Diagram" width="850">
</p>

*   **IAM Interfaces (Component):** Recibe las solicitudes HTTP/HTTPS provenientes del API Gateway y las delega al servicio correspondiente en la capa de aplicación. Utiliza Spring Security para interceptar peticiones y validar los JWT de acceso de forma perimetral.
*   **IAM Application (Component):** Orquesta los casos de uso llamando a los modelos de dominio. Envía eventos e interactúa con el componente de infraestructura.
*   **IAM Domain (Component):** Mantiene los modelos enriquecidos de dominio y define las interfaces que actúan como contratos de persistencia.
*   **IAM Infrastructure (Component):** Implementa las interfaces de repositorio de dominio mediante tecnologías específicas (Spring Data JPA conectando a la base de datos relacional PostgreSQL, e integraciones con Redis y el SDK de Google).

#### 4.2.1.6. Bounded Context Software Architecture Code Level Diagrams

##### 4.2.1.6.1. Bounded Context Domain Layer Class Diagrams

A continuación, se detalla el diagrama de clases unificado de la capa de dominio del contexto acotado IAM, mostrando todas sus entidades, value objects, repositorios y firmas de métodos con visibilidad explícita:

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/iam-bc/unified.svg" alt="Unified IAM Domain Class Diagram" width="850">
</p>

##### 4.2.1.6.2. Bounded Context Database Design Diagram

FALTA!!! - AYUDA

### 4.2.2. Bounded Context: Billing

El contexto acotado de **Billing** es responsable de administrar el modelo de monetización de la plataforma. Controla las pasarelas de pago, los límites operativos impuestos a los usuarios según su plan (Freemium o Premium) y el procesamiento de suscripciones mensuales, integrándose de forma directa con la API externa de Stripe.

**Diccionario de Clases del Contexto Billing**

A continuación, se detallan las clases principales identificadas para este contexto, clasificadas por capa de arquitectura:

| Nombre de la Clase | Capa | Propósito / Responsabilidad | Atributos Principales | Métodos Clave | Relaciones de Asociación / Dependencia |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **UserPlan** | Dominio | Entidad raíz que define el plan de suscripción asignado a un usuario y sus fechas de vigencia. | `id` (UUID), `userId` (UserId), `planType` (PlanType), `startDate` (LocalDate), `endDate` (LocalDate) | `upgradeToPremium()`, `downgradeToFreemium()`, `isPremiumExpired()` | Contiene `UserId` y `PlanType`. |
| **PaymentRecord** | Dominio | Entidad que registra el historial de cobros y transacciones de los usuarios. | `id` (UUID), `userId` (UserId), `amount` (Money), `status` (PaymentStatus), `stripePaymentIntentId` (String) | `markAsCompleted()` | Contiene `UserId`, `Money` y `PaymentStatus`. |
| **PaymentGateway** | Dominio | Interfaz (Puerto) que define los métodos de interacción con pasarelas de cobro externas. | *N/A* | `createCheckoutSession()`, `createPaymentIntent()` | Implementado por `StripePaymentGatewayAdapter`. |
| **UserPlanRepository** | Dominio | Interfaz de repositorio para persistir y consultar el plan de un usuario. | *N/A* | `save()`, `findByUserId()` | Utilizado por los servicios de comando y consulta de suscripciones. |
| **PaymentRecordRepository** | Dominio | Interfaz de repositorio para persistir transacciones financieras. | *N/A* | `save()`, `findByStripePaymentIntentId()`, `findByUserId()` | Utilizado por los servicios de comando y consulta de suscripciones. |
| **SubscriptionController** | Interfaz | Controlador REST que expone endpoints para iniciar checkouts, degradar cuentas y ver planes activos. | `subscriptionCommandService`, `subscriptionQueryService` | `createCheckoutSession()`, `getSubscriptionsByUserId()`, `downgradeToFreemium()` | Depende de `SubscriptionCommandServiceImpl` y `SubscriptionQueryServiceImpl`. |
| **StripeWebhookController** | Interfaz | Controlador de entrada que procesa eventos asíncronos enviados por webhooks de Stripe. | `subscriptionCommandService`, `stripeWebhookSecret` | `handleWebhook()` | Depende de `SubscriptionCommandServiceImpl`. |
| **BillingContextFacade** | Interfaz | Fachada expuesta para que otros contextos consulten límites de negocio (suscripción activa del usuario). | *N/A* | `getMaxOrganizations()`, `getMaxSpaces()`, `getMaxDevices()` | Implementado por `BillingContextFacadeImpl`. |
| **SubscriptionCommandServiceImpl** | Aplicación | Servicio de aplicación que procesa comandos para actualizar suscripciones y registrar pagos exitosos. | `paymentGateway`, `paymentRecordRepository`, `userPlanRepository` | `handle(CreateCheckoutSessionCommand)`, `handle(FulfillSubscriptionCommand)` | Usa `PaymentGateway`, `PaymentRecordRepository` y `UserPlanRepository`. |
| **SubscriptionQueryServiceImpl** | Aplicación | Servicio de aplicación para consultar registros de pago e historial de planes activos. | `userPlanRepository`, `paymentRecordRepository` | `handle(GetSubscriptionByIdQuery)`, `resolveUserPlan()` | Usa `UserPlanRepository` y `PaymentRecordRepository`. |
| **StripePaymentGatewayAdapter** | Infraestructura | Adaptador que implementa el puerto `PaymentGateway` utilizando el SDK de Stripe. | `stripeApiKey` | `createCheckoutSession()`, `createPaymentIntent()` | Implementa `PaymentGateway`. |
| **JpaUserPlanRepository** | Infraestructura | Adaptador JPA que implementa `UserPlanRepository` para almacenar planes en PostgreSQL. | *N/A* | *N/A* | Implementa `UserPlanRepository`. |

---

#### 4.2.2.1. Domain Layer

La capa de dominio de Billing resguarda la consistencia del modelo de monetización y límites de la plataforma.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/billing-bc/domain-layer.svg" alt="Billing Domain Layer Class Diagram" width="750">
</p>

*   **Entities y Aggregates:** `UserPlan` mantiene las reglas de upgrade/downgrade temporal, determinando si el periodo de cobro ha expirado. `PaymentRecord` almacena el estado de cada pago (`PENDING`, `COMPLETED`, `FAILED`).
*   **Value Objects:** `Money` encapsula el monto y divisa de transacciones, mientras que `UserId` e `PlanType` regulan tipados y accesos.
*   **Ports:** `PaymentGateway` abstrae la lógica del cobro para no depender directamente de las librerías de Stripe a nivel de dominio.

#### 4.2.2.2. Interface Layer

Se encarga de recibir peticiones de cobro web y registrar webhooks provenientes de la pasarela de pagos.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/billing-bc/interfaces-layer.svg" alt="Billing Interface Layer Class Diagram" width="750">
</p>

*   **SubscriptionController:** Permite a los clientes iniciar la pasarela de checkout redirigiendo al portal de Stripe.
*   **StripeWebhookController:** Endpoint de escucha perimetral que recibe y valida firmas HMAC de Stripe para autorizar el cobro y aprovisionar el plan del usuario de forma asíncrona.
*   **BillingContextFacade:** Puerto expuesto internamente que permite a contextos externos (como Device Management) consultar los límites del plan (`getMaxDevices()`) para denegar emparejamientos si el plan del usuario es Freemium y ya alcanzó su cupo.

#### 4.2.2.3. Application Layer

Orquesta el aprovisionamiento de suscripciones y la recepción segura de pagos en la plataforma.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/billing-bc/application-layer.svg" alt="Billing Application Layer Class Diagram" width="750">
</p>

*   **Command Handlers:** `SubscriptionCommandServiceImpl` maneja la creación de intenciones de cobro y finaliza la activación del plan Premium cuando recibe el evento de pago aprobado.
*   **Event Handlers:** `UserRegisteredEventHandler` escucha el evento de integración `UserRegisteredEvent` (del contexto IAM) para asignarle inmediatamente un `UserPlan` en plan `FREEMIUM` al nuevo usuario.
*   **SubscriptionPaidEventHandler:** Transforma el webhook recibido en una confirmación interna de negocio para desbloquear funciones Premium.

#### 4.2.2.4. Infrastructure Layer

Provee la comunicación externa con Stripe y la persistencia de datos financieros.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/billing-bc/infrastructure-layer.svg" alt="Billing Infrastructure Layer Class Diagram" width="750">
</p>

*   **StripePaymentGatewayAdapter:** Consume el API externo de Stripe para generar enlaces de pago de manera dinámica.
*   **Adaptadores de base de datos:** `JpaUserPlanRepository` y `JpaPaymentRecordRepository` realizan la persistencia relacional en PostgreSQL para garantizar transacciones ACID.

#### 4.2.2.5. Bounded Context Software Architecture Component Level Diagrams

A nivel de contenedores en la API principal, el contexto de Billing descompone sus responsabilidades a través de componentes en capas:

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/c4/containers/backend/components/contexts/BillingLayers-dark.svg" alt="Billing Layer Components Diagram" width="850">
</p>

*   **Billing Interfaces (Component):** Expone los controladores de checkout y recepción de webhooks de Stripe.
*   **Billing Application (Component):** Orquesta los comandos de creación de cobros y escucha de registros de usuarios.
*   **Billing Domain (Component):** Contiene el modelo lógico de cobro y límites del plan de usuario.
*   **Billing Infrastructure (Component):** Implementa la integración técnica con el SDK de Stripe y la base de datos PostgreSQL.

#### 4.2.2.6. Bounded Context Software Architecture Code Level Diagrams

##### 4.2.2.6.1. Bounded Context Domain Layer Class Diagrams

El siguiente diagrama detalla la capa de dominio de Billing de forma unificada con sus correspondientes firmas, enumeraciones y multiplicidad:

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/billing-bc/unified.svg" alt="Unified Billing Domain Class Diagram" width="850">
</p>

##### 4.2.2.6.2. Bounded Context Database Design Diagram

FALTA!!! - AYUDA

### 4.2.3. Bounded Context: Device & Space Management

El contexto acotado de **Device & Space Management** gestiona el inventario de hardware y la organización espacial lógica de la plataforma. Permite registrar dispositivos de sensores (`Device`), asignar ubicaciones organizacionales (`Organization` y `Space`), controlar las vinculaciones físicas (`DeviceAssignment`), registrar comandos enviados al hardware (`DeviceCommand`) y definir los umbrales personalizados de alerta por dispositivo.

**Diccionario de Clases del Contexto Device & Space Management**

A continuación, se detallan las clases principales identificadas para este contexto, clasificadas por capa de arquitectura:

| Nombre de la Clase | Capa | Propósito / Responsabilidad | Atributos Principales | Métodos Clave | Relaciones de Asociación / Dependencia |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Device** | Dominio | Representa el sensor físico registrado en el sistema global. | `id` (UUID), `serialNumber` (String), `name` (String), `hardwareId` (HardwareId), `apiKey` (ApiKey) | `rotateApiKey()`, `updateName()` | Contiene `HardwareId` y `ApiKey`. |
| **DeviceAssignment** | Dominio | Entidad que modela el emparejamiento físico de un sensor a un espacio y usuario específico. | `id` (UUID), `device` (Device), `ownerUserId` (UserId), `spaceId` (UUID), `status` (DeviceStatus), `claimToken` (ClaimToken) | `claimToSpace()`, `markOnline()`, `markOffline()` | Contiene `Device`. |
| **DeviceCommand** | Dominio | Entidad que almacena el historial y estado de comandos enviados a un actuador. | `id` (UUID), `deviceId` (UUID), `commandType` (String), `payload` (String), `status` (String) | `acknowledge()` | Vinculado a `Device` por ID. |
| **Organization** | Dominio | Representa la agrupación lógica superior (empresa o cuenta principal) para locales comerciales. | `id` (UUID), `name` (String), `ownerUserId` (UserId) | `updateName()` | Vinculado a `UserId`. |
| **Space** | Dominio | Representa un espacio o zona física específica asociada a una organización (ej: "Sala A"). | `id` (UUID), `name` (String), `organizationId` (UUID) | `updateName()` | Asociado a `Organization` por ID. |
| **DeviceRepository** | Dominio | Interfaz de persistencia para el inventario de sensores registrados. | *N/A* | `save()`, `findById()`, `findByHardwareId()` | Utilizado por `DeviceCommandServiceImpl`. |
| **DeviceAssignmentRepository** | Dominio | Interfaz de persistencia para los emparejamientos y estados de conexión en tiempo real. | *N/A* | `save()`, `findByDeviceId()`, `findBySpaceId()` | Utilizado por los servicios de comando de dispositivos y espacios. |
| **DeviceController** | Interfaz | Controlador REST para emparejar, reclamar, listar y renombrar dispositivos sensores. | `deviceCommandService`, `deviceQueryService` | `pairDevice()`, `claimDevice()`, `getDevices()` | Depende de los servicios de aplicación de dispositivos. |
| **DeviceCommandController** | Interfaz | Controlador REST que permite emitir acciones o comandos manuales hacia los actuadores. | `deviceControlCommandService` | `createDeviceCommand()`, `getDeviceCommand()` | Depende de `DeviceControlCommandServiceImpl`. |
| **DeviceThresholdController** | Interfaz | Controlador REST para registrar y eliminar los umbrales de advertencia específicos de métricas de aire. | `thresholdCommandService` | `writeThreshold()`, `removeThreshold()` | Depende de `DeviceThresholdCommandServiceImpl`. |
| **OrganizationController** | Interfaz | Controlador REST para crear, renombrar y eliminar organizaciones. | `organizationCommandService` | `createOrganization()`, `updateOrganizationName()` | Depende de `OrganizationCommandServiceImpl`. |
| **SpaceController** | Interfaz | Controlador REST para crear y administrar los espacios de monitoreo. | `spaceCommandService` | `createSpace()`, `updateSpaceName()` | Depende de `SpaceCommandServiceImpl`. |
| **DeviceCommandServiceImpl** | Aplicación | Servicio de aplicación para el aprovisionamiento, vinculación y desvinculación de hardware Clair. | `deviceRepository`, `deviceAssignmentRepository`, `spaceRepository`, `publisher` | `handle(PairDeviceCommand)`, `handle(ClaimDeviceCommand)` | Usa repositorios y publica eventos vía Kafka. |
| **DeviceControlCommandServiceImpl** | Aplicación | Servicio para emitir comandos y despachar colas de acciones pendientes hacia los sensores. | `deviceCommandRepository`, `publisher` | `handle(CreateDeviceCommandCommand)` | Usa `DeviceCommandRepository` y Kafka. |
| **ProvisioningDevicesChangedKafkaPublisher** | Infraestructura | Adaptador para publicar eventos de integración de cambio de dispositivos en Apache Kafka. | `kafkaTemplate` | `publish()` | Implementa el puerto de mensajería para eventos de aprovisionamiento. |
| **JpaDeviceRepository** | Infraestructura | Adaptador JPA que implementa `DeviceRepository` para la base de datos PostgreSQL. | *N/A* | `findByHardwareId()` | Implementa `DeviceRepository`. |

---

#### 4.2.3.1. Domain Layer

La capa de dominio define el inventario físico y la jerarquía organizacional del sistema.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/device-bc/domain-layer.svg" alt="Device Domain Layer Class Diagram" width="750">
</p>

*   **Entities y Aggregates:** `Device` es el agregado de hardware. `DeviceAssignment` es la raíz de agregado que controla si un dispositivo está online/offline y en qué espacio físico y usuario está asignado. `DeviceCommand` controla el ciclo de vida de confirmación de órdenes. `Organization` y `Space` estructuran la geografía física de los sensores.
*   **Value Objects:** `HardwareId` (ID físico MAC/serie) y `ApiKey` (clave criptográfica de comunicación del sensor).
*   **Ports:** Interfaces de repositorio (`DeviceRepository`, `DeviceAssignmentRepository`, `DeviceCommandRepository`, `OrganizationRepository`, `SpaceRepository`).

#### 4.2.3.2. Interface Layer

Provee la interfaz REST para la gestión física del hardware y la estructuración espacial.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/device-bc/interfaces-layer.svg" alt="Device Interface Layer Class Diagram" width="750">
</p>

*   **DeviceController:** Registra y empareja dispositivos en el sistema.
*   **DeviceThresholdController:** Endpoint para configurar los límites seguros de las lecturas.
*   **OrganizationController y SpaceController:** API para configurar la estructura de locales y áreas.

#### 4.2.3.3. Application Layer

Orquesta los flujos de configuración del entorno e ingesta/acciones del hardware.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/device-bc/application-layer.svg" alt="Device Application Layer Class Diagram" width="750">
</p>

*   **DeviceCommandServiceImpl:** Coordina el emparejamiento seguro de dispositivos, validando las existencias de espacio y publicando en Kafka los cambios de asignación.
*   **DeviceControlCommandServiceImpl:** Administra el envío y despacho de comandos asíncronos para activar extractores o ventanas de ventilación inteligentes.
*   **SpaceCommandServiceImpl:** Orquesta el ciclo de vida del local, verificando a través del servicio externo `BillingContextFacade` (comunicación inter-contexto) si el plan del usuario tiene permisos para crear nuevos espacios.

#### 4.2.3.4. Infrastructure Layer

Proporciona persistencia SQL relacional para la configuración e integra mensajería Kafka.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/device-bc/infrastructure-layer.svg" alt="Device Infrastructure Layer Class Diagram" width="750">
</p>

*   **Adaptadores de Persistencia:** Repositorios Spring Data JPA que implementan los puertos de dominio para PostgreSQL.
*   **Kafka Publishers:** Adaptadores `ProvisioningDevicesChangedKafkaPublisher` y `DeviceCommandsPendingKafkaPublisher` que formatean y transmiten los payloads hacia las colas correspondientes de Apache Kafka.

#### 4.2.3.5. Bounded Context Software Architecture Component Level Diagrams

Organización de capas de componentes en el contenedor principal de la API para Device & Space Management:

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/c4/containers/backend/components/contexts/DeviceSpaceLayers-dark.svg" alt="Device & Space Layer Components Diagram" width="850">
</p>

*   **DeviceSpace Interfaces (Component):** Expone las API HTTP REST para la manipulación de la organización y emparejamiento de hardware.
*   **DeviceSpace Application (Component):** Orquesta los casos de uso llamando al dominio y disparando publicadores.
*   **DeviceSpace Domain (Component):** Aloja las reglas de asignación y jerarquías lógicas de espacios.
*   **DeviceSpace Infrastructure (Component):** Implementa el acceso físico a las tablas relacionales y el encolamiento de eventos en Kafka.

#### 4.2.3.6. Bounded Context Software Architecture Code Level Diagrams

##### 4.2.3.6.1. Bounded Context Domain Layer Class Diagrams

El diagrama unificado de dominio para Device & Space Management define la estructura táctica y relaciones:

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/device-bc/unified.svg" alt="Unified Device Domain Class Diagram" width="850">
</p>

##### 4.2.3.6.2. Bounded Context Database Design Diagram

FALTA!!! - AYUDA

### 4.2.4. Bounded Context: Air Quality Evaluation

El contexto acotado de **Air Quality Evaluation** es el encargado de procesar, analizar y almacenar la telemetría en tiempo real recibida desde los sensores físicos. Realiza la validación de integridad técnica de los datos y la posterior evaluación de las métricas ambientales de salubridad ($CO_2$, material particulado, temperatura y humedad) contra los umbrales configurados para cada espacio.

**Diccionario de Clases del Contexto Air Quality Evaluation**

A continuación, se detallan las clases principales identificadas para este contexto, clasificadas por capa de arquitectura:

| Nombre de la Clase | Capa | Propósito / Responsabilidad | Atributos Principales | Métodos Clave | Relaciones de Asociación / Dependencia |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **TelemetryEvaluation** | Dominio | Entidad raíz del agregado que consolida los datos ambientales de un sensor e indica su estado de salud general. | `id` (UUID), `deviceId` (DeviceId), `airQuality` (AirQuality), `particulateMatter` (ParticulateMatter), `connectivity` (Connectivity), `location` (Location) | *N/A* | Contiene `DeviceId`, `AirQuality`, `ParticulateMatter`, `Connectivity` y `Location`. |
| **DeviceId** | Dominio | Objeto de Valor (*Value Object*) que tipa de manera fuerte el identificador único del sensor. | `value` (UUID) | *N/A* | Composición en `TelemetryEvaluation`. |
| **AirQuality** | Dominio | Objeto de Valor que encapsula los niveles medidos de dióxido de carbono, temperatura y humedad. | `co2` (Double), `temperature` (Double), `humidity` (Double) | *N/A* | Composición en `TelemetryEvaluation`. |
| **ParticulateMatter** | Dominio | Objeto de Valor que agrupa la densidad medida de polvo y partículas suspendidas. | `pm1_0` (Double), `pm2_5` (Double), `pm10` (Double) | *N/A* | Composición en `TelemetryEvaluation`. |
| **Connectivity** | Dominio | Objeto de Valor que almacena datos de diagnóstico del hardware (señal, red, estado). | `status` (String), `network` (String), `signalStrength` (Double) | *N/A* | Composición en `TelemetryEvaluation`. |
| **Location** | Dominio | Objeto de Valor que identifica la localización geográfica del dispositivo reportado. | `country` (String) | *N/A* | Composición en `TelemetryEvaluation`. |
| **TelemetryEvaluationRepository** | Dominio | Interfaz (Puerto) que define los métodos de persistencia para el histórico de evaluaciones ambientales. | *N/A* | `save()`, `findByDeviceId()`, `findFirstByDeviceIdValueOrderByRecordedAtDesc()` | Utilizado por los servicios de comando y consulta de telemetría. |
| **TelemetryEvaluationController** | Interfaz | Controlador REST para solicitar evaluaciones manuales y obtener históricos o la última lectura de un dispositivo. | `telemetryEvaluationQueryService`, `telemetryEvaluationCommandService` | `evaluateTelemetry()`, `getLatestEvaluationByDevice()` | Depende de `TelemetryEvaluationCommandServiceImpl` y `TelemetryEvaluationQueryServiceImpl`. |
| **EvaluationContextFacade** | Interfaz | Fachada expuesta para que otros contextos consulten históricos agregados (como el módulo de Analytics). | *N/A* | `getLatestEvaluationRecordedAt()`, `getHourlyTelemetryAggregation()` | Implementado por `EvaluationContextFacadeImpl`. |
| **TelemetryEvaluationCommandServiceImpl** | Aplicación | Servicio de aplicación que procesa el comando de ingesta, evalúa los umbrales y guarda el registro. | `telemetryEvaluationRepository` | `handle(EvaluateTelemetryCommand)` | Usa `TelemetryEvaluationRepository` para persistir la evaluación. |
| **TelemetryEvaluationQueryServiceImpl** | Aplicación | Servicio de aplicación para consultar evaluaciones históricas de forma paginada o el último registro recibido. | `telemetryEvaluationRepository` | `handle(GetEvaluationsByDeviceQuery)`, `handle(GetLatestEvaluationByDeviceQuery)` | Usa `TelemetryEvaluationRepository`. |
| **TelemetryRecordedKafkaConsumer** | Aplicación | Consumidor (Listener) de Kafka que procesa asíncronamente los mensajes de telemetría e inicia la evaluación. | `telemetryEvaluationCommandService`, `externalDeviceService` | `consume()` | Recibe datos crudos, resuelve el ID mediante `ExternalDeviceService` y delega a `TelemetryEvaluationCommandService`. |
| **ExternalDeviceService** | Aplicación | Interfaz (Puerto de comunicación inter-contexto) para validar la existencia y pertenencia de un dispositivo. | *N/A* | `findDeviceIdByHardwareId()`, `isDeviceOwnedByUser()` | Consumido por el controlador y el consumidor Kafka. |
| **JpaTelemetryEvaluationRepository** | Infraestructura | Adaptador JPA que implementa `TelemetryEvaluationRepository` para PostgreSQL. | *N/A* | *N/A* | Implementa `TelemetryEvaluationRepository`. |

---

#### 4.2.4.1. Domain Layer

La capa de dominio modela las especificaciones físicas de calidad del aire y la integridad de las lecturas ambientales.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/evaluation-bc/domain-layer.svg" alt="Evaluation Domain Layer Class Diagram" width="750">
</p>

*   **Entities y Aggregates:** `TelemetryEvaluation` representa el agregado principal que encapsula el estado físico del aire medido en un punto temporal específico.
*   **Value Objects:** `AirQuality` (parámetros de gases y ambiente), `ParticulateMatter` (concentración de polvo PM1.0, PM2.5, PM10), `Connectivity` (diagnóstico de señal), `Location` (país de reporte) y `DeviceId`.
*   **Ports:** `TelemetryEvaluationRepository` es el puerto de repositorio para guardar y recuperar mediciones.

#### 4.2.4.2. Interface Layer

Provee los endpoints HTTP y fachadas internas para consultar las evaluaciones y estados ambientales.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/evaluation-bc/interfaces-layer.svg" alt="Evaluation Interface Layer Class Diagram" width="750">
</p>

*   **TelemetryEvaluationController:** Expone endpoints RESTful para obtener la telemetría en tiempo real de un dispositivo o su histórico paginado de evaluaciones.
*   **EvaluationContextFacade:** Fachada de comunicación interna utilizada por el contexto acotado de Analytics & Reporting para recuperar consolidados de telemetría horaria sin acoplarse a los repositorios de este contexto.

#### 4.2.4.3. Application Layer

Orquesta la ingesta de eventos de telemetría y ejecuta los flujos de consulta ambiental.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/evaluation-bc/application-layer.svg" alt="Evaluation Application Layer Class Diagram" width="750">
</p>

*   **TelemetryRecordedKafkaConsumer (Event Handler):** Suscriptor de Kafka que escucha de forma reactiva y no bloqueante los eventos del bus de mensajería asíncrona cuando un sensor Clair reporta telemetría.
*   **TelemetryEvaluationCommandServiceImpl:** Recibe el comando de validación, realiza los cálculos de salubridad y guarda la evaluación en base a los umbrales configurados.
*   **ExternalDeviceService (Port):** Puerto para interactuar de forma segura con el contexto de `Device Management` y validar la existencia y propietario de los sensores.

#### 4.2.4.4. Infrastructure Layer

Provee el acceso físico al motor de series temporales/PostgreSQL.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/evaluation-bc/infrastructure-layer.svg" alt="Evaluation Infrastructure Layer Class Diagram" width="750">
</p>

*   **JpaTelemetryEvaluationRepository:** Adaptador que traduce las consultas y escrituras del dominio en sentencias SQL a través de Spring Data JPA sobre PostgreSQL.

#### 4.2.4.5. Bounded Context Software Architecture Component Level Diagrams

Dentro del backend de Platform API, las capas tácticas de Air Quality Evaluation se representan bajo los siguientes componentes organizados:

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/c4/containers/backend/components/contexts/AirQualityLayers-dark.svg" alt="Air Quality Layer Components Diagram" width="850">
</p>

*   **AirQuality Interfaces (Component):** Expone las API HTTP y la Fachada interna de consulta del aire.
*   **AirQuality Application (Component):** Procesa de forma reactiva los eventos procedentes de Kafka y ejecuta comandos de persistencia.
*   **AirQuality Domain (Component):** Modela la estructura lógica de los gases y partículas finas.
*   **AirQuality Infrastructure (Component):** Implementa el repositorio conectándose a PostgreSQL para almacenar el histórico ambiental.

#### 4.2.4.6. Bounded Context Software Architecture Code Level Diagrams

##### 4.2.4.6.1. Bounded Context Domain Layer Class Diagrams

El diagrama unificado de clases del dominio para Air Quality Evaluation define los atributos y métodos completos:

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/evaluation-bc/unified.svg" alt="Unified Air Quality Domain Class Diagram" width="850">
</p>

##### 4.2.4.6.2. Bounded Context Database Design Diagram

FALTA!!! - AYUDA

### 4.2.5. Bounded Context: Alerting & Response

El contexto acotado de **Alerting & Response** es responsable del ciclo de vida de los incidentes de calidad del aire. Evalúa de forma continua la telemetría recibida contra los umbrales específicos de seguridad, dispara alertas ante transgresiones de límites de contaminantes, gestiona el acuse de recibo de los operadores y despacha comandos de respuesta hacia los dispositivos inteligentes de forma autónoma.

**Diccionario de Clases del Contexto Alerting & Response**

A continuación, se detallan las clases principales identificadas para este contexto, clasificadas por capa de arquitectura:

| Nombre de la Clase | Capa | Propósito / Responsabilidad | Atributos Principales | Métodos Clave | Relaciones de Asociación / Dependencia |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Alert** | Dominio | Entidad raíz del agregado que modela el ciclo de vida de un incidente ambiental (abierto, reconocido, cerrado). | `id` (UUID), `deviceId` (UUID), `spaceId` (UUID), `metric` (MetricType), `thresholdValue` (BigDecimal), `actualValue` (BigDecimal), `message` (String), `status` (AlertStatus), `severity` (AlertSeverity), `occurredAt` (Instant), `resolvedAt` (Instant) | `acknowledge()`, `resolve(resolvedAt)` | Contiene `MetricType`, `AlertStatus` y `AlertSeverity`. |
| **MetricType** | Dominio | Enumeración que define las métricas propensas a generar alertas. | *N/A* | *N/A* | Composición en `Alert`. |
| **AlertSeverity** | Dominio | Enumeración que indica la gravedad de la alerta (Low, Warning, Critical). | *N/A* | *N/A* | Composición en `Alert`. |
| **AlertStatus** | Dominio | Enumeración para controlar el estado de atención del incidente (Active, Acknowledged, Resolved). | *N/A* | *N/A* | Composición en `Alert`. |
| **AlertRepository** | Dominio | Interfaz (Puerto) que define los métodos de persistencia para las alertas. | *N/A* | `save()`, `findById()`, `findFirstByDeviceIdAndMetricAndStatusIn()` | Utilizado por los servicios de aplicación de alertas. |
| **AlertController** | Interfaz | Controlador REST para consultar alertas de dispositivos, espacios y obtener resúmenes. | `alertQueryService` | `getAlertsByDevice()`, `getAlertsBySpace()`, `getDailySummary()` | Depende de `AlertQueryServiceImpl`. |
| **AlertingContextFacade** | Interfaz | Fachada interna expuesta para que otros contextos consulten detalles específicos de incidentes. | *N/A* | `findAlertDetailsById()` | Implementado por `AlertingContextFacadeImpl`. |
| **AlertCommandServiceImpl** | Aplicación | Servicio de aplicación para evaluar telemetría, generar incidentes o resolverlos automáticamente. | `alertRepository`, `externalThresholdService`, `externalDeviceService`, `publisher` | `handle(EvaluateTelemetryForAlertsCommand)` | Usa `AlertRepository`, puertos externos de consulta y publica en Kafka. |
| **AlertQueryServiceImpl** | Aplicación | Servicio de consulta para obtener historiales de incidentes filtrados y resúmenes diarios. | `alertRepository`, `externalDeviceService` | `handle(GetAlertsByDeviceQuery)`, `handle(GetAlertsByOwnerQuery)` | Usa `AlertRepository` y `ExternalAlertingDeviceService`. |
| **AlertingTelemetryRecordedKafkaConsumer** | Aplicación | Consumidor asíncrono de Kafka que procesa lecturas reportadas para gatillar la detección de alertas. | `alertCommandService` | `consume()` | Delega a `AlertCommandServiceImpl` la evaluación del payload recibido. |
| **ExternalAlertingDeviceService** | Aplicación | Interfaz (Puerto de comunicación inter-contexto) para obtener nombres y localizaciones del hardware. | *N/A* | `fetchSpaceIdByDeviceId()`, `fetchDeviceNameByDeviceId()` | Utilizado por `AlertCommandServiceImpl`. |
| **ExternalAlertingThresholdService** | Aplicación | Interfaz (Puerto de comunicación inter-contexto) para obtener los umbrales habilitados por sensor. | *N/A* | `fetchEnabledThresholdsByDeviceId()` | Utilizado por `AlertCommandServiceImpl`. |
| **JpaAlertRepository** | Infraestructura | Adaptador JPA que implementa `AlertRepository` para almacenar alertas en PostgreSQL. | *N/A* | *N/A* | Implementa `AlertRepository`. |
| **AlertIncidentsChangedKafkaPublisher** | Infraestructura | Adaptador que publica eventos de integración de cambio de estado de alertas en Apache Kafka. | `kafkaTemplate` | `publish()` | Publica eventos consumidos por otros contextos (como notificaciones). |

#### 4.2.5.1. Domain Layer

La capa de dominio gestiona la lógica del ciclo de vida de los incidentes y las reglas de severidad del aire.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/alerting-bc/domain-layer.svg" alt="Alerting Domain Layer Class Diagram" width="750">
</p>

*   **Entities y Aggregates:** `Alert` actúa como agregado que encapsula los datos puntuales del incidente, implementando los métodos de negocio `acknowledge()` (acuse de recibo humano) y `resolve()` (cierre técnico de la alerta).
*   **Value Objects / Enums:** Enums `MetricType` (CO2, PM2.5, temperatura, humedad), `AlertStatus` y `AlertSeverity`.
*   **Ports:** `AlertRepository` define el contrato para almacenar y consultar alertas activas de sensores.

#### 4.2.5.2. Interface Layer

Expone las APIs para la consulta de incidentes y provee fachadas para la interacción inter-contextos.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/alerting-bc/interfaces-layer.svg" alt="Alerting Interface Layer Class Diagram" width="750">
</p>

*   **AlertController:** Controlador REST para listar alertas e incidentes históricos o activos por local o dispositivo.
*   **AlertingContextFacade:** Fachada de comunicación directa utilizada para que otros contextos de la aplicación consulten la gravedad de un incidente específico de forma rápida.

#### 4.2.5.3. Application Layer

Orquesta la evaluación reactiva de las lecturas físicas e inicia el despacho de notificaciones de incidentes.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/alerting-bc/application-layer.svg" alt="Alerting Application Layer Class Diagram" width="750">
</p>

*   **AlertingTelemetryRecordedKafkaConsumer:** Listener asíncrono que procesa las lecturas de telemetría emitidas en el broker.
*   **AlertCommandServiceImpl:** Resuelve el caso de uso central: analiza la lectura recibida contra los umbrales configurados (obtenidos mediante `ExternalAlertingThresholdService`). Si hay transgresión y no existe una alerta activa para esa métrica, crea un nuevo incidente `Alert` y publica un evento `AlertIncidentChangedIntegrationEvent` en Kafka.
*   **Ports de consulta:** `ExternalAlertingDeviceService` y `ExternalAlertingThresholdService` resuelven datos de otros contextos de forma desacoplada.

#### 4.2.5.4. Infrastructure Layer

Provee almacenamiento relacional SQL y control del encolamiento de eventos de incidentes.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/alerting-bc/infrastructure-layer.svg" alt="Alerting Infrastructure Layer Class Diagram" width="750">
</p>

*   **JpaAlertRepository:** Adaptador concreto que persiste los registros de incidentes en PostgreSQL.
*   **AlertIncidentsChangedKafkaPublisher:** Adaptador que despacha los eventos de integración de alertas abiertas/resueltas a colas de Apache Kafka.

#### 4.2.5.5. Bounded Context Software Architecture Component Level Diagrams

Estructuración de componentes internos para Alerting & Response en el contenedor principal de la API:

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/c4/containers/backend/components/contexts/AlertingLayers-dark.svg" alt="Alerting Layer Components Diagram" width="850">
</p>

*   **Alerting Interfaces (Component):** Expone las API HTTP REST para la auditoría y gestión de alertas.
*   **Alerting Application (Component):** Consume lecturas e inicia la evaluación y despacho de eventos de incidentes.
*   **Alerting Domain (Component):** Define las reglas lógicas de incidentes y estados de severidad.
*   **Alerting Infrastructure (Component):** Conecta a PostgreSQL para almacenamiento y encola avisos en el broker de Kafka.

#### 4.2.5.6. Bounded Context Software Architecture Code Level Diagrams

##### 4.2.5.6.1. Bounded Context Domain Layer Class Diagrams

El diagrama unificado de dominio para Alerting & Response define las propiedades completas del agregado:

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/alerting-bc/unified.svg" alt="Unified Alerting Domain Class Diagram" width="850">
</p>

##### 4.2.5.6.2. Bounded Context Database Design Diagram

FALTA!!! - AYUDA

### 4.2.6. Bounded Context: Analytics & Reporting

El contexto acotado de **Analytics & Reporting** se encarga de estructurar el análisis retrospectivo del aire, consolidar métricas de telemetría en series temporales agregadas (diarias y mensuales), y generar los reportes de salubridad y dashboards interactivos. Utiliza técnicas de Server-Sent Events (SSE) para servir telemetría en tiempo real y programadores de tareas en segundo plano (*schedulers*) para consolidar reportes históricos.

**Diccionario de Clases del Contexto Analytics & Reporting**

A continuación, se detallan las clases principales identificadas para este contexto, clasificadas por capa de arquitectura:

| Nombre de la Clase | Capa | Propósito / Responsabilidad | Atributos Principales | Métodos Clave | Relaciones de Asociación / Dependencia |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **DeviceAnalyticsSnapshot** | Dominio | Entidad que almacena promedios ambientales calculados para un sensor en una ventana temporal (ej: 1 hora). | `id` (UUID), `deviceId` (DeviceId), `timeWindowStart` (Instant), `averageCo2` (Double), `calculatedAqi` (AirQualityIndex) | *N/A* | Contiene `DeviceId` y `AirQualityIndex`. |
| **DeviceDailySummary** | Dominio | Entidad raíz del agregado para reportes históricos consolidados de un día. | `id` (UUID), `deviceId` (DeviceId), `summaryDate` (LocalDate), `co2` (MetricStats), `pm2_5` (MetricStats), `averageAqi` (Integer) | *N/A* | Contiene `DeviceId`, `MetricStats` y `AqiCategoryBreakdown`. |
| **DeviceMonthlySummary** | Dominio | Entidad raíz del agregado para consolidados históricos por mes. | `id` (UUID), `deviceId` (DeviceId), `summaryMonth` (LocalDate), `daysCovered` (int) | *N/A* | Contiene `DeviceId` y `MetricStats`. |
| **MetricStats** | Dominio | Objeto de Valor (*Value Object*) que agrupa estadísticas mínimas, máximas y promedio de una métrica. | `avg` (Double), `min` (Double), `max` (Double) | *N/A* | Composición en los resúmenes diario y mensual. |
| **AqiCategoryBreakdown** | Dominio | Objeto de Valor que segmenta la cantidad de horas en que el aire estuvo en cada estado de riesgo. | `good` (Long), `moderate` (Long), `hazardous` (Long) | `plus()`, `dominant()` | Composición en los resúmenes diario y mensual. |
| **AirQualityIndex** | Dominio | Objeto de Valor que encapsula la escala y categoría oficial de AQI (Índice de Calidad del Aire). | `value` (Double), `category` (AqiCategory) | *N/A* | Composición en `DeviceAnalyticsSnapshot`. |
| **AqiCalculationDomainService** | Dominio | Servicio de Dominio que implementa las fórmulas oficiales EPA para calcular el nivel de AQI. | *N/A* | `calculateAqi(pm2_5, co2)` | Utilizado por los generadores de reportes y schedulers. |
| **DeviceAnalyticsSnapshotRepository** | Dominio | Interfaz de repositorio para almacenar y recuperar snapshots temporales. | *N/A* | `save()`, `findByDeviceIdAndTimeWindowStartBetween()` | Utilizado por servicios de consulta de tendencias. |
| **AnalyticsController** | Interfaz | Controlador REST para servir streams en tiempo real vía SSE e históricos de tendencias. | `kpiDashboardMetricsQueryService`, `analyticsSseService` | `getLiveMetrics()`, `streamLiveMetrics()`, `getTrends()` | Depende de los servicios de aplicación del dashboard. |
| **ReportController** | Interfaz | Controlador REST que exporta los resúmenes en formato de reportes diarios y mensuales. | `dailyReportQueryService`, `externalBillingService` | `getDailyReport()`, `getMonthlyReport()` | Valida permisos llamando a `ExternalBillingService`. |
| **KpiLiveMetricsCommandServiceImpl** | Aplicación | Servicio de aplicación que procesa la telemetría en caliente, refresca la caché y transmite vía SSE. | `kpiLiveMetricsCache`, `analyticsSseService` | `handle(ProcessTelemetryAnalyticCommand)` | Actualiza la caché y activa difusión SSE. |
| **DailyReportAggregationService** | Aplicación | Generador programado por lotes que procesa lecturas diarias anteriores para emitir reportes históricos. | `dailySummaryRepository`, `aqiCalculationDomainService` | `aggregatePreviousDay()` | Ejecuta agregación SQL masiva e inserta reportes en PostgreSQL. |
| **TelemetryAnalyticKafkaConsumer** | Aplicación | Consumidor de Kafka que escucha la telemetría recibida para actualizar de forma asíncrona la caché KPI. | `kpiLiveMetricsCommandService` | `consume()` | Transmite datos al procesador de métricas en vivo. |
| **ExternalBillingService** | Aplicación | Interfaz (Puerto de comunicación inter-contexto) para validar límites del plan antes de servir reportes. | *N/A* | `canAccessMonthlyReports()` | Consumido por el `ReportController`. |
| **DeviceDailySummaryRepository** | Infraestructura | Puerto (Interfaz de persistencia relacional) para guardar y buscar reportes de resumen diario. | *N/A* | `findByDeviceIdAndDate()`, `existsByDeviceIdAndDate()` | Implementado en la capa de infraestructura. |

#### 4.2.6.1. Domain Layer

La capa de dominio de Analytics implementa las estructuras estadísticas y cálculos matemáticos para reportes y AQI.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/analytics-bc/domain-layer.svg" alt="Analytics Domain Layer Class Diagram" width="750">
</p>

*   **Entities y Aggregates:** `DeviceDailySummary` y `DeviceMonthlySummary` son los agregados a largo plazo que consolidan el historial de calidad del aire. `DeviceAnalyticsSnapshot` es la entidad utilizada para agrupar lecturas en micro-ventanas de análisis.
*   **Value Objects:** `MetricStats` (mín/máx/promedio), `AqiCategoryBreakdown` (distribución de riesgo diario), `AirQualityIndex` e `DeviceId`.
*   **Domain Services:** `AqiCalculationDomainService` (calcula el índice oficial de calidad del aire), `MetricsAggregationDomainService` (funciones estadísticas de agregación) y `TrendAnalysisDomainService` (análisis de variación de contaminantes).

#### 4.2.6.2. Interface Layer

Provee interfaces para la visualización en vivo de métricas y la descarga de resúmenes estructurados.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/analytics-bc/interfaces-layer.svg" alt="Analytics Interface Layer Class Diagram" width="750">
</p>

*   **AnalyticsController:** Provee endpoints tradicionales para consultar métricas, así como conexiones asíncronas persistentes basadas en Server-Sent Events (SSE) a través de `SseEmitter` para empujar lecturas en vivo a las aplicaciones cliente sin sobrecargar el servidor.
*   **AnalyticsOverviewController:** Consolida los indicadores de salud y estados de conexión para la vista del panel principal.
*   **ReportController:** Expone la obtención de reportes diarios y mensuales, validando la autorización mediante llamadas desacopladas.

#### 4.2.6.3. Application Layer

Orquesta los flujos de analítica en tiempo real y el procesamiento diferido de reportes por lotes (*batch*).

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/analytics-bc/application-layer.svg" alt="Analytics Application Layer Class Diagram" width="750">
</p>

*   **KpiLiveMetricsCommandServiceImpl:** Recibe eventos de Kafka en caliente, actualiza un caché rápido en memoria `KpiLiveMetricsCache` y transmite la información vía SSE.
*   **Daily/Monthly Report Aggregation Service:** Tareas del sistema que leen de forma asíncrona datos del día/mes anterior para consolidar métricas transaccionales masivas.
*   **SnapshotAggregationScheduler:** Componente temporizado que ejecuta periódicamente promedios de telemetría y los guarda en base de datos.

#### 4.2.6.4. Infrastructure Layer

Implementa la persistencia a largo plazo para agregados analíticos.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/analytics-bc/infrastructure-layer.svg" alt="Analytics Infrastructure Layer Class Diagram" width="750">
</p>

*   **Adaptadores de Repositorio:** `JpaDeviceAnalyticsSnapshotRepository`, `DeviceDailySummaryRepository` y `DeviceMonthlySummaryRepository` implementan los puertos de dominio persistiendo en PostgreSQL.

#### 4.2.6.5. Bounded Context Software Architecture Component Level Diagrams

Organización de capas de componentes en el contenedor principal de la API para Analytics & Reporting:

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/c4/containers/backend/components/contexts/AnalyticsLayers-dark.svg" alt="Analytics Layer Components Diagram" width="850">
</p>

*   **Analytics Interfaces (Component):** Expone las API HTTP REST y gestiona las conexiones abiertas para streams SSE.
*   **Analytics Application (Component):** Orquesta los schedulers, consume del bus de Kafka y escribe en memoria caché.
*   **Analytics Domain (Component):** Modela las fórmulas oficiales de AQI y agregaciones estadísticas.
*   **Analytics Infrastructure (Component):** Persiste los reportes e históricos de snapshots en las tablas relacionales de PostgreSQL.

#### 4.2.6.6. Bounded Context Software Architecture Code Level Diagrams

##### 4.2.6.6.1. Bounded Context Domain Layer Class Diagrams

El diagrama unificado de dominio para Analytics & Reporting define la estructura táctica y las firmas completas del contexto:

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/analytics-bc/unified.svg" alt="Unified Analytics Domain Class Diagram" width="850">
</p>

##### 4.2.6.6.2. Bounded Context Database Design Diagram

FALTA!!! - AYUDA

### 4.2.7. Bounded Context: Notifications

El contexto acotado de **Notifications** unifica el envío de mensajes a los usuarios a través de múltiples canales, incluyendo correos electrónicos transaccionales y notificaciones push en dispositivos móviles. Actúa como un módulo puramente utilitario y reactivo que responde a eventos disparados por otros contextos de la aplicación (como alertas críticas o códigos de registro).

**Diccionario de Clases del Contexto Notifications**

A continuación, se detallan las clases principales identificadas para este contexto, clasificadas por capa de arquitectura:

| Nombre de la Clase | Capa | Propósito / Responsabilidad | Atributos Principales | Métodos Clave | Relaciones de Asociación / Dependencia |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **EmailLog** | Dominio | Entidad que registra el historial, estado y errores de los envíos de correos electrónicos. | `id` (UUID), `recipient` (EmailRecipient), `subject` (EmailSubject), `content` (EmailContent), `status` (String), `sentAt` (Instant) | *N/A* | Contiene `EmailRecipient`, `EmailSubject` y `EmailContent`. |
| **PushNotificationLog** | Dominio | Entidad que registra las notificaciones push despachadas a los dispositivos de los usuarios. | `id` (UUID), `userId` (UUID), `title` (String), `message` (String), `status` (String), `sentAt` (Instant), `externalId` (String) | *N/A* | Vinculado a `UserId` por ID. |
| **EmailDeliveryService** | Dominio | Interfaz (Puerto) que define la firma técnica para despachar correos electrónicos. | *N/A* | `send()` | Implementado por `SmtpEmailService` o adaptadores externos. |
| **PushNotificationDeliveryService** | Dominio | Interfaz (Puerto) que define el envío de alertas push directas al smartphone. | *N/A* | `sendPush()` | Implementado por `OneSignalPushNotificationService`. |
| **EmailRecipient** | Dominio | Objeto de Valor (*Value Object*) para encapsular la dirección de correo destinataria. | `value` (String) | *N/A* | Composición en `EmailLog`. |
| **EmailSubject** | Dominio | Objeto de Valor que encapsula el asunto o título del correo. | `value` (String) | *N/A* | Composición en `EmailLog`. |
| **EmailContent** | Dominio | Objeto de Valor para el cuerpo y formato del correo. | `value` (String) | *N/A* | Composición en `EmailLog`. |
| **EmailLogRepository** | Dominio | Interfaz de persistencia para auditar el historial de emails enviados. | *N/A* | `save()` | Utilizado por `EmailCommandServiceImpl`. |
| **PushNotificationLogRepository** | Dominio | Interfaz de persistencia para auditar las alertas push. | *N/A* | `save()` | Utilizado por `AlertIncidentChangedKafkaConsumer`. |
| **NotificationController** | Interfaz | Controlador REST utilitario para realizar tests rápidos de conectividad y envíos. | *N/A* | `testEmail()` | Depende de `EmailCommandServiceImpl`. |
| **NotificationsContextFacade** | Interfaz | Fachada expuesta internamente para ordenar envíos rápidos de emails de verificación. | *N/A* | `sendVerificationCode()` | Implementado por `NotificationsContextFacadeImpl`. |
| **EmailCommandServiceImpl** | Aplicación | Servicio de aplicación que procesa comandos de envío de correos (código, bienvenida). | `emailDeliveryService`, `emailLogRepository` | `handle(SendVerificationCodeCommand)`, `handle(SendWelcomeEmailCommand)` | Usa `EmailDeliveryService` y `EmailLogRepository`. |
| **AlertIncidentChangedKafkaConsumer** | Aplicación | Consumidor asíncrono de Kafka que escucha cambios en incidentes de alertas para despachar notificaciones push. | `pushNotificationDeliveryService`, `externalDeviceService`, `externalAlertingService` | `consume()` | Resuelve detalles de hardware e incidentes y envía push a través del SDK. |
| **SmtpEmailService** | Infraestructura | Adaptador concreto que despacha correos utilizando SMTP local o servidor de correo de Spring. | `mailSender` | `send()` | Implementa `EmailDeliveryService`. |
| **OneSignalPushNotificationService** | Infraestructura | Adaptador que implementa `PushNotificationDeliveryService` utilizando la API de OneSignal. | `oneSignalApiKey` | `sendPush()` | Implementa `PushNotificationDeliveryService`. |

#### 4.2.7.1. Domain Layer

La capa de dominio de Notifications contiene los modelos para auditoría de entrega de mensajes y los puertos de infraestructura.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/notifications-bc/domain-layer.svg" alt="Notifications Domain Layer Class Diagram" width="750">
</p>

*   **Entities y Aggregates:** `EmailLog` (auditoría de correos enviados, registrando errores si fallan) y `PushNotificationLog` (auditoría de notificaciones móviles con su respectivo ID externo del proveedor).
*   **Value Objects:** `EmailRecipient` (correo destinatario), `EmailSubject` y `EmailContent`.
*   **Ports:** Interfaces de servicios técnicos (`EmailDeliveryService`, `PushNotificationDeliveryService`) e interfaces de repositorio (`EmailLogRepository`, `PushNotificationLogRepository`).

#### 4.2.7.2. Interface Layer

Expone las fachadas internas del sistema para delegar envíos de forma rápida.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/notifications-bc/interfaces-layer.svg" alt="Notifications Interface Layer Class Diagram" width="750">
</p>

*   **NotificationController:** Endpoint REST utilitario de prueba.
*   **NotificationsContextFacade:** Fachada de comunicación directa que permite al contexto de IAM gatillar el envío de códigos de confirmación de forma síncrona sin acoplarse a SMTP.

#### 4.2.7.3. Application Layer

Orquesta los flujos de mensajería y procesa los eventos procedentes del bus asíncrono.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/notifications-bc/application-layer.svg" alt="Notifications Application Layer Class Diagram" width="750">
</p>

*   **AlertIncidentChangedKafkaConsumer:** Listener asíncrono que reacciona de forma inmediata a los eventos de incidentes modificados. Cuando una alerta crítica es detectada, consulta al contexto de dispositivo (`ExternalDeviceService`) para obtener al propietario y despacha la notificación push.
*   **EmailCommandServiceImpl:** Recibe comandos para formatear plantillas de correos electrónicos transaccionales y delega la transmisión física al servicio de entrega.

#### 4.2.7.4. Infrastructure Layer

Conecta la aplicación a servidores de correo electrónico y servicios externos de mensajería push.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/notifications-bc/infrastructure-layer.svg" alt="Notifications Infrastructure Layer Class Diagram" width="750">
</p>

*   **SmtpEmailService:** Adaptador SMTP estándar.
*   **OneSignalPushNotificationService:** Adaptador que realiza peticiones HTTP seguras al API de OneSignal para encolar alertas push móviles.
*   **Repositorios JPA:** Adaptadores Spring Data JPA para la persistencia del log histórico en PostgreSQL.

#### 4.2.7.5. Bounded Context Software Architecture Component Level Diagrams

Organización de componentes en el Platform API para el contexto acotado de Notifications:

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/c4/containers/backend/components/contexts/NotificationsLayers-dark.svg" alt="Notifications Layer Components Diagram" width="850">
</p>

*   **Notifications Interfaces (Component):** Expone las interfaces REST y fachadas de llamadas internas.
*   **Notifications Application (Component):** Procesa eventos de incidentes de Kafka y formatea los templates de emails.
*   **Notifications Domain (Component):** Modela el estado lógicos de envíos de alertas y correos.
*   **Notifications Infrastructure (Component):** Implementa el cliente SMTP, la integración HTTP de OneSignal y la persistencia JPA a PostgreSQL.

#### 4.2.7.6. Bounded Context Software Architecture Code Level Diagrams

##### 4.2.7.6.1. Bounded Context Domain Layer Class Diagrams

El diagrama de clases unificado del dominio de Notifications muestra todas sus entidades, value objects y métodos con visibilidad explícita:

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/backend/notifications-bc/unified.svg" alt="Unified Notifications Domain Class Diagram" width="850">
</p>

##### 4.2.7.6.2. Bounded Context Database Design Diagram

FALTA!!! - AYUDA

## 4.3. Tactical-Level Domain-Driven Design - Web application

El frontend de Clair está desarrollado bajo el framework Angular, organizando sus módulos mediante la separación estricta en cuatro capas siguiendo las directrices de Domain-Driven Design (DDD) táctico. Esta arquitectura promueve el desacoplamiento de la interfaz gráfica y los mecanismos de red del negocio principal de la aplicación.

**Arquitectura de Componentes de la Aplicación Web (Angular Frontend)**

A continuación se detalla el diagrama C4 de nivel de Componentes para la aplicación web de Clair, ilustrando la organización interna de los Bounded Contexts y cómo interactúan las capas de interfaces, aplicación, dominio e infraestructura:

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/c4/containers/frontend/WebAppComponents-dark.svg" alt="Web Application Component Architecture Diagram" width="850">
</p>

*   **Interfaces Layer (Componente de Presentación):** Contiene los componentes visuales de Angular (Pages, Cards, Tables, Modals) que se encargan de renderizar la interfaz y capturar eventos del usuario, además de mappers/transformadores locales e interceptores HTTP que inyectan el token JWT de forma transparente.
*   **Application Layer (Componente de Aplicación):** Orquesta los flujos de control de los casos de uso a través de la implementación de servicios de comandos (`CommandServiceImpl`) y consultas (`QueryServiceImpl`). No contiene lógica de negocio directa, sino que delega la ejecución de reglas al dominio y gestiona transacciones y transformaciones.
*   **Domain Layer (Componente de Dominio):** Representa el núcleo del negocio. Aquí se ubican las interfaces de servicios de comandos/consultas, los contratos de pasarela (`Gateway Interfaces`), entidades de dominio, enums y value objects puros. Esta capa es agnóstica de frameworks o librerías externas.
*   **Infrastructure Layer (Componente de Infraestructura):** Implementa los adaptadores concretos definidos en la capa de dominio. Esto incluye pasarelas HTTP (`HttpGateways`) encargadas de consumir la API REST del backend mediante el `HttpClient` de Angular y el almacenamiento persistente en el cliente mediante el uso de LocalStorage.

### 4.3.1. Bounded Context: Identity & Access Management (IAM)

#### 4.3.1.1. Domain Layer

Define las reglas de negocio principales, entidades, value objects e interfaces de servicio para la autenticación y autorización de usuarios.

*   **AuthCommandService (Interface):** Interfaz que define las operaciones de comando para iniciar sesión, registrarse y confirmar cuentas.
*   **AuthQueryService (Interface):** Interfaz que define la verificación de tokens y consultas del estado de sesión.
*   **AuthGateway (Interface):** Contrato que modela las interacciones de autenticación contra APIs externas.
*   **TokenStorageGateway (Interface):** Contrato encargado de abstraer el guardado, recuperación y eliminación de tokens de sesión (Access y Refresh tokens).
*   **SignInCommand / SignUpCommand (Value Objects):** Objetos de valor inmutables que encapsulan las credenciales del usuario.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/frontend/iam_bc_class_diagram/domain-iam.svg" alt="Frontend IAM Domain Layer Class Diagram" width="750">
</p>

#### 4.3.1.2. Interface Layer

Se encarga de la interacción directa con el usuario, controlando el ciclo de vida de los formularios y las peticiones salientes mediante interceptores.

*   **LoginPageComponent:** Componente Angular que procesa el formulario de login y maneja los eventos `onSignIn()` y `onSignInWithGoogle()`.
*   **RegisterPageComponent:** Componente Angular para el registro de nuevos usuarios en la plataforma.
*   **ConfirmPageComponent:** Componente para validar el código de verificación enviado por correo electrónico.
*   **AuthInterceptor:** Interceptor HTTP de Angular que recupera el token de acceso actual desde `TokenStorageGateway` y lo inyecta automáticamente en la cabecera `Authorization` de todas las peticiones salientes.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/frontend/iam_bc_class_diagram/interfaces-iam.svg" alt="Frontend IAM Interface Layer Class Diagram" width="750">
</p>

#### 4.3.1.3. Application Layer

Orquesta los casos de uso específicos del contexto de autenticación, interactuando con los contratos definidos en el dominio.

*   **AuthCommandServiceImpl:** Implementación del servicio de comandos de autenticación. Coordina la validación, la llamada a la pasarela de autenticación (`AuthGateway`), y el almacenamiento seguro de los tokens.
*   **AuthQueryServiceImpl:** Implementación del servicio de consultas encargado de verificar los tokens JWT.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/frontend/iam_bc_class_diagram/application-iam.svg" alt="Frontend IAM Application Layer Class Diagram" width="750">
</p>

#### 4.3.1.4. Infrastructure Layer

Proporciona la implementación concreta de los contratos del dominio a través del consumo de servicios web e interacción con la memoria persistente del navegador.

*   **AuthHttpGateway:** Adaptador que realiza las llamadas HTTP usando Angular `HttpClient` hacia el servicio IAM de la API de Clair.
*   **LocalTokenStorageGateway:** Implementación concreta encargada de guardar y leer los tokens usando la API de `LocalStorage` del navegador.
*   **AuthResponseResource:** Recurso DTO que modela el cuerpo de respuesta de la API que incluye el accessToken y refreshToken.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/frontend/iam_bc_class_diagram/infrastructure-iam.svg" alt="Frontend IAM Infrastructure Layer Class Diagram" width="750">
</p>

#### 4.3.1.5. Bounded Context Software Architecture Code Level Diagrams

El diagrama de clases unificado del contexto acotado de Identity & Access Management (IAM) muestra la relación entre todas sus entidades, value objects, servicios y adaptadores de interfaz e infraestructura:

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/frontend/iam_bc_class_diagram/diagram.svg" alt="Unified Web App IAM Class Diagram" width="850">
</p>

### 4.3.2. Bounded Context: Billing

#### 4.3.2.1. Domain Layer

Define las entidades financieras, planes y contratos de servicios para la suscripción a Clair Premium.

*   **UserPlan (Entity):** Entidad que representa la suscripción activa del usuario con su respectivo `UserId` y `PlanType`.
*   **PaymentIntent (Entity):** Modela la intención de pago generada por Stripe (`clientSecret`).
*   **PlanType (Enum):** Enumerador de planes soportados por la aplicación (`FREE`, `PREMIUM`).
*   **BillingCommandService / BillingQueryService (Interfaces):** Contratos del dominio para ejecutar pagos y consultar claves o planes de usuario.
*   **BillingGateway (Interface):** Contrato para el envío de datos de pago e integración del checkout.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/frontend/billing_bc_class_diagram/domain-billing.svg" alt="Frontend Billing Domain Layer Class Diagram" width="750">
</p>

#### 4.3.2.2. Interface Layer

Contiene los componentes visuales interactivos y los servicios de transformación de datos para los flujos de pago.

*   **SelectPlanComponent:** Vista de selección de planes (Free vs Premium).
*   **PremiumCheckoutComponent:** Componente que controla el proceso de pago, interactúa con Stripe Elements y despacha la confirmación de la transacción.
*   **PaymentModalComponent:** Modal interactivo encargado de instanciar de forma segura las pasarelas del lado del cliente.
*   **BillingTransform (Service):** Servicio encargado de mapear los datos JSON de la infraestructura (`PaymentIntentResource`) a los modelos del dominio (`PaymentIntent`).

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/frontend/billing_bc_class_diagram/interfaces-billing.svg" alt="Frontend Billing Interface Layer Class Diagram" width="750">
</p>

#### 4.3.2.3. Application Layer

Encapsula la lógica de orquestación para la generación de intentos de pago e información del plan asignado.

*   **BillingCommandServiceImpl:** Implementa la orquestación necesaria para el inicio del proceso de facturación creando un `PaymentIntent` a través del gateway.
*   **BillingQueryServiceImpl:** Maneja las consultas de planes activos y obtención segura de credenciales de plataformas terceras (Stripe Public Key).

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/frontend/billing_bc_class_diagram/application-billing.svg" alt="Frontend Billing Application Layer Class Diagram" width="750">
</p>

---

#### 4.3.2.4. Infrastructure Layer

Implementa las pasarelas de red utilizando la infraestructura Angular HTTP para comunicarse con el servidor y Stripe.

*   **BillingHttpGateway:** Implementa `BillingGateway` conectando la aplicación con el backend de Clair y recuperando las claves necesarias de Stripe.
*   **PaymentIntentResource:** DTO que define la estructura JSON de la intención de pago recibida de la API.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/frontend/billing_bc_class_diagram/infrastructure-billing.svg" alt="Frontend Billing Infrastructure Layer Class Diagram" width="750">
</p>

#### 4.3.2.5. Bounded Context Software Architecture Code Level Diagrams

El diagrama de clases unificado del contexto acotado de Billing muestra la relación entre todas sus entidades, value objects, servicios y adaptadores de interfaz e infraestructura:

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/frontend/billing_bc_class_diagram/diagram.svg" alt="Unified Web App Billing Class Diagram" width="850">
</p>

---

### 4.3.3. Bounded Context: Devices & Space Management

#### 4.3.3.1. Domain Layer

Define la estructura organizativa de la solución y las identidades de negocio de los sensores, actuadores y espacios.

*   **Organization (Entity):** Entidad que representa la organización dueña del espacio.
*   **Space (Entity):** Entidad que modela un entorno físico específico (oficina, sala, etc.).
*   **Device (Entity):** Modela el sensor físico y su estado actual (`serialNumber`, `hardwareId`, `status`).
*   **DeviceCommandService (Interface):** Contrato para manejar los comandos de emparejamiento (`PairDevice`) e inscripción (`ClaimDevice`).
*   **DeviceThresholdCommandService (Interface):** Contrato para actualizar la configuración de umbrales en un sensor específico.
*   **DeviceGateway (Interface):** Contrato para comunicarse con servicios de hardware y backend de control.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/frontend/devices_bc_class_diagram/domain-devices.svg" alt="Frontend Devices Domain Layer Class Diagram" width="750">
</p>

#### 4.3.3.2. Interface Layer

Contiene los componentes y mappers que exponen la configuración y el listado de dispositivos asignados a los espacios.

*   **SpaceDevicesPage:** Página Angular que muestra los dispositivos de un espacio y permite reclamar uno nuevo mediante `onClaimDevice()`.
*   **DeviceTransform:** Servicio encargado de mapear y formatear las respuestas de la API (`DeviceResource`) hacia las entidades de negocio (`Device`).
*   **DeviceContextFacade (Facade):** Fachada expuesta para permitir que otros Bounded Contexts consulten datos rápidos de un dispositivo de manera desacoplada.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/frontend/devices_bc_class_diagram/interfaces-devices.svg" alt="Frontend Devices Interface Layer Class Diagram" width="750">
</p>

#### 4.3.3.3. Application Layer

Orquesta los casos de uso para aprovisionamiento, emparejamiento de hardware y establecimiento de umbrales físicos del dispositivo.

*   **DeviceCommandServiceImpl:** Implementa y gestiona el registro de organizaciones y el proceso de reclamo de dispositivos (`handleClaimDevice`).
*   **DeviceQueryServiceImpl:** Orquesta las consultas para listar los sensores pertenecientes a una sala específica.
*   **DeviceThresholdCommandServiceImpl:** Gestiona la creación y modificación de umbrales recomendados por sensor.
*   **DeviceThresholdQueryServiceImpl:** Obtiene las configuraciones de alerta recomendadas de calidad de aire para un dispositivo determinado.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/frontend/devices_bc_class_diagram/application-devices.svg" alt="Frontend Devices Application Layer Class Diagram" width="750">
</p>

#### 4.3.3.4. Infrastructure Layer

Proporciona la conectividad física de red con el API de Clair e implementa los adaptadores HTTP.

*   **DeviceHttpGateway:** Adaptador que implementa la pasarela de dispositivos (`DeviceGateway`) usando el cliente HTTP de Angular para persistir cambios y emparejar.
*   **DeviceThresholdHttpGateway:** Adaptador específico encargado del canal de comunicación de umbrales de alerta del hardware.
*   **DeviceResource:** DTO que modela el JSON enviado/recibido para dispositivos en la API de Clair.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/frontend/devices_bc_class_diagram/infrastructure-devices.svg" alt="Frontend Devices Infrastructure Layer Class Diagram" width="750">
</p>

#### 4.3.3.5. Bounded Context Software Architecture Code Level Diagrams

El diagrama de clases unificado del contexto acotado de Device & Space Management muestra la relación entre todas sus entidades, value objects, servicios y adaptadores de interfaz e infraestructura:

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/frontend/devices_bc_class_diagram/diagram.svg" alt="Unified Web App Devices Class Diagram" width="850">
</p>

---

### 4.3.4. Bounded Context: Air Quality Evaluation

#### 4.3.4.1. Domain Layer

Modeliza la lógica y las métricas de evaluación ambiental del aire, procesando el estado de salubridad y la telemetría histórica.

*   **TelemetryEvaluation (Entity):** Representa el resultado detallado del análisis de calidad del aire para un dispositivo, consolidando métricas como material particulado (`ParticulateMatter`), calidad general (`AirQuality`), conectividad (`Connectivity`), y estado general de salud del ambiente (`healthStatus`).
*   **TelemetryEvaluationCommandService / TelemetryEvaluationQueryService (Interfaces):** Contratos del dominio para despachar solicitudes de evaluación y consultar históricos de mediciones.
*   **TelemetryEvaluationGateway (Interface):** Contrato que especifica el envío de telemetría a evaluar y la recuperación de reportes agregados.
*   **EvaluateTelemetryCommand / GetEvaluationsByDeviceQuery (Value Objects):** Comandos y consultas inmutables que encapsulan parámetros de dispositivo y paginación.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/frontend/evaluation_bc_class_diagram/domain-evaluation.svg" alt="Frontend Evaluation Domain Layer Class Diagram" width="750">
</p>

#### 4.3.4.2. Interface Layer

Contiene las interfaces y transformadores que comunican el contexto de evaluación de telemetría con el resto de la aplicación y componentes visuales.

*   **EvaluationContextFacade (Facade):** Fachada de integración que permite a otros módulos del frontend consultar rápidamente la última lectura o estado de telemetría de un dispositivo sin acoplarse a los detalles del módulo de evaluación.
*   **TelemetryEvaluationTransform / EvaluateTelemetryTransform (Services):** Servicios mappers de Angular que traducen recursos JSON crudos de la infraestructura a entidades y comandos limpios de negocio.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/frontend/evaluation_bc_class_diagram/interfaces-evaluation.svg" alt="Frontend Evaluation Interface Layer Class Diagram" width="750">
</p>

#### 4.3.4.3. Application Layer

Encapsula los servicios encargados de la coordinación de la lógica de evaluación en tiempo real y consultas del histórico de sensores.

*   **TelemetryEvaluationCommandServiceImpl:** Orquesta el flujo de evaluación enviando nuevas cargas de telemetría a procesar junto con la firma del API Key.
*   **TelemetryEvaluationQueryServiceImpl:** Implementa la lógica para retornar listados paginados de telemetrías y la consulta en tiempo real del último estado reportado.
*   **EvaluationContextFacadeImpl:** Implementación de la fachada que delega al servicio de consultas para exponer la información de manera limpia a otros bounded contexts frontend.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/frontend/evaluation_bc_class_diagram/application-evaluation.svg" alt="Frontend Evaluation Application Layer Class Diagram" width="750">
</p>

#### 4.3.4.4. Infrastructure Layer

Proporciona los clientes HTTP y adaptadores que se conectan con los endpoints de evaluación ambiental en el Platform API.

*   **TelemetryEvaluationHttpGateway:** Implementación de `TelemetryEvaluationGateway` usando `HttpClient` de Angular para persistir telemetrías y leer evaluaciones estructuradas.
*   **TelemetryEvaluationResource / EvaluateTelemetryResource:** DTOs que modelan la estructura JSON para la entrada de datos brutos del sensor y la salida enriquecida con los umbrales e indicadores calculados.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/frontend/evaluation_bc_class_diagram/infrastructure-evaluation.svg" alt="Frontend Evaluation Infrastructure Layer Class Diagram" width="750">
</p>

#### 4.3.4.5. Bounded Context Software Architecture Code Level Diagrams

El diagrama de clases unificado del contexto acotado de Air Quality Evaluation muestra la relación entre todas sus entidades, value objects, servicios y adaptadores de interfaz e infraestructura:

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/frontend/evaluation_bc_class_diagram/diagram.svg" alt="Unified Web App Evaluation Class Diagram" width="850">
</p>

### 4.3.5. Bounded Context: Alerting & Response

#### 4.3.5.1. Domain Layer

Define las entidades y contratos para el procesamiento y catalogación de incidentes críticos y alertas ambientales.

*   **Alert (Entity):** Entidad principal que representa un incidente de seguridad ambiental. Contiene severidad (`AlertSeverity`), estado, mensaje e indicador temporal (`timestamp`).
*   **AlertSeverity (Enum):** Gravedad del incidente (`LOW`, `MEDIUM`, `HIGH`, `CRITICAL`).
*   **AlertQueryService (Interface):** Interfaz para consultar los incidentes y resúmenes diarios de alertas.
*   **AlertGateway (Interface):** Contrato para recuperar alertas desde la persistencia externa.
*   **GetAlertsQuery (Value Object):** Query que encapsula los parámetros de paginación para la lista de alertas.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/frontend/alerting_bc_class_diagram/domain-alerting.svg" alt="Frontend Alerting Domain Layer Class Diagram" width="750">
</p>

#### 4.3.5.2. Interface Layer

Contiene los componentes y fachadas de integración visual para desplegar las alertas en la interfaz de usuario.

*   **AlertsPageComponent:** Componente Angular contenedor que inicializa la carga de alertas activas del sistema.
*   **AlertCardComponent:** Componente visual reutilizable para mostrar detalles rápidos de una alerta específica.
*   **AlertTableComponent:** Tabla estructurada que renderiza colecciones de alertas con soporte para filtros de severidad y paginación.
*   **AlertTransform (Service):** Servicio encargado de traducir los registros crudos de respuesta JSON (`AlertResponseResource`) a la entidad `Alert`.
*   **AlertingContextFacade (Facade):** Fachada que expone métodos para que otros contextos consulten alertas activas por dispositivo.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/frontend/alerting_bc_class_diagram/interfaces-alerting.svg" alt="Frontend Alerting Interface Layer Class Diagram" width="750">
</p>

#### 4.3.5.3. Application Layer

Encapsula los servicios encargados de la orquestación para consultar la telemetría fuera de rango e incidentes generados.

*   **AlertQueryServiceImpl:** Servicio de aplicación que implementa la orquestación para recuperar alertas paginadas o generar resúmenes analíticos rápidos del día.
*   **AlertingContextFacadeImpl:** Implementación concreta de la fachada para el consumo de datos de alertas por otros módulos frontend.

    }
}

class AlertQueryService
class AlertingContextFacade
class AlertGateway
class AlertTransform
class GetAlertsQuery

AlertQueryServiceImpl ..|> AlertQueryService : implements
AlertingContextFacadeImpl ..|> AlertingContextFacade : implements
AlertQueryServiceImpl --> AlertGateway : uses
AlertQueryServiceImpl --> AlertTransform : uses
<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/frontend/alerting_bc_class_diagram/application-alerting.svg" alt="Frontend Alerting Application Layer Class Diagram" width="750">
</p>

---

#### 4.3.5.4. Infrastructure Layer

Proporciona los clientes HTTP adaptados a la API REST de alertas del Platform API.

*   **AlertHttpGateway:** Adaptador que implementa `AlertGateway` usando el cliente HTTP de Angular para realizar consultas paginadas e interactuar con la persistencia.
*   **AlertResponseResource:** DTO que modela el recurso JSON de respuesta de una alerta de la API.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/frontend/alerting_bc_class_diagram/infrastructure-alerting.svg" alt="Frontend Alerting Infrastructure Layer Class Diagram" width="750">
</p>

#### 4.3.5.5. Bounded Context Software Architecture Code Level Diagrams

El diagrama de clases unificado del contexto acotado de Alerting & Response muestra la relación entre todas sus entidades, value objects, servicios y adaptadores de interfaz e infraestructura:

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/frontend/alerting_bc_class_diagram/diagram.svg" alt="Unified Web App Alerting Class Diagram" width="850">
</p>

---

### 4.3.6. Bounded Context: Analytics & Reporting

#### 4.3.6.1. Domain Layer

Define la representación lógica de las tendencias temporales y las métricas resumidas que consumen los dashboards de Clair.

*   **Trend (Entity):** Modela el comportamiento histórico de una métrica física a lo largo del tiempo (marcas temporales, valores leídos y tipo de métrica).
*   **AnalyticsOverview (Entity):** Estructura consolidada que expone el Índice de Calidad del Aire (ICA/AQI) promedio y el contador de incidentes activos para el dashboard general.
*   **AnalyticsQueryService / AnalyticsOverviewQueryService (Interfaces):** Contratos para las búsquedas de series temporales y visualización de paneles agregados.
*   **AnalyticsGateway (Interface):** Contrato que abstrae el origen de datos históricos y analíticos.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/frontend/analytics_bc_class_diagram/domain-analytics.svg" alt="Frontend Analytics Domain Layer Class Diagram" width="750">
</p>

#### 4.3.6.2. Interface Layer

Contiene los controladores de gráficos e indicadores interactivos para el análisis retrospectivo en la interfaz de usuario.

*   **AnalyticsPageComponent:** Componente Angular para el análisis avanzado y filtrado de series de telemetría.
*   **OverviewPageComponent:** Componente principal que sirve como panel de control resumen del establecimiento monitoreado.
*   **TrendChartCardComponent:** Tarjeta visual que dibuja y renderiza gráficos interactivos de líneas basados en las tendencias de `Trend`.
*   **AqiGaugeCardComponent:** Indicador visual tipo velocímetro para mostrar de manera instantánea el nivel de AQI calculado.
*   **AnalyticsTransform (Service):** Servicio encargado de traducir los datos agregados a los modelos de dominio.
*   **AnalyticsContextFacade (Facade):** Fachada de integración para que otros contextos recuperen las métricas rápidas de los dashboards.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/frontend/analytics_bc_class_diagram/interfaces-analytics.svg" alt="Frontend Analytics Interface Layer Class Diagram" width="750">
</p>

#### 4.3.6.3. Application Layer

Orquesta los flujos de consulta de series históricas y agregaciones requeridos por los componentes visuales.

*   **AnalyticsQueryServiceImpl:** Implementación del servicio de aplicación que gestiona la recuperación de tendencias históricas de los sensores.
*   **AnalyticsOverviewQueryServiceImpl:** Orquesta el cálculo y agregación rápidos de alertas y calidad de aire para construir el resumen global.
*   **AnalyticsContextFacadeImpl:** Implementación concreta de la fachada expuesta hacia el exterior del módulo analítico.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/frontend/analytics_bc_class_diagram/application-analytics.svg" alt="Frontend Analytics Application Layer Class Diagram" width="750">
</p>

---

#### 4.3.6.4. Infrastructure Layer

Adaptadores que conectan con la base de datos de telemetrías agregadas a través de la API REST de Clair.

*   **AnalyticsHttpGateway:** Adapter concreto que implementa `AnalyticsGateway` consumiendo los recursos analíticos mediante Angular `HttpClient`.
*   **TrendsResource / AnalyticsOverviewResource:** DTOs que mapean los JSON de respuestas estructuradas con tendencias y totales.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/frontend/analytics_bc_class_diagram/infrastructure-analytics.svg" alt="Frontend Analytics Infrastructure Layer Class Diagram" width="750">
</p>

#### 4.3.6.5. Bounded Context Software Architecture Code Level Diagrams

El diagrama de clases unificado del contexto acotado de Analytics & Reporting muestra la relación entre todas sus entidades, value objects, servicios y adaptadores de interfaz e infraestructura:

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/frontend/analytics_bc_class_diagram/diagram.svg" alt="Unified Web App Analytics Class Diagram" width="850">
</p>

---

### 4.3.7. Bounded Context: Notifications

#### 4.3.7.1. Domain Layer

Define la estructura de logs de auditoría de mensajes enviados y los contratos para recuperar el historial de notificaciones.

*   **PushNotificationLog (Entity):** Entidad de dominio que representa una notificación enviada (identificador, título, cuerpo del mensaje, y fecha de despacho `sentAt`).
*   **NotificationQueryService (Interface):** Contrato para el control del caso de uso de lectura del historial de notificaciones.
*   **NotificationGateway (Interface):** Contrato que abstrae las llamadas de infraestructura para recuperar el listado.
*   **GetPushNotificationsQuery (Value Object):** Query inmutable que encapsula las opciones de paginación para la lista de notificaciones.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/frontend/notifications_bc_class_diagram/domain-notifications.svg" alt="Frontend Notifications Domain Layer Class Diagram" width="750">
</p>

#### 4.3.7.2. Interface Layer

Contiene los adaptadores y fachadas que permiten a otras partes de la UI interactuar con la bandeja de entrada de notificaciones push.

*   **NotificationsContextFacade (Facade):** Fachada que expone el método `getPushNotifications(page, size)` permitiendo un desacoplamiento directo con otros módulos de la app web.
*   **PushNotificationTransform (Service):** Servicio encargado de transformar DTOs de infraestructura (`PushNotificationLogResource`) a entidades del negocio (`PushNotificationLog`).

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/frontend/notifications_bc_class_diagram/interfaces-notifications.svg" alt="Frontend Notifications Interface Layer Class Diagram" width="750">
</p>

#### 4.3.7.3. Application Layer

Encapsula la orquestación para recuperar los mensajes push del usuario autenticado.

*   **NotificationQueryServiceImpl:** Servicio de aplicación que delega en el gateway para consultar y transformar la colección de alertas enviadas.
*   **NotificationsContextFacadeImpl:** Fachada concreta que orquesta la llamada asíncrona hacia el servicio de consultas de aplicación.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/frontend/notifications_bc_class_diagram/application-notifications.svg" alt="Frontend Notifications Application Layer Class Diagram" width="750">
</p>

---

#### 4.3.7.4. Infrastructure Layer

Adaptadores que consultan el historial de notificaciones registrado en el servidor de Clair.

*   **NotificationHttpGateway:** Implementación concreta del gateway utilizando `HttpClient` de Angular para obtener el log.
*   **PushNotificationLogResource:** DTO que mapea el recurso JSON del log de notificaciones desde el API backend.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/frontend/notifications_bc_class_diagram/infrastructure-notifications.svg" alt="Frontend Notifications Infrastructure Layer Class Diagram" width="750">
</p>

#### 4.3.7.5. Bounded Context Software Architecture Code Level Diagrams

El diagrama de clases unificado del contexto acotado de Notifications muestra la relación entre todas sus entidades, value objects, servicios y adaptadores de interfaz e infraestructura:

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/frontend/notifications_bc_class_diagram/diagram.svg" alt="Unified Web App Notifications Class Diagram" width="850">
</p>

---


## 4.4. Tactical-Level Domain-Driven Design -  Mobile application

La aplicación móvil se ha desarrollado utilizando Flutter y sigue los principios del Diseño Guiado por el Dominio (DDD) estructurado bajo una arquitectura limpia adaptada para dispositivos móviles. Esto garantiza una separación clara de responsabilidades, facilitando el mantenimiento y testeo de la lógica de negocio independientemente de los detalles del framework UI o la persistencia local. A continuación, se detallan los contextos acotados implementados en el aplicativo móvil:

**Arquitectura de Componentes de la Aplicación Móvil (Flutter Mobile App)**

A continuación se detalla el diagrama C4 de nivel de Componentes para la aplicación móvil de Clair, ilustrando la organización interna de los Bounded Contexts y cómo interactúan las capas de interfaces, aplicación, dominio e infraestructura en Flutter:

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/c4/containers/mobile/MobileAppComponents-dark.svg" alt="Mobile Application Component Architecture Diagram" width="850">
</p>

*   **Interfaces Layer (Capa de Interfaces/Presentación):** Contiene las vistas móviles (Widgets, Screens, Buttons, Forms), servicios de control de UI (Cubit / BLoC Presenters) y los estados asociados que administran la interacción reactiva con el usuario.
*   **Application Layer (Capa de Aplicación):** Implementa la orquestación de casos de uso (servicios de aplicación, mapeo de consultas y comandos). Recibe flujos del presenter y delega la lógica y consulta al dominio y a las pasarelas.
*   **Domain Layer (Capa de Dominio):** El corazón puro del negocio móvil. Contiene las entidades, value objects, interfaces de repositorios/gateways, contratos de servicios de comandos y consultas que operan agnósticos al framework de Flutter.
*   **Infrastructure Layer (Capa de Infraestructura):** Encargada de interactuar con el entorno físico e interfaces de comunicación. Contiene las pasarelas HTTP (usando `Dio`), persistencia local en memoria o base de datos móvil (Secure Storage, Hive o SQLite) y el kernel de infraestructura local.

### 4.4.1. Bounded Context: Identity & Access Management (IAM)

#### 4.4.1.1. Domain Layer

Define los contratos de negocio puros, comandos y consultas que modelan las reglas de registro y acceso de usuarios de la aplicación móvil.

*   **AuthenticationCommandService (Interface):** Interfaz del dominio que declara las firmas para iniciar registro, confirmar, iniciar sesión (tradicional/Google), cerrar sesión y refrescar tokens.
*   **AuthenticationQueryService (Interface):** Interfaz para consultar los datos del usuario autenticado en la sesión activa.
*   **InitiateRegistrationCommand / ConfirmRegistrationCommand / SignInCommand (Value Objects):** Comandos inmutables que encapsulan las credenciales y datos requeridos para los casos de uso correspondientes.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/mobile/iam_class_diagram/domain-layer.svg" alt="Mobile IAM Domain Layer Class Diagram" width="750">
</p>

#### 4.4.1.2. Interface Layer

Implementa la gestión de estado reactiva en Flutter mediante el patrón **BLoC / Cubit**, capturando eventos de UI y exponiendo estados al árbol de widgets.

*   **LoginCubit:** Controla el estado del formulario de login y despacha peticiones de acceso tradicional o autenticación mediante Google.
*   **RegisterCubit:** Cubit encargado de gestionar la entrada de datos para la creación de cuentas de usuario.
*   **ConfirmRegistrationCubit:** Controla la interfaz de ingreso del código OTP para completar el alta del usuario.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/mobile/iam_class_diagram/interfaces-layer.svg" alt="Mobile IAM Interface Layer Class Diagram" width="750">
</p>

#### 4.4.1.3. Application Layer

Orquesta los flujos de autenticación e interactúa de forma desacoplada con el dominio, las pasarelas de red y persistencia local del dispositivo móvil.

*   **AuthenticationCommandServiceImpl:** Coordina las transacciones de registro e inicio de sesión. Gestiona el guardado seguro de JWTs en base a las respuestas de la pasarela y la manipulación de estados de sesión.
*   **AuthenticationQueryServiceImpl:** Orquesta la recuperación asíncrona de los datos del perfil del usuario activo.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/mobile/iam_class_diagram/application-layer.svg" alt="Mobile IAM Application Layer Class Diagram" width="750">
</p>

#### 4.4.1.4. Infrastructure Layer

Proporciona los adaptadores concretos para la persistencia del almacenamiento local y la comunicación de red con el API de Clair mediante clientes HTTP.

*   **AuthenticationGateway (Interface) / AuthenticationHttpGateway:** Define y realiza las llamadas HTTP usando la librería `Dio` para consumir los endpoints de registro, sesión y refresco.
*   **TokenLocalStorage:** Administra de forma persistente y segura los tokens en el dispositivo utilizando almacenamiento local.
*   **RegistrationSessionLocalStorage:** Almacena temporalmente el ID de sesión del registro mientras se completa la verificación por OTP.
*   **GoogleIdTokenProvider (Interface) / GoogleSignInIdTokenProvider:** Adaptador que envuelve la integración nativa con el plugin de terceros `google_sign_in` para obtener el ID Token.
*   **AuthSession:** Singleton reactivo en memoria que guarda el estado de autenticación actual del usuario.
<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/mobile/iam_class_diagram/infrastructure-layer.svg" alt="Mobile IAM Infrastructure Layer Class Diagram" width="750">
</p>

#### 4.4.1.5. Bounded Context Software Architecture Code Level Diagrams

El diagrama de clases unificado del contexto acotado de Identity & Access Management (IAM) muestra la relación entre todas sus entidades, value objects, servicios y adaptadores de interfaz e infraestructura:

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/mobile/iam_class_diagram/unified.svg" alt="Unified Mobile IAM Class Diagram" width="850">
</p>

### 4.4.2. Bounded Context: Device & Space Management

#### 4.4.2.1. Domain Layer

Define la representación de lectura de dispositivos (`Read Models`), identificadores de negocio y los contratos de servicios de telemetría y aprovisionamiento.

*   **DeviceReadModel:** Modelo de lectura optimizado para vistas que representa el estado consolidado de un sensor o extractor.
*   **DevicesCommandService / DevicesQueryService (Interfaces):** Contratos del dominio para manejar acciones de emparejamiento, renombrado, desvinculación y listado de dispositivos.
*   **DeviceId / DeviceName (Value Objects):** Envolturas tipadas inmutables para la identidad y nombres de dispositivos.
*   **PairDeviceCommand / GetDeviceByIdQuery (Value Objects):** DTOs que encapsulan parámetros de llamadas de comandos y consultas.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/mobile/devices_class_diagram/domain-layer.svg" alt="Mobile Devices Domain Layer Class Diagram" width="750">
</p>

#### 4.4.2.2. Interface Layer

Maneja los estados reactivos de la vista de detalle de sensores utilizando BLoC/Cubit y expone ViewModels adaptados a las necesidades de la UI de Flutter.

*   **DeviceDetailCubit:** Cubit encargado de orquestar la carga inicial del dispositivo, modificación de nombres, desvinculación física, y apagado o encendido.
*   **DeviceDetailState:** Representación inmutable del estado visual que detalla la carga de telemetrías y errores.
*   **DeviceDetailViewModel:** Modelo de vista adaptado que expone datos consolidados sobre potencia, conectividad (dBm), salud general (%) y umbrales activos del sensor.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/mobile/devices_class_diagram/interfaces-layer.svg" alt="Mobile Devices Interface Layer Class Diagram" width="750">
</p>

#### 4.4.2.3. Application Layer

Orquesta los casos de uso principales para el registro y modificación de dispositivos, además de servir como capa de control anticorrupción (ACL).

*   **DevicesCommandServiceImpl:** Ejecuta comandos de vinculación física, renombrado y baja de dispositivos interactuando con las pasarelas.
*   **DevicesQueryServiceImpl:** Ejecuta la recuperación y mapeo de dispositivos filtrados por espacios físicos.
*   **DeviceVitalsAcl (Anti-Corruption Layer):** Componente ACL que conecta de forma segura con el contexto de evaluación de telemetría (`TelemetryEvaluationQueryService`) para construir resúmenes rápidos de estado de hardware (`DeviceVitalsSnapshot`) sin contaminar el dominio de dispositivos.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/mobile/devices_class_diagram/application-layer.svg" alt="Mobile Devices Application Layer Class Diagram" width="750">
</p>

---

#### 4.4.2.4. Infrastructure Layer

Contiene los contratos crudos y adaptadores HTTP mediante la biblioteca `Dio` para interactuar con los servicios REST del backend.

*   **DevicesGateway (Interface) / DevicesHttpGateway:** Adaptador físico encargado de codificar los cuerpos de solicitud y parsear las respuestas crudas en mapas asociativos (`Map`) para el registro y borrado de sensores.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/mobile/devices_class_diagram/infrastructure-layer.svg" alt="Mobile Devices Infrastructure Layer Class Diagram" width="750">
</p>

#### 4.4.2.5. Bounded Context Software Architecture Code Level Diagrams

El diagrama de clases unificado del contexto acotado de Device & Space Management muestra la relación entre todas sus entidades, value objects, servicios y adaptadores de interfaz e infraestructura:

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/mobile/devices_class_diagram/unified.svg" alt="Unified Mobile Devices Class Diagram" width="850">
</p>

---


### 4.4.3. Bounded Context: Air Quality Evaluation

#### 4.4.3.1. Domain Layer

Encapsula los modelos de lectura y contratos para obtener las lecturas de telemetría procesadas por el motor de calidad de aire.

*   **TelemetryEvaluationReadModel:** Modelo de lectura para representar el estado de salubridad y métricas físicas de conectividad y uptime ambiental.
*   **Connectivity (Value Object):** Objeto de valor que detalla el estado del enlace inalámbrico, red y nivel de señal (dBm) del sensor.
*   **TelemetryEvaluationQueryService (Interface):** Interfaz del dominio que declara la firma para recuperar la última telemetría del hardware.
*   **GetLatestTelemetryEvaluationByDeviceQuery / EvaluationDeviceId (Value Objects):** Parámetros para la ejecución de la consulta.


classDiagram
namespace domain {
<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/mobile/evaluation_class_diagram/domain-layer.svg" alt="Mobile Evaluation Domain Layer Class Diagram" width="750">
</p>

---

#### 4.4.3.2. Interface Layer

*(Nota: En la aplicación móvil, este contexto no expone pantallas o Cubits independientes. Su representación visual se integra directamente en las vistas del contexto de Dispositivos a través de la capa de adaptación o control anticorrupción).*

*   **TelemetryEvaluationResponseResource:** DTO del lado del cliente que expone los datos serializados del backend.
*   **ConnectivityResource:** DTO que mapea el estado de red de la infraestructura.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/mobile/evaluation_class_diagram/interfaces-layer.svg" alt="Mobile Evaluation Interface Layer Class Diagram" width="750">
</p>

---

#### 4.4.3.3. Application Layer

Orquesta las consultas relativas a las últimas métricas capturadas por el dispositivo.

*   **TelemetryEvaluationQueryServiceImpl:** Servicio de aplicación que delega en el gateway la obtención física de la telemetría calculada y la mapea a los modelos de dominio.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/mobile/evaluation_class_diagram/application-layer.svg" alt="Mobile Evaluation Application Layer Class Diagram" width="750">
</p>

---

#### 4.4.3.4. Infrastructure Layer

Maneja la serialización y la interacción HTTP para las solicitudes de telemetría ambiental procesada.

*   **TelemetryEvaluationGateway (Interface) / TelemetryEvaluationHttpGateway:** Define e implementa las peticiones HTTP con la biblioteca `Dio` para recuperar la última lectura de telemetría del sensor.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/mobile/evaluation_class_diagram/infrastructure-layer.svg" alt="Mobile Evaluation Infrastructure Layer Class Diagram" width="750">
</p>

#### 4.4.3.5. Bounded Context Software Architecture Code Level Diagrams

El diagrama de clases unificado del contexto acotado de Air Quality Evaluation muestra la relación entre todas sus entidades, value objects, servicios y adaptadores de interfaz e infraestructura:

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/mobile/evaluation_class_diagram/unified.svg" alt="Unified Mobile Evaluation Class Diagram" width="850">
</p>

---

### 4.4.4. Bounded Context: Alerting & Response

#### 4.4.4.1. Domain Layer

Define las entidades centrales de los incidentes y los servicios para consultar resúmenes agregados e históricos de alertas en el dispositivo.

*   **Alert:** Entidad del dominio que encapsula las propiedades de la alerta (identificador, tipo de métrica, valor disparado, valor del umbral y estado de la alerta).
*   **AlertStatus (Enum):** Representa el estado del ciclo de vida del incidente (`active`, `acknowledged`, `resolved`).
*   **MetricType (Enum):** Enumerador de las variables físicas que disparan alertas (`pm25`, `co2`, `temperature`, `humidity`).
*   **AlertsQueryService (Interface):** Contrato para el control del caso de uso de lectura de alertas por sensor o por establecimiento.
*   **AlertsCommandService (Interface):** Contrato para cambiar el estado de las alertas (reconocimiento o resolución).

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/mobile/alerts_class_diagram/domain-layer.svg" alt="Mobile Alerts Domain Layer Class Diagram" width="750">
</p>

---

#### 4.4.4.2. Interface Layer

Implementa la captura de eventos visuales y la administración de estados del panel de alertas utilizando el patrón BLoC/Cubit.

*   **AlertsCubit:** Componente reactivo encargado de despachar búsquedas filtradas por estado, tipo de métrica o espacio, además de controlar la paginación de los históricos.
*   **AlertsState:** Representa el estado actual de la UI (cargando, errores, página activa de alertas, resumen diario).
*   **AlertTab / AlertViewMode (Enums):** Enumerados que definen las pestañas de visualización (activas vs históricas) y modos de grilla o lista.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/mobile/alerts_class_diagram/interfaces-layer.svg" alt="Mobile Alerts Interface Layer Class Diagram" width="750">
</p>

---

#### 4.4.4.3. Application Layer

Orquesta la lógica de aplicación para la gestión y consulta de incidentes y conteos diarios de telemetrías fuera de rango.

*   **AlertsQueryServiceImpl:** Orquestador de la lógica de aplicación que interactúa con la pasarela de alertas para obtener los datos mapeados a entidades de dominio.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/mobile/alerts_class_diagram/application-layer.svg" alt="Mobile Alerts Application Layer Class Diagram" width="750">
</p>

---

#### 4.4.4.4. Infrastructure Layer

Proporciona el adaptador HTTP concreto para consumir la API de alertas de Clair.

*   **AlertsGateway (Interface) / AlertsHttpGateway:** Pasarela física y su implementación concreta mediante `Dio` para realizar las llamadas HTTP para obtener alertas y resúmenes analíticos.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/mobile/alerts_class_diagram/infrastructure-layer.svg" alt="Mobile Alerts Infrastructure Layer Class Diagram" width="750">
</p>

#### 4.4.4.5. Bounded Context Software Architecture Code Level Diagrams

El diagrama de clases unificado del contexto acotado de Alerting & Response muestra la relación entre todas sus entidades, value objects, servicios y adaptadores de interfaz e infraestructura:

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/mobile/alerts_class_diagram/unified.svg" alt="Unified Mobile Alerts Class Diagram" width="850">
</p>

### 4.4.5. Bounded Context: Analytics & Reporting

#### 4.4.5.1. Domain Layer

Define la representación de datos analíticos, índices de calidad y contratos de consulta para series de datos históricos y transmisiones de telemetría en tiempo real.

*   **DashboardMetrics:** Entidad de dominio que consolida métricas ambientales en tiempo real (`Aqi`, `CO2`, `PM2.5`, temperatura, humedad) e indica deltas comparativos de comportamiento.
*   **LiveTelemetry:** Modelo de dominio para representar la telemetría en tiempo real transmitida mediante flujos de datos asíncronos (`Streams`).
*   **TrendPoint / Aqi / MetricDelta (Value Objects):** Objetos de valor que describen puntos de tendencia histórica, valores de ICA y variaciones en las lecturas de los sensores.
*   **AnalyticsQueryService (Interface):** Contrato que declara la firma para recuperar dashboards analíticos, tendencias históricas y flujos en tiempo real.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/mobile/analytics_class_diagram/domain-layer.svg" alt="Mobile Analytics Domain Layer Class Diagram" width="750">
</p>

---

#### 4.4.5.2. Interface Layer

Implementa componentes reactivos y controladores mediante Cubit para gestionar la carga de opciones, filtros de fechas y renderizado de telemetría viva.

*   **AnalyticsCubit:** Cubit encargado de controlar los ciclos de refresco de datos, iniciar o detener la escucha de telemetría viva mediante suscripciones a streams (`StreamSubscription`) y reaccionar ante cambios en los filtros de organizaciones, espacios y sensores.
*   **AnalyticsState:** Almacena el estado inmutable de los listados cargados, opciones seleccionadas y los datos calculados de tendencias y tiempo real.
*   **AnalyticsSelectOption:** Estructura para almacenar las opciones seleccionadas en los menús desplegables de la interfaz.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/mobile/analytics_class_diagram/interfaces-layer.svg" alt="Mobile Analytics Interface Layer Class Diagram" width="750">
</p>

---

#### 4.4.5.3. Application Layer

Orquesta los servicios de aplicación encargados de recuperar la información consolidada de los sensores y retornar flujos reactivos de datos.

*   **AnalyticsQueryServiceImpl:** Implementa el servicio de consultas de aplicación mapeando los resultados de infraestructura hacia modelos del dominio y controlando la conversión asíncrona de telemetrías.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/mobile/analytics_class_diagram/application-layer.svg" alt="Mobile Analytics Application Layer Class Diagram" width="750">
</p>

---

#### 4.4.5.4. Infrastructure Layer

Maneja los adaptadores concretos para interactuar con la API REST y las tecnologías de transmisión asíncrona del backend.

*   **AnalyticsGateway (Interface) / AnalyticsHttpGateway:** Contrato de red y su adaptador que utiliza `Dio` y `TokenLocalStorage` para realizar peticiones autenticadas hacia el API de Clair, transformando respuestas JSON crudas a modelos y mapeando transmisiones en tiempo real.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/mobile/analytics_class_diagram/infrastructure-layer.svg" alt="Mobile Analytics Infrastructure Layer Class Diagram" width="750">
</p>

#### 4.4.5.5. Bounded Context Software Architecture Code Level Diagrams

El diagrama de clases unificado del contexto acotado de Analytics & Reporting muestra la relación entre todas sus entidades, value objects, servicios y adaptadores de interfaz e infraestructura:

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/mobile/analytics_class_diagram/unified.svg" alt="Unified Mobile Analytics Class Diagram" width="850">
</p>

### 4.4.6. Bounded Context: Notifications

#### 4.4.6.1. Domain Layer

Define la estructura de logs de auditoría de mensajes enviados, objetos de valor para identificación/paginación y los contratos para recuperar el historial de notificaciones push desde el móvil.

*   **NotificationLog (Entity):** Entidad de dominio que representa una notificación enviada (identificador, título, cuerpo del mensaje, estado de envío y fecha de despacho).
*   **NotificationId (Value Object):** Objeto de valor inmutable que encapsula el identificador único del log de notificación.
*   **NotificationPage (Value Object):** Estructura de valor que empaqueta una página de registros de notificaciones con metadata de paginación.
*   **GetNotificationsQuery (Value Object):** Consulta inmutable que encapsula las opciones de paginación para la lista de notificaciones.
*   **NotificationsQueryService (Interface):** Contrato que declara la firma del caso de uso de obtención de notificaciones, retornando un `Either` con el resultado.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/mobile/notifications_class_diagram/domain-layer.svg" alt="Mobile Notifications Domain Layer Class Diagram" width="750">
</p>

---

#### 4.4.6.2. Interface Layer

Implementa la gestión de estados interactivos para mostrar la bandeja de notificaciones push dentro de la aplicación móvil.

*   **NotificationsCubit (Cubit):** Controlador de estado que orquesta las llamadas a la carga, refresco y marca de lectura de notificaciones push.
*   **NotificationsState:** Representa el estado inmutable del feed de notificaciones (indicadores de carga, lista actual de `NotificationLog`, número de elementos no leídos y banderas de paginación).

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/mobile/notifications_class_diagram/interfaces-layer.svg" alt="Mobile Notifications Interface Layer Class Diagram" width="750">
</p>

---

#### 4.4.6.3. Application Layer

Orquesta la lógica del caso de uso para consultar el listado de alertas de forma asíncrona.

*   **NotificationsQueryServiceImpl:** Servicio de aplicación que implementa el contrato de consulta, interactuando con la pasarela de red para obtener el historial paginado.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/mobile/notifications_class_diagram/application-layer.svg" alt="Mobile Notifications Application Layer Class Diagram" width="750">
</p>

---

#### 4.4.6.4. Infrastructure Layer

Adaptadores concretos que gestionan el consumo de la API de Clair sobre el canal de red del móvil.

*   **NotificationsGateway (Interface):** Contrato de red requerido para recuperar el log de notificaciones.
*   **NotificationsHttpGateway:** Implementación concreta del gateway que realiza peticiones HTTP GET seguras mediante el cliente `Dio` para deserializar el recurso de red.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/mobile/notifications_class_diagram/infrastructure-layer.svg" alt="Mobile Notifications Infrastructure Layer Class Diagram" width="750">
</p>

#### 4.4.6.5. Bounded Context Software Architecture Code Level Diagrams

El diagrama de clases unificado del contexto acotado de Notifications muestra la relación entre todas sus entidades, value objects, servicios y adaptadores de interfaz e infraestructura:

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/mobile/notifications_class_diagram/unified.svg" alt="Unified Mobile Notifications Class Diagram" width="850">
</p>

## 4.5. Tactical-Level Domain-Driven Design - Edge station

La estación base local (Edge Station) está desarrollada en Python utilizando Flask, siguiendo principios de DDD y Arquitectura Limpia para coordinar las operaciones locales fuera de la nube, la comunicación directa con las estaciones embebidas (ESP32) mediante HTTP/REST, la persistencia local y la sincronización asíncrona hacia la nube mediante Apache Kafka. A continuación, se detallan los contextos acotados que estructuran la estación local:

**Arquitectura de Componentes de la Estación Base Local (Edge Station)**

A continuación se detalla el diagrama C4 de nivel de Componentes para la estación base local (Edge Station) de Clair, ilustrando la interacción de las capas de la aplicación desarrollada en Flask:

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/c4/containers/edge/EdgeStationComponents-dark.svg" alt="Edge Station Component Architecture Diagram" width="850">
</p>

*   **Interfaces Layer (Capa de Interfaces):** Expone los endpoints REST para interactuar de forma síncrona con los dispositivos embebidos y controladores locales, recibiendo telemetrías y entregando comandos.
*   **Application Layer (Capa de Aplicación):** Orquesta los flujos de control de las tareas locales (ingesta de telemetría, encolado de comandos, publicación de presencia y ejecución de tareas programadas en segundo plano).
*   **Domain Layer (Capa de Dominio):** Contiene la lógica central independiente del framework (entidades locales, value objects y las abstracciones de repositorio).
*   **Infrastructure Layer (Capa de Infraestructura):** Implementa el almacenamiento físico local (SQLite / ORM SQLAlchemy), la mensajería asíncrona hacia Kafka y la comunicación externa con Clair Core API en la nube.

### 4.5.1. Bounded Context: Identity & Access Management (IAM)

#### 4.5.1.1. Domain Layer

Define las entidades principales y las interfaces del repositorio que gobiernan el acceso local de dispositivos en el Edge.

*   **Device (Entity):** Representa el dispositivo local registrado en el Edge, con atributos como `device_id`, `hardware_id`, `api_key`, `status` y la marca de tiempo de última comunicación `last_seen_at`.
*   **AuthService (Domain Service):** Servicio encargado de validar las credenciales de un dispositivo contra sus datos registrados.
*   **DevicePresenceChangedEvent (Event):** Evento de dominio emitido cuando cambia el estado de conexión del dispositivo.
*   **DeviceRepositoryInterface (Interface):** Interfaz para consultar y actualizar la persistencia de los dispositivos en el Edge.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/edge/iam_class_diagram/domain-layer.svg" alt="Edge IAM Domain Layer Class Diagram" width="750">
</p>

---

#### 4.5.1.2. Interface Layer

Puntos de entrada HTTP que manejan las llamadas entrantes para validar y registrar la presencia de dispositivos periféricos.

*   **IamApi:** Expone las rutas HTTP/REST para autenticar solicitudes entrantes provenientes de las estaciones embebidas y actualizar su marca de última conexión.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/edge/iam_class_diagram/interfaces-layer.svg" alt="Edge IAM Interface Layer Class Diagram" width="750">
</p>

---

#### 4.5.1.3. Application Layer

Orquesta la lógica de autenticación y el rastreo asíncrono de presencia en segundo plano.

*   **AuthApplicationService:** Coordina la autenticación delegando la lógica al servicio del dominio y al repositorio.
*   **DevicePresenceApplicationService:** Gestiona el registro de presencia y publica las actualizaciones de conexión en Kafka.
*   **DevicePresenceMonitor:** Componente en segundo plano que vigila y marca los dispositivos inactivos como offline si superan el umbral de inactividad.
*   **KafkaPresencePublisher:** Publicador concreto encargado de despachar eventos de presencia hacia Apache Kafka.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/edge/iam_class_diagram/application-layer.svg" alt="Edge IAM Application Layer Class Diagram" width="750">
</p>

---

#### 4.5.1.4. Infrastructure Layer

Adaptadores concretos de base de datos relacional y mensajería para IAM en el Edge.

*   **DeviceRepository:** Implementación concreta del repositorio de persistencia local (ej. SQLite / SQLAlchemy).
*   **DeviceModel:** Modelo de base de datos relacional para la entidad Device.
*   **IamKafkaTopics:** Mapea los tópicos de Kafka configurados para IAM (`DEVICE_PRESENCE_CHANGED`).

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/edge/iam_class_diagram/infrastructure-layer.svg" alt="Edge IAM Infrastructure Layer Class Diagram" width="750">
</p>

#### 4.5.1.5. Bounded Context Software Architecture Code Level Diagrams

El diagrama de clases unificado del contexto acotado de Identity & Access Management (IAM) muestra la relación entre todas sus entidades, value objects, servicios y adaptadores de interfaz e infraestructura:

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/edge/iam_class_diagram/unified.svg" alt="Unified Edge IAM Class Diagram" width="850">
</p>

---

### 4.5.2. Bounded Context: Device & Space Management

#### 4.5.2.1. Domain Layer

Modela las telemetrías entrantes y los comandos de actuación generados en la nube para el control de los microcontroladores.

*   **DeviceTelemetry (Entity):** Representa el reporte consolidado de mediciones del ESP32.
*   **DeviceCommand (Entity):** Representa comandos de actuación dirigidos a las estaciones embebidas (estado, payload, marcas de tiempo de entrega y confirmación).
*   **OutboxEntry (Entity):** Registro del patrón Outbox para la entrega confiable de eventos de telemetría a la nube.
*   **DeviceTelemetryService:** Lógica del dominio para validar y construir reportes de telemetría a partir de payloads crudos.
*   **AirQuality / ParticulateMatter / Connectivity / Location / DeviceConnectionStatus (Value Objects):** Atributos inmutables de telemetría y estado.
*   **DeviceTelemetryRepositoryInterface / DeviceCommandRepositoryInterface / OutboxRepositoryInterface (Interfaces):** Contratos de persistencia.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/edge/device_class_diagram/domain-layer.svg" alt="Edge Device Domain Layer Class Diagram" width="750">
</p>

---

#### 4.5.2.2. Interface Layer

Endpoints expuestos al microcontrolador para reportar telemetrías y recuperar tareas de actuación.

*   **DeviceApi:** Endpoint REST para recibir telemetría de las estaciones embebidas, entregar comandos pendientes y recibir confirmaciones de ejecución de comandos.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/edge/device_class_diagram/interfaces-layer.svg" alt="Edge Device Interface Layer Class Diagram" width="750">
</p>

---

#### 4.5.2.3. Application Layer

Orquesta los flujos de telemetría local, el procesamiento del outbox transaccional y la ingestión asíncrona de comandos.

*   **DeviceTelemetryAppService:** Procesa la telemetría, persiste localmente y crea una entrada en el Outbox.
*   **DeviceCommandApplicationService:** Ingiere comandos desde Kafka y expone los pendientes a las estaciones embebidas.
*   **GetDeviceConnectionStatusQueryHandler:** Recupera el estado de conexión actual basado en la telemetría.
*   **TelemetryOutboxProcessor:** Procesador en segundo plano que consume el Outbox local y reenvía los datos a la API en la nube con reintentos y tolerancia a fallos.
*   **Commands & Queries (Value Objects):** Estructuras para transferir parámetros de entrada a los servicios de aplicación.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/edge/device_class_diagram/application-layer.svg" alt="Edge Device Application Layer Class Diagram" width="750">
</p>

---

#### 4.5.2.4. Infrastructure Layer

Componentes de almacenamiento de base de datos relacional local e integración con APIs externas en la nube.

*   **DeviceTelemetryRepository / DeviceCommandRepository / OutboxRepository:** Implementaciones concretas de persistencia mapeadas a bases de datos SQL locales.
*   **DeviceTelemetryModel / DeviceCommandModel / OutboxRecordModel:** Modelos de base de datos ORM.
*   **ExternalCoreService:** Cliente que consume la API en la nube (Clair Core API) para sincronizar telemetrías y confirmaciones de comandos.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/edge/device_class_diagram/infrastructure-layer.svg" alt="Edge Device Infrastructure Layer Class Diagram" width="750">
</p>

#### 4.5.2.5. Bounded Context Software Architecture Code Level Diagrams

El diagrama de clases unificado del contexto acotado de Device & Space Management muestra la relación entre todas sus entidades, value objects, servicios y adaptadores de interfaz e infraestructura:

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/edge/device_class_diagram/unified.svg" alt="Unified Edge Devices Class Diagram" width="850">
</p>

---

### 4.5.3. Bounded Context: Alerting & Response

#### 4.5.3.1. Domain Layer

Define la abstracción del repositorio para almacenar los incidentes de alerta que ameritan respuesta local.

*   **AlertIncidentEventRepositoryInterface (Interface):** Contrato para el control y registro de incidentes de alertas que deben propagarse a los actuadores físicos locales.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/edge/alerting_class_diagram/domain-layer.svg" alt="Edge Alerting Domain Layer Class Diagram" width="750">
</p>

---

#### 4.5.3.2. Interface Layer

Endpoints REST para la interacción de los actuadores del dispositivo embebido con la estación local.

*   **AlertingApi:** Expone endpoints HTTP para que los ESP32 consulten incidentes activos y confirmen visualmente (LEDs/zumbador) la recepción de la alerta.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/edge/alerting_class_diagram/interfaces-layer.svg" alt="Edge Alerting Interface Layer Class Diagram" width="750">
</p>

---

#### 4.5.3.3. Application Layer

Orquesta la recepción asíncrona de alertas del bus de mensajería y la posterior consulta por parte del hardware periférico.

*   **AlertIncidentEventApplicationService:** Ingiere alertas críticas de Kafka, recupera pendientes para los ESP32 y registra sus acuses de recibo.
*   **KafkaAlertIncidentConsumer:** Consumidor en segundo plano que escucha el tópico de alertas críticas del backend en la nube.
*   **IngestAlertIncidentEventResult (Value Object):** Estructura del resultado de la ingesta de alertas.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/edge/alerting_class_diagram/application-layer.svg" alt="Edge Alerting Application Layer Class Diagram" width="750">
</p>

---

#### 4.5.3.4. Infrastructure Layer

Componentes de persistencia local y constantes de bus de eventos para las alertas.

*   **AlertIncidentEventRepository:** Implementación del repositorio de base de datos local.
*   **AlertIncidentEventModel:** ORM para registrar eventos de incidentes.
*   **AlertingKafkaTopics:** Constantes de los tópicos Kafka de alertas.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/edge/alerting_class_diagram/infrastructure-layer.svg" alt="Edge Alerting Infrastructure Layer Class Diagram" width="750">
</p>

#### 4.5.3.5. Bounded Context Software Architecture Code Level Diagrams

El diagrama de clases unificado del contexto acotado de Alerting & Response muestra la relación entre todas sus entidades, value objects, servicios y adaptadores de interfaz e infraestructura:

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/edge/alerting_class_diagram/unified.svg" alt="Unified Edge Alerting Class Diagram" width="850">
</p>

---

### 4.5.4. Bounded Context: Device Provisioning

#### 4.5.4.1. Domain Layer

Define las reglas de negocio y abstracciones de persistencia para mantener sincronizada la lista de dispositivos registrados.

*   **DeviceCacheService:** Lógica de validación de registros de dispositivos sincronizados desde el backend central.
*   **DeviceCacheRepositoryInterface (Interface):** Contrato para actualizar en lote la cache local de dispositivos autorizados.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/edge/provisioning_class_diagram/domain-layer.svg" alt="Edge Provisioning Domain Layer Class Diagram" width="750">
</p>

---

#### 4.5.4.2. Interface Layer

DTOs y recursos para transformar y mapear payloads de eventos de integración.

*   **DeviceCacheResource (DTO):** Objeto de transferencia que representa la información de los dispositivos para mapear actualizaciones.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/edge/provisioning_class_diagram/interfaces-layer.svg" alt="Edge Provisioning Interface Layer Class Diagram" width="750">
</p>

---

#### 4.5.4.3. Application Layer

Orquesta la recepción de eventos de cambio en la definición de dispositivos (altas, modificaciones, bajas) para refrescar la base de datos local.

*   **DeviceProvisioningApplicationService:** Servicio que maneja eventos de adición, edición o eliminación de dispositivos y actualiza la base de datos local.
*   **KafkaProvisioningConsumer:** Consumidor que escucha tópicos de aprovisionamiento en la nube.
*   **DeviceChangedIntegrationEvent / DevicesSyncRequestedIntegrationEvent (Events):** Eventos de integración correspondientes.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/edge/provisioning_class_diagram/application-layer.svg" alt="Edge Provisioning Application Layer Class Diagram" width="750">
</p>

---

#### 4.5.4.4. Infrastructure Layer

Implementaciones de persistencia local y definición de tópicos de aprovisionamiento.

*   **DeviceCacheRepository:** Adaptador concreto que actualiza la base de datos SQL local.
*   **DeviceModel:** Modelo persistido de la base de datos.
*   **ProvisioningKafkaTopics:** Definición de tópicos Kafka para aprovisionamiento.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/edge/provisioning_class_diagram/infrastructure-layer.svg" alt="Edge Provisioning Infrastructure Layer Class Diagram" width="750">
</p>

#### 4.5.4.5. Bounded Context Software Architecture Code Level Diagrams

El diagrama de clases unificado del contexto acotado de Device Provisioning muestra la relación entre todas sus entidades, value objects, servicios y adaptadores de interfaz e infraestructura:

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/edge/provisioning_class_diagram/unified.svg" alt="Unified Edge Provisioning Class Diagram" width="850">
</p>

---

## 4.6. Tactical-Level Domain-Driven Design - Embedded application

La aplicación embebida (Embedded Application) está desarrollada en C++ para ESP32, siguiendo los principios del framework **ModestIoT** (basado en eventos y comandos) para gestionar la adquisición de sensores, el control de actuadores y la comunicación con la estación base local (Edge Station) mediante HTTP/REST. A continuación, se detallan los componentes que estructuran la aplicación embebida, organizados según una arquitectura dirigida por eventos que respeta los bounded contexts implícitos del dominio.

**Arquitectura de Componentes de la Aplicación Embebida (Clair Device)**

A continuación se detalla el diagrama C4 de nivel de Componentes para la aplicación embebida de Clair, ilustrando la interacción de sus capas internas y su comunicación con el hardware y la Edge Station:

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/c4/containers/embedded/EmbeddedAppComponents-dark.svg" alt="Embedded Application Component Architecture Diagram" width="850">
</p>

> **Nota sobre la arquitectura de comunicación:**  
> El framework ModestIoT implementa un patrón de comunicación basado en eventos y comandos mediante handlers encadenados. No existen clases `EventBus` o `CommandBus` en el código; los recuadros con ese nombre en el diagrama son **representaciones conceptuales** para facilitar la comprensión del flujo de datos.

*   **Interfaces Layer (Capa de Interfaces):** Expone los mecanismos para recibir comandos remotos y consultar incidentes desde la Edge Station mediante polling HTTP/REST.
*   **Application Layer (Capa de Aplicación):** Orquesta los flujos de control del dispositivo: adquisición de sensores, evaluación de calidad del aire, publicación de telemetría y respuesta a comandos.
*   **Domain Layer (Capa de Dominio):** Contiene la lógica central independiente del hardware (cálculo de AQI, evaluación de umbrales, estados de calidad del aire).
*   **Infrastructure Layer (Capa de Infraestructura):** Implementa la comunicación con los sensores (I2C/UART), el control de actuadores (GPIO) y el envío de telemetría a la Edge Station (HTTP/REST).

Esta arquitectura basada en eventos y comandos, con un orquestador central desacoplado de los adaptadores de hardware y de comunicación, permite un diseño modular, testeable y altamente mantenible para el firmware del dispositivo Clair.

### 4.6.1. Bounded Context: Device Telemetry

#### 4.6.1.1. Domain Layer

Define las entidades principales, value objects y reglas de negocio para la captura y procesamiento de datos de telemetría en el dispositivo embebido.

*   **ClairData (Aggregate Root):** Agrega todos los datos de telemetría del dispositivo. Incluye las lecturas de CO₂, temperatura, humedad, partículas (PM1.0, PM2.5, PM10), el índice de calidad del aire (AQI), el estado general de calidad del aire y metadatos como timestamp y timezone.
*   **AirQuality (Value Object):** Contiene los valores de calidad del aire: `co2` (ppm), `temperature` (°C), `humidity` (%), y un flag `valid`.
*   **ParticulateMatter (Value Object):** Contiene las concentraciones de partículas: `pm1_0`, `pm2_5`, `pm10` (µg/m³), y un flag `valid`.
*   **AirQualityIndex (Value Object):** Calcula el AQI basado en PM2.5, incluye `aqi` (0-500) y la `category` (Good, Moderate, Unhealthy, etc.).
*   **AirQualityThresholds (Value Object):** Define los umbrales configurables para evaluar la calidad del aire: límites para PM2.5, PM10, CO₂ y humedad.
*   **AirQualityStatus (Enum):** Estados de calidad del aire: `OPTIMAL`, `MODERATE`, `CRITICAL`.
*   **Event (Entity):** Evento base del framework ModestIoT. Contiene un `id` único. Los sensores propagan `DATA_READY_EVENT` a través del Event Propagation.
*   **EventHandler (Interface):** Interfaz que deben implementar los suscriptores de eventos. Define el método `on(Event event)`.
*   **Sensor (Abstract Entity):** Clase base abstracta para todos los sensores. Contiene `pin` y un `handler` opcional para propagar eventos.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/embedded/device_telemetry_class_diagram/domain-layer.svg" alt="Device Telemetry Domain Layer Class Diagram" width="750">
</p>

---

#### 4.6.1.2. Interface Layer

Punto de entrada principal que orquesta la adquisición de datos, el procesamiento de eventos y la gestión del estado del dispositivo.

*   **ClairDevice (Orchestrator):** Es el orquestador central que implementa las interfaces `EventHandler` y `CommandHandler` del framework ModestIoT. Coordina la actualización de sensores, consume eventos (`on()`), ejecuta comandos (`handle()`), gestiona el estado del sistema (inicialización, modo normal, standby) y publica telemetría a través del `TelemetryPublisher`.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/embedded/device_telemetry_class_diagram/interfaces-layer.svg" alt="Device Telemetry Interface Layer Class Diagram" width="750">
</p>

---

#### 4.6.1.3. Application Layer

Orquesta los flujos de control para la publicación de telemetría y la coordinación de la actualización de sensores.

*   **TelemetryPublisher (Application Service):** Servicio que construye el payload de telemetría (formato JSON), gestiona los intervalos de envío con throttling (cada 10 segundos), envía los datos a la Edge Station mediante HTTPS (`POST /api/v1/device/telemetry`) y mantiene estadísticas de envíos exitosos/fallidos.
*   **TelemetryScheduler:** Componente auxiliar que gestiona los temporizadores para el envío periódico de telemetría.
*   **SensorUpdateOrchestrator:** Coordina la activación de lecturas de sensores (SCD41 y PMS5003) cuando se reciben eventos `DATA_READY_EVENT`.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/embedded/device_telemetry_class_diagram/application-layer.svg" alt="Device Telemetry Application Layer Class Diagram" width="750">
</p>

---

#### 4.6.1.4. Infrastructure Layer

Adaptadores concretos para comunicación con hardware de sensores (I2C/UART), mapeo de datos y mecanismo de propagación de eventos.

*   **SCD41Sensor (Concrete Sensor):** Implementación del sensor de CO₂, temperatura y humedad. Comunica vía I2C usando la librería Sensirion. Publica `DATA_READY_EVENT` a través del Event Propagation cuando hay nuevas lecturas.
*   **PMS5003Sensor (Concrete Sensor):** Implementación del sensor de partículas (PM1.0, PM2.5, PM10). Comunica vía UART (HardwareSerial), con manejo de trama de 32 bytes y checksum. Publica `DATA_READY_EVENT` a través del Event Propagation.
*   **SCD41SensorDevice (Wrapper):** Wrapper que contiene el `SCD41Sensor` y conecta sus eventos al Device Orchestrator.
*   **PMS5003SensorDevice (Wrapper):** Wrapper que contiene el `PMS5003Sensor` y conecta sus eventos al Device Orchestrator.
*   **PMS5003Data (Data Model):** Estructura de datos cruda del PMS5003 (pm1_0, pm2_5, pm10, valid).
*   **EventPropagation (Conceptual):** Mecanismo conceptual del framework ModestIoT que permite a los sensores llamar a `handler->on(event)` para notificar al orquestador. No existe una clase `EventBus` dedicada; se representa en el diagrama para claridad arquitectónica.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/embedded/device_telemetry_class_diagram/infrastructure-layer.svg" alt="Device Telemetry Infrastructure Layer Class Diagram" width="750">
</p>

---

#### 4.6.1.5. Bounded Context Software Architecture Code Level Diagrams

El diagrama de clases unificado del contexto acotado de Device Telemetry muestra la relación entre todas sus entidades, value objects, servicios y adaptadores de interfaz e infraestructura. Se incluyen también las relaciones conceptuales de Event Propagation propias del framework ModestIoT.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/embedded/device_telemetry_class_diagram/unified.svg" alt="Unified Device Telemetry Class Diagram" width="850">
</p>

> **Nota sobre la arquitectura de comunicación:**  
> El framework ModestIoT implementa un patrón de comunicación basado en eventos y comandos mediante handlers encadenados. Los sensores publican eventos invocando `handler->on(event)`, y el `ClairDevice` los consume implementando la interfaz `EventHandler`. No existen clases `EventBus` o `CommandBus` en el código; los recuadros con ese nombre en el diagrama son **representaciones conceptuales** para facilitar la comprensión del flujo de datos.

### 4.6.2. Bounded Context: Device Command

#### 4.6.2.1. Domain Layer

Define las abstracciones de comandos y el contrato para su manejo dentro del framework ModestIoT.

*   **Command (Entity):** Comando base del framework ModestIoT. Contiene un `id` único que identifica el tipo de acción a ejecutar (ej. `LED_ON_COMMAND`, `STANDBY_COMMAND`).
*   **CommandHandler (Interface):** Interfaz que deben implementar los suscriptores de comandos. Define el método `handle(Command command)`. `ClairDevice`, `Led` y `OLEDDisplay` implementan esta interfaz.
*   **RemoteCommandType (Enum):** Enumeración de los tipos de comandos remotos que el dispositivo puede recibir desde la Edge Station: `STANDBY`, `WAKE`, `RESTART`, `REPORT`, `CALIBRATE`.
*   **CommandResult (Value Object):** Objeto que encapsula el resultado de la ejecución de un comando. Incluye `success` (bool), `failureReason` (String) y `executionTimeMs` (unsigned long).

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/embedded/device_command_class_diagram/domain-layer.svg" alt="Device Command Domain Layer Class Diagram" width="750">
</p>

---

#### 4.6.2.2. Interface Layer

Punto de entrada principal que procesa los comandos recibidos y los despacha a los actuadores correspondientes.

*   **ClairDevice (Orchestrator):** Implementa la interfaz `CommandHandler` y actúa como el gestor central de comandos. Recibe comandos del `EdgeService` (vía `CommandDispatch`), los procesa según su tipo (`STANDBY`, `WAKE`, `REPORT`, `CALIBRATE`, `RESET`) y ejecuta las acciones correspondientes (cambiar estado del dispositivo, forzar reporte, recalibrar sensores, etc.). También es responsable de rutar comandos específicos hacia `Led` y `OLEDDisplay`.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/embedded/device_command_class_diagram/interfaces-layer.svg" alt="Device Command Interface Layer Class Diagram" width="750">
</p>

---

#### 4.6.2.3. Application Layer

Orquesta el polling de comandos remotos, la cola de comandos pendientes y el envío de ACKs a la Edge Station.

*   **EdgeService (Application Service):** Servicio unificado que gestiona tanto la telemetría como los comandos remotos. Contiene:
    *   **Command Polling:** Consulta periódicamente (`pollCommands()`, cada 5-10 segundos) la Edge Station (`GET /api/v1/device/commands/pending`) en busca de comandos pendientes.
    *   **Command Queue:** Mantiene una cola interna (`queue<RemoteCommand>`) para procesar comandos de forma ordenada y con un retraso configurable entre ellos (`commandProcessDelay`).
    *   **Command Dispatch:** A través de un callback (`CommandCallback`), entrega los comandos al `ClairDevice` para su ejecución.
    *   **Acknowledgments:** Envía ACKs a la Edge Station (`POST /api/v1/device/commands/{id}/ack`) indicando si el comando fue `EXECUTED` o `FAILED`.
*   **RemoteCommand (DTO):** Estructura que representa un comando recibido del Edge. Contiene `commandId`, `type` (ej. "STANDBY"), `parameters` (JSON opcional) y un flag `valid`.
*   **CommandProcessor:** Componente auxiliar que valida y parsea los comandos entrantes, extrayendo el tipo y los parámetros.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/embedded/device_command_class_diagram/application-layer.svg" alt="Device Command Application Layer Class Diagram" width="750">
</p>

---

#### 4.6.2.4. Infrastructure Layer

Adaptadores concretos que ejecutan comandos sobre el hardware y gestionan la comunicación HTTP con la Edge Station.

*   **Led (Actuator):** Implementa `CommandHandler`. Ejecuta comandos específicos de LED: `LED_ON_COMMAND` (enciende), `LED_OFF_COMMAND` (apaga), `LED_BLINK_COMMAND` (inicia parpadeo cada 500ms), `LED_ACKNOWLEDGE_ALL` (detiene parpadeo). Controla el GPIO directamente.
*   **OLEDDisplay (Actuator):** Implementa `CommandHandler`. Ejecuta comandos de pantalla: `DISPLAY_ON_COMMAND`, `DISPLAY_OFF_COMMAND`, `DISPLAY_SLEEP_COMMAND`, `DISPLAY_WAKE_COMMAND`, `DISPLAY_CLEAR_COMMAND`. Controla la pantalla vía I2C.
*   **CommandDispatch (Conceptual):** Mecanismo conceptual del framework ModestIoT que permite la propagación de comandos a través de `handler->handle(command)`. Los comandos fluyen desde el `EdgeService` hacia el `ClairDevice` y desde éste hacia los actuadores `Led` y `OLEDDisplay`.
*   **HttpCommandClient:** Cliente HTTP reutilizable para comunicarse con la Edge Station. Maneja los endpoints de comandos pendientes (GET) y ACKs (POST), incluyendo headers de autenticación (`X-Hardware-Id`, `X-API-Key`).

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/embedded/device_command_class_diagram/infrastructure-layer.svg" alt="Device Command Infrastructure Layer Class Diagram" width="750">
</p>

---

#### 4.6.2.5. Bounded Context Software Architecture Code Level Diagrams

El diagrama de clases unificado del contexto acotado de Device Command muestra la relación entre todas sus entidades, servicios y adaptadores. Se incluyen las relaciones conceptuales de Command Dispatch propias del framework ModestIoT, que conectan el `EdgeService` con el `ClairDevice` y éste con los actuadores `Led` y `OLEDDisplay`.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/embedded/device_command_class_diagram/unified.svg" alt="Unified Device Command Class Diagram" width="850">
</p>

> **Nota sobre la arquitectura de comandos:**  
> El framework ModestIoT implementa un patrón de comunicación basado en comandos mediante handlers encadenados. El `EdgeService` recibe comandos remotos y los propaga a través del `CommandDispatch` hacia el `ClairDevice` (que implementa `CommandHandler`). A su vez, el `ClairDevice` puede reenviar comandos específicos a `Led` y `OLEDDisplay`. No existe una clase `CommandBus` dedicada; el mecanismo es una representación conceptual para facilitar la comprensión del flujo de comandos.

### 4.6.3. Bounded Context: Device State

#### 4.6.3.1. Domain Layer

Define las enumeraciones de estados del dispositivo y las reglas de transición entre ellos.

*   **DeviceState (Enum):** Enumeración que representa los estados de inicialización del dispositivo: `INIT_NOT_STARTED` (no iniciado), `INIT_STARTING_SENSORS` (iniciando sensores), `INIT_WAITING_SENSORS` (esperando sensores), `INIT_COMPLETE` (inicialización completa), `INIT_PARTIAL` (inicialización parcial por timeout).
*   **OperationalMode (Enum):** Enumeración de los modos operativos del dispositivo: `NORMAL_MODE` (operación normal), `STANDBY_MODE` (modo bajo consumo), `SIMULATION_MODE` (modo simulación con datos sintéticos).
*   **AirQualityStatus (Enum):** Enumeración de los estados de calidad del aire: `OPTIMAL` (óptimo), `MODERATE` (moderado), `CRITICAL` (crítico).
*   **SystemHealth (Value Object):** Agrega indicadores de salud del sistema: `allSensorsReady`, `timeSynchronized`, `wifiConnected`, `displayInitialized`, `healthPercentage`. Incluye el método `evaluateHealth()` que calcula la salud general del dispositivo.
*   **StateTransition (Value Object):** Registra una transición de estado, incluyendo `fromState`, `toState`, `transitionTime` y `success`.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/embedded/device_state_class_diagram/domain-layer.svg" alt="Device State Domain Layer Class Diagram" width="750">
</p>

---

#### 4.6.3.2. Interface Layer

Punto de entrada principal que gestiona y mantiene todos los estados del dispositivo, coordinando las transiciones según los eventos y comandos recibidos.

*   **ClairDevice (Orchestrator):** Es el orquestador central responsable de mantener y gestionar:
    *   **Estado de Inicialización:** Controla la secuencia de inicialización de sensores con timeout de 10 segundos (`initState`, `initStartTime`, `INIT_TIMEOUT_MS`). Métodos: `updateInitialization()`, `isInitializationComplete()`, `getInitStateString()`.
    *   **Modo Operativo:** Gestiona el modo normal (`NORMAL_MODE`), modo standby (`STANDBY_MODE`) y modo simulación (`SIMULATION_MODE`). Métodos: `setStandbyMode()`, `isStandbyMode()`, `setSimulationEnabled()`.
    *   **Estado de Calidad del Aire:** Mantiene el estado actual (`currentData.status`) y su etiqueta (`statusLabel`). Se actualiza automáticamente cuando llegan nuevos datos de sensores.
    *   **Flags de Estado:** Mantiene indicadores como `allSensorsReady`, `displayInitialized`, `timeSynchronized`, `standbyMode`.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/embedded/device_state_class_diagram/interfaces-layer.svg" alt="Device State Interface Layer Class Diagram" width="750">
</p>

---

#### 4.6.3.3. Application Layer

Orquesta la lógica de transición de estados, la gestión de timeouts y la evaluación del estado general del dispositivo.

*   **StateManager (Application Service):** Coordina las transiciones de estado. Métodos: `transitionTo(newState)`, `getCurrentState()`, `canTransitionTo(newState)`, `onStateEnter()`, `onStateExit()`.
*   **InitStateManager:** Gestiona específicamente la inicialización del dispositivo. Métodos: `startInitialization()`, `updateInitialization()`, `isInitializationComplete()`, `hasInitializationTimeout()`, `getInitState()`, `getInitStateString()`.
*   **StandbyManager:** Gestiona el modo standby. Métodos: `enableStandby()`, `disableStandby()`, `isStandbyActive()`, `suspendOperations()` (apaga display, duerme sensores), `resumeOperations()` (reactiva sensores, enciende display).
*   **StatusEvaluator:** Evalúa el estado general de calidad del aire combinando todos los parámetros (CO₂, PM2.5, PM10, humedad). Métodos: `evaluateOverallStatus()`, `getCurrentStatus()`, `getStatusLabel()`, `getStatusIcon()`.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/embedded/device_state_class_diagram/application-layer.svg" alt="Device State Application Layer Class Diagram" width="750">
</p>

---

#### 4.6.3.4. Infrastructure Layer

Adaptadores concretos para persistencia opcional de estado y temporización.

*   **StatePersistence:** Servicio opcional para guardar/cargar el estado del dispositivo en memoria no volátil (ej. preferences). Métodos: `saveState(state)`, `loadState()`, `clearState()`.
*   **StateTimer:** Componente de temporización utilizado para gestionar timeouts (como el timeout de inicialización de 10 segundos). Métodos: `start()`, `hasTimedOut()`, `reset()`, `getElapsedMs()`.
*   **StateEventEmitter (Conceptual):** Mecanismo conceptual para emitir eventos cuando ocurren cambios de estado significativos (ej. `STATE_CHANGED`, `MODE_CHANGED`). Los suscriptores (como `ClairDevice`) pueden reaccionar a estos cambios.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/embedded/device_state_class_diagram/infrastructure-layer.svg" alt="Device State Infrastructure Layer Class Diagram" width="750">
</p>

---

#### 4.6.3.5. Bounded Context Software Architecture Code Level Diagrams

El diagrama de clases unificado del contexto acotado de Device State muestra la relación entre todas las enumeraciones de estado, los servicios de aplicación que gestionan las transiciones y el orquestador central que mantiene los estados del dispositivo.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/embedded/device_state_class_diagram/unified.svg" alt="Unified Device State Class Diagram" width="850">
</p>

> **Nota sobre la gestión de estados:**  
> El `ClairDevice` actúa como el agregador de estados del dispositivo. Mantiene los flags de inicialización, modo operativo y calidad del aire. La inicialización sigue una secuencia no bloqueante con timeout de 10 segundos. El modo standby suspende las operaciones no esenciales (sensores, display, telemetría) para ahorrar energía. El estado de calidad del aire se actualiza automáticamente tras cada lectura de sensores y determina el comportamiento del LED.

### 4.6.4. Bounded Context: Alerting

#### 4.6.4.1. Domain Layer

Define las entidades de incidentes, tipos de métricas y reglas de prioridad para las alertas en el dispositivo embebido.

*   **Incident (Entity):** Representa un incidente o alerta activa en el dispositivo. Contiene `id`, `metric` (CO2, PM25, TEMP, HUMIDITY), `status` (ACTIVE, RESOLVED), `occurredAt`, `resolvedAt` y `acknowledged`. Incluye el método `print()` para depuración.
*   **MetricType (Enum):** Enumeración de los tipos de métricas que pueden generar incidentes: `CO2`, `PM25`, `TEMP`, `HUMIDITY`.
*   **IncidentStatus (Enum):** Estados de un incidente: `ACTIVE` (activo), `RESOLVED` (resuelto), `ACKNOWLEDGED` (reconocido).
*   **IncidentPriority (Enum):** Niveles de prioridad para incidentes según la métrica: `HIGH` (CO2), `MEDIUM` (PM25), `LOW` (TEMP), `LOWEST` (HUMIDITY).
*   **AlertRule (Value Object):** Define las reglas que determinan cuándo se genera un incidente. Contiene `metric`, `thresholdValue`, `operator` (ej. >, <) y `priority`. Incluye el método `evaluate(actualValue)` para evaluar si se debe activar una alerta.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/embedded/alerting_class_diagram/domain-layer.svg" alt="Alerting Domain Layer Class Diagram" width="750">
</p>

---

#### 4.6.4.2. Interface Layer

Punto de entrada principal que integra el subsistema de alertas con el orquestador central y controla el LED según el estado de los incidentes.

*   **ClairDevice (Orchestrator):** Integra el `IncidentManager` en el flujo principal del dispositivo. En cada ciclo `update()` llama a `incidentManager.pollIncidents()` y `incidentManager.process()`. Implementa los callbacks estáticos `onIncidentDetected()` e `onIncidentResolved()` que son invocados por el `IncidentManager` cuando cambia el estado de un incidente. El método `updateWarningLed()` verifica `hasActiveIncidents()` y controla el LED (parpadeo si hay incidentes activos, apagado si no).

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/embedded/alerting_class_diagram/interfaces-layer.svg" alt="Alerting Interface Layer Class Diagram" width="750">
</p>

---

#### 4.6.4.3. Application Layer

Orquesta el polling de incidentes, la gestión de la cola de ACKs y la lógica de reintentos para confirmar la recepción de incidentes.

*   **IncidentManager (Application Service):** Servicio central que gestiona todo el ciclo de vida de los incidentes:
    *   **Polling:** Consulta periódicamente (`pollIncidents()`, cada 5 segundos) la Edge Station (`GET /api/v1/alerting/incidents/pending`) para obtener incidentes activos y resueltos.
    *   **Almacenamiento Local:** Mantiene un array de incidentes activos (`activeIncidents[5]`, máximo 5) y una cola de ACKs pendientes (`pendingAcks[10]`, máximo 10).
    *   **Callbacks:** Invoca los callbacks configurados (`onIncidentDetected`, `onIncidentResolved`) cuando cambia el estado de un incidente.
    *   **ACK Queue Management:** Encola ACKs cuando se detectan incidentes nuevos o resueltos, y los procesa en segundo plano con lógica de reintentos (máximo 3 reintentos, intervalo de 5 segundos).
    *   **Métricos de Prioridad:** Proporciona `getMetricPriority()` y `getMostCriticalIncident()` para determinar el incidente más crítico cuando múltiples están activos.
*   **Incident (DTO):** Estructura de datos que representa un incidente recibido del Edge o almacenado localmente.
*   **PendingAck (Value Object):** Representa un ACK pendiente de envío. Contiene `incidentId`, `status` (ACTIVE/RESOLVED), `lastAttempt`, `retryCount` y `active`.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/embedded/alerting_class_diagram/application-layer.svg" alt="Alerting Application Layer Class Diagram" width="750">
</p>

---

#### 4.6.4.4. Infrastructure Layer

Adaptadores concretos para la comunicación HTTP con la Edge Station, control del LED y gestión de la cola de ACKs.

*   **Led (Actuator):** Implementa `CommandHandler`. Es controlado indirectamente por el `IncidentManager` a través del `ClairDevice`. Cuando `hasActiveIncidents()` es `true`, se inicia el parpadeo (`startBlink(500)`); cuando no hay incidentes activos, el LED se apaga (`off()`).
*   **IncidentHttpClient:** Cliente HTTP para comunicarse con la Edge Station. Maneja el endpoint de incidentes pendientes (`GET /api/v1/alerting/incidents/pending`) y el endpoint de ACK (`POST /api/v1/alerting/incidents/{id}/ack`). Incluye headers de autenticación (`X-Hardware-Id`, `X-API-Key`).
*   **IncidentAckQueue:** Cola especializada para gestionar ACKs pendientes. Métodos: `add(incidentId, status)`, `remove(incidentId)`, `getNext()`, `size()`, `isEmpty()`.
*   **LedController (Conceptual):** Mecanismo conceptual que conecta el estado de incidentes con el control del LED. El `ClairDevice` actúa como este controlador en la implementación actual.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/embedded/alerting_class_diagram/infrastructure-layer.svg" alt="Alerting Infrastructure Layer Class Diagram" width="750">
</p>

---

#### 4.6.4.5. Bounded Context Software Architecture Code Level Diagrams

El diagrama de clases unificado del contexto acotado de Alerting muestra la relación entre todas las entidades de incidentes, el servicio de aplicación `IncidentManager`, el orquestador `ClairDevice` y el actuador `Led`. Se incluyen las relaciones de polling HTTP hacia la Edge Station y el flujo de control que activa el parpadeo del LED cuando hay incidentes activos.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/embedded/alerting_class_diagram/unified.svg" alt="Unified Alerting Class Diagram" width="850">
</p>

> **Nota sobre el flujo de incidentes:**  
> El `IncidentManager` consulta periódicamente la Edge Station para obtener incidentes pendientes. Cuando se detecta un nuevo incidente activo, se añade al array local y se invoca el callback `onIncidentDetected()`, que a su vez llama a `updateWarningLed()` en el `ClairDevice`. Este método verifica `hasActiveIncidents()` y controla el LED (inicia parpadeo a 500ms si hay incidentes, apaga si no). Los ACKs se encolan y se envían en segundo plano con reintentos automáticos (máximo 3, cada 5 segundos).

### 4.6.5. Bounded Context: Display

#### 4.6.5.1. Domain Layer

Define las estructuras de datos para mostrar en la pantalla, los estados de la pantalla y las reglas de gestión de energía.

*   **DisplayData (Aggregate Root):** Agrega todos los datos que se muestran en la pantalla OLED. Contiene `AirQualityDisplay` (CO₂, temperatura, humedad, validez, etiqueta de estado), `ParticulateMatterDisplay` (PM1.0, PM2.5, PM10, validez) y `AQIDisplay` (valor AQI, categoría).
*   **DisplayState (Enum):** Estados de la pantalla: `DISPLAY_ON` (encendida), `DISPLAY_SLEEP` (suspensión, ahorro de energía), `DISPLAY_OFF` (apagada completamente).
*   **DisplayConfig (Value Object):** Configuración de la pantalla. Contiene `width` (128), `height` (64), `i2cAddress` (0x3C), `sdaPin` (21), `sclPin` (22), `sleepAfterMs` (30000 ms de inactividad antes de dormir), `wakeDurationMs` (10000 ms de actividad tras despertar).
*   **AirQualityDisplay (Value Object):** Datos de calidad del aire para mostrar: `co2` (ppm), `temperature` (°C), `humidity` (%), `valid` (bool), `statusLabel` (String: "Optimal", "Moderate", "Critical").
*   **ParticulateMatterDisplay (Value Object):** Datos de partículas para mostrar: `pm1_0`, `pm2_5`, `pm10` (µg/m³), `valid` (bool).
*   **AQIDisplay (Value Object):** Índice de calidad del aire para mostrar: `value` (0-500), `category` (String: "Good", "Moderate", "Unhealthy", etc.).

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/embedded/display_class_diagram/domain-layer.svg" alt="Display Domain Layer Class Diagram" width="750">
</p>

---

#### 4.6.5.2. Interface Layer

Punto de entrada principal que actualiza la pantalla cuando cambian los datos del dispositivo o cuando se reciben comandos de control.

*   **ClairDevice (Orchestrator):** Integra la pantalla en el flujo principal del dispositivo. En el método `refreshDisplay()` crea un objeto `DisplayData` a partir del `ClairData` actual y llama a `display.updateData(displayData)`. También envía comandos a la pantalla (`DISPLAY_ON_COMMAND`, `DISPLAY_OFF_COMMAND`, etc.) cuando recibe comandos remotos o cambia el estado del dispositivo (ej. al entrar/salir de modo standby). Mantiene el flag `displayInitialized` y la variable `lastDisplayedStatus` para evitar refrescos innecesarios.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/embedded/display_class_diagram/interfaces-layer.svg" alt="Display Interface Layer Class Diagram" width="750">
</p>

---

#### 4.6.5.3. Application Layer

Orquesta la actualización de la pantalla, el mapeo de datos y la gestión automática de energía.

*   **DisplayManager (Application Service):** Servicio central que coordina todas las operaciones de la pantalla. Métodos: `updateDisplay(data)` (actualiza y refresca), `refreshScreen()` (redibuja), `clearScreen()`, `sleep()`, `wake()`, `off()`, `on()`, `autoPowerManagement()` (gestiona el apagado automático por inactividad), `isInitialized()`, `getState()`.
*   **DisplayDataMapper:** Servicio responsable de transformar `ClairData` (del dominio de telemetría) a `DisplayData` (del dominio de display). Métodos: `fromClairData(clairData)`, `toDisplayData(clairData)`, `getAirQualityLabel(co2)` (convierte CO₂ en etiqueta textual: "Excellent", "Good", "Normal", "Moderate", "Poor", "Bad").
*   **DisplayScheduler:** Componente auxiliar que gestiona los temporizadores para el refresco periódico de la pantalla. Métodos: `scheduleRefresh(interval)`, `isTimeToRefresh()`, `resetTimer()`.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/embedded/display_class_diagram/application-layer.svg" alt="Display Application Layer Class Diagram" width="750">
</p>

---

#### 4.6.5.4. Infrastructure Layer

Adaptadores concretos para la comunicación I2C con el hardware de la pantalla OLED SSD1306, la gestión de energía y el despacho de comandos.

*   **OLEDDisplay (Actuator):** Implementa `CommandHandler`. Es el adaptador principal que controla la pantalla SSD1306 de 128x64 píxeles.
    *   **Inicialización:** Configura I2C (`Wire.begin(sdaPin, sclPin)`, clock a 400kHz) e inicializa el display con `display.begin(SSD1306_SWITCHCAPVCC, i2cAddress)`.
    *   **Rendering:** Métodos `refresh()`, `clear()`, y métodos privados de dibujo (`drawStatusBar()`, `drawAirQualityData()`, `drawParticulateMatterData()`, `drawAQI()`, `drawFooter()`).
    *   **Power Management:** Métodos `sleep()` (envía comando `SSD1306_DISPLAYOFF`), `wake()` (envía `SSD1306_DISPLAYON` y refresca), `off()`, `on()`, `autoPowerManagement()` (duerme tras 30 segundos de inactividad).
    *   **Command Handling:** Procesa comandos `DISPLAY_ON_COMMAND`, `DISPLAY_OFF_COMMAND`, `DISPLAY_SLEEP_COMMAND`, `DISPLAY_WAKE_COMMAND`, `DISPLAY_CLEAR_COMMAND`.
*   **I2CBus:** Componente de bajo nivel para la comunicación I2C. Métodos: `begin(sda, scl)`, `setClock(frequency)`, `scanDevices()` (útil para depuración).
*   **CommandDispatch (Conceptual):** Mecanismo conceptual del framework ModestIoT que permite la propagación de comandos hacia la pantalla a través de `handler->handle(command)`.
*   **DisplayPowerManager:** Componente especializado en la gestión de energía de la pantalla. Métodos: `managePower(currentState, lastUpdateTime, sleepAfterMs)`, `shouldSleep(lastUpdateTime, sleepAfterMs)`.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/embedded/display_class_diagram/infrastructure-layer.svg" alt="Display Infrastructure Layer Class Diagram" width="750">
</p>

---

#### 4.6.5.5. Bounded Context Software Architecture Code Level Diagrams

El diagrama de clases unificado del contexto acotado de Display muestra la relación entre todas las estructuras de datos de visualización, el servicio de aplicación `DisplayManager`, el orquestador `ClairDevice` y el actuador `OLEDDisplay`. Se incluyen las relaciones de mapeo desde `ClairData` (proveniente del contexto de telemetría) hacia `DisplayData`, y el flujo de comandos a través del `CommandDispatch` del framework ModestIoT.

<p align="center">
  <img src="https://raw.githubusercontent.com/Vanana-Desarrollo-de-Soluciones-IOT/c4-diagrams/main/assets/class-diagrams/embedded/display_class_diagram/unified.svg" alt="Unified Display Class Diagram" width="850">
</p>

> **Nota sobre el diseño de la pantalla:**  
> La pantalla OLED se actualiza automáticamente cuando cambia el estado de calidad del aire o cuando se completa la inicialización del dispositivo. El contenido mostrado incluye PM1.0, PM2.5, PM10, CO₂ y temperatura/humedad. La pantalla implementa gestión automática de energía: tras 30 segundos sin actualizaciones entra en modo de suspensión para ahorrar energía, y se reactiva automáticamente cuando hay nuevos datos o se recibe un comando de activación. El layout utiliza texto de tamaño pequeño (8 píxeles por línea) y muestra "--" cuando los datos no son válidos.