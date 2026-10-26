```cpp
#include <vector>
#include <string>
#include <algorithm>
#include <climits>
using namespace std;


int solution(vector<string> arr)
{
    vector<int> nums;
    vector<char> ops;
    for(int i=0; i<arr.size(); i++) {
        if(i%2==0) nums.push_back(stoi(arr[i]));
        else ops.push_back(arr[i][0]);
    }
    
    int n = nums.size();
    vector<vector<int>> mx(n, vector<int>(n, INT_MIN));
    vector<vector<int>> mn(n, vector<int>(n, INT_MAX));
    for(int i=0; i<n; i++) mx[i][i] = mn[i][i] = nums[i];
    
    for(int len=1; len<n; len++) {
        for(int i=0; i+len<n; i++) {
            int j = i + len;
            for(int k=i; k<j; k++) {
                if(ops[k] == '+') {
                    mx[i][j] = max(mx[i][j], mx[i][k] + mx[k+1][j]);
                    mn[i][j] = min(mn[i][j], mn[i][k] + mn[k+1][j]);
                }
                else {
                    mx[i][j] = max(mx[i][j], mx[i][k] - mn[k+1][j]);
                    mn[i][j] = min(mn[i][j], mn[i][k] - mx[k+1][j]);
                }
            }
        }
    }
    return mx[0][n-1];
}
```
- dp 문제는 문제 풀이과정에서 겹치는 과정이 있는 것 / 최적 부분 구조
- 이번 문제는 마지막 연산을 기준으로 +, -냐에 따라 계산 방식이 달라진다. 그렇기에 길이에 따라 모든 최적구조를 구성해두고 저장해둬서 마지막 결과값에서 까지 사용하는 형태
- 연산자도 k와 동일하게 사용되는게 반복되는 형태라고 했기 때문에 가능한 형태
