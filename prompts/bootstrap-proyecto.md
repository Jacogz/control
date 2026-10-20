# Bootstrap de proyecto

<!-- Uso: abrir Claude Code en el repo del proyecto (nuevo) con este repo de control agregado:
       claude --add-dir ~/proyectos/<repo-control>
     y pegar este prompt con las entradas llenas. -->

Vas a convertir una idea o un documento en un proyecto listo para trabajar dentro de mi framework.

## Entradas
- **Fuente:** [idea en texto | ruta o enlace a un documento]
- **Tipo:** [clase | portafolio]
- **Repo del proyecto:** el directorio actual (ya creado y vacío o casi vacío)
- **Repo de control:** ~/Documents/control, agregado con --add-dir

## Antes de empezar
Lee del repo de control: `MANIFIESTO.md`, `proyectos/_plantilla.md`, `plantillas/CLAUDE.proyecto.md` y `plantillas/NEXT.md`. Todo lo que generes debe respetarlos.

## Fase 1 — Entender (no escribas archivos todavía)
1. Si la fuente es un documento, resúmelo en máximo 10 líneas: objetivo, requisitos, restricciones, fechas.
2. Hazme como máximo 5 preguntas, todas juntas, solo sobre lo que falte para llenar la ficha:
   - appetite en semanas;
   - fecha de inicio y fechas de entrega;
   - mi rol y el equipo (si aplica);
   - stack;
   - qué quiero aprender o demostrar.
   No preguntes lo que el documento ya responde.
3. Si es de portafolio, revisa en `proyectos/` si ya hay otro proyecto personal en estado `activo`. Si lo hay, este nace como `candidato`, no como `activo` (principio 3). Dímelo.

## Fase 2 — Ficha (borrador para mi aprobación)
1. Redacta la ficha completa con la plantilla.
2. Cuestiona tu propio borrador antes de mostrármelo:
   - ¿cada criterio de la definición de terminado es verificable?
   - ¿el alcance cabe en el appetite a ~6 h/semana (portafolio) o en las fechas del curso (clase)?
   Si no cabe, propón qué recortar y muévelo a "Fuera de alcance".
3. Muéstrame la ficha y espera mi aprobación o mis cambios.

## Fase 3 — Archivos (después de la aprobación)
En el repo del proyecto:
- `CLAUDE.md`: desde `plantillas/CLAUDE.proyecto.md`, con las secciones [CLASE] solo si aplica, comandos y stack conocidos (deja `[por definir]` en lo que no se sepa) y el índice de documentos inicial. Si es un repo de clase compartido con un equipo, escríbelo como `CLAUDE.local.md` y agrégalo al `.gitignore`.
- `NEXT.md`: desde `plantillas/NEXT.md`, con el primer paso concreto (normalmente, el primer issue sugerido).
- `docs/`: guarda ahí el documento fuente (en `docs/enunciados/` si es un enunciado de clase) e indéxalo.
- `.github/ISSUE_TEMPLATE/`: copia `tarea.yml` e `idea.yml` del repo de control.
- `.gitignore`: con `.env` incluido como mínimo.

En el repo de control:
- `proyectos/<nombre>.md`: la ficha aprobada.

Haz un commit en cada repo (`chore: bootstrap del proyecto`). Pregúntame antes de hacer push.

## Fase 4 — Issues sugeridos (cierre obligatorio)
Termina con una lista de 5 a 8 issues para arrancar, en el formato de la plantilla de tarea:

| # | Título | Resultado esperado | Modo | Verificación |
|---|---|---|---|---|

Reglas para la lista:
- El primero debe poder hacerse en la próxima sesión sin preparación adicional.
- Todos caben en 1 hora; si uno no cabe, divídelo.
- Al menos uno en modo *Solo primero*, en la parte del proyecto donde más quiero aprender.
- Si hay algo riesgoso o desconocido, el primer issue que lo toca es una exploración acotada (spike) de 1 hora, no la implementación.

No crees los issues. Cuando los apruebe, créalos con `gh issue create`, agrégalos al Project con `gh project item-add` y asígnales Tipo y Estado. Si el repo aún no tiene las labels necesarias, créalas antes con `gh label create`.
