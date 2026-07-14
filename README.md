# CICDAdventureWorks2026Karina

## Descripción del Proyecto

Este proyecto tiene como objetivo aprender y aplicar conceptos fundamentales de **Databricks** utilizando el conjunto de datos de **Adventure Works**, una empresa ficticia dedicada a la fabricación y comercialización de bicicletas, componentes y accesorios deportivos.

**Arquitectura To BE**

A través de este caso de estudio, se explorarán las capacidades de **Databricks** para la ingesta, transformación, consulta y análisis de datos, siguiendo un enfoque práctico orientado a escenarios reales de negocio.

<img width="1268" height="749" alt="image" src="https://github.com/user-attachments/assets/59ab1f4b-2e7f-4a8e-9c02-acd8a41d0318" />

## Tecnologías Utilizadas

- **Databricks**
- Azure SQL
- Azure Data Factory
- Azure Key Vault
- Databricks


## Objetivos de Aprendizaje

Durante el desarrollo del proyecto se pondrán en práctica conceptos clave de **Databricks**, tales como:

- Creación y administración de notebooks en **Databricks**.
- Procesamiento de datos con Apache Spark en **Databricks**.
- Diseño de modelos de datos para análisis de negocio.
- Creación de métricas e indicadores de ventas.
- Exploración de datos.

## Modelo de Datos

El proyecto se basa en cuatro tablas principales que representan el proceso de ventas de Adventure Works.

### Customer

Contiene la información de los clientes que realizan compras en la compañía.

### Product

Almacena el catálogo de productos disponibles para la venta.

### SalesOrderHeader

Representa la información general de cada pedido realizado por un cliente.

### SalesOrderDetail

Contiene el detalle de los productos incluidos en cada pedido.


## Relaciones del Modelo Operativo

En este diagrama se muestra el modelo entidad relación de adventure works

 <img width="998" height="1155" alt="image" src="https://github.com/user-attachments/assets/8f703dcf-c4f8-4c1c-9e99-4932394caace" />


## Casos de Uso en **Databricks**

A partir de estas tablas se pueden desarrollar diferentes ejercicios para fortalecer habilidades en **Databricks**:

- Carga de datos en formato csv.
- Creación de tablas y vistas en **Databricks SQL**.
- Implementación de procesos ETL utilizando Azure Data Factory.
- Análisis de ventas por producto y cliente.
- Construcción de métricas de negocio.
- Generación de dashboard analíticos.
- Exploración y validación de calidad de datos.
- Modelado de datos para consumo analítico.


## Modelo Entidad Relación  **Databricks: Datos Gold**

Con base en un modelo de datos  OLAP, el diseño analítico  se muestra a continuación
<img width="386" height="644" alt="image" src="https://github.com/user-attachments/assets/94c2f081-ff53-4f04-a49e-64533c1c027f" />



## Proceso
Notebooks: 9 archivos .py que orquestan el pipeline:

- 4 Bronze (Customer, Product, SalesOrderDetail, SalesOrderHeader)
- 1 Silver (validación y transformación de las 4 tablas)
- 1 Gold (star schema con DimCustomer, DimProduct, FactSales)
- 1 Rollback (DROP + UNDROP con auditoría)

## CI/CD — GitHub Actions → Databricks

**Workflows automáticos**:
- deploy-notebook.yml: exporta y despliega notebooks a Databricks workspace
- deploy-job.yml: crea/actualiza el Job MEDALLION_PIPELINE_ADVENTUREWORKS en Databricks

- Cada push a main dispara ambos workflows automáticamente.
- Job en Databricks: multitask con 8 notebooks en orden (Bronze paralelo, luego Silver, luego Gold).

En Producción:
  <img width="903" height="586" alt="image" src="https://github.com/user-attachments/assets/11e7ddf2-f67a-4d1e-8d63-a8ca7b263d08" />



## Governance y Seguridad

**Roles y Control de Acceso**

Implementamos RBAC con tres grupos principales:

GrupoPermisosAccesoData Engineers (advwks_DE)CREATE, ALTER, DELETE, SELECTCatálogo completoData Analysts (advwks_DA)SELECT (lectura)Solo GoldData Governance (advwks_DG)SELECT (lectura)Catálogo completo

 **Gestión de Secretos — Azure Key Vault**
Todos los secretos se almacenan centralizadamente en Azure Key Vault y se accede mediante identidades gestionadas (Managed Identity). 

## Preguntas de Negocio

El modelo permite responder preguntas como:

- ¿Cuáles son las ventas totales?
- ¿Qué productos de acuerdo a su categoría que generan mayores ingresos?
- ¿Cuáles son los productos más vendidos?
- ¿Cómo evolucionan las ventas a lo largo del tiempo?
- ¿Qué tendencias pueden identificarse en el comportamiento de compra?


<img width="674" height="329" alt="image" src="https://github.com/user-attachments/assets/bfb69638-d22a-468e-acac-bed2d4bdbf03" />




## Resultado Esperado

Al finalizar este proyecto, se espera adquirir experiencia práctica en el uso de **Databricks** para la gestión y análisis de datos, utilizando un escenario empresarial realista que permita comprender cómo transformar datos transaccionales en información valiosa para la toma de decisiones.



## Autor Karina Morales
