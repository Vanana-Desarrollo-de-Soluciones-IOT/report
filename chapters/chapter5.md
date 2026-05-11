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

**Web Style Guidelines**

**Comportamiento Responsivo y Sistema de Layout**

**Breakpoints oficiales:**

| Categoría | Breakpoint | Ancho mínimo | Comportamiento principal |
|-----------|------------|--------------|--------------------------|
| Móvil | `sm` | < 600px | Layout de 1 columna, menú hamburguesa, navegación vertical |
| Tablet | `md` | 600px – 1024px | Layout de 2 columnas, sidebar colapsable |
| Escritorio | `lg` | 1024px – 1440px | Layout de 3 columnas, sidebar fija |
| Escritorio amplio | `xl` | > 1440px | Layout de 3-4 columnas, espaciado generoso |

**Referencia visual:**  
Los mockups presentados en la sección 5.4.3 corresponden a resolución `xl` (1920px de ancho). En este punto de quiebre, la interfaz utiliza:
- Sidebar izquierdo expandido con navegación jerárquica (Organizations → Building A → Floor 1/2 → Devices)
- Área principal con grid fluido de tarjetas
- Márgenes laterales de `24px` (3 unidades de 8px)


**Componentes UI Especificados**

**A. Panel de Navegación Jerárquica (Espacios y Dispositivos)**

| Propiedad | Especificación |
|-----------|----------------|
| **Estructura** | Árbol colapsable: Organization → Building → Floor → Device |
| **Indicador de cantidad** | Badge con número de dispositivos (ej. "3 DEVICES") en color neutro |
| **Actualización** | Texto secundario: "Updates every minute" / "Updated 12 seconds ago" |
| **Vistas alternas** | Toggle Grid / List (íconos alineados a la derecha) |
| **Footer de acciones** | Botón "Add Organization" (estilo outline) |

**Especificaciones técnicas:**

```css
.nav-tree {
  padding: 16px 0;
  border-right: 1px solid rgba(10,10,10,0.08);
}

.nav-item {
  padding: 8px 16px;
  border-radius: 8px;
  font-family: 'Inter', sans-serif;
  font-size: 14px;
  transition: background 0.2s ease;
}

.nav-item.active {
  background: rgba(77,132,255,0.08);
  color: #4D84FF;
  font-weight: 500;
}

.device-count-badge {
  background: #F0F0F0;
  border-radius: 16px;
  padding: 2px 8px;
  font-size: 12px;
  font-family: 'Space Grotesk', monospace;
}
```

**B. Tarjeta de Sensor / Dispositivo**

| Elemento | Especificación |
|----------|----------------|
| **Contenedor** | Fondo #FFFFFF, border-radius 16px, sombra sutil `0 2px 8px rgba(0,0,0,0.04)` |
| **Padding interno** | 20px (2.5 unidades de 8px) |
| **Nombre del espacio** | Space Grotesk, 16px, peso semibold (ej. "A101") |
| **Nombre del dispositivo** | Inter, 14px, color secundario (ej. "Clair-01") |
| **Timestamp** | Inter, 12px, color #666, con ícono de reloj |
| **Borde semántico** | Borde izquierdo de 4px según estado: normal (transparente), advertencia (#FFB74D), crítico (#FF4444) |

**Estados de la tarjeta:**

| Estado | Borde izquierdo | Sombra | Comportamiento adicional |
|--------|----------------|--------|--------------------------|
| Normal | `transparent` | `0 2px 8px rgba(0,0,0,0.04)` | - |
| Hover (desktop) | `#4D84FF` | `0 8px 24px rgba(0,0,0,0.08)` | Cursor pointer, transición 0.2s |
| Focus (teclado) | `#4D84FF` | `0 0 0 2px #4D84FF` | Outline offset 2px |
| Crítico | `#FF4444` | `0 2px 12px rgba(255,68,68,0.15)` | - |


**C. Panel de Calidad del Aire (AQI)**

| Componente | Especificación |
|------------|----------------|
| **AQI principal** | Número central: Space Grotesk, 72px, peso bold. Etiqueta debajo (ej. "MODERADO") con color semántico |
| **Métricas individuales** | Grid 2 columnas (en desktop 3 columnas). Cada métrica incluye: nombre, valor, umbral (ej. "Above threshold") |
| **Descripción contextual** | Inter, 14px, color secundario. Texto accionable que indica causa y recomendación |
| **Peer Space Comparison** | Tabla compacta con: nombre del espacio, AQI actual, tendencia (flecha), status badge |
| **Botón de acción principal** | "VIEW ROOT CAUSE ANALYSIS" – estilo link con ícono de flecha |

**Especificaciones de colores semánticos para AQI:**

| Calificación | Rango AQI (ejemplo) | Color | Badge |
|--------------|---------------------|-------|-------|
| Óptimo / Good | 0–50 | #5CFFB1 | Fondo verde claro, texto verde oscuro |
| Aceptable / Moderate | 51–100 | #FFB74D | Fondo ámbar claro, texto ámbar oscuro |
| Riesgo / Unhealthy | 101–150 | #FF8A65 | Fondo naranja claro |
| Crítico / Hazardous | >150 | #FF4444 | Fondo rojo claro, texto blanco (invertido) |



**D. Tabla de Alertas**

| Propiedad | Especificación |
|-----------|----------------|
| **Estructura** | Cabecera fija, filas alternas con separador sutil |
| **Columnas** | ID, Severidad, Espacio, Contaminante, Valor/Límite, Disparo, Estado |
| **Badge de severidad** | "CRITICO" fondo #FF4444 10% + texto #FF4444; "ADVERTENCIA" fondo #FFB74D 10% + texto #B45F1B |
| **Badge de estado** | "ACTIVA" con punto verde pulsante; "PENDIENTE" con punto gris |
| **Acción en fila** | Click en cualquier lugar → abre panel lateral con detalle (ver columna derecha del mockup) |
| **Responsive (móvil)** | La tabla se convierte en lista de tarjetas verticales (cada alerta es una tarjeta colapsable) |


**E. Formularios (Login / Registro)**

| Campo | Especificación |
|-------|----------------|
| **Inputs** | Altura 48px, border-radius 8px, border 1px solid rgba(10,10,10,0.12), padding 0 16px |
| **Label** | Inter, 14px, peso medium, margin-bottom 8px |
| **Placeholder** | Inter, 14px, color #999 |
| **Focus** | Border #4D84FF + outline 2px rgba(77,132,255,0.2) |
| **Error** | Border #FF4444 + mensaje debajo (Inter, 12px, #FF4444) |
| **Checkbox (Términos)** | Custom checkbox 20px, border-radius 4px, checked background #4D84FF |
| **Botón Register/Login** | Fondo #4D84FF, texto blanco, padding 12px 24px, border-radius 8px, ancho 100% |


**F. Reportes y Exportaciones**

| Componente | Especificación |
|------------|----------------|
| **Tarjetas de resumen** | Diario/Semanal/Mensual – fondo #F8F9FA, border-radius 16px, padding 20px |
| **Métrica con tendencia** | Valor grande + ícono de flecha (↑ color #FF4444 si empeora, ↓ color #5CFFB1 si mejora) |
| **Tabla de exportaciones** | Misma especificación que tabla de alertas, con columna "Próximo Envío" |
| **Plan Premium** | Card destacada con borde gradiente (#4D84FF → #5CFFB1), botón CTA primario |
| **Botón de exportación** | Dos variantes: PDF (ícono documento) y CSV/XLSX (ícono hoja de cálculo) |



**Estados de Interacción y Micro-interacciones**

| Interacción | Comportamiento | Animación |
|-------------|----------------|-----------|
| **Hover en tarjeta de dispositivo** | Sombra elevada, borde izquierdo azul | `0.2s ease` |
| **Hover en botón primario** | Fondo #3A6BCC | `0.15s ease` |
| **Click en fila de tabla** | Fondo de fila #F5F7FA | Instantáneo + 0.1s de feedback |
| **Apertura de panel lateral (detalle alerta)** | Slide-in desde derecha, overlay semitransparente | `0.3s cubic-bezier(0.2, 0.9, 0.4, 1.1)` |
| **Toggle Grid/List** | Ícono activo con fondo #4D84FF 10% | Transición de ícono |
| **Actualización de datos** | Skeleton loader en tarjetas (solo primera carga) | Pulso de opacidad `1.5s infinite` |
| **Notificación push (alerta crítica)** | Toast en esquina inferior derecha, auto-cierre a los 8s | Slide-up + fade |



**Accesibilidad (WCAG 2.1 Nivel AA)**

| Requisito | Implementación en Clair Web App |
|-----------|--------------------------------|
| **Contraste de color** | Texto sobre #4D84FF (blanco): ratio 4.8:1. Texto sobre #FFFFFF (gris oscuro): ratio 14:1 |
| **Navegación por teclado** | `:focus-visible` visible en todos los botones, inputs, y tarjetas (outline #4D84FF, offset 2px) |
| **Skip to main content** | Enlace oculto que aparece al hacer Tab: "Saltar al contenido principal" |
| **ARIA labels** | En íconos sin texto: `aria-label="Vista de grilla"`. En gráficas AQI: `aria-describedby="aqi-description"` |
| **Texto alternativo** | En gráficas históricas: descripción textual de la tendencia (ej. "PM2.5 aumentó 15% en los últimos 30 minutos") |
| **Manejo de zoom (200%)** | No pérdida de funcionalidad en 200% zoom. Menús colapsan a hamburguesa antes de romperse |



**Integración con IoT (desde navegador web)**

| Funcionalidad | Estándar técnico | Representación en UI |
|---------------|------------------|----------------------|
| **Datos en tiempo real** | WebSocket (conexión persistente) o HTTP POST cada 5 segundos (Embedded → Edge) | Indicador "Updates every minute" + timestamp "Updated X seconds ago" |
| **Estado de conexión** | Heartbeat cada 30s | Círculo verde (#5CFFB1) en esquina superior derecha. Rojo si desconectado |
| **Comandos a dispositivos** | REST API (POST a endpoint) | Botón "Activar sistema HEPA" en detalle de alerta (sección Alerts & Actions). Feedback de éxito/error con toast |
| **Histórico offline** | IndexedDB para caché local | Mensaje: "Usando datos cacheados. Reconectando..." |
| **Permisos** | Notificaciones push (navegador) | Solicitud al primer inicio. Usuario puede modificar en Preferencias (sección Alerts & Actions) |



**Adaptación Responsiva por Pantalla**

| Pantalla | Desktop (1920px) | Tablet (768px) | Móvil (375px) |
|----------|------------------|----------------|----------------|
| **Space & Devices** | Sidebar + grid de 3 columnas | Sidebar colapsado + grid 2 columnas | Menú hamburguesa + grid 1 columna |
| **Air Quality (AQI)** | AQI central + 2 columnas de métricas | AQI reducido (48px) + 1 columna | AQI (40px) + stack vertical |
| **Alertas** | Tabla completa | Tabla con scroll horizontal | Lista de tarjetas |
| **Reports** | 3 tarjetas horizontales | stack vertical | stack vertical |
| **Login/Register** | Card centrado (400px ancho) | Card centrado (400px) | Card 90% ancho (márgenes 5%) |



**Consideraciones de Rendimiento (Web App)**

| Aspecto | Estándar |
|---------|----------|
| **Imágenes** | WebP con fallback PNG. `srcset` para DPR 2x y 3x |
| **Fuentes** | `font-display: swap` para evitar bloqueo de renderizado |
| **Carga de gráficas** | Lazy loading para gráficas históricas (solo al hacer scroll a la vista) |
| **WebSocket** | Reconexión automática con backoff exponencial (1s, 2s, 4s, max 30s) |
| **Bundle size** | Code splitting por ruta (dashboard, alerts, reports, login) |



**Resumen de Especificaciones para Desarrolladores**

```scss
// Variables globales (CSS custom properties)
:root {
  --primary: #4D84FF;
  --secondary: #5CFFB1;
  --neutral-bg: #FFFFFF;
  --neutral-dark: #0A0A0A;
  --critical: #FF4444;
  --warning: #FFB74D;
  --spacing-unit: 8px;
  --radius-md: 8px;
  --radius-lg: 16px;
  --font-heading: 'Space Grotesk', monospace;
  --font-body: 'Inter', sans-serif;
}

// Breakpoints (SCSS mixins)
@mixin mobile { @media (max-width: 599px) { @content; } }
@mixin tablet { @media (min-width: 600px) and (max-width: 1024px) { @content; } }
@mixin desktop { @media (min-width: 1025px) { @content; } }
```


**Mobile Style Guidelines**

**Comportamiento Responsivo y Sistema de Layout**

**Orientación soportada:**

| Orientación | Soporte | Comportamiento |
|-------------|---------|----------------|
| Portrait (vertical) | **Principal** | Todas las pantallas optimizadas para 375px - 428px de ancho |
| Landscape (horizontal) | Opcional | Rotación bloqueada o redimensionamiento básico (no crítico) |

**Unidad de espaciado base: 4px (4dp en Flutter)**

Siguiendo la grilla de Material Design 3, todos los márgenes, paddings y separaciones son múltiplos de 4px:

| Tamaño | Valor | Uso típico |
|--------|-------|-------------|
| `xs` | 4px | Espaciado mínimo entre elementos inline (ícono y texto) |
| `sm` | 8px | Entre elementos relacionados dentro de una tarjeta |
| `md` | 12px | Entre secciones pequeñas del mismo componente |
| `lg` | 16px | Padding estándar de tarjetas y contenedores |
| `xl` | 24px | Márgenes laterales de pantalla, entre secciones grandes |

**Safe Area (Status Bar integrada):**

Todas las pantallas utilizan el widget `SafeArea` de Flutter para evitar que el contenido se superponga con la status bar (iOS notch, Android barra de estado). El fondo oscuro se extiende detrás de la status bar para mantener la integración visual, mientras que el contenido (logo, títulos, botones) respeta el área segura.

**Alturas táctiles mínimas (Material Design):**

| Elemento | Altura mínima |
|----------|---------------|
| Botones principales (Login, Register, Confirm Selection) | 48px |
| Bottom Navigation Bar (cada ítem) | 56px |
| Items de lista (Select Floor, Settings) | 48px |
| Toggle switch, Slider (área de toque) | 40px |

**Scroll:**

Las pantallas principales (Dashboard, Sensors, Settings) **no implementan scroll vertical** en condiciones normales, ya que todo el contenido cabe dentro del área visible de la pantalla en orientación portrait. En dispositivos de pantalla pequeña (menos de 380px de altura), se permite el scroll únicamente como mecanismo de contingencia.



**Componentes UI Especificados**

**A. Bottom Navigation Bar (Navegación principal)**

| Propiedad | Especificación |
|-----------|----------------|
| Estructura | 3 ítems fijos: Dashboard, Sensors, Settings |
| Íconos | Material Icons (dashboard, sensors, settings) |
| Comportamiento | type: BottomNavigationBarType.fixed |
| Color seleccionado | #4D84FF (azul Clair primario) |
| Color no seleccionado | #9E9E9E (gris medio) |
| Fondo | #1E1E1E (oscuro, ligeramente más claro que el fondo general) |
| Altura total | 56px |
| Elevación | 8px (sombra superior) |

**Nota:** No se implementa comportamiento adaptativo para tablets (migración a sidebar) por tratarse de una app exclusivamente móvil.

**B. Tarjeta de Umbrales (Dashboard)**

| Elemento | Especificación |
|----------|----------------|
| Contenedor | Fondo #2C2C2C, border-radius 16px, padding interno 16px |
| Grid interno | 2 columnas (PM2.5 y CO₂ en fila 1; TEMP y HUMIDITY en fila 2) |
| Nombre del parámetro | Inter, 14px, color #B0B0B0 |
| Valor | Space Grotesk (o Roboto Mono en Flutter), 24px, peso bold, color #FFFFFF |
| Unidad | Inter, 12px, color #808080 (junto al valor o debajo) |

**Estado de advertencia contextual:**

Bajo el grid de umbrales, se muestra un texto de advertencia: "May affect device health" en Inter, 12px, color #FFB74D (ámbar), solo si algún umbral supera el rango óptimo.

**C. Gráfico de Network Stability (Dashboard)**

| Componente | Especificación |
|------------|----------------|
| Título | "NETWORK STABILITY" – Inter, 12px, tracking (letter-spacing) 1px, color #B0B0B0 |
| Gráfico | Línea o área simple (sin interacción táctil), altura 80px |
| Eje X temporal | "00:00" a "24:00" – Inter, 10px, color #808080 |
| Estado general | Badge "EXCELLENT" – fondo #4D84FF 20% de opacidad, texto #4D84FF, Inter 14px, border-radius 16px, padding horizontal 12px, vertical 4px |

**D. Bottom Sheet de Selección de Piso (reemplaza pantalla completa)**

| Propiedad | Especificación |
|-----------|----------------|
| Disparador | Tap en "Sensors" en bottom navigation |
| Forma | Esquinas superiores redondeadas (16px), fondo #1E1E1E |
| Altura | wrap_content (se adapta al contenido, típicamente 40-60% de la pantalla) |
| Título | "Select Floor" – Inter, 16px, peso semibold, padding vertical 16px |
| Lista de opciones | Items de 48px de altura, padding horizontal 16px, separador sutil de 0.5px entre items |
| Opción seleccionable | Texto "Floor A101", "Floor A102", "Floor B101", "Floor B202" – Inter, 16px, color #FFFFFF |
| Botón de confirmación | "CONFIRM SELECTION" – fondo #4D84FF, texto blanco, border-radius 8px, altura 48px, margen 16px |
| Cierre | Tap fuera del bottom sheet o arrastre hacia abajo |

**E. Pantalla de Detalle de Sensor (Sensor Detail)**

| Elemento | Especificación |
|----------|----------------|
| Header de ubicación | "BUILDING: A101", "FLOOR: A101" – Inter, 12px, color #B0B0B0, mayúsculas sostenidas |
| Nombre del dispositivo | "Clair-01" – Space Grotesk, 24px, peso bold |
| Indicador de estado | Ícono 🔋 estático (no representa nivel de batería, solo indica que el dispositivo está encendido). Color #4CAF50 si activo, #FF4444 si inactivo. |
| Tarjetas de métricas | Grid 2x2. Cada tarjeta: fondo #2C2C2C, border-radius 12px, padding 12px |
| Métrica - CONNECTIVITY | Valor "60 DBM" – Space Grotesk, 20px, color #FFFFFF. Subtítulo "CONNECTIVITY" – Inter, 10px, color #B0B0B0 |
| Métrica - UPTIME | Valor "~101 HOURS" – mismo estilo. Subtítulo "UPTIME" |
| Métrica - DEVICE HEALTH | Valor "92 %" – mismo estilo. Subtítulo "DEVICE HEALTH" |
| Métrica - LAST UPDATE | Valor "$ 2 M" – mismo estilo (interpretable como "2 minutes"). Subtítulo "LAST UPDATE" |

**Conectividad IoT:** El estado de conexión en tiempo real se refleja únicamente en la métrica "CONNECTIVITY". No hay indicadores persistentes adicionales en la barra superior.

**Mensaje de reconexión:** Si el dispositivo pierde conectividad, se muestra un SnackBar en la parte inferior con el texto "Dispositivo desconectado. Reconectando..." de duración indefinida hasta recuperar conexión, acompañado de un botón "Reintentar" como acción opcional.

**F. Pantalla de Configuración (Settings)**

| Categoría | Componente | Especificación |
|-----------|------------|----------------|
| ACCOUNT | Texto simple | "Neil Curipaco" – Inter, 16px, color #FFFFFF. Padding vertical 16px. No es interactivo. |
| PREFERENCES | Notificaciones (toggle) | Switch nativo de Flutter. Valor por defecto: true. Color activo: #4D84FF. |
| PREFERENCES | Idioma (dropdown) | DropdownButton nativo. Opciones: "ESPAÑOL", "ENGLISH". Valor por defecto: "ESPAÑOL". |
| DEVICE SETTINGS | Unit System (dropdown) | DropdownButton nativo. Opciones: "METRIC", "IMPERIAL". Valor por defecto: "METRIC". |
| DEVICE SETTINGS | Data Refresh Rate (slider) | Slider nativo con divisiones discretas. Valores: 1, 5, 15, 30, 60 minutos. Valor por defecto: 15. Etiqueta de valor actual visible. |
| SUPPORT & LEGAL | Help Center | Item de lista con texto "Help Center" y flecha. Tap → abre URL o navega a webview. |
| Acción final | LOGOUT | Botón o item de lista con texto "LOGOUT" en color #FF4444. Tap → muestra AlertDialog de confirmación. |

**AlertDialog de Logout:**

| Propiedad | Especificación |
|-----------|----------------|
| Título | "Cerrar sesión" – Inter, 18px, peso medium |
| Mensaje | "¿Estás seguro de que quieres cerrar sesión?" – Inter, 14px |
| Fondo | #2C2C2C |
| Botón Cancelar | Texto "Cancelar", color #B0B0B0, sin acción adicional |
| Botón Confirmar | Texto "Cerrar sesión", color #FF4444. Tap → limpia estado de autenticación y navega a Login |

**G. Pantallas de Autenticación (Login / Register)**

| Campo | Especificación |
|-------|----------------|
| Contenedor principal | Centrado vertical y horizontal. Ancho: 90% de la pantalla (márgenes laterales 5%). |
| Logo | "CLAIR" – Space Grotesk, 32px, peso bold, color #FFFFFF, margin-bottom 24px |
| Subtítulo | "Login to Clair" / "Create an account" – Inter, 14px, color #B0B0B0, margin-bottom 32px |
| Campo Email | TextFormField con keyboardType: email. Label "Email" o placeholder. Altura 48px. |
| Campo Password | TextFormField con texto enmascarado (obscureText) + ícono de visibilidad (ojo) para toggle. |
| Términos y condiciones (Register) | Checkbox nativo + texto enlazado "Acepto los Términos y Condiciones y la Política de Privacidad de Clair". Checkbox color #4D84FF. |
| Botón principal | "Login" / "Register" – fondo #4D84FF, texto blanco, altura 48px, border-radius 8px, ancho 100%. |
| Separador "OR REGISTER WITH" | Texto Inter, 12px, color #808080. Líneas horizontales a los lados. |
| Botón Google | Ícono Google + texto "Google". Fondo #FFFFFF (o #2C2C2C), texto negro (o blanco), border-radius 8px, altura 48px. |
| Enlace de navegación | "Do not have an account? Register" / "Already have an account? Login" – Inter, 14px, color #4D84FF. |


**Estados de Interacción y Micro-interacciones Táctiles**

| Interacción | Comportamiento | Retroalimentación |
|-------------|----------------|--------------------|
| Tap en botón primario | Ejecuta acción inmediata | Ripple effect (Material Design). Cambio de opacidad al 0.8 durante 50ms. |
| Tap en item de lista (Settings, Floor Selection) | Navega o selecciona | Ripple effect, sin cambio de color permanente. |
| Toggle switch | Cambia estado ON/OFF | Animación nativa de Flutter (deslizamiento). Sin haptic feedback. |
| Dropdown | Despliega opciones | Menú nativo desde abajo (Android) o rueda (iOS). |
| Slider (discreto) | Ajusta valor | Thumb se mueve a los puntos de división definidos. Valor actual mostrado en etiqueta. |
| Pull-to-Refresh (Dashboard) | Recarga datos | Indicador circular con animación de carga. |
| Tap fuera de Bottom Sheet | Cierra el modal | Animación de contracción hacia abajo (0.2s). |
| AlertDialog | Confirmación destructiva (Logout) | Diálogo modal. Tap fuera → cierra sin acción. |
| SnackBar (reconexión IoT) | Informa pérdida de conectividad | Aparece desde borde inferior. Permanece visible hasta reconexión. |

**Nota:** No se implementan long press, swipe lateral, ni haptic feedback en la versión actual.

**Accesibilidad (WCAG 2.1 Nivel AA y Material Design)**

| Requisito | Implementación en Clair Mobile |
|-----------|-------------------------------|
| Contraste de color | Texto blanco (#FFFFFF) sobre fondo oscuro (#1E1E1E) → ratio 14:1. Texto gris (#B0B0B0) sobre fondo oscuro → ratio 7:1. |
| Tamaño táctil mínimo | Todos los elementos interactivos (botones, items de lista, toggles) ≥ 48px de altura. |
| TalkBack / VoiceOver | Semantics en Flutter. Etiquetas descriptivas: "Botón de inicio de sesión", "Seleccionar piso A101". |
| Navegación por teclado externo | No aplica (app puramente táctil). |
| Manejo de zoom (200%) | Layout fluido con Flexible y Expanded. En 200% zoom, bottom sheet y diálogos escalan correctamente. |
| Texto alternativo en íconos | Semantics con label descriptivo en bottom navigation items sin texto visible (aunque tienen label textual). |


**Permisos de Notificaciones Push**

| Flujo | Comportamiento |
|-------|----------------|
| Primer inicio | Al instalar y abrir la app por primera vez (post-login), se solicita permiso de notificaciones mediante diálogo nativo del sistema operativo. |
| Rechazo inicial | Si el usuario rechaza, puede habilitarlas más tarde desde Settings del dispositivo (fuera de la app). |
| Settings dentro de la app | El toggle "Notifications" refleja el estado del permiso. Si el usuario intenta activarlo sin permiso, se muestra un diálogo informativo: "Habilita las notificaciones desde Configuración de tu dispositivo". |
| Comportamiento de las notificaciones | Todas las notificaciones (críticas y normales) tienen el mismo comportamiento: suena alerta, aparece en centro de notificaciones, badge en ícono de la app. Sin diferenciación especial. |


**Conectividad IoT y Datos en Tiempo Real**

| Funcionalidad | Estándar técnico | Representación en UI |
|---------------|------------------|----------------------|
| Datos en tiempo real | WebSocket o HTTP polling según refresh rate configurado | Dashboard actualiza valores sin recarga visual. Indicador visual de "última actualización" opcional. |
| Estado de conexión del dispositivo | Heartbeat periódico | Visible solo en Sensor Detail, métrica "CONNECTIVITY" (60 DBM = buena). Si es "0 DBM" o "OFFLINE", se considera desconectado. |
| Pérdida de conectividad | Timeout tras heartbeats consecutivos sin respuesta | SnackBar inferior: "Dispositivo desconectado. Reconectando..." + botón "Reintentar". |
| Recuperación de conexión | Reconexión automática con backoff exponencial (1s, 2s, 4s, max 30s) | SnackBar desaparece automáticamente. Los datos se refrescan en el siguiente ciclo. |
| Refresh manual | Pull-to-Refresh en Dashboard | Fuerza una consulta inmediata a la API/WebSocket. |
| Cache offline | No implementado (diseño simple) | Sin mensajes de datos cacheados. Si no hay conexión, se muestran valores estáticos o "--". |


**Consideraciones de Rendimiento para Flutter**

| Aspecto | Estándar / Recomendación |
|---------|--------------------------|
| Imágenes | Assets locales (formato PNG o WebP). Sin imágenes externas pesadas. |
| Tipografía | Fuentes empaquetadas en assets (Inter.ttf, SpaceGrotesk.ttf). font-weight correctamente mapeado. |
| Animaciones | Evitar repaints innecesarios. Usar AnimatedContainer y AnimatedCrossFade sobre setState extensivo. |
| Bottom Navigation | IndexedStack para mantener estado de cada pestaña (no reconstruir al cambiar de tab). |
| Slider | divisions definido para evitar valores no deseados. onChangeEnd para persistencia, no onChanged en tiempo real. |
| Build context | Evitar contextos largos. Usar BuildContext en widgets estatales (StatefulWidget o Riverpod/Bloc según arquitectura). |
| Tamaño de bundle | Flutter build con optimizaciones para producción. Remove debug painting. |


**Resumen de Especificaciones para Desarrolladores Flutter**

**Tema global (Material 3 oscuro):**

| Propiedad | Valor |
|-----------|-------|
| scaffoldBackgroundColor | #121212 (fondo general) |
| cardColor | #1E1E1E (tarjetas, bottom sheet) |
| primaryColor | #4D84FF (botones, switches, links) |
| colorScheme.secondary | #5CFFB1 (opcional, para estados positivos) |
| colorScheme.error | #FF4444 (logout, desconexión crítica) |
| textTheme.bodyLarge | Inter, 16px, #FFFFFF |
| textTheme.bodyMedium | Inter, 14px, #B0B0B0 |

**Dependencias clave (pubspec.yaml):**

- flutter (SDK)
- material_design_icons_flutter (íconos adicionales)
- shared_preferences (persistir settings: refresh rate, unidades)
- http (API calls)
- web_socket_channel (conexión en tiempo real con IoT)
- flutter_local_notifications (notificaciones push)

**IoT Style Guidelines**

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

**Procesamiento en Embedded (C++ / ESP32):**

| Paso | Componente | Acción | Frecuencia |
|------|------------|--------|------------|
| 1 | embeddedIoAdapter | Lectura ADC del MQ-135 vía GPIO/I2C | 1 Hz |
| 2 | embeddedTelemetryService | Filtro promedio móvil (5 muestras) + validación rangos | Continuo |
| 3 | embeddedDomainModel | Conversión a ppm (ecuación calibración) | Cada lectura |
| 4 | embeddedDomainModel | Air Quality State Classification (OPTIMAL/MODERATE/CRITICAL) | Cada lectura |
| 5 | embeddedController | Actualización display OLED vía I2C | Cada 2 segundos |
| 6 | embeddedIoAdapter | Envío HTTP POST a Edge Station vía WiFi local | Cada 5 segundos / Inmediato en alerta |

**Procesamiento en Edge (Python / Flask):**

| Componente | Función | Almacenamiento |
|------------|---------|----------------|
| edgeIoAdapter | Recepción HTTP POST de Embedded, ingesta telemetría | - |
| edgeProcessingService | Ingesta, deduplicación, normalización de lecturas | SQLite (telemetría snapshots) |
| edgeDomainModel | Reglas de ingesta, validación, batching | SQLite (checkpoints) |
| edgeSyncService | Sincronización offline-first con Cloud vía HTTPS | SQLite (cola sincronización) |
| edgeController | Exposición HTTP endpoints para configuración local | - |

**Procesamiento en Cloud (Spring Boot):**

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

**Analysis of the Processing Time**

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

**Interfaz Embedded Local (Display OLED 0.96"):**

| Sección | Contenido |
|---------|-----------|
| **Área Superior** | Icono WiFi (estado conexión al Edge Station) |
| **Área Central** | Valor CO2 ppm grande (fuente 16px) + Air Quality State |
| **Área Inferior** | "Status: OPTIMAL/MODERATE/CRITICAL" + Timestamp |

**Navegación Display (futuro):**
- Current Reading (valores tiempo real)
- Time Series History (promedio última hora)
- Device Configuration

**Interfaz Edge Station (Configuración Local HTTP):**

| Endpoint | Funcionalidad |
|----------|--------------|
| `GET /health` | Estado del Edge Station y dispositivos conectados |
| `GET /telemetry/latest` | Últimas lecturas de todos los sensores |
| `POST /device/configure` | Configuración WiFi, umbrales, frecuencia muestreo |
| `GET /sync/status` | Estado de sincronización con Cloud |

**Interfaz Web Application (Angular):**

| Módulo | Funcionalidad |
|--------|--------------|
| **Dashboard** | Time Series History (gráficos líneas), métricas actuales, Facilities overview |
| **Heat Map** | Visualización espacial calidad del aire por Space |
| **Alerting & Response** | Historial Critical Alert, Alert Reminder, Corrective Action |
| **Configuration** | Custom Threshold, Default Threshold, Notification Preferences |
| **Device & Space Management** | Facility setup, Space creation, Device Registration, Device Pairing |
| **Analytics & Reporting** | Time Series History export, tendencias, reportes PDF |
| **Billing** | Trial Subscription, Premium Plan, Freemium Plan |

**Interfaz Mobile Application (Flutter):**

| Módulo | Funcionalidad |
|--------|--------------|
| **Home** | Current Reading, Air Quality State, alertas recientes |
| **History** | Time Series History simplificado (24h, 7 días) |
| **Devices** | Lista dispositivos, Device Pairing, Device Registration |
| **Settings** | Custom Threshold, Notification Preferences, perfil usuario |
| **Offline Support** | Lecturas cacheadas en SQLite local |




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

A continuación, se presentan los wireframes y mock-ups para la Landing Page de Clair, enfocada en comunicar de manera efectiva la propuesta de valor del producto y guiar al visitante hacia la conversión.

### 5.3.1. Landing Page Wireframe.

**Home**

<img src="../assets/landing-page-wireframes/WF-Home.png" alt="WF-Home" width="1000">

Presentación principal de Clair Alpha. Este esquema define la jerarquía principal del sitio. En la parte superior, se establece un Hero Section con mensajes claros y botones de conversión inmediata. 
La sección central de Sensory Intelligence utiliza una estructura de tres columnas para presentar las métricas clave (PM2.5, CO2 e Índice de Aire), permitiendo que el usuario entienda el valor del monitoreo de un vistazo. Finaliza con bloques de imagen y texto alternados para explicar la integración del dispositivo en espacios físicos.

**Product**

<img src="../assets/landing-page-wireframes/WF-Product.png" alt="WF-Home" width="1000">

Detalle técnico y funcional del dispositivo. Se enfoca en la arquitectura técnica del dispositivo. Utiliza un layout de rejilla (grid) para organizar las "Clair Specs", donde cada tarjeta contiene un icono, un título y una descripción breve. Este diseño está pensado para descomponer conceptos complejos 
(como sensores láser o procesamiento de datos) en fragmentos de información digeribles. Incluye un pie de página con un CTA de refuerzo para incentivar la compra tras leer las especificaciones.

**Pricing**

<img src="../assets/landing-page-wireframes/WF-Pricing.png" alt="WF-Pricing" width="1000">

Estructura de costos de los servicios de Clair Alpha. La estructura está diseñada para facilitar la comparativa de servicios. Presenta dos contenedores principales que separan el plan gratuito del plan avanzado ("Mesh Network"). 
Cada contenedor detalla mediante una lista de viñetas las funcionalidades incluidas, permitiendo al usuario diferenciar rápidamente entre el monitoreo local y la gestión centralizada multidispositivo. Además, el diseño ofrece una visualización limpia de los costos.

**About**

<img src="../assets/landing-page-wireframes/WF-About.png" alt="WF-About" width="1000">

Sección dedicada a la visión de la empresa y el equipo. En la parte inferior, se reserva un espacio para el "Clair Team", organizando al equipo por etiquetas funcionales (Ingeniería, Diseño, Investigación) para proyectar confianza y multidisciplinariedad


### 5.3.2. Landing Page Mock-up.

**Home**

<img src="../assets/landing-page-mockups/Home.png" alt="MP-Home" width="1000">

Implementación visual final con un estilo minimalista y tecnológico. Se sustituyen los contenedores vacíos por imágenes fotorrealistas que muestran el dispositivo integrado en oficinas.
Los indicadores de calidad del aire ahora incluyen micro-interacciones visuales, como anillos de progreso y estados de color (verde para "Pristine Air"), que permiten una lectura intuitiva y rápida del estado ambiental.

**Product**

<img src="../assets/landing-page-mockups/Product.png" alt="MP-Product" width="1000">

Diseño detallado que muestra los componentes internos del ecosistema. Se detallan los componentes internos mediante una tipografía space grotesk y un espaciado amplio que evita la saturación visual. 
Se han integrado los nombres específicos de los sensores (SCD41 y PMS5003) para dar credibilidad técnica al producto.

**Pricing**

<img src="../assets/landing-page-mockups/Pricing.png" alt="MP-Pricing" width="1000">

Interfaz de suscripción con un enfoque limpio y directo. Se utilizan tarjetas con bordes definidos y botones de acción claros. Los iconos de moneda y los botones de compra (CTA) 
siguen una estética de alto contraste (blanco sobre negro), asegurando que el proceso de selección de plan sea visualmente directo y libre de distracciones.

**About**

<img src="../assets/landing-page-mockups/About.jpg" alt="MP-About" width="1000">

Este mockup utiliza la fotografía de alto impacto como eje central para conectar emocionalmente con el usuario. La sección presenta al equipo multidisciplinario con un diseño elegante que equilibra el espacio en blanco y el contenido textual.


## 5.4. Applications UX/UI Design.
Esta sección está dedicada al diseño de la experiencia de usuario (UX) y la interfaz de usuario (UI) de las aplicaciones que conforman la solución. El objetivo es crear interfaces funcionales, accesibles y visualmente coherentes que respondan a las necesidades y expectativas de los usuarios finales.

### 5.4.1. Applications Wireframes.

En esta sección se presentan los wireframes de las aplicaciones, que muestran el diseño estructural y la disposición de los elementos clave para la experiencia de usuario. 

**Web Application**

**Login**

<img src="../assets/webapp-wf/wf-login.png" alt="wf-login" width="1000">

La interfaz de autenticación presenta un diseño centralizado y minimalista que prioriza la claridad funcional. El wireframe utiliza un contenedor de bordes definidos sobre un fondo neutro, integrando campos de entrada directos para credenciales y un botón de acción de alto contraste, lo que refuerza una estética tecnológica y ordenada coherente con el ecosistema de Clair.

**Register**

<img src="../assets/webapp-wf/wf-register.png" alt="wf-register" width="1000">

El diseño de registro mantiene la coherencia visual mediante una estructura vertical limpia que facilita el flujo de usuario. Este wireframe integra campos de entrada estándar, un selector para términos legales y una opción de autenticación social con Google, logrando un equilibrio entre simplicidad y funcionalidad bajo una estética técnica y minimalista.

**Overview**

<img src="../assets/webapp-wf/wf-overview.png" alt="wf-overview" width="1000">

La interfaz principal despliega un tablero de control avanzado con un estilo "dark mode" que resalta métricas críticas de calidad de aire mediante una jerarquía visual clara. El diseño utiliza tarjetas modulares para organizar contaminantes como PM2.5 y CO₂, integrando gráficos de barras de estado y paneles laterales de alertas en tiempo real, lo que ofrece una experiencia analítica, técnica y altamente funcional para la gestión de múltiples organizaciones.

**Space & Devices**

<img src="../assets/webapp-wf/wf-space1.png" alt="wf-space1" width="1000">

<img src="../assets/webapp-wf/wf-space2.png" alt="wf-space2" width="1000">

La interfaz de gestión de dispositivos presenta una estructura organizada mediante un panel de navegación jerárquico que facilita la administración de organizaciones y espacios. El diseño utiliza tarjetas de inventario detalladas y una vista individual para monitorear el estado técnico de cada sensor, integrando indicadores de conectividad, salud del dispositivo y umbrales personalizados bajo una estética limpia y profesional.

**Air Quality**

<img src="../assets/webapp-wf/wf-airquality.png" alt="wf-airquality" width="1000">

La interfaz de análisis ambiental presenta un tablero detallado que permite la visualización de métricas en tiempo real y periodos históricos mediante selectores de tiempo y ubicación. El diseño integra tarjetas de diagnóstico para múltiples contaminantes, un panel de análisis de causa raíz y una comparativa entre espacios, culminando en una sección de generación de reportes técnicos en formatos PDF y CSV que refuerza el enfoque profesional y orientado a datos del ecosistema Clair.

**Alerts & Actions**

<img src="../assets/webapp-wf/wf-alerts.png" alt="wf-alerts" width="1000">

La interfaz de gestión de alertas ofrece un centro de control operativo que combina el monitoreo crítico con la capacidad de respuesta inmediata. El diseño destaca un gráfico de distribución semanal de incidencias y una tabla detallada de alertas activas, integrando paneles laterales para la configuración de notificaciones, visualización de tendencias específicas por evento y un registro de auditoría, lo que permite una administración proactiva y técnica de las contingencias ambientales en el ecosistema Clair.

**Reports**

<img src="../assets/webapp-wf/wf-reports.png" alt="wf-reports" width="1000">

La interfaz de reportes presenta un panel analítico robusto diseñado para la interpretación de datos estratégicos y el cumplimiento normativo. El wireframe organiza la información mediante tarjetas de resumen diario, semanal y mensual, integrando visualizaciones de correlación de partículas y un gestor de exportaciones automatizado que detalla la frecuencia y el estado de los registros. Este diseño facilita una supervisión integral del ecosistema Clair, permitiendo desde el análisis técnico profundo hasta la generación de resúmenes ejecutivos con una estética limpia y profesional.

**Mobile Application**

**Login**

<img src="../assets/mobileapp-wf/WF-LOGIN.png" alt="wf-Login" width="300">

La interfaz de autenticación móvil adopta un diseño vertical y centrado, adaptado a la ergonomía del pulgar. El wireframe simplifica los elementos a un campo de correo electrónico, un botón de acción primario ("Login") de alto contraste y un enlace textual para el registro de nuevos usuarios. Este enfoque minimalista reduce la carga cognitiva y acelera el acceso a la plataforma, manteniendo la estética limpia y tecnológica característica de Clair en un entorno mobile-first.

**Register**

<img src="../assets/mobileapp-wf/WF-REGISTER.png" alt="wf-Register" width="300">

El flujo de registro en dispositivos móviles prioriza la eficiencia y la seguridad mediante una estructura de pasos clara. El wireframe incorpora campos de entrada para correo electrónico y contraseña, acompañados de un componente de verificación (checkbox) para la aceptación de términos legales. Adicionalmente, se integran botones de autenticación (Google) para facilitar el proceso, culminando con un enlace de navegación para usuarios ya registrados, todo ello dentro de un contenedor de bordes redondeados que sugiere una interfaz amigable y moderna.

**Dashboard**

<img src="../assets/mobileapp-wf/WF-DASHBOARD.png" alt="wf-Dashboard" width="300">

La pantalla principal de la aplicación presenta un panel de control resumido pero altamente informativo, ideal para la supervisión rápida. 

**Sensor Selection**

<img src="../assets/mobileapp-wf/WF-SENSOR-SELECTION.png" alt="wf-Sensor-Selection" width="300">

La interfaz de selección de ubicación o dispositivo utiliza un patrón de navegación jerárquica común en móviles: una lista de selección que ocupa la mayor parte de la pantalla. Este patrón modal o de pantalla dedicada guía al usuario a través de la estructura física de la organización (Edificio → Piso) antes de visualizar datos específicos, reduciendo la complejidad y enfocando la atención en la decisión actual.

**Sensor Detail**

<img src="../assets/mobileapp-wf/WF-SENSOR.png" alt="wf-Sensor" width="300">

La vista de detalle de un sensor específico concentra la información técnica más relevante en una sola pantalla optimizada para consultas rápidas. Este diseño de alta densidad de información pero visualmente ordenado permite a los técnicos y administradores evaluar el estado operativo de un sensor de forma inmediata desde su dispositivo móvil. 

**Settings**

<img src="../assets/mobileapp-wf/WF-SETTINGS.png" alt="wf-Settings" width="300">

La pantalla de configuración sigue el estándar de plataformas móviles (iOS/Android) mediante una vista de lista desplazable (table view) agrupada por categorías funcionales. La presencia de un botón de "LOGOUT" claramente diferenciado al final de la lista refuerza las normas de usabilidad y seguridad en aplicaciones móviles, ofreciendo un control total sobre la sesión del usuario.

**Alerts**

<img src="../assets/mobileapp-wf/WF-ALERTS.png" alt="wf-Settings" width="300">

La pantalla de alertas consolida las notificaciones generadas por el sistema Clair, organizadas por niveles de prioridad para facilitar la atención diferenciada por parte del usuario. Cada alerta presenta un encabezado descriptivo, un mensaje contextual y un par de acciones rápidas que permiten responder de manera inmediata o ignorar la notificación. Refleja una arquitectura de notificaciones que equilibra la urgencia operativa con el mantenimiento programado, siguiendo las mejores prácticas de diseño de centros de control y monitoreo en aplicaciones móviles industriales o de seguridad.

### 5.4.2. Applications Wireflow Diagrams.
Esta sección presenta los diagramas de flujo (wireflows) de las aplicaciones, que ilustran la navegación y las interacciones del usuario entre las diferentes pantallas, facilitando la comprensión del recorrido dentro del sistema.

**User Goals**

| ID | User Goal | Descripción operativa |
|:---:|:---|:---|
| **UG01** | Garantizar la salud ambiental | Mantener un aire fresco y libre de viciamento para que los clientes permanezcan más tiempo en el local. |
| **UG02** | Demostrar salubridad | Contar con evidencia tangible (reportes) de que el local cumple con estándares de aire seguro para clientes y fiscalizaciones. |
| **UG03** | Optimizar la productividad | Evitar que los empleados sufran de fatiga o pérdida de concentración por mala ventilación. |
| **UG04** | Controlar síntomas crónicos | Reducir la frecuencia de episodios de rinitis alérgica, asma o dolores de cabeza asociados al ambiente cargado. |
| **UG05** | Validar acciones preventivas | Saber con certeza si sus hábitos de limpieza y ventilación están funcionando realmente para mejorar la calidad del aire. |
| **UG06** | Crear un refugio seguro | Garantizar que, a pesar de la contaminación exterior de la ciudad, el interior de su hogar sea un espacio de respiración pura. |

**Task Flow para UG01: Garantizar la salud ambiental**

*Mantener un aire fresco y libre de viciamento para que los clientes permanezcan más tiempo en el local.*

| Paso | Acción del usuario | Respuesta del sistema |
|:---:|:---|:---|
| 1 | Usuario abre la aplicación | Muestra Dashboard principal con indicadores de calidad del aire (CO2, VOC, temperatura, humedad) |
| 2 | Usuario visualiza el estado actual del ambiente | Muestra valores en tiempo real y estado general (Normal/Alerta/Crítico) |
| 3 | Sistema detecta niveles elevados de CO2 o VOC | Genera notificación push y alerta visual en el Dashboard |
| 4 | Usuario selecciona "Ver detalles" de la alerta | Muestra pantalla con datos del sensor afectado, historial reciente y nivel de gravedad |
| 5 | Usuario activa una acción correctiva (ej: "Aumentar ventilación") | Sistema registra la acción, ejecuta el comando (si aplica) y confirma la operación |
| 6 | Sistema confirma la mejora en los niveles | Actualiza el Dashboard reflejando el nuevo estado del ambiente |

**Task Flow para UG02: Demostrar salubridad**

*Contar con evidencia tangible (reportes) de que el local cumple con estándares de aire seguro para clientes y fiscalizaciones.*

| Paso | Acción del usuario | Respuesta del sistema |
|:---:|:---|:---|
| 1 | Usuario abre la aplicación | Muestra Dashboard principal |
| 2 | Usuario navega a la sección "Reportes" | Muestra lista de reportes disponibles (diario, semanal, mensual, personalizado) |
| 3 | Usuario selecciona el tipo de reporte deseado (ej: "Semanal") | Muestra pantalla de configuración del reporte (rango de fechas, zonas a incluir) |
| 4 | Usuario confirma la generación del reporte | Sistema recopila los datos del período seleccionado y muestra pantalla de progreso/carga |
| 5 | Sistema completa la generación | Muestra resumen del reporte con gráficos, métricas clave (CO2, VOC, temperatura) y comparativas con estándares |
| 6 | Usuario selecciona "Exportar PDF" o "Compartir" | Sistema genera el archivo PDF y abre opciones de compartir (correo, mensajería, almacenamiento) |
| 7 | Sistema confirma el envío o guardado | Muestra mensaje de confirmación y registra la acción en el historial |

**Task Flow para UG03: Optimizar la productividad**

*Evitar que los empleados sufran de fatiga o pérdida de concentración por mala ventilación.*

| Paso | Acción del usuario | Respuesta del sistema |
|:---:|:---|:---|
| 1 | Usuario abre la aplicación | Muestra Dashboard principal |
| 2 | Usuario accede a la sección "Bienestar por Zona" | Muestra indicadores de calidad del aire organizados por áreas del local (salón, cocina, oficina, etc.) |
| 3 | Usuario identifica una zona con niveles subóptimos | Sistema resalta visualmente la zona (amarillo para atención, rojo para crítica) |
| 4 | Usuario selecciona la zona afectada | Muestra detalle de la zona: valores específicos, duración del estado anómalo y recomendaciones de acción |
| 5 | Usuario programa una acción automática (ej: ventilación programada) | Sistema confirma la programación y muestra la hora estimada de normalización |
| 6 | Sistema detecta que los niveles vuelven al rango óptimo | Envía notificación de mejora al usuario y actualiza el Dashboard |
| 7 | Usuario visualiza el histórico de la zona | Muestra gráfico de evolución de la calidad del aire antes y después de la acción correctiva |

**Task Flow para UG04: Controlar síntomas crónicos**

*Reducir la frecuencia de episodios de rinitis alérgica, asma o dolores de cabeza asociados al ambiente cargado.*

| Paso | Acción del usuario | Respuesta del sistema |
|:---:|:---|:---|
| 1 | Usuario abre la aplicación | Muestra Dashboard del hogar con indicadores de calidad del aire interior |
| 2 | Usuario experimenta un síntoma (ej: estornudos, dolor de cabeza, dificultad respiratoria) | (El usuario inicia el registro de manera proactiva) |
| 3 | Usuario navega a la sección "Registrar Síntoma" | Muestra formulario rápido con opciones de síntoma, intensidad (leve/moderado/grave) y momento de ocurrencia |
| 4 | Usuario selecciona el síntoma y nivel de intensidad, luego guarda el registro | Sistema registra el evento con timestamp y lo vincula a los datos de calidad del aire del mismo momento |
| 5 | Usuario consulta la sección "Correlación Síntomas vs Aire" | Muestra gráfico comparativo que relaciona los episodios de síntomas con picos de CO2, VOC o partículas |
| 6 | Sistema identifica patrones automáticamente | Genera alerta preventiva cuando las condiciones actuales se asemejan a episodios anteriores donde el usuario registró síntomas |

**Task Flow para UG05: Validar acciones preventivas**

*Saber con certeza si sus hábitos de limpieza y ventilación están funcionando realmente para mejorar la calidad del aire.*

| Paso | Acción del usuario | Respuesta del sistema |
|:---:|:---|:---|
| 1 | Usuario abre la aplicación | Muestra Dashboard del hogar |
| 2 | Usuario realiza una acción preventiva en el mundo real (ej: abre ventanas, limpia filtros, enciende purificador) | (El usuario inicia el registro manual) |
| 3 | Usuario navega a la sección "Registrar Acción Preventiva" | Muestra formulario para seleccionar tipo de acción, duración y zona afectada |
| 4 | Usuario completa el formulario y guarda la acción | Sistema registra el evento con timestamp y lo marca en la línea de tiempo de calidad del aire |
| 5 | Usuario consulta la sección "Impacto de mis acciones" (inmediatamente o días después) | Muestra gráfico comparativo que aísla el período antes y después de cada acción preventiva registrada |
| 6 | Sistema evalúa la efectividad de la acción | Muestra indicador cualitativo (Ej: "Abrir ventanas redujo CO2 en un 35% en 20 minutos") y lo almacena en el historial de aprendizaje |

**Task Flow para UG06: Crear un refugio seguro**

*Garantizar que, a pesar de la contaminación exterior de la ciudad, el interior de su hogar sea un espacio de respiración pura.*

| Paso | Acción del usuario | Respuesta del sistema |
|:---:|:---|:---|
| 1 | Usuario abre la aplicación | Muestra Dashboard del hogar con indicador comparativo "Aire Interior vs Aire Exterior" |
| 2 | Usuario visualiza la comparación en tiempo real | Muestra dos medidores lado a lado: calidad interior (datos del sensor Clair) vs calidad exterior (API de contaminación de la ciudad) |
| 3 | Usuario navega a "Configuración de Alertas" | Muestra opciones para definir umbrales personalizados de contaminación exterior (PM2.5, PM10, etc.) |
| 4 | Usuario define umbral máximo deseado para recibir alertas y guarda la configuración | Sistema almacena las preferencias y activa el monitoreo continuo de la API exterior |
| 5 | Sistema detecta que la contaminación exterior supera el umbral definido | Envía notificación push al usuario con recomendación específica (Ej: "Contaminación alta en tu zona. Se recomienda cerrar ventanas y activar purificador") |
| 6 | Usuario consulta el histórico de protección | Muestra gráfico que evidencia cómo, a pesar de picos de contaminación exterior, el interior se mantuvo dentro del rango saludable gracias a las acciones tomadas |

**Web Application**

UG01: Garantizar la salud ambiental

| # | Paso | Acción del usuario | Respuesta del sistema |
|:---:|:---|:---|:---|
| 1 | Usuario accede al Overview | Usuario ingresa a la aplicación y visualiza el Dashboard principal | Muestra indicadores de calidad del aire en tiempo real  y estado general por zonas  |
| 2 | Alerta automática (dentro de Overview) | Ninguna (evento automático del sistema) | Detecta niveles elevados de CO2 o VOC. Aparece una alerta visual dentro del Overview |
| 3 | Ver más (dentro de Overview) | Clic en el botón "Ver más" / "View Details" asociado a la alerta dentro del Overview | Navega a la pantalla Alerts & Actions con el foco en la alerta específica que generó la notificación |
| 4 | Visualizar Alerts & Actions | Visualiza la lista de alertas. La alerta crítica aparece destacada con información contextual | Muestra cada alerta con título, mensaje, botones de acción |
| 5 | Activar respuesta (dentro de Alerts & Actions) | Clic en el botón "Activar respuesta" / "Apply Action" correspondiente a la alerta  | Ejecuta la acción correctiva de inmediato. Muestra toast de confirmación. La alerta se marca como "En proceso" o "Resuelta" |


<img src="../assets/webapp-wireflows/webapp-wflow1.png" alt="webapp-wflow1" width="1000">



**Registration & Onboarding Flow**

<img src="../assets/webapp-wireflows/webapp-wflow1.png" alt="webapp-wflow1" width="1000">

Este recorrido modela la experiencia de los nuevos usuarios que se integran al ecosistema a través de la interfaz Register. El flujo se centra en la simplicidad funcional, guiando al usuario por la creación de cuenta, la validación de datos y la aceptación de términos legales antes de su primer acceso. Al completarse, el sistema facilita una transición fluida hacia el Overview, asegurando que el despliegue inicial de la red de monitoreo comience con una configuración de usuario clara y estructurada.

**Asset & Infrastructure Management Flow**

<img src="../assets/webapp-wireflows/webapp-wflow2.png" alt="webapp-wflow2" width="1000">

Este flujo describe la administración jerárquica de la infraestructura IoT de la organización a través de las vistas de Space & Devices. El usuario navega desde una visión macro de los edificios hacia el control detallado de cada espacio, permitiendo la supervisión técnica individual de dispositivos como los sensores SCD41 y PMS5003. La interfaz facilita el monitoreo de la conectividad y la salud del hardware, garantizando que el despliegue en áreas comerciales o residenciales mantenga una operatividad constante y profesional.

**Detailed Environmental Analysis Flow**

<img src="../assets/webapp-wireflows/webapp-wflow3.png" alt="webapp-wflow3" width="1000">

Este proceso conecta el tablero principal de Overview con el análisis profundo en la interfaz de Air Quality para diagnosticar la salud ambiental de un espacio específico. El usuario puede profundizar en métricas críticas como $CO_2$, $PM2.5$ y compuestos orgánicos volátiles ($VOCs$), utilizando selectores de tiempo para identificar tendencias históricas y causas raíz. El diseño permite comparar la calidad de aire entre distintos sectores de la organización, proporcionando una base científica para la toma de decisiones basada en datos precisos de sensores de alta fidelidad.

**Contingency Response & Alert Flow**

<img src="../assets/webapp-wireflows/webapp-wflow4.png" alt="webapp-wflow4" width="1000">

Este flujo operativo modela la detección y mitigación de anomalías ambientales a través de la interfaz de Alerts & Actions. Se activa ante un disparo de umbral crítico (como niveles altos de material particulado), dirigiendo al usuario a revisar la distribución de incidencias y la severidad del evento en tiempo real. El flujo culmina en la ejecución de acciones sugeridas o el uso del Rules Builder para automatizar respuestas, como la activación de purificadores, asegurando una gestión proactiva ante riesgos en la calidad del aire.

**Data Intelligence & Audit Flow**

<img src="../assets/webapp-wireflows/webapp-wflow5.png" alt="webapp-wflow5" width="1000">

Este flujo se especializa en la interpretación estratégica de datos y la generación de documentación técnica mediante la interfaz de Reports. El usuario interactúa con resúmenes de cumplimiento normativo y mapas de correlación de partículas para evaluar el impacto a largo plazo en la organización. El proceso incluye la configuración de exportaciones automatizadas en formatos PDF y CSV, proporcionando una herramienta de auditoría esencial para certificar que los espacios cumplen con las directrices de salud y seguridad ambiental vigentes.

**Mobile Application**

UG01: Garantizar la salud ambiental

| # | Paso | Acción del usuario | Respuesta del sistema |
|:---:|:---|:---|:---|
| 1 | Usuario accede al Dashboard | Usuario ingresa a la aplicación y visualiza el Dashboard principal | Muestra indicadores de calidad del aire en tiempo real y estado general por zonas |
| 2 | Alerta automática (notificación/mensaje) | Ninguna (evento automático del sistema) | Detecta niveles elevados de CO2 o VOC. Aparece una notificación emergente en la parte superior de la pantalla |
| 3 | Visualizar Alerts | Usuario ingresa a la lista de alertas. La alerta crítica aparece destacada con información contextual | Muestra cada alerta con título, mensaje, botones de acción |
| 4 | Activar respuesta (dentro de Alerts) | Tap en el botón "Activar respuesta" / "Apply Action" correspondiente a la alerta | Ejecuta la acción correctiva de inmediato. Muestra toast o snackbar de confirmación. La alerta se marca como "En proceso" o "Resuelta" |

<img src="../assets/mobileapp-wireflows/mobileapp-wflow1.png" alt="mobileapp-wflow1" width="600">


**Main Monitoring & Location Selection Flow**

<img src="../assets/mobileapp-wireflows/mobileapp-wflow1.png" alt="mobileapp-wflow0" width="1000">

Este wireflow ilustra el recorrido principal de monitoreo, comenzando desde el Dashboard como punto de entrada tras la autenticación. Desde esta vista, el usuario puede navegar mediante la bottom tab bar hacia la sección Sensors (Sensores). Al acceder a la vista de Sensors, el sistema presenta la pantalla de Sensor Selection, que lista jerárquicamente los espacios disponibles. El usuario selecciona una opción y confirma mediante el botón "CONFIRM SELECTION", lo que desencadena la navegación hacia la vista Sensor Detail. El wireflow demuestra cómo la navegación por pestañas inferiores y la selección jerárquica de ubicaciones se combinan para ofrecer un recorrido eficiente desde la supervisión global hasta el diagnóstico de cada sensor.

**Device Management & Settings Flow**

<img src="../assets/mobileapp-wireflows/mobileapp-wflow2.png" alt="mobileapp-wflow0" width="1000">

Este wireflow representa el recorrido de gestión de preferencias de usuario y configuración del sistema, fundamental para la personalización de la experiencia móvil. El flujo puede iniciar desde cualquier pantalla principal (Dashboard o Sensor Detail), accediendo a la sección Settings a través de la bottom tab bar. Desde cualquier punto dentro de Settings, el usuario puede navegar hacia otras secciones principales (Dashboard, Sensors) mediante la barra inferior, o bien ejecutar la acción de cierre de sesión "LOGOUT". Al pulsar "LOGOUT", el sistema redirige al usuario hacia la pantalla Login, cerrando su sesión de forma segura. Este wireflow evidencia cómo la aplicación móvil ofrece un control completo sobre las preferencias del sistema y la gestión de cuenta, manteniendo una navegación coherente y accesible en todo momento.


### 5.4.3. Applications Mock-ups.

**Web Application**

**Login**

<img src="../assets/webapp-mockup/LOGIN.png" alt="LOGIN" width="1000">

La interfaz de inicio de sesión presenta una implementación visual final con un estilo sofisticado, minimalista y tecnológico. El mockup utiliza un fondo oscuro profundo que resalta un contenedor de bordes sutiles y el logotipo central de Clair, integrando campos de entrada oscuros con íconos descriptivos y un botón de acción principal de contraste moderado, logrando una estética sobria y profesional coherente con la identidad de la marca.

**Register**

<img src="../assets/webapp-mockup/CREATE-ACCOUNT.png" alt="CREATE-ACCOUNT" width="1000">

La interfaz de creación de cuenta presenta una implementación visual final sofisticada, minimalista y tecnológica, en coherencia con el diseño de login. El mockup utiliza un fondo oscuro profundo que resalta un contenedor de bordes sutiles y el logotipo de Clair, integrando campos de entrada oscuros con íconos descriptivos y un botón de acción principal de contraste moderado. El diseño incorpora además selectores de términos legales y una opción de autenticación social con Google, logrando una estética sobria y profesional.

**Overview**

<img src="../assets/webapp-mockup/OVERVIEW.png" alt="OVERVIEW" width="1000">

El tablero principal presenta una implementación visual final con un estilo minimalista y tecnológico, utilizando un fondo oscuro para resaltar los indicadores de calidad de aire. El diseño organiza métricas críticas como el índice de calidad de aire (AQI) y contaminantes específicos ($CO_2$, $PM2.5$) mediante tarjetas modulares de alto contraste, integrando paneles de alertas y acciones en tiempo real que refuerzan una estética técnica y funcional para el ecosistema Clair.

**Space & Devices**

<img src="../assets/webapp-mockup/SPACE&DEVICES1.png" alt="SPACE&DEVICES1" width="1000">

<img src="../assets/webapp-mockup/SPACE&DEVICES2.png" alt="SPACE&DEVICES2" width="1000">

<img src="../assets/webapp-mockup/SPACE&DEVICES3.png" alt="SPACE&DEVICES3" width="1000">

La interfaz de gestión de dispositivos se presenta con un estilo "dark mode" de alta fidelidad que optimiza la supervisión técnica de los activos. El diseño emplea una arquitectura modular mediante tarjetas interactivas que permiten alternar entre vistas de cuadrícula y lista, integrando un panel de detalle profundo para cada sensor donde se visualizan métricas de conectividad y umbrales operativos. Esta implementación logra una estética tecnológica sofisticada que facilita la administración jerárquica de espacios y organizaciones en el ecosistema Clair.

**Air Quality**

<img src="../assets/webapp-mockup/AIR-QUALITY.png" alt="AIR-QUALITY" width="1000">

La interfaz de análisis ambiental presenta una implementación visual final sofisticada con un estilo "dark mode" que jerarquiza los datos mediante acentos de color y tipografía técnica. El mockup integra un gráfico circular progresivo para el índice de calidad de aire, tarjetas detalladas para parámetros específicos como $PM2.5$ y $CO_2$, y una sección de comparativa entre espacios, culminando en un centro de reportes especializado que refuerza la capacidad analítica y profesional del sistema Clair.

**Alerts & Actions**

<img src="../assets/webapp-mockup/ALERTS&ACTION.png" alt="ALERTS&ACTION" width="1000">

La interfaz de alertas presenta una implementación visual final sofisticada en "dark mode" que centraliza el monitoreo crítico y las respuestas automatizadas del sistema. El diseño destaca un gráfico de barras apiladas para la distribución de incidencias por severidad y una tabla de alertas activas con estados en tiempo real. La sección integra un constructor de reglas lógicas ("Rules Builder") y paneles laterales para la gestión de preferencias, detalles de eventos específicos con sugerencias de acciones automatizadas y un registro detallada de auditoría, consolidando una estética técnica y profesional para la gestión proactiva de Clair.

**Reports**

<img src="../assets/webapp-mockup/REPORTS.png" alt="REPORTS" width="1000">

La sección presenta una implementación visual final sofisticada que transforma datos complejos en resúmenes estratégicos de cumplimiento. El diseño utiliza tarjetas de resumen temporal (diario, semanal y mensual) con tipografía técnica y acentos cromáticos para destacar tendencias de contaminantes como $CO_2$ y $PM2.5$. El mockup integra visualizaciones de correlación viento-partículas y un panel de gestión de exportaciones programadas, manteniendo una estética de "dark mode" profesional que refuerza el valor analítico del ecosistema Clair.

**Mobile Application**

**Login**

<img src="../assets/mobileapp-mockup/LOGIN.png" alt="LOGIN" width="300">

La pantalla de autenticación presenta una implementación visual final de estilo sobrio y corporativo, con fondo oscuro uniforme y el logotipo de Clair centrado en la parte superior. El mockup dispone campos de entrada de bordes redondeados con etiquetas flotantes o internas, acompañados de un botón de acción primaria ("Login") de color de contraste moderado que ocupa el ancho completo. Un enlace textual secundario ("Register") permite la navegación al flujo de creación de cuenta, manteniendo una estética limpia, profesional y alineada con la identidad tecnológica de la marca en el ecosistema móvil.

**Register**

<img src="../assets/mobileapp-mockup/REGISTER.png" alt="mobile-register" width="300">

La interfaz de registro mantiene la coherencia visual con la pantalla de login, utilizando un fondo oscuro y una tarjeta central que organiza el contenido de forma vertical. El mockup integra campos de entrada para correo electrónico y contraseña, este último con un indicador visual de caracteres enmascarados ("●●●●●●●"), acompañados de un componente de verificación para la aceptación de términos y condiciones. El botón de registro principal se complementa con una opción de autenticación ("Google")mediante un contenedor secundario. Finalmente, un enlace "Login" dirige a los usuarios ya registrados, completando un flujo de alta eficiente y visualmente consistente.

**Dashboard**

<img src="../assets/mobileapp-mockup/DASHBOARD.png" alt="mobile-dashboard" width="300">

La pantalla principal de la aplicación presenta un tablero de control resumido que prioriza los indicadores críticos de calidad del aire y el estado de la red. Este diseño permite una supervisión inmediata de la salud ambiental y de red desde el primer vistazo.

**Sensor Selection**

<img src="../assets/mobileapp-mockup/SENSOR-SELECTION.png" alt="mobile-sensor-selection" width="300">

La interfaz de selección de piso o ubicación adopta un patrón de lista modal que cubre la mayor parte de la pantalla, facilitando la elección en contextos de navegación jerárquica. El mockup muestra un título superior "Select Floor" seguido de una serie de opciones textuales presentadas como botones o celdas de alto contraste y fácil pulsación. Un botón de acción primaria anclado en la parte inferior, "CONFIRM SELECTION", permite validar la elección y avanzar en el flujo. Este diseño es ideal para espacios con múltiples niveles o edificios, reduciendo pasos y errores en la selección.

**Sensor Detail**

<img src="../assets/mobileapp-mockup/SENSOR.png" alt="mobile-sensor-detail" width="300">

La vista de detalle de un sensor específico concentra información técnica operativa en una pantalla optimizada para diagnóstico rápido. Este diseño ofrece una experiencia de monitoreo técnico completa pero accesible en formato móvil.

**Settings**

<img src="../assets/mobileapp-mockup/SETTINGS.png" alt="mobile-settings" width="300">

La pantalla de configuración sigue el estándar de plataformas móviles mediante una vista de lista desplazable (table view) agrupada por categorías funcionales. El mockup organiza las opciones en secciones claramente diferenciadas: "ACCOUNT", "PREFERENCES", "DEVICE SETTINGS" y "SUPPORT & LEGAL". Finalmente, un botón "LOGOUT" claramente diferenciado para el cierre la sesión. 


### 5.4.4. Applications User Flow Diagrams.

Esta sección presenta los diagramas de flujo de usuario, que ilustran las rutas y procesos que siguen los usuarios dentro de las aplicaciones, facilitando la comprensión de la navegación y las interacciones clave

**Web Application UserFlow**

**Acquisition & Authentication**

UG-W01: Acceder al ecosistema digital desde la plataforma pública

<img src="../assets/webapp-userflows/webapp-uflow0.png" alt="webapp-uflow0" width="1000">

El usuario accede a la Landing Page de Clair, donde visualiza la propuesta de valor y la arquitectura del sistema. Tras interactuar con el botón principal de "Get Started", es redirigido a la interfaz de Login. Una vez allí, ingresa sus credenciales de acceso para validar su identidad y acceder al panel de control centralizado de la organización.

**Registration & Onboarding**

UG-W02: Crear una cuenta y configurar el perfil inicial

<img src="../assets/webapp-userflows/webapp-uflow1.png" alt="webapp-uflow1" width="1000">

El usuario nuevo selecciona la opción de registro desde la Landing Page y visualiza el formulario en CREATE-ACCOUNT. Completa los campos de correo y contraseña, acepta los términos y condiciones de Clair y opta por la autenticación social si lo prefiere. Tras confirmar sus datos, el sistema lo redirige al flujo de bienvenida para iniciar la configuración de su red de monitoreo.

**Asset & Infrastructure Management**

UG-W03: Administrar jerárquicamente edificios, espacios y dispositivos

<img src="../assets/webapp-userflows/webapp-uflow2.png" alt="webapp-uflow2" width="1000">

El administrador accede a la sección "Space & Devices" desde el menú lateral para visualizar la lista de organizaciones. Selecciona un edificio específico (ej. Building A) y navega por los niveles hasta encontrar un espacio determinado, como se observa en wf-space1.png. Desde allí, elige un sensor individual (ej. Clair-01) para revisar su estado de conexión, salud técnica y configurar los umbrales operativos detallados en Space&Devices.

**Web Application UserFlow Detailed Environmental Analysis**

UG-W04: Consultar métricas detalladas y diagnóstico de calidad de aire

<img src="../assets/webapp-userflows/webapp-uflow3.png" alt="webapp-uflow3" width="1000">

Desde el panel principal, el usuario selecciona la opción "Air Quality" para profundizar en el estado de un área específica. Utiliza los selectores para filtrar por local, espacio y dispositivo, visualizando el índice de calidad de aire en tiempo real y el impacto de contaminantes como $PM2.5$ y $CO_2$. Finalmente, revisa el análisis de causa raíz para comprender qué factores externos, como el tráfico o el sistema HVAC, están afectando el entorno.

**Web Application UserFlow Contingency Response & Alerts**

UG-W05: Gestionar alertas críticas y ejecutar respuestas automatizadas

<img src="../assets/webapp-userflows/webapp-uflow4.png" alt="webapp-uflow4" width="1000">

El usuario ingresa a la sección de "Alerts & Response" para monitorear las anomalías detectadas en las últimas 24 horas. En la vista Alerts&Actions, revisa la severidad de las alertas activas y consulta el historial de eventos. Utiliza el "Rules Builder" para definir acciones automáticas (ej. activar purificadores ante exceso de $CO_2$) o ejecuta respuestas rápidas sugeridas por el sistema para mitigar riesgos ambientales de forma inmediata.

**Web Application UserFlow Data Intelligence & Audit**

UG-W06: Generar reportes de cumplimiento y exportar datos históricos

<img src="../assets/webapp-userflows/webapp-uflow5.png" alt="webapp-uflow5" width="1000">

El usuario accede al módulo de "Reports" para evaluar el rendimiento histórico de la red de sensores. En la interfaz de Reports, analiza los resúmenes de cumplimiento diario, semanal y mensual, comparando los datos obtenidos con las directrices internacionales de salud. Posteriormente, configura la generación automática de archivos PDF o CSV para ser enviados a destinatarios específicos, asegurando la trazabilidad de los datos para auditorías legales.

**Resumen de User Flows - Web Application**

| ID | Objetivo de Usuario | Pantallas Involucradas | Acción Principal |
|----|---------------------|------------------------|------------------|
| UG-W01 | Acceder al ecosistema digital desde la plataforma pública | Landing Page → Login | Autenticación de credenciales |
| UG-W02 | Crear una cuenta y configurar el perfil inicial | Landing Page → Register → Dashboard | Registro y onboarding |
| UG-W03 | Administrar jerárquicamente edificios, espacios y dispositivos | Space & Devices → Sensor Detail | Selección jerárquica y configuración |
| UG-W04 | Consultar métricas detalladas y diagnóstico de calidad de aire | Air Quality → Filtros → Análisis | Visualización de contaminantes y causa raíz |
| UG-W05 | Gestionar alertas críticas y ejecutar respuestas automatizadas | Alerts & Response → Rules Builder | Monitoreo de anomalías y acciones automáticas |
| UG-W06 | Generar reportes de cumplimiento y exportar datos históricos | Reports → Configuración de exportación | Generación de PDF/CSV para auditorías |

**Mobile Application UserFlow**

**Acquisition & Authentication**

**UG-M01:** Iniciar sesión o crear una cuenta desde la aplicación móvil

<img src="../assets/mobileapp-userflows/mobileapp-uflow0.png" alt="mobile-uflow1" width="1000">

El usuario accede a la pantalla de Login de la aplicación móvil de Clair, donde visualiza los campos de ingreso de credenciales y el enlace de registro. Si ya posee una cuenta, introduce su correo electrónico y contraseña, y pulsa el botón "Login" para ser redirigido directamente al Dashboard de monitoreo. Si es un usuario nuevo, pulsa el enlace "Register" y navega hacia la pantalla de creación de cuenta. En Register, completa el formulario con correo electrónico y contraseña (visualmente enmascarada), acepta los términos y condiciones de Clair mediante verificación, y puede optar por la autenticación social con Google como alternativa de registro rápido. Tras confirmar sus datos correctamente, el sistema valida la información y redirige al usuario autenticado hacia el Dashboard, permitiéndole iniciar el monitoreo de su red de sensores desde el primer acceso.

**Location Selection & Sensor Monitoring**

**UG-M02:** Seleccionar una ubicación y visualizar el estado detallado de un sensor

<img src="../assets/mobileapp-userflows/mobileapp-uflow1.png" alt="mobile-uflow2" width="1000">

El usuario, una vez autenticado en el Dashboard, puede navegar a la sección de gestión de sensores utilizando la barra inferior. Al pulsar la pestaña "Sensors", accede a la pantalla de selección de ubicación, donde se despliega una lista jerárquica de los espacios disponibles en su organización. El usuario selecciona la ubicación deseada y confirma su elección mediante el botón "CONFIRM SELECTION". El sistema entonces navega hacia la vista detallada del sensor, donde se presentan métricas técnicas críticas del dispositivo. Este flujo permite al usuario móvil realizar un monitoreo profundo y contextualizado, desde la selección jerárquica del espacio hasta el diagnóstico granular del estado operativo de cada sensor.

**User Preferences & System Configuration**

**UG-M03:** Configurar preferencias de usuario y ajustes del sistema

<img src="../assets/mobileapp-userflows/mobileapp-uflow2.png" alt="mobile-uflow3" width="1000">

El usuario accede a la pantalla de Settings mediante la barra inferior desde cualquier vista principal de la aplicación. Dentro de la interfaz de configuración, organizada en categorías funcionales, el usuario puede gestionar múltiples aspectos de su experiencia. Finalmente, si el usuario desea cerrar sesión de forma segura, pulsa el botón "LOGOUT", confirma la acción, y el sistema lo redirige automáticamente a la pantalla Login. Todos los ajustes se guardan de forma inmediata al ser modificados, ofreciendo una experiencia de configuración fluida, intuitiva y sin fricciones, adaptada a los estándares de usabilidad de plataformas móviles.

**Resumen de User Flows - Mobile Application**

| ID | Objetivo de Usuario | Pantallas Involucradas | Acción Principal |
|----|---------------------|------------------------|------------------|
| UG-M01 | Iniciar sesión o crear una cuenta desde la aplicación móvil | Login → Register → Dashboard | Autenticación de credenciales o registro con verificación de términos |
| UG-M02 | Seleccionar una ubicación y visualizar el estado detallado de un sensor | Dashboard → Sensors → Sensor-Selection → Sensor Detail | Navegación por bottom tab, selección jerárquica y diagnóstico técnico |
| UG-M03 | Configurar preferencias de usuario y ajustes del sistema | Settings → (Preferences / Device Settings / Support) → Login | Gestión de notificaciones, idioma, unidades, frecuencia de actualización y cierre de sesión |

## 5.5. Applications Prototyping.

En esta sección se presentan los prototipos interactivos de las aplicaciones, que permiten visualizar y probar la experiencia de usuario antes del desarrollo final. Incluye enlaces a prototipos navegables para las versiones web y móvil.

**Web Application Prototype**

El prototipo de la aplicación web muestra la estructura general de navegación, el diseño de las principales vistas y las funcionalidades clave que tendrá la plataforma. Permite simular el flujo de navegación de los usuarios y visualizar cómo interactúan con los distintos módulos del sistema.

<img src="../assets/prototypes/webapp-proto.jpg" alt="webapp-proto" width="1000">

Web Application Prototype: https://sl1nk.com/1a68tor

**Mobile Application Prototype**

El prototipo de la aplicación móvil representa la materialización interactiva de los wireframes y mockups diseñados para dispositivos móviles. Este prototipo simula la experiencia táctil del usuario final, permitiendo validar la ergonomía y la coherencia entre las diferentes secciones operativas del sistema Clair en formato móvil.

<img src="../assets/prototypes/mobileapp-proto.png" alt="webapp-proto" width="300">

Mobile Application Prototype:  https://sl1nk.com/s0e7d73

## 5.6. IoT Device Design

El siguiente diagrama presenta el diseño inicial del dispositivo IoT Clair, representando la configuración física y las conexiones entre los componentes de hardware seleccionados para el prototipo.

<p align="center">
  <img src="https://i.imgur.com/TCbXtAq.png" alt="Diseño inicial del prototipo Clair - Cirkit Designer" width="800">
</p>

El esquema fue desarrollado en **Cirkit Designer** (https://app.cirkitdesigner.com/), una plataforma web para diseño de circuitos electrónicos que permitió visualizar las conexiones entre componentes antes de la implementación física.

**Componentes del Diseño:**

| Componente | Descripción | Especificaciones Técnicas |
|------------|-------------|---------------------------|
| **ESP32 DevKit** | Microcontrolador principal con WiFi/Bluetooth integrado | Dual-core 240MHz, 520KB SRAM, USB Tipo C |
| **Sensor MQ-135** | Sensor de calidad de aire para detección de CO2 y gases | 5V, salida analógica/digital, rango 10-1000ppm |
| **Display OLED 0.96"** | Pantalla local para visualización de métricas | I2C (SDA/SCL), 128x64 píxeles, 3.3V-5V |
| **LED Panel** | Panel de LEDs para indicadores visuales de estado | Requiere definición de bits/resolución específica |
| **Protoboards** | Placas de prototipado para conexiones | MB-102 (830 puntos) y 400 puntos |
| **Cables Dupont** | Conexiones hembra-hembra, macho-hembra, macho-macho | 20cm, 40 piezas cada tipo |

Es importante destacar que durante la fase de diseño y validación técnica, se identificaron las siguientes limitaciones críticas:

1. **Sensor MQ-135 - Limitaciones Funcionales:** Según la documentación oficial del fabricante y las especificaciones técnicas revisadas, el sensor MQ-135 presenta limitaciones significativas para la detección precisa de CO2 en aplicaciones de monitoreo ambiental profesional. El sensor está diseñado principalmente para detectar una mezcla de gases (NH3, NOx, alcohol, benzeno, humo) pero carece de la selectividad y precisión requeridas para mediciones fiables de CO2 en tiempo real.

2. **Uso como Placeholder:** A pesar de estas limitaciones documentadas, el equipo decidió utilizar el MQ-135 como componente placeholder en el prototipo inicial debido a que el hardware físico ya había sido adquirido por el equipo para el desarrollo del proyecto. Esto permitió avanzar con la integración del sistema, el desarrollo del firmware del ESP32, y la validación de la arquitectura de comunicación (Embedded→Edge→Cloud), mientras se evalúa la incorporación de sensores más precisos (como el Sensirion SCD30 o MHZ-19B) en iteraciones futuras.

3. **LED Panel - Especificaciones Pendientes:** El diseño incluye un panel de LEDs para indicadores visuales del estado del sistema (conexión WiFi, umbrales de calidad de aire). Sin embargo, las especificaciones exactas del panel (número de bits, resolución, protocolo de comunicación) requieren definición adicional para la implementación final.


El diseño representa la versión inicial de prototipado enfocada en validar la arquitectura de hardware y las conexiones básicas. Las pruebas preliminares confirman el funcionamiento de la comunicación I2C con el display OLED, la lectura analógica del ADC del ESP32, y la conectividad WiFi para transmisión de datos al Edge Station.