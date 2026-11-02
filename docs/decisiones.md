# Documento de decisiones de diseño

> Cada decisión: **qué** elegiste, **por qué**, y **qué alternativa descartaste**.
> Se evalúa la justificación, no la longitud. Máximo 2 páginas en la Fase 1.

## Ruta de trabajo

- [ ] Ruta A · Figma (enlace con permiso de lectura: …)
- [X] Ruta B · VS Code (diseño directamente en `guia.html`)

## 1. Color (RA1 · CE b)

- Tono de acento de la ficha y cómo has obtenido la escala (50 … 950):
Se utiliza una gama de rojos y burdeos basada en la identidad visual de GYM HUB. Se han definido colores primitivos para los temas claro y oscuro.
- Por qué el acento de texto/fondo es el 700 en claro y el 400 en oscuro (o el que elijas):
Se utiliza el tono 700 en el tema claro y el 400 en el oscuro para mantener la identidad visual y conseguir contraste con las superficies.
- Tokens semánticos añadidos y para qué:
Se han definido tokens para fondos, superficies, textos, bordes, acentos, estados de éxito y foco. De esta manera, los componentes utilizan nombres que indican la función del color y no su valor hexadecimal.
- Pares de contraste añadidos a `$pares-contraste`:
Se han definido comprobaciones para texto principal, texto secundario, acentos, estados de éxito, bordes de controles e indicadores de foco. Se aplican mínimos de 4,5:1 para texto normal y 3:1 para controles y foco.

## 2. Tipografía (RA1 · CE b)

- Familia elegida y por qué (rendimiento, legibilidad, licencia): 
Se utiliza `system-ui` como fuente principal porque aprovecha las fuentes del sistema operativo, ofrece buena legibilidad y evita depender de fuentes externas. Para fragmentos técnicos y conceptos como códigos se utiliza `ui-monospace`, que facilita la identificación de texto monoespaciado.
- Base y razón en móvil y escritorio. Por qué esas: 
Se establece un tamaño base de 16 px en móvil y 18 px en escritorio para facilitar la lectura en ambos dispositivos. Se utiliza una razón modular de 1,2 en móvil y 1,25 en escritorio para crear una jerarquía visual progresiva entre títulos y textos.
- Medida de línea (`max-inline-size` del párrafo en `ch`):
Se establece un ancho máximo de 65ch para los párrafos, con el objetivo de evitar líneas demasiado largas y facilitar la lectura.

## 3. Espaciado y forma

- Escala de espaciado: 
Se utiliza una escala de ocho tamaños, desde 4 px hasta 64 px, basada en múltiplos de 4. Esto permite mantener una separación coherente entre los elementos de la interfaz.

- Radios: 
Se utilizan 8 px para los controles, 12 px para las tarjetas y 999 px para elementos con forma de píldora. Así se diferencian los distintos tipos de componentes manteniendo una estética uniforme.

## 4. Componentes (RA1 · CE f)

| Componente | Estados | Cómo se resuelve cada estado en CSS |
| --- | --- | --- |
| Botón | normal, hover, foco, desactivado, secundario |Fondo de acento; hover cambia el fondo; foco mediante foco-visible; desactivado con opacidad del 50 %; secundario con fondo transparente y borde de acento.|
| Turno | disponible, seleccionado, ocupado, foco | Se utiliza :has() para detectar los estados del radio. La selección cambia el borde y el fondo; el estado no disponible utiliza opacidad y borde discontinuo; el foco utiliza foco-visible.|
| Contador de invitados |Normal, seleccionado y foco | Se utilizan botones segmentados con Flexbox y radios. :has(:checked) identifica la opción seleccionada y :has(:focus-visible) muestra el foco.|
| Aviso de pago |Estado normal | Se utiliza una sección con borde de acento, fondo suave y texto del concepto con fuente monoespaciada.|

## 5. Comparativa de tecnologías (RA1 · CE e · RA2 · CE i)

| Criterio | Figma | Penpot | Diseño en código |
| --- | --- | --- | --- |
| Coste / licencia |Plan gratuito limitado y opciones de pago. |Software libre y opción alojada. | Sin coste de licencia adicional.|
| Traslado a código (handoff) | Facilita compartir diseños y especificaciones.| Permite compartir diseños y consultar medidas.| El diseño ya se realiza directamente en código.|
| Mantenimiento del sistema |Permite reutilizar componentes y variables. | Permite reutilizar componentes y estilos.|Los cambios se centralizan en los tokens y componentes Sass. |

| Criterio | Sass + CSS propio | CSS nativo sin preprocesador | Bootstrap / Tailwind |
| --- | --- | --- | --- |
| Tokens y temas | Permite organizar variables, mapas y temas.|Permite utilizar propiedades personalizadas CSS. | Ofrecen sistemas de configuración y utilidades.|
| Peso del CSS final |Se genera CSS a partir de Sass. | No necesita compilación adicional.| Puede incluir estilos y utilidades del framework.|
| Control de la cascada |Permite organizar estilos mediante módulos y capas. | Ofrece control directo sobre la cascada.| Requiere adaptarse a las convenciones del framework.|

**Decisión y motivo:**
He elegido trabajar en VS Code con Sass y CSS propio. Esta opción me permite desarrollar el sistema de diseño mientras se programa, centralizar los valores en tokens y mantener un mayor control sobre los componentes y la cascada. Se descarta utilizar Figma o Penpot porque se ha preferido trabajar directamente sobre el código. También se descartan Bootstrap y Tailwind para evitar depender de un framework y poder construir una interfaz propia.