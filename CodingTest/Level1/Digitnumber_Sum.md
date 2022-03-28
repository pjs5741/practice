문제 설명

자연수 N이 주어지면, N의 각 자릿수의 합을 구해서 return 하는 solution 함수를 만들어 주세요.
예를들어 N = 123이면 1 + 2 + 3 = 6을 return 하면 됩니다.

제한사항

N의 범위 : 100,000,000 이하의 자연수

```
#include <iostream>

using namespace std;
int solution(int n)
{   

    int answer = 0;
    int a=1;
    for(int i=0;i<9;i++)
    {
        answer+=n/a%10;
        a*=10;
    }
    
    return answer;
}
```

하샤드문제 풀때 했던것 만들고 보니 저번 하샤드때보다 변수를 더 적게썻다. 더 잘해진듯 하다.