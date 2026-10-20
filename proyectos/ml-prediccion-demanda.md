---
nombre: ML Predicción de Demanda
tipo: clase
estado: activo
repo: https://github.com/Jacogz/ML-Prediccion-Demanda
ciclo: 1
inicio: 2026-10-19
appetite: 1 semana (fijada por el curso; entrega 2026-10-26)
---

# ML Predicción de Demanda

## Por qué existe
Proyecto final de Fundamentos de Aprendizaje Automático (2026-2), en equipo con Nicolás Zapata (@Nicolaszj). Predice la demanda diaria por familia de producto con datos de Favorita.
Lo que quiero aprender: construir un pipeline reutilizable (plantilla de datos → variables → entrenamiento → evaluación → artefacto) y seleccionar modelos con validación temporal sin fuga.
Para un empleador: ML de punta a punta, con despliegue y reentrenamiento, no solo un notebook.

## Entregables
En proyectos de clase, esta tabla se sincroniza desde el CLAUDE.md del repo (que es la fuente de verdad). En portafolio, la fuente es esta tabla.

| # | Entregable | Fecha | Descripción | Estado | Enlace |
|---|---|---|---|---|---|
| 1 | Repo + `model_development.ipynb` + video de 2 min | 2026-10-26 | Entrega única; puede cambiar tras la revisión del profesor esta semana | pendiente | |
| 2 | Presentación final | por confirmar | Sustentar problema, metodología, modelo, generalización, métricas, despliegue y reajuste | pendiente | |

Estados: pendiente · en curso · entregado · recortado

## Definición de terminado
Cada criterio debe poder verificarse con un comando, un test o una captura.
- [ ] El notebook `model_development.ipynb` corre completo en un runtime nuevo de Colab: "Ejecutar todo" termina sin errores, también desde la cuenta de Nicolás.
- [ ] El notebook tiene una sección por cada requisito 3.1–3.9 del enunciado; el README los enlaza en una tabla requisito → sección.
- [ ] La división es temporal: un test verifica que `max(fecha_train) < min(fecha_test)` y que ninguna variable usa datos del día predicho o posteriores (`pytest` en verde).
- [ ] Se compara la línea base (mismo día de la semana anterior) contra al menos tres modelos candidatos, con validación cruzada temporal (`TimeSeriesSplit`). El notebook muestra una tabla de MAE por modelo y los hiperparámetros elegidos.
- [ ] El modelo final tiene un MAE en test menor que la línea base, reportado en el notebook y en el README.
- [ ] El pipeline se corre con un solo comando sobre cualquier CSV con la plantilla fija (fecha, categoría, unidades, [precio], [promoción]) y deja un modelo guardado: `python -m src.pipeline --data <csv>` funciona con el subconjunto de Favorita y con un CSV de prueba distinto.
- [ ] Una app de Streamlit en una URL pública permite subir un CSV, ver la predicción y su explicación con SHAP. Verificación: la URL abre en una ventana de incógnito y una captura queda en el README.
- [ ] `docs/reajuste.md` define la métrica de monitoreo, el umbral, la frecuencia y cómo se valida y publica la nueva versión, reutilizando el mismo comando del pipeline.
- [ ] El enlace al video de 2 minutos está en el README.

## Fuera de alcance
- El segundo caso con datos de un negocio real. Solo entra si la revisión del profesor mueve la fecha.
- Infraestructura más allá de Streamlit Community Cloud (Docker, VPS o nube). Se evalúa en el Cierre como candidatura.
- Varias tiendas, todas las familias, modelos de series de tiempo (ARIMA, Prophet) y deep learning.
- Paradigmas no supervisado y de refuerzo.
- Monitoreo automático de drift: solo se diseña, no se implementa.

## Riesgos y huecos conocidos
- **Plazo de 7 días.** Si el 22/10 el pipeline no corre de punta a punta con la línea base, se reduce la lista de candidatos y se simplifica la interfaz.
- **Horizonte, tienda y familias por definir tras el EDA.** Se deciden a más tardar el 21/10; si no, define la variable objetivo y el horizonte y bloquea todo lo demás.
- **Fuga de información.** La tabla de transacciones queda fuera. El precio del petróleo y las promociones solo entran si se conocen antes del día predicho.
- **Fecha sujeta a cambio** por la revisión del profesor.
- **Trabajo en equipo:** reparto con Nicolás y principio 6. Los dos tienen que poder explicar todo en la presentación.
- **Kaggle:** hay que aceptar las reglas de la competencia para descargar los datos. Y Streamlit Cloud necesita acceso al repo.

## Decisiones
- [Pendiente] ADR 0001: plantilla de datos y horizonte de predicción.
- [Pendiente] ADR 0002: modelos candidatos y por qué.

## Cierre
Se llena al archivar o entregar, mientras el contexto está fresco.
- **Estado real:** qué quedó funcionando y qué no.
- **Mi rol:** [si fue en equipo: qué hice yo, qué hicieron otros, nombres].
- **Cómo correrlo:** [comandos].
- **Qué aprendí / qué haría distinto:** 
- **¿Candidato a demo?** IA+infra: sí/no · Derecho a publicar: sí/no · Demo en un ciclo: sí/no
- **Pitch (si los tres son sí):** [5 líneas: qué sería el demo, qué se recorta, cuánto tiempo]. Evaluar aquí la candidatura con infraestructura (Docker / despliegue propio).
