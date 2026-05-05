# Capítulo VI: Product Implementation, Validation & Deployment

## 6.1. Software Configuration Management.

### 6.1.1. Software Development Environment Configuration.

Esta sección establece el ecosistema de herramientas y servicios seleccionados para garantizar un flujo de trabajo estandarizado, facilitando la colaboración entre los miembros del equipo y la integración de los componentes IoT.

| **Nombre del Producto** | **Propósito de Uso** | **Descripción de Uso en el Proyecto** | **Ruta de Referencia / Descarga** |
| ----------------------- | ---------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Trello** | Project Management | Gestión de tareas mediante tableros Kanban y seguimiento de Sprints. | https://trello.com/ |
| **Figma** | Product UX/UI Design | Diseño de interfaces de usuario, wireframes y prototipos de alta fidelidad. | https://figma.com/ |
| **Git / GitHub** | Software Development | Control de versiones y alojamiento del repositorio de código fuente. | https://github.com/ |
| **Spring Boot (Java)** | Backend Development | Framework principal para el desarrollo de la API y lógica del negocio. | https://spring.io/projects/spring-boot |
| **OpenAPI / Swagger** | Software Documentation | Generación de documentación interactiva y técnica de los endpoints del backend. | https://swagger.io/ |
| **C++ (Arduino IDE)** | Embedded App | Programación de la lógica de sensores y conectividad en hardware físico. | https://www.arduino.cc/en/software |
| **Python** | Automation & Analytics | Scripts para análisis de datos ambientales y automatización de tareas. | https://www.python.org/downloads/ |
| **Google OAuth2** | Identity & Access | Servicio para la autenticación segura de usuarios mediante cuentas de Google. | https://console.cloud.google.com/ |
| **Stripe** | Billing & Subscription | Pasarela de pagos para la gestión de suscripciones y transacciones. | https://stripe.com/ |
| **Resend** | Notifications | Plataforma para el envío de correos electrónicos y alertas críticas a usuarios. | https://resend.com/ |
| **Postman** | Software Testing | Validación de endpoints y pruebas de integración de la API REST. | https://www.postman.com/downloads/ |
| **Docker** | Deployment | Contenedorización de microservicios para asegurar la portabilidad del sistema. | https://www.docker.com/products/docker-desktop |
| **Flutter SDK** | Mobile Development | Framework multiplataforma para el desarrollo de la aplicación móvil de Clair. | [docs.flutter.dev](https://docs.flutter.dev/get-started/install) |
| **Angular CLI** | Web Development | Herramienta de línea de comandos para la creación y gestión de la aplicación web. | https://angular.io/cli |
| **Material Design 3** | UI Framework | Librería de componentes y tokens de diseño para la interfaz de la web app. | https://m3.material.io/ |
| **Dart DevTools** | Debugging | Conjunto de herramientas para el perfilado y depuración de la app en Flutter. | https://dart.dev/tools/dart-devtools |

### 6.1.2. Source Code Management.

### 6.1.3. Source Code Style Guide & Conventions.

Para garantizar la mantenibilidad, escalabilidad y legibilidad del ecosistema tecnológico de **Clair**, el equipo ha adoptado un conjunto de directrices estrictas basadas en estándares internacionales de la industria. Una decisión fundamental de diseño es que toda la nomenclatura (nombres de clases, variables, métodos y comentarios) se realizará exclusivamente en inglés, asegurando la consistencia técnica y facilitando la integración de servicios de terceros.

A continuación, se describen las convenciones y guías de estilo adoptadas para los lenguajes principales de la solución:

- **Java (Backend):** Se seguirá estrictamente la **Google Java Style Guide**. Se empleará *UpperCamelCase* para los nombres de clases y *lowerCamelCase* para métodos y variables. Al utilizar **Spring Boot**, se respetarán sus convenciones de estructura de paquetes orientada a dominios y el uso de anotaciones para la inyección de dependencias, garantizando un código limpio y desacoplado.
- **C++ (Embedded App):** Para la lógica de los dispositivos físicos, se aplican convenciones de nombrado claras que reflejen acciones físicas del hardware, como la captura de telemetría. Se utilizará *SCREAMING_SNAKE_CASE* para constantes y macros, manteniendo una estructura que facilite el rastreo de cambios en el código de sensores.
- **TypeScript & Angular (Web App):** Se implementará la **Angular Coding Style Guide** oficial. Se prioriza el uso de tipos estrictos en TypeScript y el nombrado de componentes siguiendo el patrón `nombre.component.ts`. La interfaz se construirá bajo los estándares de **Material Design 3**, utilizando sus tokens de diseño para garantizar la consistencia visual.
- **HTML & CSS:** Se implementará la **Google HTML/CSS Style Guide**. Las clases de estilo se nombrarán bajo la metodología BEM (Block Element Modifier) en inglés, buscando evitar la confusión visual y optimizar la reutilización de componentes de UI.
- **Dart & Flutter (Mobile App):** Se adoptan las **Effective Dart** guidelines. Se utilizará *UpperCamelCase* para clases y *lowerCamelCase* para variables y funciones. Para la estructura de archivos, se seguirá la convención de *snake_case* y se aplicará una arquitectura de estados limpia para asegurar la reactividad de la interfaz.
- **Python (Automation & Data):** Se seguirá el estándar **PEP 8** para todos los scripts de análisis y automatización. Esto asegura que las visualizaciones técnicas y el procesamiento de datos ambientales mantengan un estándar de calidad profesional.
- **Gherkin (.feature files):** Para la automatización de pruebas y especificación de requerimientos, se utilizarán las **Gherkin Conventions for Readable Specifications**. Todas las historias de usuario y criterios de aceptación se redactarán en inglés empleando las palabras clave *Given, When, Then* para describir el comportamiento esperado del sistema.

Esta uniformidad en todos los niveles del stack tecnológico permite que cualquier miembro del equipo pueda intervenir en los diferentes módulos de la solución con una curva de aprendizaje reducida, manteniendo siempre un estándar de calidad profesional en el repositorio de **GitHub**.

### 6.1.4. Software Deployment Configuration.

# 6.2. Landing Page, Services & Applications Implementation.

### 6.2.1. Sprint 1

#### 6.2.1.1. Sprint Planning 1.

#### 6.2.1.2. Aspect Leaders and Collaborators.

#### 6.2.1.3. Sprint Backlog 1.

#### 6.2.1.4. Development Evidence for Sprint Review.

#### 6.2.1.5. Testing Suite Evidence for Sprint Review.

#### 6.2.1.6. Execution Evidence for Sprint Review.

#### 6.2.1.7. Services Documentation Evidence for Sprint Review.

#### 6.2.1.8. Software Deployment Evidence for Sprint Review.

#### 6.2.1.9. Team Collaboration Insights during Sprint.

### 6.2.2. Sprint 2

#### 6.2.2.1. Sprint Planning 2.

#### 6.2.2.2. Aspect Leaders and Collaborators.

#### 6.2.2.3. Sprint Backlog 2.

#### 6.2.2.4. Development Evidence for Sprint Review.

#### 6.2.2.5. Testing Suite Evidence for Sprint Review.

#### 6.2.2.6. Execution Evidence for Sprint Review.

#### 6.2.2.7. Services Documentation Evidence for Sprint Review.

#### 6.2.2.8. Software Deployment Evidence for Sprint Review.

#### 6.2.2.9. Team Collaboration Insights during Sprint.

### 6.2.3. Sprint 3

#### 6.2.3.1. Sprint Planning 3.

#### 6.2.3.2. Aspect Leaders and Collaborators.

#### 6.2.3.3. Sprint Backlog 3.

#### 6.2.3.4. Development Evidence for Sprint Review.

#### 6.2.3.5. Testing Suite Evidence for Sprint Review.

#### 6.2.3.6. Execution Evidence for Sprint Review.

#### 6.2.3.7. Services Documentation Evidence for Sprint Review.

#### 6.2.3.8. Software Deployment Evidence for Sprint Review.

#### 6.2.3.9. Team Collaboration Insights during Sprint.

### 6.2.4. Sprint 4

#### 6.2.4.1. Sprint Planning 4.

#### 6.2.4.2. Aspect Leaders and Collaborators.

#### 6.2.4.3. Sprint Backlog 4.

#### 6.2.4.4. Development Evidence for Sprint Review.

#### 6.2.4.5. Testing Suite Evidence for Sprint Review.

#### 6.2.4.6. Execution Evidence for Sprint Review.

#### 6.2.4.7. Services Documentation Evidence for Sprint Review.

#### 6.2.4.8. Software Deployment Evidence for Sprint Review.

#### 6.2.4.9. Team Collaboration Insights during Sprint.

## 6.3. Validation Interviews.

### 6.3.1. Diseño de Entrevistas.

### 6.3.2. Registro de Entrevistas.

### 6.3.3. Evaluaciones según heurísticas.

## 6.4. Video About-the-Product.