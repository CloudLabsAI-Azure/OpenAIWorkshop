# Exercício 4B: Conceitos Avançados (Somente Leitura)

### Duração estimada: 30 minutos

Este laboratório oferece conhecimento teórico aprofundado e conhecimento prático avançado relacionado ao OpenAI e suas aplicações. Abrange a introdução à engenharia de promoção, seus casos de uso e vários tipos de prompts que podem ser implementados para alcançar os resultados desejados.

## Tópicos

  - [Introdução](#introduction)
  - [Zero-Shot Prompts](#zero-shot-prompts)
  - [One-Shot Prompts](#one-shot-prompts)
  - [Few-Shot Prompts](#few-shot-prompts)

---

## Introdução

Neste ponto, você já experimentou o poder e a flexibilidade dos prompts. Ajustar prompts para obter os resultados desejados é a ideia por trás da engenharia de prompts.

Agora, abordaremos alguns tópicos mais avançados para ajustar nossas saídas sem introduzir o ajuste fino de nossos modelos GPT.

Vejamos um exemplo simples de classificação:

*Prompt:*
```
Classify the sentiment of the text below.

Text: I think this movie was terrible. What a waste of time.
```

*Output:*
```
Negative
```

A saída parece estar correta, mas poderíamos melhorá-la fornecendo mais informações ao modelo se quiséssemos uma classificação mais granular. Vamos fazer isso por meio de um prompt de Zero-Shot.

---

## Prompts de Tiro Zero

Os LLMs do GPT são treinados com quantidades de dados tão grandes que, na maioria dos casos, são capazes de compreender instruções complexas para levar à saída desejada. Isso é chamado de prompt de Tiro Zero.

Poderíamos refinar o exemplo abaixo sendo mais descritivos sobre nossas instruções.

*Prompt:*
```
Classify the sentiment of the text below into very negative, negative, neutral, positive, and very positive.

Text: I think this movie was terrible. What a waste of time.
```

*Output:*
```
Very Negative
```

Isso se chama Zero-Shot. Uma instrução precisa leva à saída desejada sem nenhum exemplo.

---

## Prompts de Uma Disparada

Às vezes, pode ser mais fácil fornecer um exemplo do modelo para aprender. Isso é chamado de prompt de "Uma Disparada".

Primeiro, vamos fazer um prompt de Disparada Zero.

*Prompt:*
```
Tell me in which city a university is located.

University: UCLA
```

*Output:*
```
City: Los Angeles, California
```

Digamos que você queira ter uma saída específica para este prompt. Você pode fornecer um exemplo do modelo para aprender.

Aqui está um Prompt Único que leva à mesma saída.

*Prompt:*
```
Tell me in which city a university is located.

University: UCLA
City: Los Angeles, CA, USA

University: MIT
```

*Output:*
```
City: Cambridge, MA, USA
```

Observe que você também poderia ter usado o prompt Zero-Shot para este exemplo. Mas os prompts One-Shot são mais flexíveis e podem ser usados para ajustar o modelo às suas necessidades.

Aqui está um equivalente de prompt Zero-Shot.

*Prompt:*
```
Tell me in which city a university is located. Provide the city name, state code and country, comma separated as one line.

University: UCLA
```

*Output:*
```
City: Los Angeles, CA, USA
```

---

## Prompts de Poucas Tentativas

Os prompts de poucas tentativas permitem que você forneça vários exemplos do modelo para aprendizado. Isso é útil quando você deseja ajustar a saída para cenários mais complexos, onde a saída pode variar com base na entrada. Também pode ser uma maneira mais simples de definir uma tarefa do que fornecer instruções detalhadas e em linguagem natural sobre o que você espera.

Aqui está um exemplo de extração de entidade que é adequado para prompts de poucas tentativas.

Vamos tentar primeiro com um prompt de Zero Tentativas.

*Prompt:*
```
Generate a JSON document that provides the name, position, and company from the text below.

Text: Fred is a serial entrepreneur. Co-founder and CEO of Platform.sh, he previously co-founded Commerce Guys, a leading Drupal e-commerce provider. His mission is to guarantee that as we continue on an ambitious journey to profoundly transform how cloud computing is used and perceived, we keep our feet well on the ground, continuing the rapid growth we have enjoyed up until now.
```

*Output:*
```
{
  "Name": "Fred",
  "Position": "Co-founder and CEO",
  "Company": "Platform.sh, Commerce Guys"
}
```

Não é exatamente o que esperamos (apenas 'Platform.sh' deve estar no campo 'Company'), e pode ser difícil expressar isso em um prompt Zero-Shot. 

Vamos tentar um prompt Few-Shot. Note que vamos deixar cair as instruções e apenas fornecer a saída desejada.

*Prompt:*
```
Text: Fred is a serial entrepreneur. Co-founder and CEO of Platform.sh, he previously co-founded Commerce Guys, a leading Drupal e-commerce provider. His mission is to guarantee that as we continue on an ambitious journey to profoundly transform how cloud computing is used and perceived, we keep our feet well on the ground, continuing the rapid growth we have enjoyed up until now.

JSON:
{
  "Name": "Fred",
  "Position": "Co-founder and CEO",
  "Company": "Platform.sh"
}

Text: Microsoft (the word being a portmanteau of "microcomputer software") was founded by Bill Gates on April 4, 1975, to develop and sell BASIC interpreters for the Altair 8800. Steve Ballmer replaced Gates as CEO in 2000 and later envisioned a "devices and services" strategy.

JSON:
```

*Output:*
```
{
  "Name": "Microsoft",
  "Founder": "Bill Gates",
  "Founded": "April 4, 1975",
  "CEO": "Steve Ballmer",
  "Strategy": "Devices and Services"
}
```

Observe que o output não é o que queremos aqui, mas não houve exemplos suficientes para entender se o objetivo é extrair entidades-chave ou apenas determinadas entidades.

Usando few-shots esclarecerão isso.

*Prompt:*
```
Text: Fred is a serial entrepreneur. Co-founder and CEO of Platform.sh, he previously co-founded Commerce Guys, a leading Drupal e-commerce provider. His mission is to guarantee that as we continue on an ambitious journey to profoundly transform how cloud computing is used and perceived, we keep our feet well on the ground, continuing the rapid growth we have enjoyed up until now.

JSON:
{
  "Name": "Fred",
  "Position": "Co-founder and CEO",
  "Company": "Platform.sh"
}

Text: Microsoft (the word being a portmanteau of "microcomputer software") was founded by Bill Gates on April 4, 1975, to develop and sell BASIC interpreters for the Altair 8800. Steve Ballmer replaced Gates as CEO in 2000 and later envisioned a "devices and services" strategy.

JSON:
{
  "Name": "Bill Gates",
  "Position": "Co-founder and CEO",
  "Company": "Microsoft"
}

Text: Franck Riboud was born on November 7, 1955, in Lyon. He is the son of Antoine Riboud, the previous CEO, who transformed the former European glassmaker BSN Group into a leading player in the food industry. He is the CEO of Danone.

JSON:
```

*Output:*
```
{
  "Name": "Franck Riboud",
  "Position": "CEO",
  "Company": "Danone"
}
```
Agora podemos ver que o modelo entende claramente que queremos extrair apenas três entidades do texto e nada mais.

## Resumo

Neste laboratório, você adquiriu conhecimento teórico aprofundado e conhecimento prático avançado relacionado ao OpenAI e a vários tipos de métodos de engenharia de prompt.
