# Ejercicio 4C: Ajuste fino (Solo lectura)

### Duración estimada: 15 minutos

Este laboratorio se centra en el proceso de ajuste fino de los modelos de OpenAI para mejorar su rendimiento en tareas o conjuntos de datos específicos. Los participantes aprenden a ajustar los parámetros del modelo, optimizar las estrategias de entrenamiento y evaluar las métricas de rendimiento del modelo mediante ejercicios prácticos y ejemplos.

## Temas

  - [¿Qué es el Ajuste Fino?](#qué-es-el-ajuste-fino)
  - [¿Cuándo consideraría Ajuste Fino frente a la Ingeniería de Prompts?](#cuándo-consideraría-ajuste-fino-frente-a-la-ingeniería-de-prompts)
  - [Consideraciones de Costos de Operación](#consideraciones-de-costos-de-operación)

---
## Qué es el Ajuste Fino

El ajuste fino (fine-tuning) es el proceso de personalizar un modelo de IA existente para una tarea o dominio específico mediante el uso de datos adicionales. OpenAI ofrece ajuste fino para sus modelos de lenguaje, tales como GPT-3, el cual puede generar textos en lenguaje natural para diversos fines.

El ajuste fino permite a los usuarios crear modelos personalizados que pueden producir resultados más precisos y relevantes que los modelos generales.

Para ajustar un modelo OpenAI, los usuarios deben preparar sus propios datos de entrenamiento y validación, seleccionar un modelo base y usar la CLI de OpenAI u OpenAI Studio para comenzar con la tarea de ajuste.

El ajuste fino puede mejorar el rendimiento y reducir significativamente las tasas de error de los modelos OpenAI.

---
## Datos de Entrenamiento en Ajuste Fino

Los datos de entrenamiento para ajustar los modelos OpenAI son pares de mensajes de entrada y resultados deseados que reflejan la tarea o dominio específico para el que desea personalizar el modelo. Por ejemplo, si desea ajustar un modelo para generar reseñas de productos, sus datos de entrenamiento podrían verse así:

```
{"prompt": "Reseña: Compré esta computadora portátil para mis clases en línea y funciona muy bien.", "completion": "Calificación: 5 estrellas"}
{"prompt": "Reseña: La duración de la batería es terrible y la pantalla es demasiado pequeña.", "completion": "Calificación: 2 estrellas"}
{"prompt": "Reseña: Esto es una estafa. El producto nunca llegó y el vendedor no respondió.", "completion": "Calificación: 1 estrella"}
```

Puede utilizar la CLI de OpenAI CLI u OpenAI Studio para preparar, validar y formatear sus datos de entrenamiento en un archivo JSON que se puede utilizar para ajustar un modelo.

**NOTA IMPORTANTE**:
Es importante tener en cuenta que para esperar mejores resultados que utilizar ingeniería de prompts, necesitará tener un conjunto de datos grande y de alta calidad que sea relevante para su tarea o dominio, generalmente unos cientos de ejemplos de alta calidad.

---
## Cuándo consideraría Ajuste Fino frente a la Ingeniería de Prompts

El ajuste fino es una herramienta poderosa que se puede utilizar para personalizar modelos OpenAI para tareas o dominios específicos. Sin embargo, no siempre es necesario ajustar un modelo para obtener los resultados deseados.

El ajuste fino y la ingeniería de prompts son dos métodos para condicionar a los modelos de lenguaje para realizar tareas de dominio específico.

El ajuste fino implica volver a entrenar un modelo existente con nuevos datos, mientras que la ingeniería de prompts implica diseñar y probar instrucciones de entrada que obtengan el resultado deseado de un modelo.

### Ajuste Fino

Podría considerar ajustar un modelo cuando tenga un conjunto de datos grande y de alta calidad que sea relevante para su tarea o dominio y desee crear un modelo personalizado que pueda producir resultados más precisos y consistentes que el modelo general.

### Ingeniería de Prompts

Podría considerar la ingeniería de prompts cuando tenga un conjunto de datos limitado o nulo y desee aprovechar el conocimiento y las capacidades existentes de un modelo general haciendo las preguntas correctas o proporcionando el contexto adecuado.

**NOTA IMPORTANTE**: Ambos métodos requieren algo de prueba y error, pero el ajuste fino generalmente requiere más tiempo y recursos que la ingeniería de prompts, y no siempre es necesario ajustar un modelo para obtener los resultados deseados. Por lo tanto, es preferible comenzar con una ingeniería de prompts y únicamente considerar el ajuste de un modelo si no puede obtener los resultados deseados.

---

## Consideraciones de Costos de Operación

La Ingeniería de Prompts podría ser menos rentable si necesita proporcionar una gran cantidad de instrucciones para lograr algo similar a lo que obtendría con un Modelo Ajustado, ya que consumiría tokens con cada solicitud enviada.

Alojar un Modelo Ajustado también tiene su costo, pero en volúmenes medianos a altos, ese costo sería prácticamente irrelevante, por lo que la eficiencia de costos operativos podría ser un factor impulsor de Ajuste Fino.

---
## Referencias

[Ajuste Fino de OpenAI](https://platform.openai.com/docs/guides/fine-tuning)

[Ajuste Fino en Azure OpenAI Service](https://learn.microsoft.com/en-us/azure/cognitive-services/openai/how-to/fine-tuning?pivots=programming-language-studio)

## Resumen

En este laboratorio, adquirió conocimientos sobre diversos temas: qué es exactamente el ajuste fino, las diferencias entre el ajuste fino y la ingeniería de señales, y los costos operativos que deben considerarse.