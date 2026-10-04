```cpp
#include <string>
#include <algorithm>

using namespace std;

int solution(string name) {
    int n = name.size();
    int answer = 0;
    int move = n - 1;  // 오른쪽으로 쭉 가는 경우

    for (int i = 0; i < n; i++) {
        answer += min(name[i] - 'A', 'Z' - name[i] + 1);

        if (i != 0 && name[i] == 'A') continue;  // 시작점은 예외

        int next = i + 1;
        while (next < n && name[next] == 'A') next++;
        move = min(move, i * 2 + (n - next));
        move = min(move, (n - next) * 2 + i);
    }
    return answer + move;
}
```
- 이문제에서 중요한 것은 변경해야하는 지점 사이에서 어떤 A집단을 넘기는 것이 가장 이득인가를 구하는 과정
   - 그래서 특정 지점에 대해서 다음 A아닌 지점까지 어떤 것을 먼저 방문하는 것이 이득인지를 계산
