# movil.html — la maqueta de móvil, interactiva

- Sustituye al `.phone` estático de la tarjeta grande de `#get` en `lab/b/index.html`. No usa GSAP: HTML, CSS y una IIFE.
- Cuatro pestañas reales (`Services`, `Hours`, `Find us`, `Reviews`) como `<button role="tab">` dentro de un `role="tablist"`: `aria-selected`, `aria-controls`, tabindex móvil y flechas ←/→/Home/End. Comprobado en navegador.
- La transición es un deslizamiento lateral de 260 ms en la dirección del cambio; el panel saliente se oculta con `hidden` al terminar. Con `prefers-reduced-motion` se cambia en seco, sin deslizamiento.
- **Sin JS se ven las cuatro secciones una debajo de otra, completas**: las pestañas y la barra inferior solo aparecen con la clase `mkm-js`, y la pantalla solo se fija a 600 px de alto con JS. Verificado.
- El botón de WhatsApp abre una conversación falsa dentro de la pantalla (dos mensajes, entran escalonados), con botón atrás, Esc, `aria-expanded` y foco gestionado. Se cierra sola al cambiar de pestaña. **No abre WhatsApp ni enlaza a `wa.me`**, y lo dice en dos sitios: «Demo · nothing is sent» y «Demo only. This does not open WhatsApp.»
- «Open now / Closed» se calcula en el cliente con la hora real del visitante contra un horario ficticio (Mar–Dom 10:00–20:00, lunes cerrado): «closes at 20:00», «opens today at 10:00», «opens tomorrow at 10:00» o «opens on Tuesday». Se refresca cada minuto y marca el día de hoy en la tabla.
- El HTML de partida trae un horario fijo como texto por si el JS no llega; ninguna caja queda vacía.
- Negocio inventado («Tiong Bahru Hair»), dirección y reseñas ficticias, y dos rótulos que lo dicen. Al integrar, **no** cambiar esto por datos de un negocio real sin su permiso.
- Con JS el `<h3>` de cada panel queda solo para lectores de pantalla (la pestaña ya lo nombra); sin JS se ve como encabezado de sección.
- El mapa es CSS puro (rejilla + calle + chincheta), sin imágenes ni peticiones externas. Nada de la pieza sale a la red salvo las fuentes propias.
- Prefijo `mkm-`. Sin scroll horizontal a 390 px; probado a 390 y a 1280.
