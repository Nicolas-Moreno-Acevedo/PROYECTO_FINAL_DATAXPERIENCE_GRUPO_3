# Relación entre los hábitos de vida y el rendimiento académico de adolescentes (13-19 años)

## Descripción del proyecto

Este proyecto realiza un análisis exploratorio de datos (EDA) sobre la relación entre tres hábitos de vida — horas de sueño, uso diario de redes sociales y actividad física — y el rendimiento académico de adolescentes entre 13 y 19 años. Los adolescentes distribuyen su tiempo entre actividades que compiten entre sí (dormir, usar redes sociales, hacer actividad física, estudiar), y no siempre es evidente, a partir de la sola observación cotidiana, de qué manera estos hábitos se relacionan con su desempeño académico. El proyecto documenta de forma ordenada el proceso de Ciencia de Datos seguido: desde la obtención y comprensión de los datos, pasando por su diagnóstico, limpieza y preparación, hasta el análisis exploratorio, el análisis estadístico, el modelado y las conclusiones.

Este trabajo fue desarrollado para el curso **DataXperience** (Grupo 3) de la **Universidad EAN**.

## Objetivo

Analizar exploratoriamente la relación entre determinados hábitos de vida (horas de sueño, uso diario de redes sociales y actividad física) y el rendimiento académico de adolescentes entre 13 y 19 años, identificando asociaciones —no relaciones de causalidad— entre estas variables.

## Pregunta de investigación

**¿De qué modo ciertos hábitos se relacionan con el rendimiento académico de los adolescentes entre 13 y 19 años?**

De esta pregunta principal se derivan las siguientes preguntas específicas:

- ¿Existe relación entre las horas de sueño y el rendimiento académico?
- ¿Existe relación entre el tiempo diario de uso de redes sociales y el rendimiento académico?
- ¿Existe relación entre la actividad física y el rendimiento académico?
- ¿Cuál de estos hábitos presenta la asociación más fuerte con el rendimiento académico?

## Dataset

- **Archivo:** `dataset_salud_mental_Alfons.csv`
- **Procedencia:** publicado en Kaggle por el usuario `alfonselcaudelfons`, bajo una temática de hábitos de vida y salud mental en adolescentes/jóvenes. No se cuenta con el enlace exacto de la página de Kaggle ni con una ficha técnica detallada de la metodología de recolección en los materiales entregados para el proyecto, por lo que esa información no se documenta más allá de lo aquí indicado.
- **Registros:** 2500 (uno por adolescente encuestado).
- **Variables:** 12 columnas, sin valores nulos ni filas duplicadas.

**Variables principales (usadas en el análisis central):**

| Variable | Descripción | Rango observado |
|---|---|---|
| `horas_sueño` | Horas de sueño diarias | 4.0 a 9.0 |
| `horas_diarias_redes_sociales` | Horas diarias en redes sociales | 1.0 a 8.0 |
| `actividad_física` | Nivel de actividad física (escala no documentada en la fuente) | 0.0 a 2.0 |
| `rendimiento_académico` | Variable de resultado (escala no documentada en la fuente) | 2.0 a 4.0 |
| `edad` | Edad del encuestado (delimita la población de estudio) | 13 a 19 |

**Variables secundarias** (se conservan en el dataset y se incluyen en el diagnóstico y la limpieza, pero no se analizan en profundidad porque no forman parte de la pregunta de investigación): `género`, `uso_plataforma`, `tiempo_pantalla_antes_dormir`, `nivel_interacción_social`, `nivel_estrés`, `nivel_ansiedad`, `riesgo_depresión`.

> Para `rendimiento_académico` y `actividad_física` el archivo fuente no documenta una unidad o escala específica, por lo que en todo el proyecto se trabaja únicamente sobre los valores observados, sin asumir que correspondan a un GPA, un promedio sobre una escala determinada o un porcentaje.

## Tecnologías utilizadas

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- SciPy (`scipy.stats`)
- Google Colab / Jupyter Notebook

## Proceso del proyecto

1. **Obtención de los datos:** carga del archivo `dataset_salud_mental_Alfons.csv` con `pandas.read_csv()`.
2. **Comprensión del dataset:** revisión de dimensiones, columnas, primeras filas y diccionario de variables.
3. **Diagnóstico inicial:** verificación de tipos de dato, valores nulos, filas duplicadas, estadística descriptiva y conteo de categorías, sobre el DataFrame original.
4. **Limpieza y preparación:** trabajo sobre una copia (`df_limpio`) que incluye normalización de nombres de columna, eliminación de duplicados exactos, limpieza de espacios en texto, verificación de categorías equivalentes, validación de valores lógicamente imposibles, tratamiento de valores faltantes y creación de variables de grupo (`grupo_sueño`, `grupo_redes`, `grupo_actividad`).
5. **Análisis exploratorio (EDA):** distribución de cada variable principal (histogramas) y detección de valores atípicos (boxplots, regla del IQR).
6. **Análisis estadístico:** cálculo de correlaciones de Pearson entre cada hábito, la edad y el rendimiento académico, con diagramas de dispersión y un mapa de calor de correlaciones.
7. **Comparación por grupos:** rendimiento académico promedio por categoría (Bajo/Medio/Alto) de cada hábito.
8. **Modelado:** ajuste de un modelo de regresión lineal simple (`scipy.stats.linregress`) usando `horas_diarias_redes_sociales` como predictor y `rendimiento_académico` como variable objetivo, por ser el hábito con la correlación más fuerte.
9. **Evaluación:** cálculo de R² y error absoluto medio (MAE), e inspección visual de los residuos del modelo.
10. **Conclusiones y recomendaciones:** interpretación de los resultados dentro de los límites de un análisis correlacional y transversal.

## Estructura del repositorio

```text
/
├── README.md
├── informe/
│   └── Informe_Final_DataXperience_Habitos_Rendimiento.docx
├── notebook/
│   └── Proyecto_DataXperience_Habitos_Rendimiento_CORREGIDO.ipynb
└── datos/
    └── dataset_salud_mental_Alfons.csv
```

## Instrucciones de ejecución

1. **Descargar o clonar el repositorio** en el equipo local, o descargar cada archivo (notebook, CSV e informe) de forma individual.
2. **Ubicar el archivo de datos:** asegurarse de que `dataset_salud_mental_Alfons.csv` esté en la misma carpeta desde la que se ejecuta el notebook (o ajustar la ruta en la celda `pd.read_csv("dataset_salud_mental_Alfons.csv")` si se guarda en otra ubicación).
3. **Abrir el notebook** `Proyecto_DataXperience_Habitos_Rendimiento_CORREGIDO.ipynb`:
   - En **Google Colab**: subir el notebook a Colab (`Archivo > Subir cuaderno`) y luego subir el CSV al entorno de ejecución (`Archivos > Subir`), o montar Google Drive si el CSV está almacenado allí.
   - En **Jupyter/local**: abrir el notebook con Jupyter Notebook o JupyterLab desde la carpeta que contiene también el CSV.
4. **Instalar dependencias**, solo si no están ya disponibles en el entorno: `pandas`, `numpy`, `matplotlib`, `seaborn`, `scipy`. En Google Colab estas librerías ya vienen preinstaladas.
5. **Ejecutar las celdas en orden**, de la Etapa 1 a la Etapa 14, sin saltar celdas, ya que las etapas posteriores dependen de variables creadas en etapas anteriores (por ejemplo, `df_limpio` se crea en la Etapa 4 y se usa en el resto del notebook).
6. **Revisar las salidas**: cada celda de código imprime resultados (tablas, estadísticas) o genera una gráfica; las celdas de texto (Markdown) inmediatamente después de cada bloque de código explican cómo interpretar esa salida.

No se requieren pasos adicionales (no hay claves de API, credenciales ni servicios externos involucrados).

## Resultados principales

- Existe una **asociación negativa fuerte** entre el uso diario de redes sociales y el rendimiento académico (r = -0.863).
- Existe una **asociación positiva fuerte** entre las horas de sueño y el rendimiento académico (r = 0.805).
- Existe una **asociación positiva pero débil** entre la actividad física y el rendimiento académico (r = 0.204).
- La **edad no muestra asociación relevante** con el rendimiento académico (r = -0.001, no significativa), consistente con su papel como variable de delimitación de la población.
- La comparación por grupos de hábito confirma el mismo orden de importancia: redes sociales > horas de sueño > actividad física.
- El modelo de regresión lineal simple (predictor: horas diarias en redes sociales) obtiene **R² = 0.7441** y **MAE = 0.2251** dentro de la muestra analizada.

## Conclusiones

El hábito con la asociación más fuerte con el rendimiento académico, en esta muestra, es el uso diario de redes sociales, seguido de las horas de sueño y, en tercer lugar y con una asociación considerablemente más débil, la actividad física. Todos estos resultados son evidencia de asociación estadística dentro de esta muestra específica, no evidencia de causalidad: el análisis es transversal y correlacional, por lo que no permite afirmar que modificar alguno de estos hábitos produzca, por sí mismo, un cambio en el rendimiento académico de un adolescente en particular.

## Autores

- Laura V. Virguez Letrado
- Simón A. Barrantes Arévalo
- Ana S. Chávez Puerta
- Nicolás D. Moreno Acevedo

**Curso:** DataXperience — Grupo 3, Universidad EAN, Facultad de Ingeniería. Bogotá D. C., Colombia, 2026.
