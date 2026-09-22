```cpp
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

vector<int> solution(vector<int> answers) {
    vector<int> n1 = {1,2,3,4,5};
    vector<int> n2 = {2,1,2,3,2,4,2,5};
    vector<int> n3 = {3,3,1,1,2,2,4,4,5,5};
    
    int score1 = 0;
    int score2 = 0;
    int score3 = 0;
    
    for(int i=0; i<answers.size(); i++) {
        if(answers[i] == n1[i%n1.size()]) score1++;
        if(answers[i] == n2[i%n2.size()]) score2++;
        if(answers[i] == n3[i%n3.size()]) score3++;
    }
    
    int max_score = max(score1, score2);
    max_score = max(max_score, score3);
    vector<int> answer;
    
    if(max_score == score1) answer.push_back(1);
    if(max_score == score2) answer.push_back(2);
    if(max_score == score3) answer.push_back(3);
    
    return answer;
}
```
