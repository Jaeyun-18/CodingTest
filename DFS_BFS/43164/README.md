```cpp
#include <string>
#include <vector>
#include <unordered_map>
#include <algorithm>

using namespace std;

vector<string> solution(vector<vector<string>> tickets) {
    unordered_map<string, vector<string>> hash_map;
    vector<string> ans;
    vector<string> st = {"ICN"};
    
    for(const auto&t : tickets) {
        hash_map[t[0]].push_back(t[1]);
    }
    for(auto&p : hash_map) {
        sort(p.second.rbegin(), p.second.rend());
    }
    
    while(!st.empty()) {
        auto& nxt = hash_map[st.back()];
        if(!nxt.empty()) {
            st.push_back(nxt.back());
            nxt.pop_back();
        } else {
            ans.push_back(st.back());
            st.pop_back();
        }
    }
    
    reverse(ans.begin(), ans.end());
    
    return ans;
}
```
- 문제의 조건이 모든 티켓을 전부 사용하는 경로가 존재하고 그것을 찾아야함 -> 그렇기에 처음으로 나온 다음 행선지가 없는 티켓이 마무리 위치가 된다
- 역정렬은 rbegin, rend 형태로 사용할수도 있지만, sort(v.begin(), v.end(), greater<string>()); 이형태가 더 명시적임ㄴ
