# Exercício 4D: Visão Geral Básica dos Hiperparâmetros do Serviço Azure OpenAI (Somente Leitura)

### Duração estimada: 20 Minutos

Este exercício fornece conhecimento fundamental sobre hiperparâmetros no contexto do Serviço OpenAI do Azure. Os participantes entenderão como os hiperparâmetros influenciam o treinamento e o desempenho do modelo, e aprenderão técnicas básicas para ajustar esses parâmetros para alcançar melhores resultados.

## Nota rápida sobre o ajuste de hiperparâmetros

Ao trabalhar com prompts, você interagirá com a LLM por meio de uma API ou diretamente. Você pode configurar alguns parâmetros para obter resultados diferentes para seus prompts.

**Temperatura:** Em resumo, quanto menor a temperatura, mais determinísticos serão os resultados, pois o próximo token mais provável é sempre escolhido. Aumentar a temperatura pode levar a mais aleatoriedade, incentivando saídas mais diversas ou criativas. Em termos de aplicação, usamos uma temperatura mais baixa para tarefas como perguntas e respostas baseadas em fatos (Q&A), a fim de obter respostas mais factuais e concisas. Para a geração de poemas ou outras tarefas criativas, pode ser benéfico aumentar a temperatura.

**Top_p:** De forma semelhante à temperatura, com o top_p (uma técnica de amostragem chamada *nucleus sampling*), você pode controlar o quão determinístico o modelo é ao gerar uma resposta. Se você procura respostas exatas e factuais, mantenha este valor baixo. Se busca respostas mais diversificadas, aumente o valor.

A recomendação geral é alterar um parâmetro ou outro, não ambos ao mesmo tempo.

### Modelo gpt-35-turbo-instruct

**temperatura**
```
Controla a aleatoriedade. Diminuir o valor resulta em conclusões menos aleatórias. Conforme a temperatura se aproxima de zero, o modelo se torna determinístico e repetitivo.
```

**max_tokens**
```
Define um limite para o número de tokens a serem gerados em uma resposta. O sistema suporta um máximo de 2048 tokens compartilhados entre o prompt e a resposta. (Um token equivale a aproximadamente 4 caracteres em textos comuns em inglês).
```

**top_p**
```
Controla quais tokens o modelo irá considerar ao gerar uma resposta, via nucleus sampling. Definir este valor como 0.9 fará com que o modelo considere os 90% dos tokens mais prováveis dentre todos os possíveis. Isso evita o uso de tokens incorretos, mantendo a variedade.
```

**frequency_penalty**
```
Reduz a chance de repetir um token proporcionalmente com base na frequência com que ele já apareceu no texto. Isso diminui a probabilidade de o modelo repetir o mesmo trecho em uma resposta.
```

**presence_penalty**
```
Reduz a chance de repetir qualquer token que já tenha aparecido no texto. Isso aumenta a probabilidade de o modelo introduzir novos tópicos em uma resposta.
```

**best_of**
```
Gera múltiplas respostas e exibe apenas a que tiver a melhor probabilidade total em todos os seus tokens. As respostas descartadas ainda gerarão custos de uso, então use este parâmetro com cuidado. Note que o streaming só funcionará quando best_of for definido como 1.
```

**stop**
```
Faz com que as respostas parem em um ponto desejado, como o final de uma frase ou lista. Você pode especificar até quatro sequências que, ao serem detectadas, interromperão a geração de novos tokens. O texto retornado não conterá a sequência de parada.
```

## Resumo

Neste exercício, você aprendeu sobre os hiperparâmetros do Serviço OpenAI do Azure e suas funcionalidades.

### Clique em Próximo >> para prosseguir com o próximo exercício.

![](../natural_language_query/images/30-7-25-g5.png)
