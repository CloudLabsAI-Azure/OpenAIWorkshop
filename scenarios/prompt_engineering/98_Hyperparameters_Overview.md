# Exercício 4D: Visão geral básica dos hiperparâmetros do Serviço Azure OpenAI (somente leitura)

### Duração estimada: 20 Minutos

Este exercício fornece conhecimentos básicos sobre hiperparâmetros no contexto do Serviço Azure OpenAI. Os participantes entendem como os hiperparâmetros influenciam o treinamento e o desempenho do modelo e aprendem técnicas básicas para ajustar esses parâmetros e obter melhores resultados.

## Nota rápida sobre o ajuste de hiperparâmetros

Ao trabalhar com prompts, você interagirá com o LLM por meio de uma API ou diretamente. Você pode configurar alguns parâmetros para obter resultados diferentes para seus prompts.

**Temperatura:** Em resumo, quanto menor a temperatura, mais determinísticos são os resultados, no sentido de que o próximo token com maior probabilidade é sempre escolhido. Temperaturas mais altas podem levar a mais aleatoriedade, incentivando resultados mais diversos ou criativos. Estamos essencialmente aumentando os pesos dos outros tokens possíveis. Em termos de aplicação, podemos querer usar uma temperatura mais baixa para algo como QA baseado em fatos para incentivar respostas mais factuais e concisas. Para geração de poemas ou outras tarefas criativas, pode ser benéfico aumentar a temperatura.

**Top_p:** Da mesma forma, com top_p, uma técnica de amostragem com temperatura chamada amostragem de núcleo, você pode controlar o quão determinístico o modelo é na geração de uma resposta. Se você está procurando respostas exatas e factuais, mantenha isso baixo. Se você está procurando respostas mais diversificadas, aumente o valor.
A recomendação geral é alterar um, não ambos.

### gpt-35-turbo-instruct model

**temperatura**
```
Controls randomness: Lowering results in fewer random completions. 
As the temperature approaches zero, the model will become deterministic and repetitive.
```

**max_tokens**
```
Set a limit on the number of tokens to generate in a response. 
The system supports a maximum of 2048 tokens shared between a given prompt and response completion. 
(One token is roughly 4 characters for typical English text.)
```

**top_p**
```
Control which tokens the model will consider when generating a response via nucleus sampling. 
Setting this to 0.9 will consider the top 90% most likely of all possible tokens. 
This will avoid using tokens that are incorrect while still maintaining variety
when the model has low confidence in the highest-scoring tokens.
```

**frequency_penalty**
```
Reduce the chance of repeating a token proportionally based on how often it has appeared in the text so far.
This decreases the likelihood of repeating the same text in a response.
```

**presence_penalty**
```
Reduce the chance of repeating any token that has appeared in the text at all so far. 
This increases the likelihood of introducing new topics in a response.
```

**best_of**
```
Generate multiple responses, and display only the one with the best total probability across all its tokens. 
The unused candidates will still incur usage costs, so use this parameter carefully and make sure to set the
parameters for max response length and ending triggers as well. Note that streaming will only work when this is set to 1.
```

**stop**
```
Make responses stop at a desired point, such as the end of a sentence or list.
Specify up to four sequences where the model will stop generating further tokens
in a response. The returned text will not contain the stop sequence.
```

## Resumo

Neste exercício, você adquiriu conhecimento sobre os hiperparâmetros do Azure OpenAI e suas funcionalidades.

### Clique em Próximo >> para prosseguir com o próximo exercício.

![](../natural_language_query/images/30-7-25-g5.png)
