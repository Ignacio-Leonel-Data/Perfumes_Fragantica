📊 Medidas DAX – Tablero Power BI Fragantica Perfumes (1900 - 2026)
Este documento reúne las principales medidas DAX utilizadas en el dashboard desarrollado en Power BI, organizadas según la estructura del proyecto.

# 📁 Panorama General
⭐ Calificación promedio
Calificación Promedio =
AVERAGE('perfumes_limpio'[rating_avg])

Descripción

Calcula la calificación promedio otorgada por los usuarios a todos los perfumes del catálogo.

❤️ Interés Total
Interes Total =
SUM('perfumes_limpio'[want])

Descripción

Calcula el interés total de compra sumando la cantidad de usuarios que marcaron cada perfume como "Want".

🗳️ Media de votos por perfume
Media_Votos_Perfume =
DIVIDE(
    SUM('perfumes_limpio'[vote_count]),
    COUNT('perfumes_limpio'[id]),
    0
)

Descripción

Obtiene el promedio de votos recibidos por perfume.

Se utilizó para comparar la media con la mediana durante el análisis estadístico.

📈 Mediana de votos
Mediana_Votos_Perfume =
MEDIAN('perfumes_limpio'[vote_count])

Descripción

Calcula la mediana de votos recibidos por perfume.

Este indicador permitió comprobar que la distribución de votos es asimétrica debido a la presencia de valores atípicos.

📅 Año Máximo
Año Máximo =
MAX('perfumes_limpio'[year])

Descripción

Se utilizó para verificar el año máximo presente dentro del dataset durante el proceso de validación del gráfico temporal.

🐍 Limpieza de datos en Python

Antes de importar la información a Power BI se realizó una limpieza del dataset utilizando Python.

Las principales transformaciones fueron:

Selección únicamente de las columnas necesarias para el proyecto.
Verificación de registros duplicados.
Identificación de valores nulos.
Eliminación de espacios en blanco innecesarios.
Reemplazo de valores faltantes en las columnas accords y perfumers por el valor "Desconocido".
Conversión de tipos de datos.
Exportación de un nuevo dataset limpio para Power BI.
🧹 Scripts aplicados
Importación de librerías
import pandas as pd
Lectura del archivo
df = pd.read_csv("perfumes.csv")
Selección de columnas
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
Información general del dataset
df.info()
Registros duplicados
df.duplicated().sum()
Valores nulos
df.isnull().sum()
Eliminación de espacios
columnas_texto = [
    "name",
    "brand",
    "gender",
    "accords",
    "perfumers"
]

for col in columnas_texto:
    df[col] = df[col].str.strip()
Reemplazo de valores faltantes
df["accords"] = df["accords"].fillna("Desconocido")
df["perfumers"] = df["perfumers"].fillna("Desconocido")
Exportación del dataset limpio
df.to_csv(
    "perfumes_limpio.csv",
    index=False,
    encoding="utf-8-sig"
)
📊 Análisis estadístico en Python

Para la segunda etapa del proyecto se utilizó Python para visualizar la distribución de los votos mediante un Box Plot, con el objetivo de identificar valores atípicos (Outliers).

import pandas as pd
import matplotlib.pyplot as plt

df = pd.read_csv("perfumes_limpio.csv")

plt.figure(figsize=(12,2))
plt.boxplot(df["vote_count"], vert=False)

plt.title("Distribución de votos por perfume")
plt.xlabel("Cantidad de votos")

plt.show()

Este gráfico permitió observar una distribución fuertemente asimétrica, donde un reducido grupo de perfumes concentra una cantidad muy elevada de votos respecto al resto del catálogo.

🛠 Herramientas utilizadas
Python
Pandas
Power BI
DAX
Power Query
Visual Studio Code
GitHub
