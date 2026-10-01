```cpp
#include<vector>
#include<queue>
using namespace std;

int solution(vector<vector<int>> maps)
{
    int n = maps.size(), m = maps[0].size();
    int dy[4] = {-1,1,0,0};
    int dx[4] = {0,0,-1,1};
    
    vector<vector<int>> dist(n, vector<int>(m,0));
    queue<pair<int, int>> q;
    q.push({0,0});
    dist[0][0] = 1;
    
    while(!q.empty()) {
        auto [y,x] = q.front(); q.pop();
        if(y == n-1 && x == m-1) return dist[y][x];
        
        for(int i=0; i<4; i++) {
            int ny = y + dy[i], nx = x + dx[i];
            if(ny < 0 || ny >= n || nx < 0 || nx >= m)  continue;
            if(maps[ny][nx] == 0 || dist[ny][nx] != 0) continue;
            dist[ny][nx] = dist[y][x] + 1;
            q.push({ny,nx});
        }
    }
    return -1;
}
```
- 가중치가 없는 격자에서 최단거리 탐색이기 때문에 BFS 형태로 원점에서부터 탐색한다 -> QUEUE를 사용
- 큐에 들어갈때 최소값부터 들어가고 나오기 때문에 최단거리를 가진 다는 것을 증명함
