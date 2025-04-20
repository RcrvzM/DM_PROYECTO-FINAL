# DM_PROYECTO-FINAL

Resumen de Módulos y Funciones
Este resumen describe los módulos, sus funciones, y dónde se utiliza Spark en el código:

**1. Instalación y Configuración de Spark**
****Módulos:** os, findspark, pyspark**
Funciones:

Instalar Java (utilizando comandos del sistema operativo a través de !apt-get).
Descargar y descomprimir Spark (usando !wget y !tar).
Instalar findspark para ubicar la instalación de Spark (!pip).
Configurar variables de entorno (os.environ) para JAVA_HOME y SPARK_HOME.
Inicializar findspark (findspark.init()).
Crear una sesión de Spark (SparkSession).

Spark: crear y configurar la sesión de Spark

**2. Carga de Datos y Formatos**
**Módulos: requests, json, xml.etree.ElementTree, csv, pyspark**
Funciones:

Descargar datos de APIs (Banco Mundial y FMI) usando requests.
Guardar datos en formatos JSON, XML y CSV.
Leer datos desde archivos JSON, XML y CSV utilizando spark.read.
Fuentes de Datos:
API del Banco Mundial (PIB y tasa de empleo).
API SDMX del FMI (tipo de cambio).
Repositorio de GitHub (códigos de países).
Formatos de Datos:
JSON: para datos del PIB y tasa de empleo.
XML: para datos del tipo de cambio.
CSV: para códigos de países y para guardar datos procesados.

Spark: leer datos desde archivos y crear DataFrames.

**3. Limpieza y Preparación de Datos**
**Módulos: pyspark**
Funciones:
Filtrar registros con valores nulos utilizando filter y isNotNull.
Renombrar columnas usando alias.
Convertir tipos de datos con cast.
Spark: realizar las operaciones de limpieza y transformación en los DataFrames.

**4. Unión de Datos**
**Módulos: pyspark**
Funciones:

Unir DataFrames (PIB, empleo y tipo de cambio) usando join en base a las columnas "pais" y "anio".
Especificar el tipo de unión (inner join) para obtener solo los registros coincidentes en todos los DataFrames.

Spark: realizar las operaciones de unión entre DataFrames.


**5. Validaciones de Uniones**
**Módulos: pyspark**
Funciones:

Verificar valores nulos en el DataFrame final usando isNull y cast.
Obtener estadísticas descriptivas con describe.
Contar registros por país con groupBy y count.

Spark:  validaciones y análisis en el DataFrame final.

**6. Entrenamiento del Modelo y Salida**
**Módulos: pandas, matplotlib.pyplot, pyspark.ml.feature, pyspark.ml.regression**
Funciones:

Definir una función (entrenar_y_graficar_proyeccion) que:
Prepara los datos: indexa el país y ensambla features.
Entrena un modelo de regresión lineal (LinearRegression).
Genera proyecciones futuras.
Crea una gráfica con matplotlib.pyplot.
Llamar a la función para entrenar el modelo y visualizar los resultados.

Spark: 
Ingeniería de features (StringIndexer, VectorAssembler).
Entrenamiento del modelo (LinearRegression).
Transformación de datos para la predicción.

**Conclusiones:**

El modelo busca realizar un modelo predictivo base a las siguientes variables.

Las variables predominantes que se utilizan para entrenar el modelo son:

pib_usd: PIB en dólares estadounidenses.
tasa_empleo: Tasa de empleo como porcentaje de la población.
pais_index: Índice numérico que representa al país.
anio: Año al que corresponden los datos.
Estas variables se utilizan como features (variables predictoras) para predecir la variable objetivo tipo_cambio, que es el tipo de cambio de la moneda local frente al dólar estadounidense.

Se intento realizar un entrenamiento de todos los paises juntos utilizando VectorAssembler sin embargo este modelo preductivo entrego variables de salida muy bajas lo que indicaron que no era posible realizar un entrenamiento global para la preduccion ya que cada una de las variables dependen de cada pais,

Estos fueron los valores resultantes.

Modelo global entrenado.
R²: 0.0008

RMSE: 72189.3526

MAE: 3339.8067

Coeficientes: [54.6650551268906,-2.1901394481731463e-10,80.5904101825595,47.36846329731525]

Sin embargo al realizar un entrenamiento por pais, fueron bastante buenos base a la informacion que se tenia y variables seleccionadas dando un modelo predictivo adecuado.

 -_Resultados del modelo para Mexico
R²: 0.9609

RMSE: 1.012

MAE: 0.8584

Coeficientes: [0.8935414171983743,-1.1037892043536777e-11,0.3828599611411305,0.0]

Intercepto: -1792.5016230021602
