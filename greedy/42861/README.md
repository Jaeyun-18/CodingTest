```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

vector<int> parent;

int find(int x) {
    if(parent[x] == x) return x;
    return parent[x] = find(parent[x]); //경로압축을 계속해서 진행 -> 사이클은 없음
}

int solution(int n, vector<vector<int>> costs) {
    int ans = 0;
    parent.resize(n);
    for(int i=0; i<n; i++) parent[i] = i;
    
    sort(costs.begin(), costs.end(), [](const vector<int>& a, const vector<int>& b) {
        return a[2] < b[2];
    });
    
    int cnt = 0;
    for(auto&c : costs) {
        int ra = find(c[0]), rb = find(c[1]);
        if(ra != rb) {
            parent[ra] = rb;
            ans += c[2];
            if(++cnt == n-1) break;
        }
    }
    
    return ans;
}
```
- sort에서 2차원배열을 대입하면 행을 기준으로 접근함, 지금처럼 작성하지 않으면 원소를 순서대로 비교하는형태
- 크루스칼 알고리즘 : cost가 있는 mst 문제에선 다른 그룹을 연결하는 최소 간선이 포합되어야 함
  - ++cnt == n-1은 n개의 점이 존재할때 n-1간선이 생기면 모든 지점이 순환하는 형태로 연결되기 때문에 조기 종료하는 형태
  - find에서 경로압축 즉 parent를 계속 최신화해준다.
- prim 알고리즘 : 한 섬에서 시작해서 가장 작은 cost의 선을 연결함. 큐 형태로 연결된 섬들 중 가장 작은 것을 꺼내고 이미 방분했는지를 확인하고 간선을 추가한다
```cpp
#include <vector>
#include <queue>
using namespace std;

int solution(int n, vector<vector<int>> costs) {
    // 인접 리스트: adj[u] = {cost, v}
    vector<vector<pair<int,int>>> adj(n);
    for (auto& c : costs) {
        adj[c[0]].push_back({c[2], c[1]});
        adj[c[1]].push_back({c[2], c[0]});
    }

    vector<bool> visited(n, false);
    // 최소 힙: cost가 작은 게 top
    priority_queue<pair<int,int>, vector<pair<int,int>>, greater<>> pq;

    pq.push({0, 0});  // {cost, 섬}: 시작 섬은 비용 0
    int answer = 0, cnt = 0;

    while (!pq.empty() && cnt < n) {
        auto [cost, u] = pq.top(); pq.pop();
        if (visited[u]) continue;   // 이미 트리 안이면 버림

        visited[u] = true;
        answer += cost;
        cnt++;

        for (auto& [w, v] : adj[u])
            if (!visited[v]) pq.push({w, v});
    }
    return answer;
}
```
- priority 큐는 들어온 순서보다 값 자체가 중요할때 사용하는 DS
```cpp
priority_queue<pair<int,int>, vector<pair<int,int>>, greater<>> pq;
//             원소 타입      내부 저장 컨테이너        비교 함수
```
