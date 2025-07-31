# Exercício 4C: Ajuste Fino (Somente Leitura)

### Duração Estimada: 25 Minutos

Este laboratório se concentra no processo de ajuste fino de modelos OpenAI para melhorar seu desempenho em tarefas ou conjuntos de dados específicos. Os participantes aprendem como ajustar parâmetros do modelo, otimizar estratégias de treinamento e avaliar métricas de desempenho do modelo por meio de exercícios práticos e exemplos.

## Tópicos

- [O que é Ajuste Fino?](#o-que-e-ajuste-fino)
- [Quando você consideraria Ajuste Fino vs. Engenharia de Prompt?](#quando-voce-consideraria-ajuste-fino-vs-engenharia-de-prompt)
- [Considerações sobre Custos Operacionais](#considerações-sobre-custos-operacionais)

---
## O que é Ajuste Fino?

O ajuste fino é o processo de personalizar um modelo de IA existente para uma tarefa ou domínio específico usando dados adicionais. A OpenAI oferece ajuste fino para seus modelos de linguagem, como o GPT-3, que pode gerar textos em linguagem natural para diversos fins.

O ajuste fino permite que os usuários criem modelos personalizados que podem produzir resultados mais precisos e relevantes do que modelos gerais.

Para ajustar um modelo OpenAI, os usuários precisam preparar seus próprios dados de treinamento e validação, selecionar um modelo base e usar a CLI ou o Studio do OpenAI para iniciar o trabalho de ajuste fino.

O ajuste fino pode melhorar o desempenho e reduzir significativamente as taxas de erro dos modelos OpenAI.

---
## Dados de Treinamento de Ajuste Fino

Os dados de treinamento para o ajuste fino de modelos OpenAI são pares de prompts de entrada e saídas desejadas que refletem a tarefa ou domínio específico para o qual você deseja personalizar o modelo. Por exemplo, se você quiser ajustar um modelo para gerar avaliações de produtos, seus dados de treinamento podem ser assim:

```
{"prompt": "Review: I bought this laptop for my online classes and it works great.", "completion": "Rating: 5 stars"}
{"prompt": "Review: The battery life is terrible and the screen is too small.", "completion": "Rating: 2 stars"}
{"prompt": "Review: This is a scam. The product never arrived, and the seller did not respond.", "completion": "Rating: 1 star"}
```

Você pode usar o OpenAI CLI ou o Studio para preparar, validar e formatar seus dados de treinamento em um arquivo JSON que pode ser usado para ajustes finos.

**NOTA IMPORTANTE:**
É importante observar que, para esperar resultados melhores do que usar a engenharia de prompts, você precisará de um conjunto de dados amplo e de alta qualidade, relevante para sua tarefa ou domínio, geralmente algumas centenas de exemplos de alta qualidade.

---
## Quando você consideraria o Ajuste Fino versus Engenharia de Prompts?

O ajuste fino é uma ferramenta poderosa que pode ser usada para personalizar modelos OpenAI para tarefas ou domínios específicos. No entanto, nem sempre é necessário ajustar um modelo para obter os resultados desejados.

O ajuste fino e a engenharia de prompts são dois métodos de condicionamento de modelos de linguagem para executar tarefas ou domínios específicos.

O ajuste fino envolve o retreinamento de um modelo existente com novos dados, enquanto a engenharia de prompts envolve projetar e testar instruções de entrada que geram a saída desejada de um modelo.

### Ajuste Fino

Você pode considerar o ajuste fino quando tiver um conjunto de dados amplo e de alta qualidade, relevante para sua tarefa ou domínio, e quiser criar um modelo personalizado que possa produzir saídas mais precisas e consistentes do que o modelo geral.

### Engenharia Rápida

Você pode considerar a engenharia rápida quando tiver um conjunto de dados limitado ou inexistente e quiser aproveitar o conhecimento e os recursos existentes de um modelo geral, fazendo as perguntas certas ou fornecendo o contexto correto.

**NOTA IMPORTANTE:** Ambos os métodos exigem tentativa e erro, mas o ajuste fino geralmente consome mais tempo e recursos do que a engenharia rápida, e nem sempre é necessário ajustar um modelo para obter os resultados desejados. Portanto, é preferível começar com a engenharia rápida e considerar o ajuste fino somente se você não conseguir obter os resultados desejados.

---
## Considerações sobre Custo Operacional

A engenharia rápida pode ser menos econômica se você precisar fornecer um grande número de instruções para realizar algo semelhante ao que obteria com um modelo com Ajuste Fino, já que consumiria tokens a cada solicitação enviada.

Hospedar um modelo com Ajuste Fino também tem seu custo, mas em volumes médios a altos, esse custo seria irrelevante, portanto, a eficiência de custos operacionais pode ser um fator determinante para o Ajuste Fino.

## Referências

[Ajuste Fino do OpenAI](https://platform.openai.com/docs/guides/fine-tuning)

[Ajuste Fino no Serviço OpenAI do Azure](https://learn.microsoft.com/en-us/azure/cognitive-services/openai/how-to/fine-tuning?pivots=programming-language-studio)

## Resumo

Neste exercício, você adquiriu conhecimento sobre vários tópicos sobre o que exatamente é ajuste fino, as diferenças entre ajuste fino e engenharia de prompts e os custos operacionais a serem considerados.

### Clique em **Próximo >>** para prosseguir com o próximo exercício.

![](../natural_language_query/images/30-7-25-g5.png)
