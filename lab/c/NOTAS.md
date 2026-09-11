# Dirección C — Studio editorial (web completa)

**Qué construyo:** las 13 secciones del brief sobre el mismo lenguaje del hero (tinta `#111214`,
retícula de 12 columnas, display Bricolage a sangre). El bento de "Recent drafts" ya construido pasa
a cubrir la sección 10: le añado pies estáticos (sector + descriptor, sin necesitar hover) y el aviso
de que son propuestas, sin crear una segunda galería.

**Cifras (85/76/87):** tipográficas enormes en retícula de 3 columnas, con su frase y su fuente; el
HTML ya lleva el valor final ("85%"...) para que sea correcto sin JS, y el contador solo resetea a 0
y cuenta hacia arriba si GSAP corre (mismo patrón que la web actual).

**"What you get":** bento de texto asimétrico (7 tarjetas, tamaños distintos, una grande con las dos
ideas de rendimiento/datos combinadas para no llegar a 8 cajas iguales).

**Precio:** tarifa tipográfica con línea de puntos (concepto — valor) a la izquierda; tabla de costes
de Singapur como tabla editorial con la fila de MNKY en teal a la derecha.

**"How it works":** sticky real con CSS (`position:sticky`, sin JS) — el título se queda fijo en
desktop (≥900px) mientras pasan los tres pasos numerados; en móvil se apila normal. Un solo efecto.

**Confianza y FAQ:** bajo el espectáculo: medida de línea corta (42-62ch), `--muted-2` (#c9c7c2, ratio
~13:1 sobre tinta) para todo párrafo largo en vez del gris medio que ya usaba el bento, foco visible.

**Nota de color única:** "Who you deal with" en papel `#F9F6EF` sobre tinta — el único respiro claro
de toda la página, tal como pide el brief.

**Retrato de Miguel:** `<img src="../assets/img/miguel.jpg" onerror="...">` cae al logo (contain, con
relleno) dentro del mismo marco circular de 220px. El día 12/09 que exista el archivo, basta con que
esté en esa ruta — no hay que tocar el HTML, el `onerror` deja de disparar solo.

**Qué dejo fuera:** SplitText real palabra a palabra (ya lo decía la nota de la fase 1); un segundo
efecto sticky o parallax en "how" para no acumular espectáculo sobre la misma sección.

**Riesgo:** el sticky de "how it works" no se ha probado con Lighthouse real; si el CLS del `wrap`
al hacerse sticky penaliza, la salida simple es quitar `position:sticky` en ese breakpoint y dejarlo
apilado como el resto — la marca HTML no cambia. Medir longitud móvil (~12 pantallas) con el propio
Lighthouse antes de dar por cerrado.
