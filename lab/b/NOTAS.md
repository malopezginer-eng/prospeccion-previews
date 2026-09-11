# Dirección B — pasada «vibrante» y arreglos (2026-09-11, fase 3)

## Parte 1 — lo que estaba roto
- **«Fast on a phone»** ya no es un rectángulo negro: lleva dentro una **maqueta de móvil en HTML/CSS** copiada y
  adaptada de la dirección A (`.phone`, `.p-topbar`, `.p-hero`, `.p-services`, `.p-hours`, `.p-map`, `.p-cta`), con
  el mismo recorte de foto (`width:230%; left:-65%; top:-27.6%`). Negocio ficticio «YOURSALON», rotulado
  «Example page · not a real business». Todos los bloques llevan `flex: none` y el mapa es el único elástico: no
  colapsa ni desborda, comprobado de 320 a 1600 px.
- El bento pasa a **6 columnas**: la tarjeta grande ocupa 2 col × 3 filas (móvil vertical), cinco tarjetas de 2 col
  y las dos de texto más corto en columnas estrechas. Ninguna celda vacía en ningún ancho; la tarjeta más aireada
  queda al 53 % de aire, el resto por debajo del 50 %.
- **«How it works»** ya no son barras de color: son **tres estados de la misma web** con la captura `after-salon`.
  01 barra `· draft` + sello «draft»; 02 la misma captura con **tres marcas de revisión** en ámbar (recuadro
  discontinuo + etiqueta «photo», «price», «hours»); 03 barra `· live` con **candado SVG** y sello «LIVE» teal.

## Parte 2 — que vibre
- **Dos bandas a color pleno**: las tres cifras sobre teal profundo `#1B615F` (85/76/87 a `clamp(62px,8.6vw,128px)`,
  en blanco) y el cierre sobre el mismo teal con «S$590» gigante en ámbar. «How it works» sigue en tinta y el pie
  pasa a tinta. Ritmo: papel → teal → tinte → papel → tinta → papel → tinte → papel → tinte → teal → tinta.
- **Ámbar `#F2B134`** como acento vivo: marcas de revisión, subrayado de «already built» y de «S$590», filetes de
  sección, número de paso y botón del cierre. Para texto pequeño sobre teal se usa `--accent-lite: #F8CE7E` (4,8:1)
  y `--brand-lite: #2F9A96` para el teal pequeño sobre oscuro, como avisaba el brief.
- Titulares a `clamp(34px,5.2vw,68px)`; retícula de fondo al 4,5 % en las secciones claras; sombras largas y
  distintas por pieza; micro-interacciones de 150-160 ms en botones, tarjetas, filas de la tabla, FAQ y nav.
- **Movimiento**: el barrido del hero sigue siendo el acto principal (arranca al 14 % para que el tirador no se
  corte en móvil); se añaden las cifras contando sobre el teal y el **build escalonado del bento**. La cinta de
  drafts ya existía y sigue parándose en hover y foco. Nada más se anima.

## Comprobado en navegador
Sin scroll horizontal ni recortes de 320 a 1600 px · contraste AA automático: **0 fallos** (incluida la FAQ abierta)
· **12,8 pantallas** a 390 px · HTML bien formado, ninguna caja vacía salvo gradientes decorativos · contenido
completo sin JS y en `prefers-reduced-motion` · solo GSAP 3.13.0 (core + ScrollTrigger) por jsDelivr.
Bug encontrado y corregido de paso: la barra de navegación desbordaba a 1440 px (etiqueta + anclas + botón).

## Retrato de Miguel
Cuando llegue, basta copiar el archivo a `lab/assets/img/miguel.jpg`: la `<img>` ya apunta ahí y el `onerror` la
sustituye por el logo mientras no exista. No hay que tocar el HTML.

## Fuera / riesgo
Fuera: iconos por tarjeta en el bento y la «web espectacular» aparte. Riesgo: entre 620 y 1040 px la mitad izquierda
de la tarjeta grande respira mucho; y las tres capturas de «How it works» son la misma imagen, así que si Miguel
quiere tres pantallas realmente distintas hay que producirlas.
