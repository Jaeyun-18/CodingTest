```cpp
#include <string>
#include <vector>

using namespace std;

int solution(int n, vector<vector<int>> results) {
    vector<vector<bool>> connect(n+1, vector<bool>(n+1, false));
    for(auto& r : results) {
        connect[r[0]][r[1]] = true;
    }
    
    for(int k=1; k<n+1; k++) {
        for(int i=1; i<n+1; i++) {
            for(int j=1; j<n+1; j++) {
                if(connect[i][k] && connect[k][j]) connect[i][j] = true;
            }
        }
    }
    
    int ans=0;
    for(int i=1; i<n+1; i++) {
        int cnt = 0;
        for(int j=1; j<n+1; j++) {
            if(connect[i][j] || connect[j][i]) cnt++;
        }
        if(cnt == n-1) ans++;
    }
    
    return ans;
}
```
- 플로이드 워셜 DP
- K를 바깥에 두는 이유는 K가 변경됨에 따라 모든 쌍을 확인하기 위함
- 결국 모든 쌍에 대해서 확인하는 것이기 때문에 K의 반복 순서와 관계없이 모든 연결 관계를 찾아낼 수 있음
