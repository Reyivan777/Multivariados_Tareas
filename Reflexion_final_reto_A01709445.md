# Reflexión final del reto

Rey Iván de la Fuente Chávez — A01709445

## Parte A. Reflexión argumentada

### 1. Afirmación

Después de realizar el reto, considero que la principal utilidad del modelado multivariado es que permite estudiar un problema real considerando varias variables al mismo tiempo. En el caso de la calidad del aire, explicar el comportamiento del ozono usando una sola variable hubiera dejado fuera una parte importante del problema, ya que su concentración cambia junto con la temperatura, la radiación solar, la humedad, el viento, la estación de monitoreo y también con su comportamiento de horas o días anteriores. Para mí, el valor del modelo estuvo en juntar toda esa información y encontrar qué relaciones realmente ayudan a entender y anticipar el comportamiento del O3.

### 2. Evidencia

Un resultado que me ayudó a entender esto fue el análisis de componentes principales. Al trabajar con O3, su valor rezagado 24 horas y variables meteorológicas, se necesitaron cinco componentes para superar el 80 % de la varianza acumulada. El primer componente estuvo relacionado principalmente con el O3 actual, el O3 de 24 horas antes, la temperatura y la radiación solar, mientras que la humedad se comportó en sentido contrario. El segundo componente estuvo más relacionado con las componentes del viento. Esto mostró que había grupos de variables que compartían información y que el comportamiento del ozono estaba relacionado con diferentes condiciones ambientales.

La parte predictiva también fue importante. En la muestra común de 2025, la persistencia diaria tuvo un MAE de 14.144 y un RMSE de 19.561. El modelo GAM redujo estos errores a 12.270 y 16.620, mientras que XGBoost obtuvo 12.110 y 16.579. La diferencia entre GAM y XGBoost fue pequeña, pero los dos mejoraron la referencia de persistencia. Además, XGBoost pudo trabajar con más observaciones porque tolera valores faltantes en los predictores, mientras que el GAM necesitó casos completos.

### 3. Justificación

Estos resultados respaldan mi idea porque muestran que agregar diferentes variables sí dio información que no estaba presente al observar solamente el valor anterior de O3. La persistencia era una referencia bastante razonable porque el análisis temporal mostró una relación fuerte con el valor de la misma hora del día anterior. Aun así, los modelos lograron reducir el error cuando se agregó información meteorológica, temporal y de la estación. Esto me hizo ver que un modelo multivariado no sirve únicamente para dar una predicción final, sino también para entender qué partes del problema contienen información útil y cómo se relacionan entre ellas.

También entendí que lo que se hace antes de construir el modelo puede cambiar mucho los resultados. Al inicio teníamos datos desde 2020, pero después encontramos que en ese año faltaba más del 93 % de las mediciones de O3 en todas las estaciones analizadas y en algunas prácticamente no había datos. Incluir ese año solo porque estaba disponible hubiera dado una idea equivocada de que teníamos más información de la que realmente podía usarse. Al final se decidió trabajar con 2021-2025. Esta fue una de las partes que más me ayudó a entender que un buen modelo no puede arreglar una base de datos que no se conoce bien.

### 4. Respaldo

Lo que observamos también se puede relacionar con varios conceptos vistos en el curso. El PCA permitió resumir la información de varias variables relacionadas entre sí sin analizarlas completamente por separado. Por otro lado, el GAM permitió representar relaciones que no tenían que ser necesariamente lineales, algo que tenía más sentido para un fenómeno como la calidad del aire. La validación temporal también fue muy importante. En lugar de dividir los datos al azar, se usaron años anteriores para construir los modelos y se dejó 2025 como prueba final. De esta manera se evitó utilizar información futura para predecir el pasado y la evaluación fue más parecida a una situación real.

### 5. Contraargumento o limitaciones

A pesar de los resultados, no creo que el modelo pueda tomarse como una explicación completa de la contaminación por ozono. Una relación estadística no significa que una variable sea necesariamente la causa de otra y también existen factores que no estaban incluidos completamente en la base. Además, hubo diferencias importantes en la disponibilidad de datos entre estaciones y periodos. Otra limitación es que 2025 solamente tiene información hasta junio, así que la prueba final no representa un año completo. También puede pasar que un modelo tenga un error promedio razonable, pero falle justo en algunos episodios de O3 alto, que son de los momentos más importantes desde el punto de vista ambiental. Por eso considero que siempre se deben revisar los errores, el contexto y la calidad de los datos antes de confiar demasiado en una predicción.

### 6. Conclusión

Al terminar el reto, mi forma de ver el modelado multivariado cambió. Antes era fácil pensar que lo más importante era encontrar el modelo con el menor error, pero ahora veo que todo el proceso también importa: entender los datos, decidir qué información usar, comparar métodos y reconocer las limitaciones. En este proyecto, el modelado permitió encontrar patrones entre O3, meteorología y tiempo, además de construir predicciones mejores que una referencia sencilla. Para mí, el valor del análisis multivariado está en convertir muchas mediciones relacionadas en información que se pueda entender y usar, teniendo claro que un modelo siempre es una aproximación y no una representación perfecta de lo que pasa en la realidad.

---

## Parte B. Autoevaluación personal — Modelo PER

### 1. Propósito

Considero que el propósito del reto era aprender a llevar un problema real desde una pregunta bastante abierta hasta un análisis que se pudiera justificar y evaluar con datos. No se trataba solamente de aplicar PCA, GAM u otra técnica porque la vimos en clase, sino de entender cuándo tenía sentido usarla y qué información daba. También se trabajaron habilidades de programación, interpretación, comunicación de resultados y trabajo en equipo. Para mí, una de las partes más importantes fue aprender a diferenciar entre simplemente obtener un resultado y realmente entender qué significa dentro del problema de calidad del aire.

### 2. Estrategia

Nuestra estrategia cambió bastante conforme avanzó el reto. Al principio el objetivo era muy amplio y se consideraban varios contaminantes y relaciones. Conforme exploramos los datos nos dimos cuenta de que era mejor plantear una pregunta más concreta, así que terminamos enfocándonos en predecir O3 con 24 horas de anticipación. También tuvimos que cambiar algunas decisiones después de encontrar problemas como la falta de datos de O3 en 2020 y las diferencias de disponibilidad entre variables.

En lo personal, algo que me ayudó fue tratar de no quedarme solamente con ejecutar el código. Intenté entender qué representaba cada base que íbamos creando, por qué se eliminaba o conservaba cierta información y qué significaban las tablas y gráficas antes de seguir. R y Quarto ayudaron a mantener el análisis junto con su explicación, mientras que GitHub fue útil para integrar el trabajo del equipo y guardar los cambios. También aprendí que en un proyecto largo es fácil perderse si no se mantiene cierto orden en el código y en las decisiones que se van tomando.

### 3. Resultado

El primer aprendizaje importante que me llevo es que los datos reales casi nunca están listos para usarse directamente en un modelo. En este reto hubo que homologar nombres, convertir tipos, revisar valores faltantes, detectar mediciones fuera de rango y analizar la disponibilidad por año y estación. Antes veía la limpieza como una etapa previa al análisis; ahora entiendo que también forma parte del análisis porque las decisiones tomadas ahí cambian directamente lo que el modelo puede aprender.

El segundo aprendizaje es que la validación importa tanto como el modelo. Aprendí que en un problema temporal no sería correcto mezclar al azar observaciones del pasado y del futuro. Separar los años cronológicamente y dejar 2025 para la prueba final hizo que la evaluación fuera más exigente, pero también más confiable.

El tercer aprendizaje es que un modelo más complejo no necesariamente hace que los modelos más interpretables dejen de ser útiles. XGBoost obtuvo el menor error y una mejor cobertura, pero la diferencia con el GAM fue pequeña. El GAM permitió entender mejor la forma de algunas relaciones y tuvo un desempeño muy parecido. Esto me ayudó a dejar de pensar en la selección de modelos como si solamente ganara el que tiene el número más bajo y a considerar también la interpretación, la cantidad de datos que puede usar y la utilidad práctica.

Todavía quiero mejorar mi capacidad para interpretar modelos no lineales y series de tiempo con mayor profundidad. Puedo construir y evaluar este tipo de modelos, pero todavía quiero entender mejor sus supuestos, diagnosticar sus errores y justificar mejor por qué una opción puede ser preferible a otra. También creo que puedo mejorar la organización del código desde el inicio para no tener que rehacer tantas partes cuando cambia el objetivo. En general, el reto me ayudó a conectar mejor la teoría del análisis multivariado con un problema real y a entender que llegar a una conclusión confiable requiere mucho más que simplemente correr un método estadístico.

---

## Declaratoria de uso de IA durante el desarrollo del trabajo

Opción B. Se utilizó IA.

Herramienta: ChatGPT de OpenAI.

Uso realizado: apoyo para organizar ideas, revisar redacción, aclarar conceptos estadísticos y apoyar la revisión de código durante distintas etapas del reto.

Secciones donde se utilizó: apoyo en la estructuración y revisión de explicaciones, interpretaciones y código del proyecto, así como en la organización inicial de esta reflexión.

Validación realizada por el estudiante: el contenido, los resultados numéricos y las interpretaciones fueron revisados con base en los archivos, código y resultados obtenidos durante el reto. La versión final fue revisada por el estudiante, quien asume la responsabilidad del contenido entregado.
