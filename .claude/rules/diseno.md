---
paths:
  - "index.html"
---

# Diseño visual

El estilo es neo-brutalista y está inspirado en la página de enlaces de mouredev. Tiene solo modo oscuro.

- Nunca pongas colores ni sombras sueltos: usa o crea variables en `:root`. Cada color de tarjeta nuevo necesita su variable (`--x`) y su clase utilitaria (`.x { background: var(--x); }`).
- El texto de las tarjetas es `--tinta` (#111). Por eso el color de fondo de una tarjeta tiene que ser claro, con contraste de al menos 4.5:1 con #111. Los tonos oscuros, como el magenta de Instagram, no sirven.
- Bordes: blancos y rectos, sin `border-radius` en tarjetas, botones ni cajas.
- Sombras: blancas, desplazadas y sin difuminar (`--sombra`, `--sombra-hover`).
- Hover y active: `translate` hacia arriba o hacia abajo.
- No añadas un tema claro ni un botón de tema. Se quitó a propósito.
- No uses más fuentes que Poppins.
- No añadas librerías ni frameworks: todo va inline en `index.html`.
- Cualquier cambio de layout tiene que funcionar en móvil. Si hace falta, ajústalo en `@media (max-width: 480px)`.
