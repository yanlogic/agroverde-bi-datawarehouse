# AgroVerde · Data Warehouse y dashboard de Inteligencia de Negocios

Proyecto del curso **Soluciones de Inteligencia de Negocios** (Universidad Privada del Norte, 2026-2). Resuelve el caso de una empresa agroindustrial ficticia, **AgroVerde S.A.C.**: se limpian tres fuentes de datos con Python, se cargan a un data warehouse en SQL Server y se presentan en un dashboard de Power BI.

## Cómo funciona

```
Excel (3 fuentes) → Python (limpieza y transformación) → SQL Server (data warehouse) → Power BI (dashboard)
```

1. **Fuentes:** tres archivos de Excel con datos simulados de producción de campo, ventas y pedidos, y logística y despachos.
2. **Python:** un notebook lee las fuentes y las guarda en tablas de paso (`stg_produccion`, `stg_ventas`, `stg_despachos`). Luego las limpia y transforma.
3. **SQL Server:** el notebook carga las tablas de dimensiones y de hechos del data warehouse `DW_AgroVerde`.
4. **Power BI:** el dashboard muestra los datos del data warehouse.

## Qué limpia y transforma el notebook

- Normaliza nombres de países y de cultivos (por ejemplo, variantes como "Holanda" y "Países Bajos").
- Convierte fechas que vienen en varios formatos.
- Convierte textos a números (quita separadores de miles y símbolos).
- Elimina duplicados por lote.
- Valida campos obligatorios y descarta registros con valores no válidos.
- Estandariza el número de pedido (por ejemplo, `PED-000123`).
- Agrega categorías derivadas, como la categoría del cultivo y el continente del mercado.

## Modelo del data warehouse

- **Dimensiones:** `Dim_Tiempo`, `Dim_Producto`, `Dim_Cliente`, `Dim_Mercado`.
- **Hechos:** `Fact_Produccion`, `Fact_Pedido`, `Fact_Despacho`.

## Estructura del repositorio

```
├── fuentes/     # 3 archivos .xlsx con datos simulados
├── notebook/    # transformacion_datos.ipynb (limpieza y carga con Python)
├── sql/         # scripts para crear el data warehouse (ejecutar en orden)
├── powerbi/     # AgroVerdeEF.pbix (dashboard)
└── docs/        # AgroVerdeEF_dashboard.pdf (exportación del dashboard)
```

## Cómo reproducirlo

1. Instala **SQL Server Express** y el **ODBC Driver 18 for SQL Server**. SQL Server Management Studio es opcional.
2. Ejecuta los scripts de la carpeta `sql/` en orden numérico para crear la base de datos y sus tablas.
3. Instala las librerías de Python:
   ```
   pip install pandas numpy sqlalchemy pyodbc openpyxl jupyter
   ```
4. Abre `notebook/transformacion_datos.ipynb` y, si tu servidor tiene otro nombre, cambia la variable `SERVIDOR` (por defecto es `localhost\SQLEXPRESS`). Ejecuta todas las celdas.
5. Abre `powerbi/AgroVerdeEF.pbix` con Power BI Desktop. Si pide la conexión, apúntala a tu servidor y a la base `DW_AgroVerde`.

## Herramientas

Python (pandas, NumPy, SQLAlchemy, pyodbc) · SQL Server (T-SQL) · Power BI · Jupyter Notebook

## Autoría

- **Yanela Acori:** scripts SQL, notebook de Python (ETL) y dashboard de Power BI.
- **Mónica Candiotti:** apoyo en la redacción del informe técnico del curso, que no se incluye en este repositorio.

Los datos son simulados y no corresponden a una empresa real.
