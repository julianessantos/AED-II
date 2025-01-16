# Avaliação do Algoritmo de Dijkstra e MST em Natal-RN

## Problema #1
Este projeto tem como objetivo avaliar o algoritmo de Dijkstra utilizando duas implementações diferentes:
- **Dijkstra com Min Heap** (implementado no arquivo `dijkstra_min_heap.ipynb`)
- **Dijkstra do NetworkX**

A visualização dos resultados é feita utilizando a biblioteca **OSMnx**, que permite traçar os caminhos encontrados no mapa da cidade de **Natal-RN**.

## Requisitos

### Requisito #1
- Selecionar **10 pares de pontos de interesse** (origem e destino) dentro da cidade de Natal-RN.
- Avaliar e comparar os caminhos encontrados pelos algoritmos de Dijkstra (**Min Heap e NetworkX**).
- Visualizar os resultados no **OSMnx** para uma melhor compreensão das diferenças entre as abordagens.

### Requisito #2
- A partir dos pontos de interesse escolhidos, calcular a **Árvore Geradora Mínima (MST - Minimum Spanning Tree)**.
- Utilizar o notebook `kruskal_natal.ipynb` como referência.

## Estrutura do Repositório
```
/
|-- dijkstra_min_heap.ipynb   # Implementação do algoritmo de Dijkstra com Min Heap
|-- kruskal_natal.ipynb       # Cálculo da MST para pontos de interesse
|-- figures/                  # Visualizações geradas
|-- README.md                 # Este documento
|-- video_link.txt            # Link para o vídeo explicativo
```

## Como Executar
### 1. Clonar o repositório
```bash
git clone https://github.com/seu_usuario/seu_repositorio.git
cd seu_repositorio
```

### 2. Instalar dependências
Crie um ambiente virtual (opcional) e instale as dependências:
```bash
pip install -r requirements.txt
```

### 3. Executar os notebooks
Abra um dos notebooks e execute as células para visualizar os resultados:
```bash
jupyter notebook
```

## Resultados e Conclusão
O algoritmo de Dijkstra é amplamente usado para encontrar o caminho mais curto em um grafo. Ele sempre escolhe o nó com o menor custo acumulado.
No projeto, estamos usando duas implementações diferentes:
- A implementação pronta do NetworkX, que usa otimizadores subjacentes
- Uma implementação personalizada baseada em Min Heap, que nos dá mais controle e flexibilidade

Os resultados das avaliações são documentados e comparados visualmente nos mapas gerados pelo **OSMnx**. 

A figura a seguir apresenta o resultado de um dos 10 pares selecionados, Ponta Negra → Shopping Midway Mall, onde o caminho em vermelho é a representação da implementação do min-heap. Além dessa visulização, temos a apresentação dos tempos de execução para o cálculo do caminho mais curto com NetworkX e Min Heap, permitindo uma comparação de eficiência.

<img src="https://github.com/julianessantos/AED-II/blob/main/Unidade%202/Imagens/100000.png" alt="Ponta Negra → Shopping Midway Mall" width="1000" height="600"/>

Calculando caminho entre 505055020 e 502752741
NetworkX Dijkstra: 0.0494 segundos
Min Heap Dijkstra: 0.0338 segundos

Percebemos que nesse caso o algoritimo com menor tempo foi o Min Heap. Em outros casos, temos o NetworkX como a melhor forma de implementação.

Já o algoritmo de Kruskal é eficiente para encontrar a MST ao classificar as arestas pelo peso e adicionar as menores, desde que não formem ciclos. Onde uma MST é uma subárvore que conecta todos os nós do grafo com o menor custo total, sem formar ciclos. É amplamente utilizada em problemas de design de redes, como distribuição de energia e transporte."
Algoritmo de Kruskal:

A solução inclui a geração da **MST (Minimum Spanning Tree)** para um conjunto de estações de trem. Onde é apresentendo na seguinte figura o menor caminho gerado por essa arvore ligando os pontos em analise.

<img src="https://github.com/julianessantos/AED-II/blob/main/Unidade%202/Imagens/100000.png" alt="Ponta Negra → Shopping Midway Mall" width="1000" height="600"/>

