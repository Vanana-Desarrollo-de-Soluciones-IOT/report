**Artefactos de UX (Cuando corresponda) Cuando corresponda, cada equipo tendrá creado un proyecto en UXPressia, en el cual deben elaborar los artefactos de UX soportados por la herramienta. Capturas en imagen de estos artefactos deben incluirse en el Document Report en las secciones adecuadas y con las explicaciones y análisis que correspondan. Del mismo modo, los diagramas en herramientas indicadas como LucidChart o Figma, deben incluirse como imágenes en el documento junto con su explicación, además de ser mostradas y explicadas en el video de exposición.**



Para los diagramas de EventStorming se utilizará LucidChart / Miro.

# Capítulo II: Requirements Elicitation & Analysis

## 2.1. Competidores.

En esta sección se realiza la identificación y descripción de los principales competidores directos (3 como mínimo) con modelos de negocio basados en productos digitales similares, o en su defecto competidores indirectos con ofertas parcialmente similares

### 2.1.1. Análisis competitivo.

<table>
    <thead>
        <tr>
            <th colspan="6">Competitive Analysis Landscape</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td colspan="2">¿Por qué llevar a cabo este análisis?</td>
            <td colspan="4">El objetivo es identificar las brechas tecnológicas y de experiencia de usuario en las plataformas actuales de monitoreo de aire en Perú, para validar que la integración de alertas personalizadas de Clair responde a una demanda insatisfecha en espacios cerrados.</td>
        </tr>
        <tr>
            <td colspan="2">(En la cabecera colocar por cada competidor nombre y logo)</td>
            <td>Vanana <img src="../assets/competitors/Clair.svg" alt="Su startup"></td>
            <td>Airly <img src="../assets/competitors/airly.png" alt="Su startup"></td>
            <td>IQAir <img src="../assets/competitors/iqair.jpg" alt="Su startup"></td>
            <td>Kaiterra <img src="../assets/competitors/kaiterra.jpg" alt="Su startup"></td>
        </tr>
        <tr>
            <td rowspan="2"><strong>Perfil</strong></td>
            <td>Overview</td>
            <td>Clair se enfoca en el microclima de espacios comerciales cerrados, integrando sensores PM2.5/CO2 con una plataforma que prioriza la interpretabilidad visual y la acción correctiva.</td><td>Empresa polaca con una de las redes de sensores de aire más grandes del mundo. En Lima, son el referente en monitoreo de exteriores (calle) mediante mapas de calor comunitarios y datos abiertos.</td><td>Estándar de oro global en tecnología de purificación y monitoreo. Su serie Visual es el dispositivo de referencia para oficinas de alto nivel y sedes corporativas que buscan prestigio y precisión suiza.</td><td>Empresa enfocada exclusivamente en el sector B2B y Smart Buildings. Sus dispositivos, como el Sensedge, están diseñados para ser empotrados en paredes y techos, integrándose directamente con los sistemas de aire acondicionado (HVAC).</td>
        </tr>
        <tr>
            <td>Ventaja competitiva ¿Qué valor ofrece a los clientes?</td>
            <td>Gestión Basada en Evidencia: Ofrece reportes históricos semanales que transforman suposiciones en decisiones de gestión de aforo y ventilación. <br> Accesibilidad Operativa: Diseñado para administradores que no son expertos en calidad del aire, facilitando una tasa de respuesta del 40% ante alertas.</td><td>Efecto de Red: Sus datos son utilizados por municipalidades y medios de comunicación, lo que les da una visibilidad de marca masiva. <br> Familiaridad: Los usuarios de Lima ya reconocen sus estaciones en distritos como Miraflores o San Borja.</td><td>Autoridad de Marca: Poseen la base de datos de calidad del aire más consultada del mundo; aparecer en su ranking otorga validación internacional. <br> Certificación de Datos: Sus sensores están validados para auditorías de salud ambiental de alto rigor.</td><td>Cumplimiento Normativo: Sus productos son los únicos que garantizan puntos directos para certificaciones internacionales de edificios verdes como LEED, WELL y RESET. <br> Integración BMS: Se comunica mediante protocolos industriales (BACnet, Modbus) con la infraestructura inteligente del edificio.</td>
        </tr>
        <tr>
            <td rowspan="2"><strong>Perfil de Marketing</strong></td>
            <td>Mercado objetivo</td>
            <td>Primario: Administradores de centros comerciales, gimnasios, oficinas y restaurantes en Lima. <br> Secundario: Personas preocupadas por la calidad del aire en el Hogar. </td><td>Gobiernos municipales, ONGs ambientales y empresas de Retail con fuertes políticas de responsabilidad social (ESG) que operan principalmente en Lima (Miraflores, San Isidro).</td><td>Consumidores de lujo, instituciones de salud privadas y embajadas en Perú que no escatiman en costos para garantizar pureza total.</td><td>Desarrolladoras inmobiliarias corporativas y administradores de Centros Comerciales que necesitan cumplir con estándares internacionales de construcción sostenible.</td>
        </tr>
        <tr>
            <td>Estrategias de marketing</td>
            <td>Estrategia de Gamificación y Reportes: Envío de un "Reporte de Salud Semanal" a los administradores.</td><td>Open Data: Mantener un mapa de acceso gratuito para el ciudadano común, lo que sirve como "caballo de Troya" para vender soluciones privadas a las empresas del entorno.</td><td>Inbound Marketing Global: Uso de su App para enviar notificaciones de alerta de polución en Lima, sugiriendo la compra de sus equipos como solución inmediata.</td><td>Account-Based Marketing (ABM): Campañas dirigidas específicamente a arquitectos y gestores de infraestructura para que incluyan sus sensores en los planos de nuevos proyectos desde la fase de diseño.</td>
        </tr>
        <tr>
            <td rowspan="3"><strong>Perfil de Producto</strong></td>
            <td>Productos & Servicios</td>
            <td>Hardware: Sensor "Clair-V1". <br> Software: App móvil para usuarios/clientes y Dashboard Web para administradores con reportes históricos semanales. <br> Servicio: Sistema de alertas inteligentes vía Notificaciones con recomendaciones de ventilación basadas en niveles de ocupación. </td><td>Hardware: Sensores de exterior de alta resistencia y sensores de interior simplificados.<br> Software: Mapa global de calidad del aire (Airly Map) y API de datos para integración en pantallas publicitarias o webs municipales.<br> Servicio: Pronóstico de calidad del aire a 24h mediante Inteligencia Artificial.</td><td>Hardware: Monitor AirVisual Pro (pantalla a color de alta resolución incorporada). <br> Software: Integración con la red global AirVisual. <br> Servicio: Sincronización automática con purificadores de aire de la misma marca.</td><td>Hardware: Sensedge y Sensedge Mini (sensores modulares calibrables). <br> Software: Dashboard de nivel industrial con protocolos de seguridad de datos para empresas. <br> Servicio: Consultoría para obtención de certificaciones WELL, LEED y RESET. Integración total con sistemas HVAC (Aire acondicionado centralizado).</td>
        </tr>
        <tr>
            <td>Precios & Costos</td>
            <td>Modelo Híbrido: Venta del hardware (pago único accesible) + Suscripción mensual "Clair Pro" para acceso a analítica avanzada y reportes históricos (SaaS).</td><td>Modelo B2B/B2G: Contratos anuales de "Aire como Servicio" (Air as a Service) que incluyen mantenimiento y acceso a la plataforma de datos. <br> Costo Estimado: Suscripciones anuales desde $500 - $1,000 USD por punto de monitoreo.</td><td>Modelo Retail Premium: Venta directa de hardware de alto costo. No suele requerir suscripción para funciones básicas, pero el equipo es costoso. <br> Costo Estimado: Hardware $280 - $350 USD por unidad.</td><td>Modelo de Proyecto: Presupuestos por volumen para edificios completos o centros comerciales. Incluye planes de reemplazo de módulos de sensores cada 2 años. <br> Costo Estimado: Proyectos desde $1,500 USD en adelante según la escala del edificio.</td>
        </tr>
        <tr>
            <td>Canales de distribución (Web y/o Móvil)</td>
            <td>Web: Plataforma de gestión centralizada para administradores de múltiples locales. <br> Móvil: App (iOS/Android) para monitoreo en tiempo real y recepción de alertas.</td><td>Web: Mapa interactivo público y panel de control para clientes corporativos. <br> Móvil: App Airly (enfocada en el ciudadano que consulta el aire de su zona).</td><td>Web: E-commerce global y base de datos de consulta mundial. <br> Móvil: App AirVisual (líder en descargas, usada como canal de marketing para vender sus purificadores).</td><td>Web: Dashboard empresarial compatible con protocolos industriales (BACnet, Modbus). <br> Móvil: App de visualización técnica para gestores de mantenimiento de edificios (Facility Managers).</td>
        </tr>
        <tr>
            <td rowspan="4"><strong>Análisis SWOT</strong></td>
            <td>Fortalezas</td>
            <td>Profundo conocimiento del contexto de Lima; interfaz intuitiva basada en Lean UX; bajo costo de implementación.</td><td>Red de sensores ya establecida en distritos clave de Lima; algoritmos de IA predictiva muy avanzados; fuerte presencia en medios de comunicación.</td><td>Marca número 1 a nivel mundial en confianza; ecosistema completo que conecta monitores con purificadores de aire.</td><td>Único que garantiza puntos para certificaciones LEED/WELL; diseño modular que facilita el mantenimiento en grandes infraestructuras.</td>
        </tr>
        <tr>
            <td>Debilidades</td>
            <td>Marca nueva en el mercado; recursos limitados para I+D comparado con globales; dependencia inicial de la adopción de los administradores.</td><td>Su enfoque principal es el exterior (calle), perdiendo precisión en las dinámicas de flujo de personas dentro de comercios cerrados.</td><td>Precios muy elevados para el mercado promedio peruano; soporte técnico remoto o inexistente en Lima (depende de distribuidores).</td><td>Demasiado complejo y caro para un comercio mediano o pequeño; requiere instalación técnica especializada.</td>
        </tr>
        <tr>
            <td>Oportunidades</td>
            <td>Creciente preocupación por la salud post-pandemia en Lima; falta de soluciones específicas para el sector comercial peruano; posibilidad de crear un "Sello de Calidad de Aire" local.</td><td>Alianzas con municipalidades para integrar datos de interiores en proyectos de "Smart Cities".</td><td>Capturar el mercado de lujo y corporativos transnacionales en San Isidro y Miraflores.</td><td>Crecimiento de la construcción de edificios de oficinas clase A+ en el centro financiero de Lima.</td>
        </tr>
        <tr>
            <td>Amenazas</td>
            <td>Ingreso de clones económicos de China; cambios bruscos en las normativas de salud del gobierno peruano que favorezcan certificaciones internacionales caras.</td><td>Saturación de datos públicos gratuitos que hagan que las empresas no quieran pagar por una versión privada.</td><td>Aparición de sensores de bajo costo con precisión "suficiente" para el usuario común que no requiere estándares suizos.</td><td>Crisis en el sector inmobiliario comercial que detenga la construcción de nuevos edificios "Smart".</td>
        </tr>
    </tbody>
</table>


### 2.1.2. Estrategias y tácticas frente a competidores.

Se debe incluir las estrategias y tácticas preliminares que aplicará su startup para afrontar las fortalezas y aprovechar las debilidades, así como el contexto de oportunidades y amenazas en relación a la competencia. 

## 2.2. Entrevistas.

En esta sección se aborda la investigación tomando como base la recolección de información en base a entrevistas a representantes de los segmentos objetivo.

### 2.2.1. Diseño de entrevistas.

Esta sección incluye la relación de preguntas principales y complementarias para entrevistas, dirigidas a cada uno de los segmentos. Es importante considerar que debe aplicarse buenas prácticas para diseño de entrevistas. También debe considerar qué tipo de información principal y complementaria necesita recolectar para construir los arquetipos (características demográficas como género, edad, distrito de residencia, estado civil, familia, ocupación, al igual que otras características como personalidad, habilidades, marcas e influencias, dispositivos de preferencia, canales digitales de interacción, objetivos, frustraciones, biografía o background). 

### 2.2.2. Registro de entrevistas.

Para cada segmento se requiere de 3 a 5 entrevistas. Para cada una de las entrevistas se debe indicar la información de nombres, apellidos, edad, distrito, un screenshot de un cuadro de video y el URL del video subido en Microsoft Stream/Clipchamp (es un solo video editado para todas las entrevistas) incluyendo el timing donde inicia la entrevista y su duración. La entrevista debe ser registrada en video, que sirve de evidencia de entrevistas. Para cada entrevista debe redactarse en este informe un resumen, que explique de forma descriptiva las respuestas del entrevistado a las preguntas realizadas. Todas las características objetivas y subjetivas, incluyendo aspectos como personalidad, marcas e influencias, tecnología, canales de interacción, browser, dispositivos, etc. Deben estar incluidas como parte de los resúmenes para cada entrevista. Debe ser evidente que cada característica de los arquetipos que se construirán en base a esta información provienen de datos recolectados. Ver otras indicaciones importantes en el Anexo C. Indicaciones para secciones que incluyen Videos.

### 2.2.3. Análisis de entrevistas.

En esta sección se debe realizar un análisis por cada segmento objetivo, identificando con sustento estadístico (porcentajes) todas las características objetivas y subjetivas que representan los aspectos más comunes de cada segmento y que son necesarios para la construcción de los arquetipos. La fuente de información para este análisis proviene de las entrevistas registradas. Debe evidenciarse que cada característica tiene relación con las entrevistas registradas y los resúmenes realizados para las mismas.

## 2.3. Needfinding.

En esta sección el equipo explica y presenta los artefactos resultantes del proceso de análisis de la información recolectada. Aquí se incluye secciones internas para User Personas, User Task Matrix, User Journey Maps, Empathy Mapping y As-Is Scenario Mapping.

### 2.3.1. User Personas.

En esta sección se presenta el User Task Matrix, que concentra las tareas que los User Persona (que representan a cada segmento) realizan para cumplir sus objetivos. No confundir tareas (tasks) con opciones o características de software, pues las tareas deben ser realizadas por los segmentos independientemente de la existencia de su solución de software. Esta sección inicia con una introducción donde se establece los segmentos que se están considerando. El cuadro debe incluir como columna cada User Persona y para cada una como sub-columnas, la Frecuencia y la Importancia de cada tarea (task). Como filas se colocan las tareas identificadas. Luego del cuadro se realiza una explicación resaltando las tareas con mayor frecuencia e importancia, principales diferencias y coincidencias entre lo realizado por los User Personas. 

### 2.3.2. User Task Matrix.

Se incluye el proceso de Needfinding junto con análisis de la competencia. Las entrevistas se registrarán en video y se editarán para construir el video de evidencia de entrevistas. El análisis de dichas entrevistas servirá de base para la identificación de necesidades y la construcción de los User Persona para cada segmento objetivo, así como la construcción del User Task Matrix, los User Journey Map para los User Persona identificados, así como los Empathy Maps, Big Picture EventStorming y Ubiquitous Language. 

### 2.3.3. User Journey Mapping.

En esta sección se elabora los User Journey Maps (uno por cada User Persona). La sección inicia con una introducción que resume el end-to-end journey que se pretende ilustrar. Debe incluirse capturas de imagen de los diagramas elaborados en la herramienta indicada. En este caso se elabora las versiones As-Is de los User Journey Maps, es decir los journey de cada segmento representado para la situación actual, sin que exista su solución. Cada User Journey Map debe vincularse con el User Persona correspondiente (cuya ficha de User Persona también debe haberse elaborado en la misma herramienta indicada).

### 2.3.4. Empathy Mapping.

En esta sección, el equipo resume el proceso de elaboración y presenta capturas de los Empathy Maps realizados en la herramienta indicada, para cada uno de los User Personas. El proceso de elaboración incluye la preparación, colocar al centro el User Persona. Colocar en la sección correspondiente en la herramienta cada observación de los miembros del equipo sobre el User Persona, buscando responder las preguntas ¿Con quién estamos empatizando? ¿Qué necesita hacer? ¿Qué está diciendo? ¿Qué está viendo? ¿Qué está haciendo? ¿Qué está escuchando? ¿Cómo se siente y qué piensa? Identificar Pains y Gains en base a las preguntas ¿Qué le  14/47 V1.0 preocupa? Y ¿Qué puede ayudar a resolver sus problemas? ¿Qué puede convencerlo de que somos la alternativa correcta? ¿Qué dice?

## 2.4. Big Picture EventStorming.

En esta sección el equipo introduce, resume el proceso realizado por el equipo y presenta capturas y explicaciones de las etapas del Big Picture Event Storming. En una sesión colaborativa, el equipo se enfoca en entender el dominio del negocio en general, plasmando los eventos significativos y sus relaciones. Es una primera aproximación visual de alto nivel que explora el landscape del negocio, identificando procesos clave, exponiendo potenciales problemas u oportunidades. En https://bit.ly/bpes-guide encontrará un Step-by-Step Guide para realizar el proceso.

## 2.5. Ubiquitous Language.

En esta sección el equipo redacta un glosario de términos y conceptos con definiciones utilizadas en el business domain, sin ambigüedad, relacionados al área de especialidad o sector en el que se establecen el problema y la solución. Mantener un glosario de este tipo completo y actualizado, permite que se comuniquen claramente todos los miembros y stakeholders en el equipo. Solo debe incluirse términos del dominio, no términos técnicos del área de ingeniería de software. Los términos deben estar en inglés (puede incluirse adicionalmente el término equivalente en español entre paréntesis). La definición correspondiente al término puede estar en español. Eric Evans habla sobre Ubiquitous Language en su libro Domain-Driven Design: Tackling Complexity in the Heart of Software2 .