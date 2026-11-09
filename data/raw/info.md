# Carpeta `data/raw/`

Esta carpeta está destinada a almacenar el dataset original sin filtrar (el cual contiene datos de múltiples países). Sin embargo, **no encontrarás el archivo `.csv` en el repositorio por defecto**.

## ¿Por qué no está el dataset original aquí?

El archivo original de *Our World in Data* es extremadamente pesado. Subir archivos de este tamaño a un repositorio de GitHub no es una buena práctica, ya que ralentiza la clonación del proyecto y puede exceder los límites de almacenamiento de la plataforma. 

Para mantener el repositorio ligero y optimizado, el archivo se descarga de forma dinámica durante la ejecución.

## Flujo de trabajo de los datos

El proceso para obtener y preparar los datos se divide en dos pasos automatizados:

1. **Descarga (`descargar_datos.py`)**: Este script se conecta a los servidores de *Our World in Data* y descarga automáticamente el dataset original, guardándolo directamente en esta carpeta (`data/raw/covid_owid.csv`).
2. **Filtrado (`analisis_datos.py`)**: Este script lee el archivo descargado, realiza la limpieza de datos y filtra la información para quedarse únicamente con los registros de Colombia. El resultado se guarda en la carpeta de datos procesados (`data/processed/covid_limpio.csv`), que es el archivo que finalmente utiliza el modelo.

> **Nota:** El archivo descargado en esta carpeta está excluido del control de versiones mediante el archivo `.gitignore`.

## ¿Cómo simular otro país?

Por defecto, el proyecto está configurado para Colombia. Si deseas realizar la simulación con otro país, sigue estos pasos:

1. Abre el archivo `src/analisis_datos.py`.
2. Ubica la función principal o la variable de configuración del país.
3. Modifica el parámetro `pais` por el nombre exacto del país que deseas analizar (debe coincidir con el nombre en el dataset de OWID). Por ejemplo: `pais="Mexico"` o `pais="Argentina"`.
4. Vuelve a ejecutar el script de análisis y los scripts posteriores (calibración, validación, escenarios) para obtener los nuevos resultados.
