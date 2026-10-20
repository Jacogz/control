<!-- Plantilla de CLAUDE.md para repos de proyecto.
     Las secciones marcadas [CLASE] se borran en proyectos de portafolio.
     En repos de clase compartidos con un equipo, este contenido va en CLAUDE.local.md
     (agregado al .gitignore), no en CLAUDE.md. Borra este comentario al usarla. -->

# [Proyecto]

[2 líneas: qué es y para qué existe.]
Ficha en el repo de control: [url a proyectos/nombre.md]
Tipo: [clase | portafolio]

## Comandos
- Levantar: `[docker compose up]`
- Tests: `[pytest]`
- Lint/formato: `[ruff check . && ruff format .]`

## Arquitectura e invariantes
- [Invariante 1 — enlace al ADR si existe]
- [Invariante 2]

## Índice de documentos
Documentos relevantes del proyecto. Una línea por documento. Si el índice pasa de ~25 entradas, muévelo a `docs/INDICE.md` e impórtalo aquí con `@docs/INDICE.md`.

| Documento | Ruta o enlace | Descripción | Agregado |
|---|---|---|---|
| Ficha del proyecto | [url] | Alcance, definición de terminado, entregables | AAAA-MM-DD |
| | | | |

### Gestión de documentos
- **Si te pido subir o indexar un documento:** guárdalo en `docs/` (o en `docs/enunciados/` si es un enunciado), agrega su fila al índice con una descripción de una línea y haz commit con `docs: indexa <nombre>`.
- **Si usamos en la sesión un documento que no está en el índice** (pegado en el chat, un enlace, un archivo fuera del repo), pregúntame al cerrar la sesión si lo subo e indexo. No lo agregues sin confirmación.
- Antes de buscar contexto en otro lado, revisa este índice.

## [CLASE] Entregables
Esta tabla es la fuente de verdad de las fechas de este proyecto.

| # | Entregable | Fecha | Descripción | Enunciado |
|---|---|---|---|---|
| 1 | | AAAA-MM-DD | | [docs/enunciados/... o enlace] |

## [CLASE] Asimilar un enunciado nuevo
Cuando comparta un enunciado en la sesión o lo suba al repo:
1. **Guárdalo** en `docs/enunciados/AAAA-MM-DD-titulo.<ext>`. Si lo pegué en el chat, guárdalo como `.md`.
2. **Indéxalo** en el índice de documentos.
3. **Agrega su fila** a la tabla de entregables.
4. **Extrae los requisitos** como una lista de criterios verificables.
5. **Contrástalos con el trabajo actual** (`gh issue list --state open` y la definición de terminado de la ficha) y repórtame tres listas:
   - requisitos ya cubiertos por issues existentes (con número);
   - requisitos nuevos sin issue;
   - ambigüedades o contradicciones, formuladas como preguntas para el profesor.
6. **Propón issues nuevos** para los requisitos sin cubrir, con el formato de la plantilla de tarea: resultado, modo, verificación y tamaño de 1 hora. No los crees sin mi confirmación.
7. **Sincroniza:** actualiza la tabla de entregables de la ficha en el repo de control y el campo "Entrega" del Project. Si no tienes acceso al repo de control en esta sesión, pídeme que lo agregue con `/add-dir` o dime exactamente qué actualizar.

## Protocolo de sesión

### Al iniciar
1. Lee `NEXT.md`.
2. Lee el issue activo (`gh issue view <n>`).
3. [CLASE] Revisa la tabla de entregables. Si hay una entrega en los próximos 7 días, dilo primero.
4. Resume en máximo 3 líneas qué vamos a hacer y en qué modo. Espera mi confirmación antes de tocar código.

### Durante: respeta el modo del issue
- **Delegar:** implementa, corre los tests y resume los cambios.
- **Pareja:** antes de escribir código, propone el enfoque con al menos una alternativa y explica el porqué. Espera mi decisión.
- **Solo primero:** NO escribas código de implementación. Revisa lo que yo escribo, haz preguntas y señala errores y riesgos. Escribe tests solo si te lo pido.

### Al cerrar
1. Actualiza `NEXT.md`.
2. Prepara un comentario para el issue: qué se hizo y qué queda.
3. Pregúntame si algún documento usado en la sesión debe subirse e indexarse.
4. Si hubo cambios en modo Delegar, hazme 2 preguntas concretas sobre ellos antes de proponer el merge. Si no puedo responderlas, no se mergea.

## Reglas
- No amplíes el alcance más allá del issue activo. Si ves algo que vale la pena, propón un issue con label `inbox`.
- Nunca escribas secretos en archivos versionados. Usa `.env`, que debe estar en `.gitignore`.
- Commits con Conventional Commits. Los PR referencian el issue con `Closes #N`.
