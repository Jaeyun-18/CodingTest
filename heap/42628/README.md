```cpp
#include <string>
#include <vector>
#include <set>

using namespace std;

vector<int> solution(vector<string> operations) {
    multiset<int> ms;
    for(const auto& op : operations) {
        int num = stoi(op.substr(2));
        if(op[0] == 'I') {
            ms.insert(num);
        }
        else if(!ms.empty()) {
            if(num == 1) ms.erase(prev(ms.end()));
            else ms.erase(ms.begin());
        }
    }
    
    if(ms.empty()) return {0,0};
    else return {*ms.rbegin(), *ms.begin()};
}
```
- multiset 활용해서 구현
- set의 경우 index 접근이 안됨 그리고 오름차순 형태로 정렬됨. 그냥 set은 중복 허용 x
