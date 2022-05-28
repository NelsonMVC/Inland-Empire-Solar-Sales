# Inland-Empire-Solar-Sales
#include<bits/stdc++.h>
using namespace std;

vector<pair<int,int>>adj[4];
int V =4;
map<int,string>m;
vector<int> dist(V, 10000);


void search(int source){
priority_queue< pair<int,int>, vector <pair<int,int>> , greater<pair<int,int>> > p_q;

p_q.push(make_pair(0, source)); 
dist[source] = 0;
while (!p_q.empty())
{
int u = p_q.top().second; 
p_q.pop();
for (int j = 0; j <adj[u].size(); ++j)
{
int v = adj[u][j].first;
int weight = adj[u][j].second;
  
if (dist[v] > dist[u] + weight)
{
dist[v] = dist[u] + weight;
p_q.push(make_pair(dist[v], v));
}
}
}
  
printf("Node Distance from Source\n");
for (int k = 0; k < V; ++k)
{ cout<<m[k];
printf(" \t\t %d\n",dist[k]);
   }
}

// Driver Function
int main(){
   //riverside->0,moreno valley->1,perris->2,hemet->3
   m[0]="riverside";
m[1]="moreno valley";
m[2]="perris";
m[3]="hemet";
//making the adjacency list
   adj[0].push_back(make_pair(1,16));
   adj[0].push_back(make_pair(2,24));
   adj[0].push_back(make_pair(3,33));
   adj[1].push_back(make_pair(0,16));
   adj[1].push_back(make_pair(2,18));
   adj[1].push_back(make_pair(3,26));
   adj[2].push_back(make_pair(0,24));
   adj[2].push_back(make_pair(1,18));
   adj[2].push_back(make_pair(3,30));
   adj[3].push_back(make_pair(0,33));
   adj[3].push_back(make_pair(1,26));
   adj[3].push_back(make_pair(2,30));

   

   search(0);

   int total_cost=0;
   for(int i=0;i<V;i++)
   total_cost+=2*dist[i];
  
   cout<<"Minimum cost will be: "<<total_cost;
}
