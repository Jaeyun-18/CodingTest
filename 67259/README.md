```cpp
#include <string>
#include <vector>
#include <queue>
#include <tuple>
#include <climits>

using namespace std;

int solution(vector<vector<int>> board) {
    int sz = board.size() - 1;
    using Data = tuple<int, int, int, int>;
    priority_queue<Data, vector<Data>, greater<Data>> pq;
    vector<int> dx = {1,-1,0,0};
    vector<int> dy = {0,0,1,-1};
    vector<vector<vector<int>>> dist(board.size(), vector<vector<int>>(board.size(), vector<int>(4, INT_MAX)));
    pq.push({0, 0, 0, -1});
    
    while(!pq.empty()) {
        auto [cost, y, x, dir] = pq.top(); pq.pop();
        if (dir != -1 && cost > dist[y][x][dir]) continue;
        if(y == sz && x == sz) return cost;
        
        for(int i=0; i<4; i++) {
            int ny = y + dy[i], nx = x + dx[i];
            if(ny < 0 || ny > sz || nx < 0 || nx > sz) continue;
            if(board[ny][nx] == 1) continue;
            
            int nc;
            if(i == dir || dir == -1) nc = cost + 100;
            else nc = cost + 600;
            if(nc < dist[ny][nx][i]) {
                dist[ny][nx][i] = nc;
                pq.push({nc, ny, nx, i});
            }
        }
    }
    
    return -1;
}

//pq 사용, cost, 현재점, 어디방향인지 상하좌우 0,1,2,3 -1은 상관없음
```
