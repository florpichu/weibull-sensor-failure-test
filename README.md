# ¿Fallan por azar? Un test para sensores industriales

Trabajo final de la materia **Métodos Estadísticos para Física Experimental (MEFE)** (FCEyN, UBA, 2025).

## Problema

En la industria de procesos, los sensores de temperatura son componentes críticos cuya falla puede generar paradas costosas no planificadas. Este trabajo aborda una pregunta concreta: **¿la probabilidad de que un sensor falle depende del tiempo que lleva operando, o es constante en el tiempo?**

Se modela el tiempo hasta la falla con una **distribución de Weibull**, donde el parámetro de forma *k* determina el comportamiento:
- *k* = 1 → fallas aleatorias (equivalente a una distribución exponencial)
- *k* < 1 → fallas tempranas, con tasa decreciente en el tiempo

## Metodología

Se plantea un contraste de hipótesis (H₀: k=1 vs H₁: k<1) y se resuelve mediante **simulación Monte Carlo**:

1. Se simulan muestras de 100 sensores bajo cada hipótesis.
2. Se estima el parámetro *k* por **máxima verosimilitud (MLE)**, repitiendo el procedimiento 1000 veces para construir la distribución empírica del estimador bajo cada hipótesis.
3. A partir de esa distribución se determina el **valor crítico**, el **error tipo I** (α = 0.05) y el **error tipo II** (β).
4. Se calcula la **curva de potencia del test** (1−β) para distintos valores de *k*, caracterizando la sensibilidad del test.
5. Como validación adicional, se verifica que los **p-valores simulados bajo H₀ sean uniformes en [0,1]** — la condición teórica esperada si el test está bien calibrado.

## Resultados

El estimador MLE resultó preciso (baja dispersión) y capaz de distinguir claramente entre escenarios (k=1 vs k=0.8). La potencia del test es alta (>90%) para fallas tempranas marcadas (k≤0.75), pero cae por debajo del 50% cuando k se acerca a 1, revelando el límite práctico de sensibilidad del método en casos límite.

## Contenido del repositorio

- `weibull_sensor_test.ipynb` — código completo de las simulaciones y figuras.
- `informe_tecnico.pdf` — informe final en formato de paper, con introducción, metodología, resultados y apéndice teórico.

## Herramientas

Python · scipy.stats (`weibull_min`, MLE) · NumPy · Matplotlib
