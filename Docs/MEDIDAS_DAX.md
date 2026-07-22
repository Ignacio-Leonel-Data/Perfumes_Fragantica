📊 Medidas DAX – Dashboard Power BI | Análisis de Perfumes

Este documento reúne las principales medidas DAX utilizadas durante el desarrollo del dashboard en Power BI, organizadas según la funcionalidad de cada indicador dentro del proyecto.

📁 KPIs Principales
🔹 Calificación Promedio
Calificación Promedio =
AVERAGE('perfumes_limpio'[rating_avg])
🔹 Interés Total
Interes Total =
SUM('perfumes_limpio'[want])
🔹 Media de Votos por Perfume
Media_Votos_Perfume =
DIVIDE(
    SUM('perfumes_limpio'[vote_count]),
    COUNT('perfumes_limpio'[id]),
    0
)
🔹 Mediana de Votos por Perfume
Mediana_Votos_Perfume =
MEDIAN('perfumes_limpio'[vote_count])
🔹 Año Máximo
Año Máximo =
MAX('perfumes_limpio'[year])
📁 Análisis Estadístico
🔹 Comparación Media vs Mediana

Las medidas Media_Votos_Perfume y Mediana_Votos_Perfume fueron utilizadas para analizar la distribución de la variable vote_count.

Su comparación permitió comprobar que la distribución de votos presenta una fuerte asimetría positiva debido a la existencia de perfumes con una cantidad de votos considerablemente superior al resto del catálogo.

📁 Visualización Temporal
🔹 Evolución del Catálogo

La medida Año Máximo fue utilizada durante la validación del gráfico temporal para verificar los límites del eje cronológico y asegurar una representación correcta de la evolución histórica del catálogo.

🐍 Scripts de Python – Limpieza y Preparación de Datos

Durante la etapa de preparación de datos se utilizó Python para limpiar y transformar el conjunto de datos antes de su importación a Power BI.

📁 Importación de Librerías
🔹 Librería Principal
import pandas as pd
📁 Carga del Dataset
🔹 Lectura del archivo CSV
df = pd.read_csv("perfumes.csv")
📁 Selección de Variables
🔹 Columnas utilizadas
columnas = [
    "id",
    "name",
    "brand",
    "year",
    "gender",
    "rating_avg",
    "vote_count",
    "longevity_avg",
    "sillage_avg",
    "price_value_avg",
    "have",
    "want",
    "winter",
    "spring",
    "summer",
    "autumn",
    "magnitude",
    "accords",
    "perfumers"
]

df = df[columnas]
📁 Exploración Inicial
🔹 Información General
df.info()
🔹 Búsqueda de Registros Duplicados
df.duplicated().sum()
🔹 Identificación de Valores Nulos
df.isnull().sum()
📁 Limpieza de Datos
🔹 Eliminación de Espacios en Blanco
columnas_texto = [
    "name",
    "brand",
    "gender",
    "accords",
    "perfumers"
]

for col in columnas_texto:
    df[col] = df[col].str.strip()
🔹 Reemplazo de Valores Faltantes
df["accords"] = df["accords"].fillna("Desconocido")
df["perfumers"] = df["perfumers"].fillna("Desconocido")
📁 Exportación
🔹 Generación del Dataset Limpio
df.to_csv(
    "perfumes_limpio.csv",
    index=False,
    encoding="utf-8-sig"
)
📁 Análisis Estadístico
🔹 Box Plot - Distribución de Votos
import pandas as pd
import matplotlib.pyplot as plt

df = pd.read_csv("perfumes_limpio.csv")

plt.figure(figsize=(12,2))

plt.boxplot(
    df["vote_count"],
    vert=False
)

plt.title("Distribución de votos por perfume")
plt.xlabel("Cantidad de votos")

plt.show()
📁 Interpretación Estadística
🔹 Valores Atípicos (Outliers)

El Box Plot permitió identificar una distribución fuertemente asimétrica de la variable vote_count.

La mayor parte de los perfumes concentra una baja cantidad de votos, mientras que un reducido grupo presenta valores excepcionalmente altos, considerados outliers. Estos registros corresponden a fragancias con una elevada popularidad dentro de la comunidad de usuarios y constituyen información relevante para el análisis de negocio.

📁 Decisiones de Modelado
🔹 Filtrado de Años

Durante la construcción del dashboard se detectaron registros con años inconsistentes (por ejemplo 20 y 2027) que afectaban la visualización del gráfico temporal.

Para garantizar una representación cronológica correcta, se filtró el análisis considerando únicamente los registros comprendidos entre 1900 y 2026, sin modificar el resto del conjunto de datos.

🛠 Tecnologías Utilizadas
Python
Pandas
Power BI
DAX
Power Query
Visual Studio Code
GitHub
