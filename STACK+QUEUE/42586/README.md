```cpp
#include <string>
#include <vector>
#include <queue>

using namespace std;

vector<int> solution(vector<int> progresses, vector<int> speeds) {
    vector<int> answer;
    queue<int> q;
    
    int t=0;
    for(int i=0; i<progresses.size(); i++) {
        t = (100-progresses[i]) / speeds[i];
        if((100-progresses[i]) % speeds[i] != 0) t++;
        q.push(t);
        t=0;
    }
    
    int cur = 0;
    int cnt = 0;
    while(q.size() > 0) {
        cur = q.front(), cnt++, q.pop();
        while(!q.empty() && q.front() <= cur) {
            q.pop();
            cnt++;
        }
        answer.push_back(cnt);
        cnt=0;
    }
    
    return answer;
}
```
- queue 사용법
