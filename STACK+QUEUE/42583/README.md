```cpp
#include <string>
#include <vector>
#include <queue>

using namespace std;

int solution(int bridge_length, int weight, vector<int> truck_weights) {
    int time=0;
    int cnt=0;
    queue<int> q;
    
    int cur = 0;
    while(cnt != truck_weights.size()) {
        time++;
        if(!q.empty() && time - q.front() == bridge_length) {
            q.pop();
            cur-=truck_weights[cnt];
            cnt++;
        }

        int next = cnt + q.size();
        if(next < truck_weights.size() && cur + truck_weights[next] <= weight) {
            cur+=truck_weights[next];
            q.push(time);
        }
    }
    return time;
}
```
