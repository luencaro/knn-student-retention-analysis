---
title: Conclusiones
---

# Conclusiones

### Clasificación 

- El grid search con **5-fold Stratified CV** seleccionó **k\* = 5** y **top_n\* = 10** como la mejor combinación, con un F1 medio de **0.7669**.
- En test, el modelo alcanzó un **F1 = 0.77**, **ROC AUC = 0.77** y un **Recall de 73.6 %** para la clase Dropout, lo que indica que detecta aproximadamente 3 de cada 4 estudiantes en riesgo de abandono.
- La matriz de confusión muestra 209 Dropouts correctamente identificados frente a 75 falsos negativos, y 57 falsas alarmas sobre 159 Enrolled. El principal costo del modelo son los estudiantes que abandonan sin ser detectados (~26 %).
- La curva ROC confirma que el modelo supera ampliamente al clasificador aleatorio, con un umbral óptimo en **0.60**. El AUC es estable entre distintos valores de k (0.742–0.772), evidenciando robustez.
- El heatmap del grid search muestra que los scores F1 son relativamente estables (0.735–0.767), lo que sugiere que el modelo no es hipersensible a los hiperparámetros. No obstante, top_n = 10 ofrece consistentemente los mejores resultados.

### Regresión 

- El grid search con **5-fold CV** seleccionó **k\* = 9** y **top_n\* = 15**, con un RMSE medio de **3.7321**.
- En test: **RMSE = 3.788**, **MAE = 2.557** y **R² = 0.500**. El modelo explica el 50 % de la varianza del promedio final, con un error absoluto medio de ~2.6 puntos.
- El gráfico de predicción vs valor real revela que el modelo predice bien la zona de notas altas (10–14), pero tiene dificultades con estudiantes de promedio cercano a 0 (muchos Dropout), donde tiende a sobreestimar la nota. **El modelo de regresión solo tiene sentido para estudiantes con actividad académica registrada.** El EDA reveló que una fracción significativa de Dropout presenta `promedio_final = 0` porque abandonaron antes de cursar o ser evaluados en materias, de ahí la bimodalidad del target y el pico en 0. En el scatter de predicción vs real, el cluster en valor real = 0 es donde el modelo comete los errores más grandes y sistemáticos, inflando artificialmente el RMSE (3.788). De limitarse a estudiantes con al menos una unidad evaluada, las métricas de regresión mejorarían sustancialmente y reflejarían mejor la capacidad real del modelo para estimar rendimiento académico.

- Más features (top_n = 15) mejoran la regresión, al contrario que en clasificación (top_n = 10), sugiriendo que predecir la nota requiere capturar más matices del perfil del estudiante.

Finalmente podemos afirmar, que:

- **Las variables financieras son las más discriminantes**: estar al día en matrícula, no tener deudas y tener beca reducen drásticamente la probabilidad de abandono.
- **Las unidades curriculares** (enrolled, evaluations) del 1er y 2do semestre son los predictores más fuertes para ambos targets, confirmando que el rendimiento académico temprano es la señal de alerta más clara.
- KNN ofrece un modelo interpretable y razonablemente preciso como **línea base** para un sistema de alerta temprana, aunque modelos más complejos (e.g., ensemble methods) podrían mejorar el rendimiento, especialmente en la zona de notas bajas en regresión.