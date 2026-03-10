```{image} logo.png
:width: 200px
:align: center
```

# KNN — Análisis de Retención Estudiantil

```{admonition} Información del Curso
:class: info

| | |
|---|---|
| **Curso** | Machine Learning — NRC 1627 |
| **Docente** | Lihki Rubio |
| **Integrantes** | Luis Cabarcas · Natalia Frias · Luis Cantillo |
```

Modelo de **K-Nearest Neighbors** para predecir el abandono académico y el rendimiento de estudiantes universitarios, orientado a un sistema de **alerta temprana**.

---

## Objetivo

- **Clasificación:** predecir si un estudiante **abandona** (Dropout) o permanece **Enrolled**.
- **Regresión:** estimar el **promedio final** del estudiante a partir de variables socioeconómicas y académicas.

## Dataset

El dataset contiene **2 209 registros** (tras excluir graduados) con 32 variables predictoras:

| Tipo | Cantidad | Ejemplos |
|---|---|---|
| Categóricas | 9 | Course, Application mode, Nacionality |
| Booleanas | 8 | Tuition fees up to date, Scholarship holder, Debtor |
| Numéricas | 15 | Age at enrollment, Curricular units (enrolled/evaluations) |

> Fuente: [UCI Machine Learning Repository — Predict Students' Dropout and Academic Success](https://archive.ics.uci.edu/dataset/697/predict+students+dropout+and+academic+success)

## Resultados

### Clasificación (k=5, top_n=10)

| Métrica | Test |
|---|---|
| F1-score | **0.77** |
| ROC AUC | **0.77** |
| Recall (Dropout) | **73.6 %** |

### Regresión (k=9, top_n=15)

| Métrica | Test |
|---|---|
| RMSE | **3.788** |
| MAE | **2.557** |
| R² | **0.500** |

## Estructura del Proyecto

```
├── notebooks/
│   ├── 01-eda.ipynb               # Análisis Exploratorio de Datos
│   ├── 02-preprocesamiento.ipynb  # División y Pipeline
│   ├── 03-clasificacion.ipynb     # KNN Clasificación
│   └── 04-regresion.ipynb         # KNN Regresión
├── Data/
│   └── data.csv                   # Dataset
├── conclusiones.md                # Conclusiones del análisis
├── knn-notebook.ipynb             # Notebook completo (referencia)
├── requirements.txt               # Dependencias
└── README.md
```

## Instalación

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```