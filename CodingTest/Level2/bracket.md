문제 설명   
괄호가 바르게 짝지어졌다는 것은 '(' 문자로 열렸으면 반드시 짝지어서 ')' 문자로 닫혀야 한다는 뜻입니다. 예를 들어   

"()()" 또는 "(())()" 는 올바른 괄호입니다.   
")()(" 또는 "(()(" 는 올바르지 않은 괄호입니다.   
'(' 또는 ')' 로만 이루어진 문자열 s가 주어졌을 때, 문자열 s가 올바른 괄호이면 true를 return 하고, 올바르지 않은 괄호이면 false를 return 하는 solution 함수를 완성해 주세요.   

제한사항   
문자열 s의 길이 : 100,000 이하의 자연수   
문자열 s는 '(' 또는 ')' 로만 이루어져 있습니다.  

```
#include<string>
#include <iostream>

using namespace std;

bool solution(string s)
{
    int counta=0;
    int countb=0;
    bool answer = true;
    for(int i:s)
    {
        if(i=='(')
            counta++;
         else if(i==')')
            countb++;
    }
    
    if(counta==countb)
        answer = true;
    else
        answer = false;
    return answer;
}
```

처음코드인데 생각을 너무 대충하고 풀었어서그런지 당연히 틀렸다. 이건 그냥 수만 샌거고 필요한건 '('와')'가 짝을 맞춰야한다는 것이다.

```
#include<string>
#include<vector>
#include <iostream>

using namespace std;

bool solution(string s)
{
    vector<string> v;
    bool answer = true;
    for(int i:s)
    {
        if(i=='(')
            v.push_back("(");
         else if(i==')' && !v.empty())
            v.pop_back();
        else if(i==')' && v.empty())
            v.push_back(")");
    }
    
    (v.empty())?answer = true:answer=false;
    
    return answer;
}
```

)로 시작하면 무조건 false이므로 '('로시작했을때 push_back , 만약 ')'일때 v가 비어있으면 ')'를 넣어서 false로 유도 '('가 들어있으면 삭제해서 짝을맞추고 true를 유도