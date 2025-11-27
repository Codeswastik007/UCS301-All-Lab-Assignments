###add1
```cpp
#include <bits/stdc++.h>
using namespace std;

int main(){
    int V, E;
    if(!(cin >> V >> E)) return 0;
    vector<vector<int>> adj(V);
    for(int i = 0; i < E; ++i){
        int u, v;
        cin >> u >> v;
        if(u >= 0 && u < V && v >= 0 && v < V){
            adj[u].push_back(v);
            adj[v].push_back(u);
        }
    }

    vector<char> visited(V, 0);
    int components = 0;

    for(int i = 0; i < V; ++i){
        if(visited[i]) continue;
        ++components;
        queue<int> q;
        q.push(i);
        visited[i] = 1;
        while(!q.empty()){
            int u = q.front(); q.pop();
            for(int w : adj[u]){
                if(!visited[w]){
                    visited[w] = 1;
                    q.push(w);
                }
            }
        }
    }

    cout << components << "\n";
    return 0;
}
```

###add2
```cpp
#include <bits/stdc++.h>
using namespace std;

int main(){
    int V, E;
    if(!(cin >> V >> E)) return 0;
    vector<vector<int>> adj(V);
    for(int i = 0; i < E; ++i){
        int u, v;
        cin >> u >> v;
        if(u >= 0 && u < V && v >= 0 && v < V){
            adj[u].push_back(v);
            adj[v].push_back(u);
        }
    }

    vector<char> visited(V, 0);
    int components = 0;

    for(int i = 0; i < V; ++i){
        if(visited[i]) continue;
        ++components;
        queue<int> q;
        q.push(i);
        visited[i] = 1;
        while(!q.empty()){
            int u = q.front(); q.pop();
            for(int w : adj[u]){
                if(!visited[w]){
                    visited[w] = 1;
                    q.push(w);
                }
            }
        }
    }

    cout << components << "\n";
    return 0;
}
```

###add3
```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    int N, K, M;
    if (!(cin >> N >> K >> M)) return 0;

    vector<vector<pair<int,int>>> adj(N + 1);
    for (int i = 0; i < M; ++i) {
        int u, v, w;
        cin >> u >> v >> w;
        adj[u].push_back({v, w});
    }

    vector<int> dist(N + 1, INT_MAX);
    using Node = pair<int,int>;
    priority_queue<Node, vector<Node>, greater<Node>> pq;

    dist[K] = 0;
    pq.push({0, K});

    while (!pq.empty()) {
        int d = pq.top().first;
        int u = pq.top().second;
        pq.pop();

        if (d != dist[u]) continue;

        for (auto &e : adj[u]) {
            int v = e.first;
            int w = e.second;
            int nd;
            if (d > INT_MAX - w) nd = INT_MAX;
            else nd = d + w;
            if (nd < dist[v]) {
                dist[v] = nd;
                pq.push({nd, v});
            }
        }
    }

    int ans = 0;
    for (int i = 1; i <= N; ++i) {
        if (dist[i] == INT_MAX) {
            cout << -1 << endl;
            return 0;
        }
        ans = max(ans, dist[i]);
    }

    cout << ans << endl;
    return 0;
}
```

###add4
```cpp
#include <bits/stdc++.h>
using namespace std;

int m, n;
vector<vector<int>> grid;
vector<vector<int>> vis;

void dfs(int r, int c) {
    vis[r][c] = 1;

    int dr[4] = {1, -1, 0, 0};
    int dc[4] = {0, 0, 1, -1};

    for (int k = 0; k < 4; k++) {
        int nr = r + dr[k];
        int nc = c + dc[k];

        if (nr >= 0 && nr < m && nc >= 0 && nc < n) {
            if (!vis[nr][nc] && grid[nr][nc] == 1) {
                dfs(nr, nc);
            }
        }
    }
}

int main() {
    cin >> m >> n;

    grid.assign(m, vector<int>(n));
    vis.assign(m, vector<int>(n, 0));

    for (int i = 0; i < m; i++)
        for (int j = 0; j < n; j++)
            cin >> grid[i][j];

    int count_islands = 0;

    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            if (!vis[i][j] && grid[i][j] == 1) {
                count_islands++;
                dfs(i, j);
            }
        }
    }

    cout << count_islands << endl;
    return 0;
}
```

###BFS-Traversal
```cpp
#include<iostream>
#include<vector>
#include<queue>
using namespace std;

class Graph{
public:
    int n; 
    vector<vector<int>> adj;

    Graph(int nodes) {
        n = nodes;
        adj = vector<vector<int>>(n);
    }
    
    void addEdge(int v , int u){
        adj[u].push_back(v);
        adj[v].push_back(u);
    }

    vector<int> BfsTraversal(int start){
        vector<bool> visited(n,false);
        queue<int> q; 
        visited[start] = true; 
        q.push(start);

        vector<int> bfsSeq; 

        while(!q.empty()){
            int node = q.front();
            q.pop();
            bfsSeq.push_back(node);

            for (auto it : adj[node]){
                if (!visited[it]){
                    visited[it] = true;
                    q.push(it);
                }
            }
        }
        return bfsSeq; 
    }
};

int main()
{
    cout << "Enter the number of nodes : ";
    int n; 
    cin >> n;

    Graph g(n);  

    cout << "Enter the number of edges : ";
    int m; 
    cin >> m;

    cout << "Enter the edge connections : ";
    for (int i = 0; i < m; i++){
        int u, v; 
        cin >> u >> v;
        g.addEdge(u, v);
    }

    cout << "Enter the starting number for the BFS traversal : ";
    int start; 
    cin >> start;

    vector<int> bfsSeq = g.BfsTraversal(start);

    cout << "------The BFS traversal Sequence is as follows : ------\n";
    for (int node : bfsSeq){
        cout << node << " ";
    }

    cout << endl; 
    return 0;
}
```

###DFS-travesral
```cpp
#include<iostream>
#include<vector>
using namespace std;
class Graph{
    public:
    int n; 
    vector<vector<int>> adj;

    Graph(int nodes) {
        n = nodes;
        adj = vector<vector<int>>(n);
    }
    void addEdge(int v , int u){
        adj[u].push_back(v);
        adj[v].push_back(u);
    }
    void dfsHelp(int node , vector <bool>& visited , vector<int> &dfsSequence){
        visited[node] = true; 
        dfsSequence.push_back(node);
        for ( auto it : adj[node]){
            if(!visited[it]){
                dfsHelp(it , visited , dfsSequence);
            }
        }
    }
    vector<int> dfsTraversal(int start){
        vector<bool> visited(n , false);
        vector<int> dfsSequence; 
        dfsHelp(start , visited , dfsSequence);
        return dfsSequence;
    }
};
int main()
{
    // creating the adj list
    // 1-2,3
    // 2-1,5,6 
    // 3-1,7,4 
    // 5-2
    // 6-2 
    // 4-3,8 
    // 7-3,8 
    int n; 
    cout<<"Enter the number of nodes : ";
    cin>>n; 
    Graph g(n);
    int m; 
    cout<<"Enter the number of edges : ";
    cin>>m; 
    cout<<"Enter the edges connections : ";
    for( int i = 0 ; i < m ; i ++){
        int u , v; 
        cin>>u>>v; 
        g.addEdge(u , v);
    }    
    int start; 
    cout<<"Enter the start node for the dfs sequence : ";
    cin>>start; 
    vector <int> dfsSeq = g.dfsTraversal(start);
    cout<<"The traversal is : ";
    for(auto it : dfsSeq) cout<<it <<" ";
    cout<<endl; 
    return 0;
}
```

###Kruskal
```cpp
#include <bits/stdc++.h>
using namespace std;

class Edge {
public:
    int u;
    int v;
    long long w;
    Edge(int uu=0, int vv=0, long long ww=0): u(uu), v(vv), w(ww) {}
};

class DisjointSet {
    vector<int> parent;
    vector<int> rankv;
public:
    DisjointSet(int n): parent(n+1), rankv(n+1,0) {
        for(int i=1;i<=n;i++) parent[i]=i;
    }
    int find(int x) {
        while(parent[x] != x) x = parent[x];
        return x;
    }
    bool unite(int a, int b) {
        a = find(a);
        b = find(b);
        if(a==b) return false;
        if(rankv[a] < rankv[b]) swap(a,b);
        parent[b] = a;
        if(rankv[a] == rankv[b]) rankv[a] ++;
        return true;
    }
};

class KruskalMST {
    int n;
    vector<Edge> edges;
public:
    KruskalMST(int nodes): n(nodes) {}
    void addEdge(int u, int v, long long w){ edges.emplace_back(u,v,w); }
    pair<long long, vector<Edge>> build(){
        sort(edges.begin(), edges.end(), [](const Edge& a, const Edge& b){
            if(a.w != b.w) return a.w < b.w;
            if(a.u != b.u) return a.u < b.u;
            return a.v < b.v;
        });
        DisjointSet dsu(n);
        vector<Edge> mst;
        long long total = 0;
        for(const Edge& e : edges){
            if(dsu.unite(e.u, e.v)){
                mst.push_back(e);
                total += e.w;
                if((int)mst.size() == n-1) break;
            }
        }
        if((int)mst.size() != n-1) return {-1, {}};
        return {total, mst};
    }
};

int main(){
    int n, m;
    if(!(cin >> n >> m)) return 0;
    KruskalMST solver(n);
    for(int i=0;i<m;i++){
        int u,v;
        long long w;
        cin >> u >> v >> w;
        solver.addEdge(u,v,w);
    }
    auto res = solver.build();
    if(res.first == -1){
        cout << "IMPOSSIBLE\n";
        return 0;
    }
    cout << res.first << "\n";
    for(const Edge& e : res.second) cout << e.u << " " << e.v << " " << e.w << "\n";
    return 0;
}
```

###Prim
```cpp
#include <bits/stdc++.h>
using namespace std;

class Graph {
    int n;
    vector<vector<pair<int,long long>>> adj;
public:
    Graph(int nodes): n(nodes), adj(nodes+1) {}
    void addEdge(int u, int v, long long w){
        adj[u].push_back({v,w});
        adj[v].push_back({u,w});
    }
    pair<long long, vector<tuple<int,int,long long>>> primMST(){
        vector<char> used(n+1, 0);
        vector<long long> dist(n+1, LLONG_MAX);
        vector<int> parent(n+1, -1);
        using P = pair<long long,int>;
        priority_queue<P, vector<P>, greater<P>> pq;

        dist[1] = 0;
        pq.push({0,1});
        long long total = 0;
        vector<tuple<int,int,long long>> mst;

        while(!pq.empty()){
            auto cur = pq.top(); pq.pop();
            long long d = cur.first;
            int u = cur.second;
            if(used[u]) continue;
            used[u] = 1;
            if(parent[u] != -1){
                mst.emplace_back(parent[u], u, d);
                total += d;
            }
            for(const auto &pr : adj[u]){
                int v = pr.first;
                long long w = pr.second;
                if(!used[v] && w < dist[v]){
                    dist[v] = w;
                    parent[v] = u;
                    pq.push({dist[v], v});
                }
            }
        }

        int visitedCount = 0;
        for(int i=1;i<=n;i++) if(used[i]) visitedCount++;
        if(visitedCount != n) return {-1, {}};
        return {total, mst};
    }
};

int main(){
    int n, m;
    if(!(cin >> n >> m)) return 0;
    Graph g(n);
    for(int i=0;i<m;i++){
        int u,v;
        long long w;
        cin >> u >> v >> w;
        g.addEdge(u,v,w);
    }
    auto res = g.primMST();
    if(res.first == -1){
        cout << "IMPOSSIBLE\n";
        return 0;
    }
    cout << res.first << "\n";
    for(const auto &t : res.second){
        int u,v; long long w;
        tie(u,v,w) = t;
        cout << u << " " << v << " " << w << "\n";
    }
    return 0;
}
```
