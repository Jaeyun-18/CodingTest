```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

int solution(int n, vector<int> lost, vector<int> reserve) {
    int ans=0;
    vector<int> cnt(n+2, 1);
    for(int l:lost) cnt[l]--;
    for(int r:reserve) cnt[r]++;
    
    for(int i=1; i<=n; i++) {
        if(cnt[i] != 0) continue;
        if(cnt[i-1] == 2) { cnt[i-1]--; cnt[i]++; }
        else if(cnt[i+1] == 2) { cnt[i+1]--; cnt[i]++; }
    }
    
    for(int i=1; i<=n; i++) {
        if(cnt[i] > 0) ans++;
    }
    
    return ans;
}
```
- 옷의 유무 및 개수를 하나의 배열로 표시
- 특정 지점 앞에서부터는 주고받음이 완료된 상태이기 때문에 앞에 추가 옷이 있다면 그것을 먼저 받는 것이 이득
