# Análise de Grafos em Livros de Stephen King: Joyland e Depois
## 🎡Introdução
Neste artigo, iremos explorar a análise de grafos aplicada aos textos dos livros Joyland e Depois de Stephen King, com o objetivo de entender as interações e a complexidade das narrativas através de entidades e suas conexões. A utilização dos grafos irá permitir uma visão mais visual e quantitativa das relações entre personagens e os elementos do enredo, ajudando a explorar características como a densidade de personagens, as conexões entre entidades e a centralidade dos personagens na trama.

## 📌Objetivos
O principal objetivo deste estudo foi construir redes de entidades com base nos textos de Joyland e Depois, identificando as relações entre personagens, locais e organizações. A partir disso, comparamos as diferenças e semelhanças nos grafos, focando especialmente nos seguintes aspectos:

- **Conexões entre Entidades**: Análise das interações entre personagens, locais e organizações.
- **Centralidade dos Personagens**: Identificação dos personagens mais influentes na narrativa, com base na sua centralidade no grafo.

O acesso às redes interativas feitas no software Gephi podem ser visualizadas nestes dois links: [Joyland](https://julianessantos.github.io/NetworkSites/RedeJoyland/RedeNetworkJoyland/) e [Depois](https://julianessantos.github.io/NetworkSites/RedeDepois/networkDepois/)

## 📋Ferramentas Utilizadas
Para realizar essa análise, utilizamos as seguintes ferramentas e bibliotecas:

- Python: Linguagem de programação principal para processamento de dados e geração de grafos.
- spaCy: Para processamento de linguagem natural (PoS Tagging e NER), identificando e extraindo entidades do texto.
- NetworkX: Para construção e análise dos grafos, incluindo cálculo de métricas como centralidade e densidade.
- Gephi: Software utilizado para modificar e visualizar grafos de forma interativa.

## 🔎Dataset
Os dados para a construção das redes foram extraídos dos textos de ambos os livros. Entretanto, foi necessário realizar uma limpeza inicial nos arquivos .txt para uma melhor utilização dos dados presentes nos livros.

### Limpeza dos Dados
O passo inicial foi eliminar as linhas de cabeçalho e rodapé presentes nos livros, que não contribuem para a construção dos grafos. Como, caso a remoção do cabeçalho fosse feita primeiro, o número de linhas do rodapé seria modificado, iniciamos a limpeza retirando o rodapé para, logo em seguida, remover o cabeçalho.

Para a execução dessa atividade, foi aplicado um comando !sed, visível no bloco de código abaixo:
```
#Rodapé
# Para o Livro 1 (Joyland)
!sed -i '6043,6055d' Joyland_StephenKing.txt # Remove linhas 6043 a 6055
# Para o Livro 2 (Depois)
!sed -i '4676,4902d' Depois_StephenKing.txt # Remove linhas 4500 a 4550

# Cabeçalho
# Para o Livro 1 (Joyland)
!sed -i '1,105d' Joyland_StephenKing.txt # Remove linhas 1 a 105
# Para o Livro 2 (Depois)
!sed -i '1,175d' Depois_StephenKing.txt # Remove linhas 1 a 175
```
Os números e o arquivo “livro.txt” são exemplos e podem ser ajustados conforme a necessidade e tamanho do projeto.

Logo em seguida, aplicamos uma limpeza mais profunda, onde foi possível realizar a remoção de linhas vazias ou que possuem apenas espaços, a remoção de espaços extras, a normalização de espaços múltiplos entre palavras, a correção de pontuações e, por fim, a conversão de todo o texto para minúsculas.

Esse processo garantiu que os dados ficassem mais uniformes e prontos para a análise posterior. A seguir, um exemplo do comando utilizado para essas operações:

```
# Função para limpar o texto
def clean_text(file_path, output_path):
    with open(file_path, 'rt', encoding='utf-8') as file:
        lines = file.readlines()

    cleaned_lines = []
    for line in lines:
        # Remover linhas vazias ou apenas com espaços
        if not line.strip():
            continue

        # Normalizar espaços e pontuação
        line = line.strip()  # Remove espaços extras no início e fim
        line = " ".join(line.split())  # Remove espaços múltiplos entre palavras
        line = line.replace(" ,", ",").replace(" .", ".")  # Corrigir vírgulas e pontos
        line = line.replace(" ?", "?").replace(" !", "!")  # Corrigir interrogação/exclamação

        # Transformar em minúsculas (opcional, dependendo da análise futura)
        line = line.lower()

        cleaned_lines.append(line)

    # Salvar o texto limpo em um novo arquivo
    with open(output_path, 'w', encoding='utf-8') as output_file:
        output_file.write("\n".join(cleaned_lines))
    print(f"Texto limpo salvo em: {output_path}")
```
### Análise de PoS Tagging e NER
Após a limpeza, devemos realizar a identificação das categorias gramaticais (PoS) e entidades nomeadas (NER). Para isso, iremos baixar o modelo de linguagem em português maior do spaCy, denominado pt_core_news_lg. O comando para instalar e carregar o modelo é o seguinte:
```
!python -m spacy download pt_core_news_lg
```
Com isso, iremos agora realizar uma análise gramatical do texto, identificando os tipos de palavras e preparando o texto para análises mais avançadas. Vamos então utilizar o bloco de código a seguir para fazer essa extração:

```
# Carregar modelo de linguagem em português (versão maior)
nlp = spacy.load("pt_core_news_lg")

# Carregar o arquivo limpo.txt
with open('Joyland_cleaned.txt', 'r', encoding='utf-8') as file:
    text = file.read()

# Limpeza adicional dos textos (remoção de espaços extras)
joyland_cleaned = ' '.join(text.split())  # Limpeza do texto

# Processando o texto limpo
doc1 = nlp(joyland_cleaned)

# Exibindo todos os tokens no texto (sem segmentação de sentenças)
print("Tokens do texto:")
for token in doc1:
    print(f"{token.text}: {token.tag_}")  # Token e sua tag PoS
```
Logo após, iremos fazer uma filtragem para apresentar apenas as entidades específicas, sendo elas:

- ‘PER’ (pessoa),
- ‘ORG’ (organização),
- ‘GPE’ (localização geopolítica, como países ou cidades),
- ‘LOC’ (outros tipos de localizações, como regiões ou pontos geográficos),
- ‘PROPN’ (nomes próprios).
```
# Filtragem para incluir outras entidades além de 'PERSON', 'ORG', 'GPE'
print("\nEntidades nomeadas no texto Joyland (PERSON, ORG, GPE, LOC, PROPN):")
for ent in doc1.ents:
    if ent.label_ in ['PER', 'ORG', 'GPE', 'LOC', 'PROPN']:
        print(f"{ent.text}: {ent.label_}")
```
O objetivo desse código é apresentar algo semelhante a:

- Joyland: LOC
- Stephen King: PER
- Disney: ORG

## 📓Fundamentação teórica
### Como Funciona a Construção do Grafo?
Ao término do processo de limpeza do texto e extração das entidades relevantes, passamos para a construção dos grafos. Porém, é necessário uma breve explicação dos conceitos principais de um grafo e das métricas abordadas e suas explicações.

- Nós: É um ponto em um grafo. No estudo de caso, cada entidade identificada se tornou um nó no grafo.
- Arestas: É uma conexão entre dois nós em um grafo. Nesse caso, se duas entidades apareciam na mesma sentença, uma aresta era criada entre elas. Isso representava uma interação ou conexão narrativa.
Esses grafos permitem observar visualmente como as entidades estão relacionadas, identificando clusters e destacando personagens centrais.

### Métricas de um grafo
O código apresentado no início do texto dispõe de um bloco de códigos feitos especificamente para o cálculo de algumas métricas, que seria a função calcular_metricas(). São essas métricas apresentadas:
- Número de nós (Nodes): Refere-se à quantidade de vértices ou entidades presentes no grafo.
- Número de arestas (Edges): Refere-se à quantidade de conexões entre os nós do grafo.
- Centralidade de grau (Degree Centrality): Mede a importância de um nó com base no número de conexões que ele tem. Quanto maior o número de conexões, maior a centralidade de grau.
- Coeficiente de agrupamento (Clustering Coefficient): Mede a tendência dos vizinhos de um nó estarem conectados entre si.
- Hubs (nós com maior grau): São os nós com o maior número de conexões, ou seja, os mais centrais e conectados na rede.
_ Grau do Grafo (Degree of Graph): Refere-se ao número de conexões de cada nó. Quanto maior o grau, mais “importante” é o nó dentro da rede.
_ Centralidade de intermediação (Betweenness Centrality): Mede a importância de um nó com base na quantidade de caminhos mais curtos que passam por ele entre outros nós.
_ Centralidade de proximidade (Closeness Centrality): Mede a proximidade de um nó em relação a todos os outros nós do grafo.
Essas métricas ajudam a entender a estrutura e o comportamento do grafo, destacando quais nós são mais conectados, influentes ou próximos uns dos outros na rede.

## 🔎Resultados e Insights
### Redes
Partindo para a criação da rede em si, com as entidades analisadas, podemos gerar os grafos necessários para as análises. O primeiro grafo formado foi a rede completa, contendo quatro entidades principais: pessoa, organização, local e localização geopolítica.
```
# Criar um grafo direcionado
G3 = nx.Graph()

# Extrair as entidades nomeadas do texto
entities = [ent.text for ent in doc1.ents if ent.label_ in ['PER', 'ORG', 'GPE', 'LOC']]

# Adicionar as entidades como nós no grafo
G3.add_nodes_from(entities)

# Criar relações entre entidades que aparecem próximas (exemplo: na mesma sentença)
for sent in doc1.sents:
    # Extrair entidades na sentença
    ents_in_sent = [ent.text for ent in sent.ents if ent.label_ in ['PER', 'ORG', 'GPE', 'LOC']]
    # Adicionar arestas entre as entidades que aparecem na mesma sentença
    for i in range(len(ents_in_sent)):
        for j in range(i + 1, len(ents_in_sent)):
            G3.add_edge(ents_in_sent[i], ents_in_sent[j])

# Visualizando a rede
import matplotlib.pyplot as plt
plt.figure(figsize=(10, 10))
nx.draw_networkx(G3, with_labels=True, node_size=3000, node_color='skyblue', font_size=10, font_weight='bold')
plt.title("Rede de Relações entre Entidades Nomeadas")
plt.show()
```
Com o auxílio do Gephi, foi possível fazer a formatação do layout do grafo gerado. O primeiro grafo apresentado é a rede do livro Joyland. Nessa rede, conseguimos visualizar uma maior conexão entre as entidades presentes no livro, mas também vemos a presença de alguns nós soltos. No entanto, como o livro se passa em poucos espaços, a interação entre as entidades torna-se maior.

<img src="https://github.com/julianessantos/AED-II/blob/main/Unidade%203/Imagens/Rede%20NetworkJoyland.png" alt="Rede do livro Joyland." width="600" height="800"/>

Enquanto isso, o livro Depois apresenta um grafo mais complexo, com mais nós com menos de duas conexões e um grau menor de entidades conectadas entre si. Isso reflete uma história com mais personagens e cenários, resultando em uma rede mais dispersa e com interações mais distribuídas.

<img src="https://github.com/julianessantos/AED-II/blob/main/Unidade%203/Imagens/Rede%20NetworkDepois.png" alt="Rede do livro Depois." width="600" height="800"/>

Logo após, vemos a rede da entidade “localização”, onde é possível observar que, no primeiro livro, por se passar no parque de diversão Joyland, a localização com mais conexões é, consequentemente, Joyland. Analisando as métricas, rodando a função calcular_metrica() citada anteriormente e presente no código disponível, vemos que o nó Joyland possui a maior Degree Centrality da rede, indicando que é o local mais conectado e central dentro da trama, com um número elevado de interações com outras entidades.

<img src="https://github.com/julianessantos/AED-II/blob/main/Unidade%203/Imagens/RedeLOCJoyland.png" alt="Rede da entidade “localização” para o primeiro livro." width="600" height="800"/>

Em contrapartida, a rede do segundo livro apresenta uma maior variedade de comunidades, demonstrando um número mais elevado de locais mencionados ao longo do enredo. Além disso, ao analisar suas métricas, é possível observar valores mais próximos entre si, o que reflete a diversificação dos locais e a descentralização em relação a um único ambiente predominante.

<img src="https://github.com/julianessantos/AED-II/blob/main/Unidade%203/Imagens/RedeLOCDepois.png" alt="Rede da entidade “localização” para o segundo livro." width="600" height="800"/>

Comentando sobre a rede de pessoas, a próxima rede destaca esses dados. Na primeira trama, o personagem Mike se destaca como um dos principais, com mais conexões, o que reflete sua importância narrativa e suas interações frequentes com outros personagens ao longo da história. Isso é visível no grafo, onde ele aparece como um nó central, com um alto grau de conectividade.

Por outro lado, Dev, apesar de ser um personagem relevante na história, não ocupa o papel de personagem central na rede. Isso pode ser explicado pelo fato de que suas interações estão mais concentradas em subgrupos ou comunidades específicas.

Essa descentralização do papel de Dev pode ser um reflexo direto da maneira como a narrativa foi estruturada, priorizando Mike como um elemento chave de conexão e desenvolvimento da história.

<img src="https://github.com/julianessantos/AED-II/blob/main/Unidade%203/Imagens/Rede%20Ego2Joyland.png" alt="Rede da entidade “Pessoas” para o primeiro livro." width="600" height="800"/>

Aqui está um grafo baseado na rede ego do personagem Mike.

<img src="https://github.com/julianessantos/AED-II/blob/main/Unidade%203/Imagens/Rede%20EgoJoyland.png" alt="Rede ego para o personagem Mike." width="600" height="800"/>

Para a segunda história, conseguimos observar como Liz, uma das personagens principais, também se destaca mais do que o personagem central, Jamie. Essa análise pode ser explicada pelo fato de Liz estar envolvida em diversas interações ao longo da trama, tanto com Jamie quanto com outros personagens, como a mãe dele, Tia, e outras figuras centrais do enredo.

<img src="https://github.com/julianessantos/AED-II/blob/main/Unidade%203/Imagens/Rede%20Ego2Depois.png" alt="Rede da entidade “pessoas” para o segundo livro." width="600" height="800"/>

Aqui está o grafo para o ego principal, Liz.
<img src="https://github.com/julianessantos/AED-II/blob/main/Unidade%203/Imagens/Rede%20EgoDepois.png" alt="Rede ego para a personagem Liz." width="600" height="800"/>

## Insights
A análise revelou algumas diferenças importantes entre os dois livros de King, especialmente no que diz respeito à estrutura das interações entre personagens e o papel que os locais e eventos desempenham na trama.

- Densidade: Joyland apresenta um grafo mais compacto, com interações limitadas e uma narrativa mais focada, enquanto Depois tem um grafo mais complexo, com mais nós com menos de duas conexões refletindo uma história com mais personagens e cenários.
- Conexões: As interações em Joyland são mais diretas e centralizadas no parque, enquanto Depois tem uma trama mais dispersa, com personagens interagindo em diferentes locais e eventos.
- Centralidade: Em Joyland, a centralidade foi dominada pelo personagem Mike, enquanto em Depois, a centralidade é mais distribuída entre vários personagens, especialmente aqueles envolvidos com os eventos sobrenaturais.
## Links Relevantes
- Grafo Interativo: Acesse os grafos gerados para [Joyland](https://julianessantos.github.io/NetworkSites/RedeJoyland/RedeNetworkJoyland/) e [Depois](https://julianessantos.github.io/NetworkSites/RedeDepois/networkDepois/) e explore as interações entre os personagens.
- [Podcast Explicativo](https://notebooklm.google.com/notebook/5be3c582-cad2-48f0-9486-3e2081f6fbca/audio): Um podcast que explora os principais conceitos e abordagens utilizados nesta análise de grafos.