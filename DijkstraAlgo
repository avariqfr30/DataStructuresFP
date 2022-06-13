#include<iostream>
#include<queue>
#include<stack>
#include <limits>
#define INFINITY 9999

using namespace std;

class Graph {
    private:
    // define Graph parameters
        int **adjMatrix;
        int vCount;

	    int *key;
	    // if a node's key is 1, it means that the node is already a part of the Minimum Spanning Tree
	    int *distance;
	    // if the parent is -1, it means the node has no parent
	    int *parent;

    public:
    // define functions
        Graph(int vCount);
        ~Graph();
	    void addEdge(int i, int j, int cost);
	    void removeEdge(int i, int j);
        int isEdge(int i, int j);
        void display();
	    void initState();
	    void showBasicInfo();
	    void Dijkstra(int startNode);
	    bool isAllKeyTrue();  // 0 means not MST yet, 1 means MST
	    int findMinDisNode();

};
Graph::Graph(int vCount) {
    this->vCount = vCount;

	this->key = new int[vCount];
	this->distance = new int[vCount];
	this->parent = new int[vCount];

    adjMatrix = new int*[vCount];
    for (int i = 0; i < vCount; i++) {
        adjMatrix[i] = new int[vCount];
           for (int j = 0; j < vCount; j++)
              adjMatrix[i][j] = 0;
    }
}
Graph::~Graph() {
    for (int i = 0; i < vCount; i++)
        delete[] adjMatrix[i];
        delete[] adjMatrix;
}
void Graph::initState(){
	for(int i=0; i<this->vCount; i++) {
		this->key[i] = 0; // 0 means node is not in MST, 1 means node is in MST
		this->distance[i]= INFINITY; // distance is set to infinity initially
		this->parent[i] = -1;  // -1 means node has no parent
		                       //
	}
}
// add weighted edge to directed graph
void Graph::addEdge(int i, int j, int cost) {
    if (i >= 0 && i < vCount && j >= 0 && j < vCount) {
		adjMatrix[i][j] = cost;
    }
}
// remove weighted edge from directed graph
void Graph::removeEdge(int i, int j) {
    if (i >= 0 && i < vCount && j >= 0 && j < vCount) {
		adjMatrix[i][j] = 0;
		adjMatrix[j][i] = 0;
    }
}
// checks if an edge exists between two nodes
int Graph::isEdge(int i, int j) {
    if (i >= 0 && i < vCount && j >= 0 && j < vCount)
        return adjMatrix[i][j];
    else{
		cout<<"Invalid vertex number.\n";
		return 0;
	}
}
// displays adjacent matrix specifically
void Graph::display() {
    int  u,v; //vertex
	cout<<"\t   ";
	for(u=0; u<vCount; u++) {
		cout<<u<<" ";
	}
    for(u=0; u<vCount; u++) {
        cout << "\nNode[" << (char) (u+48) << "] -> ";
        for(v=0; v<vCount; ++v) {
            cout << " " << adjMatrix[u][v];
        }
    }
    cout << "\n\n";
}
// prints all nodes and their attributes
void Graph::showBasicInfo() {
	for (int i=0; i<vCount; i++) {
		cout<<"node: "<<i<<" Key: "<<key[i]<<" distance: "<<distance[i]<<" parent: "<<parent[i]<<"\n";
	}
}
// effectively checks if the Minimum Spanning Tree is complete
bool Graph::isAllKeyTrue() {
	for (int i=0; i<this->vCount; i++){
		if (this->key[i]==0)
			return 0; // not MST yet
	}
	return 1; // MST done
}
// finds node with the least weight
int Graph::findMinDisNode() {
	int minDis=INFINITY;
	int minDisNode;

	for(int i=0; i<vCount; i++) {
		if(minDis > this->distance[i] && this->key[i]==0)
		{ // 0 means that node is not in MST
			minDisNode = i;
			minDis = this->distance[i];
		}
	}
	return minDisNode;
}
// executes Dijkstra's algorithm with a starting node
void Graph::Dijkstra(int startNode) {
	cout<<"\nDijkstra Shortest Path starts . . . \n";

	// initialization is done before call this method
	this->distance[startNode]=0; //start node's distance is 0
	int minDisNode, i;

	// Loop continues until MST is complete
	while(!this->isAllKeyTrue()) {
		minDisNode = findMinDisNode();
		this->key[minDisNode] = 1;  // this node's shortest path has been found

		cout<<"Shortest Path: "<<this->parent[minDisNode]<<"->"<<minDisNode<<", Destination Node's cost is: "<<distance[minDisNode]<<"\n";

		for(i=0; i<vCount; i++) {
			if(this->isEdge(minDisNode, i) && this->key[i] == 0 ) {
                // Edge relaxation
				if(this->distance[i] > this->distance[minDisNode] + adjMatrix[minDisNode][i]) {
					this->distance[i] = this->distance[minDisNode] + adjMatrix[minDisNode][i];
					this->parent[i] = minDisNode;
				}
			}
		}
	}

}

int main() {
	Graph g(5);
	g.addEdge(0, 1, 10); 
	g.addEdge(0, 3, 5);
	g.addEdge(1, 2, 1);  
	g.addEdge(1, 3, 2);
	g.addEdge(2, 4, 4);
	g.addEdge(3, 1, 3);  
	g.addEdge(3, 2, 9);
	g.addEdge(3, 4, 2);
	g.addEdge(4, 0, 7);  
	g.addEdge(4, 2, 6);

	g.display();

	g.initState();
	int startNode = 0;
	g.showBasicInfo();
	g.Dijkstra(startNode);
	g.showBasicInfo();
	return 0;
}