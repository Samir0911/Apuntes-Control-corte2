

# MATLAB, Simscape y Multibody

## ¿Qué es MATLAB?

MATLAB (Matrix Laboratory) es un entorno de programación y un lenguaje interpretado desarrollado por MathWorks. Es ampliamente utilizado en ingeniería, matemáticas, ciencia y análisis de datos debido a su capacidad para manejar cálculos numéricos, visualización de datos y desarrollo de algoritmos. MATLAB permite el análisis y la visualización de grandes cantidades de datos, el diseño de sistemas de control y la simulación de modelos matemáticos.

**Principales características de MATLAB:**
- Procesamiento de señales, imágenes y video.
- Análisis de datos y visualización gráfica.
- Cálculo numérico y simbólico.
- Programación orientada a objetos.
- Desarrollo de interfaces gráficas (GUIs).
- Integración con otros lenguajes (como C, C++, Python).

---

## ¿Qué es Simscape?

Simscape es una herramienta de MATLAB diseñada para modelar y simular sistemas físicos multidominio. Forma parte del entorno de Simulink y permite integrar modelos físicos basados en ecuaciones diferenciales dentro de un diagrama de bloques. 

**Características principales:**
- Modelado de sistemas eléctricos, mecánicos, hidráulicos y térmicos.
- Interfaz gráfica intuitiva para construir modelos físicos.
- Librerías de componentes como motores, sensores y actuadores.
- Integración directa con Simulink para simulaciones en tiempo continuo y discreto.

**Ventajas:**
- Facilita el modelado de sistemas complejos con componentes prefabricados.
- Permite el uso de modelos físicos reales y simulación en tiempo real.
- Compatible con otros paquetes de simulación en MATLAB.

---

## ¿Qué es la herramienta Multibody?

Multibody es un entorno dentro de Simscape para modelar sistemas mecánicos compuestos por cuerpos rígidos conectados mediante juntas, restricciones y fuerzas. Permite el análisis dinámico de mecanismos complejos, como robots, máquinas y estructuras articuladas. 

**Características principales:**
- Modelado de sistemas mecánicos en 3D.
- Representación gráfica de cuerpos rígidos y articulaciones.
- Análisis de movimiento, fuerzas y trayectorias.
- Exportación de modelos CAD para simulación y análisis.

**Aplicaciones:**
- Diseño de mecanismos robóticos.
- Análisis de movimientos en máquinas industriales.
- Simulación de vehículos y sistemas de transporte.
- Evaluación de sistemas articulados en biomecánica.


Simscape Multibody es una herramienta de MATLAB que permite modelar y simular sistemas mecánicos tridimensionales complejos, como robots, suspensiones de vehículos y equipos de construcción. Utiliza una representación basada en bloques para construir modelos físicos que reflejan la estructura y el comportamiento de sistemas mecánicos reales.

## Componentes Principales y Flujo de Trabajo

Al construir un modelo en Simscape Multibody, se emplean varios bloques fundamentales que representan diferentes aspectos del sistema mecánico. A continuación, se describen algunos de los componentes clave y su función en el diagrama de flujo:

1. **World Frame (Marco Mundial):**
   - Define el sistema de coordenadas global para el modelo.
   - Sirve como referencia absoluta para todos los demás componentes.

2. **Mechanism Configuration (Configuración del Mecanismo):**
   - Establece parámetros generales del sistema, como la gravedad y las unidades de medida.
   - Asegura la coherencia en las simulaciones al definir condiciones físicas globales.

3. **Rigid Transform (Transformación Rígida):**
   - Especifica desplazamientos y rotaciones entre diferentes marcos de referencia.
   - Se utiliza para posicionar y orientar componentes en el espacio tridimensional.

4. **Brick Solid (Sólido Tipo Ladrillo):**
   - Representa un cuerpo rígido con forma de paralelepípedo.
   - Permite definir propiedades físicas como dimensiones, masa e inercia.

5. **Revolute Joint (Unión Revoluta):**
   - Modela una conexión entre dos cuerpos que permite rotación alrededor de un eje fijo.
   - Es esencial para simular movimientos articulados, como bisagras o ejes de rotación.

## Ejemplo de Construcción de un Modelo Simple

Para ilustrar el uso de estos componentes, consideremos la construcción de un péndulo simple:
  ![Figura 1](imagenes_apuntes_2/eje1.png) 
  Figura 1. Diagrama de bloques en multibody de un pendulo.

  
  ![Figura 2](imagenes_apuntes_2/ejemplo1.png) 
  Figura 2. simulacion del pendulo en multibody.

## Pasos para Modelar el Sistema de Péndulo Invertido

1. **Definir el Marco Mundial:**
   - Colocar el bloque *World Frame* para establecer el sistema de coordenadas global, asegurando que todos los objetos en el modelo estén alineados con el sistema de referencia global.

2. **Configurar el Mecanismo:**
   - Añadir el bloque *Mechanism Configuration* para definir las propiedades del modelo mecánico.
   - Establecer la gravedad como *[0, -9.80665, 0]* para simular la aceleración debida a la gravedad en dirección negativa al eje Y.

3. **Crear la Base del Péndulo:**
   - Utilizar un bloque *Brick Solid* para representar la base (Bloque "B").
   - Definir sus dimensiones, por ejemplo, *[5 5 5]* y propiedades de masa, asegurándose de que el material tenga una masa representativa.
     
      ![Figura 3](imagenes_apuntes_2/B.png)
           Figura 3. Bloque "B".

4. **Crear el Brazo del Péndulo:**
   - Utilizar un bloque *Brick Solid* para representar el brazo del péndulo (Bloque "A").
   - Establecer las dimensiones del brazo, por ejemplo, *[20 1 1]*, y asignar las propiedades de masa correspondientes.

      ![Figura 4](imagenes_apuntes_2/A.png)
         Figura 4. Bloque "A".

5. **Posicionar el Brazo:**
   - Colocar el brazo en la posición correcta usando un bloque *Rigid Transform*.
   - Definir las coordenadas y la orientación del brazo en relación con el marco mundial.

     ![Figura 5](imagenes_apuntes_2/Frames.png)   
       Figura 5. Rigid Transform.

6. **Añadir la Articulación:**
   - Conectar el brazo al marco mundial mediante un bloque *Revolute Joint*, lo que permite que el brazo gire alrededor de un eje fijo.
   - Asegurarse de que el eje de rotación del *Revolute Joint* esté alineado con el eje de rotación deseado.

7. **Definir las Restricciones de Movimiento:**
   - Ajustar las propiedades del *Revolute Joint* para definir los límites de movimiento, como los ángulos máximo y mínimo de rotación para evitar movimientos no deseados.

8. **Añadir un Motor o Fuerza (Opcional):**
   - Si se desea simular el control o la activación del péndulo, agregar un bloque *Torque* o un *Electric Motor* para proporcionar la fuerza necesaria para controlar el movimiento del brazo.

9. **Simular el Sistema:**
   - Ejecutar la simulación para observar el comportamiento del sistema de péndulo.
   - Ajustar parámetros como la masa, dimensiones y gravedad según sea necesario para obtener el comportamiento deseado.

     ![Figura 6](imagenes_apuntes_2/grafica1.png)   
       Figura 6. Grafica de posición.

---

# Ejemplo #2.
# Movimiento de Puerta Giratoria en Simscape Multibody


## Nombre del Movimiento

El movimiento mostrado en la simulación es un **"movimiento de compuerta o viga oscilante"**, similar a una **estructura en pórtico** donde la viga horizontal (roja) oscila o gira respecto a los dos pilares verticales.


# Instructivo: Cómo Crear el Movimiento en MATLAB Simscape Multibody

##  Elementos Necesarios

- `World Frame`
- `Mechanism Configuration`
- `Solver Configuration`
- `Rigid Transform`
- `Revolute Joint`
- `Solid`
- `Simulink-PS Converter`
- `Signal Builder` o `Step` o `Ramp` (fuente de señal)


##  Insertar el Marco Mundial

- Agregar bloque `World Frame`.
- Define el sistema de coordenadas global del modelo.

## Configurar el Mecanismo

- Agregar bloque `Mechanism Configuration`.
- Establecer la gravedad como: [0 -9.80665 0]

## Entrada del Movimiento

- Añadir un bloque `Signal Builder`, `Step` o una señal `Sine Wave`.
- Convertir señal con el bloque `Simulink-PS Converter`.
- Esto generará un torque en una junta.

## Crear Sólidos (`Brick Solid`)

### Brazo vertical (gris)
- Dimensiones: `[0.1 0.4 0.1]` 

### Brazo horizontal (rojo)
- Dimensiones: `[0.6 0.1 0.1]`

     ![Figura 7](imagenes_apuntes_2/frames2.png)   
       Figura 7. Brazos (Brick solid).

### Agregar Frames
- En cada bloque `Brick Solid`:
  - Activar `Frame1` y `Frame2`
  - Estos se usarán para conectar con las juntas rotacionales.

## Conectar con Juntas Rotacionales

- Agregar tres bloques `Revolute Joint`:
  - Junta 1: `World Frame` ↔ `Brazo vertical izquierdo`
  - Junta 2: `Brazo vertical izquierdo` ↔ `Brazo horizontal`
  - Junta 3: `Brazo horizontal` ↔ `Brazo vertical derecho`

- En cada junta:
  - Conectar `port B` y `port F` correctamente con los `Frames` de los sólidos.

    
     ![Figura 8](imagenes_apuntes_2/eje2.png)   
       Figura 8. Diagrama de bloques.

## Configurar el Movimiento Actuado

En la `Junta 1` (conectada al mundo):

- Pestaña `Actuation`:
  - `Torque`: `Provided by Input`
  - `Motion`: `Automatically Computed`

- Conectar el `Simulink-PS Converter` al `puerto del torque`.


## Ejecutar y Visualizar

- Ejecutar la simulación.
- Se abrirá el `Mechanics Explorer` con la animación del sistema.
- El movimiento será oscilatorio, tipo vaivén, dependiendo del perfil de señal aplicado.

     ![Figura 9](imagenes_apuntes_2/ejemm2.png)   
       Figura 9. simulación de movimiento.

---

# Ejemplo #3.
# Movimiento de Biela manivela

biela_manivela_simscape:
  titulo: Simulación de mecanismo biela-manivela en Simscape Multibody
  descripcion: >
    Este instructivo describe cómo construir y simular un sistema biela-manivela en MATLAB Simscape Multibody.
    El sistema convierte un movimiento rotacional en un movimiento lineal usando una manivela, una biela y un émbolo.

  ![Figura 10](imagenes_apuntes_2/man.png)   
   Figura 10. simulación de movimiento.
   
  pasos:
    - paso: Crear un nuevo modelo
      instrucciones:
        - Abrir MATLAB y crear un nuevo modelo de Simulink.
        - Arrastrar el bloque "Simscape > Multibody > World Frame" al espacio de trabajo.
    
 - paso: Agregar la manivela
      instrucciones:
        - Insertar un bloque "Solid" y configurar sus dimensiones para representar la manivela.
        - Añadir un "Revolute Joint" y conectarlo entre el World Frame y la manivela.
        - Establecer un torque con un bloque "Joint Actuator" o una señal senoidal.

 - paso: Agregar la biela
      instrucciones:
        - Insertar otro bloque "Solid" para representar la biela.
        - Conectar un nuevo "Revolute Joint" entre la manivela y la biela.
        - Ajustar la posición inicial con un "Rigid Transform" si es necesario.

 - paso: Agregar el émbolo
      instrucciones:
        - Insertar un bloque "Solid" para el émbolo o pistón.
        - Conectar la biela al émbolo mediante un "Revolute Joint".
        - Agregar un "Prismatic Joint" entre el émbolo y el World Frame, restringido al eje X.

 - paso: Establecer condiciones iniciales y señales
      instrucciones:
        - Aplicar una entrada de velocidad angular constante o sinusoidal a la manivela.
        - Verificar que todos los ejes de rotación estén alineados correctamente.
        - Usar "Scopes" o "Simscape Results Explorer" para visualizar el movimiento del émbolo.

    ![Figura 11](imagenes_apuntes_2/gram.png)   
    Figura 11. Diagrama de bloques con grafica de posicion de vector final.

   - paso: Ejecutar simulación
      instrucciones:
        - Configurar el tiempo de simulación (ej. 10 segundos).
        - Ejecutar el modelo.
        - Observar el movimiento oscilatorio generado en el émbolo.

---

# Diseño de Transmisión - Control de Movimiento
   
## Requerimientos Clave del Diseño

1. **Torque del motor:** Asegurarse de que sea mayor que el requerido por la aplicación (¡con margen de seguridad!).
2. **Inercia:** Debe existir un equilibrio adecuado entre la inercia del motor y la de la carga.
3. **Criterios adicionales:** También se debe considerar costo, precisión, tiempo de ciclo, etc.

---

## Fundamentos: Inercia y Torque Reflejado

### ¿Qué es la Inercia?

Es la resistencia de un cuerpo a cambiar su velocidad angular. Es como la masa, pero en el mundo rotacional.

> **Fórmula fundamental de dinámica rotacional:**
> 
$$\sum T = J \cdot \alpha$$
- `T` es el torque.
- `J` es la inercia.
- `α` es la aceleración angular.

- ## Transmisión por Engranajes

### Relación de Engranajes

Esta se define por el número de dientes. Influye en:

- El **torque**
- La **velocidad angular**

En sistemas reales se usa para amplificar o reducir estos parámetros.

## Simulación en MATLAB (Simscape Multibody)

### Paso a Paso para Crear una Simulación:

1. **Abrir Simulink** y buscar `Simscape Multibody`.
2. Insertar componentes como `Solid`, `Revolute Joint`, y `Gear Constraint`.
3. Configurar la **relación de engranaje** (por ejemplo, 5:1).
4. Agregar sensores para medir velocidad, torque, y posición angular.
5. Ejecutar la simulación y observar la animación.
6. Analizar cómo la inercia reflejada varía con la transmisión.

## Inercia Reflejada

Cuando usamos un sistema con engranajes, la **inercia de la carga** se "refleja" al eje del motor dependiendo de la relación de transmisión.

 **Acople directo:**

 $$J_{total} = J_{motor} + J_{carga}$$
 
 **Con engranajes:**
 $$J_{reflejada} = J_{carga} / (N^2) $$
 
- `N` es la relación de engranaje (por ejemplo, 5 si es 5:1).

---

## Torque Reflejado

Al igual que la inercia, el torque también se transforma con la relación de engranajes:

**Fórmula:**
$$T_{reflejado} = T_{carga} / N$$

## Eficiencia del Sistema

En sistemas reales, hay pérdidas. La eficiencia `η` se define como:

**Fórmula de potencia:**
$$P = T * ω$$

Y entonces: $η = P_{salida} / P_{entrada}$

## Inercia Total Reflejada al Eje del Motor

Lo ideal es calcular toda la inercia reflejada al eje del motor para dimensionar correctamente el sistema.

## Relación de Inercia

Es una comparación entre la inercia de la carga y la del motor.

**Fórmula:**$Relación_{inercia} = J_{carga}_{reflejada} / J_{motor}$

## Ejemplo (Interpretado):

- **Relación de engranaje**: $5:1$ (reductor)
- **Inercia reflejada del engranaje**: $0.15\ \text{Kg} \cdot \text{cm}^2 = 1.5 \times 10^{-5}\ \text{Kg} \cdot \text{m}^2$
- **Eficiencia del engranaje**: $97\%$
- **Inercia del rotor del motor**: $1.5 \times 10^{-5}\ \text{Kg} \cdot \text{m}^2$
- **Inercia de la carga (lado de la carga)**: $1.0 \times 10^{-3}\ \text{Kg} \cdot \text{m}^2$

**Relación de inercia:**
### Cálculo de inercia reflejada y relación de inercias

$$
J_{\text{carga reflejada}} = \frac{J_{\text{carga}}}{N^2}
$$

$$
J_{\text{carga reflejada}} = \frac{1.0 \times 10^{-3}}{5^2} = 4.0 \times 10^{-5}\ \text{Kg} \cdot \text{m}^2
$$

#### Relación de inercia entre carga reflejada y rotor del motor

$$
\text{Relación de inercia} = \frac{J_{\text{carga reflejada}}}{J_{\text{motor}}} = \frac{4.0 \times 10^{-5}}{1.5 \times 10^{-5}} \approx 2.67
$$

## Recomendaciones de Diseño (Guías Prácticas)

| Relación de Inercia | Rango        | Casos de Uso                    | Posibles Problemas         |
|---------------------|--------------|----------------------------------|----------------------------|
| Baja                | 1 - 2        | Movimientos rápidos              | Motor sobredimensionado    |
| Alta                | > 10         | Dinámicas no críticas            | Baja eficiencia, torque bajo |

Tabla 1. Relación de Inercia


## Polea-Correa

### ¿Qué es?

Es un sistema que transforma movimiento rotacional de un eje a otro usando una correa. Se compone de dos poleas conectadas por una correa que puede ser **lisa** o **dentada**. La relación de transmisión se define por los radios de las poleas.

---

### Relación de transmisión

Se basa en que la velocidad lineal de la correa es la misma en ambas poleas.

**Fórmula:**
$$v_1 = v_2 \Rightarrow \omega_1 \cdot r_1 = \omega_2 \cdot r_2$$

### Simulación en Simscape (Polea-Correa)

#### Paso a paso:

1. Abrir **Simulink** y crear un nuevo modelo.
2. Agregar un bloque de `Belt Drive` desde la biblioteca de `Simscape`.
3. Conectar dos `Rotational Motion Sources` y dos `Inertias`.
4. Establecer los radios de las poleas (`r1` y `r2`).
5. Ejecutar la simulación para observar cómo se transmite la velocidad angular.

###  Inercia Reflejada en Correa

La inercia reflejada de la correa se comporta igual que en los engranajes. Se modela como una masa rotatoria.

**Fórmula:**
 $$J_{\text{belt} \rightarrow \text{in}} = \left( \frac{W_{\text{belt}}}{g \cdot \eta} \right) \cdot r_{\text{ip}}^2$$

### Torque de carga

El torque reflejado del sistema también se comporta como en engranajes:

**Fórmula (implícita en engranajes):**
$$T_{\text{ref}} = \frac{T_{\text{load}}}{N}$$

## Tornillo Guía

### ¿Qué es?

Es un sistema que convierte **movimiento rotacional en lineal**, usado en máquinas CNC, actuadores lineales, impresoras 3D, etc.

Hay dos tipos comunes:

- Tornillos **ACME** (eficiencia: 35% – 85%)
- Tornillos **de bolas** (eficiencia: 85% – 95%)

### Relación de transmisión (Tornillo)

La relación entre el movimiento angular del tornillo y el movimiento lineal de la carga está dada por el paso (lead) $p$.

**Fórmulas:**

$$\frac{\Delta \theta}{\Delta x} = \frac{2\pi}{p}$$
$$\frac{\dot{\theta}}{\dot{x}} = \frac{2\pi}{p}$$

### 🔧 Simulación en Simscape (Tornillo Guía)

#### Paso a paso:

1. Abrir Simulink y seleccionar `Simscape Multibody`.
2. Añadir un bloque `Lead Screw`.
3. Configurar el paso del tornillo (`Lead`) en metros por revolución.
4. Agregar una masa lineal (`Prismatic Joint`) y una fuerza de carga.
5. Ejecutar la simulación para ver el desplazamiento.

#### Resultado de ejemplo:

$$117.8\ \text{rad} \cdot \left( \frac{1\ \text{rev}}{2\pi\ \text{rad}} \right) \cdot 0.015\ \text{m/rev} = 0.28\ \text{m}$$

###  Inercia reflejada

Cuando la carga se mueve linealmente, su energía cinética puede expresarse como rotacional, reflejándola al eje del motor.

**Fórmula de inercia del tornillo:**

$$J_{\text{screw}} = \frac{\pi \cdot L \cdot \rho \cdot D^4}{32}$$

### Torque de carga

Para calcular el torque reflejado hacia el motor desde la carga, se tiene en cuenta:

- El **coeficiente de fricción**
- Si la **fuerza gravitacional** actúa o no (depende de la inclinación del sistema)

### Ejemplo interpretado

- **Carga**: $50\ \text{kg}$
- **Tornillo**: esferado  
- **Densidad**: $0.14\ \text{kg/cm}^3 = 140000\ \text{kg/m}^3$
- **Diámetro**: $0.182\ \text{cm} = 0.00182\ \text{m}$
- **Longitud**: $36\ \text{cm} = 0.36\ \text{m}$
- **Paso**: $0.75\ \text{cm/rev} = 0.0075\ \text{m/rev}$
- **Eficiencia**: $90\% = 0.9$
- **Peso del carro**: $0.23\ \text{kg}$

> **Cálculo de inercia del tornillo:**

$$J_{\text{screw}} = \frac{\pi \cdot 0.36 \cdot 140000 \cdot (0.00182)^4}{32} = 5.42 \times 10^{-8}\ \text{Kg} \cdot \text{m}^2$$

> **Inercia reflejada total:**

$$J_{\text{ref, trans}} = 5.42 \times 10^{-8} + \left( \frac{1}{0.9 \cdot 8.382} \right) \cdot \left( \frac{50 + 0.23}{9.89} \right) = 8.1\ \text{Kg} \cdot \text{m}^2$$

# Elementos de Transmisión (Parte 3)

## Piñón - Cremallera

### ¿Qué es?

Es un mecanismo que convierte **movimiento rotacional en movimiento lineal**. El piñón (rueda dentada) se acopla a la cremallera (guía lineal dentada). Muy usado en CNC, robótica y actuadores.

### Relación de transmisión

Se basa en la velocidad lineal que genera el piñón al girar.

**Fórmulas:**

$$V_{\text{rack}} = r_{\text{pinion}} \cdot \omega_{\text{pinion}}$$

$$N = \frac{\text{Velocidad}_{\text{motor}}}{\text{Velocidad}_{\text{carga}}}$$

*Importante:* $\omega_{\text{pinion}}$ debe estar en rad/s.

### Simulación en Simscape (Piñón-Cremallera)

#### Paso a paso:

1. Abrir Simulink y seleccionar `Simscape > Multibody`.
2. Insertar `Rack and Pinion Constraint`.
3. Conectar un `Revolute Joint` al piñón y un `Prismatic Joint` a la cremallera.
4. Configurar el radio del piñón.
5. Agregar sensores para medir posición y velocidad.
6. Ejecutar la simulación y observar la conversión rotacional-lineal.

### Inercia reflejada

Funciona igual que con el tornillo guía. La masa lineal de la cremallera se puede reflejar como inercia al eje del motor.

### Torque de carga

El torque que el motor necesita depende de la fuerza que se necesita en la cremallera y del radio del piñón:

**Fórmula base (implícita):**

$$T = F \cdot r$$


## Banda Transportadora

### ¿Qué es?

Es un sistema que **transforma el movimiento rotacional de un eje en movimiento lineal continuo**, usando una banda plana. Usada en líneas de producción y robótica móvil.


### Relación de transmisión

Se determina por el radio del eje motriz y su velocidad angular.

**Fórmulas:**

$$V_{\text{belt}} = r_{\text{ip}} \cdot \omega_{\text{ip}}$$

$$N = \frac{\text{Velocidad}_{\text{motor}}}{\text{Velocidad}_{\text{carga}}}$$


### Inercia reflejada y torque de carga

Las bandas se modelan igual que los tornillos guía, por lo tanto la inercia reflejada sigue una relación similar.

**Fórmula:**

$$J_{\text{IP}} = J_{\text{LP}} = J_p$$


### Consideraciones con bandas más largas

Cuando hay varios rodillos locos, la banda es más larga y la carga se distribuye. Esto afecta la **relación de transmisión** y la **inercia reflejada**.


### Torque de carga con ángulo

Cuando la banda sube o baja en un ángulo, se considera el efecto del peso proyectado en la dirección del movimiento, afectando el torque requerido.


## Simulación en Simscape (Banda Transportadora)

#### Paso a paso:

1. Abrir Simulink y crear un nuevo modelo.
2. Usar bloques como `Rotational Motion Source`, `Pulley`, `Belt`, `Mass`, y `Prismatic Joint`.
3. Configurar los radios y masas involucradas.
4. Agregar sensores para registrar velocidades, fuerzas y posición.
5. Ejecutar la simulación.
6. Observar cómo la banda transmite el movimiento.


conclusiones:

   Se comprendió el principio de conversión de movimiento rotacional en movimiento lineal mediante el mecanismo biela-manivela, observando cómo la rotación continua de una manivela genera un movimiento alternativo en el émbolo. 
   
   La implementación en Simscape Multibody permite visualizar claramente la cinemática del sistema, identificando cómo interactúan las juntas rotacionales y prismáticas para permitir el movimiento deseado.
   
   Se reforzó el uso adecuado de bloques fundamentales como "Solid", "Revolute Joint", "Prismatic Joint" y "Rigid Transform", así como la importancia de alinear correctamente los ejes de movimiento entre cada componente.
   
   El uso de sensores y bloques de visualización como "Scope" o "Mechanics Explorer" permitió analizar gráficamente el comportamiento dinámico del sistema, facilitando su validación.
   
   Este ejercicio sirvió como base para modelar sistemas mecánicos más complejos, permitiendo aplicar principios de diseño mecánico, simulación y análisis en un entorno virtual antes de su implementación física.

   A lo largo de este estudio, se ha aprendido que los sistemas de transmisión como el piñón-cremallera, el tornillo guía y la banda transportadora convierten el movimiento rotacional en lineal, y que su relación de transmisión depende del radio y la velocidad angular de los componentes motrices. Además, se comprendió el concepto de inercia reflejada, que permite modelar la energía cinética de la carga como rotacional y reflejarla al motor, y cómo el torque de carga está determinado por la fuerza necesaria para mover la carga y el radio del componente. La simulación en Simscape se destacó como una herramienta esencial para modelar estos sistemas, validar su comportamiento y medir variables clave como velocidad, posición y fuerzas. También se aprendió que factores como la geometría, la eficiencia y la longitud de la banda afectan el rendimiento y la distribución de la carga en sistemas más complejos. En general, se adquirió una comprensión profunda de cómo estos mecanismos operan y cómo se pueden optimizar para mejorar el rendimiento en aplicaciones industriales y robóticas.
