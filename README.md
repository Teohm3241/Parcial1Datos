
# Pipeline de Datos: Extracción, Transformación, Calidad y Almacenamiento

Este repositorio contiene la implementación de un pipeline ETL (Extracción, Transformación y Carga) desarrollado en **Python** y ejecutado en **Google Colab**, diseñado para procesar un volumen de datos superior a 500 registros respetando estrictos estándares de calidad y arquitectura.

---

## 📋 1. Propósito del Proyecto

Automatizar el flujo de datos desde una fuente externa (API REST), aplicando procesos robustos de limpieza, normalización, validación de calidad y almacenamiento estructurado multiformato (CSV, Parquet y SQLite), minimizando la intervención manual y garantizando la reproducibilidad.

---

## 🔌 2. Fuente de Datos

* **Nombre de la Fuente:** Random User Generator API
* **Endpoint:** `https://randomuser.me/api/?results=500`
* **Formato de Origen:** JSON
* **Volumen:** 500 registros dinámicos con atributos demográficos, geográficos y de contacto.

---

## 🛠️ 3. Tecnologías Utilizadas

* **Python 3.x:** Lenguaje principal de programación.
* **Google Colab:** Entorno de ejecución en la nube.
* **Pandas & NumPy:** Manipulación, transformación y análisis tabular de datos.
* **Requests:** Consumo de solicitudes HTTP hacia la API REST.
* **SQLite3:** Almacenamiento relacional embebido.
* **PyArrow:** Generación de archivos optimizados en formato Parquet.

---

## 🏗️ 4. Arquitectura del Pipeline

El flujo de datos sigue una secuencia lineal estructurada para garantizar trazabilidad y control de calidad en cada etapa:

```mermaid
flowchart LR
    A[<b>1. Fuente API</b><br>RandomUser API] -->|Solicitud HTTP GET| B[<b>2. Extracción</b><br>Python / requests]
    B -->|Respuesta JSON| C[<b>3. Datos Brutos</b><br>Raw DataFrame<br>500 Registros]
    C -->|DataFrame Pandas| D[<b>4. Transformaciones</b><br>• Renombrado a snake_case<br>• Mayúsculas/Minúsculas<br>• Variable age_group<br>• Extracción email_domain]
    D -->|Datos Limpios| E[<b>5. Validaciones</b><br>• Volume Check >= 500<br>• Unicidad user_id<br>• Regex Formato Email<br>• Control de Nulos]
    E -->|Aprobado| F[<b>6. Almacenamiento</b><br>• CSV<br>• Parquet<br>• Base de Datos SQLite]
    F -->|Consultas / Reportes| G[<b>7. Consumo / Análisis</b><br>BI & SQL Analytics]
