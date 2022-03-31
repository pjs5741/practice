문제 설명

JadenCase란 모든 단어의 첫 문자가 대문자이고, 그 외의 알파벳은 소문자인 문자열입니다. 단, 첫 문자가 알파벳이 아닐 때에는 이어지는 알파벳은 소문자로 쓰면 됩니다. (첫 번째 입출력 예 참고)
문자열 s가 주어졌을 때, s를 JadenCase로 바꾼 문자열을 리턴하는 함수, solution을 완성해주세요.

제한 조건

s는 길이 1 이상 200 이하인 문자열입니다.
s는 알파벳과 숫자, 공백문자(" ")로 이루어져 있습니다.
숫자는 단어의 첫 문자로만 나옵니다.
숫자로만 이루어진 단어는 없습니다.
공백문자가 연속해서 나올 수 있습니다.

```
#include <string>
#include <vector>

using namespace std;

string solution(string s) {
    string answer = "";
    bool a =true;
    for(int i=0;i<s.size();i++)
    {
        if(s[i]>='a'&&s[i]<='z' &&a==true)
        {
            s[i]=toupper(s[i]);
            a = false;
        }
        else if(a==true)
        {
            a = false;
        }
        else if(s[i] == ' ')
        {
            a = true;
        }
        else
        {
            s[i]=tolower(s[i]);
        }
        
    }
    answer = s;
    return answer;
}
```

위는 처음 만든 코드인데 테스트를 성공하고 제출해보니 몇몇개가 안되는 것을 확인했다.
이런 문제는 거의 공백이 두개 들어가면 오류가 나는 것을 생각해보고 테스트케이스에 공백2개인 문자열을 넣어보니 역시나 공백이 연속으로 나오면 오류가 나오는 것을 확인했다.

```
        else if(a==true)
        {
            a = false;
        }
        else if(s[i] == ' ')
        {
            a = true;
        }
```
이 부분때문에 공백이 홀수번때는 잘 작동되고 짝수번이면 오류가 나는 걸 확인해서

```
#include <string>
#include <vector>

using namespace std;

string solution(string s) {
    string answer = "";
    bool a =true;
    for(int i=0;i<s.size();i++)
    {
        if(a==true&&s[i]!=' ')
        {
            a=false;
            if(s[i]>='a'&&s[i]<='z')
            {
            s[i]=toupper(s[i]);
            }   
        }
        else if(s[i] == ' ')
        {
            a = true;
        }
        else
        {
            s[i]=tolower(s[i]);
        }
        
    }
    answer = s;
    return answer;
}
```

a가 true면서 공백이 아닐시에 if문이 돌아가도록 바꾸니까 해결되었다.