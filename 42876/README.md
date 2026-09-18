# vector를 각각 sort한 후에 위치가 다른 것을 찾아내는 방식
```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

string solution(vector<string> participant, vector<string> completion) {
    string answer = "";
    
    sort(participant.begin(), participant.end());
    sort(completion.begin(), completion.end());
    
    for(int i=0; i<completion.size(); i++) {
        if(participant[i] != completion[i]) 
            return participant[i];
    }
    return participant[participant.size() - 1];
}
```
---
# 해시 테이블을 사용한 방식
```cpp
#include <string>
#include <vector>
#include <unordered_map>

string solution(vector<string> participant, vector<string> completion) {
    unordered_map<string, int> cnt;
    for (const auto& c : completion) cnt[c]++;
    for (const auto& p : participant)
        if (--cnt[p] < 0) return p;
    return "";
}
```
- string을 키로 정수를 값으로 갖는 해시맵
- const auto& c : completion -> 컨테이너의 원소를 처음부터 하나씩 꺼낸다는 의미 (auto가 타입을 알아서 추론, const는 읽기만 하는 형태일때)
- 해시맵에 없는 키가 새로 만들어질때는 0으로 넣음 / 중요한건 []로 조회하면 바로 생기기 때문에 count, find, contains 형태로 순환해야 키값이 안생김
