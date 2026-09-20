```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

vector<int> solution(vector<int> array, vector<vector<int>> commands) {
    vector<int> ans;
    for(const auto&c : commands) {
        vector<int> newarray(array.begin()+c[0]-1, array.begin()+c[1]);
        sort(newarray.begin(), newarray.end());
        ans.push_back(newarray[c[2]-1]);
    }
    
    return ans;
}
```
- vector에 slice 해서 넣는 방법 -> (v.begin(), v.end())
  - 시작은 포함 마지막은 미포함
