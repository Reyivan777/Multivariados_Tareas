# Reflexión final del reto — guía para redactar mi versión personal

> **Importante:** este archivo es una guía de trabajo. La evidencia pide que la reflexión sea personal y señala que se revisará su autenticidad. Por eso, antes de entregar, debo convertir estas ideas en mis propias palabras, agregar lo que realmente pensé o aprendí y eliminar todo lo que no represente mi experiencia.

## Datos concretos de mi proyecto que puedo usar como evidencia

- El proyecto terminó enfocado en **predecir la concentración horaria de O3 con hasta 24 horas de anticipación**, para horas objetivo entre **10:00 y 20:00**, usando las estaciones **NTE, NTE2, NO y NE**.
- La base integrada tuvo **192,723 registros**. En O3 se identificaron **46,839 valores faltantes (24.30 %)**, por lo que la calidad y disponibilidad de los datos influyeron directamente en las decisiones de modelado.
- No se encontraron registros duplicados para una misma combinación de estación y fecha-hora.
- La dirección del viento no se trató como una variable lineal común; se representó mediante componentes seno y coseno para respetar su naturaleza circular.
- La evaluación final respetó el orden temporal: se utilizaron periodos anteriores para entrenamiento/validación y **2025 como prueba final**, evitando mezclar aleatoriamente pasado y futuro.
- La comparación final consideró un **GAM Gamma** y **XGBoost**, además de una referencia de **persistencia diaria**. Para comparar GAM y XGBoost de forma justa se planteó una muestra común de evaluación.
- El proyecto cambió bastante desde la idea inicial de estudiar muchos contaminantes al mismo tiempo hasta una pregunta más concreta y medible centrada en O3.

---

# Parte A. Reflexión argumentada

## 1. Afirmación

### Idea que quiero defender

La utilidad principal del modelado multivariado no fue solamente obtener una predicción, sino **entender un fenómeno en el que varias variables cambian al mismo tiempo y determinar cuáles aportan información útil para anticipar el comportamiento del O3**.

### Escribir con mis palabras

Completar en 3–4 oraciones:

- Antes del reto yo veía un modelo principalmente como: ________.
- Después de trabajar con datos reales de calidad del aire entendí que: ________.
- Para mí, la mayor utilidad de un modelo multivariado en este problema fue: ________.

## 2. Evidencia

Puedo usar uno o dos ejemplos concretos, no necesito contar todo el proyecto.

### Evidencia posible A: los datos faltantes cambiaron el análisis

El O3 tenía 24.30 % de valores faltantes en la base integrada. Esto obligó a revisar **dónde** faltaban las mediciones y no solamente a observar un porcentaje global. La disponibilidad de los datos terminó afectando los periodos que podían utilizarse para entrenar y evaluar.

**Mi interpretación personal:** ¿qué me sorprendió de esto?, ¿yo esperaba que limpiar la base fuera tan importante?, ¿qué decisión tuvimos que cambiar por este problema?

Escribir 3–5 oraciones: ________

### Evidencia posible B: comparar modelos y no quedarse con uno

En la etapa final se compararon GAM Gamma y XGBoost, además de una referencia de persistencia. La comparación se hizo sobre 2025 y también sobre una muestra común para que las diferencias no fueran consecuencia de evaluar cada modelo con observaciones distintas.

**Mi interpretación personal:** ¿qué aprendí al comparar un modelo más interpretable con uno más flexible?, ¿qué significa para mí que un modelo deba superar una referencia sencilla antes de considerarlo útil?

Escribir 3–5 oraciones: ________

### Evidencia posible C: la estructura temporal sí importa

El proyecto no podía dividirse como una base cualquiera de forma aleatoria, porque utilizar información futura para predecir el pasado produciría fuga de información. Por eso se respetó el orden cronológico y 2025 quedó como prueba final.

**Mi interpretación personal:** explicar por qué esto cambió mi forma de pensar sobre la validación de modelos: ________

## 3. Justificación

Aquí debo explicar **por qué la evidencia anterior apoya mi afirmación**, no repetir los resultados.

Ideas que puedo desarrollar:

- Una relación entre O3 y una sola variable puede ser engañosa si se ignoran temperatura, radiación, humedad, viento, estación y comportamiento temporal.
- Trabajar varias variables conjuntamente permite encontrar patrones que no se observan al revisar columnas por separado.
- En datos reales, el proceso de seleccionar variables, preparar rezagos y validar cronológicamente forma parte del modelo; no es solamente una etapa previa sin importancia.

Completar con mi razonamiento:

> Lo que esta evidencia me permitió entender y que no era tan evidente antes de modelar fue que ________. Al considerar las variables de manera conjunta, pude ver que ________. Esto es importante porque ________.

## 4. Respaldo conceptual o metodológico

No necesito llenar esta parte de teoría. Puedo relacionar lo que pasó con algunos conceptos vistos en el curso:

- **Relaciones entre variables:** el O3 no depende de una única medición aislada; su comportamiento se estudia junto con variables meteorológicas, contaminantes y temporales.
- **No linealidad:** un GAM permite modelar relaciones que no tienen que seguir una línea recta.
- **Validación:** separar entrenamiento, validación y prueba permite evaluar el comportamiento del modelo con datos que no utilizó para ajustarse.
- **Comparación contra una referencia:** la persistencia diaria sirve para comprobar si un modelo más elaborado realmente aporta algo.
- **Reducción o síntesis de información:** si en el reporte final se conserva PCA, puedo explicar cómo ayuda a resumir variables correlacionadas sin analizar cada una de manera aislada.

Escribir un párrafo corto conectando **solo dos o tres** de estos conceptos con mi experiencia: ________

## 5. Contraargumento o limitaciones

Esta parte no debe sonar como si el modelo resolviera todo. Algunas limitaciones reales del reto fueron:

- hubo faltantes importantes en varias variables;
- las estaciones tienen comportamientos y disponibilidades distintas;
- un buen error promedio no significa que el modelo prediga correctamente todos los episodios altos de O3;
- encontrar asociación entre variables no demuestra causalidad;
- el modelo depende del periodo, estaciones y variables con los que fue construido;
- un modelo más complejo puede mejorar predicción, pero ser más difícil de interpretar.

### Preguntas para escribir mi párrafo

¿Qué podría pasar si alguien usara el modelo sin revisar sus errores? ¿En qué situaciones no confiaría completamente en la predicción? ¿Qué información externa no estaba incluida en nuestra base y podría influir en el O3?

Mi párrafo: ________

## 6. Conclusión

Evitar repetir todo. Cerrar con lo que realmente cambió en mi forma de entender el análisis de datos.

Posible estructura:

> Al terminar el reto, mi idea sobre el modelado multivariado cambió porque ________. Más que obtener una ecuación o una métrica, aprendí que ________. En un problema ambiental como este, considero que el verdadero valor del modelo está en ________, siempre que ________.

---

# Parte B. Autoevaluación personal — Modelo PER

## 1. Propósito

### Lo que probablemente buscaba desarrollar el reto

No solamente aplicar fórmulas, sino aprender a convertir un problema real en una pregunta que pudiera analizarse con datos, preparar una base imperfecta, escoger técnicas adecuadas, validar resultados y explicar qué significan dentro del contexto de calidad del aire.

### Lo que debo agregar de manera personal

- ¿Qué habilidad siento que más se me exigió: programar, interpretar, investigar, trabajar con el equipo, tomar decisiones?
- ¿Qué parte del reto me costó más al principio?
- ¿Qué concepto del curso ahora entiendo mejor porque lo tuve que aplicar?

Mi párrafo: ________

## 2. Estrategia

### Cambios reales que puedo mencionar

El proyecto comenzó con un objetivo demasiado amplio. Conforme se exploraron los datos, el equipo fue delimitando la pregunta hasta centrarse en la predicción de O3. También fue necesario cambiar decisiones después de revisar faltantes, estructura temporal y disponibilidad por año y estación. El trabajo se apoyó en R, Quarto y GitHub para mantener el análisis reproducible y poder integrar las aportaciones del equipo.

### Para volverlo realmente mío

Responder antes de redactar:

- ¿Qué parte hice yo directamente?
- ¿En qué momento tuve que rehacer algo porque el primer enfoque no funcionó?
- ¿Cómo nos repartimos el trabajo?
- ¿Qué aprendí usando GitHub que antes no sabía hacer bien?
- ¿Hubo alguna decisión del equipo con la que inicialmente no estaba de acuerdo o que después entendí mejor?

Mi párrafo: ________

## 3. Resultado

Debo mencionar al menos tres aprendizajes significativos. Puedo usar estos como punto de partida, pero necesito describirlos desde mi experiencia.

### Aprendizaje 1 — Los datos reales no llegan listos

Idea: una parte grande del trabajo fue homologar nombres, convertir tipos, revisar valores inválidos y faltantes antes de poder modelar.

Lo que yo aprendí de esto: ________

### Aprendizaje 2 — Validar bien importa tanto como ajustar el modelo

Idea: en una serie temporal no es correcto mezclar aleatoriamente pasado y futuro. La forma de separar los datos puede hacer que una evaluación parezca mejor de lo que realmente es.

Lo que yo aprendí de esto: ________

### Aprendizaje 3 — El modelo más complejo no necesariamente es el más útil

Idea: comparar GAM, XGBoost y persistencia obliga a pensar no solo en el error, sino también en interpretabilidad, cobertura, facilidad de uso y comportamiento por estación.

Lo que yo aprendí de esto: ________

### Algo que todavía necesito fortalecer

Elegir algo específico y creíble, por ejemplo:

- interpretar con mayor profundidad modelos no lineales;
- justificar mejor la selección de variables;
- trabajar con series de tiempo y validación temporal;
- entender mejor los supuestos estadísticos;
- organizar mejor el código desde el inicio para evitar rehacer partes después.

Lo que quiero seguir fortaleciendo y por qué: ________

---

# Revisión final antes de entregar

Antes de convertir esto en mi reflexión final debo asegurarme de que:

- [ ] La Parte A tenga aproximadamente una página.
- [ ] La Parte B tenga entre media página y una página.
- [ ] No describa el código paso por paso.
- [ ] Incluya al menos un resultado o decisión concreta del reto.
- [ ] Explique qué entendí gracias a ese resultado.
- [ ] Incluya limitaciones y no presente el modelo como una verdad absoluta.
- [ ] En la Parte B aparezcan al menos tres aprendizajes reales.
- [ ] Mencione mi participación personal y no solamente lo que hizo “el equipo”.
- [ ] Reescriba todo con expresiones que yo usaría normalmente.
- [ ] Elimine cualquier idea que no represente lo que realmente hice o aprendí.
