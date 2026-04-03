# Capítulo I: Introducción

## 1.1. Startup Profile

### 1.1.1. Descripción de la Startup

Somos Vanana y buscamos identificar la calidad del aire interior en espacios comerciales cerrados de Lima Metropolitana, con el fin de visibilizar esta variable y permitir a los usuarios tomar decisiones informadas sobre su salud.
Para ello implementaremos Clair, un sistema de monitoreo de calidad del aire que integra un sensor PM2.5, con una plataforma tanto móvil como web que ofrece visualización en tiempo real, alertas personalizadas y recomendaciones para mejorar la ventilación.

**Misión:** Fomentar la conciencia y el cuidado de la calidad de aire en espacios comerciales con el fin de mejorar la salud y el bienestar de los usuarios.

**Visión:** Crecer como la plataforma líder en monitoreo de calidad del aire interior en el Perú, promoviendo espacios más saludables.

### 1.1.2. Perfiles de integrantes del equipo

| Foto del estudiante                                                                                  | Nombres y apellidos                     | Código de estudiante | Descripcion                                                                                                                                                                                                                                                             |
|------------------------------------------------------------------------------------------------------|-----------------------------------------|----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <img src="../assets/members/U202319963.jpg" alt="Dante Mateo Aleman Romano" width="100">             | Dante Mateo Aleman Romano               | u202319963           | Soy un desarrollador de 20 años que usa Linux como su sistema operativo principal. Disfruto crear servicios y configurar máquinas, con un fuerte interés en las prácticas de seguridad.                                                                                 |
| <img src="../assets/members/U202319889.jpg" alt="Fabrizio Alessandro Contreras Peralta" width="100"> | Contreras Peralta, Fabrizio Alessandro  | u202319889           | Estudiante de 21 años, disfrutó resolver problemas a través de ideas creativas. Tengo bastante interés por la automatización del desarrollo de proyectos con LLMs, asimismo, por nuevas herramientas emergentes.                                                        |
| <img src="../assets/members/u20231b866.jpeg" alt="Neil Curipaco" width="100">                        | Curipaco Huayllani, Neil Aldrin Wilhelm | U20231B866           | Soy Neil Curipaco Huayllani. Estoy cursando el 7to ciclo de la carrera de Ingeniería de Software en la UPC. Me gusta jugar videojuegos, aprender cosas nuevas, escuchar música y mejorar mis habilidades para ser de ayuda en el equipo de trabajo del que formo parte. |
| <img src="../assets/members/U202121325.jpg" alt="Ian Macavilca Quispe" width="100">                  | Macavilca Quispe, Ian                   | U202121325           | Soy un estudiante de 21 años, con interes en optimización y diseño de Apps Web/Mobile. Me gusta resolver problemas con ideas creativas.                                                                                                                                 |
| <img src="../assets/members/U202119095.jpeg" alt="Josue Gonzalo Paiva Quispe" width="100">           | Paiva Quispe, Josue Gonzalo             | u202119095           | Soy estudiante de Ingeniería de Software, me encuentro cursando el 8vo ciclo y realizando prácticas pre profesionales como fullstack junior web developer                                                                                                               |



## 1.2. Solution Profile

### 1.2.1 Antecedentes y problemática

La calidad del aire se ha consolidado, a través de los años, como uno de los principales retos de salud pública, adquiriendo matices críticos en metrópolis con alta densidad vehicular. En este contexto, Lima figura recurrentemente entre las ciudades con peor calidad del aire en América Latina. Según reportes de monitoreo global, nuestra capital registra promedios de material particulado fino (PM2.5) que superan de forma sostenida las directrices de la Organización Mundial de la Salud (OMS), llegando en determinadas zonas de la ciudad a exceder hasta en nueve veces el límite máximo recomendado de 5 µg/m³ (IQAir, 2024).

La gravedad de esta exposición radica en la naturaleza del PM2.5. Al medir menos de 2.5 micrómetros de diámetro, estas partículas evaden las defensas respiratorias primarias, penetran profundamente en los alvéolos pulmonares y logran ingresar directamente al torrente sanguíneo. Esta infiltración desencadena inflamación sistémica y estrés oxidativo.

A pesar de estas alarmantes cifras, las estrategias de mitigación y evaluación se han enfocado casi exclusivamente en el ámbito macroscópico. Entidades del gobierno operan redes de monitoreo y estaciones meteorológicas a escala metropolitana que evalúan únicamente la contaminación del exterior. Sin embargo, existe un vacío crítico en la medición a nivel micro, específicamente dentro de las edificaciones donde las personas transcurren más del 80% de su tiempo. La evidencia científica deja en claro que la contaminación ambiental se infiltra en los interiores, sumándose a los contaminantes generados por la propia ocupación humana. El mercado peruano aún no ofrece las soluciones tecnológicas necesarias para gestionar esta variable en espacios comerciales.

El problema central radica principalmente en la incapacidad tecnológica y estructural para monitorear, visibilizar y gestionar la calidad del aire dentro de locales comerciales cerrados en Lima, lo que expone a los ocupantes a riesgos sanitarios y deterioros cognitivos. Para estructurar y delimitar la problemática, se aplicó el marco analítico de las 5 ‘W’s y 2 ‘H’s:

1. What (Qué): Existe una carencia significativa de sistemas de monitoreo de aire de grado industrial que sean asequibles para el sector de servicios. Esto convierte a la contaminación interior en un riesgo invisible, presentando problemas graves como la acumulación de dióxido de carbono (CO2) dentro de un ambiente cerrado y la presencia de PM2.5

2. Who (Quién): Los segmentos directamente afectados son los consumidores y usuarios que permanecen tiempos prolongados en espacios cerrados (gimnasios, restaurantes, _coworkings_ y aulas).

3. Where (Dónde): El problema ocurre en espacios comerciales, educativos e institucionales de uso público situados en Lima Metropolitana

4. When (Cuándo): La exposición es un evento continuo, acentuándose mayormente durante las horas de máxima ocupación operativa de los locales (horas pico).

5. Why (Por qué): Existe una alta barrera de entrada tecnológica; los sensores industriales son sumamente costosos. Segundo, a diferencia de las calificaciones de higiene alimentaria, no existe un mecanismo normativo o comercial que obligue a transparentar la calidad del aire, dejando al consumidor sin capacidad de verificar la salubridad del local antes de ingresar.

6. How (Cómo): La problemática se manifiesta de forma silente y progresiva. En recintos de alta densidad y pobre renovación de aire, se asume erróneamente que el ambiente está purificado solo por contar con aire acondicionado.

7. How Much (Cuánto): La infiltración de aire exterior contaminado somete a los usuarios a niveles de PM2.5 hasta 9 veces superiores a lo tolerable. Por otro, la exhalación humana en espacios cerrados dispara rápidamente el CO2 por encima de las 1000 partes por millón (ppm). Según los estándares de la _American Society of Heating, Refrigerating and Air-Conditioning Engineers_, superar este umbral de 1000 ppm degrada el rendimiento cognitivo, altera la concentración e incrementa la fatiga mental de forma significativa (ASHRAE, 2022).


### 1.2.2 Lean UX Process.

#### 1.2.2.1. Lean UX Problem Statements.

El estado actual del monitoreo ambiental en Lima Metropolitana se ha centrado exclusivamente en redes de escala macroscópica para exteriores, donde los administradores de locales comerciales y usuarios carecen de visibilidad sobre la calidad del aire interior (PM2.5 y CO2) y dependen de suposiciones erróneas sobre la eficacia del aire acondicionado.

Lo que los servicios y normativas existentes no logran abordar es la medición a nivel micro en espacios cerrados que, según la OMS (2021) y IQAir (2024), suelen exceder hasta en nueve veces los límites de material particulado fino, ni la gestión de niveles de CO2 que, al superar las 1000 ppm, degradan el rendimiento cognitivo y la salud sistémica de los ocupantes (ASHRAE, 2022; AAP, 2024).

Nuestro producto, Clair, abordará esta brecha mediante un sistema de monitoreo en tiempo real (sensor PM2.5 y plataforma web/móvil) que facilite la visibilización de contaminantes invisibles y permita la toma de decisiones informadas para mejorar la ventilación.

Nuestro enfoque inicial serán los administradores de espacios comerciales cerrados (gimnasios, restaurantes, coworkings) y padres de familia preocupados por la salud respiratoria en distritos de alta densidad vehicular en Lima.

Sabremos que tenemos éxito cuando observemos que el 50% de los locales afiliados logren reducir sus picos de CO2 por debajo del umbral crítico de 1000 ppm mediante acciones correctivas sugeridas por la app, y cuando al menos el 20% de los usuarios recurrentes de dichos locales consulten el estado del aire en la plataforma antes de su permanencia, durante los primeros seis meses de implementación.

#### 1.2.2.2. Lean UX Assumptions.

**User Assumptions**

- Creemos que los usuarios que permanecen en espacios cerrados por largos periodos no son conscientes de la calidad del aire interior, porque no cuentan con información visible ni accesible en tiempo real.
- Creemos que los administradores de espacios comerciales valoran la salud y bienestar de sus clientes, porque esto influye directamente en la percepción de su negocio y en la fidelización
- Creemos que los usuarios prefieren soluciones tecnológicas simples e intuitivas, porque no tienen conocimiento técnico sobre indicadores tecnicos
- Creemos que, si los usuarios reciben información clara y visual sobre la calidad del aire, tomarán decisiones inmediatas para mejorar su entorno.

**User Outcome Assumptions**

- Creemos que, si los usuarios pueden visualizar la calidad del aire en tiempo real, se sentirán más seguros dentro de los espacios que frecuentan, lo que aumentará su confianza en el entorno.
- Creemos que, si los administradores cuentan con datos accesibles sobre la calidad del aire, podrán tomar decisiones operativas para mejorar la ventilación, lo que impactará positivamente en la experiencia del usuario.
- Creemos que, si los usuarios reciben alertas oportunas, modificarán su comportamiento (ventilar, reducir aforo, etc.), lo que contribuirá a mejorar la calidad del aire.

**Business Assumptions**

- Creemos que existe una oportunidad de mercado en Lima Metropolitana, porque actualmente no hay soluciones accesibles de monitoreo de calidad del aire interior.
- Creemos que los negocios están dispuestos a invertir en soluciones que mejoren su reputación, porque la percepción de seguridad y bienestar es un factor diferenciador competitivo.
- Creemos que un modelo de suscripción será viable, porque los usuarios necesitarán acceso continuo a datos, alertas y reportes.
- Creemos que la integración de hardware (sensor) y software (plataforma digital) es viable, porque la tecnología actual permite monitoreo en tiempo real a bajo costo.

**Business Outcome Assumptions**

- Creemos que, si la solución se implementa en espacios comerciales, los negocios mejorarán su percepción de seguridad y confianza frente a los clientes, lo que fortalecerá su posicionamiento.
- Creemos que, si el producto demuestra valor en etapas iniciales, se logrará adopción progresiva en diferentes tipos de locales (gimnasios, restaurantes, coworkings).
- Creemos que el uso continuo de la plataforma generará ingresos recurrentes, porque el servicio depende del monitoreo constante y actualización de datos.

**Feature Assumptions**

- Creemos que un sensor capaz de medir PM2.5 y CO2 en tiempo real es suficiente para generar valor inicial, porque estos son los principales indicadores de calidad del aire interior.
- Creemos que una interfaz basada en indicadores visuales (colores, niveles) facilitará la comprensión del usuario, porque reduce la necesidad de interpretar datos técnicos.
- Creemos que las alertas en tiempo real incentivarán la acción inmediata, porque informan al usuario en el momento en que ocurre el problema.
- Creemos que los reportes históricos serán valorados por los administradores, porque les permitirán demostrar condiciones seguras en sus espacios.
- Creemos que incluir recomendaciones automáticas (ej. abrir ventanas) aumentará el uso de la plataforma, porque guía al usuario sin necesidad de conocimiento previo.

#### 1.2.2.3. Lean UX Hypothesis Statements.

1. Hypothesis Statement #1: **Creemos que** los dueños de locales comerciales empezaran a tomar conciencia sobre el factor de riesgo que representa la calidad del aire en espacios cerrados para sus clientes, **Sabremos** que esto es cierto **Cuando** al menos el 50% de dueños de locales comerciales afiliados a Clair consulten las medidas correctivas tras haber analizado los reportes de calidad del aire en sus locales.
2. Hypothesis Statement #2: **Creemos que** los padres de familia tomaran medidas para mejorar la calidad de sus hogares gracias a Clair **Sabremos** que esto es cierto **Cuando** al menos el 40% de usuarios registrados como padres de familia obtengan una tendencia de decrecimiento en los niveles de PM2.5 y CO2 en el reporte de sus hogares durante los primeros 3 meses de uso.


#### 1.2.2.4. Lean UX Canvas.

/report/assets/lean-ux-canvas usar la plantilla ppt de esta ruta

## 1.3. Segmentos objetivo

| Segmento Objetivo #1:  | Administradores de Establecimientos Públicos y Privados      |
| ---------------------- | ------------------------------------------------------------ |
| Aspectos demográficos  | Sexo: Indistinto<br />Edad: 25 a 50 años<br />Nivel socioeconómico: Sectores que buscan optimizar costos operativos y cumplir con estándares de salubridad) |
| Aspectos geográficos   | Nacionalidad: Peruana<br />Zona geográfica:  Lima Metropolitana, especialmente en áreas de alta afluencia y densidad comercial |
| Aspectos psicográficos | Profesionales orientados a la eficiencia y la seguridad ocupacional que buscan diferenciar su local mediante el bienestar de sus clientes.<br />Valoran la transparencia y la tecnología como herramientas para demostrar que sus espacios son seguros frente a "amenazas invisibles" como el CO2 y el PM2.5.<br />Muestran interés en soluciones de bajo costo que ofrezcan un alto valor reputacional. |
| Aspectos conductuales  | **Necesidad:** Buscan optimizar el uso de sistemas de aire acondicionado y ventilación para reducir riesgos sanitarios y fatiga mental en sus ocupantes.<br />**Uso de herramientas:** Requieren acceso a una Web App para generar reportes históricos que certifiquen la calidad del aire del establecimiento.<br />**Respuesta:** Actúan de forma inmediata ante alertas móviles cuando el CO2 supera las 1000 ppm para evitar el deterioro cognitivo de sus clientes. |

| Segmento Objetivo #2:  | Personas preocupadas por la calidad del aire en el hogar     |
| ---------------------- | ------------------------------------------------------------ |
| Aspectos demográficos  | Sexo: Indistinto<br />Edad: 25 a 50 años<br />Nivel socioeconómico: Hogares con acceso a dispositivos móviles y servicios digitales |
| Aspectos geográficos   | Nacionalidad: Peruana<br />Zona geográfica: Distritos con alta contaminación vehicular o zonas residenciales densas.<br />Departamento: Lima |
| Aspectos psicográficos | Individuos con una mentalidad preventiva que consideran el aire limpio como un factor crítico para la salud de su familia.<br />Sienten desconfianza de la pureza ambiental en zonas urbanas y buscan "visibilizar" los contaminantes invisibles para reducir riesgos sanitarios.<br />Valoran la seguridad y la paz mental que les brinda el monitoreo constante basado en datos reales. |
| Aspectos conductuales  | **Interacción:** Consultan frecuentemente aplicaciones de monitoreo para verificar el estado de su vivienda.<br />**Acción:** Toman decisiones inmediatas ante alertas, como abrir ventanas para reducir el CO2 o cerrarlas ante picos de contaminación externa.<br />**Tecnología:** Prefieren interfaces móviles intuitivas que utilicen indicadores visuales de colores para una comprensión rápida sin requerir conocimientos técnicos. |