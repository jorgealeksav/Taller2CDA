# Taller 2 – MINE-4101 Ciencia de Datos Aplicada

Predicción de abandono (churn) de clientes bancarios para FinAlpes: modelo de machine learning, interpretación, estimación del valor para el negocio y recomendación.

**Integrantes:** Jorge Acosta (202324675) · Mateo Bernal Bonil (202510037)

## Estructura

```
data/churn.csv                 dataset utilizado
notebooks/Taller2_CDA.ipynb    notebook con los puntos 1 a 7 (único notebook)
docs/informe_ejecutivo.md      punto 6: informe ejecutivo y recomendación
docs/declaracion_IA.md         punto 7: declaración de uso de IA generativa y prompts
docs/Taller2.pdf               enunciado del taller
requirements.txt               dependencias con versiones fijas
```

## Ejecutar en local

Requiere Python 3.10 o superior.

```bash
python3 -m venv .venv
source .venv/bin/activate          # en Windows: .venv\Scripts\activate
pip install -r requirements.txt
jupyter notebook notebooks/Taller2_CDA.ipynb
```

Luego ejecutar **todas las celdas en orden** (*Run all*). El notebook lee el dataset desde `../data/churn.csv`, por eso debe abrirse desde la carpeta `notebooks/`. La ejecución completa tarda unos minutos (búsqueda de hiperparámetros).

Las versiones de `requirements.txt` (scikit-learn 1.6.1) reproducen exactamente los resultados guardados en el notebook; con versiones más recientes, los números de Random Forest pueden variar levemente.
