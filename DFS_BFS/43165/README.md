```cpp
#include <string>
#include <vector>

using namespace std;

int ans = 0;

void dfs(vector<int> numbers, int target, int idx, int cur) {
    if(idx == numbers.size()) {
        if(cur == target) ans++;
        return;
    }
    
    dfs(numbers, target, idx+1, cur + numbers[idx]);
    dfs(numbers, target, idx+1, cur - numbers[idx]);
}

int solution(vector<int> numbers, int target) {
    dfs(numbers, target, 0, 0);
    return ans;
}
```
- 전형적인 재귀 dfs 형태
- +,- 해야하는 두가지 형태가 있기 때문에 두형태 모두 재귀 실행
- 재귀 탈출조건은 idx가 size와 동일해져서 더이상 추가할게 없을때 + 그 상태가 전부 더해진 상태이기 때문에 정답 요건과 맞는지 확인하고 return
