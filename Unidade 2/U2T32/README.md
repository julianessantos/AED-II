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
- Organizar este repositório no **GitHub**, incluindo:
  - Códigos
  - Figuras e visualizações geradas
  - Explicações sobre a solução adotada
  - Arquivo `README.md` (este documento)
- Criar um **vídeo explicativo (até 5 minutos)** demonstrando a solução e os resultados obtidos.
- Disponibilizar o link do vídeo no repositório.

### Requisito #3
- A partir dos pontos de interesse escolhidos, calcular a **Árvore Geradora Mínima (MST - Minimum Spanning Tree)**.
- Utilizar o notebook `kruskal_natal.ipynb` como referência.
- Como **PoIs (Points of Interest)**, utilizar as **estações de trem de Natal-RN**.

## Estrutura do Repositório
```
/
|-- dijkstra_min_heap.ipynb   # Implementação do algoritmo de Dijkstra com Min Heap
|-- networkx_dijkstra.ipynb   # Uso do algoritmo de Dijkstra com NetworkX
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
Os resultados das avaliações são documentados e comparados visualmente nos mapas gerados pelo **OSMnx**. 
A solução também inclui a geração da **MST (Minimum Spanning Tree)** para um conjunto de pontos de interesse.

Mais detalhes podem ser encontrados nos notebooks e na documentação do projeto.

---
**Autores:** Seu Nome | Contato | [GitHub](https://github.com/seu_usuario)
