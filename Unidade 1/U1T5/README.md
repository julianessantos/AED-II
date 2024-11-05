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
<<<<<<< HEAD:Unidade 1/U1T5/Trabalho5.md

### Requisito 1 - Métricas de centralidade
#### Centralidade de Grau
A centralidade de grau (ou degree centrality) é uma métrica de análise de redes que mede o número de conexões diretas (arestas) que cada nó possui. Em um grafo que representa uma rede viária, como o da imagem, cada nó representa uma interseção (cruzamento de ruas) e cada aresta representa uma rua que conecta duas interseções.

![Rede viária escolhida](https://github.com/julianessantos)

No caso da rede escolhida, os nós em roxo indicam uma centralidade de grau menor (menos conexões ou menor importância na rede viária). Enquanto, os nós em amarelo possuem maior centralidade de grau, indicando pontos de maior conexão e, possivelmente, áreas mais movimentadas ou interseções centrais.

#### Centralidade de Proximidade
A centralidade de proximidade (ou closeness centrality) é uma medida que indica o quão próximo um nó está de todos os outros nós na rede. Em outras palavras, ela avalia a acessibilidade de um nó, considerando a soma das menores distâncias entre ele e todos os outros nós. Ele ajuda a identificar quais interseções (nós) estão mais “próximas” de todas as outras em termos de distância geodésica, ou seja, menor número de ruas necessárias para chegar a qualquer outro ponto da rede.

![Rede viária escolhida](https://github.com/julianessantos)

Na rede vistas os nós em tons mais claros (amarelos) têm uma centralidade de proximidade mais alta, o que significa que são interseções com acessibilidade vantajosa, possivelmente no centro do bairro ou em pontos de convergência de várias ruas. Esses nós estão em uma posição central dentro da rede e podem ser alcançados mais rapidamente a partir de qualquer outro nó. Diferente dos nós em tons mais escuros (roxo/preto), ou seja, estes nós têm centralidade de proximidade mais baixa, o que indica que estão em regiões menos conectadas ou na periferia da área analisada. Eles provavelmente precisam de mais etapas (ou ruas) para acessar a maioria dos outros pontos da rede.

#### Centralidade de Intermediação
A centralidade de intermediação (ou betweenness centrality) é uma métrica que mede a frequência com que um nó atua como um ponto de passagem em caminhos mínimos entre outros nós da rede. Em termos simples, ela indica a importância de um nó como uma “ponte” ou um ponto crítico para o fluxo de informação ou movimento dentro do grafo.

![Rede viária escolhida](https://github.com/julianessantos)

Nós em tons mais claros (amarelos e verdes) têm uma alta centralidade de intermediação, significando que eles atuam como pontos de passagem chave na rede. Já os nós em tons mais escuros (roxos) têm baixa centralidade de intermediação, o que indica que são menos importantes para a conectividade geral da rede. Eles estão frequentemente localizados nas periferias ou em ruas que não servem como rotas principais de tráfego.

#### Centralidade de Autovetor
A centralidade de autovetor mede a importância de um nó na rede não apenas pela quantidade de conexões que ele possui, mas também pela importância dos nós aos quais ele está conectado. Ou seja,um nó conectado a outros nós altamente conectados terá uma alta centralidade de autovetor. Isso cria um efeito de "prestígio" ou "influência", onde os nós que estão próximos de outros nós centrais se tornam mais importantes.

![Rede viária escolhida](https://github.com/julianessantos)

No grafo da rede os nós com tons mais claros (como amarelo ou verde claro) representam locais com alta centralidade de autovetor. Esses pontos são importantes para a estrutura da rede, pois estão conectados a outros nós influentes e com grande fluxo. Diferente dos nós em tons mais escuros (como roxo).

### Requisito 2 - PDF e CDF

### Requisito 3 - Analisando a Matriz de Correlação das Métricas de Centralidade

### Requisito 4 - Quem é o core/shell da rede?
=======
>>>>>>> 6a1177316d435deeae2b006e7770c64e6be4fe8c:Unidade 1/U1T5/README.md
