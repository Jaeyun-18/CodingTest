```cpp
#include <string>
#include <vector>
#include <queue>
#include <algorithm>

using namespace std;

int solution(vector<int> priorities, int location) {
    queue<int> q;
    vector<int> prior_sort;
    for(int i=0; i<priorities.size(); i++) {
        q.push(i);
        prior_sort.push_back(priorities[i]);
    }
    
    sort(prior_sort.begin(), prior_sort.end());
    
    int check = -1;
    int cnt = 0;
    while(check != location) {
        int cur = q.front();
        if(priorities[cur] == prior_sort.back()) {
            check = cur;
            cnt++;
            q.pop();
            prior_sort.pop_back();
        } else {
            int num = q.front();
            q.pop();
            q.push(num);
        }
    }
    
    return cnt;
}
```
