# **TRABALHO FINAL DE FIA**

## Discentes

| Nome | E-mail |
|-------------|-------------|
| Beatriz Quaresma Athaide    | beatriz.quaresma@icomp.ufam.edu.br      | 
| Gabriel Conceição dos Santos     | gabriel.conceicao@icomp.ufam.edu.br      | 
| Gabriela Pontes Borges | gabriela.borges@icomp.ufam.edu.br |
| Nestor Antony Farias de Souza  | Nestor.souza@icomp.ufam.edu.br  |
| Ruthelene Rodrigues Farias | ruthelene.farias@icomp.ufam.edu.br |
| Thales Arevalo dos Reis | thales@icomp.ufam.edu.br |
| Vinicius Gato Santana | vinicius.santana@icomp.ufam.edu.br |
| Victor da Silva Dantas | victor.dantas@icomp.ufam.edu.br |
| Guilherme Teles da Costa Moura | guilherme.moura@icomp.ufam.edu.br |

## **Descrição breve do trabalho**

Este trabalho investiga o uso de **Inteligência Artificial Neuro-Simbólica (NeSy)** por meio de **Logic Tensor Networks (LTN)** aplicadas a um **dataset sintético inspirado no CLEVR**. O objetivo é avaliar a capacidade do modelo em aprender relações entre objetos enquanto respeita regras lógicas explícitas, analisando tanto métricas clássicas de aprendizado supervisionado quanto medidas de **consistência lógica** (satisfatibilidade).

## **1\. Neuro-Symbolic AI (NeSy) e Logic Tensor Networks (LTN)**

### **Neuro-Symbolic AI (NeSy)**

A abordagem **NeSy** combina:

* **Redes neurais**, responsáveis por aprender padrões a partir de dados;  
* **Lógica simbólica**, que impõe restrições e regras explícitas ao modelo.

Essa integração permite maior **interpretabilidade**, **generalização** e **controle lógico**, superando limitações de abordagens puramente neurais ou puramente simbólicas.

### **Logic Tensor Networks (LTN)**

As **LTNs** implementam lógica de primeira ordem em um espaço contínuo, onde:

* Predicados são funções diferenciáveis;  
* Fórmulas lógicas retornam valores reais em (\[0,1\]);  
* O treinamento busca maximizar a **satisfatibilidade agregada (SatAgg)** do conjunto de fórmulas.

Assim, é possível treinar modelos via gradiente descendente respeitando conhecimento lógico explícito.

## **2\. Dataset CLEVR – Descrição Simplificada**

O **CLEVR** é um dataset voltado para raciocínio visual e relacional. Ele contém cenas compostas por objetos com atributos como:

* Forma (cubo, esfera, cilindro);  
* Cor, tamanho e material;  
* Posições espaciais.

Neste trabalho, foi utilizada uma **versão vetorial simplificada**, onde:

* Cada objeto é representado por um vetor de atributos;  
* Relações espaciais (esquerda, direita, acima, empilhado, proximidade) são inferidas a partir das posições;  

## **3\. Valor de Satisfatibilidade das Fórmulas no Conjunto de Teste**

Para cada fórmula lógica definida no notebook, foi calculada a **satisfatibilidade agregada (SatAgg)** no conjunto de teste. Essa métrica indica o grau em que o modelo respeita cada regra lógica após o treinamento.

As fórmulas incluem:

* Restrições estruturais (unicidade, cobertura, empilhamento);  
* Propriedades relacionais (assimetria, transitividade, inversão);  
* Consultas existenciais e compostas.

Os valores de SatAgg permitem avaliar diretamente a **coerência lógica** do modelo.

## **4\. Resultados para 5 Execuções com Datasets Aleatórios**

O passo **3.1.1 (Geração de Dados)** foi repetido **5 vezes**, produzindo **5 datasets aleatórios distintos**. Para cada dataset, os passos **3.2 e 3.3** foram executados novamente.

Para cada execução, foram calculadas as seguintes métricas:

* **Satisfatibilidade (SatAgg)** de cada fórmula e consulta;  
* **Acurácia**;  
* **Precisão**;  
* **Recall**;  
* **F1-Score**.

### **Resultados médios das 5 execuções**

Índices sorteados: [10188, 9149, 9744, 11947, 10136]

| Fórmula | SatAgg | Acurácia | Precisão | Recall | F1 |
| ----- | ----- | ----- | ----- | ----- | ----- |
| Unique Constraint | 0.9999 | 0.60 | 0.60 | 1.00 | 0.75 |
| Cover Constraint | 0.9996 | 0.40 | 0.40 | 1.00 | 0.57 |
| Irreflexivity | 0.5000 | 0.00 | 0.00 | 0.00 | 0.00 |
| Asymmetry | 0.8704 | 0.40 | 0.40 | 1.00 | 0.57 |
| Inverse Relation | 0.7678 | 0.40 | 0.40 | 1.00 | 0.57 |
| Transitivity | 0.9625 | 0.40 | 0.40 | 1.00 | 0.57 |
| Stack Rule | 0.9998 | 1.00 | 1.00 | 1.00 | 1.00 |
| Complex Query | 0.0488 | 0.60 | 0.00 | 0.00 | 0.00 |

Esses resultados mostram o impacto da complexidade lógica no desempenho do modelo.

## **5\. Conclusões**

Os resultados obtidos ao longo dos experimentos demonstram que a abordagem **Neuro-Simbólica (NeSy)** baseada em **Logic Tensor Networks (LTN)** é eficaz na aprendizagem e no respeito a **regras lógicas estruturais simples**, como restrições de unicidade, empilhamento e relações diretas entre objetos. Esses cenários apresentaram **altos valores de satisfatibilidade (SatAgg)** e métricas de desempenho consistentes, indicando que o modelo consegue incorporar conhecimento simbólico explícito ao processo de aprendizado neural de forma estável.

Entretanto, observou-se que **consultas lógicas mais complexas**, que envolvem múltiplas inferências relacionais, quantificações aninhadas e dependência de várias relações simultâneas, resultaram em **valores inferiores de SatAgg**, bem como em métricas tradicionais menos expressivas. Esse comportamento evidencia limitações atuais da abordagem na generalização de raciocínios simbólicos mais profundos, especialmente em cenários onde a complexidade lógica cresce significativamente em relação à estrutura dos dados disponíveis.

A análise conjunta entre **métricas tradicionais de classificação** (acurácia, precisão, recall e F1-score) e a **satisfatibilidade lógica** mostrou-se essencial para uma avaliação mais completa do modelo. Enquanto as métricas clássicas indicam o desempenho preditivo, a SatAgg fornece uma medida direta do **grau de coerência lógica** das soluções aprendidas, permitindo identificar situações em que o modelo pode obter bons resultados empíricos, mas ainda violar restrições simbólicas importantes  ou, inversamente, manter coerência lógica mesmo com desempenho preditivo limitado.

Além disso, a repetição dos experimentos com **cinco datasets aleatórios distintos**, gerados a partir do mesmo processo, demonstrou uma **consistência no comportamento lógico do modelo** ao longo das execuções. Apesar das variações naturais nos dados, os padrões de satisfatibilidade e desempenho mantiveram-se relativamente estáveis, reforçando a **robustez da abordagem NeSy com LTN** e reduzindo a probabilidade de que os resultados sejam fruto de um conjunto de dados específico.

Por fim, este trabalho evidencia o potencial das **Logic Tensor Networks** como uma ferramenta promissora para tarefas que exigem **raciocínio relacional, interpretabilidade e integração entre dados e conhecimento simbólico**, ao mesmo tempo em que destaca desafios relevantes a serem explorados em trabalhos futuros, como o aprimoramento da generalização em consultas complexas e o aumento da expressividade lógica do modelo.
