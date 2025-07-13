# INFORME DE PREDICCIÓN AUTOMÁTICA DE FALLOS EN MÁQUINAS MEDIANTE DATOS DE SENSORES

## Introducción

El objetivo de este proyecto es desarrollar un modelo de predicción automática de fallos en distintas máquinas que permita predecir la ocurrencia de posibles averías antes de que ocurran, con el objetivo de:

- Reducir el tiempo de inactividad de las máquinas al evitar paradas no planificadas.
- Reducir la producción de material defectuoso como consecuencia de fallos.
- Optimizar los trabajos de mantenimiento preventivo, realizándolos solo cuando sea necesario.
- Aumentar la productividad de los equipos.

## Descripción de los datos

Los datos utilizados en este proyecto provienen de Kaggle y están disponibles públicamente:

[Kaggle Dataset - Machine Failure Prediction Using Sensor Data](https://www.kaggle.com/datasets/umerrtx/machine-failure-prediction-using-sensor-data/data)

Este conjunto de datos contiene lecturas de sensores de varias máquinas, así como los fallos registrados. A continuación se describe cada columna:

- **footfall**: Número de personas u objetos que pasan por la máquina. Influye en el desgaste.
- **tempMode**: Modo o ajuste de temperatura de la máquina.
- **AQ**: Índice de calidad del aire. El polvo o humedad afectan el rendimiento.
- **USS**: Medición de proximidad. Indica obstáculos o acumulaciones de residuos.
- **CS**: Consumo eléctrico. Un aumento puede indicar sobrecarga o fallo.
- **VOC**: Nivel de compuestos químicos volátiles. Puede afectar los componentes.
- **RP**: Revoluciones por minuto (RPM). Anomalías pueden indicar desgaste mecánico.
- **IP**: Presión de entrada de fluido. Caídas pueden indicar fugas o bloqueos.
- **Temperature**: Temperatura de funcionamiento. Cambios bruscos son señal de posibles fallos.
- **fail**: Variable objetivo. Indica si hubo (1) o no (0) un fallo en la máquina.

## Tecnologías utilizadas

- Python  
- Pandas  
- Numpy  
- Matplotlib  
- Seaborn  
- Scikit-learn  
- imblearn  
- Streamlit  

## Análisis exploratorio (EDA) y preprocesamiento

Se realizó un análisis exploratorio para identificar correlaciones entre variables y patrones que puedan influir en la predicción de fallos. Posteriormente se eliminaron duplicados y se trataron valores atípicos.

Se definieron tres pipelines para adaptar el preprocesamiento al tipo de modelo:

- **Pipeline 1**: Log Transform + Normalización + Balanceo → Modelos lineales, de distancia y probabilísticos.
- **Pipeline 2**: Log Transform + Balanceo → Modelos basados en árboles y probabilísticos.
- **Pipeline 3**: Solo Balanceo → Modelos basados en árboles.

## Modelado y evaluación de modelos

| Tipo de Modelo            | Algoritmo                  | Descripción                                                                                                                                   |
|---------------------------|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------|
| **Modelos Lineales**      | `LogisticRegression`       | Estima la probabilidad de una clase en función de una combinación lineal de características.                                                  |
| **Modelos de Árboles**    | `DecisionTreeClassifier`   | Divide datos en ramas según decisiones en nodos. Captura relaciones no lineales.                                                              |
|                           | `RandomForestClassifier`   | Varios árboles en subconjuntos aleatorios de datos y variables. Reduce sobreajuste.                                                           |
|                           | `GradientBoostingClassifier`| Boosting secuencial. Cada modelo corrige errores del anterior.                                                                                |
|                           | `LightGBM`                 | Boosting eficiente con histogramas y crecimiento por niveles.                                                                                 |
|                           | `XGBoost`                  | Boosting con regularización, manejo de nulos y paralelización. Potente y robusto.                                                             |
| **Modelos de Distancia**  | `KNeighborsClassifier`     | Clasifica según los k vecinos más cercanos en el espacio de características.                                                                  |
|                           | `SVC`                      | Encuentra el hiperplano óptimo. Soporta kernels para relaciones no lineales.                                                                  |
| **Modelos Probabilísticos**| `GaussianNB`             | Clasificador bayesiano. Asume distribución normal para cada característica. Calcula probabilidades condicionales por clase.                  |

### Métricas utilizadas

- **Accuracy**: Porcentaje de predicciones correctas.  
- **Precision**: Proporción de predicciones positivas que realmente lo son.  
- **Recall (Sensibilidad)**: Proporción de fallos reales correctamente detectados.  
- **F1-Score**: Media armónica entre precisión y recall.  
- **ROC AUC**: Área bajo la curva ROC, que muestra la relación entre TPR y FPR.

## Resultados y conclusiones

El modelo seleccionado fue **Logistic Regression**, ya que obtuvo los mejores resultados en las métricas clave:

- **Recall**: 0,911  
- **ROC AUC**: 0,971  

Estos resultados lo convierten en el mejor modelo para detectar la mayoría de fallos reales y minimizar falsos negativos.

## Archivos del proyecto

- `sensores_01.csv`: Dataset utilizado.  
- `cargar_datos.py`: Carga de datos y división entre entrenamiento y test.  
- `data_preprocessing.py`: Procesamiento y creación de pipelines.  
- `model_training.py`: Entrenamiento del modelo.  
- `logisticRegression_fallos.pkl`: Modelo entrenado guardado (pipeline).  

## Estructura del proyecto
📁 proyecto_fallos_maq
├── sensores_01.csv # Dataset de sensores con fallos
├── cargar_datos.py # Carga de datos y división en train/test
├── data_preprocessing.py # Preprocesamiento de datos 
├── model_training.py # Entrenamiento del modelo y pipelines
├── logisticRegression_fallos.pkl # Modelo entrenado guardado
├── app.py # Aplicación en Streamlit para uso del modelo
└── README.md # Documentación del proyecto

## Ejecución Local
1. Clona el repositorio:
git clone https://github.com/h2p5b7m9/Prediccion_paradas_de_maquinas
2. Instala las dependencias:
pip install -r requirements.txt
3. Ejecuta la app:
streamlit run app.py

## Autor

**Ignacio Macipe**
Grado Superior en desarrollo de aplicaciones web | Ciencia de Datos | Consultor host