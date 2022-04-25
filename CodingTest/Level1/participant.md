문제 설명   
수많은 마라톤 선수들이 마라톤에 참여하였습니다. 단 한 명의 선수를 제외하고는 모든 선수가 마라톤을 완주하였습니다.   

마라톤에 참여한 선수들의 이름이 담긴 배열 participant와 완주한 선수들의 이름이 담긴 배열 completion이 주어질 때, 완주하지 못한 선수의 이름을 return 하도록 solution 함수를 작성해주세요.   

제한사항   
마라톤 경기에 참여한 선수의 수는 1명 이상 100,000명 이하입니다.   
completion의 길이는 participant의 길이보다 1 작습니다.   
참가자의 이름은 1개 이상 20개 이하의 알파벳 소문자로 이루어져 있습니다.   
참가자 중에는 동명이인이 있을 수 있습니다.   

```
#include <string>
#include <vector>

using namespace std;

string solution(vector<string> participant, vector<string> completion) {
    string answer = "";
    for(int i=0;i<participant.size();i++)
    {
        for(int j=0;j<completion.size();j++)
        {
            if(participant[i]==completion[j])
            {
                participant.erase(participant.begin()+i);
                completion.erase(completion.begin()+j);
                i--;
                break;
            }
        }
    }
   answer+=participant[0];
    return answer;
}
```

처음코드로 실행해보니 다 맞았는데 효율성검사가 실패로나왔다.

```
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

string solution(vector<string> participant, vector<string> completion) {
    string answer = "";
    int j=0;
    sort(participant.begin(),participant.end());
    sort(completion.begin(),completion.end());
        for(int i=0;i<completion.size();i++)
        {
            if(participant[j]==completion[i])
            {
                participant.erase(participant.begin()+j);
                completion.erase(completion.begin()+i);
                i--;
                j--;
            }       
            j++;
         
        }
    if(answer.empty())
        answer+=participant[0];
    return answer;
}
```

두번째 코드 시간을 줄이기위해 for문 중첩을 없애려고 처음에 sort로 시작해서 n^2이 2nlogn+n이 되는줄알았는데 아니었나보다. 다시 효율성검사에걸렸다.
그래도 통과시간은 조금 빨라졌다.

```
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

string solution(vector<string> participant, vector<string> completion) {
    string answer = "";
    int j=0;
    sort(participant.begin(),participant.end());
    sort(completion.begin(),completion.end());
        for(int i=0;i<completion.size();i++)
        {
            if(participant[j]!=completion[i])
            {
                answer+=participant[j];
                j++;
            }       
            j++;
         
        }
    if(answer.empty())
        answer+=participant[participant.size()-1];
    return answer;
}
```

대망의 마지막 코드 erase를 안하고 그냥 다르면 answer에 그 문자열을 추가해버렸다. 그리해서 불필요한 연산을 줄여서 성공했다.