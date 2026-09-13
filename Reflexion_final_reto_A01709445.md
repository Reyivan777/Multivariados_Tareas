# Reflexión final del reto

**Rey Iván de la Fuente Chávez — A01709445**

## Parte A. Reflexión argumentada

### 1. Afirmación

Después de realizar el reto, considero que la principal utilidad del modelado multivariado es que permite estudiar un fenómeno real tomando en cuenta que sus variables no actúan de manera aislada. En el caso de la calidad del aire, tratar de explicar el comportamiento del ozono únicamente con una variable hubiera dejado fuera gran parte del problema, porque su concentración cambia junto con la temperatura, la radiación solar, la humedad, el viento, la estación de monitoreo y su propio comportamiento en horas o días anteriores. Para mí, el valor del modelo estuvo en poder organizar toda esa información y encontrar qué relaciones realmente aportaban algo para comprender y anticipar el comportamiento del O3.

### 2. Evidencia

Un resultado que me ayudó a entender esto fue el análisis de componentes principales. Al trabajar con O3, su valor rezagado 24 horas y variables meteorológicas, se necesitaron cinco componentes para superar el 80 % de la varianza acumulada. El primer componente estuvo relacionado principalmente con el O3 actual, el O3 de 24 horas antes, la temperatura y la radiación solar, mientras que la humedad tuvo un comportamiento contrario. El segundo componente estuvo dominado por las componentes del viento. Esto mostró que había grupos de variables que compartían información y que el comportamiento del ozono estaba relacionado con más de un tipo de condición ambiental.

La parte predictiva también fue una evidencia importante. En la muestra común de 2025, la persistencia diaria tuvo un MAE de 14.144 y un RMSE de 19.561. El modelo GAM redujo estos errores a 12.270 y 16.620, mientras que XGBoost obtuvo 12.110 y 16.579. La diferencia entre GAM y XGBoost fue pequeña, pero ambos mejoraron claramente la referencia de persistencia. Además, XGBoost pudo trabajar con una mayor cantidad de observaciones debido a que tolera valores faltantes en los predictores, mientras que el GAM necesitó casos completos.

### 3. Justificación

Estos resultados respaldan mi idea porque muestran que combinar distintas variables sí agregó información que no estaba presente al observar solamente el valor anterior de O3. La persistencia era una referencia bastante razonable, ya que el análisis temporal mostró una relación fuerte con el valor de la misma hora del día anterior. Aun así, los modelos lograron reducir el error cuando agregaron información meteorológica, temporal y espacial. Esto me hizo ver que un modelo multivariado no sirve solamente para producir una predicción final, sino también para entender qué partes del fenómeno contienen información útil y cómo se relacionan entre ellas.

También entendí que el proceso previo al modelo puede cambiar completamente las conclusiones. Por ejemplo, al inicio teníamos datos desde 2020, pero después descubrimos que en ese año faltaba más del 93 % de las mediciones de O3 en todas las estaciones analizadas, llegando prácticamente al 100 % en algunas. Incluir ese año solamente porque estaba disponible hubiera dado una falsa sensación de tener más información. Finalmente se decidió trabajar con 2021-2025. Para mí, esta fue una de las partes más importantes del reto porque dejó claro que un modelo no puede compensar una base de datos mal entendida o de mala calidad.

### 4. Respaldo

Lo que observamos también tiene sentido desde los conceptos vistos en el curso. El PCA permitió reducir y resumir la información de varias variables correlacionadas sin analizar cada una de forma completamente separada. Por otro lado, el GAM permitió representar relaciones no lineales entre O3 y sus predictores, lo cual era más razonable que asumir que todos los efectos eran lineales. La validación temporal también fue fundamental. En lugar de dividir los datos aleatoriamente, se utilizó información de años anteriores para construir los modelos y se dejó 2025 como prueba final. Esto evitó que información del futuro se utilizara para predecir el pasado y permitió evaluar los modelos en una situación más parecida a su uso real.

### 5. Contraargumento o limitaciones

A pesar de los resultados, no considero que el modelo deba interpretarse como una explicación completa de la contaminación por ozono. Una relación estadística no demuestra causalidad y existen factores que no están representados completamente en la base. También hubo diferencias importantes en disponibilidad de datos entre estaciones y periodos. Otra limitación es que 2025 solamente contiene información hasta junio, por lo que la prueba final no representa un año completo. Además, un error promedio aceptable no garantiza que el modelo funcione igual de bien durante episodios extremos de O3, que probablemente son los momentos más importantes desde el punto de vista ambiental. Por estas razones, utilizar un modelo sin revisar su contexto, sus errores y la calidad de los datos puede llevar a conclusiones equivocadas.

### 6. Conclusión

Al terminar el reto, mi forma de ver el modelado multivariado cambió. Antes era fácil pensar que el objetivo principal era encontrar el modelo con el menor error, pero ahora considero que el proceso completo es igual de importante: entender los datos, justificar qué información se utiliza, comparar métodos y reconocer cuándo un resultado tiene limitaciones. En este proyecto, el modelado permitió identificar patrones entre O3, meteorología y temporalidad, además de construir predicciones mejores que una referencia sencilla. Para mí, el verdadero valor del análisis multivariado está en convertir muchas mediciones relacionadas en información que pueda interpretarse y utilizarse para tomar decisiones, sin perder de vista que el modelo es una aproximación del fenómeno y no el fenómeno mismo.

---

## Parte B. Autoevaluación personal — Modelo PER

### 1. Propósito

Considero que el propósito del reto era aprender a llevar un problema real desde una pregunta bastante abierta hasta un análisis que pudiera justificarse y evaluarse con datos. No se trataba únicamente de aplicar PCA, GAM u otra técnica porque apareciera en el curso, sino de decidir cuándo tenía sentido utilizarla. También estaban en juego habilidades de programación, interpretación, comunicación de resultados y trabajo en equipo. Una parte que considero especialmente importante fue aprender a diferenciar entre obtener un resultado y realmente entender qué significa dentro del problema de calidad del aire.

### 2. Estrategia

Nuestra estrategia cambió bastante conforme avanzó el reto. Al principio el objetivo era muy amplio y se consideraban distintos contaminantes y relaciones. Conforme exploramos los datos nos dimos cuenta de que era mejor plantear una pregunta más concreta, por lo que terminamos enfocándonos en predecir O3 con 24 horas de anticipación. También tuvimos que modificar decisiones después de encontrar problemas como la falta de datos de O3 en 2020 y las diferencias de disponibilidad entre variables.

En lo personal, algo que me funcionó fue no limitarme a ejecutar el código. Traté de entender qué representaba cada base intermedia, por qué se eliminaba o conservaba determinada información y qué significaban las tablas y gráficas antes de continuar. El uso de R y Quarto ayudó a mantener juntos el análisis y su explicación, mientras que GitHub fue importante para integrar el trabajo del equipo y conservar los cambios. Trabajar de esta manera también me mostró que en un proyecto largo es muy fácil perder claridad si el código y las decisiones no se documentan conforme se avanza.

### 3. Resultado

El primer aprendizaje importante que me llevo es que **los datos reales casi nunca están listos para modelarse**. En este reto hubo que homologar nombres, convertir tipos, revisar valores faltantes, detectar mediciones fuera de rango y analizar la disponibilidad por año y estación. Antes podía ver la limpieza como una etapa previa al análisis; ahora la considero parte del análisis, porque las decisiones tomadas ahí cambian directamente qué puede aprender el modelo.

El segundo aprendizaje es que **la validación importa tanto como el modelo**. Aprendí que en un problema temporal no sería correcto mezclar aleatoriamente observaciones del pasado y del futuro. Separar los años cronológicamente y dejar 2025 para la prueba final hizo que la evaluación fuera más exigente, pero también mucho más creíble.

El tercer aprendizaje es que **un modelo más complejo no necesariamente vuelve inútiles a los modelos más interpretables**. XGBoost obtuvo el menor error y una mejor cobertura, pero su ventaja frente al GAM fue pequeña. El GAM permitió entender mejor la forma de algunas relaciones y tuvo un desempeño muy parecido. Esto me ayudó a dejar de pensar en la selección de modelos como una competencia en la que solamente gana el menor número y a considerar también interpretabilidad, cobertura y utilidad práctica.

Todavía quiero fortalecer mi capacidad para interpretar modelos no lineales y series de tiempo con mayor profundidad. Puedo construir y evaluar este tipo de modelos, pero me interesa entender mejor sus supuestos, diagnosticar sus errores y justificar de manera más sólida por qué una especificación es preferible a otra. También considero que puedo mejorar la organización del código desde el inicio de un proyecto para reducir la necesidad de rehacer partes cuando el objetivo cambia. En general, el reto me ayudó a conectar mejor la teoría de análisis multivariado con un problema real y, sobre todo, a entender que llegar a una conclusión confiable requiere mucho más que simplemente ejecutar un método estadístico.

---

## Declaratoria de uso de IA durante el desarrollo del trabajo

**Opción B. Se utilizó IA.**

**Herramienta:** ChatGPT de OpenAI.

**Uso realizado:** apoyo para organizar ideas, revisar redacción, aclarar conceptos estadísticos y apoyar la revisión de código durante distintas etapas del reto.

**Secciones donde se utilizó:** apoyo en la estructuración y revisión de explicaciones, interpretaciones y código del proyecto, así como en la organización inicial de esta reflexión.

**Validación realizada por el estudiante:** el contenido, los resultados numéricos y las interpretaciones fueron revisados con base en los archivos, código y resultados obtenidos durante el reto. La versión final fue revisada por el estudiante, quien asume la responsabilidad del contenido entregado.
