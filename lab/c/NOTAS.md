# Dirección C — Studio editorial

**Idea ejecutada:** registro tinta/papel con retícula de 12 columnas visible de fondo (líneas de
`--line` al 8% de opacidad), hero tipográfico a sangre (clamp 48–140px) con máscara de línea que
sube desde abajo, banda de lectura con scrub (palabras de gris apagado a papel al entrar en foco),
bento asimétrico de las 4 previews con distinto `aspect-ratio`/`border-radius` cada una, cursor
"View" solo dentro del bento en desktop, marquee de sectores que se para en hover/foco.

**Técnica:** GSAP core + ScrollTrigger + SplitText por jsDelivr, `defer`. Máscara de líneas con
`overflow:hidden` + `span` trasladado (no uso SplitText real para el H1 —el texto ya está partido
en 4 `<span class="line-mask">` en el HTML para que sea legible sin JS—, dejo el plugin cargado por
si se quiere refinar a nivel de palabra). Scrub de la banda: un `ScrollTrigger` por palabra con
`scrub`. Marquee: `@keyframes` inyectado por JS solo si no hay `prefers-reduced-motion`, con
`animation-play-state:paused` en `:hover`/`:focus-within`. Cursor con `requestAnimationFrame` +
lerp, solo si `matchMedia(min-width:900px)` y sin touch.

**Qué dejo fuera:** el resto de la web (precio detallado, garantía, pasos, FAQ); eso es del scope
completo, no de este tramo. No añado testimonios ni nombres reales (regla legal del frente).

**Qué cambiaría si se elige:** SplitText real por palabra en el H1 para un stagger más fino;
precargar `draft-barber` (la imagen grande del bento) con `fetchpriority` si se confirma que es la
primera imagen bajo el fold; revisar el corte de columnas de la retícula en pantallas muy anchas
(>1600px) para que no se vea desproporcionada.
