---
description: Convierte una idea suelta en una tarjeta nueva del bloque «Mis ideas» (título, descripción y emoji)
argument-hint: <tu idea, como te salga>
---

# /idea: de idea suelta a tarjeta

Idea de Sander:

> $ARGUMENTS

Si la idea está vacía, pregunta cuál es y no sigas hasta tenerla.

## 1. Lee el bloque de ideas

Lee `ul#lista-ideas` en `index.html`, dentro de la sección `#ideas`, para ver las ideas que ya hay y sus colores. Si la idea nueva repite una que ya existe, dilo y pregunta si prefiere mejorar esa en vez de crear otra.

Las ideas van **solo** en `#lista-ideas`. No las metas en «Mis enlaces» (`ul.tarjetas` de arriba) ni toques el bloque de tareas, ni su HTML ni su JS.

## 2. Propón la tarjeta

Convierte la idea en:

- **Emoji**: uno solo, que se entienda de un vistazo.
- **Título**: de 1 a 4 palabras, con mayúscula inicial y sin punto final.
- **Descripción**: una frase corta, de 70 caracteres como máximo, sin punto final y en un tono cercano y en primera persona («Una app para apuntar lo que gasto cada día»).
- **Color**: uno de los que ya existen (`verde`, `azul`, `rosa`, `morado`, `amarillo`, `naranja`), distinto al de la última idea para que no queden dos iguales seguidas.
- **Enlace**: es opcional. Úsalo solo si la idea trae una URL. **No inventes ninguna URL.** Si no hay enlace, la tarjeta no lo lleva.

Enséñale la propuesta así y espera a que la confirme o la ajuste antes de tocar nada:

```
🚀  Título
    Descripción corta
    Color: morado · Enlace: ninguno
```

## 3. Añádela

Cuando la confirme, añade un `<li>` al final de `ul#lista-ideas`. El emoji va directamente en `.icono`.

Si la idea no tiene enlace, usa un `<div>`. Así la tarjeta no se mueve con el hover:

```html
<li>
  <div class="tarjeta COLOR">
    <span class="icono" aria-hidden="true">EMOJI</span>
    <span>
      <span class="titulo">TÍTULO</span>
      <span class="detalle">DESCRIPCIÓN</span>
    </span>
  </div>
</li>
```

Si la idea tiene enlace, usa `<a class="tarjeta COLOR" href="URL" target="_blank" rel="noopener noreferrer">` en lugar del `<div>`.

- Si es la primera idea, borra el párrafo `<p class="ideas-vacio">`.
- Si Sander pide un color nuevo, sigue `.claude/rules/diseno.md`. Crea la variable en `:root` y su clase utilitaria, y comprueba que el color tenga un contraste de al menos 4.5:1 con `#111`.

## 4. Comprueba

Haz una captura con Chrome headless (el comando está en `CLAUDE.md`) y guárdala en el scratchpad. Revisa que la tarjeta se vea alineada con las demás y que el emoji tenga el tamaño correcto. Después enséñale a Sander el resultado.
