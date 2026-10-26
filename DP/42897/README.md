```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

int check(const vector<int>& money, int h, int t) {
    int prev1 = 0, prev2 = 0;
    for(int i=h; i<=t; i++) {
        int cur = max(prev1, prev2 + money[i]);
        prev2 = prev1;
        prev1 = cur;
    }
    return prev1;
}

int solution(vector<int> money) {
    int n = money.size();
    return max(check(money, 0, n-2), check(money, 1, n-1));
}
```
- 원형이기에 크게 두가지 형태로 분활 -> 0을 포함 / 0을 제외
- 앞선 형태의 값에서 i를 털때 그리고 i를 털지 않을때의 최선을 확인하고 다음에 사용하는 형태
