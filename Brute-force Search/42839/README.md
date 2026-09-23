```cpp
#include <string>
#include <vector>
#include <algorithm>
#include <set>

using namespace std;

bool visited[7];
set<int> nums;

bool is_prime(int n) {
    if(n < 2) return false;
    for(int i=2; i*i<=n; i++) {
        if(n%i == 0) return false;
    }
    return true;
}

void dfs(const string& numbers, string cur) {
    if(!cur.empty()) nums.insert(stoi(cur));
    for(int i=0; i<numbers.size(); i++) {
        if(visited[i]) continue;
        visited[i] = true;
        dfs(numbers, cur + numbers[i]);
        visited[i] = false;
    }
}

int solution(string numbers) {
    int answer = 0;
    dfs(numbers, "");
    for(const auto&n : nums) {
        if(is_prime(n)) answer++;
    }
    return answer;
}
```
- string을 int로 변환 stoi
- 소수판별은 for문 사용해서 해당수의 제곱근 보다 아래의 숫자들 중에 나머지가 0인게 있으면 false
- 순열생성은 dfs 형태로 진행하거나 next_permutation이라는 순열 return 함수가 algorithm 헤더에 존재
