```cpp
#include <string>
#include <vector>
#include <queue>
#include <tuple>

using namespace std;

int solution(vector<vector<int>> rectangle, int characterX, int characterY, int itemX, int itemY) {
    bool visited[102][102] = {};
    int dx[4] = {1,-1,0,0};
    int dy[4] = {0,0,1,-1};

    int sx = characterX*2, sy = characterY*2;
    int tx = itemX*2, ty = itemY*2;

    queue<tuple<int,int,int>> q;
    q.push({sx, sy, 0});
    visited[sx][sy] = true;

    while (!q.empty()) {
        auto [x, y, cost] = q.front(); q.pop();
        if (x == tx && y == ty) return cost / 2;

        for (int i = 0; i < 4; i++) {
            int nx = x + dx[i], ny = y + dy[i];
            if (nx < 0 || nx >= 102 || ny < 0 || ny >= 102) continue;
            if (visited[nx][ny]) continue;

            bool inAny = false;     // 어떤 사각형의 경계 포함 범위 안에 있는지
            bool inInner = false;   // 어떤 사각형의 내부에 있는지
            for (const auto& r : rectangle) {
                int x1 = r[0]*2, y1 = r[1]*2, x2 = r[2]*2, y2 = r[3]*2;
                if (nx > x1 && nx < x2 && ny > y1 && ny < y2) {
                    inInner = true;
                    break;          // 내부면 더 볼 필요 없음
                }
                if (nx >= x1 && nx <= x2 && ny >= y1 && ny <= y2)
                    inAny = true;
            }
            if (inInner || !inAny) continue;   // 테두리가 아니면 건너뜀

            visited[nx][ny] = true;
            q.push({nx, ny, cost + 1});
        }
    }
    return 0;
}
```
- BFS로 찾아가는건 동일한데 2배를 해서 계산해야 된다는 이유가 어려웠음
- 정수 좌표 위에서만 BFS를 하면, **두 점은 모두 테두리 위에 있는데 그 사이 선분은 테두리가 아닌 경우**가 생기기 때문입니다.
**예시: ㄷ자(U자) 모양**

```
사각형 A: [1,1,2,5]   (왼쪽 기둥)
사각형 B: [3,1,4,5]   (오른쪽 기둥)
사각형 C: [1,1,4,2]   (아래 받침)
```

```
y=5  ┌─┐ ┌─┐
     │ │ │ │
y=4  │ ● ● │      ← (2,4)와 (3,4)
     │ │ │ │
y=3  │ │ │ │
     │ └─┘ │
y=2  │     │
y=1  └─────┘
     x=1 2 3 4
```

- `(2,4)`는 왼쪽 기둥의 오른쪽 변 위에 있고, `(3,4)`는 오른쪽 기둥의 왼쪽 변 위에 있습니다. 둘 다 테두리 위의 점입니다.
- 정수 격자에서 두 점은 바로 옆 칸이라, BFS가 한 칸 만에 건너가 버립니다.
- 하지만 실제로는 두 기둥 사이가 빈 공간이라 그 사이에 길이 없습니다. 올바른 경로는 아래로 내려가 `y=2`의 홈 바닥을 돌아서 다시 올라가는 것입니다.

**2배로 늘리면**

- `(2,4)` → `(4,8)`, `(3,4)` → `(6,8)`
- 이제 두 점 사이에 `(5,8)`이라는 칸이 생깁니다.
- `(5,8)`은 원래 좌표로 `(2.5, 4)`입니다. 어떤 사각형에도 속하지 않으므로 테두리가 아니고, BFS가 그 칸을 지나갈 수 없습니다.

즉, 2배로 늘리는 건 **두 점 사이 선분의 중간 지점도 검사하기 위해서**입니다. 원래 좌표에서는 한 칸 이동이 "점에서 점으로 점프"라서 그 사이를 확인할 방법이 없지만, 2배 좌표에서는 한 칸 이동이 원래 선분의 절반이라 중간점이 격자 위에 올라와서 판별할 수 있게 됩니다.

거리도 모든 이동이 2배가 되었으니 마지막에 `cost / 2`로 되돌리면 됩니다.
