# **Procesamiento de Datos desde APIs usando Apache Spark en Databricks**

Este proyecto está diseñado para **procesar datos desde APIs públicas** utilizando **Apache Spark** en el entorno de **Databricks**, permitiendo la carga, transformación y visualización de datos provenientes de APIs abiertas de Colombia.

---

## ✅ **Objetivo del Proyecto**

El objetivo de este programa es:

1. **Conectarse a dos APIs públicas** de datos abiertos en Colombia (SECOP y MEN).
2. **Descargar archivos CSV** directamente desde las URLs proporcionadas por las APIs.
3. **Cargar los datos en DataFrames** de Apache Spark para su posterior análisis y manipulación.
4. **Realizar transformaciones y limpieza de los datos** para asegurar su calidad y precisión.
5. **Visualizar los datos** usando herramientas integradas de Databricks.
6. **Preparar los datos para análisis futuros**, permitiendo su almacenamiento y exportación a otros formatos como Parquet o CSV.

---

## 🔗 **APIs Utilizadas**

### **1. SECOP (Sistema Electrónico para la Contratación Pública)**

- **Descripción**: El SECOP es una plataforma del gobierno colombiano que centraliza los procesos de contratación pública, garantizando la transparencia y eficiencia de los contratos.
- **URL CSV**: [https://www.datos.gov.co/resource/rpmr-utcd.csv](https://www.datos.gov.co/resource/rpmr-utcd.csv)
- **Datos disponibles**: Información sobre contratos, proveedores, y entidades públicas.

### **2. MEN (Ministerio de Educación Nacional)**

- **Descripción**: API del Ministerio de Educación Nacional de Colombia con datos sobre la cobertura educativa, tasas de matrícula y estadísticas relacionadas al sistema educativo.
- **URL CSV**: [https://www.datos.gov.co/resource/nudc-7mev.csv](https://www.datos.gov.co/resource/nudc-7mev.csv)
- **Datos disponibles**: Información sobre población estudiantil, cobertura y tasas de matrícula por departamento y municipio.

---

## ✅ **Consideraciones Importantes**

- **Tamaño de los Archivos**: Los archivos CSV pueden ser grandes, por lo que se recomienda verificar la capacidad del cluster en Databricks antes de cargarlos.
- **Accesibilidad de las APIs**: Las URLs de las APIs deben estar accesibles públicamente. Si se requiere autenticación o tokens API, será necesario adaptarlo.
- **Adaptabilidad**: El proceso está configurado para trabajar con archivos CSV, pero puede adaptarse a otros formatos como JSON o Parquet, según el caso de uso.
- **Validación de Datos**: Es importante validar los esquemas de los datos para asegurarse de que las lecturas y transformaciones se realicen correctamente.
- **Calidad de los Datos**: Asegurarse de que los datos no contengan valores nulos o inconsistencias que puedan afectar los análisis posteriores.

---

## 🛠 **Pasos del Proyecto**

### 1. **Configuración del Cluster en Databricks**
   - Asegúrate de tener un cluster adecuado en Databricks con suficiente memoria y recursos para procesar grandes volúmenes de datos. Si los archivos CSV son grandes, considera aumentar la memoria del cluster.

### 2. **Descarga de los Archivos desde las APIs**
   - Utiliza Python o herramientas integradas en Databricks para realizar solicitudes HTTP a las APIs y descargar los archivos CSV. A continuación, se muestra un ejemplo básico para la descarga de archivos:
   
   ```python
   import requests

   url_secop = "https://www.datos.gov.co/resource/rpmr-utcd.csv"
   url_men = "https://www.datos.gov.co/resource/nudc-7mev.csv"

   # Descargar el archivo de SECOP
   response_secop = requests.get(url_secop)
   if response_secop.status_code == 200:
       with open("/dbfs/tmp/SECOP.csv", "wb") as f:
           f.write(response_secop.content)

   # Descargar el archivo del MEN
   response_men = requests.get(url_men)
   if response_men.status_code == 200:
       with open("/dbfs/tmp/MEN.csv", "wb") as f:
           f.write(response_men.content)
