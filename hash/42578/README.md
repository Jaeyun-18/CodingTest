```cpp
#include <string>
#include <vector>
#include <unordered_map>

using namespace std;

int solution(vector<vector<string>> clothes) {
    unordered_map<string, int> cloth_type;
    int answer = 1;
    
    for(const auto&cloth : clothes) cloth_type[cloth[1]]++;
    
    for(const auto&p : cloth_type) answer *= (p.second + 1);
    
    return answer - 1;
}
```
- 문제풀이 방법이 중요한 문제 -> 옷의 타입마다 안입는 경우를 위해 +1해서 전체 곱 추가적으로 다 안입는 경우 제외 -1
- map도 for문을 이용한 순환이 가능함
