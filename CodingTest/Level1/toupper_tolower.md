문제 설명

문자열 s는 한 개 이상의 단어로 구성되어 있습니다. 각 단어는 하나 이상의 공백문자로 구분되어 있습니다. 각 단어의 짝수번째 알파벳은 대문자로, 홀수번째 알파벳은 소문자로 바꾼 문자열을 리턴하는 함수, solution을 완성하세요.

제한 사항

문자열 전체의 짝/홀수 인덱스가 아니라, 단어(공백을 기준)별로 짝/홀수 인덱스를 판단해야합니다.
첫 번째 글자는 0번째 인덱스로 보아 짝수번째 알파벳으로 처리해야 합니다.
```
#include <string>
#include <vector>
#include <iostream>

using namespace std;

string solution(string s) {
    string answer = "";
    int a=0;
    for(int i=0;i<s.size();i++)
    {
        if(s[i] != ' ')
        {
            if(a%2==0)
            {
                s[i]=toupper(s[i]);
            }
            else if(a%2!=0)
            {
                s[i]=tolower(s[i]);
            }
            a++;
            
        }
        else
        {
            a=0;
            
        }
    }
    answer = s;
    
    return answer;
}
```
공백을 읽어서 공백이있으면 a를 초기화하고 아니면 쭉가서 홀수 짝수를 읽게하고 첫글자를 대문자로 만드는 함수를 만들었다.


 toupper(), tolower() 함수는 솔직히 이문제를 보고 짝수 홀수를 어떻게만드는지 처음보고 감도안잡혀서 검색해서 알아냈다.

```
int tolower(int c)
{
if ((c >= 'A') && (c <= 'Z'))
{
c = c - 'A' + 'a';
}
return c;
}
int toupper(int c)
{
if ((c >= 'a') && (c <= 'z'))
{
c = c - 'a' + 'A';
}
return c;
}

```
이렇게하면 아스키 코드의 숫자의 차이때문에 대문자, 소문자로 변환이 가능하다고 한다.

