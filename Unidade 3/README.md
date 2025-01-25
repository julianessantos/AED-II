Análise de Grafos em Livros de Stephen King: Joyland e Depois
Problema #1
Este projeto tem como objetivo realizar uma análise de grafos para entender as interações e conexões entre os personagens dos livros Joyland e Depois de Stephen King. Utilizando técnicas de processamento de linguagem natural (NLP) e ferramentas de análise de grafos, identificamos padrões narrativos e relações entre os personagens.

Requisitos
Requisito #1
Preparação e limpeza dos textos: Extração de entidades relevantes, como personagens, utilizando técnicas de NLP (PoS Tagging e NER).
Construção dos grafos: Nós representam personagens e arestas representam interações baseadas na coocorrência em parágrafos ou cenas.
Métricas e análises:
Degree Centrality: Identifica personagens mais conectados.
Closeness Centrality: Mede a proximidade de um personagem em relação a todos os outros.
Betweenness Centrality: Identifica personagens que servem como pontes entre clusters.
Eigenvector Centrality: Mede a influência de um personagem com base nas conexões de suas conexões.
Requisito #2
Visualizações interativas:
Criação de grafos com clusters coloridos e destaques para personagens centrais.
Comparação da estrutura de conexões entre os dois livros.
Análise narrativa:
Joyland: Rede mais densa e conectada, com Devin Jones como centro.
Depois: Rede mais esparsa e linear, com Jamie Conklin como protagonista central.
Estrutura do Repositório
lua
Copiar
Editar
/
|-- notebooks/
|   |-- graph_analysis.ipynb     # Construção e análise dos grafos
|
|-- figures/                     # Visualizações geradas dos grafos
|-- README.md                    # Este documento
|-- requirements.txt             # Dependências do projeto

Como Executar
Clonar o repositório

bash
Copiar
Editar
git clone https://github.com/seu_usuario/seu_repositorio.git
cd seu_repositorio
Instalar as dependências Crie um ambiente virtual (opcional) e instale as dependências listadas no arquivo requirements.txt:

bash
Copiar
Editar
pip install -r requirements.txt
Executar os notebooks Abra os notebooks e execute as células para reproduzir as análises:

bash
Copiar
Editar
jupyter notebook
Resultados e Conclusão
Joyland
Personagem central: Devin Jones, com alta centralidade em todas as métricas.
Clusters principais: Formados por colegas de trabalho e moradores de Heaven's Bay.
Densidade: A trama apresenta uma rede mais conectada, destacando a importância das interações entre personagens.
Depois
Personagem central: Jamie Conklin, com alta centralidade de grau e betweenness.
Clusters principais: Menor quantidade de clusters, refletindo a narrativa linear.
Densidade: Rede esparsa, destacando a solidão do protagonista em sua jornada.
Comparação
Os grafos de Joyland e Depois mostram diferenças claras na complexidade narrativa:

Joyland é mais interativo e comunitário.
Depois foca em um arco narrativo mais individualizado.
As figuras geradas estão disponíveis na pasta figures/ e mostram detalhes das redes de cada livro, incluindo visualizações interativas e análises de centralidade.

Link para o Vídeo Explicativo
O vídeo explicativo detalhando o processo de análise está disponível aqui.