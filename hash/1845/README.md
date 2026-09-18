```cpp
#include <vector>
#include <unordered_map>
using namespace std;

int solution(vector<int> nums)
{
    int answer = 0;
    int num = nums.size() / 2;
    unordered_map<int, int> cnt;
    
    for(const auto&i : nums) cnt[i]++;
    
    if(cnt.size() > num || cnt.size() == num) return num;
    else
        return cnt.size();
}
```
- map.size() 맵 사이즈 반환
- algorithm include 해서 min(cnt.size(), nums.size() / 2)가 더 깔끔함

---
```cpp
#include <bits/stdc++.h>
using namespace std;

int solution(vector<int> nums) {
    unordered_set<int> s(nums.begin(), nums.end());

    return min(nums.size() / 2, s.size());
}
```
- set 컨테이너 타입 - 중복되는거는 저장하지 않는 형태
