import pandas as pd
import matplotlib.pyplot as plt
import networkx as nx
from networkx.algorithms import bipartite

en1 = input('Digite o nome do arquivo: ')
en2 = input('Digite o nome da coluna 1: ')
en3 = input('Digite o nome da coluna 2: ')


arquivo = open(en1)

resultado = pd.read_csv(arquivo)

#lê o arquivo em pandas e transforma num grafo G
G = nx.from_pandas_edgelist(resultado, source = en2, target = en3, edge_attr=None, create_using=nx.Graph)


#divide o grado em dois conjuntos de nós, configurando visualmente um grafo bipartido
X, Y = bipartite.sets(G)
pos = dict()
pos.update( (n, (1, i)) for i, n in enumerate(X) ) # put nodes from X at x=1
pos.update( (n, (2, i)) for i, n in enumerate(Y) ) # put nodes from Y at x=2
nx.draw(G, pos=pos, with_labels= True
        )



# d = conectancia direcionada / nd = conectancia não direcionada
n = G.number_of_nodes()
m = G.number_of_edges()

d = m/(n*(n-1))

nd = (2*m)/(n*(n-1))





plt.show()
