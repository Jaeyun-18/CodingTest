```cpp
#include <string>
#include <vector>
#include <algorithm>
#include <numeric>

using namespace std;

vector<int> W;
vector<vector<int>> L;
int limit, cnt;

int dfs(int n) {
    int l, r;
    if(L[n][0] == -1) l=0;
    else l=dfs(L[n][0]);
    
    if(L[n][1] == -1) r=0;
    else r=dfs(L[n][1]);
    
    if(W[n] + l + r <= limit) return W[n] + l + r;
    else if(W[n] + min(l,r) <= limit) {
        cnt++;
        return W[n] + min(l,r);
    }
    cnt+=2;
    return W[n];
}


int solution(int k, vector<int> num, vector<vector<int>> links) {
    int n = num.size();
    W = num; L = links;
    
    vector<bool> ischild(n, false);
    for(auto& l : links) {
        for(int  c : l) if(c != -1) ischild[c] = true;
    }
    
    int root = 0;
    while(ischild[root]) root++;
    
    int h = *max_element(num.begin(), num.end());
    int t = accumulate(num.begin(), num.end(), 0);
    
    while(h < t) {
        int mid = (t+h)/2;
        limit = mid; cnt = 0;
        dfs(root);
        if(cnt <= k-1) t = mid;
        else h = mid+1;
    }
    
    return h;
}
```
- 이분탐색으로 풀이 (최적값을 찾기는 어렵지만 x로 가능한가는 판단하기 쉬울때 사용하는 형태)
- 특정 값보다 작게 만들려면 몇개의 그룹이 필요한지를 확인
   - 몇개의 그룹이 필요한지는 dfs를 사용 leaf에서 올라오면서 특정 부분보다 크다면 버리는 그룹을 추가하는 즉 링크를 자르는 형태로 확인가능함
