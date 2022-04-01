문제 설명

문자열 s에 나타나는 문자를 큰것부터 작은 순으로 정렬해 새로운 문자열을 리턴하는 함수, solution을 완성해주세요.
s는 영문 대소문자로만 구성되어 있으며, 대문자는 소문자보다 작은 것으로 간주합니다.

제한 사항

str은 길이 1 이상인 문자열입니다.

```
#include <string>
#include <vector>

using namespace std;

string solution(string s) {
    string answer = "";
    char temp;
    for(int i=0;i<s.size();i++)
    {
        for(int j=0;j<s.size();j++)
        {
            if(s[i]>s[j])
            {
              temp=s[i];
                s[i]=s[j];
                s[j]=temp;
            }
        }
    }
    answer=s;
    return answer;
}
```

for문중첩하고 비교해서 순서를바꾼다.