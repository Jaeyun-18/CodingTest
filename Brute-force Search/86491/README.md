```cpp
int solution(vector<vector<int>> sizes) {
    int w = 0, h = 0;
    for (auto& s : sizes) {
        int a = max(s[0], s[1]);
        int b = min(s[0], s[1]);
        w = max(w, a);
        h = max(h, b);
    }
    return w * h;
}
```
- wide와 height의 차이가 없기 때문에 w,h 중 작은값을 저장하는 곳과 큰 값을 저장하는 곳으로 구별지어서 탐색함.
