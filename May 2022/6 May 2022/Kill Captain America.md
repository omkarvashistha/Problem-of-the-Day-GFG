## Problem 
Captain America is hiding from Thanos in a maze full of N rooms connected by M gates.
The maze is designed in such a way that each room leads to another room via gates. All connecting gates are unidirectional. Captain America is hiding only in those rooms which are accessible directly/indirectly through every other room in the maze.
Help Thanos find the number of rooms in which Captain America can hide. 

## Explanation

## Code
```
  #define vi vector<int>
    void make_graph(vector<vi> &V,vi* adj,vi* trans_adj){
        for(int i=0;i<V.size()-1;i++){
            adj[V[i][0]].push_back(V[i][1]);
            trans_adj[V[i][1]].push_back(V[i][0]);
        }
        
        return;
    }
    
	int outdeg(unordered_set<int> st,vi* adj){
	    int out=0;
	    for(auto i:st){
	        for(int child:adj[i]){
	            if(st.find(child)==st.end()) out++;
	        }
	    }
	    
	    return out;
	}
	
	void topo_dfs(int node,vi* adj,vi &vis,stack<int> &st){
	    vis[node]=true;
	    
	    for(auto i:adj[node]){
	        if(!vis[i]){
	            topo_dfs(i,adj,vis,st);
	        }
	    }
	    
	    st.push(node);
	    return;
	}
	
	void dfs(int node,vi* adj,vi &vis,unordered_set<int> &sett){
	    vis[node]=true;
	    sett.insert(node);
	    
	    for(auto i:adj[node]){
	        if(!vis[i]){
	            dfs(i,adj,vis,sett);
	        }
	    }
	    
	    return;
	}
	
    int captainAmerica(int N, int M, vector<vector<int>> &V){
        // Code Here
        int out_0=0;
        int max_size=INT_MIN;
        
        vi adj[N+1];
        vi vis(N+1,false);
        stack<int> st;
        vi trans[N+1];
        
        make_graph(V,adj,trans);
        
        for(int i=1;i<N+1;i++){
            if(!vis[i]){
                topo_dfs(i,adj,vis,st);
            }
        }
        
        for(int i=0;i<N+1;i++){
            vis[i]=false;
        }
        
        
        while(!st.empty()){
            unordered_set<int> sett;
            if(!vis[st.top()]){
                dfs(st.top(),trans,vis,sett);
                
                if(outdeg(sett,adj)==0){
                    int size=sett.size();
                    //cout<<size;
                    max_size=max(max_size,size);
                    out_0++;
                }
            }
            st.pop();
        }
        
        if(out_0>1) return 0;
        return max_size;
    } 
```
