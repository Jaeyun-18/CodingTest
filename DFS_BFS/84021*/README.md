```cpp
#include <vector>
#include <algorithm>
#include <climits>
using namespace std;

using Shape = vector<pair<int,int>>;
int n;
int dr[4] = {-1, 1, 0, 0}, dc[4] = {0, 0, -1, 1};

Shape normalize(Shape s) {
    int mr = INT_MAX, mc = INT_MAX;
    for (auto& [r, c] : s) { mr = min(mr, r); mc = min(mc, c); }
    for (auto& [r, c] : s) { r -= mr; c -= mc; }
    sort(s.begin(), s.end());
    return s;
}

Shape rotate(const Shape& s) {
    Shape t;
    for (auto [r, c] : s) t.push_back({c, -r});
    return normalize(t);
}

void dfs(vector<vector<int>>& b, int r, int c, int target, Shape& cells) {
    b[r][c] = !target;               // 방문 표시 (target과 반대 값으로)
    cells.push_back({r, c});
    for (int d = 0; d < 4; d++) {
        int nr = r + dr[d], nc = c + dc[d];
        if (nr >= 0 && nr < n && nc >= 0 && nc < n && b[nr][nc] == target)
            dfs(b, nr, nc, target, cells);
    }
}

vector<Shape> extract(vector<vector<int>> b, int target) {   // 복사본 사용
    vector<Shape> res;
    for (int r = 0; r < n; r++)
        for (int c = 0; c < n; c++)
            if (b[r][c] == target) {
                Shape cells;
                dfs(b, r, c, target, cells);
                res.push_back(normalize(cells));
            }
    return res;
}

int solution(vector<vector<int>> game_board, vector<vector<int>> table) {
    n = game_board.size();
    vector<Shape> blanks = extract(game_board, 0);   // 빈칸 = 0
    vector<Shape> pieces = extract(table, 1);        // 조각 = 1
    vector<bool> used(pieces.size(), false);
    int ans = 0;

    for (auto& blank : blanks) {
        for (int i = 0; i < pieces.size(); i++) {
            if (used[i] || pieces[i].size() != blank.size()) continue;
            Shape p = pieces[i];
            bool matched = false;
            for (int k = 0; k < 4; k++) {
                if (p == blank) { matched = true; break; }
                p = rotate(p);
            }
            if (matched) {
                used[i] = true;
                ans += blank.size();
                break;               // 이 빈칸은 채웠으니 다음 빈칸으로
            }
        }
    }
    return ans;
}
```
- 봤던것들 중에 가장 어려운 문제 인듯 -> 전체적은 흐름 : DFS로 BOARD와 TABLE의 조각들을 다 찾아냄( 조각들은 Shape라는 자료구조를 별칭을 붙여서 사용한다 )
  - 그 후 조각별로 크기 같은 것을 우선적으로 탐색해서 조각을 90도씩 회전시켜 비교한다.
  - 회전시키는건 [r,c] -> [c, -r] 형태
