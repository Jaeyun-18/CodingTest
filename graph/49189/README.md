```cpp
#include <string>
#include <vector>
#include <queue>
#include <algorithm>

using namespace std;

int solution(int n, vector<vector<int>> edge) {
    vector<vector<int>> link(n+1);
    for(auto& e : edge) {
        link[e[0]].push_back(e[1]);
        link[e[1]].push_back(e[0]);
    }
    vector<int> dist(n+1, -1);
    queue<int> q;
    dist[1] = 0;
    q.push(1);
    
    while(!q.empty()) {
        int cur = q.front(); q.pop();
        for(int next : link[cur]) {
            if(dist[next] == -1) {
                q.push(next);
                dist[next] = dist[cur] + 1;
            }
        }
    }
    
    int mx = *max_element(dist.begin(), dist.end());
    int ans=0;
    for(int i=1; i<n+1; i++) {
        if(dist[i] == mx) ans++;
    }
    
    return ans;
}
```
- BFS로 순차적으로 탐색
- edge를 2차원배열이 아니라 vector 2중으로 해서 연결된 형태에만 push_back 하는 형태 사용
