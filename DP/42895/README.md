```cpp
#include <string>
#include <vector>
#include <unordered_set>

using namespace std;

int solution(int N, int number) {
    unordered_set<int> dp[9];
    int rep=0;
    
    for(int k=1; k<=8; k++) {
        rep = rep*10+N;
        dp[k].insert(rep);
        for(int i=1; i<k; i++) {
            for(int a : dp[i]) {
                for(int b : dp[k-i]) {
                    dp[k].insert(a+b);
                    dp[k].insert(a-b);
                    dp[k].insert(a*b);
                    if(b != 0) dp[k].insert(a/b);
                }
            }
        }
        if(dp[k].count(number)) return k;
    }
    return -1;
}
```
- greedy 형태가 안되기 때문에 가능한 모든 결과를 남겨두는 형태
- k번 사용한 숫자를 만들기 위해 i번 사용한 것과 k-i번 사용한 결과물을 합쳐서 k번 결과물을 만듦
- 8번 보다 초과하면 return -1
- unordered_set은 순서는 없고 중복은 처리해주는 형태 -> 지금의 경우엔 순서는 필요없고 중복된 경우만 제외하면 되기 때문에 사용
