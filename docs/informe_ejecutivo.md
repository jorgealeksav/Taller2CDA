# Informe ejecutivo – Predicción de abandono de clientes (FinAlpes)

**MINE-4101 Ciencia de Datos Aplicada · Taller 2**
**Integrantes:** Jorge Acosta (202324675) · Mateo Bernal Bonil (202510037)

---

## 1. El problema

En un mercado bancario maduro, crecer depende más de retener clientes que de atraer nuevos. Un banco minorista pierde cerca del **15% de sus clientes cada año** y cada cliente activo genera entre **COP 500.000 y 900.000** de ingreso anual. FinAlpes busca una herramienta que identifique a tiempo a los clientes en riesgo de abandono para dirigirles campañas de retención.

Como prueba de concepto se usó una muestra de **10.000 clientes europeos** (después de limpiar duplicados, categorías inconsistentes y valores imposibles), en la que el **20,4%** abandonó el banco.

## 2. El modelo

Se compararon tres modelos: regresión logística, Random Forest y Gradient Boosting. El elegido es **Gradient Boosting**:

| Indicador (conjunto de prueba, 2.000 clientes) | Resultado |
|---|---|
| ROC-AUC (capacidad de separar a quienes se van de quienes se quedan) | **0,866** (IC 95%: 0,844 – 0,884) |
| Clientes que abandonan y el modelo detecta (recall), umbral 0,25 | **68 de cada 100** |
| Clientes contactados que realmente iban a abandonar (precisión), umbral 0,25 | **58 de cada 100** |

Random Forest obtuvo un desempeño prácticamente igual (la diferencia no es estadísticamente significativa); la regresión logística es claramente inferior (AUC 0,778) porque no capta relaciones no lineales como la del número de productos.

## 3. Hallazgos principales

1. **El número de productos es la señal más fuerte, y no es lineal.** Con 2 productos el abandono es cercano al 8%; con 3 productos sube al 83% y con 4 llega al 100%. Tener más productos no significa más fidelidad: los clientes con 3 o 4 productos podrían estar insatisfechos con lo que tienen.
2. **La edad es el segundo factor.** El riesgo es bajo hasta los 35-40 años, sube entre los 45 y 65 años y alcanza su punto más alto entre los 56 y 62 años.
3. **La inactividad duplica el riesgo:** 27% de abandono en inactivos frente a 14% en activos.
4. **Alemania (32%) y las mujeres (25%)** muestran más abandono que el promedio. Estas variables deben usarse con cuidado para no generar decisiones discriminatorias.
5. **Tener tarjeta de crédito y la antigüedad** casi no ayudan a predecir el abandono.

## 4. Valor para el negocio

Para un banco de **20.000 clientes** con churn del 15%, efectividad de campaña del 30% y costo de COP 38.000 por cliente contactado:

| Concepto | Valor |
|---|---|
| Clientes contactados al año | 4.151 |
| Clientes retenidos al año | 615 |
| Ganancia anual (antes de operación) | **COP 272,6 millones** |
| Costo de operación anual | COP 19,0 millones |
| Inversión inicial | COP 26,2 millones |
| Ganancia neta anual | **COP 253,5 millones** |
| ROI del primer año | **866%** |
| Punto de equilibrio | **≈ 1,2 meses** |
| Alternativa "contactar a todos" | pérdida de COP 130 millones |

El valor del modelo está en **a quién no contactar**: la campaña es rentable mientras la precisión supere el 18,1%, y el modelo opera muy por encima de ese mínimo.

**Sensibilidad.** Incluso con ingreso de COP 500.000 y costo de contacto de COP 100.000, la ganancia sigue siendo positiva (≈ COP 23 millones/año). El supuesto crítico es la **efectividad de la campaña**: si solo retiene al 10% (en lugar del 30%), el resultado pasa a una pérdida de ≈ COP 14 millones.

## 5. Limitaciones

- Los datos son de clientes europeos; el comportamiento en Colombia puede ser distinto. Hay que reentrenar y validar con datos locales.
- La efectividad del 30%, el costo de contacto y el costo de mantenimiento son supuestos, no resultados de una campaña real.
- El modelo usa características estáticas (no transacciones, quejas ni uso de canales digitales) y el análisis financiero solo considera un año de ingresos.

## 6. Recomendación

**Implementar el modelo Gradient Boosting mediante un piloto controlado**, con umbral de 0,25:

1. **Prueba A/B antes de escalar:** un grupo de clientes en riesgo recibe la campaña y otro grupo comparable no; así se mide la efectividad real y se valida el supuesto del 30%.
2. **Campañas por segmento:**
   - 1 producto → ofrecer productos complementarios que fortalezcan la vinculación.
   - 3 o 4 productos → revisar satisfacción y dar acompañamiento personalizado.
   - Inactivos → campañas de reactivación e incentivos por uso.
   - 45 a 65 años → asesoría financiera personalizada y atención preferencial.
3. **Enriquecer y monitorear el modelo:** incorporar transacciones, PQRS y uso digital; reentrenar periódicamente y vigilar el sesgo por género y país.
