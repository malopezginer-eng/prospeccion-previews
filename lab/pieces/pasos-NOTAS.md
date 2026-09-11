# pasos.html — los tres pasos, contados

- Sustituye a la `<ol class="steps">` de `#how` en `lab/b/index.html`. Los tres titulares y sus párrafos son literales de ahí; las notas del cliente («make this bigger», «use our photo», «we open at 10») son microcopy nuevo.
- Una sola página dibujada en HTML/CSS dentro del marco, y un timeline de GSAP con `scrub` sobre `.mkp-stage` (360vh en escritorio, 240vh en móvil). El bloque queda quieto con `position: sticky`, **sin `pin`**.
- **RIESGO Nº1 AL INTEGRAR:** la web actual lleva `body { overflow-x: hidden }` y eso **rompe `position: sticky`** (crea un contenedor de scroll). Cámbialo a `overflow-x: clip` o quítalo; si no, la secuencia no se queda pegada.
- La página del marco se mide en `cqw` (`container-type: inline-size` en `.mkp-browser`, `font-size: 1.68cqw` en `.mkp-page`) y todo lo de dentro va en `em`: escala exacta a cualquier ancho. Comprobado: el contenido cabe justo en la caja 16:10, sin hueco ni recorte. Si tocas un texto o un padding, vuelve a mirar que `.mkp-doc` no desborde.
- Los porcentajes del esqueleto (`#mkpSk i`) y de las anotaciones (`.mkp-a1/a2/a3`) están calcados de la maqueta medida en el navegador. Si cambias la maqueta, hay que recalcularlos.
- Sin JS, sin GSAP o con `prefers-reduced-motion`, la clase `.mkp-anim` no llega a ponerse: el raíl no ocupa alto, nada queda pegado y se ve la página **terminada** (URL `live`, foto final, horario corregido) con los tres pasos completos. Verificado.
- El `.mkp-swap` apila dos textos en la misma celda de grid (draft/live y los dos horarios); en estado base solo se ve el final, por CSS. No quites esas reglas.
- Los rótulos de paso se encienden por `onUpdate` del ScrollTrigger con cortes en 0.38 y 0.775, alineados con el timeline. Si mueves tiempos, mueve los cortes.
- En móvil solo el paso activo lleva párrafo, para que el bloque pegado quepa siempre en pantalla.
- GSAP 3.13.0 por jsDelivr con `defer`. Ojo: **un `<script>` en línea ignora `defer`**, por eso el JS espera a `DOMContentLoaded` (si no, GSAP aún no existe y la pieza se cae al estado estático).
- Prefijo `mkp-`, IIFE, sin conflictos con las clases de la web actual.
