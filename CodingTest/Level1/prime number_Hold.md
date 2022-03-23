1부터 입력받은 숫자 n 사이에 있는 소수의 개수를 반환하는 함수, solution을 만들어 보세요.

소수는 1과 자기 자신으로만 나누어지는 수를 의미합니다.
(1은 소수가 아닙니다.)

제한 조건
n은 2이상 1000000이하의 자연수입니다.

```
#include <string>
#include <vector>

using namespace std;

int solution(int n) {
    int answer = 0;
    int count=0;
    int a=1;
    int b=1;
    for(int i=0;i<n-1;i++)
    {
        a++;
        for(int j=0;j<i+1;j++)
        {
            b++;
            if(a%b==0)
            {
                count++;  
            }
          
             if(count==2)
                break;
            
        }
       
        
        if(count==1)
        {
        answer++;
        }
        count=0;
        b=1;
      
    }
    return answer;
}
```

이 코드는 수가적으면 잘 작동되지만 수가 높아질수록 검사가 길어져서 효용성문제로 풀어지지않았다. 지금 나로는 어찌해야될지 도저히 생각이안나서 검색의 힘을 살짝 빌려서 더 알아보고 다음에 다시 해봐야 될 듯 하다.