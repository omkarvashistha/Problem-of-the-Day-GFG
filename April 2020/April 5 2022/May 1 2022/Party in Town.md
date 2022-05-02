## Question
Geek town has N Houses numbered from 1 to N. They are connected with each other via N-1 bidirectional roads and an adjacency list adj is used to represent the connections. To host the optimal party, you need to identify the house from which the distance to the farthest house is minimum. Find this distance.
## Explanation
So as we can clearly see this is a graph question and the answer is also very simple the only challenging part here was to understand what the question actually wants from us. So in this question what we have to do was we have to find the minumum of maxmimum heights of each tree where root nodes are from 1-N and that is what we did to find the height we used dfs tarversal and stored the max height in maxd and the minimum of max heights will be stored in mx which will be our answer
## Code :
```
  class Solution{
  public:
    int maxd = 0;
    
    void dfs(int i,vector<vector<int>> &adj,vector<int> &vis,int c){
        vis[i] = 1;
        maxd = max(maxd,c);
        for(int it : adj[i]){
            if(!vis[it]){
                dfs(it,adj,vis,c+1);
            }
        }
    }
    
    int partyHouse(int N, vector<vector<int>> &adj){
        int mx = INT_MAX;
        int house = -1;
        
        for(int i=1;i<=N;i++){
            vector<int> vis(N+1,0);
            maxd = 0;
            dfs(i,adj,vis,0);
            
            if(maxd < mx){
                mx = maxd;
               // house = i;
            }
        }
        return mx;
    }
};
```
