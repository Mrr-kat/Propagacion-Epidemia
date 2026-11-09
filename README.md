# Simulación Basada en Agentes de la Propagación de COVID-19 en Colombia

Modelo SEIR con red de contactos, calibrado con datos reales de Our World in Data.
SEIR model with a contact network, calibrated with real data from Our World in Data.

**Curso / Course:** Modelado y Simulación / Modeling and Simulation
**Tecnologías / Technologies:** Python, Mesa, NetworkX, Pandas, Matplotlib, Seaborn

[Español](#español) | [English](#english)

---

## Español

### Contenido

- [Descripción general](#descripción-general)
- [Características del modelo](#características-del-modelo)
- [Estructura del proyecto](#estructura-del-proyecto)
- [Resultados principales](#resultados-principales)
- [Validación](#validación)
- [Requisitos e instalación](#requisitos-e-instalación)
- [Ejecución](#ejecución)
- [Referencias](#referencias)

### Descripción general

Este proyecto es una simulación basada en agentes (ABM, por sus siglas en inglés) que reproduce la propagación del COVID-19 durante la primera ola en Colombia (2020-2021). Cada persona de la población simulada es un agente que interactúa con sus contactos a través de una red social, y la epidemia surge de esas interacciones individuales.

El modelo se calibra con datos reales de Our World in Data y se usa para evaluar el impacto de tres escenarios de intervención: vacunación, cuarentena y una combinación de ambas.

### Características del modelo

| Característica          | Detalle                                                                                  |
|-------------------------|------------------------------------------------------------------------------------------|
| Tipo de modelo          | SEIR (Susceptible, Expuesto, Infeccioso, Recuperado), extendido con un estado Vacunado (V) |
| Red de contactos        | Topología small-world (Watts-Strogatz)                                                   |
| Agentes                 | 1,000 personas simuladas                                                                 |
| Framework               | Mesa                                                                                     |
| Fuente de datos         | Our World in Data                                                                        |

**Parámetros calibrados**

| Parámetro                       | Valor                                              |
|---------------------------------|----------------------------------------------------|
| Tasa de transmisión (β)         | 0.045                                              |
| Periodo de incubación           | 3 días                                             |
| Periodo infeccioso              | 7 días                                             |
| Número reproductivo básico (R₀) | aproximadamente 2.8, consistente con las estimaciones reales |

### Estructura del proyecto

```text
proyecto_epidemia/
├── data/
│   ├── raw/                     # Dataset original de OWID
│   └── processed/               # Datos filtrados (covid_limpio.csv)
├── src/
│   ├── descargar_datos.py       # Descarga el dataset
│   ├── explorar.py              # Exploración inicial
│   ├── analisis_datos.py        # Estadísticas y gráficos
│   ├── modelo_epidemia.py       # Modelo ABM (Mesa)
│   ├── calibracion.py           # Ajuste de beta
│   ├── validacion.py            # Validación contra datos reales
│   ├── escenarios.py            # Ejecución de escenarios y caso base
│   ├── emergente.py             # Análisis de comportamiento emergente
│   └── generar_diapositivas.py  # Genera el archivo de presentación
├── results/
│   ├── figuras/                 # Gráficos exportados
│   └── tablas/                  # Tablas CSV y reportes
├── presentacion/                # Entregable final (.pptx)
└── requirements.txt             # Dependencias del proyecto
```

### Resultados principales

Se ejecutaron 10 simulaciones por escenario, con 1,000 agentes y un máximo de 200 días.

| Escenario                          | Pico de infectados | Reducción vs. base |
|------------------------------------|-------------------:|-------------------:|
| Base (situación actual)            |                462 |                  - |
| Escenario 1: vacunación al 30%     |                142 |              69.3% |
| Escenario 2: cuarentena al 1%      |                 54 |              88.3% |
| Escenario 3: vacunación y cuarentena |               14 |              96.9% |

La combinación de vacunación y cuarentena produce la mayor reducción del pico epidémico, superior a la de cada intervención por separado.

### Validación

El modelo se validó comparando la curva simulada con la curva real de casos suavizada de Colombia. Aunque no captura todos los picos de la realidad, porque no modela cambios en las políticas públicas, sí reproduce la dinámica cualitativa general de la epidemia.

| Métrica     | Valor |
|-------------|------:|
| MSE         | 0.115 |
| MAE         | 0.231 |
| Correlación | 0.41  |

### Requisitos e instalación

Se recomienda usar un entorno virtual para instalar las dependencias.

```bash
# Clonar el repositorio
git clone <url-del-repositorio>
cd proyecto_epidemia

# Crear y activar el entorno virtual (opcional pero recomendado)
python -m venv venv
venv\Scripts\activate           # En Linux/macOS: source venv/bin/activate

# Instalar dependencias
pip install -r requirements.txt
```

### Ejecución

Para reproducir los resultados del proyecto, ejecuta los scripts en el siguiente orden:

```bash
# 1. Descargar el dataset
python src/descargar_datos.py

# 2. Análisis exploratorio
python src/analisis_datos.py

# 3. Calibrar beta (búsqueda en grilla)
python -m src.calibracion

# 4. Validar el modelo
python -m src.validacion

# 5. Ejecutar los escenarios
python -m src.escenarios

# 6. Analizar el comportamiento emergente
python -m src.emergente

# 7. Generar las diapositivas (opcional)
python -m src.generar_diapositivas
```

Los gráficos se guardan en `results/figuras/` y las tablas en `results/tablas/`.

### Referencias

- [Our World in Data: COVID-19](https://ourworldindata.org/covid-deaths)
- [Mesa: Agent-based modeling framework](https://mesa.readthedocs.io/)
- [NetworkX: Network analysis in Python](https://networkx.org/)

---

## English

### Contents

- [Overview](#overview)
- [Model features](#model-features)
- [Project structure](#project-structure)
- [Main results](#main-results)
- [Validation](#validation-1)
- [Requirements and installation](#requirements-and-installation)
- [Execution](#execution)
- [References](#references)

### Overview

This project is an agent-based model (ABM) that simulates the spread of COVID-19 during the first wave in Colombia (2020-2021). Each person in the simulated population is an agent that interacts with their contacts through a social network, and the epidemic emerges from those individual interactions.

The model is calibrated with real data from Our World in Data and is used to evaluate the impact of three intervention scenarios: vaccination, quarantine, and a combination of both.

### Model features

| Feature         | Detail                                                                                     |
|-----------------|--------------------------------------------------------------------------------------------|
| Model type      | SEIR (Susceptible, Exposed, Infectious, Recovered), extended with a Vaccinated (V) state   |
| Contact network | Small-world topology (Watts-Strogatz)                                                      |
| Agents          | 1,000 simulated individuals                                                                |
| Framework       | Mesa                                                                                       |
| Data source     | Our World in Data                                                                          |

**Calibrated parameters**

| Parameter                       | Value                                              |
|---------------------------------|----------------------------------------------------|
| Transmission rate (β)           | 0.045                                              |
| Incubation period               | 3 days                                             |
| Infectious period               | 7 days                                             |
| Basic reproduction number (R₀)  | approximately 2.8, consistent with real-world estimates |

### Project structure

```text
proyecto_epidemia/
├── data/
│   ├── raw/                     # Original OWID dataset
│   └── processed/               # Filtered data (covid_limpio.csv)
├── src/
│   ├── descargar_datos.py       # Dataset downloader
│   ├── explorar.py              # Initial exploration
│   ├── analisis_datos.py        # Statistics and plots
│   ├── modelo_epidemia.py       # ABM model (Mesa)
│   ├── calibracion.py           # Beta calibration
│   ├── validacion.py            # Validation against real data
│   ├── escenarios.py            # Base case and scenario execution
│   ├── emergente.py             # Emergent behavior analysis
│   └── generar_diapositivas.py  # Presentation generator
├── results/
│   ├── figuras/                 # Exported plots
│   └── tablas/                  # CSV tables and reports
├── presentacion/                # Final deliverable (.pptx)
└── requirements.txt             # Project dependencies
```

### Main results

10 simulations were run per scenario, with 1,000 agents and a maximum of 200 days.

| Scenario                              | Peak active infections | Reduction vs. base |
|---------------------------------------|-----------------------:|-------------------:|
| Base (current situation)              |                    462 |                  - |
| Scenario 1: 30% vaccination           |                    142 |              69.3% |
| Scenario 2: quarantine at 1%          |                     54 |              88.3% |
| Scenario 3: vaccination and quarantine |                    14 |              96.9% |

Combining vaccination and quarantine produces the largest reduction in the epidemic peak, greater than either intervention alone.

### Validation

The model was validated by comparing the simulated curve with the smoothed real case curve from Colombia. While it does not capture every real-world peak, because it does not model public policy changes, it reproduces the overall qualitative dynamics of the epidemic.

| Metric      | Value |
|-------------|------:|
| MSE         | 0.115 |
| MAE         | 0.231 |
| Correlation | 0.41  |

### Requirements and installation

Using a virtual environment is recommended.

```bash
# Clone the repository
git clone <repository-url>
cd proyecto_epidemia

# Create and activate the virtual environment (optional but recommended)
python -m venv venv
venv\Scripts\activate           # On Linux/macOS: source venv/bin/activate

# Install dependencies
pip install -r requirements.txt
```

### Execution

To reproduce the project results, run the scripts in the following order:

```bash
# 1. Download the dataset
python src/descargar_datos.py

# 2. Exploratory analysis
python src/analisis_datos.py

# 3. Calibrate beta (grid search)
python -m src.calibracion

# 4. Validate the model
python -m src.validacion

# 5. Run the scenarios
python -m src.escenarios

# 6. Analyze emergent behavior
python -m src.emergente

# 7. Generate presentation slides (optional)
python -m src.generar_diapositivas
```

Plots are saved to `results/figuras/` and tables to `results/tablas/`.

### References

- [Our World in Data: COVID-19](https://ourworldindata.org/covid-deaths)
- [Mesa: Agent-based modeling framework](https://mesa.readthedocs.io/)
- [NetworkX: Network analysis in Python](https://networkx.org/)
