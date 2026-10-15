---
name: text-reviewer
description: Revisa los textos visibles de la web de Sander (index.html) para corregir la ortografía y la puntuación, mantener un tono cercano y cambiar los anglicismos por palabras en español. Úsala cuando Sander pida revisar, corregir o pulir los textos, la redacción, las faltas o el tono de su web, o de una parte concreta (bio, tarjetas, ideas, tareas…).
argument-hint: "[parte opcional: bio, enlaces, ideas, tareas…]"
model: sonnet
---

# text-reviewer: revisión de los textos de la web

Revisa los textos de `index.html` que ve el visitante. Si Sander indica una parte (`$ARGUMENTS`), revisa solo esa. Si no, revisa la página entera.

**Primero propón los cambios y no edites nada hasta que Sander los apruebe.**

## 1. Qué textos revisar

Revisa todo lo que lee o escucha una persona:

- `<title>`, `h1`, `h2`, la fila `p.datos` y la `.bio`;
- `.titulo` y `.detalle` de las tarjetas de «Mis enlaces» y de «Mis ideas»;
- en el bloque de tareas: `placeholder`, botones, filtros, el texto de lista vacía, `.ayuda` y el contador;
- los atributos `alt`, `aria-label` y los `<label>` (incluidos los `.sr-only`);
- el `footer`;
- las cadenas de texto del JS que acaban en pantalla (por ejemplo, el texto del contador, «pendientes»).

Hay cosas que no se tocan:

- **Nombres propios y marcas**: GitHub, LinkedIn, TikTok, Instagram, Microsoft MVP, GitHub Star, Poppins…
- Nombres de usuario, URL, el email y los comentarios del HTML.
- El código: clases, ids, variables, claves de `localStorage` (`'tareas-personales'`) y valores internos como `data-filtro="todas"`.

## 2. Qué buscar

### Ortografía y puntuación (según la RAE y la Fundéu)
- Tildes: «está», «aquí», «qué» en preguntas y exclamaciones, «júnior»… Y también tildes que sobran: «solo», «guion» y «este» no llevan tilde.
- Los signos de apertura `¿` y `¡`, y la puntuación entre frases (por ejemplo, un punto antes de abrir una exclamación).
- Mayúsculas: no van después de dos puntos, salvo excepciones, ni en meses o días.
- Erratas, letras repetidas y concordancias de género y número.
- Formas que la RAE no acepta, como la arroba para el género (`Bienvenid@`). Propón una alternativa natural, como «¡Te doy la bienvenida!».
- Una regla de esta web: las descripciones de las tarjetas (`.detalle`) no llevan punto final.

### Tono cercano
- Tutea siempre al visitante (tú, no usted) y mantenlo igual en toda la página. Es el tono que ya usa la web: «Escríbeme», «Mira mis proyectos», «¿Qué necesitas hacer?».
- Sander habla en primera persona, con frases cortas, claras y cálidas.
- Marca lo que suene frío, corporativo o de plantilla («Proceda a…», «Haga clic aquí», «Contenido no disponible») y propón una versión más natural.
- No exageres el tono: nada de demasiadas exclamaciones, emojis en el texto ni expresiones forzadas.

### Anglicismos
Cuando haya una palabra en español clara y natural, proponla. Algunos ejemplos:

| Anglicismo | Alternativa |
|---|---|
| link | enlace |
| post | publicación |
| feedback | comentarios, opinión |
| app | aplicación (*app* se usa mucho; márcalo como opcional) |
| email, mail | correo, correo electrónico |
| online | en línea, en internet |
| skills | habilidades, conocimientos |
| tips | consejos |
| checklist | lista de comprobación, lista |
| delete, clear | borrar, limpiar |
| deadline | fecha límite |
| full stack, frontend, backend | términos técnicos asentados: márcalos solo como opcionales y en cursiva |

No traduzcas los nombres propios ni las marcas. Si un término técnico no tiene un equivalente que suene natural, déjalo como está y no lo marques.

## 3. Cómo presentar la revisión

Agrupa los hallazgos por categoría y numéralos para que Sander pueda decir «aplica 1, 3 y 5»:

```
### Ortografía
1. index.html:470 · bio
   Ahora:     «…mis enlaces ¡Bienvenid@!»
   Propuesta: «…mis enlaces. ¡Te doy la bienvenida!»
   Motivo:    falta el punto antes de la exclamación; la arroba no es un signo lingüístico

### Tono
…

### Anglicismos
…
```

- Indica siempre el archivo, la línea y la parte de la página donde está el texto.
- Distingue entre **errores**, que conviene corregir, y **sugerencias** de estilo, que son opcionales.
- Si no encuentras nada en una categoría, dilo en una línea.
- Termina con un resumen corto, por ejemplo: «3 errores, 2 sugerencias».

## 4. Aplicar los cambios

Cuando Sander apruebe los cambios:

- Aplica solo los que haya elegido, con `Edit`.
- Respeta las reglas de `.claude/rules/`:
  - en `p.datos` y la bio solo se corrige la forma, nunca se inventan datos;
  - en el JS de tareas no se cambian la estructura ni las claves.
- Si un cambio afecta al texto que se ve, haz una captura con Chrome headless (el comando está en `CLAUDE.md`). Guárdala en el scratchpad y comprueba que nada se rompe ni se desborda, sobre todo en las tarjetas.
- Al final, enumera lo que cambiaste.
