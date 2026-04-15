# Capítulo IV: Solution Software Design

## 4.1. Strategic-Level Domain-Driven Design.

### 4.1.1. Design-Level EventStorming.

El Strategic-Level Domain-Driven Design constituye la base fundamental para el desarrollo de la aplicación Clair. Este enfoque nos permite identificar y definir los límites de los contextos de dominio, establecer las relaciones entre ellos y crear una arquitectura de software sólida que soporte los objetivos del negocio.
En esta fase estratégica, nos enfocamos en:

- Comprensión profunda del dominio: Identificación de los procesos de negocio críticos

- Definición de bounded contexts: Establecimiento de límites claros entre diferentes áreas funcionales

- Modelado de relaciones: Definición de cómo interactúan los diferentes contextos

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
- Reducir la ambigüedad en la conversación técnico-funcional  
- Mejorar la trazabilidad entre decisiones de negocio y diseño de software  

En paralelo, se definieron doce flujos principales *end-to-end*, representando los recorridos críticos del sistema:

**Leyenda de Elementos**

<p align="center">
  <img src="https://i.imgur.com/nqINlqg.png" width="500">
</p>

**1. User Registration and Access Activation**

<p align="center">
  <img src="https://i.imgur.com/3MbRs9Z.png" width="700">
</p>

**2. Login and Session Start**

<p align="center">
  <img src="https://i.imgur.com/jvEigtT.png" width="700">
</p>

**3. Trial and Subscription Lifecycle**

<p align="center">
  <img src="https://i.imgur.com/7wSa5xs.png" width="700">
</p>

**4. Checkout and Payment Outcome**

<p align="center">
  <img src="https://i.imgur.com/1dgJLHX.png" width="700">
</p>

**5. Facility and Space Setup**

<p align="center">
  <img src="https://i.imgur.com/PopJW9Q.png" width="700">
</p>

**6. Device Onboarding**

<p align="center">
  <img src="https://i.imgur.com/FDUiEL9.png" width="700">
</p>

**7. Threshold Management**

<p align="center">
  <img src="https://i.imgur.com/dEGlvX9.png" width="700">
</p>

**8. Telemetry Ingestion and Validation**

<p align="center">
  <img src="https://i.imgur.com/R7wW3kx.png" width="700">
</p>

**9. Air Quality Evaluation**

<p align="center">
  <img src="https://i.imgur.com/qkJ8oVo.png" width="700">
</p>

**10. Critical Alert Management**

<p align="center">
  <img src="https://i.imgur.com/TTe7xX5.png" width="700">
</p>

**11. Corrective Action Orchestration**

<p align="center">
  <img src="https://i.imgur.com/ffAxj7b.png" width="700">
</p>

**12. Reporting and Insights**

<p align="center">
  <img src="https://i.imgur.com/RzEd1me.png" width="700">
</p>
Cada flujo fue modelado de manera independiente y detallada, utilizando *post-its* atómicos (sin combinación de elementos), lo que asegura que cada evento, comando, regla y reacción se mantenga explícito y alineado con el *Ubiquitous Language* del dominio.

El tablero completo del  Candidate Context Discovery puede visualizarse en el siguiente enlace: https://bit.ly/3QwYkAS

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