```cpp
#include <string>
#include <vector>
#include <queue>
#include <algorithm>

using namespace std;

int cost[50];

int solution(string begin, string target, vector<string> words) {
    int size = words.size();
    queue<pair<string, int>> q;
    q.push({begin, -1});
    
    auto exist = find(words.begin(), words.end(), target);
    if(exist == words.end()) return 0;
    
    while(!q.empty()) {
        auto [cur, idx] = q.front(); q.pop();
        if(cur == target) return cost[idx];
        

        for(int i=0; i<size; i++) {
            int cnt=0;
            if(cost[i] == 0) {
                for(int j=0; j<words[i].size(); j++)
                    if(words[i][j] != cur[j]) cnt++;
                if(cnt == 1) {
                    if(idx == -1) cost[i] = 1;
                    else cost[i] = cost[idx] + 1;
                    q.push({words[i], i});
                }
            }
        }
    }
    return 0;
}
```
- BFS 형태 vector에서 특정 값 찾는 것 find -> algorithm에 있음
