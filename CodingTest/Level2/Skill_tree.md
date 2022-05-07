문제 설명   
선행 스킬이란 어떤 스킬을 배우기 전에 먼저 배워야 하는 스킬을 뜻합니다.   

예를 들어 선행 스킬 순서가 스파크 → 라이트닝 볼트 → 썬더일때, 썬더를 배우려면 먼저 라이트닝 볼트를 배워야 하고, 라이트닝 볼트를 배우려면 먼저 스파크를 배워야 합니다.   

위 순서에 없는 다른 스킬(힐링 등)은 순서에 상관없이 배울 수 있습니다. 따라서 스파크 → 힐링 → 라이트닝 볼트 → 썬더와 같은 스킬트리는 가능하지만, 썬더 → 스파크나 라이트닝 볼트 → 스파크 → 힐링 → 썬더와 같은 스킬트리는 불가능합니다.

선행 스킬 순서 skill과 유저들이 만든 스킬트리1를 담은 배열 skill_trees가 매개변수로 주어질 때, 가능한 스킬트리 개수를 return 하는 solution 함수를 작성해주세요.   

제한 조건    
스킬은 알파벳 대문자로 표기하며, 모든 문자열은 알파벳 대문자로만 이루어져 있습니다.   
스킬 순서와 스킬트리는 문자열로 표기합니다.   
예를 들어, C → B → D 라면 "CBD"로 표기합니다   
선행 스킬 순서 skill의 길이는 1 이상 26 이하이며, 스킬은 중복해 주어지지 않습니다.   
skill_trees는 길이 1 이상 20 이하인 배열입니다.   
skill_trees의 원소는 스킬을 나타내는 문자열입니다.   
skill_trees의 원소는 길이가 2 이상 26 이하인 문자열이며, 스킬이 중복해 주어지지 않습니다.   

```
#include <string>
#include <vector>

using namespace std;

int solution(string skill, vector<string> skill_trees) {
    
    int answer = 0;

    for(auto c:skill_trees)
    {
        string s="";
        string s1="";
        bool check=false;
        
        s1+=c;    
        for(auto a:s1)
        {
            for(auto b:skill)
            {
                if(a==b)
                {
                    s+=a;
                    break;
                }
            }
        }
    
        for(int i=0;i<s.size();i++)
        {
            if(skill[i]==s[i])
                check=true;
            else
            {
                check = false;
                break;
            }
        }
    
    
        if(check)
            answer++;
    }
    return answer;
}
```

처음에 만든코드인데 뭔가 당연하듯이 코드실행은 맞고 테스트케이스는 다틀렸다. 첫 for문에 s1+=c를 안하고 바로 넣으면 무슨 char를 string으로 변환할수없다면서 안되길래 벡터를 스트링으로 한번바꿔놓았다 그 후로 skill_trees에서 skill에있는 문자들을 확인해서 같은문자가있으면 s에 넣었고 중복이 없기때문에 s가 skill보다 사이즈가 작거나 같아서 s사이즈를 조사해 순서가 맞는지 확인하였다.

무엇을 틀렸는지 생각해보다가 알아낸게 만약 스킬트리에서 스킬에있는 문자열을 하나도 사용하지않았다면 그건 false가 아니라 true가 되어야 되는데 그걸 안건든것 같다.

```
#include <string>
#include <vector>

using namespace std;

int solution(string skill, vector<string> skill_trees) {
    
    int answer = 0;

    for(auto c:skill_trees)
    {
        string s="";
        string s1="";
        bool check=false;
        
        s1+=c;    
        for(auto a:s1)
        {
            for(auto b:skill)
            {
                if(a==b)
                {
                    s+=a;
                    break;
                }
            }
        }
    
        for(int i=0;i<s.size();i++)
        {
            if(skill[i]==s[i])
                check=true;
            else
            {
                check = false;
                break;
            }
        }
    
        if(check)
            answer++;
        else if(s=="")
            answer++;
    }
    return answer;
}
```

나이스