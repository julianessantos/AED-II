### Departamento de Engenharia de Computação e Automação
#### Algoritmo e Estrutura de Dados II (DCA3702)
#### Trabalho 4

Usando como fonte os notebooks do [OSMnx](https://github.com/gboeing/osmnx) e a documentação da biblioteca, o quarto projeto tem como objetivo criar um exemplo que use de alguma forma a rede, ou parte dela, referente a cidade de Natal-RN. Além de criar a rede, o trabalho propoem elaborar perguntas cujas as respostas podem ser respondidas com as métricas estudadas durante as aulas, tais como Cycles, Average Shortest Path Length, Diameter of Network, Shortest Path Length, Connected Components, Giant Connected Components, number connected components, BFS, DFS, SCC, WCC, Clustering Coefficient.

O quarto trabalho foi realizado de maneira individual. Além dos codigo é possivel observar uma breve explicação do trabalho no [video](URL) salvo na plataforma Loom.

#### 🎯 Objetivos
- [x] Baixar a rede viária de Felipe Camarão
- [x] Análise de algumas métricas

> [!WARNING]
> Para a realização do projeto é necessário realizar alguns passos iniciais.

1º Intalação da biblioteca 
```
pip install osmnx
```

Você pode checar se a instalação foi bem sucedida utilizando o código a seguir
```
import networkx as nx
import osmnx as ox

ox.__version__
```

2º Download da rede viária
```
# Download dos dados da rede viária do bairro de Felipe Camarão
G = ox.graph_from_place("Felipe Camarão ,Natal, Rio Grande do Norte, Brasil", network_type="drive") # Visualização para veículos motorizados (carros, caminhões, motos, etc.).

# Personalizando o grafo
fig, ax = ox.plot_graph(
    G,
    node_color="red",        # Cor dos nós
    node_size=5,             # Tamanho dos nós
    edge_color="blue",       # Cor das arestas
    edge_linewidth=0.8,      # Largura das arestas
    bgcolor="lightgray"      # Cor de fundo do gráfico
)
```