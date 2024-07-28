# 📊 Previsão de Estoque Inteligente na AWS com [SageMaker Canvas](https://aws.amazon.com/pt/sagemaker/canvas/)

Bem-vindo ao desafio de projeto "Previsão de Estoque Inteligente na AWS com SageMaker Canvas. Neste Lab DIO, vamos criar previsões de estoque baseadas em Machine Learning (ML). Siga os passos abaixo para completar o desafio!

## 📋 Pré-requisitos

Criar uma conta na AWS. [AWS Cloud Quickstart](https://github.com/digitalinnovationone/aws-cloud-quickstart).
Ficar atendo ao plano Free Tier para não ter surpresas.


## 🎯 Objetivos Deste Desafio de Projeto (Lab)

![image](https://github.com/digitalinnovationone/lab-aws-sagemaker-canvas-estoque/assets/730492/72f5c21f-5562-491e-aa42-2885a3184650)

- Criar ou selecinar `dataset` fornecido pela DIO na pasta `datasets` deste repositório.
- Submeter o arquivo csv no SageMaker Canvas.
- Configurar as variáveis de entrada e saída de acordo com os dados.
- Realizar o treinamento do modelo.
- Após o treinamento, examinar as métricas de performance do modelo.
- Usar o modelo treinado para fazer previsões de estoque.
- Exportar os resultados e analise as previsões geradas.
- Documentar suas conclusões e qualquer insight obtido a partir das previsões.


## 🚀 Passo a Passo

### 1. Selecionando o Dataset

- O `datasets` selecionado foi o dataset-1000-com-preco-promocional-e-renovacao-estoque para projeção do projeto de **_Previsão de Estoque Inteligente na AWS com Sagemaker Canvas._**
- Dentro do SageMaker Canvas crie um domínio e abra o SageMaker Canvas:
> Importe o `datasets` selecionado;
![Imgur](https://imgur.com/5ER9cM2)
> Crie um novo modelo de Análise preditiva e dê um novo nome;
![Imgur](https://imgur.com/Y9oMjiY.png)
> Selecine o `datasets`.
![Imgur](https://imgur.com/4LPss1L)


### 2. Construindo e Treinando o modelo

- Realizar a configuração do meu modelo apontando como `target` a coluna QUANTIDADE_ESTOQUE.
> A configuração ficou assim:
![Imgur](https://imgur.com/zqKZ4oI.png)

- Configurar o modelo selecionando o ID_PRODUTO como `ITEM ID` para identificação de valor único.
- O indicativo para a coluna que contém `timestamps` ele reconheceuu automáticamente.
- Alterar a projeção me mostrar o os 5 próximos dias.
- Adicionar como base os feriados nacionais no Brasil.
> A configuração ficou assim:
![Imgur](https://imgur.com/QXneugO.png)

- Executar o Quick build.

### 3. Analisando o modelo

- Temos o `Avg wQL` que é a perda média ponderada de quantis, é uma previsão calculando como um todo a média de precisão de pontos de distribuição, formando o P10, P50 e P90. Quanto mais baixo esse valor mais preciso é o modelo.
- Temos o `MAPE` que é o erro percentual médio absoluto que seria a diferença percentual entre o valor médio previsto com o valor real. O valor quanto mais próximo de `0`, melhor, sendo `MAPE=0` como um modelo perfeito e sem erros.
- O `WAPW` é o erro percentual absoluto ponderado, onde mede o desvio geral dos valores previstos em relação aos valores observados e é definido pela soma do erro absoluto normalizado pela soma da meta absoluta. Um valor mais baixo indica um modelo mais preciso com `WAPE=0` como um modelo perfeito e sem erros.
- O `RMSE` é a raiz quadrada dos erros quadráticos médios. Um `RMSE` mais baixo indica um modelo mais preciso com `RMSE=0` como um modelo perfeito e sem erros.
- O `MASE` é a média do erro absoluto da previsão normalizada pelo erro médio absoluto de um método simples de previsão de linha de base. Um valor mais baixo indica um modelo mais preciso com `MASE < 1` como um modelo estimado como melhor que a linha de base e um `MASE > 1` como um modelo estimado como pior que a linha de base.
> **Resultado do modelo.**
![Imgur](https://imgur.com/Fgrqcal.png)
![Imgur](https://imgur.com/CYzL9pl.png)


### 4. Previsão Final

- As previsões de estoque ficaram assim.
- Aqui temos o `Item 1011` onde temos uma demanda histórica e as projeções para os 5 próximos dias em `P10, P50 e P90`
> Projeção gráfica:
![Imgur](https://imgur.com/CYzL9pl.png)

> Após algumas modificações na Build obtive novos resultados:
![Imgur](https://imgur.com/omV6VL8.png)

## Explicando P10, P50 e P90

- Esses quantis são utilizados para considerar a incerteza das previsões. Por padrão, as previsões são geradas para 0,1 (P10), 0,5 (P50) e 0,9 (P90).
> P10 (Linha Rosa): Reflete um cenário pessimista.
> P50 (Linha Verde): Reflete um cenário neutro.
> P90 (Linha Amarela): Reflete um cenário otimista.
