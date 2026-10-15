# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Proyecto

Página personal de enlaces de Sander Ramirez. Es un sitio estático sin compilación, dependencias, pruebas ni linter. Está en un repositorio git (rama `main`, remoto `origin` en GitHub).

- `index.html`: todo el sitio. Tiene el CSS dentro de `<style>` y el JS dentro de `<script>`. Contiene:
  - una cabecera con foto e iconos de redes;
  - una fila de datos y una bio;
  - las tarjetas de enlaces;
  - una lista de tareas guardada en `localStorage`;
  - el bloque «Mis proyectos» (`#proyectos`), con botones de demo y código;
  - el bloque «Mis ideas» (`#lista-ideas`), con tarjetas estáticas sin JS.
- `foto.jpg`: el avatar.

Se publica con GitHub Pages en `https://sanderjona.github.io/` (repositorio público `Sanderjona/sanderjona.github.io`): cada `git push` a `main` actualiza la web en uno o dos minutos. Las etiquetas Open Graph de `index.html` apuntan a esa dirección. La rama local `respaldo-historial` guarda el historial antiguo, que incluye `index-anterior.html`: no la subas nunca (nada de `git push --all`).

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

## Estado del proyecto

### Hecho el 15/10/2026

- Título «sanderdev» en la esquina superior izquierda (`p.marca`). «dev» va en `--azul`.
- La foto (`.avatar`) se mueve al pasar el ratón, igual que las tarjetas de enlaces.
- Sección «Mis proyectos» (`#proyectos`) con cuatro proyectos sacados de los repositorios de GitHub: Bienes raíces, El Blog de Sander, Hello-Git y esta página. En «Mis enlaces» hay una tarjeta que lleva a la sección.
- Etiquetas `meta description`, Open Graph y `twitter:card` para que se vea la vista previa al compartir.
- `index-anterior.html` y `mi-pagina.html` se quitaron y se añadieron a `.gitignore`. El historial se juntó en un único commit para que no aparezcan en GitHub. El historial antiguo quedó en la rama local `respaldo-historial`.
- Web publicada en GitHub Pages: `https://sanderjona.github.io/`.

### Pendiente

- La lista de tareas usa `localStorage`, así que cada visitante ve la suya, vacía, y no las de Sander. Hay que elegir entre convertirla en una lista fija tipo «Ahora estoy aprendiendo…» o dejarla solo para uso personal y quitar su tarjeta de «Mis enlaces».
- Decidir si se quedan las sombras negras de los botones de proyectos (`--sombra-boton`). Rompen la regla de «sombras blancas» de `diseno.md`, pero las blancas casi no se ven sobre las tarjetas claras. Si se quedan, hay que anotarlo en la regla.
- Favicon con el estilo neo-brutalista (por ejemplo, «sd»).
- Botón «Descargar CV» (falta el PDF).
- Quitar los enlaces repetidos: las redes aparecen en los iconos de la cabecera y otra vez en las tarjetas. Ojo con la regla de `redes-sociales.md`, que pide mantener ambos sitios.
- Desactivar las animaciones con `prefers-reduced-motion`.
- Pasar `text-reviewer` a los textos (por ejemplo, «¡Bienvenid@!») y el agente `reviewer` a la accesibilidad. Para el agente hace falta que el MCP de Playwright conecte (el 15/10 falló con un timeout).
- Opcional: añadir una captura de cada proyecto y borrar `respaldo-historial` cuando ya no haga falta.

### Siguiente paso

Decidir qué pasa con la lista de tareas. Ahora que la web es pública, es lo primero que nota un visitante.
