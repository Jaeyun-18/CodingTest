```cpp
#include <string>
#include <vector>

using namespace std;
int solution(string word) {
    int weight[5] = {781, 156, 31, 6, 1};
    const string v = "AEIOU";
    
    int answer = word.size();
    for(int i=0; i<word.size(); i++) {
        answer += v.find(word[i]) * weight[i];
    }
    
    return answer;
}
```
- string.find() 하면 몇번 인덱스에 있는지 확인하 수 있음 + 위치별로 가중치를 따로 줌
```cpp
#include <string>
#include <vector>
using namespace std;

const string V = "AEIOU";
int cnt = 0, answer = 0;

void dfs(const string& cur, const string& target) {
    if (answer) return;               // 찾았으면 조기 종료
    for (char c : V) {
        string next = cur + c;
        cnt++;
        if (next == target) { answer = cnt; return; }
        if (next.size() < 5) dfs(next, target);
        if (answer) return;
    }
}

int solution(string word) {
    cnt = 0; answer = 0;
    dfs("", word);
    return answer;
}
```
- 완전탐색 방법 AEIOU 형태로 하나씩 추가하면서 target과 동일한 형태가 있는지 확인하는 것
- 탈출 조건은 answer가 생겼을때 / 반복하는 형태의 사이즈가 5보다 커지면 안되기 때문에 next.size() < 5 형태로 방어
