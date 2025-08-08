# Exercício 4B: Conceitos Avançados (Somente Leitura)

### Duração estimada: 30 Minutos

Este exercício fornece conhecimento teórico aprofundado e prático avançado relacionado à OpenAI e suas aplicações. Ele aborda a introdução à engenharia de prompt, seus casos de uso e os vários tipos de prompts que podem ser implementados para obter os resultados desejados.

## Tópicos

  - [Introdução](#introduction)
  - [Prompts Zero-Shot](#zero-shot-prompts)
  - [Prompts One-Shot](#one-shot-prompts)
  - [Prompts Few-Shot](#few-shot-prompts)

---

## Introdução

Neste ponto, você já experimentou o poder e a flexibilidade dos prompts. Ajustar os prompts para obter os resultados desejados é a ideia por trás da engenharia de prompt.

Agora, abordaremos alguns tópicos mais avançados para aprimorar nossas saídas sem a necessidade de realizar o ajuste fino (fine-tuning) de nossos modelos GPT.

Vejamos um exemplo simples de classificação:

*Prompt:*
```
Classifique o sentimento do texto abaixo.

Texto: Eu achei este filme terrível. Que perda de tempo.
```

*Saída:*
```
Negativo
```

A saída parece correta, mas poderíamos melhorá-la fornecendo mais informações ao modelo se quiséssemos uma classificação mais granular. Vamos fazer isso por meio de um prompt *Zero-Shot*.

---

## Prompts Zero-Shot

Os LLMs GPT são treinados com volumes de dados tão grandes que, na maioria dos casos, são capazes de compreender instruções complexas para chegar ao resultado desejado. Isso é chamado de prompt *Zero-Shot*.

Poderíamos refinar o exemplo abaixo sendo mais descritivos em nossas instruções.

*Prompt:*
```
Classifique o sentimento do texto abaixo em muito negativo, negativo, neutro, positivo e muito positivo.

Texto: Eu achei este filme terrível. Que perda de tempo.
```

*Saída:*
```
Muito Negativo
```

Isso é chamado de *Zero-Shot*. Uma instrução precisa leva ao resultado desejado sem a necessidade de exemplos.

---

## Prompts One-Shot

Às vezes, pode ser mais fácil fornecer um exemplo para o modelo aprender. Isso é chamado de prompt *One-Shot*.

Primeiro, vamos fazer um prompt *Zero-Shot*.

*Prompt:*
```
Diga-me em que cidade uma universidade está localizada.

Universidade: UCLA
```

*Saída:*
```
Cidade: Los Angeles, California
```

Digamos que você quisesse uma saída específica para este prompt. Você poderia fornecer um exemplo para o modelo aprender.

Aqui está um Prompt *One-Shot* que leva ao mesmo resultado.

*Prompt:*
```
Diga-me em que cidade uma universidade está localizada.

Universidade: UCLA
Cidade: Los Angeles, CA, USA

Universidade: MIT
```

*Saída:*
```
Cidade: Cambridge, MA, USA
```

Note que você também poderia ter usado o prompt *Zero-Shot* para este exemplo. Mas os prompts One-Shot são mais flexíveis e podem ser usados para ajustar o modelo às suas necessidades.

Aqui está um Prompt *Zero-Shot* equivalente.

*Prompt:*
```
Diga-me em que cidade uma universidade está localizada. Forneça o nome da cidade, o código do estado e o país, separados por vírgula em uma única linha.

Universidade: UCLA
```

*Saída:*
```
Cidade: Los Angeles, CA, USA
```
---

## Prompts Few-Shot

Prompts *Few-shot* permitem que você forneça múltiplos exemplos para o modelo aprender. Isso é útil quando você deseja ajustar a saída para cenários mais complexos, onde o resultado pode variar com base na entrada. Também pode ser uma maneira mais simples de definir uma tarefa do que fornecer instruções detalhadas em linguagem natural sobre o que você espera.

Aqui está um exemplo de extração de entidades que se adapta bem a prompts *few-shot*.

Vamos tentar primeiro com um prompt *Zero-Shot*.

*Prompt:*
```
Gere um documento JSON que forneça o nome, a posição e a empresa a partir do texto abaixo.

Texto: Fred é um empreendedor em série. Co-fundador e CEO da Platform.sh, ele anteriormente co-fundou a Commerce Guys, um dos principais provedores de comércio eletrônico Drupal. Sua missão é garantir que, enquanto continuamos em uma jornada ambiciosa para transformar profundamente a forma como a computação em nuvem é usada e percebida, mantenhamos os pés no chão, continuando o rápido crescimento que desfrutamos até agora.
```

*Saída:*
```
{
  "Nome": "Fred",
  "Cargo": "Cofundador e CEO",
  "Companhia": "Platform.sh, Commerce Guys"
}
```

Não é exatamente o que esperávamos (apenas 'Platform.sh' deveria aparecer em 'Companhia'), e pode ser difícil expressar isso em um prompt *Zero-Shot*.

Vamos tentar um prompt *Few-Shot*. Note que vamos omitir as instruções e apenas fornecer a saída desejada.

*Prompt:*
```
Texto: Fred é um empreendedor em série. Co-fundador e CEO da Platform.sh, ele anteriormente co-fundou a Commerce Guys, um dos principais provedores de comércio eletrônico Drupal. Sua missão é garantir que, enquanto seguimos em uma jornada ambiciosa para transformar profundamente a forma como a computação em nuvem é usada e percebida, mantenhamos os pés no chão, continuando o rápido crescimento que temos desfrutado até agora.

JSON:
{
  "Nome": "Fred",
  "Posição": "Cofundador e CEO",
  "Companhia": "Platform.sh"
}

Texto: A Microsoft (nome que é uma junção das palavras "microcomputer" e "software") foi fundada por Bill Gates em 4 de abril de 1975, para desenvolver e vender interpretadores BASIC para o Altair 8800. Steve Ballmer substituiu Gates como CEO em 2000 e, posteriormente, idealizou uma estratégia de "dispositivos e serviços.

JSON:
```

*Saída:*
```
{
  "Nome": "Microsoft",
  "Fundador": "Bill Gates",
  "Fundação": "April 4, 1975",
  "CEO": "Steve Ballmer",
  "Estratégia": "Dispositivos e Serviços"
}
```

Note que a saída aqui não é o que queremos, mas não houve exemplos suficientes para entender se o objetivo é extrair entidades-chave ou apenas certas entidades.

Um prompt com mais alguns exemplos esclarecerá isso.

*Prompt:*
```
Texto: Fred é um empreendedor em série. Cofundador e CEO da Platform.sh, ele cofundou anteriormente a Commerce Guys, uma das principais provedoras de e-commerce em Drupal. Sua missão é garantir que, à medida que continuamos nossa jornada ambiciosa para transformar profundamente a forma como a computação em nuvem é usada e percebida, mantenhamos os pés bem firmes no chão, dando continuidade ao rápido crescimento que tivemos até agora.

JSON:
{
  "Nome": "Fred",
  "Posição": "Cofundador e CEO",
  "Companhia": "Platform.sh"
}

Texto: A Microsoft, cujo nome é uma junção das palavras "microcomputador" e "software", foi fundada por Bill Gates em 4 de abril de 1975 para desenvolver e vender interpretadores BASIC para o Altair 8800. Steve Ballmer substituiu Gates como CEO em 2000 e, mais tarde, idealizou a estratégia de "dispositivos e serviços.

JSON:
{
  "Nome": "Bill Gates",
  "Posição": "Cofundador e CEO",
  "Companhia": "Microsoft"
}

Texto: Franck Riboud nasceu em 7 de novembro de 1955, em Lyon. Ele é filho de Antoine Riboud, o CEO anterior, que transformou a antiga fabricante europeia de vidros Grupo BSN em um dos principais players do setor de alimentos. Ele é o CEO da Danone.

JSON:
```

*Saída:*
```
{
  "Nome": "Franck Riboud",
  "Posição": "CEO",
  "Companhia": "Danone"
}
```
Agora podemos ver que o modelo compreende claramente que queremos extrair apenas três entidades do texto e nada mais.

## Resumo

Neste exercício, você adquiriu conhecimento teórico aprofundado e prático avançado relacionado à OpenAI e a vários métodos de engenharia de prompt.

### Clique em Próximo >> para prosseguir com o próximo exercício.

![](../natural_language_query/images/30-7-25-g5.png)
