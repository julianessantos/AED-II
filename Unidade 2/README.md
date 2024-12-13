### Departamento de Engenharia de Computação e Automação
#### Algoritmo e Estrutura de Dados II (DCA3702)
#### Trabalho 2

Avaliar o desempenho de dois algoritmos fornecidos (solver_closest.ipynb e solver_kth_largest.ipynb) considerando diversas entradas aleatórias e reproduzíveis, variando o tamanho do vetor de entrada até um valor N grande


Usando como fonte os código disponibilizados durante a [semana 9](https://github.com/ivanovitchm/datastructure/tree/main/lessons/week_09) e aulas teoricas, o segundo projeto da segunda unidade tem como objetivo avaliar o desempenho de dois algoritmos fornecidos (solver_closest.ipynb e solver_kth_largest.ipynb) considerando diversas entradas aleatórias e reproduzíveis, variando o tamanho do vetor de entrada até um valor N grande.

O projeto foi realizado de maneira individual. Além dos código é possível observar uma breve explicação do trabalho no [video](https://www.loom.com/share/65226a7974b34bdaa5b53db2ade94c15?sid=fc75173f-ed7b-4660-8860-17c211dd0dee) salvo na plataforma Loom.

#### 🎯 Objetivos
- [x] Avaliar o desempenho de dois algoritmos fornecidos (solver_closest.ipynb e solver_kth_largest.ipynb) 

### Explicação do Código
O código está configurado para medir o desempenho de duas funções, solver_closest e solver_kth_largest, que operam sobre uma árvore de busca binária (BST). Ele faz isso para diferentes tamanhos de vetores de entrada, com múltiplas execuções por tamanho para obter medidas confiáveis de desempenho e calcular intervalos de confiança, lembrando que:

- solver_closest(tree, target): Encontra o valor mais próximo de target na árvore.
- solver_kth_largest(tree, k): Encontra o k-ésimo maior valor na árvore.

#### Parâmetros de Teste:

- N: Define o tamanho máximo dos vetores gerados.
- steps: Controla o número de tamanhos de vetor a serem testados.
- executions_per_size: Define o número de execuções repetidas para cada tamanho de vetor, para melhorar a precisão dos resultados.
- Vetores de Teste: vector_sizes cria uma lista de tamanhos uniformemente espaçados entre 100 e N.

#### Medições:
Para cada tamanho de vetor, o script:
- Gera dados aleatórios.
- Constrói uma BST com esses dados.
- Mede o tempo necessário para executar as funções solver_closest e solver_kth_largest.

#### Cálculo Estatístico:
- Calcula a média e o desvio padrão dos tempos registrados para cada tamanho de vetor.
- Determina intervalos de confiança de 95% para as médias, usando a distribuição t.
- Ajustes e Pontos a Considerar


> [!WARNING]
> Para a realização do projeto é necessário realizar alguns passos iniciais.

1º: Realizar o download do arquivo binarysearchtree.py

2º: Realizar a importação das bibliotecas
```
import numpy as np
import matplotlib.pyplot as plt
from time import perf_counter
from scipy.stats import t
from binarysearchtree import BST
```

Como forma de melhor analisar a rede foi decidio incluir, além da rede da UFRN, nós dentro de um raio de 3km de distância da faculdade.

2º:Modificar os valores de setup para os desejados
```
# Setup

N = 1000000 # Tamanho máximo do vetor
steps = 10  # Número de tamanhos de vetor a testar
executions_per_size = 20  # Número de execuções por tamanho de vetor

vector_sizes = np.linspace(100, N, steps, dtype=int)

# ... 

data = np.random.randint(0, N, size)
# Crie uma árvore de pesquisa binária com os dados
    tree = BST()
    for value in data:  
        tree.add(value)
```
### Resultados
Para um melhor entendimento foi realizado uma implemetação com três valores de N diferente, N = 1000, N = 10000 e N = 100000.

#### Primeiro Gráfico (Desempenho Geral dos Algoritmos)
##### Eixos:
- O eixo x representa o tamanho do vetor (Vector Size), que varia de valores pequenos até 100.000.
- O eixo y mostra o tempo médio de execução dos algoritmos em segundos (Mean Execution Time).

##### Linhas e Barras de Erro:
- Azul (Solver Closest): O tempo médio de execução do algoritmo Solver Closest. Ele é muito pequeno (próximo a zero) em todos os tamanhos de vetor, indicando alta eficiência.
- Vermelho (Solver Kth Largest): O tempo médio de execução do algoritmo Solver Kth Largest. Ele cresce linearmente à medida que o tamanho do vetor aumenta. As barras de erro indicam a variabilidade nos tempos entre as execuções.

##### Para N = 1000
<img src="https://github.com/julianessantos/AED-II/blob/main/Unidade%202/Imagens/1000.png" alt="N = 1000" width="600" height="700"/>

##### Para N = 10000
<img src="https://github.com/julianessantos/AED-II/blob/main/Unidade%202/Imagens/10000.png" alt="N = 10000" width="600" height="700"/>

##### Para N = 100000
<img src="https://github.com/julianessantos/AED-II/blob/main/Unidade%202/Imagens/100000.png" alt="N = 100000" width="600" height="700"/>

#### Segundo Gráfico (Desempenho do Solver Closest)
##### Eixos:
- O eixo x novamente representa o tamanho do vetor (Vector Size).
- O eixo y mostra o tempo médio de execução em uma escala muito pequena (segundos).

##### Características Específicas:
- Escala de Tempo Reduzida: Este gráfico é dedicado exclusivamente ao Solver Closest, com uma escala mais sensível para observar variações pequenas.
- Curva Suave: O tempo de execução aumenta ligeiramente nos primeiros tamanhos de vetor, mas rapidamente se estabiliza em torno de um valor muito baixo.

##### Para N = 1000
<img src="https://github.com/julianessantos/AED-II/blob/main/Unidade%202/Imagens/10002.png" alt="N = 1000" width="600" height="700"/>

##### Para N = 10000
<img src="https://github.com/julianessantos/AED-II/blob/main/Unidade%202/Imagens/100002.png" alt="N = 10000" width="600" height="700"/>

##### Para N = 100000
<img src="https://github.com/julianessantos/AED-II/blob/main/Unidade%202/Imagens/1000002.png" alt="N = 100000" width="600" height="700"/>
