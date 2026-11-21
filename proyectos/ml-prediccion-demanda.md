---
nombre: ML Predicción de Demanda
tipo: clase
estado: entregado
repo: https://github.com/Jacogz/ML-Prediccion-Demanda
ciclo: 1
inicio: 2026-10-19
appetite: 2 semanas (fijada por el curso; entrega 2026-11-03)
---

# ML Predicción de Demanda

## Por qué existe
Proyecto final de Fundamentos de Aprendizaje Automático (2026-2), en equipo con Nicolás Zapata (@Nicolaszj). Predice la venta total del día siguiente de un supermercado (tienda 44 de Favorita, 5 familias de mayor venta).
Lo que quiero aprender: construir un pipeline reutilizable (plantilla de datos → variables → entrenamiento → evaluación → artefacto) y seleccionar modelos con validación temporal sin fuga.
Para un empleador: ML de punta a punta, con despliegue y reentrenamiento, no solo un notebook.

## Entregables
En proyectos de clase, esta tabla se sincroniza desde el CLAUDE.md del repo (que es la fuente de verdad). En portafolio, la fuente es esta tabla.

| # | Entregable | Fecha | Descripción | Estado | Enlace |
|---|---|---|---|---|---|
| 1 | Repo + `model_development.ipynb` + video de 2 min | 2026-11-03 | Entrega única; movida del 2026-10-26 | entregado | [repo](https://github.com/Jacogz/ML-Prediccion-Demanda) |
| 2 | Presentación final | por confirmar | Sustentar problema, metodología, modelo, generalización, métricas, despliegue y reajuste | entregado | |

Estados: pendiente · en curso · entregado · recortado

## Definición de terminado
Cada criterio debe poder verificarse con un comando, un test o una captura.
- [ ] El notebook `model_development.ipynb` corre completo en un runtime nuevo de Colab: "Ejecutar todo" termina sin errores, también desde la cuenta de Nicolás.
- [ ] El notebook tiene una sección por cada requisito 3.1–3.9 del enunciado; el README los enlaza en una tabla requisito → sección.
- [x] La división es temporal: un test verifica que `max(fecha_train) < min(fecha_test)` y que ninguna variable usa datos del día predicho o posteriores (`pytest` en verde).
- [ ] Se compara la línea base (mismo día de la semana anterior) contra al menos tres modelos candidatos, con validación cruzada temporal (`TimeSeriesSplit`). El notebook muestra una tabla de MAE por modelo y los hiperparámetros elegidos.
- [ ] El modelo final tiene un MAE en test menor que la línea base, reportado en el notebook y en el README.
- [x] El pipeline se corre con un solo comando sobre cualquier CSV con la plantilla fija (fecha, categoría, unidades, [precio], [promoción]) y deja un modelo guardado: `python -m src.pipeline --data <csv>` funciona con el subconjunto de Favorita y con un CSV de prueba distinto.
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
- **Plazo de 2 semanas** (era de 7 días antes de mover la entrega al 3/11). Si el 28/10 el pipeline no corre de punta a punta con la línea base (#6), se reduce la lista de candidatos y se simplifica la interfaz.
- **Horizonte por definir** (tienda 44 y 5 familias ya elegidas, #2). Se decide a más tardar el 27/10 en el ADR 0001 (#5); si no, define la variable objetivo y el horizonte y bloquea todo lo demás.
- **Puntos de control hacia el 3/11:** 27/10 ADR 0001 (#5) y EDA de promociones (#4) · 28/10 pipeline con línea base (#6) y spike de Streamlit (#9) · 29/10 variables sin fuga (#7) y ADR 0002 (#8) · 31/10 comparación de modelos con `TimeSeriesSplit` y SHAP (#11) · 1–2/11 Streamlit con SHAP, `docs/reajuste.md`, README y video.
- **Fuga de información.** La tabla de transacciones queda fuera. El precio del petróleo y las promociones solo entran si se conocen antes del día predicho.
- **Fecha sujeta a cambio** por la revisión del profesor.
- **Trabajo en equipo:** reparto con Nicolás y principio 6. Los dos tienen que poder explicar todo en la presentación.
- **Kaggle:** hay que aceptar las reglas de la competencia para descargar los datos. Y Streamlit Cloud necesita acceso al repo.

## Decisiones
- [Pendiente] ADR 0001: plantilla de datos y horizonte de predicción.
- [Pendiente] ADR 0002: modelos candidatos y por qué.

## Cierre
Se llenó el 2026-11-20, después de la entrega (3/11) y la presentación.
- **Estado real:** entregado y presentado; nota perfecta, sin retroalimentación particular. Funciona: notebook con modelo final HGBT (MAE en prueba 2750.6 vs 4125.5 de la línea base, −33 %, WAPE 7.7 %), pipeline de un comando con tests de división temporal y no-fuga, app pública en Streamlit con predicción del día siguiente y explicación SHAP, y video grabado. Todos los issues quedaron cerrados. Contra la definición de terminado, en el repo no quedó evidencia de: corrida completa en un runtime nuevo de Colab, tabla requisito → sección en el README, tercer modelo candidato (se compararon HGBT y Random Forest; el ADR 0002 no se subió), MAE final, captura y enlace al video en el README, y `docs/reajuste.md` (el reajuste quedó dentro del notebook). Se deja así por decisión propia: la entrega se calificó completa.
- **Mi rol:** en equipo con Nicolás Zapata (@Nicolaszj). Yo: modelo final (#12: `GridSearchCV` de HGBT con `TimeSeriesSplit`, selección en 8 semanas de prueba), revisión del pipeline (completar el 25-dic, una sola forma de medir el MAE), la app como herramienta de negocio (WAPE, atribución de la venta por familia, ventana de entrenamiento, datos de prueba) y su publicación en Streamlit Cloud. Nicolás: interpolación de los meses dañados, `src/pipeline.py`, la primera versión de la app y SHAP (#11).
- **Cómo correrlo:** `pip install -r requirements.txt pytest` · `python -m src.pipeline --data <csv>` · `pytest` · `streamlit run app.py`. App: https://fzlsgz3jep2ztsjwtfz3ze.streamlit.app/. El notebook (`src/model_development.ipynb`) corre en Colab con un token de Kaggle (ver README).
- **Qué aprendí / qué haría distinto:** trabajo con series de tiempo (validación temporal, fuga de información, rezagos y huecos de calendario) e interpretabilidad con SHAP. Haría distinto la presentación de los hallazgos: hablarle más a la persona de negocio que usa una herramienta predictiva, sobre todo en la app de Streamlit.
- **¿Candidato a demo?** IA+infra: sí · Derecho a publicar: no · Demo en un ciclo: sí → **no es candidato** por ahora.
- **Pitch:** no aplica (falta el derecho a publicar). La app ya empezó a evolucionar como versión de portafolio (cambios del 6/11, para mostrársela a un posible usuario); si se resuelve el derecho a publicar, se vuelve a evaluar como candidato.
