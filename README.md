Simulación Basada en Agentes de la Propagación de COVID-19 en Colombia

Tema: COVID-19 en Colombia — Modelo SEIR con red de contactos
Tecnologías: Python, Mesa, NetworkX, Pandas, Matplotlib, Seaborn

Descripción
Modelo de simulación basada en agentes (ABM, por sus siglas en inglés) que reproduce la propagación del COVID-19 durante la primera ola en Colombia (2020-2021). El proyecto utiliza datos reales de Our World in Data para calibrar el modelo y evaluar el impacto de tres escenarios de intervención diferentes (vacunación, cuarentena y una combinación de ambas).

Características del Modelo
Tipo de modelo: SEIR (Susceptible, Expuesto, Infeccioso, Recuperado) adaptado con la inclusión de un estado Vacunado (V).

Red de contactos: Topología de red small-world (Watts-Strogatz).

Agentes: 1,000 personas simuladas.

Parámetros calibrados:

Tasa de transmisión (
β
β) = 0.045

Periodo de incubación = 3 días

Periodo infeccioso = 7 días

Número reproductivo efectivo (
R
0
R 
0
​
 ): 
≈
≈ 2.8 (consistente con las estimaciones reales).

Estructura del Proyecto
text
proyecto_epidemia/
├── data/
│   ├── raw/                    # Dataset original de OWID
│   └── processed/              # Datos filtrados (covid_limpio.csv)
├── src/
│   ├── descargar_datos.py      # Descarga el dataset
│   ├── explorar.py             # Exploración inicial
│   ├── analisis_datos.py       # Estadísticas y gráficos
│   ├── modelo_epidemia.py      # Modelo ABM (Mesa)
│   ├── calibracion.py          # Ajuste de beta
│   ├── validacion.py           # Validación vs. datos reales
│   ├── escenarios.py           # Ejecución de escenarios + base
│   ├── emergente.py            # Análisis de comportamiento emergente
│   └── generar_diapositivas.py # Genera el archivo de presentación
├── results/
│   ├── figuras/                # Gráficos exportados
│   └── tablas/                 # Tablas CSV y reportes
├── presentacion/               # Entregable final (.pptx)
└── requirements.txt            # Dependencias del proyecto
Resultados Principales
Se ejecutaron 10 simulaciones por escenario (N=1000 agentes, 200 días máximos).

Escenario	Pico de Infectados	Reducción vs Base
BASE (situación actual)	462	—
Esc1 (vacunación 30%)	142	69.3%
Esc2 (cuarentena al 1%)	54	88.3%
Esc3 (vacunación + cuarentena)	14	96.9%
Validación
El modelo se validó comparando la curva simulada con la curva real de casos suavizada de Colombia. Aunque el modelo no captura todos los picos de la realidad (dado que no modela cambios en las políticas públicas), sí reproduce la dinámica cualitativa general.

MSE: 0.115

MAE: 0.231

Correlación: 0.41

Requisitos e Instalación
Se recomienda usar un entorno virtual para instalar las dependencias.

bash
# Clonar el repositorio
git clone <url-del-repositorio>
cd proyecto_epidemia

# Crear y activar entorno virtual (opcional pero recomendado)
python -m venv venv
source venv/bin/activate  # En Windows: venv\Scripts\activate

# Instalar dependencias
pip install -r requirements.txt
Ejecución
Para reproducir los resultados del proyecto, ejecute los scripts en el siguiente orden:

bash
# 1. Descargar dataset
python src/descargar_datos.py

# 2. Análisis exploratorio
python src/analisis_datos.py

# 3. Calibrar beta (Búsqueda en grilla)
python -m src.calibracion

# 4. Validar modelo
python -m src.validacion

# 5. Ejecutar escenarios
python -m src.escenarios

# 6. Analizar comportamiento emergente
python -m src.emergente

# 7. Generar diapositivas (Opcional)
python -m src.generar_diapositivas
Referencias
Our World in Data COVID-19

Mesa: Agent-based modeling framework

NetworkX: Network analysis in Python

Agent-Based Simulation of COVID-19 Propagation in Colombia
Course: Modeling and Simulation
Topic: COVID-19 in Colombia — SEIR Model with Contact Network
Technologies: Python, Mesa, NetworkX, Pandas, Matplotlib, Seaborn

Description
Agent-Based Model (ABM) that simulates the spread of COVID-19 during the first wave in Colombia (2020-2021). The project uses real data from Our World in Data to calibrate the model and evaluate the impact of three different intervention scenarios (vaccination, quarantine, and a combination of both).

Model Features
Model type: SEIR (Susceptible, Exposed, Infectious, Recovered) extended with a Vaccinated (V) state.

Contact network: Small-world network topology (Watts-Strogatz).

Agents: 1,000 simulated individuals.

Calibrated parameters:

Transmission rate (
β
β) = 0.045

Incubation period = 3 days

Infectious period = 7 days

Effective reproductive number (
R
0
R 
0
​
 ): 
≈
≈ 2.8 (consistent with real-world estimates).

Project Structure
text
proyecto_epidemia/
├── data/
│   ├── raw/                    # Original OWID dataset
│   └── processed/              # Filtered data (covid_limpio.csv)
├── src/
│   ├── descargar_datos.py      # Dataset downloader
│   ├── explorar.py             # Initial exploration
│   ├── analisis_datos.py       # Statistics and plots
│   ├── modelo_epidemia.py      # ABM Model (Mesa)
│   ├── calibracion.py          # Beta calibration
│   ├── validacion.py           # Validation vs. real data
│   ├── escenarios.py           # Base + scenario execution
│   ├── emergente.py            # Emergent behavior analysis
│   └── generar_diapositivas.py # Presentation generator
├── results/
│   ├── figuras/                # Exported plots
│   └── tablas/                 # CSV tables and reports
├── presentacion/               # Final deliverable (.pptx)
└── requirements.txt            # Project dependencies
Main Results
10 simulations were run per scenario (N=1000 agents, max 200 days).

Scenario	Peak Active Infections	Reduction vs Base
BASE (current situation)	462	—
Scen1 (30% vaccination)	142	69.3%
Scen2 (quarantine at 1%)	54	88.3%
Scen3 (vaccination + quarantine)	14	96.9%
Validation
The model was validated by comparing the simulated curve with the smoothed real case curve from Colombia. While the model does not capture every real-world peak (as it does not model public policy changes), it successfully reproduces the overall qualitative dynamics.

MSE: 0.115

MAE: 0.231

Correlation: 0.41

Requirements and Installation
Using a virtual environment is recommended.

bash
# Clone the repository
git clone <repository-url>
cd proyecto_epidemia

# Create and activate virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
Execution
To reproduce the project results, run the scripts in the following order:

bash
# 1. Download dataset
python src/descargar_datos.py

# 2. Exploratory analysis
python src/analisis_datos.py

# 3. Calibrate beta (Grid search)
python -m src.calibracion

# 4. Validate model
python -m src.validacion

# 5. Run scenarios
python -m src.escenarios

# 6. Analyze emergent behavior
python -m src.emergente

# 7. Generate presentation slides (Optional)
python -m src.generar_diapositivas
References
Our World in Data COVID-19

Mesa: Agent-based modeling framework

NetworkX: Network analysis in Python
