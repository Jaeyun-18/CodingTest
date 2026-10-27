```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

int solution(int distance, vector<int> rocks, int n) {
    sort(rocks.begin(), rocks.end());
    int h = 1;
    int t = distance+1;
    
    while(h < t) {
        int mid = h + (t-h)/2;
        int prev = 0;
        int remove = 0;
        for(int i=0; i<rocks.size(); i++) {
            if(remove > n) break;
            
            int dis = rocks[i] - prev;
            if(dis < mid) remove++;
            else prev = rocks[i];
            
            if(i == rocks.size()-1 && distance - prev < mid) remove++;
        }
        
        if(remove > n) t = mid;
        else h = mid+1;
    }
    
    return h-1;
}
```
- distance를 기준으로 이분탐색 진행
- 불가능한 형태를 남기는 방식으로 진행하기 때문에 h와 t의 변경이 다음 코드 처럼 변경된다
- 거리가 x보다 작을때 이전과 현재돌 중 삭제할 것을 정해야 함 -> 결과적으로 현재돌을 삭제하는 것이 다음돌과의 거리를 더 크게 유지할 수 있기 때문에 다음 로직을 선택
