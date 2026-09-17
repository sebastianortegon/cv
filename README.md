# sebastianortegon.com — v4 (maqueta de dos columnas)

Versión basada en la maqueta que hiciste tú: panel izquierdo fijo (perfil, contacto, partners oficiales) + panel derecho con scroll (About me, marquee de logos de clientes, globo de puntos rotable). Sin frameworks ni build step — un solo `index.html` con CSS y JS inline.

## Qué incluye esta versión

- **Layout de 2 columnas**: en pantallas ≥900px el panel gris de la izquierda queda fijo (`position: fixed`) mientras el contenido de la derecha hace scroll normal. En mobile todo se apila en una sola columna y el bloque de "official partner" pasa a ser una franja oscura al final de la página (como en tu mockup mobile).
- **Logos en escala de grises → color al hacer hover**: aplica a todos los logos (clientes y partners oficiales) vía CSS (`filter: grayscale`).
- **Marquee de logos de clientes**: dos filas infinitas — una se desplaza a la derecha, la otra a la izquierda — ambas con difuminado (fade) en los bordes usando `mask-image`. Se pausan al pasar el mouse por encima.
- **Globo de puntos rotable**: construido desde cero en `<canvas>` (no reutiliza el código de Shopify que pegaste — ese snippet no traía lógica real, solo el HTML ya compilado). Los puntos siguen la silueta real de los continentes (se generaron a partir de un mapa de tierra/agua, no es una esfera genérica), así que se ven las costas reconocibles en vez de una bola de puntos pareja. Se arrastra libre en ambos ejes con el mouse o el dedo (con inercia al soltar), y cuando no lo tocas hace un **"tour" automático** por Francia, Canadá, España, U.S.A, Portugal, Colombia y Uruguay — copiando el efecto del globo de "visitantes en vivo" del panel de Shopify: rota y reencuadra hasta centrar un país, aparece un pin con una tarjeta flotante (bandera + nombre + "Client project"), lo mantiene unos segundos, y salta al siguiente. Si arrastras el globo mientras el tour está corriendo, se pausa y retoma donde iba al soltar.

## Cómo reemplazar los placeholders

Todo lo que necesitas cambiar vive en `assets/`. El `index.html` no necesita tocarse para reemplazar imágenes — solo respeta los mismos nombres de archivo.

### 1. Foto de perfil
- Archivo: `assets/img/profile.jpg`
- Reemplázalo por tu foto real (cuadrada, mínimo 500x500px — se recorta en círculo automáticamente).

### 2. Logos de clientes (marquee)
- Carpeta: `assets/logos/`
- Fila 1 (marquee a la derecha): `smurfit-kappa.png`, `carvajal.png`, `tecnoquimicas.png`, `gobierno-colombia.png`, `haceb.png`, `colombina.png`
- Fila 2 (marquee a la izquierda): `la-french-tech.png`, `asocana.png`, `eurekakids.png`, `procolombia.png`, `ccca-cali.png`
- Reemplaza cada uno por el logo real (idealmente PNG con fondo transparente, mismo nombre de archivo, buen contraste ya que se ven en escala de grises por defecto). Si agregas o quitas logos, edita las dos secciones `.marquee-track` en `index.html` — cada fila tiene los logos duplicados una vez (para el loop infinito sin cortes), así que agrega/quita el logo en ambas copias de la fila.

### 3. Logos de "Official partner" (panel izquierdo / footer mobile)
- Carpeta: `assets/partners/`
- Archivos: `meta.png`, `google-partner.png`, `tiktok.png`, `shopify.png`, `wix.png`, `vtex.png`
- Mismo criterio: PNG con fondo transparente, mismo nombre de archivo.

### 4. CV descargable
- Archivo: `assets/cv/sebastian-ortegon-cv.pdf`
- Reemplázalo por el PDF real de tu CV (el mismo que sale de `cv-ats-master.md` del proyecto, exportado a PDF).

### 5. Textos y datos
Todo el texto vive directo en `index.html` — ábrelo con cualquier editor y busca:
- El bloque `<aside class="sidebar">` — nombre, rol, stat de ads, bio corta, botones de contacto.
- El bloque `<section class="about">` — los 3 párrafos de "About me".
- El array `PINS` dentro del `<script>` al final del archivo — ahí están los países del globo (nombre, lat/lon, bandera), en el orden en que el tour los va mostrando. Puedes agregar, quitar o reordenar países ajustando ese array; las coordenadas son aproximadas (centro del país). El globo reencuadra automáticamente cada país que agregues, así que no hay que ajustar nada más.
- `TOUR_HOLD_MS` (mismo bloque, cerca del array `PINS`) — cuántos milisegundos se queda cada país en pantalla antes de saltar al siguiente (2600 = 2.6s por defecto).
- `TOUR_SUBTITLE` (mismo bloque) — el texto gris debajo del nombre del país en la tarjeta ("Client project" por defecto). Es el mismo texto para los 7 países; cámbialo por lo que prefieras.
- **Nota**: el dato "$250k/year in ads" que pusiste en el panel izquierdo quedó tal cual lo dejaste en tu mockup — solo asegúrate de que sea la cifra que quieres publicar (en un hilo anterior habíamos hablado de "+2M USD spent in ads" como alternativa; usa la que puedas sostener si alguien te pregunta por el detalle).

## Cómo publicarlo en sebastianortegon.com
Es un sitio estático (HTML + CSS + JS inline, sin build step, sin dependencias externas) — funciona con cualquier hosting estático:
- **Vercel / Netlify**: arrastra la carpeta completa o conéctala a un repo de GitHub — deploy automático.
- **GitHub Pages**: sube esta carpeta a un repo y activa Pages apuntando a la raíz.
- Cualquier hosting compartido tradicional también sirve: sube todos los archivos (`index.html` + `assets/`) a la raíz del dominio.

Abre `index.html` directo en el navegador para previsualizar antes de publicar.
