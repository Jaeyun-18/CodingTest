```cpp
#include <string>
#include <vector>
#include <algorithm>
#include <functional>

using namespace std;

int solution(vector<int> people, int limit) {
    int ans=0;
    sort(people.begin(), people.end(), greater<int>());
    
    int h=0, t=people.size()-1;
    while(h <= t) {
        if(people[h] + people[t] <= limit) t--;
        ans++;
        h++;
    }
    
    return ans;
}
```
- 정렬해서 앞뒤로 찾아가는 형태
