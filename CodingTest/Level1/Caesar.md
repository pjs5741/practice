문제 설명

어떤 문장의 각 알파벳을 일정한 거리만큼 밀어서 다른 알파벳으로 바꾸는 암호화 방식을 시저 암호라고 합니다. 예를 들어 "AB"는 1만큼 밀면 "BC"가 되고, 3만큼 밀면 "DE"가 됩니다. "z"는 1만큼 밀면 "a"가 됩니다. 문자열 s와 거리 n을 입력받아 s를 n만큼 민 암호문을 만드는 함수, solution을 완성해 보세요.

제한 조건

공백은 아무리 밀어도 공백입니다.
s는 알파벳 소문자, 대문자, 공백으로만 이루어져 있습니다.
s의 길이는 8000이하입니다.
n은 1 이상, 25이하인 자연수입니다.

```
#include <string>
#include <cstring>
#include <vector>

using namespace std;

string solution(string s, int n) {
    string answer = "";
    for(int i=0;i<s.size();i++)
    {
        if(s[i] != ' ')
        {
            if(s[i]>='a'&&s[i]<='z')   
            {
                if(s[i]+n>'z')
                {
                    s[i]=s[i]+n-26;
                }
                else
                {
                    s[i]=s[i]+n;
                }
            }
            
            if(s[i]>='A'&&s[i]<='Z')   
            {
                if(s[i]+n>'Z')
                {
                    s[i]=s[i]+n-26;   
                }
                else
                {
                    s[i]=s[i]+n;
                }
            }
            
        }
        
    }
   
    answer=s;
    
    return answer;
}
```

소문자로 예를들면 a가 97,z가 122이므로 123때 97이 되게하기위해선 26을 빼야함으로 만든코드다.