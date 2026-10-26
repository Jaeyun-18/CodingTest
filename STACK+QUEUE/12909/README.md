```cpp
#include <string>
#include <iostream>
#include <stack>

using namespace std;

bool solution(string s)
{   
    stack<int> stack;
    
    stack.push(s[0]);
    for(int i=1; i<s.size(); i++) {
        if(s[i] == '(') stack.push('(');
        else if(s[i] == ')' && stack.size() != 0) stack.pop();
        else return false;
    }
    
    if(stack.size() == 0) return true;
    else return false;
}
```
