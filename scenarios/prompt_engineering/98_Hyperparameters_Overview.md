# Exercício 4D: Visão geral básica dos hiperparâmetros do Serviço Azure OpenAI (somente leitura)

### Duração estimada: 15 minutos

Este laboratório fornece conhecimentos básicos sobre hiperparâmetros no contexto do Serviço Azure OpenAI. Os participantes entendem como os hiperparâmetros influenciam o treinamento e o desempenho do modelo e aprendem técnicas básicas para ajustar esses parâmetros e obter melhores resultados.

## Nota rápida sobre o ajuste de hiperparâmetros

Ao trabalhar com prompts, você interagirá com o LLM por meio de uma API ou diretamente. Você pode configurar alguns parâmetros para obter resultados diferentes para seus prompts.

**Temperatura** - Em resumo, quanto menor a temperatura, mais determinísticos são os resultados, no sentido de que o próximo token com maior probabilidade é sempre escolhido. Temperaturas mais altas podem levar a mais aleatoriedade, incentivando resultados mais diversos ou criativos. Estamos essencialmente aumentando os pesos dos outros tokens possíveis. Em termos de aplicação, podemos querer usar uma temperatura mais baixa para algo como QA baseado em fatos para incentivar respostas mais factuais e concisas. Para geração de poemas ou outras tarefas criativas, pode ser benéfico aumentar a temperatura.

**Top_p** - Da mesma forma, com top_p, uma técnica de amostragem com temperatura chamada amostragem de núcleo, você pode controlar o quão determinístico o modelo é na geração de uma resposta. Se você busca respostas exatas e factuais, mantenha esse valor baixo. Se você busca respostas mais diversas, aumente para um valor mais alto.

A recomendação geral é alterar um, não ambos.

### gpt-35-turbo-instruct model

**temperatura**
```
Controla a aleatoriedade: a redução resulta em menos finalizações aleatórias. 
À medida que a temperatura se aproxima de zero, o modelo tornar-se-á determinista e repetitivo.
```

**max_tokens**
```
À medida que a temperatura se aproxima de zero, o modelo tornar-se-á determinista e repetitivo.
```

**top_p***
```
Controle quais tokens o modelo considerará ao gerar uma resposta por meio de amostragem de núcleo. 
Definir isso como 0,9 considerará os 90% mais prováveis de todos os tokens possíveis. 
Isso evitará o uso de tokens incorretos, mantendo a variedade quando o modelo tem baixa confiança nos tokens de maior pontuação.
```

**frequency_penalty**
```
Reduza a chance de repetir um token proporcionalmente com base na frequência com que ele apareceu no texto até agora.
Isso diminui a probabilidade de repetir o mesmo texto em uma resposta.
```

**presence_penalty**
```
Reduza a chance de repetir qualquer token que tenha aparecido no texto até agora. 
Isso aumenta a probabilidade de introduzir novos tópicos em uma resposta.
```

**best_of**
```
Gere várias respostas e exiba apenas aquela com a melhor probabilidade total em todos os seus tokens. 
Os candidatos não utilizados ainda incorrerão em custos de uso, portanto, use este parâmetro com cuidado e certifique-se de definir os parâmetros para o comprimento máximo de resposta e triggers finais também. Observe que o streaming só funcionará quando estiver definido como 1.
```

**stop**
```
Faça com que as respostas parem em um ponto desejado, como o final de uma frase ou lista.
Especifique até quatro sequências em que o modelo deixará de gerar mais tokens numa resposta. O texto gerado não conterá a sequência de parada.
```

## Resumo

Neste laboratório, você adquiriu conhecimento sobre os hiperparâmetros do Azure OpenAI e suas funcionalidades.