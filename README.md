📱 Análisis de clientes de ConnectaTel

Open In Colab

Análisis de datos de una empresa de telecomunicaciones de Latinoamérica para entender cómo usan el servicio sus clientes y proponer mejoras a sus planes.

🎯 Objetivo
Limpiar los datos y corregir errores.
Resumir el uso de cada cliente (mensajes, llamadas y minutos).
Agrupar a los clientes por edad y por nivel de uso.
Detectar usos extremos (outliers).
Dar recomendaciones al negocio.
🗂️ Datos

Son tres archivos CSV. El notebook los lee desde la carpeta /datasets/.

Archivo	Qué contiene
plans.csv	Los 2 planes: Básico ($12/mes) y Premium ($25/mes), con minutos, mensajes y GB incluidos.
users_latam.csv	4 000 clientes: edad, ciudad, fecha de registro, plan y fecha de cancelación.
usage.csv	40 000 registros de uso: llamadas (call) y mensajes (text). Cubre desde el 1 de enero hasta el 30 de junio de 2024.
🔬 Qué se hizo
Cargar y explorar los tres archivos.
Buscar problemas de calidad: valores nulos, valores falsos que hacen de "dato desconocido" y fechas imposibles.
Limpiar los datos:
Edad -999 (55 filas): se reemplazó por la mediana.
Ciudad "?" (96 filas): se convirtió en dato vacío.
Fechas de registro fuera del periodo de los datos: se marcaron como vacías.
Los vacíos en duration y length se dejaron así a propósito: un mensaje no tiene duración y una llamada no tiene longitud.
Resumir el uso por cliente: cantidad de mensajes, de llamadas y total de minutos.
Graficar la distribución de cada variable según el plan.
Detectar outliers con diagramas de caja y el método IQR. Se mantuvieron porque son clientes muy activos, no errores.
Segmentar clientes:
Por uso: Bajo uso, Uso medio y Alto uso.
Por edad: Joven (menos de 30), Adulto (30 a 59) y Adulto Mayor (60 o más).
Redactar el análisis ejecutivo con hallazgos y recomendaciones.
📊 Resultados principales
Grupo	Clientes	%
Uso medio	2 943	73.6 %
Bajo uso	778	19.4 %
Alto uso	279	7.0 %
Adulto	2 018	50.4 %
Adulto Mayor	1 222	30.6 %
Joven	760	19.0 %
Básico y Premium se usan casi igual: el plan no refleja cuánto consume cada cliente.
El grupo Alto uso es el que más cancela (14.0 %, frente a cerca de 11.5 % en los otros dos), aunque es un grupo pequeño.
Recomendaciones: mejorar el plan Premium, ofrecer un cambio de plan a los clientes de Alto uso en Básico, crear un plan económico para Bajo uso y cobrar por tramos los minutos extra.

El detalle completo está al final del notebook.

▶️ Cómo ejecutarlo
En Google Colab (lo más fácil)
Haz clic en el botón Open In Colab de arriba.
Sube los tres archivos CSV desde el panel de archivos de la izquierda.
Cambia las rutas de la celda de carga (por ejemplo '/datasets/users_latam.csv' por 'users_latam.csv').
Ve a Entorno de ejecución > Ejecutar todo.
En tu computadora
bash
pip install pandas seaborn matplotlib jupyter
jupyter notebook

Abre el notebook y ejecuta las celdas de arriba hacia abajo.

✅ Para comprobar que todo salió bien
users['age'].min() da 18 (ya no -999).
users['city'].isna().sum() da 565.
user_profile['grupo_uso'].value_counts() da 2 943, 778 y 279.
user_profile['grupo_edad'].value_counts() da 2 018, 1 222 y 760.
⚠️ Limitaciones
Los datos de uso cubren solo el primer semestre de 2024.
Un cliente sin registros de uso quedó clasificado como Alto uso. Se arregla con fillna(0) en las tres métricas antes de clasificar. Afecta a 1 de 4 000 clientes.
No hay datos de ingresos, así que el valor de cada grupo se estima por su consumo.
No se cruzó la edad con el nivel de uso.
📁 Estructura sugerida
.
├── README.md
├── notebooks/
│   └── connectatel_analisis.ipynb
└── datasets/
    ├── plans.csv
    ├── users_latam.csv
    └── usage.csv
