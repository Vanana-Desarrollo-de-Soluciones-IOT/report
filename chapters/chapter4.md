# Capítulo IV: Solution Software Design

## 4.1. Strategic-Level Domain-Driven Design.

El Strategic-Level Domain-Driven Design constituye la base fundamental para el desarrollo de la aplicación Clair. Este enfoque nos permite identificar y definir los límites de los contextos de dominio, establecer las relaciones entre ellos y crear una arquitectura de software sólida que soporte los objetivos del negocio.
En esta fase estratégica, nos enfocamos en:

- Comprensión profunda del dominio: Identificación de los procesos de negocio críticos

- Definición de bounded contexts: Establecimiento de límites claros entre diferentes áreas funcionales

- Modelado de relaciones: Definición de cómo interactúan los diferentes contextos

- Arquitectura de alto nivel: Diseño de la estructura general del sistema



La aplicación Clair está diseñada con una arquitectura IoT Edge que prioriza el procesamiento distribuido entre el borde (sensores y edge stations) y la nube, permitiendo:

- Procesamiento en el borde: Los sensores y edge stations procesan datos localmente antes de sincronizar con la nube, reduciendo latencia y ancho de banda

- Tolerancia a fallos: El edge station almacena datos localmente en SQLite, permitiendo operación offline y sincronización eventual cuando la conectividad se restore

- Escalabilidad horizontal: Múltiples edge stations pueden gestionar diferentes zonas o instalaciones de forma independiente

- Seguridad en capas: Comunicación cifrada entre sensores, edge y cloud; autenticación OAuth2; tokens revocables

### 4.1.1. Design-Level EventStorming.

#### 4.1.1.1 Candidate Context Discovery.

#### 4.1.1.2 Domain Message Flows Modeling.

#### 4.1.1.3 Bounded Context Canvases.

### 4.1.2. Context Mapping.

### 4.1.3. Software Architecture.

#### 4.1.3.1. Software Architecture System Landscape Diagram.

#### 4.1.3.2. Software Architecture Context Level Diagrams.

#### 4.1.3.2. Software Architecture Container Level Diagrams.

#### 4.1.3.3. Software Architecture Deployment Diagrams.

## 4.2. Tactical-Level Domain-Driven Design

-----------------

4.2.3. Bounded Context: <Bounded Context Name>
4.2.3.1. Domain Layer.
4.2.3.2. Interface Layer.
4.2.3.3. Application Layer.
4.2.3.4. Infrastructure Layer.
4.2.3.5. Bounded Context Software Architecture Component Level Diagrams.
4.2.3.6. Bounded Context Software Architecture Code Level Diagrams.
4.2.3.6.1. Bounded Context Domain Layer Class Diagrams.
4.2.3.6.2. Bounded Context Database Design Diagram.