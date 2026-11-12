# Declaración de uso de IA generativa

## Modelo utilizado

| Modelo | Herramienta | Fecha |
|---|---|---|
| Claude Opus 5.5 (Anthropic) | Claude Code (asistente en terminal) | 11-nov-2026 |

## Porcentaje de ayuda por sección

| Sección (peso) | Ayuda de IA | Qué hizo la IA |
|---|---|---|
| 1. Entendimiento de datos (10%) | ~1% | Ajuste del título del diccionario de variables |
| 2. Entrenamiento (15%) | ~3% | Corrección de numeración en la documentación del entrenamiento |
| 3. Análisis cuantitativo (20%) | ~3% | Una frase que conecta el umbral F1 (0,31) con el umbral de negocio (0,25) |
| 4. Análisis cualitativo (20%) | ~10% | Reorganización de las conclusiones en global / local / sesgo; precisión sobre la comparación SHAP vs. LIME |
| 5. Generación de valor (20%) | ~10% | Búsqueda y enlace de las fuentes; reemplazo de una fuente no verificable (cuota de manejo premium) por el tarifario de Bancolombia |
| 6. Insights (10%) | ~60% | Redacción del informe ejecutivo (`docs/informe_ejecutivo.md`) a partir de los resultados y conclusiones del notebook; corrección de las cifras al umbral 0,25 |
| 7. Declaración (5%) | ~80% | Estructura y redacción de este documento |
| Repositorio y ejecución | ~100% | Estructura de carpetas, `README.md`, `requirements.txt` con versiones fijas, verificación de que el notebook se ejecuta completo sin errores |
| **Total ponderado** | **~15%** | |

Todas las cifras del notebook y del informe provienen de la ejecución del notebook; la IA no generó resultados nuevos.

## Prompts empleados

1. `hola revisa el taller ajusta para que corra local y ajusta la estructura de carpetas`
2. `y comparaste con los puntos del taller? ejecutalo y revisa resultados`
3. `agrega punto 6 y 7 y corrige todo`

## Resumen de lo realizado en la sesión

1. **Ejecución local y estructura:** se organizó el repositorio en `data/`, `notebooks/` y `docs/`, se ajustó la ruta del dataset y se creó un entorno con `requirements.txt`. Las versiones quedaron fijas (scikit-learn 1.6.1) para reproducir exactamente los resultados guardados en el notebook.
2. **Revisión contra el enunciado:** se ejecutó el notebook completo y se comparó cada punto con lo que pide el taller. Se detectaron:
   - un umbral inconsistente entre las secciones 3, 5 y 6;
   - restos de texto de plantilla;
   - fuentes sin enlace, dos de ellas no verificables;
   - el informe ejecutivo y la declaración de IA faltantes.
3. **Correcciones:** se ajustaron los textos señalados en la tabla anterior, se agregaron los enlaces de las fuentes, se redactó el informe ejecutivo y este documento, y se volvió a ejecutar el notebook completo para confirmar que no tiene errores.
