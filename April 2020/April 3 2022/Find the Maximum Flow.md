## Explanation
I also need a clear explanation for this lol :)
## Code
```
int solve(int N,int M,vector<vector<int>> Edges)
    {
        // code here
        vector<vector<int>> graph(N,vector<int>(N,0));
        
        for(auto it:Edges){
            int u = it[0]-1;
            int v = it[1]-1;
            int wt = it[2];
            
            graph[u][v]+=wt;
            graph[v][u]+=wt;
        }
        return ford(graph,0,N-1,N);
    }
    
int ford(vector<vector<int>> &graph,int s,int t,int N){
         vector<int> parent(N);
         int u,v;
         vector<vector<int>> rgraph(N,vector<int>(N,0));
         
         for(u=0;u<N;u++){
             for(v=0;v<N;v++){
                 rgraph[u][v] = graph[u][v];
             }
         }
         
         int max_path = 0;
         while(bfs(rgraph,s,t,parent)){
             int path_flow = INT_MAX;
             for(v=t;v!=s;v=parent[v]){
                 u = parent[v];
                 path_flow = min(path_flow,rgraph[u][v]);
             }
             
             for(v=t;v!=s;v = parent[v]){
                 u = parent[v];
                 rgraph[u][v]-=path_flow;
                 rgraph[v][u]+=path_flow;
             }
             
             max_path+=path_flow;
             
         }
         return max_path;
    }
    
    bool bfs(vector<vector<int>> &rgraph,int s,int t,vector<int> &parent){
        bool vis[rgraph.size()] = {false};
        queue<int> q;
        q.push(s);
        vis[s] = true;
        parent[s] = -1;
        
        while(!q.empty()){
            int u = q.front();
            q.pop();
            
            for(int v= 0;v<rgraph.size();v++){
                if(!vis[v] && rgraph[u][v]>0){
                    if(v==t){
                        parent[v] = u;
                        return true;
                    }
                    q.push(v);
                    vis[v] = true;
                    parent[v] = u;
                }
            }
        }
        return false;
        
    }

```
