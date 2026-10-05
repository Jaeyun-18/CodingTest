```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

string solution(string number, int k) {
    string ans;
    ans.reserve(number.size());
    
    for(auto&n : number) {
        while(k>0 && !ans.empty() && ans.back() < n) {
            ans.pop_back();
            k--;
        }
        ans.push_back(n);
    }
    
    ans.resize(ans.size()-k);
    return ans;
}
```
- 현재 숫자보다 작은 앞자리를 지워버리는 형태
- reserve는 메모리만 할당, resize로 해당 크기만큼 뒤에를 삭제한다 왜냐하면 남은것은 그럼 내림차순의 형태일것이기때문
- stack의 형태
