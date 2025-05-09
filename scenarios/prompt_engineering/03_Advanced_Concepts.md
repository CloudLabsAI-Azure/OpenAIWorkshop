# Ejercicio 4B: Conceptos Avanzados (Solo Lectura)

### Duración estimada: 30 minutos

Este laboratorio proporciona conocimientos teóricos y prácticos avanzados sobre OpenAI y sus aplicaciones. Abarca la introducción a la ingeniería de promociones, sus casos de uso y los diversos tipos de indicaciones que se pueden implementar para obtener los resultados deseados.

## Temas

  - [Introducción](#introducción)
  - [Prompts Zero-Shot](#prompts-zero-shot)
  - [Prompts One-Shot](#prompts-one-shot)
  - [Prompts Few-Shot](#prompts-few-shot)

---

## Introducción

En este punto, ha experimentado el poder y la flexibilidad de los prompts. Ajustar los prompts para obtener los resultados deseados es la idea detrás de la ingeniería de prompts.

Ahora cubriremos algunos temas más avanzados para ajustar nuestras salidas sin introducir el ajuste fino de nuestros modelos GPT.

Tomemos un ejemplo de clasificación simple:

*Prompt:*
```
Clasifica el sentimiento del texto a continuación.

Texto: Creo que esta película fue terrible. Qué perdida de tiempo.
```

*Salida:*
```
Negativo
```

El resultado parece ser correcto, pero podríamos mejorarlo proporcionando más información al modelo si quisiéramos una clasificación más granular. Hagámoslo mediante un prompt Zero-Shot.

---

## Prompts Zero-Shot

Los LLMs de GPT están entrenados con cantidades tan grandes de datos que son capaces de comprender instrucciones complejas para obtener el resultado deseado en la mayoría de los casos. Esto se denomina Prompts 'Zero-Shot'.

Podríamos refinar el siguiente ejemplo siendo más descriptivos sobre nuestras instrucciones.

*Prompt:*
```
Clasifica el sentimiento del texto a continuación en muy negativo, negativo, neutral, positivo y muy positivo.

Texto: Creo que esta película fue terrible. Qué perdida de tiempo.
```

*Salida:*
```
Muy Negativo
```

Esto se conoce como Zero-Shot. Una instrucción precisa conduce al resultado deseado sin ningún ejemplo.

---

## Prompts One-Shot

En ocasiones puede ser más fácil proporcionar un ejemplo del modelo del cual aprender. Esto se denomina Prompt 'One-Shot'.

Primero, hagamos un prompt Zero Shot.

*Prompt:*
```
Dime en qué ciudad está ubicada una universidad.

Universidad: UCLA
```

*Salida:*
```
Ciudad: Los Angeles, California
```

Supongamos que desea tener un resultado específico para este mensaje. Podría proporcionar un ejemplo del modelo del cual aprender.

Aquí hay un Prompt One-Shot que conduce al mismo resultado.

*Prompt:*
```
Dime en qué ciudad está ubicada una universidad.

Universidad: UCLA
Ciudad: Los Angeles, CA, USA

Universidad: MIT
```

*Salida:*
```
Ciudad: Cambridge, MA, USA
```

Tenga en cuenta que también podría haber utilizado el prompt Zero-Shot para este ejemplo. Pero los prompts One-Shot son más flexibles y se pueden utilizar para ajustar el modelo a sus necesidades.

Aquí hay un Prompt Zero-Shot equivalente.

*Prompt:*
```
Dime en qué ciudad está ubicada una universidad. Proporciona el nombre de la ciudad, el código de estado y el país, separados por comas en una línea.

Universidad: UCLA
```

*Salida:*
```
Ciudad: Los Angeles, CA, USA
```

---

## Prompts Few-Shot

Los prompts Few-Shot le permiten proporcionar múltiples ejemplos del modelo del cual aprender. Esto es útil cuando desea ajustar la salida para escenarios más complejos donde la salida puede variar según la entrada. También puede ser una forma más sencilla de definir una tarea en lugar de proporcionar instrucciones detalladas en lenguaje natural de lo que se espera.

A continuación se muestra un ejemplo de extracción de entidades que se adapta muy bien a prompts Few-Shot.

Intentémoslo primero con un prompt Zero-Shot.

*Prompt:*
```
Genera un documento JSON que proporcione el nombre, el puesto y la empresa a partir del texto siguiente.

Texto: Fred es un emprendedor en serie. Cofundador y CEO de Platform.sh, anteriormente cofundó Commerce Guys, un proveedor líder de comercio electrónico de Drupal. Su misión es garantizar que, a medida que continuamos en un ambicioso viaje para transformar profundamente la forma en que se utiliza y se percibe la computación de la nube, mantengamos los pies bien puestos en el suelo, continuando con el rápido crecimiento del que hemos disfrutado hasta ahora.
```

*Salida:*
```
{
  "Nombre": "Fred",
  "Puesto": "Cofundador y CEO",
  "Empresa": "Platform.sh, Commerce Guys"
}
```

No es exactamente lo que esperábamos (solo 'Platform.sh' debería aparecer en 'Empresa'), y puede ser difícil expresarlo en un prompt Zero-Shot.

Probemos con un prompt Few-Shot. Note que dejaremos de lado las instrucciones y solo proporcionaremos el resultado deseado.

*Prompt:*
```
Texto: Fred es un emprendedor en serie. Cofundador y CEO de Platform.sh, anteriormente cofundó Commerce Guys, un proveedor líder de comercio electrónico de Drupal. Su misión es garantizar que, a medida que continuamos en un ambicioso viaje para transformar profundamente la forma en que se utiliza y se percibe la computación de la nube, mantengamos los pies bien puestos en el suelo, continuando con el rápido crecimiento del que hemos disfrutado hasta ahora.

JSON:
{
  "Nombre": "Fred",
  "Puesto": "Cofundador y CEO",
  "Empresa": "Platform.sh"
}

Texto: Microsoft (la palabra es un acrónimo de "microcomputer software") fue fundada por Bill Gates el 4 de Abril de 1975 para desarrollar y vender intérpretes de BASIC para la Altair 8800. Steve Ballmer sustituyó a Gates como CEO en el año 2000 y más tarde ideó una estrategia de "dispositivos y servicios".

JSON:
```

*Salida:*
```
{
  "Nombre": "Microsoft",
  "Fundador": "Bill Gates",
  "Fundada": "4 de Abril de 1975",
  "CEO": "Steve Ballmer",
  "Estrategia": "Dispositivos y Servicios"
}
```

Observe que el resultado mostrado no es lo que esperábamos, pero no ha habido suficientes ejemplos para comprender si el objetivo es extraer entidades clave o solo ciertas entidades.

Un prompt Few-Shot aclarará esto.

*Prompt:*
```
Texto: Fred es un emprendedor en serie. Cofundador y CEO de Platform.sh, anteriormente cofundó Commerce Guys, un proveedor líder de comercio electrónico de Drupal. Su misión es garantizar que, a medida que continuamos en un ambicioso viaje para transformar profundamente la forma en que se utiliza y se percibe la computación de la nube, mantengamos los pies bien puestos en el suelo, continuando con el rápido crecimiento del que hemos disfrutado hasta ahora.

JSON:
{
  "Nombre": "Fred",
  "Puesto": "Cofundador y CEO",
  "Empresa": "Platform.sh"
}

Texto: Microsoft (la palabra es un acrónimo de "microcomputer software") fue fundada por Bill Gates el 4 de Abril de 1975 para desarrollar y vender intérpretes de BASIC para la Altair 8800. Steve Ballmer sustituyó a Gates como CEO en el año 2000 y más tarde ideó una estrategia de "dispositivos y servicios".

JSON:
{
  "Nombre": "Bill Gates",
  "Puesto": "Cofundador y CEO",
  "Empresa": "Microsoft"
}

Texto: Franck Riboud nació el 7 de Noviembre de 1955 en Lyon. Es hijo de Antoine Riboud, el anterior CEO, que transformó el antiguo fabricante de vidrio europeo BSN Group en una empresa líder de la industria alimentaria. Él es el CEO de Danone.

JSON:
```

*Salida:*
```
{
  "Nombre": "Franck Riboud",
  "Puesto": "CEO",
  "Empresa": "Danone"
}
```
Ahora podemos ver que el modelo entiende claramente que solo queremos extraer tres entidades del texto y nada más.


## Resumen

En este laboratorio, adquirirá conocimientos teóricos profundos y prácticos avanzados sobre OpenAI y diversos tipos de métodos de ingeniería rápida.