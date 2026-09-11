# Dirección B — Before → After theatre (corregida 2026-09-11)

**Qué cambió y por qué:** la captura dejó de ser el fondo del hero. Ahora hay un `<header>` con solo
el logo, luego el titular en texto real sobre papel `#F9F6EF` (nada de texto sobre la foto), y debajo
un `.browser-frame`: barra de ventana en CSS (tres puntos + `yoursalon.com.sg`) que enmarca el par
before/after a máx. 1000px. Así la captura se lee como "una web que enseñamos", no como el hero de
MNKY. El logo ya no cae sobre el logo tapado de la peluquería. El botón principal pasó de
`btn-accent` (ámbar) a `btn-brand` (teal `#237A77`); el ámbar queda solo para el foco, como pide la
identidad.

**Se conserva intacto:** el barrido `clip-path` sobre `--p` con `ScrollTrigger` (`pin`+`scrub` en
escritorio, disparo único en móvil), los rótulos "Their site today"/"Our draft", el comparador
arrastrable — ahora un único elemento (`#heroRange`) que sirve para el scrub Y el arrastre manual
posterior en cualquier tamaño, ya no hay un `.mobile-compare` duplicado — el marquee de previews,
`prefers-reduced-motion` (todo queda al 50%, ambas etiquetas visibles, contenido completo sin JS) y
el pie de foto legal exacto.

**Dejado fuera:** subtítulo largo bajo el titular (el brief pide "una línea corta" con precio+botón,
así que no añadí la frase de subtítulo disponible); duplicar el marco de navegador en el marquee de
abajo (las cuatro previews siguen en tarjetas simples).

**Riesgo que queda:** el `pin` de ScrollTrigger ahora fija un elemento más pequeño que el viewport
(`.frame-wrap`, no toda la pantalla); visualmente funciona pero no lo he verificado en un navegador
real con DevTools — si al probarlo el pin se ve raro (salto, layout shift), cambiar `start` de
`"top 90px"` o quitar `pin:true` y dejar solo `scrub` sin pin.
