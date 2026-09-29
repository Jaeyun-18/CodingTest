```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

bool visited[8];
int answer = 0;

void dfs(int k, int count, vector<vector<int>> dungeons) {
    answer = max(answer, count);
    for(int i=0; i<dungeons.size(); i++) {
        if(!visited[i] && k >= dungeons[i][0]) {
            visited[i] = true;
            dfs(k - dungeons[i][1], count+1, dungeons);
            visited[i] = false;
        }
    }
}

int solution(int k, vector<vector<int>> dungeons) {
    dfs(k, 0, dungeons);
    return answer;
}
```
```cpp
#include <vector>
#include <algorithm>
using namespace std;

int solution(int k, vector<vector<int>> dungeons) {
    int n = dungeons.size();
    vector<int> idx(n);
    for (int i = 0; i < n; i++) idx[i] = i;

    int best = 0;
    do {
        int f = k, cnt = 0;
        for (int i : idx) {
            if (f < dungeons[i][0]) break;
            f -= dungeons[i][1];
            cnt++;
        }
        best = max(best, cnt);
    } while (next_permutation(idx.begin(), idx.end()));

    return best;
}
```
- 전체 순환하는 형태
- next_permutation은 정렬된 형태에서 사용해야됨 그래서 idx라는 새로운 배열을 만들어서 구성해야함
