```cpp
#include <vector>
#include <iostream>

using namespace std;

vector<int> solution(vector<int> arr) 
{
    vector<int> answer;
    int check = arr[0];
    
    answer.push_back(arr[0]);
    for(int i=1; i<arr.size(); i++) {
        if(arr[i] == check) continue;
        else {
            answer.push_back(arr[i]);
            check = arr[i];
        }
    }

    return answer;
}
```

```cpp
#include <vector>
#include <iostream>
#include <algorithm>
using namespace std;

vector<int> solution(vector<int> arr) 
{

    arr.erase(unique(arr.begin(), arr.end()),arr.end());

    vector<int> answer = arr;
    return answer;
}
```
- unique 함수 사용형태
- unique는 중복이 아닌 원소들을 당겨 채우고 새로운 위치의 반복자를 반환한다. 그 이후에 erase로 해당 반환자부터 end까지 지워 vector 크기를 줄임
