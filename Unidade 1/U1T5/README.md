### Departamento de Engenharia de Computação e Automação
#### Algoritmo e Estrutura de Dados II (DCA3702)
#### Trabalho 5

Usando como fonte os notebooks do [OSMnx](https://github.com/gboeing/osmnx) e a documentação da biblioteca, o quinto projeto tem como objetivo avaliar a mobilidade no entorno da UFRN, em Natal-RN, com o intuito de analisar os melhores locais para a implementação de dock-station(S) de compartilhamento de bicicletas no enterno da universidade.

O projeto final foi realizado de maneira individual. Além dos codigo é possivel observar uma breve explicação do trabalho no [video](https://www.loom.com/share/65226a7974b34bdaa5b53db2ade94c15?sid=fc75173f-ed7b-4660-8860-17c211dd0dee) salvo na plataforma Loom.

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

![Rede viária escolhida](https://github.com/julianessantos/AED-II/blob/main/Unidade%201/U1T5/Imagens/RedeViaria.png)

### Requisito 1 - Métricas de centralidade
#### Centralidade de Grau
A centralidade de grau (ou degree centrality) é uma métrica de análise de redes que mede o número de conexões diretas (arestas) que cada nó possui. Em um grafo que representa uma rede viária, como o da imagem, cada nó representa uma interseção (cruzamento de ruas) e cada aresta representa uma rua que conecta duas interseções.

<img src="https://github.com/julianessantos/AED-II/blob/main/Unidade%201/U1T5/Imagens/CentralidadeDeGrau.png" alt="Centralidade de Grau" width="600" height="700"/>

No caso da rede escolhida, os nós em roxo indicam uma centralidade de grau menor (menos conexões ou menor importância na rede viária). Enquanto, os nós em amarelo possuem maior centralidade de grau, indicando pontos de maior conexão e, possivelmente, áreas mais movimentadas ou interseções centrais.

#### Centralidade de Proximidade
A centralidade de proximidade (ou closeness centrality) é uma medida que indica o quão próximo um nó está de todos os outros nós na rede. Em outras palavras, ela avalia a acessibilidade de um nó, considerando a soma das menores distâncias entre ele e todos os outros nós. Ele ajuda a identificar quais interseções (nós) estão mais “próximas” de todas as outras em termos de distância geodésica, ou seja, menor número de ruas necessárias para chegar a qualquer outro ponto da rede.

<img src="https://github.com/julianessantos/AED-II/blob/main/Unidade%201/U1T5/Imagens/CentralidadeDeProximidade.png" alt="Centralidade de Proximidade" width="600" height="700"/>

Na rede vistas os nós em tons mais claros (amarelos) têm uma centralidade de proximidade mais alta, o que significa que são interseções com acessibilidade vantajosa, possivelmente no centro do bairro ou em pontos de convergência de várias ruas. Esses nós estão em uma posição central dentro da rede e podem ser alcançados mais rapidamente a partir de qualquer outro nó. Diferente dos nós em tons mais escuros (roxo/preto), ou seja, estes nós têm centralidade de proximidade mais baixa, o que indica que estão em regiões menos conectadas ou na periferia da área analisada. Eles provavelmente precisam de mais etapas (ou ruas) para acessar a maioria dos outros pontos da rede.

#### Centralidade de Intermediação
A centralidade de intermediação (ou betweenness centrality) é uma métrica que mede a frequência com que um nó atua como um ponto de passagem em caminhos mínimos entre outros nós da rede. Em termos simples, ela indica a importância de um nó como uma “ponte” ou um ponto crítico para o fluxo de informação ou movimento dentro do grafo.

<img src="https://github.com/julianessantos/AED-II/blob/main/Unidade%201/U1T5/Imagens/CentralidadeDeIntemidiacao.png" alt="Centralidade de Intermediação" width="600" height="700"/>

Nós em tons mais claros (amarelos e verdes) têm uma alta centralidade de intermediação, significando que eles atuam como pontos de passagem chave na rede. Já os nós em tons mais escuros (roxos) têm baixa centralidade de intermediação, o que indica que são menos importantes para a conectividade geral da rede. Eles estão frequentemente localizados nas periferias ou em ruas que não servem como rotas principais de tráfego.

#### Centralidade de Autovetor
A centralidade de autovetor mede a importância de um nó na rede não apenas pela quantidade de conexões que ele possui, mas também pela importância dos nós aos quais ele está conectado. Ou seja,um nó conectado a outros nós altamente conectados terá uma alta centralidade de autovetor. Isso cria um efeito de "prestígio" ou "influência", onde os nós que estão próximos de outros nós centrais se tornam mais importantes.

<img src="https://github.com/julianessantos/AED-II/blob/main/Unidade%201/U1T5/Imagens/CentralidadeDeAutovetor.png" alt="Centralidade de Autoveto" width="600" height="700"/>

No grafo da rede os nós com tons mais claros (como amarelo ou verde claro) representam locais com alta centralidade de autovetor. Esses pontos são importantes para a estrutura da rede, pois estão conectados a outros nós influentes e com grande fluxo. Diferente dos nós em tons mais escuros (como roxo).

### Requisito 2 - PDF e CDF
#### Curva de Densidade de Probabilidade (PDF)
Representa uma estimativa da distribuição contínua dos graus. Ajuda a entender a frequência relativa dos graus em relação a toda a rede, indicando quais graus são mais comuns.

![PDF](https://github.com/julianessantos/AED-II/blob/main/Unidade%201/U1T5/Imagens/PDF.png)

O grau mais frequente na rede é em torno de 6, indicando que a maioria dos nós tende a ter aproximadamente 6 conexões.

#### Função de Densidade Cumulativa (CDF)
A CDF pode ser muito útil para analisar a conectividade da rede. Ao observar como a CDF se comporta, você pode inferir se a maioria dos nós tem um número baixo de conexões ou se há muitos nós altamente conectados.

![CDF](https://github.com/julianessantos/AED-II/blob/main/Unidade%201/U1T5/Imagens/CDF.png)

A curva da CDF se estabiliza perto de 1 (ou 100%) após o grau 8, o que sugere que poucos nós têm graus superiores a este valor.

### Requisito 3 - Analisando a Matriz de Correlação das Métricas de Centralidade
#### Analisando a Matriz de Correlação das Métricas de Centralidade
- A diagonal principal mostra a distribuição de cada métrica individualmente. A forma da distribuição (normal, bimodal, etc.) pode indicar características particulares da rede. Por exemplo, uma distribuição de grau com uma cauda longa sugere a presença de poucos nós com muitas conexões.

- A sobreposição das distribuições pode indicar que algumas métricas estão capturando informações semelhantes. Por exemplo, se a distribuição de degree e betweenness forem altamente sobrepostas, isso pode indicar que os nós com alto degree também tendem a ter alto betweenness.

Correlações: Os valores fora da diagonal principal representam as correlações entre pares de métricas. Um valor próximo de 1 indica uma correlação positiva forte, ou seja, quando uma métrica aumenta, a outra também tende a aumentar. Um valor próximo de -1 indica uma correlação negativa forte, ou seja, quando uma métrica aumenta, a outra tende a diminuir. Um valor próximo de 0 indica que não há correlação entre as métricas.

Interpretação das Correlações:

- Degree e Betweenness: Uma correlação positiva forte indica que os nós com mais conexões (alto degree) tendem a estar nos caminhos mais curtos entre outros nós (alto betweenness). Isso é esperado, pois nós com muitas conexões geralmente estão bem posicionados para conectar diferentes partes da rede.

- Closeness e Betweenness: Uma correlação positiva moderada indica que os nós que estão próximos de todos os outros (alto closeness) também tendem a estar nos caminhos mais curtos entre outros nós (alto betweenness). Isso também é esperado, pois nós centrais tendem a ter alta closeness e betweenness.
  
![MCMC](https://github.com/julianessantos/AED-II/blob/main/Unidade%201/U1T5/Imagens/Matriz%20de%20Correla%C3%A7%C3%A3o%20das%20M%C3%A9tricas%20de%20Centralidade.png)

### Requisito 4 - Quem é o core/shell da rede?
O conceito de core/shell se refere à estrutura da rede, onde os nós no core são aqueles que têm uma alta conectividade (ou centralidade), enquanto os nós no shell são aqueles que têm uma conectividade mais baixa.

- Os nós do core (vermelhos) são os mais conectados na rede. Eles têm um alto número de conexões (grau) e desempenham um papel crucial na estrutura da rede. Em um contexto de mobilidade, isso significa que esses locais são mais acessíveis e podem servir como pontos de partida ou chegada importantes para um sistema de compartilhamento de bicicletas. Colocar dock-stations nesses pontos pode maximizar a utilização do sistema. Shell:

- Os nós do shell (azul) têm uma conectividade mais baixa e estão nas bordas da rede. Eles podem representar áreas que têm menos acesso a rotas principais ou que não são frequentemente usadas. Embora possam não ser pontos de acesso principais, ainda são importantes para a conectividade da rede, pois ajudam a conectar áreas menos centrais. A inclusão de dock-stations em alguns desses locais pode incentivar o uso de bicicletas em áreas menos exploradas.

![coreshell](https://github.com/julianessantos/AED-II/blob/main/Unidade%201/U1T5/Imagens/coreshell%20da%20rede.png)

## Resultados

As análises indicaram a distribuição da mobilidade e conectividade ao redor da UFRN, destacando bairros como Candelária e Capim Macio, que apresentaram altos índices de centralidade. Com base nas métricas, foram identificados locais potenciais para a instalação de dock-stations de bicicletas compartilhadas, levando em conta áreas com elevada conectividade e proximidade apresentadas nas analises do requisito 1.
