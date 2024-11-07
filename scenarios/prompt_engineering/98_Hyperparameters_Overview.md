# Ejercicio 4D: Descripción Básica de los Hiperparámetros de Azure OpenAI Service (Solo Lectura)
## Nota Rápida sobre el ajuste de Hiperparámetros

Cuando trabaje con prompts, interactuará con el LLM directamente o a través de una API. Puede configurar algunos parámetros para obtener resultados diferentes para sus prompts.

**temperature** - En pocas palabras, cuanto más baja es la temperatura, más deterministas son los resultados, en el sentido de que siempre se elige el siguiente token más probable. Incrementar la temperatura podría generar más aleatoriedad, fomentando resultados más diversos o creativos. Básicamente, estamos aumentando los pesos de los otros tokens posibles. En términos de aplicación, es posible que deseemos utilizar una temperatura más baja para algo como el control de calidad basado en hechos para fomentar respuestas más objetivas y concisas. Para la generación de poemas u otras tareas creativas, puede resultar beneficioso aumentar la temperatura.

**top_p** - De manera similar, con top_p, una técnica de muestreo con temperatura llamada muestreo de núcleo, puede controlar qué tan determinista es el modelo al generar una respuesta. Si está buscando respuestas exactas y objetivas, manténgalo en un valor bajo. Si busca respuestas más diversas, auméntelo a un valor más alto.

La recomendación general es modificar uno, no ambos parámetros a la vez.

### Modelo gpt-35-turbo-instruct

**temperature**
```
Controla la aleatoriedad: Reducirla da como resultado finalizaciones menos aleatorias.
A medida que la temperatura se acerque a cero, el modelo se volverá determinista y repetitivo.
```

**max_tokens**
```
Establece un límite en la cantidad de tokens que se generarán en una respuesta.
El sistema admite un máximo de 2048 tokens compartidos entre un prompt determinado y la respuesta de finalización.
(Un token equivale aproximadamente a 4 caracteres para un texto típico en idioma Inglés).
```

**top_p**
```
Controla qué tokens considerará el modelo al generar una respuesta mediante muestreo de núcleos.
Establecerlo en 0.9 considerará el 90% más probable de todos los tokens posibles.
Esto evitará el uso de tokens que sean incorrectos y al mismo tiempo mantendrá la variedad 
cuando el modelo tiene poca confianza en los tokens con mayor puntuación.
```

**frequency_penalty**
```
Reduce la posibilidad de repetir un token proporcionalmente según la frecuencia con la que ha aparecido en el texto hasta el momento.
Esto disminuye la probabilidad de repetir el mismo texto en una respuesta.
```

**presence_penalty**
```
Reduce la posibilidad de repetir cualquier token que haya aparecido en el texto hasta ahora.
Esto aumenta la probabilidad de introducir nuevos temas en una respuesta.
```

**best_of**
```
Genera múltiples respuestas y muestra solo la que tenga la mejor probabilidad total entre todos sus tokens.
Los candidatos no utilizados seguirán incurriendo en costos de uso, así que use este parámetro con cuidado y asegúrese también de configurar los
parámetros de la longitud máxima de la respuesta y los triggers de finalización. Tenga en cuenta que la función de streaming solo funcionará cuando esté configurado en 1.
```

**stop**
```
Hace que las respuestas se detengan en un punto deseado, como el final de una oración o lista.
Especifique hasta cuatro secuencias en las que el modelo dejará de generar más tokens
en una respuesta. El texto devuelto no contendrá la secuencia de detención.
```
