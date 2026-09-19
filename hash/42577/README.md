```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

bool solution(vector<string> phone_book) {
    sort(phone_book.begin(), phone_book.end());
    for(int i=0; i<phone_book.size() - 1; i++) {
        if(phone_book[i] == phone_book[i+1].substr(0, phone_book[i].size())) {
            return false;
        }
    }
    return true;
}
```
- string.substr(시작위치, 길이) -> string에서 추출하는 method
---
```cpp
#include <string>
#include <vector>
#include <unordered_map>

using namespace std;

bool solution(vector<string> phone_book) {
    bool answer = true;

    unordered_map<string, int> hash_map;
    for(int i = 0; i < phone_book.size(); i++)
        hash_map[phone_book[i]] = 1;

    for(int i = 0; i < phone_book.size(); i++) {
        string phone_number = "";
        for(int j = 0; j < phone_book[i].size(); j++) {
            phone_number += phone_book[i][j];
            if(hash_map.count(phone_number) && phone_number != phone_book[i])
              answer = false;
        }
    }
    return answer;
}
```
- phone_number를 hash에 저장, 그후에 각 phone_number 별로 자신을 제외한 접두사를 키로 하는 hash가 있는지 확인
