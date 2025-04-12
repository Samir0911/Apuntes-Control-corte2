
# Sintonización PID en Lazo Cerrado

## Objetivo
Diseñar un controlador PID basado en pruebas en lazo cerrado, identificando la dinámica del sistema mediante métodos empíricos.

## Método de Ziegler & Nichols (Ciclo Último)

### Procedimiento paso a paso:
1. Ajustar las ganancias PID a 0.
2. Aumentar la ganancia proporcional (Kp) progresivamente hasta lograr una oscilación sostenida (estado marginalmente estable).
3. Medir el período de oscilación obtenido, denominado Pu.
4. La ganancia en la que se produce la oscilación se denomina ganancia última (Ku).

### Ejemplo de solución analítica

Se parte de la función de transferencia:

$$G = \frac{1}{s^3 + 6s^2 + 11s + 6}$$

En lazo cerrado, la función se convierte en:

$$Go = \frac{Kp}{s^3 + 6s^2 + 11s + 6 + Kp}$$

Para analizar la respuesta, se utiliza la sustitución $$s = j\omega$$, lo que permite separar la parte real y la parte imaginaria.

#### Paso 1: Encontrar $\(\omega\)$ (frecuencia de oscilación)

Se iguala a 0 la parte imaginaria del denominador:

$$-\omega^2 + 11 = 0 \quad \Rightarrow \quad \omega = 11$$

Luego, el período de oscilación es:

$$Pu = \frac{2\pi}{11} \approx 1.894 \text{ segundos}$$

#### Paso 2: Encontrar Ku (ganancia última)

Se iguala a 0 la parte real del denominador:

$$Kp = 6\omega^2 - 6$$

Reemplazando $\(\omega = 11\)$:

$$Kp = 6 \times 11 - 6 = 60 \quad \Rightarrow \quad Ku = 60$$

## Ecuaciones de diseño según Ziegler & Nichols

| Tipo de Controlador | Kp      | Ti       | Td      |
|---------------------|---------|----------|---------|
| P                   | $0.5 Ku$  | -        | -       |
| PI                  | $0.45 Ku$ | $Pu / 1.2$ | -       |
| PID                 | $0.6 Ku$  | $Pu / 2$   | $Pu / 8$  |

Tabla 1. Ecuaciones de diseño según Ziegler & Nichols.

## Método del Relé

Este método mejora al de Ziegler & Nichols al evitar elevar excesivamente la señal de control.

### Procedimiento:
1. Cerrar el lazo utilizando un relé con histéresis.
2. Observar la oscilación sostenida.
3. Medir el período (Pu) y la amplitud del ciclo último (Au).
4. Calcular la ganancia crítica (Kc) usando la fórmula:

$$Kc = \frac{4d}{\pi \left(Au^2 - \varepsilon^2\right)}$$

## Sintonización PI utilizando el método del relé

| Parámetro | Fórmula                                |
|-----------|----------------------------------------|
| Kp        | $\( \frac{5Kc}{6} \)$                    |
| Ti        | $\( \frac{12 + KKc}{15 + 14KKc} \)$        |
| Td        | $\( \frac{Pu}{5} \)  (según ajuste)$     |

Tabla 2. Sintonización PI utilizando el método del relé

Estos ajustes permiten lograr un sobreimpulso inferior al 10%.

## Fenómeno Wind-up

El fenómeno wind-up ocurre cuando el integrador del controlador sigue acumulando error a pesar de la saturación del actuador, afectando la respuesta del sistema.

### Estrategias de Anti Wind-up:

1. **Saturación de la acción integral:** Limita el acumulado del integrador.
2. **Integración condicional:** Solo se integra cuando el actuador no está saturado.
3. **Recálculo y seguimiento:** Se estima la saturación y se ajusta suavemente la acción integral.

La fórmula para el recálculo es:

$$Tt = Ti \times Td$$

# Ejercicios Aplicando la Teoría de Sintonización PID en Lazo Cerrado

A continuación se presentan varios ejercicios complejos que aplican la teoría explicada, usando tanto el método de Ziegler & Nichols como el método del relé, e incluyendo estrategias para mitigar el fenómeno de wind-up. Se asume que se tiene conocimiento de funciones de transferencia, análisis en frecuencia y conceptos básicos de control.

---

## Ejercicio 1: Sintonización PID con Método de Ziegler & Nichols

**Enunciado:**

Considere el siguiente sistema representado por la función de transferencia:

$$G(s) = \frac{1}{s^3 + 4s^2 + 5s + 2}$$

Realice los siguientes pasos:

1. Configure un lazo cerrado partiendo de la función de transferencia y con un controlador proporcional (Kp) puro.
2. Incrementando Kp desde 0, determine el valor crítico de Kp, denominado Ku, en el que el sistema presenta oscilaciones sostenidas (estado marginalmente estable).  
3. Sustituyendo $\( s = j\omega \)$, encuentre la frecuencia $\(\omega\)$ (y el período Pu) a partir de la condición de que la parte imaginaria del denominador es cero.
4. Utilice los resultados para calcular los parámetros del controlador PID usando las siguientes ecuaciones:

| Tipo de Controlador | \( Kp \)    | \( Ti \)  | \( Td \)  |
|---------------------|-------------|-----------|-----------|
| PID                 | $$\( 0.6Ku \)$$ | $$\( Pu/2 \)$$  | $$\( Pu/8 \)$$  |

Tabla 3. PID


**Solución:**

1. La función en lazo cerrado con una acción proporcional es:

   $$Go(s) = \frac{Kp}{s^3 + 4s^2 + 5s + 2 + Kp}$$

2. Para encontrar la oscilación sostenida, se realiza el análisis en frecuencia sustituyendo $\( s = j\omega \)$:

   $$Go(j\omega) = \frac{Kp}{(j\omega)^3 + 4(j\omega)^2 + 5(j\omega) + 2 + Kp}$$

   Se despejan las partes real e imaginaria del denominador de la siguiente forma:
   - Expresar cada potencia de $\( j\omega \)$ (recordando que $$\( j^2 = -1 \)$$, $$\( j^3 = -j \)$$, etc.).
   - Imponer la condición de que la parte imaginaria sea cero para hallar \(\omega\).

3. Suponga que, mediante análisis o simulación, se determina que:
   - La condición de oscilación se cumple para $$\(\omega = 3 \, rad/s\)$$.
   - Entonces, el período es:
     
     $$Pu = \frac{2\pi}{3} \approx 2.094 \, \text{segundos}$$
     
   - De igual forma, se encuentra que el valor crítico (ganancia última) es:
     
     $$Ku = 50$$

4. Con estos resultados se procede a sintonizar el controlador PID:
   - $$\(Kp_{PID} = 0.6Ku = 0.6 \times 50 = 30\)$$
   - $$\(Ti = Pu/2 = 2.094/2 \approx 1.047 \, \text{segundos}\)$$
   - $$\(Td = Pu/8 = 2.094/8 \approx 0.262 \, \text{segundos}\)$$

---

## Ejercicio 2: Sintonización PI mediante el Método del Relé

**Enunciado:**

Se tiene un sistema cuya respuesta en lazo cerrado se obtiene utilizando un relé con histéresis para evitar aumentar demasiado la señal de control. Durante la prueba se miden:
- Amplitud del ciclo último: $\(Au = 0.5\)$
- Período del ciclo último: $\(Pu = 1.5 \, \text{segundos}\)$
- La constante de histéresis es $\( d = 0.1 \)$
- Se asume un pequeño valor de error $\(\varepsilon\)$ que puede considerarse despreciable para simplificar el cálculo.

1. Calcule la ganancia crítica \(Kc\) utilizando la fórmula:

   $$Kc = \frac{4d}{\pi \left(Au^2 - \varepsilon^2\right)}$$

2. Sintonice un controlador PI aplicando las siguientes fórmulas (una posible formulación empírica):

| Parámetro | Fórmula                    |
|-----------|----------------------------|
| $\( Kp \)$  | $\( \frac{5Kc}{6} \)$        |
| $\( Ti \)$  | $\( \frac{Pu}{1.2} \)$       |

Tabla 4. Parametros para controlador.

**Solución:**

1. Calculando $\(Kc\)$ $(tomando \(\varepsilon \approx 0\))$:

   $$Kc = \frac{4 \times 0.1}{\pi (0.5^2)} = \frac{0.4}{\pi \times 0.25} = \frac{0.4}{0.785} \approx 0.51$$

2. Sintonizando el controlador PI:
   - $$\(Kp = \frac{5Kc}{6} = \frac{5 \times 0.51}{6} \approx 0.425\)$$
   - $$\(Ti = \frac{Pu}{1.2} = \frac{1.5}{1.2} \approx 1.25 \, \text{segundos}\)$$

---

## Ejercicio 3: Análisis y Aplicación de Estrategias Anti Wind-up

**Enunciado:**

Un sistema controlado por un PID presenta saturación en el actuador, lo que provoca el fenómeno wind-up. Se le ha implementado una estrategia de recálculo y seguimiento, en la que se establece que la acción de integración se modula para reducir la acumulación excesiva. Se dispone de los siguientes parámetros:
- Tiempo integral configurado: $$\(Ti = 2.0 \, \text{segundos}\)$$
- Tiempo derivativo configurado: $$\(Td = 0.5 \, \text{segundos}\)$$

Determine el valor de la constante para el anti wind-up $\(Tt\)$ usando la siguiente relación:

$$Tt = Ti \times Td$$

Además, discuta brevemente la implicación de este parámetro en la velocidad de respuesta del sistema.

**Solución:**

1. Calcular $\(Tt\)$:

   $$Tt = Ti \times Td = 2.0 \times 0.5 = 1.0 \, \text{segundo}$$

2. Interpretación:
   - El parámetro $\(Tt\)$ define la velocidad a la cual se suspende o modula la acción integral cuando se acerca la señal de control a la saturación.
   - Un valor de $\(Tt\)$ menor puede hacer que la acción anti wind-up sea demasiado agresiva, afectando la respuesta del sistema, mientras que un valor mayor permite una respuesta más suave.
   - En este caso, $\(Tt = 1.0 \, s\)$ se recomienda para equilibrar el tiempo de respuesta del sistema y prevenir la acumulación excesiva en el integrador.

---


## Conclusiones

- Se aprendío a aplicar la teoría de sintonización PID en lazo cerrado mediante el análisis de funciones de transferencia y el uso de métodos empíricos como Ziegler & Nichols y el método del relé; se estudio cómo identificar parámetros críticos como Ku, Pu y Kc para alcanzar un estado marginalmente estable, interpreté la importancia de ajustar adecuadamente los parámetros del controlador (Kp, Ti, Td) para optimizar la respuesta del sistema, y comprendímos que implementar estrategias anti wind-up es fundamental para evitar la saturación del actuador y mantener un rendimiento robusto en aplicaciones reales de control.
- La sintonización en lazo cerrado es ampliamente utilizada en la industria.
- El método del relé permite obtener una respuesta mejorada sin incrementar excesivamente la señal de control.
- Es fundamental implementar estrategias anti wind-up para proteger el actuador y optimizar la respuesta del sistema.







