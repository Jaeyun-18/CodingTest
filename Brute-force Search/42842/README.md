```cpp
#include <string>
#include <vector>

using namespace std;

vector<int> solution(int brown, int yellow) {
    vector<int> answer;
    int total;
    total = (brown+4)/2;
    
    for(int i=3; i*2 <= total; i++) {
        if((i-2)*(total-i-2) == yellow) {
            answer.push_back(total-i);
            answer.push_back(i);
            break;
        }
    }
    
    return answer;
}
```
