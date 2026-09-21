```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

int solution(vector<int> citations) {
    sort(citations.begin(), citations.end());
    
    for(int i=0; i<citations.size(); i++) {
        if(citations[i] >= citations.size() - i)
            return citations.size()-i;
    }
    return 0;
}
```
- 풀이방식 : 결과적으로 논문의 총 갯수가 h의 최댓값을 정함 거기에서 부터 한개씩 내려오면서 인용수와 h를 비교
- 해당 인용수가 h 이상이면 그것이 max H-index가 된다
