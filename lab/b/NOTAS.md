# Dirección B — web completa (2026-09-11, fase 2)

**Qué he construido:** las 13 secciones del brief sobre el hero ya aprobado, sin tocarlo. El hilo
conductor es el marco de navegador (tres puntos + barra de dirección), usado 3 veces con cabeza: el
hero/teatro (ya existía), los tres pasos de «How it works» (mini ventanas CSS, sin imágenes, con la
URL cambiando `yoursalon.com.sg · draft` → `· edits` → `yoursalon.com · live`) y el marquee de
«Recent drafts». El resto de secciones (stats, get, price, safe, who, faq, cta) son papel/teal planos,
para que el recurso no se repita hasta el ridículo, tal y como pide el brief.

**Decisiones de composición:** «What you get» es un bento asimétrico (1 tarjeta grande oscura + 1
acento teal + 6 normales), no 8 tarjetas iguales. «How it works» sigue en fondo oscuro (`--ink`) como
la web fuente: es el único acento oscuro de la página, coherente con el resto en papel. No añadí un
segundo efecto de scroll grande: los tres pasos usan solo `data-reveal-group` (fade+slide ligero), el
barrido con `pin`+`scrub` del hero sigue siendo el único efecto grande. Fusioné «Recent drafts» con el
marquee ya construido en fase 1 (mismo bloque, cabecera y texto de advertencia copiados literales de
la web fuente) en vez de duplicar las cuatro previews en una rejilla aparte.

**Retrato de Miguel:** `#who` usa `<img id="miguelPhoto" src="../assets/img/miguel.jpg" onerror="...">`
— si el archivo no existe cae automáticamente al logo (`logo-512.png`, con `object-fit:contain` y
relleno en tinte) dentro del mismo círculo de 200px. El día 12/09 en que llegue `miguel.jpg` no hay que
tocar nada más: el `onerror` deja de dispararse y se ve la foto real recortada en círculo.

**Dejado fuera:** subtítulo largo repetido (ya está como `.lead` bajo el H1); segundo marco de
navegador en «what you get» o «price» (se dejaron en tarjetas planas a propósito, ver arriba); rejilla
separada de drafts (ver fusión con marquee).

**Riesgo:** no he verificado en navegador real con Lighthouse; el pin de ScrollTrigger en el hero es
el mismo de la fase 1 (riesgo ya anotado entonces). La página completa mide justo por debajo de las 12
pantallas de móvil pedidas — si Miguel la ve más larga de la cuenta en el móvil, el primer recorte
lógico es apretar el `padding` de `section` (clamp actual 48–96px), no quitar contenido.
