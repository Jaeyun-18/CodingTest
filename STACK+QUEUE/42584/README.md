```cpp
#include <string>
#include <vector>
#include <stack>

using namespace std;

vector<int> solution(vector<int> prices) {
    stack<int> s;
    vector<int> ans(prices.size());
    
    for(int i=0; i<prices.size(); i++) {
        while(!s.empty() && prices[s.top()] > prices[i]) {
            int j = s.top();
            s.pop();
            ans[j] = i - j;
        }
        s.push(i);
    }
    
    while(!s.empty()) {
        int j = s.top();
        s.pop();
        ans[j] = prices.size() - j - 1;
    }
    
    return ans;
}
```
