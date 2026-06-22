# Relatório da AVA 2 
**Aluno:** Hugo Miranda Machado Barroso  

## 1. Divisão de Treino / Teste e Normalização
Dividi a base usando a regra do 80/20, mas mantendo a ordem do tempo (cronológica), já que dados financeiros não podem ser embaralhados:
* **Treino:** 75 dias (os primeiros 80%)
* **Teste:** 19 dias (os últimos 20% para validar)

## 2. Os Modelos que testei
Rodei os 5 algoritmos, configurando alguns hiperparâmetros para controlar o aprendizado:
1. **Árvore de Decisão:** Travei a profundidade máxima em 4 para não deixar ela criar regras demais e bitolar no treino.
2. **Random Forest:** Usei 100 árvores menores com profundidade máxima de 5.
3. **SVM:** Configurei com o kernel rbf e margem C=1.0.
4. **KNN:** Usei para checar os 7 vizinhos mais próximos K=7.
5. **Rede Neural (MLP):** Uma rede simples com uma camada oculta de 50 neurônios e até 500 iterações.

## 3. Tabela Comparativa dos Resultados

| Modelo | Acurácia | Precisão | Recall | F1-Score |
| :--- | :---: | :---: | :---: | :---: |
| **Árvore de Decisão** | **0.842** | **0.833** | 0.714 | **0.769** |
| **Rede Neural (MLP)** | 0.684 | 0.556 | 0.714 | 0.625 |
| **Random Forest** | 0.579 | 0.462 | **0.857** | 0.600 |
| **SVM** | 0.526 | 0.429 | **0.857** | 0.571 |
| **KNN** | 0.526 | 0.429 | **0.857** | 0.571 |


## 4. Conclusão e qual modelo eu recomendaria

Com base nos resultados apresentados, a **Árvore de Decisão** foi o modelo com melhor desempenho neste experimento prático, alcançando o maior F1-Score. Isso indica uma boa capacidade de equilíbrio entre precisão e recall, sendo eficaz tanto em identificar corretamente os dias em que a ação fecha acima da média móvel, quanto em minimizar falsos positivos e negativos.

### Análise do resultado da Árvore de Decisão:

A Árvore de Decisão, com profundidade máxima de 4, conseguiu extrair regras de decisão claras e eficazes a partir dos dados de treinamento. Sua superioridade pode ser atribuída à sua capacidade de modelar relações não-lineares e interações entre as features de forma relativamente simples e interpretabil. Em um conjunto de dados pequeno como este (75 dias de treino e 19 de teste), a limitação da profundidade ajuda a evitar o *overfitting*, garantindo que o modelo generalize melhor para novos dados ao invés de memorizar o ruído do treinamento. Isso contrasta com modelos como a Rede Neural, que geralmente requerem muito mais dados para convergir e aprender padrões robustos, e o KNN, que pode ser mais sensível a dados ruidosos ou à distribuição específica de um pequeno conjunto de teste.

## 5. Justificativa de Descarte dos Outros Modelos

* **Rede Neural (MLP) e Random Forest:** Apresentaram desempenhos fracos (Acurácia de 68.4% e 57.9%, respectivamente) porque são arquiteturas de alta complexidade matemática. Esses modelos exigem volumes massivos de dados para ajustar seus múltiplos parâmetros e pesos de forma eficiente. Com apenas 75 dias de treino, eles sofreram para convergir e acabaram se perdendo.
* **SVM e KNN:** Apesar de mostrarem uma sensibilidade excelente para detectar as subidas (Recall de 0.857), falharam gravemente no critério de Precisão (42.9%). Isso gera uma taxa inaceitável de falsos positivos. No mercado financeiro real, seguir os sinais desses dois modelos resultaria em um número excessivo de operações perdedoras, gerando prejuízo financeiro.
