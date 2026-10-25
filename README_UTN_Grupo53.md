# Predicción de churn bancario — Grupo 53

Trabajo Final Integrador, Diplomatura en Ciencia de Datos y Análisis Avanzado (UTN). Clasificación binaria de abandono de clientes bancarios, comparando cuatro modelos y priorizando al 20% de clientes de mayor riesgo para una campaña de retención.

**Equipo:** Julian Appella, Cintia Opaso, Leonardo Caporossi, Mariangeles Fontela

## Estructura del repositorio

```
├── Entrega_Final_TP_Diplomatura_Data_Science_Grupo53.ipynb   # Notebook principal (ejecutar este)
├── Entrega_Final_Diplomatura_Data_Science_Grupo53.pdf         # Informe/presentación final
├── Churn Modeling.csv                                 # Dataset
└── README_UTN_Grupo53.md
```

Requisitos

- Python 3.9+  
- `numpy`, `pandas`, `matplotlib`, `scikit-learn`, `lightgbm`, `ipython`

```sh
pip install numpy pandas matplotlib scikit-learn lightgbm ipython
```

## Cómo ejecutar

**En Google Colab (recomendado):**

1. Subir `Entrega_Final_TP_Diplomatura_Data_Science_Grupo53.ipynb` a Colab, o abrirlo desde Drive.  
2. `Entorno de ejecución → Ejecutar todas`.  
3. Cuando lo pida, subir `Churn Modeling.csv`.  
4. Esperar a que terminen la validación cruzada, la evaluación en test y los gráficos (unos minutos).

**En local (Jupyter):**

1. Clonar este repositorio.  
2. Instalar las dependencias (ver arriba).  
3. Dejar `Churn Modeling.csv` en la misma carpeta que el notebook.  
4. Abrir el notebook y ejecutar todas las celdas en orden.

Si falta LightGBM, el propio notebook intenta instalarlo automáticamente (requiere conexión a internet).

## Datos

`Churn Modeling.csv` — 10.000 registros, 14 columnas. Target: `Exited` (1 \= abandonó, 0 \= permanece). Fuente citada como Kaggle; licencia y URL exacta pendientes de confirmar.

## Qué genera la ejecución

- `resultados_validacion_cruzada.csv`, `resultados_test.csv`  
- `resumen_resultados_UTN.json`  
- `eda_segmentos.png`, `comparacion_modelos.png`, `curvas_pr.png`, `matriz_confusion.png`, `importancia_variables.png`

## Metodología (resumen)

Split 80/20 estratificado, validación cruzada de 5 folds dentro de train, scores out-of-fold para fijar umbral y comparar modelos por F1 (desempate por PR-AUC). El modelo ganador se elige antes de abrir el test. Evaluados: Regresión Logística, SVM RBF, Árbol de Decisión y LightGBM.

## Resultado principal

**LightGBM** fue el modelo seleccionado (F1 CV-OOF: 0,628; PR-AUC CV: 0,693).

En test: F1 \= 0,642, PR-AUC \= 0,712, ROC-AUC \= 0,867.

Priorizando al 20% de clientes de mayor riesgo se detecta el **63,4%** de los abandonos reales (258 de 407), frente al 20% esperable por azar — un lift de ≈3,17×.

Detalle completo de metodología, resultados, limitaciones e interpretación de negocio en `Entrega_Final_Diplomatura_Data_Science_Grupo53.pdf`.

## Limitaciones

El dataset no tiene dimensión temporal (no se afirma predicción a un horizonte determinado), no hay relación causal demostrada entre contacto comercial y retención, y no se dispone de costos reales de campaña. Ver el informe para el detalle completo.