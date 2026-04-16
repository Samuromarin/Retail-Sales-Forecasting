# Retail Sales Forecasting

Proyecto de series temporales sobre ventas de una empresa retail online (**TodoVentas S.A.**) con el objetivo de predecir las ventas del mes de diciembre de 2023 por país, en el contexto de una decisión de ampliación de capital.

## Objetivo

Comparar tres modelos de predicción (**Prophet**, **SARIMAX** y **XGBoost**) sobre datos de ventas semanales, seleccionar el más adecuado y generar una estimación de ventas para diciembre 2023.

## Dataset

Datos de ventas diarias de TodoVentas S.A. entre diciembre 2022 y diciembre 2023, con transacciones en 10 países europeos. United Kingdom representa el 93% de las ventas totales.

## Estructura del proyecto
├── TodoVentas_proyecto_final.ipynb   # Notebook principal
├── retail_todo_ventas.csv            # Dataset de ventas
└── prod_dict.csv                     # Diccionario de productos

## Metodología

- **Preprocesamiento**: limpieza de datos, agregación semanal por país
- **Análisis exploratorio**: descomposición de la serie, test ADF, ACF/PACF
- **Modelado UK**: comparativa de Prophet, SARIMAX y XGBoost con test en noviembre 2023
- **Variables exógenas**: festivos UK, Black Friday, temporada navideña, cierre navideño
- **Predicción final**: XGBoost aplicado a UK y 9 mercados internacionales

## Resultados

| Modelo | RMSE | MAPE |
|--------|------|------|
| Prophet | 118,111 | 37.72% |
| SARIMAX | 49,995 | 14.37% |
| XGBoost | 62,046 | 16.55% |

> Métricas sobre el periodo de test (noviembre 2023). SARIMAX baseline produce una línea constante — al incorporar variables exógenas deja de serlo pero el MAPE sube a 41.32% por falta de histórico suficiente para calibrar el Black Friday.

**XGBoost** fue seleccionado como modelo final por generar predicciones más realistas semana a semana.

Estimación total diciembre 2023: **£1,257,821** (UK: 91%, mercados internacionales: 9%)

## Principales conclusiones

- La serie muestra una **tendencia ascendente sostenida** a lo largo de 2023
- Las variables exógenas no mejoran los modelos con solo un año de histórico — el Black Friday cae en test y no puede aprenderse en train
- Con 2-3 años de datos la precisión mejoraría significativamente al capturar la estacionalidad de diciembre

## Tecnologías

Python · Pandas · Prophet · Statsmodels · XGBoost · sktime · Plotly
