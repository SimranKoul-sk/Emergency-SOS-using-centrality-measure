# Emergency-SOS-using-centrality-measure
This whole project is based on centrality and how it can be effectively used in daily life during emergency situations. Here , in this project,  every person acts as a node. So when a person contacts an appropriate center which will multicast to different other nodes,  this means that when a node will contact an appropriate center which will multicast to other nodes so that help may reach the emergency critical situation as soon as possible. The person who receives the message of the individual in need should neither have a very small group of people linked to him/her that not everyone will be aware,  and neither a very large group of people resulting in denial of service . This means that an appropriate center will be one which has neither a very small centrality that not everyone who need to know wouldn't be aware, and neither a very large centrality which may result in a denial of service towards the individual in need. This centrality measure is a practical approach to problems which can be as casual as a punctured tire or as serious as someone's life. This measure ,if applied seriously, can make sure that people get help when in need and hence reduce crime in extreme cases.
This centrality measure can act as a life guard in situations that people may not be able to comprehend with. This may save them from life threatening situations . When an individual is in trouble and has no one to ask for help in their surroundings,  they can inform a particular node and that node makes sure that the message is circulated and hence help is provided within no time. This, if put to extreme and professional use, can reduce criminal cases and also help women who need help if they feel that they are being stalked or in some cases prevent rapes to a large extent. This measure can actually be put to a great use and solve numerous problems. People won't be worrying if there phones run out of batteries, as they have already informed a particular node and are certain that through this effective measure, a help will  be provided to them for sure. They will feel safe and secure if we use this centrality measure and bring them safety and security.

WORK DONE AND IMPLEMENTATION
METHODOLOGY USED:
Firstly , a dataset is made by using the kaggle.com which has predefined datasets. This will consist of names and birth significance ,birth year ,death year etc and its target node. Thus the nodes will be evaluated using different measures.
The dataset will consist of the distances between nodes with a direct path between them. For nodes that have only indirect paths between them, the shortest path will be calculating by adding the distances of the edges in this path. 
Analysis will be done on the basis of:
1.	Degree
2.	Betweenness 
3.	Closeness 
Using this top 20 nodes will be  listed out. So anyone if in an emergency can reachc out to anyone of them for help.
There is also a visualization tool called GEPHI which we will be using for a proper see through of the project.

DATASET USED
a.The reference data set being used is taken from kaggle.
b.Our project is an innovative self created idea, not referenced from anywhere else. The justification of validity of need of such a project, lies in the immense time shortage and immediate action requirement during critical emergency times.
HARDWARE AND SOFTWARE REQUIREMENTS
A laptop/desktop with 4GB of ram along with a java 1.8 or higher , python idle 3.7 and networkx library.
Tools used:
The only tool we have sed comprises of gephi graph visualization which consist of jdk home prompt and several python libraries.

RUNNING CODE
import csv                                                             
import networkx as nx
from operator import itemgetter
import community

# Read in the nodelist file
with open('quakers_nodelist.csv', 'r') as nodecsv:                 
    nodereader = csv.reader(nodecsv)                                       
    nodes = [n for n in nodereader][1:]                                    

# Get a list of just the node names (the first item in each row)
node_names = [n[0] for n in nodes]                                       

# Read in the edgelist file
with open('quakers_edgelist.csv', 'r') as edgecsv:                         
    edgereader = csv.reader(edgecsv)                                   
    edges = [tuple(e) for e in edgereader][1:]                         

# Print the number of nodes and edges in our two lists
print(len(node_names))  
print(len(edges))                                                                               

G = nx.Graph() # Initialize a Graph object                                                        
G.add_nodes_from(node_names) # Add nodes to the Graph                             
G.add_edges_from(edges) # Add edges to the Graph  
print(nx.info(G)) # Print information about the Graph

hist_sig_dict = {}
gender_dict = {}
birth_dict = {}
death_dict = {}
id_dict = {}

for node in nodes: # Loop through the list, one row at a time
    hist_sig_dict[node[0]] = node[1]
    gender_dict[node[0]] = node[2]
    birth_dict[node[0]] = node[3]
    death_dict[node[0]] = node[4]
    id_dict[node[0]] = node[5]

nx.set_node_attributes(G, hist_sig_dict, 'historical_significance')
nx.set_node_attributes(G, gender_dict, 'gender')
nx.set_node_attributes(G, birth_dict, 'birth_year')
nx.set_node_attributes(G, death_dict, 'death_year')
nx.set_node_attributes(G, id_dict, 'sdfb_id')

for n in G.nodes(): # Loop through every node, in our data "n" will be the name of the person
    print(n, G.node[n]['birth_year']) # Access every node by its name, and then by the attribute "birth_year"

density = nx.density(G)
print("Network density:", density)

fell_whitehead_path = nx.shortest_path(G, source="Margaret Fell", target="George Whitehead")

print("Shortest path between Fell and Whitehead:", fell_whitehead_path)

print("Length of that path:", len(fell_whitehead_path)-1)


print(nx.is_connected(G))

# Next, use nx.connected_components to get the list of components,
# then use the max() command to find the largest one:
components = nx.connected_components(G)
largest_component = max(components, key=len)

# Create a "subgraph" of just the largest component
# Then calculate the diameter of the subgraph, just like you did with density.
#

subgraph = G.subgraph(largest_component)
diameter = nx.diameter(subgraph)
print("Network diameter of largest component:", diameter)

triadic_closure = nx.transitivity(G)
print("Triadic closure:", triadic_closure)

degree_dict = dict(G.degree(G.nodes()))
nx.set_node_attributes(G, degree_dict, 'degree')

print(G.node['William Penn'])

sorted_degree = sorted(degree_dict.items(), key=itemgetter(1), reverse=True)

print("Top 20 nodes by degree:")
for d in sorted_degree[:20]:
    print(d)

betweenness_dict = nx.betweenness_centrality(G) # Run betweenness centrality
eigenvector_dict = nx.eigenvector_centrality(G) # Run eigenvector centrality

# Assign each to an attribute in your network
nx.set_node_attributes(G, betweenness_dict, 'betweenness')
nx.set_node_attributes(G, eigenvector_dict, 'eigenvector')

sorted_betweenness = sorted(betweenness_dict.items(), key=itemgetter(1), reverse=True)
sorted_betweenness1 = sorted(eigenvector_dict.items(), key=itemgetter(1), reverse=True)
print("Top 20 nodes by betweenness centrality:")
for b in sorted_betweenness[:20]:
    print(b)
print("Top 20 nodes by eigenvector centrality:")
for b in sorted_betweenness1[:20]:
    print(b)


#First get the top 20 nodes by betweenness as a list
top_betweenness = sorted_betweenness[:20]
#First get the top 20 nodes by betweenness as a list
top_betweenness = sorted_betweenness1[:20]

#Then find and print their degree
for tb in top_betweenness: # Loop through top_betweenness
    degree = degree_dict[tb[0]] # Use degree_dict to access a node's degree, see footnote 2
    print("Name:", tb[0], "| Betweenness Centrality:", tb[1], "| Degree:", degree)
