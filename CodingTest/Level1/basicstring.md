문제 설명


문자열 s의 길이가 4 혹은 6이고, 숫자로만 구성돼있는지 확인해주는 함수, solution을 완성하세요. 예를 들어 s가 "a234"이면 False를 리턴하고 "1234"라면 True를 리턴하면 됩니다.

제한 사항

s는 길이 1 이상, 길이 8 이하인 문자열입니다.

```
#include <string>
#include <vector>

using namespace std;

bool solution(string s) {
    bool answer = true;

    if(s.size()==4 || s.size()==6)
    {
        for(int i=0;i<s.size();i++)
        {
            if(!(s[i]>='0'&&s[i]<='9'))
            {
                answer = false;
                break;
            }
      
        }
    }
    else
    {
        answer = false;
    }
    return answer;
}
```

문자열 길이를 4혹은 6인지 확인후에 문자열이 0에서9가 아니면 false를 반환한다.

```
#include <string>
#include <vector>

using namespace std;

bool solution(string s) {
    bool answer = true;

    if(s.size()==4 || s.size()==6)
    {
        for(int i=0;i<s.size();i++)
        {
            if(s[i]>='0'&&s[i]<='9')
            {
                answer = true;         
            }
            else
            {
                answer = false;
            }
      
        }
    }
    else
    {
        answer = false;
    }
    return answer;
}
```

처음 했던 코드인데 이렇게 하니까 무조건으로 true값이 나와서 그냥 else문을 없애고 0부터9가 아니면으로 조건을 바꾼후에 처음 answer값이 true인 점을 활용했다.