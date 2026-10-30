```cpp
#include <string>
#include <vector>
#include <queue>

using namespace std;

int solution(vector<string> board) {
    queue<pair<int, int>> q;
    int m = board.size();
    int n = board[0].size();
    vector<vector<int>> check(m, vector<int>(n, 0));
    int ans = -1;
    
    for(int i=0; i<m; i++) {
        for(int j=0; j<n; j++) {
            if(board[i][j] == 'D') check[i][j]=-1;
            else if(board[i][j] == 'R') {
                check[i][j]=1;
                q.push({i,j});
            }
            else if(board[i][j] == 'G') {
                check[i][j] = -2;
            }
        }
    }
    
    while(!q.empty()) {
        auto [sy, sx] = q.front(); q.pop();
        int ny = sy;
        int nx = sx;
        
        while(ny-1 >= 0 && check[ny-1][sx] != -1) ny--; //상
        if(check[ny][sx] == 0) {
            q.push({ny, sx});
            check[ny][nx] = check[sy][sx] + 1;
        }
        else if(check[ny][nx] == -2) {
            ans = check[sy][sx];
            break;
        }
        ny = sy;
        
        while(ny+1 < m && check[ny+1][sx] != -1) ny++; //하
        if(check[ny][sx] == 0) {
            q.push({ny, sx});
            check[ny][nx] = check[sy][sx] + 1;
        }
        else if(check[ny][nx] == -2) {
            ans = check[sy][sx];
            break;
        }
        ny = sy;
        
        while(nx-1 >= 0 && check[sy][nx-1] != -1) nx--; //좌
        if(check[sy][nx] == 0) {
            q.push({sy, nx});
            check[sy][nx] = check[sy][sx] + 1;
        }
        else if(check[ny][nx] == -2) {
            ans = check[sy][sx];
            break;
        }
        nx = sx;
        
        while(nx+1 < n && check[sy][nx+1] != -1) nx++; //우
        if(check[sy][nx] == 0) {
            q.push({sy, nx});
            check[sy][nx] = check[sy][sx] + 1;
        }
        else if(check[ny][nx] == -2) {
            ans = check[sy][sx];
            break;
        }
        nx = sx;
    }
    
    return ans;
}

//최단 이니까 bfs로 진행 - 4방향이동을 따로 계산해서 방분 한적 없는 곳에 도달한 경우만 이어서 진행 아니라면 drop - 성공시 이동한 횟수 저장

//1인 방문했음. -1은 D, 0은 방문X
```
