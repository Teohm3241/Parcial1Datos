# Pipeline de Datos de Gran Volumen - Procesamiento y Calidad (500+ Registros)

Este repositorio contiene la solución completa para la construcción de un pipeline de datos dinámico, automatizado y reproducible desarrollado en **Python** utilizando **Google Colab**. 

El pipeline consume datos brutos desde una API REST pública, realiza transformaciones de limpieza y enriquecimiento, ejecuta validaciones de calidad estricta mediante aserciones programáticas y persiste el dataset procesado en múltiples formatos de almacenamiento (CSV, Parquet y SQLite).

---

## 📸 1. Arquitectura del Pipeline

El siguiente diagrama representa el flujo completo de los datos a través de las etapas del pipeline:

```mermaid
flowchart LR
    A[<b>1. Fuente</b><br>API REST RandomUser] -->|Solicitud HTTP GET| B[<b>2. Extracción</b><br>Python / requests]
    B -->|Respuesta JSON| C[<b>3. Datos Crudos</b><br>pd.json_normalize<br>500 Registros]
    C -->|DataFrame Pandas| D[<b>4. Transformación</b><br>• Renombrado a snake_case<br>• Mayúsculas/Minúsculas<br>• Categorización age_group<br>• Extracción email_domain]
    D -->|Datos Limpios| E[<b>5. Validación</b><br>• Check >= 500 filas<br>• Unicidad de user_id<br>• Formato Regex Email<br>• No Nulos]
    E -->|Aprobado| F[<b>6. Datos Procesados</b><br>Dataset Validado]
    F -->|Persistencia| G[(<b>7. Almacenamiento</b><br>• CSV / Parquet<br>• Base de Datos SQLite)]
    G -->|Consultas SQL / BI| H[<b>8. Consumo</b><br>Analítica / Reportes]
