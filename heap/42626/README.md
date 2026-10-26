```cpp
#include <string>
#include <vector>
#include <queue>

using namespace std;

int solution(vector<int> scoville, int K) {
    priority_queue<int, vector<int>, greater<int>> pq(scoville.begin(), scoville.end());
    
    int cnt=0;
    while(pq.size() != 1 && pq.top() < K) {
        int i, j;
        i = pq.top(); pq.pop();
        j = pq.top(); pq.pop();
        pq.push(i + j*2);
        cnt++;
    }
    
    if(pq.top() >= K) return cnt;
    else return -1;
}
```
- 힙은 특수한 큐칙이 있는 트리이고
- pq를 구현할때 heap을 사용하게 된다
