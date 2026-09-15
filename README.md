# Data Processing Pipeline: Global Countries & Regions Dataset

Este repositorio contiene la estructura de datos, scripts de procesamiento y consultas SQL para el análisis demográfico y geográfico del conjunto de datos de países (`paises`).

## 📁 Estructura del Proyecto

```text
.
├── paises_database.db     # Base de datos SQLite principal
├── paises_procesados.csv  # Archivo CSV exportado y estructurado
└── README.md              # Documentación del proyecto
```

---

## 📊 Esquema de la Base de Datos (`paises`)

La tabla `paises` contiene la siguiente estructura de columnas:

| Columna | Tipo de Dato | Descripción |
| :--- | :--- | :--- |
| `country_name` | `TEXT` | Nombre del país |
| `region` | `TEXT` | Continente o región principal (ej. *Europe*, *Americas*, *Asia*, *Africa*, *Oceania*) |
| `subregion` | `TEXT` | Subregión geográfica específica (ej. *Western Europe*, *North America*) |
| `capital_city` | `TEXT` | Ciudad capital |
| `population` | `INTEGER` | Población total |
| `area` | `INTEGER` | Superficie territorial en km² |
| `population_density` | `REAL` | Densidad de población (habitantes por km²) |

---

## ⚡ Consultas SQL de Ejemplo

### 1. Obtener la población total y densidad promedio por región
```sql
SELECT 
    region, 
    SUM(population) AS poblacion_total,
    ROUND(AVG(population_density), 2) AS densidad_promedio
FROM paises
GROUP BY region
ORDER BY poblacion_total DESC;
```

### 2. Obtener los 10 países con mayor superficie territorial
```sql
SELECT country_name, capital_city, region, area
FROM paises
ORDER BY area DESC
LIMIT 10;
```

---

## 🚀 Uso e Integración en Python

Para cargar y consultar los datos en Python utilizando `sqlite3` y `pandas`:

```python
import sqlite3
import pandas as pd

# Conectar a la base de datos SQLite
conn = sqlite3.connect('paises_database.db')

# Cargar los datos en un DataFrame de pandas
df = pd.read_sql_query("SELECT * FROM paises", conn)

# Exportar o guardar a CSV si es necesario
df.to_csv("paises_procesados.csv", index=False)

print(df.head())
```

---

## 📝 Licencia

Este proyecto está bajo la licencia [MIT](LICENSE).
