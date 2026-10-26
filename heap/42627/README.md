```cpp
#include <string>
#include <vector>
#include <queue>
#include <tuple>
#include <algorithm>

using namespace std;

int solution(vector<vector<int>> jobs) {
    using Data = tuple<int, int, int>;
    priority_queue<Data, vector<Data>, greater<Data>> pq;
    
    sort(jobs.begin(), jobs.end());
    
    int time=0;
    int complete=0;
    int cnt=0;
    int ans=0;
    while(complete != jobs.size()) {
        while(cnt < jobs.size() && jobs[cnt][0] <= time) {
            pq.push({jobs[cnt][1], jobs[cnt][0], cnt});
            cnt++;
        }
        
        if(pq.empty()) {
            time = jobs[cnt][0];
            continue;
        }
        
        auto [spendt, startt, num]  = pq.top(); pq.pop();
        time += spendt;
        ans += time - startt;
        complete++;
    }
    return ans/jobs.size();
}
```
- 시간 지남에 따라서 1초씩 증가시키는 것이 아니라 한번에 다음 끝나는 시점으로 옮겨서 소요 시간을 줄인다.
