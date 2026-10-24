---
nombre: DL-QPI
tipo: clase
estado: activo
repo: https://github.com/Jacogz/DL-QPI
ciclo: 1
inicio: 2026-10-24
appetite: ~2.7 semanas (fijada por el curso; entrega 2026-11-11)
---

# DL-QPI

## Por qué existe
Proyecto final del curso de Deep Learning (semestre 2026-2), en equipo con Juan Lotero
(@juanlotero2552) y Sahian Salomé (@sahiansalome14); roles por definir. Reconstruye mapas de
fase cuantitativa (QPI) a partir de hologramas de microscopía holográfica digital (DHM), con
foco en eritrocitos infectados con malaria (*P. vivax*), probablemente con una arquitectura
tipo CycleGAN.
Lo que quiero aprender: GANs / traducción imagen-a-imagen, pareada y no pareada.
Para un empleador: arquitecturas generativas aplicadas a un caso real con restricciones de
datos (dos dominios de imagen sin pares holograma-fase disponibles).

## Entregables
En proyectos de clase, esta tabla se sincroniza desde el CLAUDE.md del repo (que es la fuente de verdad). En portafolio, la fuente es esta tabla.

| # | Entregable | Fecha | Descripción | Estado | Enlace |
|---|---|---|---|---|---|
| 1 | Título + objetivo general + 2-3 específicos | 2026-10-29 | Definición formal del problema, última instancia de decisión: reunión con el profesor el 2026-10-28 | pendiente | |
| 2 | Notebook (Colab) + sustentación | 2026-11-11 | Entrega final: reconstrucción de QPI, metodología, resultados | pendiente | |

Estados: pendiente · en curso · entregado · recortado

## Definición de terminado
Cada criterio debe poder verificarse con un comando, un test o una captura.
- [ ] Título, objetivo general y 2-3 objetivos específicos están definidos, documentados en el README y entregados antes de 2026-10-29.
- [ ] El notebook corre completo en un runtime nuevo de Colab ("Ejecutar todo" sin errores), verificado también desde la cuenta de al menos otro integrante del equipo.
- [ ] El modelo entrenado reconstruye mapas de fase a partir de las imágenes de entrada definidas el 28-oct, con al menos una métrica cuantitativa reportada en el notebook (p. ej. SSIM/PSNR contra el ground truth del dataset QPI). *Provisional: arquitectura y métrica exactas dependen de la reunión del 28-oct.*
- [ ] La sustentación final cubre: problema, metodología, arquitectura, resultados y limitaciones.

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
- [Pendiente] ADR 0001: problema concreto a abordar y arquitectura (CycleGAN vs. otra), tras la reunión del 2026-10-28.

## Cierre
Se llena al archivar o entregar, mientras el contexto está fresco.
- **Estado real:** qué quedó funcionando y qué no.
- **Mi rol:** [si fue en equipo: qué hice yo, qué hicieron otros, nombres].
- **Cómo correrlo:** [comandos].
- **Qué aprendí / qué haría distinto:**
- **¿Candidato a demo?** IA+infra: sí/no · Derecho a publicar: sí/no · Demo en un ciclo: sí/no
- **Pitch (si los tres son sí):** [5 líneas: qué sería el demo, qué se recorta, cuánto tiempo].
