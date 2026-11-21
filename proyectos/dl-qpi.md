---
nombre: DL-QPI
tipo: clase
estado: entregado
repo: https://github.com/Jacogz/DL-QPI
ciclo: 1
inicio: 2026-10-24
appetite: ~2.7 semanas (fijada por el curso; entrega 2026-11-11)
---

# DL-QPI

## Por qué existe
Proyecto final del curso de Deep Learning (semestre 2026-2), en equipo con Juan Lotero
(@juanlotero2552) y Sahian Salomé (@sahiansalome14); roles por definir. Tras la reunión del 28-oct, evalúa la viabilidad de traducir imágenes de campo brillante de
eritrocitos (dataset *P. vivax*) a fase plausible tipo DHM con una CycleGAN no pareada, con
pérdidas físicas y morfológicas.
Lo que quiero aprender: GANs / traducción imagen-a-imagen, pareada y no pareada.
Para un empleador: arquitecturas generativas aplicadas a un caso real con restricciones de
datos (dos dominios de imagen sin pares holograma-fase disponibles).

## Entregables
En proyectos de clase, esta tabla se sincroniza desde el CLAUDE.md del repo (que es la fuente de verdad). En portafolio, la fuente es esta tabla.

| # | Entregable | Fecha | Descripción | Estado | Enlace |
|---|---|---|---|---|---|
| 1 | Título + objetivo general + 2-3 específicos | 2026-10-29 | Definición formal del problema, última instancia de decisión: reunión con el profesor el 2026-10-28 | entregado | [README](https://github.com/Jacogz/DL-QPI#readme) |
| 2 | Notebook (Colab) + sustentación | 2026-11-11 | Entrega final. Sustentación el 2026-11-12, informe el 2026-11-13 | entregado | [informe](https://github.com/Jacogz/DL-QPI/blob/main/docs/informe-dl-qpi.pdf) |

Estados: pendiente · en curso · entregado · recortado

## Definición de terminado
Cada criterio debe poder verificarse con un comando, un test o una captura.
- [x] Título, objetivo general y 2-3 objetivos específicos están definidos, documentados en el README y entregados antes de 2026-10-29.
- [ ] El notebook corre completo en un runtime nuevo de Colab ("Ejecutar todo" sin errores), verificado también desde la cuenta de al menos otro integrante del equipo.
- [x] El modelo entrenado reconstruye mapas de fase a partir de las imágenes de entrada definidas el 28-oct, con al menos una métrica cuantitativa reportada en el notebook (p. ej. SSIM/PSNR contra el ground truth del dataset QPI). *Provisional: arquitectura y métrica exactas dependen de la reunión del 28-oct.*
- [x] La sustentación final cubre: problema, metodología, arquitectura, resultados y limitaciones.

## Fuera de alcance
- Cualquier decisión de arquitectura/alcance de modelado anterior a la reunión del 2026-10-28: no se implementa nada de eso hasta confirmarla.
- Despliegue o integración clínica real.
- Expandir el dataset original salvo que la reunión del 28-oct lo defina como el problema a abordar.

## Riesgos y huecos conocidos
- **Problema concreto sin definir** hasta la reunión del 28-oct. El appetite real de ejecución son ~14 días (28-oct → 11-nov), no las 2.7 semanas completas desde hoy.
- **Dos modalidades de imagen distintas** (hologramas DHM vs. campo claro teñido del dataset de malaria) sin pares holograma-fase para malaria → probablemente exige CycleGAN no pareado, más inestable de entrenar que el cGAN pareado del paper de referencia.
- **Roles del equipo sin definir** (Juan, Sahian, yo) — riesgo de reparto desbalanceado; aplica el principio 6 (nada se mergea si no lo puedo explicar) a los tres.
- **Fuente exacta del dataset "P. Vivax (Malaria) Infected Human Blood Smears"** sin confirmar.

## Decisiones
- Problema elegido en la reunión del 2026-10-28: `docs/reunion-2026-10-28.md` (opción 3, puente CycleGAN malaria → fase).
- El ADR de arquitectura (#9) se recortó; la arquitectura quedó en el informe final.

## Cierre
Se llenó el 2026-11-20. Sustentación el 2026-11-12 e informe el 2026-11-13.
- **Estado real:** entregado. La revisión fue muy positiva y el profesor propuso seguir trabajando juntos en el proyecto. Funciona: pipeline de limpieza (notebooks 03–04), segmentación SAM con perfil y delta de fase por célula (05) y CycleGAN no pareada con pérdida física de Δφ y pérdida morfológica (06). Corrida final: KID 0.060 (desde 0.24), IoU 0.71 contra las máscaras, mediana de Δφ 1.98 rad frente a 1.63 real y W1 0.32. No verificado: que el notebook corra completo en un runtime nuevo de Colab desde otra cuenta. La métrica final no fue SSIM/PSNR porque no hay ground truth pareado. Issues #7 y #8 cerrados como hechos, #6 y #9 como recortados.
- **Mi rol:** en equipo con Juan Lotero (@juanlotero2552) y Sahian Salomé (@sahiansalome14). Yo: arquitectura, EDA de ambos datasets, la CycleGAN y sus dos variantes (pérdida física y morfológica), el filtro de densidad de células y el informe final. Juan: limpieza de los datasets (#7). Sahian: segmentación SAM y la heurística de perfil/delta de fase (#8).
- **Cómo correrlo:** notebooks `00` a `06` en orden, en Colab (ver `README_DEV.md`). Las máscaras SAM quedan en Drive bajo `dl-qpi/runs/masks`.
- **Qué aprendí / qué haría distinto:** aprendí de óptica y microscopía digital, CycleGAN y modelos informados por la física. Haría distinto: cambiar cómo se calcula la fase, explorar la fase de las imágenes reales con respecto al fondo, aplicar *phase unwrapping* al dataset, reportar las métricas por época de entrenamiento contra validación después de entrenar, y poner la reconstrucción de fase por célula como foco principal.
- **¿Candidato a demo?** IA+infra: no (IA sí, infra no) · Derecho a publicar: sí · Demo en un ciclo: no → **no es candidato**.
- **Pitch:** no aplica. Es un trabajo de investigación: lo alcanzable en un ciclo sería un informe mucho mejor o el borrador de un artículo, en continuidad con la propuesta del profesor.
