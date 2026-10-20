# Repo de control

Fuente de verdad de mi framework de proyectos: manifiesto, fichas, plantillas y prompts.
El código de cada proyecto vive en su propio repo.

## Estructura

```
repo-control/
├── README.md                     ← este archivo: estructura y montaje
├── MANIFIESTO.md                 ← principios, ritmo, ciclos, rituales
├── CLAUDE.md                     ← instrucciones para Claude Code en este repo
├── proyectos/
│   └── _plantilla.md             ← plantilla de ficha de proyecto
├── plantillas/
│   ├── CLAUDE.proyecto.md        ← plantilla de CLAUDE.md para repos de proyecto
│   └── NEXT.md                   ← plantilla de NEXT.md para repos de proyecto
├── prompts/
│   ├── bootstrap-proyecto.md     ← idea/documento → proyecto listo (Claude Code)
│   ├── revision-semanal.md       ← tarea programada de Cowork (domingo)
│   └── cowork-control.md         ← instrucciones del proyecto "Control" en Cowork
└── .github/ISSUE_TEMPLATE/
    ├── tarea.yml                 ← unidad de trabajo de 1 hora
    └── idea.yml                  ← captura rápida al inbox
```

## Montaje (una sesión de 1 hora)

1. Crear el repo en GitHub y subir estos archivos. Reemplazar los `[corchetes]`.
2. Crear un GitHub Project (de usuario) con:
   - Campos: Estado (selección única: idea, candidato, activo, demo, vivo, entregado, archivado), Tipo (`portafolio` / `clase`), Iteración (1 semana), Entrega (fecha).
   - Vistas: "Esta semana" (`iteration:@current`), "Inbox" (`label:inbox`), "Tablero" (agrupado por Estado).
3. Crear las labels `inbox`, `candidato-demo` y una por proyecto (`ferv`, `dfs`) en cada repo que las use. Si la label no existe, la plantilla de idea no la aplica.
4. Crear en este repo un issue fijo "Revisiones semanales" y anotar su número en `prompts/revision-semanal.md` y `prompts/cowork-control.md`.
5. En Cowork: crear el proyecto "Control", pegar el contenido de `prompts/cowork-control.md` como instrucciones, conectar GitHub y programar la revisión semanal (domingo en la noche).
6. Verificar:
   - [ ] El conector de GitHub en Cowork puede comentar en el issue de revisiones (escritura real, no solo lectura).
   - [ ] La tarea programada corre con el computador apagado.
   - [ ] Las plantillas de issue se ven bien en GitHub Mobile (si la captura es lenta, usar issue en blanco + label `inbox`).
   - [ ] `gh auth status` funciona en la shell.

## Cuándo montar este repo como directorio adicional en Claude Code

Solo cuando la sesión necesita leer o escribir archivos de aquí. Los issues y el Project se manejan con `gh` sin necesidad del directorio.

| Momento | ¿`--add-dir` / `/add-dir`? |
|---|---|
| Sesión normal de trabajo en un proyecto | No |
| Bootstrap de un proyecto | Sí, desde el inicio |
| Asimilar un enunciado de clase | Sí (a mitad de sesión con `/add-dir`) |
| Ritual de cierre de un proyecto de clase | Sí |
| Planeación del lunes | No: abrir Claude Code directamente aquí |

No activar `CLAUDE_CODE_ADDITIONAL_DIRECTORIES_CLAUDE_MD`: los prompts leen de este repo solo lo que necesitan.
