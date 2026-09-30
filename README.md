# Rotisería Yamil – Página de pedidos por WhatsApp

**Página:** https://rotiseriayamil.github.io

Prototipo funcional de una página de pedidos para una rotisería de barrio en General Rodríguez, Buenos Aires. El cliente arma su pedido desde el celular y le llega al negocio por WhatsApp, ordenado y con el total calculado.

Proyecto hecho por **Benjamín Cavia**, 100 % desde el celular (Android), sin computadora.

---

## El problema

- La rotisería recibe unos **300 pedidos por mes** por WhatsApp (unos 30 un sábado a la noche).
- Los pedidos llegan en mensajes sueltos: falta la dirección, el gusto, la forma de pago o el vuelto, y hay que preguntar todo de nuevo.
- Según el dueño, se pierden **unos 3 pedidos por mes por errores**, de unos $20.000 cada uno (≈ $60.000 por mes).
- El catálogo de WhatsApp Business que ya usaban no muestra precios ni calcula totales.

## La solución

Una página simple, pensada primero para celular:

1. El cliente elige del menú, con fotos y precios visibles.
2. Si un producto tiene variantes (carne o pollo, gusto de gaseosa, gustos de empanadas de una promo), la página las pregunta antes de agregarlo.
3. Completa nombre, dirección y forma de pago.
4. Al tocar **"Enviar pedido por WhatsApp"**, se abre WhatsApp con el mensaje armado.

**Quien atiende no tiene que aprender nada nuevo:** el pedido le llega por WhatsApp, como siempre, pero completo.

## Funciones

- **Menú completo** por categorías, con barra fija para saltar entre secciones y lo más vendido primero.
- **Total automático**, incluido el precio por docena y media docena de empanadas.
- **Formas de pago:** efectivo (pregunta con cuánto paga, para el vuelto), transferencia (muestra el alias con botón para copiarlo) y tarjeta.
- **Control de stock desde Google Sheets:** quien atiende destilda una casilla y el producto aparece como "Sin stock hoy".
- **Vista previa al compartir el link:** logo, nombre y frase del negocio.
- **Recuerda los datos del cliente** (nombre y dirección) para el próximo pedido.

## Decisiones de diseño

- **Stock por ingrediente, no por producto.** Si se acaba la milanesa de pollo, se destilda una sola fila y la página bloquea la opción "pollo" en todos los sándwiches y milanesas. Menos casillas, menos errores.
- **Fail-open.** Si la planilla no carga (sin internet, Google caído), todo aparece disponible. Es preferible que el negocio siga recibiendo pedidos a que la página quede vacía.
- **Un solo archivo HTML**, con las fotos incluidas adentro. Se actualiza subiendo un archivo, sin servidor ni base de datos.
- **Colores tomados de la identidad del negocio:** el amarillo del logo y el crema y marrón de sus placas de promociones.
- **Validar antes de construir.** Antes de programar la versión final, se le mostraron al dueño maquetas de dos estilos visuales.

## Tecnologías

- HTML, CSS y JavaScript, sin librerías.
- GitHub Pages para publicar.
- Google Sheets publicado como CSV para el stock.
- Links de WhatsApp (`wa.me`) para enviar el pedido.
- Etiquetas Open Graph para la vista previa del link.

## Estado

**Prototipo funcional, listo para implementar.** Todavía no está en uso con clientes reales, así que no hay resultados medidos.

Para ponerlo en producción falta:
- Cambiar el número de WhatsApp de prueba por el del negocio.
- Confirmar el alias de transferencia.
- Reemplazar las fotos por las originales en buena calidad.
- Definir quién actualiza la planilla de stock.

## Cómo se actualiza

- **Precios y productos:** se editan en la sección `MENÚ` del archivo `index.html`.
- **Número de WhatsApp y alias:** en la sección `CONFIGURACIÓN`, al principio del código.
- **Stock:** desde la planilla de Google Sheets (tildado = hay, destildado = no hay). Los cambios tardan hasta 5 minutos en verse.
