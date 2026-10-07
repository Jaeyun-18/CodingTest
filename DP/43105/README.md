```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

int solution(vector<vector<int>> triangle) {
    for(int i=1; i<triangle.size(); i++) {
        for(int j=0; j<i+1; j++) {
            if(j == 0) triangle[i][j] += triangle[i-1][0];
            else if(j == i) triangle[i][j] += triangle[i-1][i-1];
            else triangle[i][j] += max(triangle[i-1][j-1], triangle[i-1][j]);
        }
    }
    
    int l = triangle.size();
    sort(triangle[l-1].begin(), triangle[l-1].end());
    return triangle[l-1][l-1];
}
```
- 아래에서 위로 올라가는 방법도 있음
