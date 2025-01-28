```cpp
#include<bits/stdc++.h>
// its theorytically proven when we use rank and parent array for checking the size, it takes logarithmic of time logn, we can reduce this too, we can simply do path compression, what it does is lets take example we 
// go and find ulitimate parent of 7, initially 7's parent is 6 and 6's parent is 4 so ulimate parent of 7 is 4, so what we can do is mark first time while figuring out the ultimate parent of 7 is 4 and next time
// when someone comes and ask ulti parent of 7 we can say that its 4. So, this is the optimal way to tell and it takes constant time to do this so.
// WE are not storing height as we will be doing path compression, because at last we want ultimate parent and there is no use of height
#include <iostream>
#include <vector>

using namespace std;

class DisjointSet {
private:
    vector<int> parent;
    vector<int> rank;
    vector<int> size;

public:
    DisjointSet(int n) {
        rank.resize(n + 1, 0);
        parent.resize(n + 1);
        size.resize(n+1);
        for (int i = 0; i <= n; i++) {
            parent[i] = i;
            size[i] = 1;
        }
    }

    int findUP(int node) {
        if (node == parent[node]) { 
            return node;
        }
        return parent[node] = findUP(parent[node]);
    }

    void uninoByRank(int u, int v) { 
        int ulp_u = findUP(u);
        int ulp_v = findUP(v);
        if (ulp_u == ulp_v) return;
        if (rank[ulp_u] < rank[ulp_v]) {
            parent[ulp_u] = ulp_v;
        }
        else if (rank[ulp_u] > rank[ulp_v]) {
            parent[ulp_v] = ulp_u;
        }
        else {
            parent[ulp_v] = ulp_u;
            rank[ulp_u]++;
        }
    }
    void uninoBySize(int u, int v) { 
        int ulp_u = findUP(u);
        int ulp_v = findUP(v);
        if (ulp_u == ulp_v) return;
        if (size[ulp_u] < size[ulp_v]) {
            parent[ulp_u] = ulp_v;
            size[ulp_v] += size[ulp_u];
        }
        else if (size[ulp_u] > size[ulp_v]) {
            parent[ulp_v] = ulp_u;
            size[ulp_u] += size[ulp_v];
        }
        else {
            parent[ulp_v] = ulp_u;
            size[ulp_u] += size[ulp_v];
        }
    }
};

int main() {
    DisjointSet ds(7);
    ds.uninoBySize(1, 2);
    ds.uninoBySize(2, 3);
    ds.uninoBySize(4, 5);
    ds.uninoBySize(6, 7);
    ds.uninoBySize(5, 6); 

    if (ds.findUP(3) == ds.findUP(7)) {
        cout << "Same" << endl;
    }
    else {
        cout << "Not Same" << endl;
    }

    ds.uninoBySize(3, 7); 
    if (ds.findUP(3) == ds.findUP(7)) {
        cout << "Same" << endl;
    } 
    else {
        cout << "Not Same" << endl;
    }

    return 0;
}
```
