```cpp
#include <string>
#include <vector>

using namespace std;

bool check[199];

void dfs(int head, int n, const vector<vector<int>>& computers) {
    for(int i=0; i<n; i++) {
        if(computers[head][i] == 1 && !check[i]) {
            check[i] = true;
            dfs(i, n, computers);
        }
    }
}

int solution(int n, vector<vector<int>> computers) {
    int ans = 0;
    for(int i=0; i<n; i++) {
        if(!check[i]) {
            check[i] = true;
            ans++;
            dfs(i, n, computers);
        }
    }
    
    return ans;
}
```
- 탐색한 적 없는 head를 기준으로 dfs를 진행하고 ans++ 해준다
- 상삼각형만 탐색하면 된다고 생각했는데 반례로 0-2 2-1로 탐색하면 안되기 때문에 전체 형태로 탐색을 진행해줘야 함
