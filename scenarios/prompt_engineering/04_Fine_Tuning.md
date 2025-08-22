# Exercício 4C: Ajuste Fino (Somente Leitura)

### Duração Estimada: 25 Minutos

Este laboratório se concentra no processo de ajuste fino de modelos OpenAI para melhorar seu desempenho em tarefas ou conjuntos de dados específicos. Os participantes aprendem como ajustar parâmetros do modelo, otimizar estratégias de treinamento e avaliar métricas de desempenho do modelo por meio de exercícios práticos e exemplos.

## Tópicos

- [O que é Ajuste Fino?](#o-que-e-ajuste-fino)
- [Quando considerar Ajuste Fino em vez de Engenharia de Prompt?](#quando-voce-consideraria-ajuste-fino-vs-engenharia-de-prompt)
- [Considerações sobre Custos Operacionais](#considerações-sobre-custos-operacionais)

---
## O que é Ajuste Fino?

O ajuste fino é o processo de personalizar um modelo de IA existente para uma tarefa ou domínio específico, utilizando dados adicionais. A OpenAI oferece a opção de ajusto fino para seus modelos de linguagem, como o GPT-3, que podem gerar textos em linguagem natural para diversos fins.

O ajuste fino permite que os usuários criem modelos personalizados capazes de produzir resultados mais precisos e relevantes do que os modelos genéricos.

Para fazer o ajuste fino de um modelo da OpenAI, os usuários precisam preparar seus próprios dados de treinamento e validação, selecionar um modelo base e usar a CLI ou o Azure AI Foundry para iniciar o processo de ajuste fino.

O ajuste fino pode melhorar significativamente o desempenho e reduzir as taxas de erro dos modelos da OpenAI.

---
## Dados de Treinamento de Ajuste Fino

Os dados de treinamento para o fine-tuning de modelos da OpenAI são pares de prompts de entrada e saídas desejadas que refletem a tarefa ou o domínio específico para o qual você deseja personalizar o modelo. Por exemplo, se você quiser fazer o fine-tuning de um modelo para gerar análises de produtos, seus dados de treinamento poderiam ser assim:

```
{"prompt": "Análise: Comprei este notebook para minhas aulas online e ele funciona muito bem.", "completion": "Avaliação: 5 estrelas"}
{"prompt": "Análise: A duração da bateria é péssima e a tela é muito pequena.", "completion": "Avaliação: 2 estrelas"}
{"prompt": "Análise: Isso é um golpe. O produto nunca chegou e o vendedor não respondeu.", "completion": "Avaliação: 1 estrela"}
```

Você pode usar o OpenAI CLI ou o Azure AI Foundry para preparar, validar e formatar seus dados de treinamento em um arquivo JSON que pode ser usado para ajustes finos.

**NOTA IMPORTANTE:**
É crucial observar que, para obter resultados superiores aos da engenharia de prompt, você precisará de um conjunto de dados grande e de alta qualidade que seja relevante para sua tarefa ou domínio, geralmente algumas centenas de exemplos de alta qualidade.

---
## Quando considerar Ajuste Fino em vez de Engenharia de Prompt?

O ajuste fino é uma ferramenta poderosa que pode ser usada para personalizar modelos OpenAI para tarefas ou domínios específicos. No entanto, nem sempre é necessário ajustar um modelo para obter os resultados desejados.

O ajuste fino e a engenharia de prompts são dois métodos de condicionamento de modelos de linguagem para executar tarefas ou domínios específicos.

O ajuste fino envolve o retreinamento de um modelo existente com novos dados, enquanto a engenharia de prompts envolve projetar e testar instruções de entrada que geram a saída desejada de um modelo.

### Ajuste Fino

Você pode considerar o ajuste fino quando possuir um conjunto de dados grande e de alta qualidade, relevante para sua tarefa ou domínio, e desejar criar um modelo personalizado que possa gerar resultados mais precisos e consistentes do que o modelo genérico.

### Engenharia de Prompt

Você pode considerar a engenharia de prompt quando tiver um conjunto de dados limitado ou inexistente e quiser aproveitar o conhecimento e as capacidades de um modelo genérico, fazendo as perguntas certas ou fornecendo o contexto adequado.

**NOTA IMPORTANTE:**  Ambos os métodos exigem um processo de tentativa e erro, mas o ajuste fino geralmente consome mais tempo e recursos. Portanto, é preferível começar com a engenharia de prompt e só considerar o ajuste fino se não for possível alcançar os resultados esperados com a primeira abordagem.

---
## Considerações sobre Custos Operacionais

A engenharia de prompt pode ter um custo-benefício menor se você precisar fornecer um grande número de instruções para alcançar um resultado semelhante ao que obteria com um modelo de ajuste fino, pois você consumirá tokens a cada requisição enviada.

Hospedar um modelo de ajuste fino também tem seu custo, mas para volumes médios a altos, esse custo se torna praticamente irrelevante. Portanto, a eficiência do custo operacional pode ser um fator decisivo para optar pelo ajuste fino.

## Referências

[Ajuste Fino do OpenAI](https://platform.openai.com/docs/guides/fine-tuning)

[Ajuste Fino no Serviço Azure OpenAI](https://learn.microsoft.com/en-us/azure/cognitive-services/openai/how-to/fine-tuning?pivots=programming-language-studio)

## Resumo

Neste exercício, você aprendeu sobre o que é o fine-tuning, as diferenças entre essa técnica e a engenharia de prompt, e as considerações de custos operacionais de cada abordagem.

### Clique em **Próximo >>** para prosseguir com o próximo exercício.

![](../natural_language_query/images/30-7-25-g5.png)
