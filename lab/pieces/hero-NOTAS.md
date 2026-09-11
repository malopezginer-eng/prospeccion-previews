# hero.html — «la web vieja se reconstruye delante de ti»

Marco de navegador pegado en pantalla con una web de pyme de 2006 **dibujada entera en HTML/CSS** (nada de capturas) que se desmonta mientras la nueva se monta debajo. Titular exacto pedido, con «already built» en ámbar.

**Cómo funciona.** `.mkh-scroller` (340vh; 300svh en móvil) + `.mkh-stage` con `position: sticky` — **sin `pin`**. GSAP 3.13 + ScrollTrigger por jsDelivr, `scrub: .55`. Una línea de tiempo por breakpoint con `gsap.matchMedia()`: ≥900px todos los gestos (banner que se despega, obra en curso que cae, contador que se apaga, celdas que se descuadran y caen en cascada); <900px la misma historia en menos pasos. Único global: `window.MKH_init`. Botón «Replay» real (`<button>`, foco visible) que salta al inicio y recorre el scroll con un tween.

**Tres estados, los tres comprobados en navegador.** Con JS: la secuencia. Sin JS o si el CDN falla: la clase `mkh-js` no se añade (o `init` la quita) y el CSS deja la web nueva terminada, la vieja en `display:none`, sin Replay. `prefers-reduced-motion`: sin secuencia, las dos versiones una al lado de otra rotuladas «Before/After».

**Clases.** Todo `mkh-`. `mkh-o-*` web vieja, `mkh-n-*` web nueva, `mkh-lab--a/b` el rótulo que cambia, `mkh-u--old/new` la barra de direcciones. Las variables cuelgan de `.mkh-hero`, no de `:root`.

**Al integrar.**
- El script del `<head>` que pone `mkh-js` debe seguir siendo **inline y antes de pintar**; si no, parpadea la web nueva antes de empezar.
- `.mkh-viewport` es quien lleva el color (gris → papel). Las dos páginas van transparentes: no le pongas fondo a ninguna.
- La banda de foto de la web nueva está **dibujada en CSS**, sin imagen: todas las de `lab/assets` son capturas de web con texto incrustado y ningún recorte lo escondía. Cuando haya foto real del negocio, se mete un `<img position:absolute; inset:0; object-fit:cover>` dentro de `.mkh-n-photo` y el degradado y el pie siguen valiendo.
- La única imagen que usa es `../assets/img/after-salon-720.webp`, estirada a propósito en la web vieja (ahí el texto incrustado es parte del chiste).
- `.mkh-demo-bar`, `.mkh-demo-tail` y la regla de `body` son andamio de la demo: se borran.
- Probado a 1440×860, 1280×640, 390×844 y 390×640. Hay un bloque `@media (max-height: 700px)` que aprieta la web nueva para que su pie no se salga del marco.
