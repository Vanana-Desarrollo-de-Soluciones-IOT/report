# Capítulo V: Solution UI/UX Design

## 5.1. Style Guidelines.

### 5.1.1. General Style Guidelines.

La identidad visual y la experiencia de usuario de Clair han sido diseñadas bajo un enfoque de minimalismo funcional, priorizando la claridad de la información ambiental y la eficiencia en la respuesta automática. Esta estrategia visual busca reducir la carga cognitiva del usuario, permitiéndole interpretar estados de calidad del aire complejos de manera instantánea. Para garantizar la consistencia en todas las interfaces, se ha tomado como referencia un sistema de diseño basado en principios de Material Design 3, adaptando sus componentes para reflejar una estética tecnológica, limpia y confiable.



<p align="center">
 <img src="https://i.imgur.com/6zjoyOt.png" width="500">
</p>



**Branding y Concepto Visual**

El branding de la solución se fundamenta en la idea de "transparencia y pureza". Los elementos visuales utilizan bordes redondeados y superficies con elevaciones sutiles (*soft shadows*) para evocar una sensación de modernidad y cercanía. El logotipo y la iconografía siguen líneas geométricas simples, asegurando legibilidad incluso en dispositivos de dimensiones reducidas, como las pantallas integradas en el hardware o aplicaciones móviles en condiciones de baja luminosidad.

**Tipografía y Legibilidad**

Para el sistema tipográfico, se ha seleccionado una familia de fuentes de inter y Space Grotesk. La decisión se sustenta en la necesidad de presentar datos numéricos precisos (como niveles de $CO_2$ y PM2.5) que deben ser legibles de un solo vistazo. Se aplica una jerarquía visual estricta mediante variaciones de peso y escala: los valores críticos utilizan cuerpos tipográficos prominentes para atraer la atención inmediata, mientras que la información contextual y de soporte emplea pesos más ligeros para evitar el ruido visual.

**Paleta de Colores y Significado Semántico**

La paleta de colores de Clair no es solo estética, sino funcional y semántica. Se utiliza una base de tonos neutros (blancos técnicos y grises pizarra) para el fondo y la estructura, permitiendo que los colores de estado destaquen. El sistema emplea una escala cromática de seguridad: **verde** para niveles óptimos, **ámbar** para advertencias preventivas y **rojo** para niveles críticos. Estas decisiones de color se basan en convenciones universales de seguridad y salud, garantizando que tanto el **Home User** como el **Facility Admin** comprendan la urgencia de la situación sin necesidad de leer texto adicional.

**Espaciado y Retícula**

Se ha implementado un sistema de espaciado basado en una rejilla de **8px**, lo que garantiza una alineación matemática perfecta entre componentes y una distribución equilibrada del espacio negativo. El uso generoso de márgenes (*white space*) es una decisión deliberada para separar las diferentes métricas de los sensores, evitando la saturación visual en los dashboards de analítica. Este enfoque permite que el usuario se enfoque en los datos más relevantes, facilitando la navegación tanto en interfaces táctiles como de escritorio.

**Tono de Comunicación y Lenguaje**

El tono de comunicación adoptado para Clair se define como **Sereno, Formal y Respetuoso**. Dado que la solución gestiona información crítica relacionada con la salud y la seguridad de las personas, el lenguaje debe transmitir autoridad y precisión técnica sin generar pánico innecesario.

- **Formalidad:** Se utiliza un lenguaje directo y profesional en las notificaciones y reportes.
- **Serenidad:** Ante situaciones críticas, las instrucciones de mitigación se presentan de forma clara y accionable (ej. "Nivel de $CO_2$ elevado. Se recomienda ventilar el área"), manteniendo una comunicación que brinde seguridad al usuario sobre el control que el sistema ejerce sobre el ambiente.

### 5.1.2. Web, Mobile and IoT Style Guidelines.

- **Web Style Guidelines**

- **Mobile Style Guidelines**

- **IoT Style Guidelines**

Para establecer las guidelines de diseño IoT de Clair, es fundamental comprender la metodología de los 12 pasos de diseño de sistemas IoT, un marco de trabajo estructurado propuesto por investigadores de la Universidad de Sannio, Italia (Balestrieri et al., 2018). Esta metodología, presentada en el paper "Research challenges in Measurement for Internet of Things systems" publicado en Acta IMEKO, proporciona un enfoque sistemático y disciplinado para el desarrollo de soluciones IoT, abarcando desde la definición de requisitos del sistema hasta la implementación de interfaces de usuario. Basada en principios de arquitectura en capas (physical, exchange, information y application service layers), esta metodología garantiza la coherencia entre componentes físicos, de comunicación y aplicativos. El equipo de Vanana adopta estos 12 pasos como fundamento metodológico para asegurar que el diseño del hardware de Clair, incluyendo la selección de sensores PM2.5 y CO2, microcontroladores y radio transceivers, así como la experiencia de usuario de la plataforma, respondan a estándares internacionales de calidad, facilitando la escalabilidad, interoperabilidad y mantenibilidad del sistema de monitoreo de calidad del aire. 

<p align="center">
 <img src="https://imgur.com/SgRnp13.png" width="500">
</p>


A continuación, se presenta la aplicación detallada de los 12 pasos de diseño IoT para el prototipo de Clair, estructurada de forma clara y organizada:

**1. Definition of the System Requirements**

| Categoría | Especificación |
|-----------|----------------|
| **Objetivo Principal** | Monitorear calidad del aire interior en espacios comerciales de Lima Metropolitana |
| **Parámetros a Medir** | CO2, NH3, NOx, benzeno, compuestos orgánicos volátiles |
| **Requisitos Funcionales** | • Medición en tiempo real<br>• Visualización local (OLED)<br>• Transmisión WiFi a la nube<br>• Alimentación estable 5V<br>• Capacidad de expansión |
| **Requisitos No Funcionales** | • Tiempo de respuesta < 10 segundos<br>• Consumo optimizado<br>• Rango temperatura: 15-35°C |

**2. Selection of the IoT System Typology**

| Aspecto | Descripción |
|---------|-------------|
| **Tipo de Sistema** | WSN (Wireless Sensor Network) con arquitectura Edge-Cloud híbrida |
| **Topología** | Estrella extendida - múltiples nodos conectados a un punto de acceso WiFi |
| **Procesamiento** | Edge computing básico en ESP32 + Cloud para análisis avanzado |
| **Modo Offline** | Buffer local limitado con sincronización posterior |

**3. Definition of Physical Layer Requirements**

| Componente | Especificaciones Técnicas |
|------------|---------------------------|
| **Sensor MQ-135** | • Detección: CO2, NH3, NOx, alcohol, benzeno, humo<br>• Rango: 10-1000 ppm (CO2)<br>• Voltaje: 5V DC<br>• Calentamiento: 20-30s para estabilización |
| **Display OLED 0.96"** | • Resolución: 128×64 píxeles<br>• Interfaz: I2C (SDA/SCL)<br>• Voltaje: 3.3V-5V<br>• Ángulo visión: 160° |
| **Prototipado** | • 2× Protoboard MB-102 (830 puntos)<br>• 2× Protoboard 400 puntos<br>• Cables macho-macho/hembra-hembra |
| **Condiciones Ambientales** | • Temperatura: 0-50°C<br>• Humedad: <85% sin condensación |

**4. Definition of Exchange Layer Requirements**

| Capa | Protocolo | Descripción |
|-----------|-----------|-------------|
| **Embedded → Edge** | HTTP/REST sobre red local | Comunicación directa entre ESP32 y Edge Station vía WiFi local |
| **Edge → Cloud** | HTTPS/REST (JSON) | Edge Station sincroniza con API Gateway vía Internet |
| **Conectividad** | WiFi 802.11 b/g/n | Integrado en ESP32, conexión al Edge Station local |
| **Formato Datos** | JSON | `device_id`, `timestamp`, `co2_ppm`, `aqi_index`, `status` |
| **Seguridad** | TLS 1.2 | Encriptación en tránsito Edge-Cloud |
| **Frecuencia Transmisión** | • Local HTTP: cada 5 segundos<br>• Edge-Cloud: cada 60 segundos<br>• Modo alerta: inmediato |

**5. Definition of Information Layer Requirements**

| Proceso | Detalle |
|---------|---------|
| **Adquisición Datos** | ADC 12 bits ESP32 (resolución 0.8mV) |
| **Filtrado** | Promedio móvil de 5 muestras |
| **Conversión** | Ecuación de calibración: `ppm = 116.6020682 × (Rs/Ro)^(-2.769034857)` |
| **Detección Umbrales** | CO2 > 1000 ppm = alerta crítica |
| **Estructura JSON** | `device_id`, `timestamp`, `co2_ppm`, `aqi_index`, `status` |
| **Buffer Local** | 100 lecturas en caso de desconexión WiFi |
| **Sincronización** | NTP (Network Time Protocol) |

**6. Definition of Application Service Layer Requirements**

| Interfaz | Funcionalidades |
|----------|----------------|
| **Display OLED Local** | • Valores CO2 ppm en tiempo real<br>• Air Quality Index (AQI) con Air Quality State (OPTIMAL/MODERATE/CRITICAL)<br>• Indicador estado WiFi |
| **Aplicación Web** | • Dashboard con gráficos históricos<br>• Gestión umbrales de alerta<br>• Exportación reportes PDF/Excel |
| **API REST** | • Recepción telemetría<br>• Consulta datos históricos<br>• Configuración remota dispositivo |
| **Roles Usuario** | Administrador de local / Usuario residencial |

**7. Selection of the Architectures of Data Exchange and Information Integration Layers**

| Componente | Tecnología | Función |
|------------|------------|---------|
| **API Gateway** | Spring Cloud Gateway | Enrutamiento, autenticación JWT, rate limiting, entry point único |
| **Platform API** | Spring Boot | Microservicios: IAM, Billing, Device & Space, Air Quality, Alerting, Analytics, Notifications |
| **Edge Station** | Flask (Python) | Gateway local: recepción HTTP de dispositivos, deduplicación, sincronización offline-first HTTPS |
| **Edge Database** | SQLite | Almacenamiento local telemetría, estados, cola de sincronización |
| **Cloud Database** | PostgreSQL | Datos persistentes: usuarios, dispositivos, telemetría, configuraciones |
| **Cache** | Redis | Sesiones, tokens, rate limits, datos temporales |
| **External Services** | Stripe, Resend, Google OAuth | Pagos, notificaciones email, autenticación social |

**8. Selection of the Sensors and the Actuators**

| Componente | Modelo | Especificaciones |
|------------|--------|------------------|
| **Sensor de Aire** | MQ-135 | • Detección: CO2, NH3, NOx, alcohol, benzeno, humo<br>• Voltaje: 5V<br>• Salida: Analógica (0-5V) + Digital (TTL)<br>• Tiempo respuesta: < 10 segundos<br>• Rango: 10-1000 ppm (CO2)<br>• Calentamiento: 20-30s para estabilización |
| **Display Local** | OLED 0.96" I2C SSD1306 | • Resolución: 128×64 píxeles<br>• Dirección I2C: 0x3C o 0x3D<br>• Pines: SDA, SCL<br>• Voltaje: 3.3V-5V tolerante |
| **Prototipado** | Protoboards + Cables | • 2× Protoboard MB-102 (830 puntos)<br>• 2× Protoboard 400 puntos<br>• Cables macho-macho, hembra-hembra, macho-hembra |
| **Actuadores Futuros** | Relés / HVAC Controller | Control ventiladores, actuadores de ventanas (no incluidos en prototipo inicial) |

**9. Selection of the Microcontroller and Radio Transceivers**

| Componente | Especificaciones Técnicas |
|------------|---------------------------|
| **Microcontrolador** | ESP32-WROOM-32 |
| **Procesador** | Dual-core Xtensa LX6 @ 240MHz |
| **Memoria** | 520KB SRAM / 4MB Flash |
| **Conectividad** | WiFi 802.11 b/g/n + Bluetooth 4.2/BLE |
| **GPIOs** | 34 programables |
| **ADC** | 12 bits, 18 canales |
| **Interfaces** | I2C, SPI, UART |
| **Alimentación** | USB Tipo C (5V) o VIN (7-12V) |
| **Radio Transceiver** | WiFi integrado (antena PCB 2dBi, rango 50m interiores) |

**10. Definition of the Data Processing for Each Node and in Cloud**

**A. Procesamiento en Embedded (C++ / ESP32):**

| Paso | Componente | Acción | Frecuencia |
|------|------------|--------|------------|
| 1 | embeddedIoAdapter | Lectura ADC del MQ-135 vía GPIO/I2C | 1 Hz |
| 2 | embeddedTelemetryService | Filtro promedio móvil (5 muestras) + validación rangos | Continuo |
| 3 | embeddedDomainModel | Conversión a ppm (ecuación calibración) | Cada lectura |
| 4 | embeddedDomainModel | Air Quality State Classification (OPTIMAL/MODERATE/CRITICAL) | Cada lectura |
| 5 | embeddedController | Actualización display OLED vía I2C | Cada 2 segundos |
| 6 | embeddedIoAdapter | Envío HTTP POST a Edge Station vía WiFi local | Cada 5 segundos / Inmediato en alerta |

**B. Procesamiento en Edge (Python / Flask):**

| Componente | Función | Almacenamiento |
|------------|---------|----------------|
| edgeIoAdapter | Recepción HTTP POST de Embedded, ingesta telemetría | - |
| edgeProcessingService | Ingesta, deduplicación, normalización de lecturas | SQLite (telemetría snapshots) |
| edgeDomainModel | Reglas de ingesta, validación, batching | SQLite (checkpoints) |
| edgeSyncService | Sincronización offline-first con Cloud vía HTTPS | SQLite (cola sincronización) |
| edgeController | Exposición HTTP endpoints para configuración local | - |

**C. Procesamiento en Cloud (Spring Boot):**

| Bounded Context | Función Principal | Persistencia |
|-----------------|-------------------|--------------|
| **IAM** | Autenticación, autorización, sesiones, OAuth2 | PostgreSQL + Redis |
| **Device & Space Management** | Gestión facilities, espacios, devices, ownership | PostgreSQL |
| **Air Quality Evaluation** | Evaluación telemetría, thresholds, métricas | PostgreSQL |
| **Alerting & Response** | Generación alertas, escalations, acciones correctivas | PostgreSQL |
| **Analytics** | Agregaciones, tendencias, reportes históricos | PostgreSQL |
| **Notifications** | Plantillas, enrutamiento, delivery email vía Resend | PostgreSQL |
| **Billing** | Suscripciones, pagos Stripe, facturas | PostgreSQL + Stripe API |

**Air Quality State Classification (Usado en todos los niveles):**

| CO2 Range (ppm) | Air Quality State | Threshold Level |
|-----------------|-------------------|-----------------|
| < 400 | Optimal | Normal |
| 400 - 1000 | Moderate | Warning |
| > 1000 | Critical | Critical Threshold Exceeded |

**11. Analysis of the Processing Time**

| Operación | Capa | Tiempo Estimado |
|-----------|------|----------------|
| Boot del ESP32 | Embedded | < 500 ms |
| Conexión WiFi (Embedded → Edge) | Embedded | 2-3 segundos |
| Lectura ADC MQ-135 | Embedded | < 10 ms |
| Conversión y validación | Embedded | < 5 ms |
| Actualización display OLED (I2C @400kHz) | Embedded | < 50 ms |
| Envío HTTP POST local (payload ~200 bytes) | Embedded → Edge | < 100 ms |
| Ingesta y procesamiento Edge | Edge | < 200 ms |
| Persistencia SQLite Edge | Edge | < 50 ms |
| Sincronización HTTPS Edge → Cloud | Edge → API Gateway | 1-3 segundos (depende red) |
| Procesamiento API Gateway + Bounded Context | Cloud | < 500 ms |
| Persistencia PostgreSQL | Cloud | < 100 ms |
| **Latencia total Embedded → Cloud** | End-to-end | 3-8 segundos |
| **Latencia Embedded → Edge (local)** | Local network | < 200 ms |
| **Respuesta ante alertas críticas** | End-to-end | < 10 segundos |
| Estabilización sensor MQ-135 | Hardware | 20-30 segundos |
| Frecuencia muestreo efectiva | Embedded | 1 lectura/segundo |
| Frecuencia sincronización Edge-Cloud | Edge | Cada 60 segundos / Inmediato alertas |

**12. Definition of the Graphical User Interface**

**A. Interfaz Embedded Local (Display OLED 0.96"):**

| Sección | Contenido |
|---------|-----------|
| **Área Superior** | Icono WiFi (estado conexión al Edge Station) |
| **Área Central** | Valor CO2 ppm grande (fuente 16px) + Air Quality State |
| **Área Inferior** | "Status: OPTIMAL/MODERATE/CRITICAL" + Timestamp |

**Navegación Display (futuro):**
- Current Reading (valores tiempo real)
- Time Series History (promedio última hora)
- Device Configuration

**B. Interfaz Edge Station (Configuración Local HTTP):**

| Endpoint | Funcionalidad |
|----------|--------------|
| `GET /health` | Estado del Edge Station y dispositivos conectados |
| `GET /telemetry/latest` | Últimas lecturas de todos los sensores |
| `POST /device/configure` | Configuración WiFi, umbrales, frecuencia muestreo |
| `GET /sync/status` | Estado de sincronización con Cloud |

**C. Interfaz Web Application (Angular):**

| Módulo | Funcionalidad |
|--------|--------------|
| **Dashboard** | Time Series History (gráficos líneas), métricas actuales, Facilities overview |
| **Heat Map** | Visualización espacial calidad del aire por Space |
| **Alerting & Response** | Historial Critical Alert, Alert Reminder, Corrective Action |
| **Configuration** | Custom Threshold, Default Threshold, Notification Preferences |
| **Device & Space Management** | Facility setup, Space creation, Device Registration, Device Pairing |
| **Analytics & Reporting** | Time Series History export, tendencias, reportes PDF |
| **Billing** | Trial Subscription, Premium Plan, Freemium Plan |

**D. Interfaz Mobile Application (Flutter):**

| Módulo | Funcionalidad |
|--------|--------------|
| **Home** | Current Reading, Air Quality State, alertas recientes |
| **History** | Time Series History simplificado (24h, 7 días) |
| **Devices** | Lista dispositivos, Device Pairing, Device Registration |
| **Settings** | Custom Threshold, Notification Preferences, perfil usuario |
| **Offline Support** | Lecturas cacheadas en SQLite local |

---


## 5.2. Information Architecture.

### 5.2.1. Organization Systems.

El equipo ha definido sistemas de organización diferenciados para cada componente de la plataforma, asegurando que la disposición del contenido responda a la naturaleza de la interacción del usuario. El objetivo es que la arquitectura sea capaz de manejar desde la simplicidad de una lectura doméstica hasta la complejidad de una red de sensores industriales, manteniendo siempre la coherencia y el orden lógico.

Para la organización visual y la categorización del contenido, se han tomado las siguientes decisiones:

- **Organización Jerárquica (Visual Hierarchy):** Se aplica de manera prioritaria en los dashboards de monitoreo en tiempo real. Se utiliza una jerarquía de "arriba hacia abajo", donde el estado general de la calidad del aire del establecimiento ocupa el nivel superior, seguido por el detalle individual de cada zona y, finalmente, las métricas específicas de cada sensor. Esto permite una rápida identificación de anomalías sin necesidad de navegar por menús profundos.
- **Organización Secuencial (Step-by-Step):** Este sistema se utiliza exclusivamente en los flujos operativos de configuración, tales como el **Onboarding de Dispositivos** y la **Configuración Inicial de Espacios**. Al guiar al usuario mediante una secuencia lógica de pasos, se minimizan los errores de emparejamiento entre el hardware y la aplicación, asegurando que el sistema quede operativo de forma correcta y sencilla.
- **Esquemas de Categorización Cronológica:** Es el método principal aplicado en el módulo de **Analytics & Reporting**. Los eventos de telemetría, el historial de alertas y los reportes semanales se organizan de forma temporal, permitiendo al usuario realizar un seguimiento histórico de la evolución de la calidad del aire e identificar patrones cíclicos de contaminación.
- **Esquemas por Tópicos:** Se implementa en la sección de configuraciones y soporte. La información se agrupa en temas específicos como "Gestión de Dispositivos", "Preferencias de Alertas" y "Seguridad de la Cuenta", facilitando la localización de funciones administrativas que no dependen de una secuencia temporal.
- **Esquemas según Audiencia (Grupos de Usuarios):** La plataforma adapta su contenido según el rol del usuario autenticado. Mientras que el **Home User** visualiza una interfaz simplificada centrada en el bienestar familiar, el **Facility Admin** accede a una organización de datos matricial que permite supervisar múltiples locales y dispositivos de manera simultánea, optimizando la gestión de grandes superficies.

### 5.2.2. Labeling Systems.

El sistema de etiquetado de Clair ha sido diseñado bajo el principio de máxima claridad con el mínimo de palabras, buscando eliminar cualquier ambigüedad técnica que pueda confundir al usuario en momentos de urgencia. Dado que el sistema maneja variables de salud ambiental, las etiquetas funcionan como indicadores semánticos inmediatos que permiten asociar los datos con acciones concretas. Se ha priorizado el uso de verbos de acción y sustantivos descriptivos estándar, asegurando que la terminología sea consistente tanto en el hardware físico como en las interfaces digitales.

Para garantizar una representación de datos simplificada y efectiva, se han definido las siguientes convenciones:

- **Etiquetado de Métricas Ambientales:** En lugar de utilizar nombres químicos complejos, se emplean acrónimos estándar y descripciones breves. Las etiquetas principales son **"CO2"** (Dióxido de Carbono) y **"PM2.5"** (Material Particulado), acompañadas de unidades de medida simplificadas (ppm y µg/m³). Esta asociación directa permite que el usuario relacione el número con el contaminante específico de forma instantánea.
- **Etiquetas de Estado y Salud:** Para representar la calidad del aire de manera cualitativa, se utiliza un sistema de etiquetas unívocas asociadas a rangos de seguridad: **"Óptimo"**, **"Aceptable"**, **"Riesgo"** y **"Crítico"**. Estas etiquetas actúan como el primer nivel de interpretación, permitiendo que el usuario comprenda la situación ambiental sin necesidad de analizar los valores numéricos brutos.
- **Nomenclatura de Navegación y Control:** Se utilizan etiquetas de un solo término para las secciones principales del sistema, tales como **"Inicio"**, **"Sensores"**, **"Zonas"**, **"Alertas"** y **"Planes"**. En los botones de acción, se emplean imperativos claros como **"Vincular"**, **"Editar"**, **"Exportar"** y **"Resolver"**, lo que reduce el tiempo de procesamiento mental durante la navegación.
- **Asociaciones de Identidad y Espacio:** Para la gestión de establecimientos, se establecen etiquetas de asociación lógica que vinculan el hardware con el entorno. Se utilizan términos como **"Local"** para la entidad principal y **"Espacio"** para las subdivisiones internas, permitiendo que el usuario organice su infraestructura bajo una jerarquía familiar y fácil de rastrear.

Este sistema de etiquetado asegura que la plataforma **Clair** hable el mismo lenguaje que sus usuarios, transformando datos sensores complejos en información accionable y comprensible.

### 5.2.3. SEO Tags and Meta Tags

La estrategia de visibilidad de **Clair** se centra en el posicionamiento de la marca como líder en soluciones IoT para la salud ambiental. Para el sitio web y la aplicación web, se han definido etiquetas SEO y Meta Tags que priorizan la relevancia semántica y la autoridad técnica. En el caso de las aplicaciones móviles, se aplican técnicas de ASO (App Store Optimization) diseñadas para mejorar la tasa de conversión y el descubrimiento orgánico en plataformas como Google Play Store y Apple App Store.

**SEO & Meta Tags (Landing Page y Web Application)**

Para las plataformas web, se han asignado valores específicos que buscan capturar el tráfico interesado en monitoreo de aire y automatización inteligente:

- **Title Tag:** `Clair | Smart Air Quality and CO2 Monitoring`
- **Meta Description:** `Protect your home and business health with Clair. A comprehensive CO2 and PM2.5 monitoring system with real-time alerts and smart automated responses.`
- **Meta Keywords:** `Air quality, CO2 sensor, PM2.5 monitoring, environmental health, IoT Peru, ventilation automation, smart air purification.`
- **Author:** `& Team Clair`
- **Robots Tag:** `index, follow`

**ASO Elements (Mobile Applications)**

Para garantizar que la aplicación móvil sea fácilmente localizable por los segmentos objetivo —administradores de establecimientos y personas preocupadas por la salud en el hogar— se han definido los siguientes elementos:

- **App Title:** `Clair: Air & CO2 Monitor`
- **App Subtitle:** `Air quality and IoT alerts.`
- **App Description:** `Clair is the ultimate solution for managing air quality in your spaces. Connect your smart sensors to visualize CO2 and PM2.5 particle levels in real time. Receive critical notifications, generate sanitary compliance reports, and configure automated responses to activate ventilation systems. Ideal for offices, schools, and homes that prioritize well-being and environmental safety.`
- **App Keywords:** `Air quality, CO2 meter, pollution sensor, home health, well-being, remote monitoring, sanitary safety, air purifier.`

Esta configuración asegura que la propuesta de valor de **Clair** sea comunicada con precisión desde el primer contacto del usuario en los resultados de búsqueda o en la tienda de aplicaciones, facilitando el crecimiento de la base de usuarios de manera orgánica.

### 5.2.4. Searching Systems.

El sistema de navegación de **Clair** ha sido diseñado para ser intuitivo y persistente, garantizando que el usuario siempre mantenga la noción de su ubicación dentro de la plataforma y pueda desplazarse hacia sus metas con el mínimo número de clics. La estrategia se basa en una estructura de navegación multidireccional que combina menús globales para la movilidad entre módulos y elementos de navegación contextual para la profundización en los datos ambientales. Se busca que la transición entre el Landing Page informativo y la aplicación operativa sea fluida, reforzando la confianza del usuario en el producto.

Para guiar el recorrido de los usuarios, se han implementado las siguientes técnicas y estructuras:

- **Global Navigation (Barra Principal):** Presente de forma constante en la parte superior o lateral de la interfaz. Permite el salto inmediato entre las funciones núcleo como el Dashboard de monitoreo, la gestión de dispositivos y el módulo de analítica. Esta barra actúa como el ancla del usuario, ofreciendo un camino de retorno siempre visible hacia la pantalla de inicio.
- **Contextual Navigation (Enlaces Internos):** Se utiliza dentro de las tarjetas de información y paneles de control. Por ejemplo, al visualizar el estado de una zona específica, el sistema ofrece enlaces directos para "Ver historial de alertas" o "Ajustar umbrales", permitiendo que el usuario navegue hacia funcionalidades relacionadas sin pasar por el menú principal.
- **Breadcrumbs (Migas de Pan):** Aplicado especialmente en la versión web y en la gestión de infraestructuras complejas por parte del **Facility Admin**. Este sistema permite visualizar la ruta jerárquica recorrida (ej. Local Principal > Piso 2 > Oficina Norte), facilitando el retroceso a niveles superiores de organización de manera lógica.
- **Scrolling Narrativo y CTAs (Landing Page):** En el sitio público, se emplea una navegación vertical guiada. A través de botones de "Llamada a la Acción" (Call to Action) estratégicamente ubicados, se conduce al visitante desde la comprensión del problema (Problem Statement) hacia la adquisición de la solución, eliminando puntos de fricción en el proceso de conversión.
- **Navegación Táctil y Gestos (Mobile Application):** En la aplicación móvil, se prioriza el uso de un menú de pestañas inferior (*Bottom Navigation Bar*) para facilitar el acceso con el pulgar. Además, se integran gestos intuitivos como el *swipe* para cambiar entre diferentes zonas de monitoreo, optimizando la experiencia en dispositivos móviles.

Este enfoque asegura que el recorrido por el contenido de **Clair** no solo sea funcional, sino que también actúe como un facilitador de la eficiencia operativa, permitiendo que la interacción con el sistema sea natural y satisfactoria.

### 5.2.5. Navigation Systems.

Dada la arquitectura de información simplificada y el enfoque en la visualización directa de datos de Clair, el equipo ha optado por un sistema de búsqueda basado en la navegación asistida y el filtrado por categorías en lugar de un motor de búsqueda global por texto. Esta decisión estratégica busca evitar que el usuario se sienta abrumado por un volumen excesivo de herramientas de búsqueda innecesarias, considerando que la interfaz ha sido diseñada para que cada dato sea localizable mediante la exploración lógica de los espacios configurados.

Para garantizar que el usuario nunca se sienta perdido, se han implementado las siguientes soluciones de localización de datos:

- **Segmentación Temporal en Reportes:** Para la consulta de datos históricos en el módulo de analítica, se ofrecen selectores de fecha predefinidos (Día, Semana, Mes). Esta forma de "búsqueda por tiempo" permite que los datos se presenten de forma agregada, facilitando la identificación de tendencias sin requerir consultas técnicas complejas.
- **Visualización de Resultados Pos-Búsqueda:** Una vez seleccionado un filtro o una zona específica, los datos se presentan en tarjetas informativas con una jerarquía visual clara. Los valores de telemetría más recientes (CO2 y PM2.5) se muestran de forma destacada, seguidos por el estado de conectividad del dispositivo, asegurando que la respuesta del sistema sea siempre visual y fácil de interpretar.
- **Landing Page Informativa:** En el sitio web estático, la información se distribuye de manera lineal y secuencial, eliminando la necesidad de un sistema de búsqueda interno. El visitante encuentra los contenidos mediante un flujo narrativo diseñado para cubrir todas sus dudas frecuentes de forma orgánica.

Este enfoque de búsqueda simplificada refuerza el compromiso de **Clair** con una experiencia de usuario directa y eficiente, donde la información no necesita ser buscada activamente porque ya se encuentra organizada de manera intuitiva dentro del flujo de trabajo diario.

## 5.3. Landing Page UI Design.

### 5.3.1. Landing Page Wireframe.

### 5.3.2. Landing Page Mock-up.

## 5.4. Applications UX/UI Design.

### 5.4.1. Applications Wireframes.

### 5.4.2. Applications Wireflow Diagrams.

### 5.4.2. Applications Mock-ups.

### 5.4.3. Applications User Flow Diagrams.

## 5.5. Applications Prototyping.

## 5.6. IoT Device Design



https://imgur.com/z3BEd0f