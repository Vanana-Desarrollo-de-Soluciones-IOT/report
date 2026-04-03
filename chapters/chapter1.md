# Capítulo I: Introducción

## 1.1. Startup Profile

### 1.1.1. Descripción de la Startup

Somos Vanana y buscamos identificar la calidad del aire interior en espacios comerciales cerrados de Lima Metropolitana, con el fin de visibilizar esta variable y permitir a los usuarios tomar decisiones informadas sobre su salud.
Para ello implementaremos Clair, un sistema de monitoreo de calidad del aire que integra un sensor PM2.5, con una plataforma tanto móvil como web que ofrece visualización en tiempo real, alertas personalizadas y recomendaciones para mejorar la ventilación.

**Misión:** Fomentar la conciencia y el cuidado de la calidad de aire en espacios comerciales con el fin de mejorar la salud y el bienestar de los usuarios.

**Visión:** Crecer como la plataforma líder en monitoreo de calidad del aire interior en el Perú, promoviendo espacios más saludables.

### 1.1.2. Perfiles de integrantes del equipo

| Foto del estudiante                                          | Nombres y apellidos                     | Código de estudiante | Descripcion                                                  |
| ------------------------------------------------------------ | --------------------------------------- | -------------------- | ------------------------------------------------------------ |
| <img src="../assets/members/U202319963.jpg" alt="Dante Mateo Aleman Romano" width="100"> | Dante Mateo Aleman Romano               | u202319963           | Soy un desarrollador de 20 años que usa Linux como su sistema operativo principal. Disfruto crear servicios y configurar máquinas, con un fuerte interés en las prácticas de seguridad. |
| <img src="../assets/members/U202319889.jpg" alt="Fabrizio Alessandro Contreras Peralta" width="100"> | Contreras Peralta, Fabrizio Alessandro  | u202319889           | Estudiante de 21 años, disfrutó resolver problemas a través de ideas creativas. Tengo bastante interés por la automatización del desarrollo de proyectos con LLMs, asimismo, por nuevas herramientas emergentes. |
| <img src="../assets/members/u20231b866.jpeg" alt="Neil Curipaco" width="100"> | Curipaco Huayllani, Neil Aldrin Wilhelm | U20231B866           | Soy Neil Curipaco Huayllani. Estoy cursando el 7to ciclo de la carrera de Ingeniería de Software en la UPC. Me gusta jugar videojuegos, aprender cosas nuevas, escuchar música y mejorar mis habilidades para ser de ayuda en el equipo de trabajo del que formo parte. |
|                                                              | Macavilca Quispe, Ian                   | U202121325           |                                                              |
| <img src="../assets/members/U202119095.jpeg" alt="Josue Gonzalo Paiva Quispe" width="100"> | Paiva Quispe, Josue Gonzalo             | u202119095           | Soy estudiante de Ingeniería de Software, me encuentro cursando el 8vo ciclo y realizando prácticas pre profesionales como fullstack junior web developer |



## 1.2. Solution Profile

### 1.2.1 Antecedentes y problemática

​La calidad del aire se ha consolidado, a través de los años, como uno de los principales retos de salud pública, adquiriendo matices críticos en metrópolis con alta densidad vehicular. En este contexto, Lima figura recurrentemente entre las ciudades con peor calidad del aire en América Latina. Según reportes de monitoreo global, nuestra capital registra promedios de material particulado fino (PM2.5) que superan de forma sostenida las directrices de la Organización Mundial de la Salud (OMS), llegando en determinadas zonas de la ciudad a exceder hasta en nueve veces el límite máximo recomendado de 5 µg/m³ (IQAir, 2024).

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

Contexto

Observación del problema

Impacto

Necesidad insatisfecha

Pregunta de mejora

#### 1.2.2.2. Lean UX Assumptions.

- **User Assumptions:** Necesidades y comportamientos esperados de los usuarios.
- **User Outcome Assumptions:** Beneficios que los usuarios deberían obtener.
- **Business Assumptions:** Modelo de negocio y el entorno de mercado.
- **Business Outcome Assumptions:** Impactos positivos esperados en el negocio.
- **Feature Assumptions:** Funcionalidades específicas y resolución de necesidades.

#### 1.2.2.3. Lean UX Hypothesis Statements.

Creemos

Sabremos

Cuando

#### 1.2.2.4. Lean UX Canvas.

/report/assets/lean-ux-canvas usar la plantilla ppt de esta ruta

## 1.3. Segmentos objetivo

## 

| Segmento Objetivo #1:  | Administradores de Espacios Comerciales y Servicios          |
| ---------------------- | ------------------------------------------------------------ |
| Aspectos demográficos  | Sexo: Indistinto<br />Edad: 25 a 55 años<br />Nivel socioeconómico: Dueños de PYMES o administradores. |
| Aspectos geográficos   | Nacionalidad: Peruana<br />Zona geográfica: Lima Metropolitana (Zonas de alta densidad: Gamarra, Miraflores, Lima Centro).<br />Departamento: Lima |
| Aspectos psicográficos | Emprendedores y administradores preocupados por el bienestar de sus clientes y la productividad de su personal. Valoran la tecnología como un diferenciador competitivo y buscan soluciones de bajo costo pero efectivas. |
| Aspectos conductuales  | Buscan optimizar el uso de aire acondicionado y ventilación. Necesitan reportes (Web App) para demostrar que su local es seguro. Suelen estar en movimiento y requieren alertas en el celular si los niveles de CO2 exceden lo permitido. |

| Segmento Objetivo #2:  | Padres de Familia Preocupados por la Salud                   |
| ---------------------- | ------------------------------------------------------------ |
| Aspectos demográficos  | Sexo: Indistinto<br />Edad: 25 a 45 años<br />Nivel socioeconómico: Medio-Alto, Medio y Medio-Bajo |
| Aspectos geográficos   | Nacionalidad: Peruana<br />Zona geográfica: Distritos con alta contaminación vehicular (ej. San Juan de Lurigancho, Ate, Carabayllo) o zonas residenciales densas.<br />Departamento: Lima |
| Aspectos psicográficos | Personas con un estilo de vida saludable o que tienen hijos/familiares con problemas respiratorios. Son usuarios frecuentes de gadgets tecnológicos y buscan tener el control de la seguridad de su hogar desde el smartphone. |
| Aspectos conductuales  | Monitorean constantemente el estado de su casa mediante apps. Activan/desactivan dispositivos remotamente. Prefieren interfaces móviles sencillas y visuales para tomar decisiones rápidas como abrir ventanas o encender purificadores. |