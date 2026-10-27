```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

long long solution(int n, vector<int> times) {
    long long h = 0;
    long long t = (long long)*max_element(times.begin(), times.end()) * n;
    
    while(h < t) {
        long long mid = h + (t - h) / 2;
        
        long long num = 0;
        for(int t : times) {
            num += mid / t;
            if(num >= n) break;
        }
        
        if(num >= n) t = mid;
        else h = mid+1;
    }
    
    return h;
}
```
- 이분 탐색 구현 방법
- 정렬된 배열에서 특정값 찾기 + 불가능에서 가능으로 변경되는 첫 지점 찾기
