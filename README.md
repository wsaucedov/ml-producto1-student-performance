# Predicción de la nota final en educación secundaria con k-NN

Producto 1 del proyecto integrador · *Machine Learning y Deep Learning* · Escuela de Posgrado – UPG de Ingeniería y Arquitectura, Universidad Peruana Unión.
Docente: Johann A. Ospina-Galindez · Autor: Dr. Walter Saucedo Vega (trabajo individual).

## Problema

¿Qué tan bien puede predecirse la nota final de un estudiante de secundaria en lengua portuguesa (`G3`, escala 0–20) con información disponible al inicio del año (demografía, familia, hábitos y trayectoria escolar), **sin usar las notas parciales** `G1` y `G2`?

- **Tarea:** regresión.
- **Métrica principal:** RMSE (puntos de nota); complementarias: MAE y R².
- **Modelos:** modelo trivial (media) y k vecinos más cercanos (k-NN), con k elegido en un conjunto de validación.
- **Uso previsto:** alerta temprana; el error más costoso es sobrestimar la nota de un estudiante que terminará desaprobando.

## Datos

| Elemento | Detalle |
|---|---|
| Fuente | Cortez, P. (2008). *Student performance* [Conjunto de datos]. UCI Machine Learning Repository. https://doi.org/10.24432/C5TG7T |
| Licencia | CC BY 4.0 |
| Archivo | `student-por.csv` (separador `;`): 649 estudiantes, 30 predictores + `G1`, `G2`, `G3` |
| Datos personales | No contiene nombres ni identificadores |
| Tratamiento | Se excluyen `G1` y `G2` (fuga de información) y los 15 estudiantes con `G3 = 0` (abandono); quedan 634 observaciones |

El notebook descarga el archivo desde una copia pública e idéntica alojada en el repositorio de ejemplos de *Regression and Other Stories* (Gelman, Hill y Vehtari, 2020):
`https://raw.githubusercontent.com/avehtari/ROS-Examples/master/Student/data/student-por.csv`.
Se incluye además una copia en `data/student-por.csv`; para usarla, cambie `DATA_URL` por la URL *raw* de este repositorio.

## Estructura

```
├── Producto1_StudentPerformance.ipynb   # notebook completo (desarrollado desde S01_Producto1_Plantilla.ipynb)
├── data/
│   └── student-por.csv                  # copia de los datos (CC BY 4.0, Cortez, 2008)
├── requirements.txt
└── README.md
```

## Ejecución

**Google Colab (recomendado):** abra el notebook desde GitHub en Colab y ejecute *Entorno de ejecución → Reiniciar y ejecutar todas*. No requiere subir archivos: los datos se cargan desde la URL.

**Local:**

```bash
pip install -r requirements.txt
jupyter notebook Producto1_StudentPerformance.ipynb
```

Todas las particiones usan semillas fijas (`SEMILLA = 2026`; semillas 1–5 en el análisis de variabilidad), por lo que los resultados son reproducibles. El notebook se verificó con Python 3.12, numpy 2.5, pandas 3.0, scikit-learn 1.9 y matplotlib 3.11; la última celda imprime las versiones del entorno en uso.

## Resultados principales (conjunto de prueba, n = 127)

| Modelo | RMSE | MAE | R² |
|---|---|---|---|
| Trivial (media) | 2.58 | 2.12 | −0.01 |
| k-NN (k = 35) | 2.38 | 1.94 | 0.13 |

El k-NN reduce el RMSE en 7.6 %, pero predice notas en un rango estrecho (10.3–14.1) y no identifica a ninguno de los 19 estudiantes que desaprobaron. El k óptimo varía entre 7 y 50 según la partición.

## Licencia y citación

Los datos se distribuyen bajo CC BY 4.0; cite a Cortez (2008) y a Cortez y Silva (2008) al reutilizarlos.
