```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

vector<int> connect[101];
bool visited[101];

int dfs(int head) {
    visited[head] = true;
    int cnt=1;
    for(const auto&c : connect[head]) {
        if(!visited[c]) cnt += dfs(c);
    }
    return cnt;
}

int solution(int n, vector<vector<int>> wires) {
    int answer = n;
    for(int cut=0; cut<wires.size(); cut++) {
        for(int i=0; i<=n; i++) {
            connect[i].clear();
            visited[i] = false;
        }
        
        for(int i=0; i<wires.size(); i++) {
            if(i == cut) continue;
            connect[wires[i][0]].push_back(wires[i][1]);
            connect[wires[i][1]].push_back(wires[i][0]);
        }
        int cnt = dfs(1);
        answer = min(answer, abs(n-2*cnt));
    }
    
    return answer;
}
```
- tree연결 형태에서 양방향이기 때문에 connect를 다음과 같은 형태로 저장함

```cpp
#include <vector>
#include <cstdlib>
#include <algorithm>
using namespace std;

vector<int> adj[101];
int N, answer;

int dfs(int v, int parent) {
    int sz = 1;
    for (int nx : adj[v])
        if (nx != parent) sz += dfs(nx, v);
    answer = min(answer, abs(N - 2 * sz));
    return sz;
}

int solution(int n, vector<vector<int>> wires) {
    N = n;
    answer = n;
    for (auto& w : wires) {
        adj[w[0]].push_back(w[1]);
        adj[w[1]].push_back(w[0]);
    }
    dfs(1, 0);
    return answer;
}
```
- dfs를 한번만 돌려서 끊는것 뿐 아니라 사이즈까지 전부 탐색 => 트리라서 가능한 형태
- 트리이기 때문에 이전에 parent만 아니면 중복을 삭제할 수 있음
- 추가적으로 하나의 서브트리마다 answer를 뽑는 것이 해당 지점의 연결을 끊었을 때의 트리 크기 즉 정답형태이기 때문에 문제 없음
