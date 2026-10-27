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
- 풀이방식은 각 심사관이 쉬지 않고 진행될때가 최소값을 포함하기 때문에 시간이 주어졌을때 심사관이 몇명을 심사할수 있는지를 보는 것으로 결과를 도출한다.
