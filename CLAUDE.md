# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Proyecto

Página personal de enlaces de Sander Ramirez. Es un sitio estático sin compilación, dependencias, pruebas ni linter. Está en un repositorio git (rama `main`, sin remoto).

- `index.html`: todo el sitio. Tiene el CSS dentro de `<style>` y el JS dentro de `<script>`. Contiene:
  - una cabecera con foto e iconos de redes;
  - una fila de datos y una bio;
  - las tarjetas de enlaces;
  - una lista de tareas guardada en `localStorage`;
  - el bloque «Mis proyectos» (`#proyectos`), con botones de demo y código;
  - el bloque «Mis ideas» (`#lista-ideas`), con tarjetas estáticas sin JS.
- `foto.jpg`: el avatar.

Se publicará con GitHub Pages en `https://sanderjona.github.io/` (repositorio público `sanderjona.github.io`). Las etiquetas Open Graph de `index.html` ya apuntan a esa dirección.

Las reglas detalladas están en `.claude/rules/`:

| Archivo | Tema |
|---------|------|
| `idioma.md` | Idioma y nombres |
| `diseno.md` | Diseño visual |
| `redes-sociales.md` | Enlaces y redes sociales |
| `tareas-js.md` | Lista de tareas (JS) |
| `archivos-y-verificacion.md` | Archivos y verificación |

Comandos en `.claude/commands/`:

- `/idea <texto>`: convierte una idea suelta en una tarjeta nueva del bloque «Mis ideas» (`ul#lista-ideas`), con emoji, título, descripción, color y un enlace opcional. Propone la tarjeta y espera confirmación antes de editar.

Skills en `.claude/skills/`:

- `text-reviewer`: revisa los textos visibles de `index.html` (ortografía, tono cercano con tuteo y anglicismos). Propone los cambios numerados y solo los aplica cuando Sander los aprueba. Siempre se ejecuta con Sonnet (`model: sonnet` en su frontmatter).

Agentes en `.claude/agents/`:

- `reviewer` (`reviewer.md`): audita la accesibilidad de `index.html` según WCAG 2.2 AA y devuelve una lista priorizada de mejoras. Usa Opus y es de solo lectura: tiene `Read`, `Grep`, `Glob` y las herramientas de Playwright para navegar y ver el árbol de accesibilidad, pero no `Edit`, `Write` ni `Bash`. Necesita el servidor en marcha para revisar la página en vivo.

MCP del proyecto en `.mcp.json`:

- `playwright` (`@playwright/mcp`): controla un navegador para abrir `http://localhost:8000`, hacer clic, rellenar formularios y sacar capturas. Sirve para probar la lista de tareas o la versión móvil, que Chrome headless no renderiza por debajo de unos 500 px.
  - Solo puede guardar archivos dentro del proyecto. Guarda las capturas en `.playwright-mcp/`, muévelas al scratchpad y borra esa carpeta al terminar.
  - El navegador guarda el HTML en caché: después de editar, abre la URL con `?v=N` para ver los cambios.

## Cómo ejecutarlo

```sh
python -m http.server 8000   # desde la raíz del proyecto; luego abre http://localhost:8000
```

Captura para revisar el resultado:

```sh
"/c/Program Files/Google/Chrome/Application/chrome.exe" --headless=new --disable-gpu --hide-scrollbars --window-size=780,1500 --screenshot=out.png http://localhost:8000/index.html
```

Chrome headless no renderiza por debajo de unos 500 px de ancho. La versión móvil (`max-width: 480px`) se revisa en el modo dispositivo de DevTools (F12).

Para abrir el proyecto en Antigravity, usa `"$LOCALAPPDATA/Programs/Antigravity IDE/bin/antigravity-ide" .`. El comando `antigravity` no existe.
