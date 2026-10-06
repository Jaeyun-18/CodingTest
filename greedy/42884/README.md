```cpp
#include <string>
#include <vector>
#include <algorithm>
#include <iostream>

using namespace std;

int solution(vector<vector<int>> routes) {
    int ans = 0;
    
    sort(routes.begin(), routes.end(), [](const vector<int>& a, const vector<int>& b) {
        return a[1] < b[1];
    });
    
    int pre = routes[0][1];
    ans++;
    
    for(auto&r : routes) {
        if(pre >= r[0] && pre <= r[1]) continue;
        pre = r[1];
        ans++;
    }
    
    return ans;
}
```
- 자동차들의 경로를 나가는 지점에 오름차순으로 정렬함 -> 즉 처음 나가는 자동차의 마지막 부분에 카메라를 설치하고 해당 카메라에 다음 경로들이 속하지 않으면 카메라를 다시 설치하는 것
