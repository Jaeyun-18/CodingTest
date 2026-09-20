```cpp
#include <string>
#include <vector>
#include <unordered_map>
#include <algorithm>

using namespace std;

vector<int> solution(vector<string> genres, vector<int> plays) {
    vector<int> answer;
    unordered_map<string, int> genres_count;
    unordered_map<string, vector<pair<int, int>>> genre_song;
    
    for(int i=0; i<genres.size(); i++) {
        genres_count[genres[i]] += plays[i];
        genre_song[genres[i]].push_back({plays[i], i});
    }
    
    vector<pair<int, string>> sortgenre;
    for(const auto&g : genres_count) sortgenre.push_back({g.second, g.first});
    sort(sortgenre.begin(), sortgenre.end(), 
        [](const pair<int, string>& a, const pair<int, string>& b) {
            return a.first > b.first;
        });
    
    for(const auto&g : sortgenre) {
        auto& songs = genre_song[g.second];
        sort(songs.begin(), songs.end(), 
            [](const pair<int, int>& a, const pair<int, int>& b) {
                return a.first > b.first;
            });
        
        for(int i=0; i<min((int)songs.size(), 2); i++) answer.push_back(songs[i].second);
    }
    
    return answer;
}
```
- auto& 를 사용하는건 type으로 인한 오류를 방지
  - 추가적으로 auto&를 사용하면 값을 참조하며 수정시 원래 형태도 수정된다
- sort(,,cmp) cmp의 문구를 통해 sort를 진행한다
  - cmp가 true면 최종 결과에서 a가 b보다 앞에 놓인다
- utility를 include를 해야 pair를 사용할 수 있음
