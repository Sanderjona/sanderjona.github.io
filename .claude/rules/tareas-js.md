---
paths:
  - "index.html"
---

# Lista de tareas (JS)

- El flujo es siempre estado → `guardar()` → `render()`. Ninguna acción toca el DOM de la lista directamente, y `render()` reconstruye la lista entera.
- El texto del usuario se escribe siempre con `textContent` y nunca con `innerHTML`, para evitar XSS.
- Los eventos de la lista se delegan en `#lista` (`change`, `click`, `dblclick`). No añadas listeners a cada `<li>`.
- Cada lectura o escritura de `localStorage` va dentro de try/catch, y la página tiene que funcionar sin almacenamiento.
- No cambies la clave `'tareas-personales'` ni la forma de los objetos (`{ id, texto, hecha }`). Si lo haces, se pierden las tareas guardadas de quien ya visitó la página.
- Mantén la accesibilidad: `aria-pressed` en los filtros, `aria-label` en los botones que solo tienen icono y `.sr-only` en los labels ocultos.
