# 📊 Medidas DAX – Dashboard Power BI | Análisis de Perfumes

Este documento reúne las principales medidas DAX utilizadas en el dashboard desarrollado en **Power BI**, organizadas según la estructura del proyecto.

---

# 📁 KPIs

## 🔹 Calificación Promedio

```DAX
Calificación Promedio =
AVERAGE('perfumes_limpio'[rating_avg])
```

---

## 🔹 Interés Total

```DAX
Interes Total =
SUM('perfumes_limpio'[want])
```

---

## 🔹 Media de Votos por Perfume

```DAX
Media_Votos_Perfume =
DIVIDE(
    SUM('perfumes_limpio'[vote_count]),
    COUNT('perfumes_limpio'[id]),
    0
)
```

---

## 🔹 Mediana de Votos por Perfume

```DAX
Mediana_Votos_Perfume =
MEDIAN('perfumes_limpio'[vote_count])
```

---

## 🔹 Año Máximo

```DAX
Año Máximo =
MAX('perfumes_limpio'[year])
```

---

# 📁 Validación

## 🔹 Año Máximo

```DAX
Año Máximo =
MAX('perfumes_limpio'[year])
```

# 🐍 Scripts de Python – Limpieza y Preparación de Datos

Este documento reúne los principales scripts utilizados durante el proceso de limpieza y preparación del dataset antes de su carga en **Power BI**.

---

# 📁 Importación

## 🔹 Librería Pandas

```python
import pandas as pd
```

---

# 📁 Carga del Dataset

## 🔹 Lectura del archivo CSV

```python
df = pd.read_csv("perfumes.csv")
```

---

# 📁 Selección de Variables

## 🔹 Columnas utilizadas

```python
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
```

---

# 📁 Exploración de Datos

## 🔹 Información General

```python
df.info()
```

---

## 🔹 Registros Duplicados

```python
df.duplicated().sum()
```

---

## 🔹 Valores Nulos

```python
df.isnull().sum()
```

---

# 📁 Limpieza

## 🔹 Eliminación de Espacios

```python
columnas_texto = [
    "name",
    "brand",
    "gender",
    "accords",
    "perfumers"
]

for col in columnas_texto:
    df[col] = df[col].str.strip()
```

---

## 🔹 Reemplazo de Valores Faltantes

```python
df["accords"] = df["accords"].fillna("Desconocido")
df["perfumers"] = df["perfumers"].fillna("Desconocido")
```

---

# 📁 Exportación

## 🔹 Dataset Limpio

```python
df.to_csv(
    "perfumes_limpio.csv",
    index=False,
    encoding="utf-8-sig"
)
```

---

# 📁 Análisis Estadístico

## 🔹 Box Plot

```python
import pandas as pd
import matplotlib.pyplot as plt

df = pd.read_csv("perfumes_limpio.csv")

plt.figure(figsize=(12,2))
plt.boxplot(df["vote_count"], vert=False)

plt.title("Distribución de votos por perfume")
plt.xlabel("Cantidad de votos")

plt.show()
```
