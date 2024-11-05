### Departamento de Engenharia de Computação e Automação
#### Algoritmo e Estrutura de Dados II (DCA3702)
#### Trabalho 5

Usando como fonte os notebooks do [OSMnx](https://github.com/gboeing/osmnx) e a documentação da biblioteca, o quinto projeto tem como objetivo avaliar a mobilidade no entorno da UFRN, em Natal-RN, com o intuito de analisar os melhores locais para a implementação de dock-station(S) de compartilhamento de bicicletas no enterno da universidade.

O projeto final foi realizado de maneira individual. Além dos codigo é possivel observar uma breve explicação do trabalho no [video](URL) salvo na plataforma Loom.

#### 🎯 Objetivos
- [x] Baixar a rede viária da UFRN
- [x] Análise do requisitos solicitados 

> [!WARNING]
> Para a realização do projeto é necessário realizar alguns passos iniciais.

1º: Intalação da biblioteca 
```
pip install osmnx
```

Como forma de melhor analisar a rede foi decidio incluir, além da rede da UFRN, nós dentro de um raio de 3km de distância da faculdade.
2º: Download da rede viária
```
# Baixar a rede viária para bike da UFRN incluindo nós dentro de 3 km ao longo da rede a partir do endereço
G = ox.graph_from_address(
    address="Universidade Federal do Rio Grando do Norte, Natal, RN",
    dist=3000,
    dist_type="network",
    network_type="bike",
)
fig, ax = ox.plot_graph(G, figsize=(10, 10), node_size=5, edge_color="y", edge_linewidth=0.2)
```

![Rede viária escolhida](https://github.com/julianessantos)