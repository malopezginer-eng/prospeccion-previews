# NOTAS — Dirección A: «Built in front of you»

**Idea ejecutada:** el hero no vende con una foto de "antes/después"; vende con un móvil vacío que se
construye a la vista mientras haces scroll (topbar → foto → precios → horario con "open now" → mapa →
WhatsApp), con un rótulo corto a la izquierda por cada pieza. Cierre: "Your site is already at this
stage..." + S$590 + WhatsApp Miguel.

**Negocio ficticio:** "DELTA WAVE AIRCON" (inventado, sin relación con negocios reales), con la foto
`draft-aircon-720.webp/jpg` ya anonimizada del banco de assets.

**Técnica:**
- El móvil se dibuja en HTML/CSS puro (retícula punteada de fondo + 6 piezas absolutas/flex, sin imágenes
  de marco). Con CSS solo, ya se ve completo y final — es la garantía de "completo sin JS".
- El JS (GSAP + ScrollTrigger) es lo único que oculta las piezas (`gsap.set(autoAlpha:0)`) y las revela una
  a una con `ScrollTrigger.create` por cada bloque de texto (`onEnter`/`onEnterBack`), sin timeline maestro
  ni `pin`. Deliberadamente **no uso `pin` de ScrollTrigger** ni en escritorio ni en móvil: en su lugar el
  móvil queda con `position: sticky` (CSS nativo, sin coste de frame) mientras los rótulos pasan al lado.
  Es más barato que un pin+scrub real y el resultado visual es el mismo (el teléfono se queda quieto,
  el texto se monta encima). En escritorio añado un `scrub` muy ligero (solo un `scale` del 0.96→1 del
  móvil) para que el conjunto lea como un único gesto, no seis “pops” sueltos.
- Con `prefers-reduced-motion` o sin JS: el script no corre nada, así que el móvil aparece ya montado y
  completo desde el primer frame — no hace falta rama de código aparte.

**Qué dejo fuera:** el remate con más detalle (reseñas, galería) que pedía el brief general de la web
completa; aquí solo hero + acto de montaje + cierre con precio, tal como pide la dirección A. No toco
`../assets/`, `mnkykonnekt-web` ni nada fuera de `lab/a/`.

**Si se elige esta dirección:** cambiaría el `scrub` del escritorio por un pin real cuando haya presupuesto
de rendimiento probado en un móvil de gama media, y añadiría una segunda ronda de piezas (reseñas, botón
de llamada) si el remate se queda corto en la versión completa del sitio.
