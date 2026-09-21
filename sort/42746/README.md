```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

string solution(vector<int> numbers) {
    vector<string> nstr;
    for(int n : numbers) nstr.push_back(to_string(n));
    
    sort(nstr.begin(), nstr.end(), 
        [](const string& a, const string& b) {
            return a+b > b+a;
        });
    
    if(nstr[0] == "0") return "0";
    
    string answer;
    for(const auto& s : nstr) answer += s;
    return answer;
}
```
- 이것도 풀이 방식이 goat 합쳤을때 가장 큰수를 찾기 위해선 cmp 자체를 합쳐서 비교하는 형태로 가져갈것
- to_string() int형 string으로
