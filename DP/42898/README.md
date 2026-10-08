```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

int solution(int m, int n, vector<vector<int>> puddles) {
    vector<vector<int>> dp(m+1, vector<int>(n+1, 0));
    vector<vector<bool>> blocked(m+1, vector<bool>(n+1, false));
    for(auto&p : puddles) blocked[p[0]][p[1]] = true;
    
    dp[1][1] = 1;
    for(int i=1; i<=m; i++) {
        for(int j=1; j<=n; j++) {
            if(i==1 && j==1) continue;
            if(blocked[i][j]) {
                dp[i][j] = 0; 
                continue;
            }
            else dp[i][j] = (dp[i-1][j] + dp[i][j-1]) % 1000000007;
        }
    }
    
    return dp[m][n];
}
```
- 전체 순환 형태
- 지금은 blocked로 다른 배열을 표시했지만 그냥 물웅덩이를 -1로 처리해도 순환에 영향이 없기 때문에 상관없음
