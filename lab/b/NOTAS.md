# Dirección B — montaje final con las cuatro piezas (2026-09-11, fase 4)

Un solo archivo, `lab/b/index.html`. Las piezas de `lab/pieces/` están **copiadas dentro**, cada una en su
bloque de CSS rotulado dentro del `<style>` y su IIFE dentro del único `<script>` del final. Las piezas
originales no se han tocado. El montaje se hizo con un script reproducible que falla si un marcador no
aparece: `%TEMP%\claude\C--dev-prospeccion\<sesión>\scratchpad\build\build.py`.

## Qué pieza vive dónde

| Pieza | Dónde queda | Qué sustituyó |
|---|---|---|
| `hero.html` (`mkh-`) | `<header class="mkh-hero" id="top">`, primer bloque del cuerpo | El marco con la captura de la peluquería, el barrido por scroll y el comparador arrastrable |
| `movil.html` (`mkm-`) | Dentro de `article.lg` («Fast on a phone») de `#get` | La maqueta estática `.phone` / `.p-*` |
| `pasos.html` (`mkp-`) | `<section class="mkp-root" id="how">` | La `<ol class="steps">` entera de `#how` |
| `demos.html` (`mkd-`) | `<section class="mkd-root" id="demos">` + su `<dialog>`, entre `#how` y `#safe` | Nada: sección nueva |

Orden final: nav → hero → cifras (teal) → What you get (móvil dentro) → precio → tres pasos → **demos** →
confianza → quién te atiende → FAQ → cierre → pie.

## Qué se retiró

- **«Recent drafts» (la cinta) entera.** Enseñaba capturas estáticas de los mismos cuatro sectores que las
  demos, que además se abren y se navegan: era la versión peor de la misma idea y costaba ~0,7 pantallas de
  móvil. El enlace «See a draft» de la nav apunta ahora a `#demos` y el ítem «Drafts» desaparece.
- Andamio de las piezas: `.mkh-demo-bar` / `.mkh-demo-tail`, el escaparate de `movil` (`.mkm-root`,
  `.mkm-wrap`, `.mkm-grid`, su `<h2>` y su lead, que duplicaban el titular y el lead de `#get`), y la nav y
  la banda teal de contexto de `demos`. Y de las cuatro: `@font-face`, `:root`, reset, `body`, `img`,
  `:focus-visible` (ya estaban en la página).
- CSS muerta de la página: hero viejo (`.theatre`, `.stage`, `.handle`, `.img-*`, `.frame-*`), maqueta
  `.phone`/`.p-*`, `#how` viejo (`.steps`, `.step-frame`, `.shot`, `.stamp`, `.mark`), `.drafts`/`.marquee-*`
  y `.dots`. El JS del comparador y de la cinta también.
- Direcciones postales de las maquetas: «12 Duxton Road, Singapore 089490» → «Tanjong Pagar, Singapore»;
  «78 Tiong Poh Road…» → «Tiong Bahru»; «…, #01-12 / Singapore 160078» → «Tiong Bahru · Singapore».
  Nombres unificados en el inventado que ya usaba la página: **YOURSALON** (antes «HAIR STUDIO» / «Hair
  Studio» / «Tiong Bahru Hair»), con `yoursalon.sg` y `yoursalon-sg.webspace.net`.

## Qué se conservó a propósito (textos de venta)

El hero **mantiene** el kicker, el subtítulo aprobado, «S$590», el botón de WhatsApp, las cinco garantías y
el pie legal de la captura; la pieza solo aporta el titular y el teatro. `#how` mantiene el párrafo largo de
garantía de la página (no el corto de la pieza), con su filete ámbar.

## Adaptaciones de integración (y por qué)

- `body { overflow-x: clip }` en vez de `hidden`: `hidden` crea contenedor de scroll y **rompe los dos
  sticky**. Comprobado: sin scroll horizontal a 390 px (`scrollWidth − clientWidth = 0`).
- En el `<html>`: `scrollbar-gutter: stable` y `html.mkd-locked { overflow: hidden }` (visor de demos).
- La nav es fija y mide 64 px: los dos sticky van a `top: 64px` con `height/min-height: calc(100svh − 64px)`.
- El `<script>` inline que pone `mkh-js` sigue inline, en el `<head>`, antes de pintar.
- Un solo `<script>` al final, dentro de `DOMContentLoaded` (un `<script>` en línea ignora `defer`, así que
  espera a que GSAP 3.13.0 —cargado una sola vez, por jsDelivr, con `defer`— exista). `RM` se lee una vez y
  se comparte con las cuatro piezas.
- **Fugas de cascada arregladas**: `.get-grid article p/h3` y `.get-grid article.lg p/h3` pintaban de blanco
  el texto de dentro de la pantalla del móvil (texto blanco sobre blanco); ahora van al hijo directo o a
  `.lg-copy`. Y `footer { background: var(--ink) }` alcanzaba al `<footer>` de la web nueva del hero (caja
  negra dentro del marco); ahora es `body > footer`. El `<h2>` de la web de 2006 recupera su serif con
  `font-family: inherit`.
- **`html { scroll-behavior: smooth }` rompía el botón «Replay»** (cada `scrollTo` del tween arrancaba su
  propia animación suave; medido: 2306 → 2108 → 2887 en vez de recorrer el raíl). Ahora el Replay pide
  `behavior: "instant"`.
- **Los reveals usaban `autoAlpha`**, que pone `visibility: hidden` y sacaba de la tabulación todo lo que
  hubiera dentro (con Tab se saltaban los botones de `#price`). Pasan a `opacity`, más una red de seguridad
  en `focusin`. Recorrido con Tab completo verificado, de la nav al pie, con foco visible en cada parada.
- La tarjeta «Fast on a phone» pasa a ancho completo (`grid-column: 1 / -1`, copia y teléfono en fila): el
  teléfono de 520 px no cabía en una columna de 2/6 sin dejar 250 px de aire en las siete tarjetas vecinas.
  Dentro de la tarjeta, el teléfono pierde el `order: -1` de la pieza (manda el titular) y oculta la barra
  de scroll de los paneles (un móvil real no enseña ninguna).
- El lead de los pasos («Scroll and watch…») solo aparece con la secuencia activa: sin JS o con
  reduced-motion no hay nada que mirar.

## Recorte de pantallas

Con todo montado salían **16,91 pantallas** de móvil. Se recortó **aire, nunca contenido**: raíles del hero
(300 → 163 svh) y de los pasos (240 → 158 vh) —la única concesión de la que avisa el brief—, paddings de
sección, póster de las demos a 5:2 en móvil (se recorta por arriba: se sigue viendo cabecera y titular de
cada diseño), pantalla del teléfono a 445 px y una pasada de micro-aire en cifras, precio, confianza, FAQ,
cierre y pie. Resultado: **14,83 pantallas a 390×844**. Los scrubs quedan en ~600 px cada uno (la pieza
original tenía ~1700 y ~1200): la secuencia es más rápida en móvil, es el precio del tope.

## Comprobado en navegador (1440×900 y 390×844, servido por http)

Hero se reconstruye y «Replay» recorre el raíl entero · los tres pasos avanzan y las anotaciones del cliente
cambian la página · las cuatro pestañas del móvil con ratón y con ←/→/Home/End, y el botón abre la
conversación falsa (Esc la cierra, el foco vuelve) · **las cuatro demos** abren en el visor, se navegan por
dentro, Phone/Desktop escala (1440→0,861), `Esc` y la X cierran, el `src` vuelve a `about:blank` y el foco
vuelve a su tarjeta · **0 iframes en la carga inicial** · ninguna imagen rota, ninguna caja vacía, sin scroll
horizontal · los seis enlaces del menú llevan a su sección con el título a 164 px (la barra mide 64) ·
contraste AA: 0 fallos reales · `prefers-reduced-motion`: hero en «Before/After» lado a lado, pasos en la
página terminada, 11,1 pantallas · sin JS: página completa, precio, garantías, tres pasos y las cuatro demos
como enlaces normales, 0 iframes · estilos computados de las cuatro piezas comparados uno a uno contra sus
archivos originales: **demos 0 diferencias, móvil y pasos solo subpíxeles, hero solo el `font-size` heredado
del `body` (17 px en vez de 16), que no cambia ningún texto**.

## Riesgo y pendiente

- **Único error de consola: `assets/img/miguel.jpg` 404.** Es el hueco del retrato, anterior a este montaje:
  el `onerror` pone el logo y se ve bien. Se apaga solo el día que se copie la foto ahí.
- Tres de las cuatro demos desbordan en horizontal a 375 px (hallazgo de `demos-NOTAS.md`, pasa también
  abriéndolas solas); está fuera de `lab/b/`.
- Dentro de la web de 2006 del hero sigue habiendo una captura real anonimizada (`after-salon-720.webp`)
  estirada, con «The Hair Studio» incrustado; por eso se conserva el pie legal aprobado. Si molesta que no
  case con «YOURSALON», se recorta o se sustituye por una foto real del negocio.
- Sin JS, el móvil de `#get` se estira (las cuatro secciones una debajo de otra, ~1520 px): es la caída
  prevista por la pieza, legible y completa, pero larga.
- El repo tiene `lab/pieces/` y `lab/demos/` sin trackear (de las otras sesiones). **No se ha commiteado
  nada**: el brief acota el trabajo a `lab/b/` y el commit de todo el lote es del que coordina.

# Tercera vuelta (2026-09-12) — las ocho peticiones de Miguel

Encargo: `C:\dev\prospeccion\docs\plans\2026-09-12-web-tercera-vuelta.md`. Informes largos de cada pieza en el
scratchpad de la sesión (`INFORME-hero.md`, `INFORME-telefono.md`, `INFORME-demos.md`, `INFORME-dinamismo.md`).

## Diagnóstico de «no se anima en escritorio»

El código funcionaba en un Chromium limpio a 1440×900. Dos causas reales: (1) el teatro empezaba a 727 px, bajo el
pliegue; (2) **Miguel navega con `prefers-reduced-motion: reduce`** (Windows por RDP apaga los efectos de
animación) y la página apagaba hero, pasos y entradas. Criterio nuevo: **el scrub ligado al scroll se mantiene con
`reduce`** (lo gobierna el visitante); solo se paran las animaciones autónomas (loops, marquee, latidos).

## Qué cambió

- **Hero**: a ≥ 1100 px el stage sticky es una rejilla copia | navegador y el ScrollTrigger arranca a 1 px. «Antes»
  = plantilla de constructor de hoy (menú de 6, hero de stock, tres tarjetas, mapa enorme, WhatsApp flotante,
  cookies, «© 2019 · Powered by SiteBuilder Pro»); «después» = foto real a sangre, prueba social, tarifa de 5, dos
  reseñas, mapa teal, horario, barra Call · WhatsApp · Directions; proporción fija con `cqw`. Coreografía: rotura →
  barrido diagonal → montaje en orden de lectura → subrayado ámbar de la garantía. Trampa nueva: `gsap.matchMedia`
  necesita declaradas las dos condiciones o el móvil se queda sin timeline.
- **How it works**: sin condición `RM`; `start: "top 64px"`, rail 300vh; cuarto golpe (destello en la URL y un
  latido del sello «live»).
- **Teléfono `.mk-phone`** compartido por «Fast on a phone» y el visor: 9/19.5, isla dinámica, botones, barra de
  estado con hora real. Visor en modo teléfono con proporción real (`h = min(availH, 390·19.5/9)`) e iframe escalado.
  Dentro del móvil: hoja inferior por servicio, franja de fotos con snap, chat de WhatsApp.
- **Dinamismo**: una entrada con significado por sección (barras en cifras, teléfono que se endereza, cifra y
  subrayado del precio, tarjetas de demos con `clip-path`, cascada de razones, foto circular, FAQ animada, marquee de
  sectores, nav `.is-scrolled`). Todo GSAP, 0 KB extra; 0 long tasks con CPU ×4 en móvil emulado; CLS 0,03.
- **Demos**: `MAX_BLOCKS` 8 → 9 en el motor; barber, salon y pets ganan `about`/`faq`/`services`/`reviews` sin
  perder `gallery`; JSON enriquecidos, reseñas sin autor, sin mapa (sin `address` a propósito); pósters regenerados.
  Arreglo de `preview.css` para `.services-list .row` a 320 px.

## Auditoría (Playwright, 2026-09-12)

1440×900 / 1280×800 / 390×844: sin scroll horizontal (390 = 390), **14,87 pantallas de móvil**, 0 iframes en carga,
0 imágenes rotas, 0 fallos de contraste AA (parseando `color(srgb)`), 0 frases prohibidas de OFERTA §6, 66 paradas
de Tab; sin JS página completa (14,55 pantallas); con `reduce` hero y pasos siguen animando por scroll. Único 404:
`assets/img/miguel.jpg` (la foto de Miguel, pendiente).

# Cuarta vuelta (2026-09-12, noche) — feedback de Miguel sobre la tercera

Encargo y copy pendiente: `C:\dev\prospeccion\docs\plans\2026-09-12-web-cuarta-vuelta-y-copy.md`. Informes:
`INFORME-{hero,telefono,pasos,visor,offer}-v4.md` en el scratchpad de la sesión.

- **Más lento**: hero 260 → 360vh (móvil 163 → 230svh), pasos 300 → 400vh (móvil 158 → 200vh), `scrub` .9,
  entradas y staggers ×1,5, marquee 68 s.
- **Hero con contraste**: «antes» con fondo gris frío, texto apelmazado, azul de plantilla, franja «SALE», popup de
  newsletter, hero de stock desenfocado, segunda fila de tarjetas con iconos rotos, pie de 13 enlaces; «después» con
  más aire y tipografía mayor; rótulos grandes; frío → cálido durante el barrido.
- **Fast on a phone**: escritorio `clamp(304px, 39vh, 356px)`; en < 760 px escena sticky en la que el teléfono
  crece hasta que su pantalla cubre el viewport (la pantalla nace con la proporción del viewport para que un solo
  `scale` la cubra exacta) y los paneles reciben toques solo a pantalla completa (`html.mkm-full`).
- **How it works**: «we open at 10» solo cambia la hora (Mon–Sun se mantiene); «make this bigger» rodea el titular
  y este crece 2.2 → 3.1em; «use our photo» pasa de un placeholder «STOCK PHOTO» dibujado a la foto real con barrido;
  un ✓ ámbar por respuesta.
- **Visor de demos**: sin barra externa ni nota. Escritorio: ventana de macOS a `min(96vw, 1600px)`, el punto rojo
  cierra, conmutador y «new tab» dentro de la barra, iframe a 1440 escalado al ancho. Teléfono: 87-91 % de la altura,
  × flotante, píldora debajo; isla, botones y radios proporcionales (24 % / 3,3 % de la pantalla), que era la
  diferencia NUC ↔ portátil. < 760 px a sangre con solo la ×.
- **`/offer/`**: rediseñada con el mismo copy (1086 palabras, multiset idéntico): pasos en fila, tarjetas de altura
  natural con el botón bajo el precio y toda la tarjeta clicable, secciones a dos columnas.

**Pantallas de móvil: 16,42 a 390×844** (tope anterior 15). El exceso viene de los rails más largos que pidió Miguel
(hero +0,67, pasos +0,38, escena del teléfono +0,49). Se deja así salvo que Miguel prefiera recortar.
Auditoría: 1440×900 / 1280×800 / 390×844 sin scroll horizontal, 0 iframes en carga, 0 imágenes rotas, 0 fallos AA,
0 frases prohibidas, sin JS completa, con `reduce` scrubs vivos, todas las entradas disparadas en scroll continuo.

## Quinta pasada (2026-09-12, madrugada): «Fast on a phone» con demo real

Miguel rechazó la escena de la cuarta vuelta (móvil achatado, zoom raro a pantalla completa, demasiado rápida) y
pidió que fuera «prácticamente igual que las demos en móvil: si se pone una demo, problema resuelto». Hecho: la
pantalla del teléfono muestra `demos/demo-salon` en un iframe a 390 px lógicos (creado solo cuando `#get` se acerca:
0 iframes en la carga), el teléfono mantiene 9/19.5 siempre, y en móvil el rail (220svh) hace crecer el teléfono
hasta que la pantalla mide `innerWidth × (innerHeight − 64)` con el iframe a `scale(innerWidth/390)` (≈ 1: nítido),
el marco se desvanece y la demo queda a sangre y tocable (`html.mkm-full`). La maqueta dibujada queda como estado
sin JS. Foto de Miguel añadida (`assets/img/miguel.jpg`, 800×800). Página: 17,19 pantallas a 390×844.
