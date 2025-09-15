# prueba-senior-bi-jeffer
Prueba senior Jeffer Arias - Global Cruices

- Este proyecto corresponde a la prueba técnica para la posición Senior BI Analyst.
El objetivo es demostrar el ciclo completo de un proyecto de Business Intelligence:

1. Extracción y transformación de datos (ETL) con Python.

2. Carga y modelado en Power BI.

3. Uso de GitHub para control de versiones.

4. Documentación de procesos y consideraciones en la nube.

Programas utilizados

Python 3.13

Visual studio code

Librerías: pyodbc, pandas, os, re

SQL Server (ODBC Driver 18) para conexión a la base de datos.

Power BI Desktop para modelado y visualización.

Git + GitHub para versionamiento.

Visual Studio Code con soporte de Jupyter Notebooks


Descripcion a detalle: 

1. Lo primero trabajo fue la conexion a la base de datos: 

import pyodbc
import pandas as pd

conn = pyodbc.connect(
    "DRIVER={ODBC Driver 17 for SQL Server};"
    "SERVER=te3-training-eu.database.windows.net;"
    "DATABASE=SpacePartsCoDW;"
    "UID=dwreader;"
    "PWD=TE3#reader!"
)

2. Extracción

Tablas pequeñas (dim.Customers, dim.Products, dim.Employees, etc.) se exportaron completas.

Tablas grandes (fact.Invoices, fact.Orders) se filtraron por Billing Date 2020–2022 para optimizar rendimiento, así mismo se trasnformo las fechas debido a que estaban en nanosegundos

3. Transformación

Conversión de fechas (Billing Date) desde formato numérico (epoch * 100ns) a datetime.
Group by en la tabla invoices por el motivo que esta teniamo muchos datos, así mismo llevarlo al nivel de la tabla Budget con el fon de comparar los mismos rangos de fechas establecidos del año 2020 al 2022

Limpieza de valores numéricos (ventas, costos, penalizaciones).

4. Carga

Exportación de tablas a CSV:

exported_tables/ → datos crudos.

5. Modelado en Power bi

Algunas tablas no se les realizo el proceso de transofrmación desde el scrip de python, se realizaorn directamente en power bi. 

- Se construyó un modelo estrella con:

-Fact table: Invoices (ventas), Orders, Budget, Forecast.

-Dimensiones: Customers, Products, Regions, Employees, etc.

## Medidas principales en DAX:

Ventas Totales = SUM(fact_Invoices[Net Invoice Value])

Costos Totales = SUM(fact_Invoices[Net Invoice Cost])


Margen bruto = [Ventas Totales] - [Costos Totales]

6. Dashboards:

Evolución de ventas por año/mes (2020–2022).

Top clientes y top productos por ventas.

Análisis de márgenes brutos por clientes

Comparativo de facturación vs pedidos(Ventas, cantidades)

Tiempo promedio de facturación, entregas.

