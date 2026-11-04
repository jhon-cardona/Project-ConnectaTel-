📊 Análisis de clientes ConnectaTel

Proyecto final del Sprint 7 (Bootcamp de Análisis de Datos). Análisis exploratorio, limpieza y segmentación de los clientes de ConnectaTel, una empresa de telecomunicaciones en Latinoamérica, usando datos de 2024.

🎯 Objetivo

Evaluar el comportamiento de los clientes para:

Construir un perfil estadístico de uso por usuario.
Detectar comportamientos atípicos (outliers).
Crear segmentos de clientes por nivel de uso y por edad.
Proponer recomendaciones de planes y retención para el negocio.
🗂️ Datasets
Archivo	Contenido
plans.csv	Planes disponibles (precio, minutos y GB incluidos, costo por extra). Solo 2 filas.
users_latam.csv	4 000 clientes: edad, ciudad, fecha de registro, plan y fecha de cancelación (churn).
usage.csv	40 000 registros de uso real: llamadas y mensajes (tipo, fecha, duración, longitud).

Los CSV no están incluidos en el repositorio. El notebook los lee desde /datasets/, la ruta del entorno del bootcamp.

🧪 Etapas del análisis
Carga y exploración: lectura de los 3 datasets, shape, info() y vista previa.
Calidad de datos: nulos, valores centinela y fechas imposibles.
Limpieza
age: el centinela -999 se reemplaza por la mediana.
city: el "?" se convierte en nulo.
reg_date: solo las fechas del año 2026 (imposibles) pasan a NaT. Los registros válidos de 2024 se conservan.
duration y length: los nulos son MAR (dependen de type), por lo que se dejan como nulos.
Estadísticas por usuario: se agrega usage por user_id (mensajes, llamadas y minutos) y se une a users con un left merge. El usuario sin actividad queda con 0 en las tres métricas (fillna(0)).
Visualización: histogramas por plan (hue='plan') y boxplots.
Outliers: método IQR con límite superior y porcentaje de outliers sobre el total válido. Se mantienen porque son valores plausibles de usuarios muy activos.
Segmentación
Por uso (grupo_uso): Bajo uso, Uso medio y Alto uso, según llamadas y mensajes.
Por edad (grupo_edad): Joven (< 30), Adulto (30–59) y Adulto Mayor (60 o más).
Insight ejecutivo: problemas de datos, segmentos, valor para el negocio, outliers y recomendaciones.
🔍 Hallazgos principales
Calidad de datos: 55 centinelas en age, 565 ciudades sin dato (469 nulos y 96 "?") y 40 fechas de registro en 2026.
Uso típico: medianas de 5 mensajes, 4 llamadas y ~19.8 minutos por usuario. La mayoría de los clientes (~74 %) es de Uso medio.
Planes: Básico y Premium se comportan casi igual en edad y uso.
Edad: la distribución es casi uniforme entre 18 y 79 años. Los Adultos de 30 a 59 son la mitad de la base.
Outliers: solo en el extremo superior de mensajes, llamadas y minutos. Los minutos tienen la cola más larga, por eso conviene reportar la mediana.
Recomendaciones: rediseñar Premium, ofrecer upgrade a usuarios de Alto uso en Básico, un programa de retención para Alto uso, un plan económico para Bajo uso, cobro escalonado por minutos extra y mejorar la captura de city y age.
🛠️ Tecnologías

Python 3 · pandas · seaborn · matplotlib · Jupyter Notebook

▶️ Cómo ejecutar el notebook
Clona el repositorio:
bash
   git clone https://github.com/jhon-cardona/Project-ConnectaTel-.git
   cd Project-ConnectaTel-
Instala las dependencias:
bash
   pip install pandas seaborn matplotlib jupyter
Coloca plans.csv, users_latam.csv y usage.csv en una carpeta datasets/, o cambia las rutas /datasets/... del notebook por las tuyas.
Abre el notebook (jupyter notebook) o súbelo a Google Colab y ejecuta las celdas en orden con Run all.
📁 Estructura
Project-ConnectaTel-/
├── S7_Version-Estudiante-Project-ConnectaTel.ipynb   # análisis completo
└── README.md
└── datasets/
    ├── plans.csv
    ├── users_latam.csv
    └── usage.csv
