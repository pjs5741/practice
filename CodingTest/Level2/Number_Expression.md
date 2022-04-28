문제 설명    
Finn은 요즘 수학공부에 빠져 있습니다. 수학 공부를 하던 Finn은 자연수 n을 연속한 자연수들로 표현 하는 방법이 여러개라는 사실을 알게 되었습니다. 예를들어 15는 다음과 같이 4가지로 표현 할 수 있습니다.   

1 + 2 + 3 + 4 + 5 = 15   
4 + 5 + 6 = 15   
7 + 8 = 15   
15 = 15    
자연수 n이 매개변수로 주어질 때, 연속된 자연수들로 n을 표현하는 방법의 수를 return하는 solution를 완성해주세요.   

제한사항   
n은 10,000 이하의 자연수 입니다.    

```
#include <string>
#include <vector>

using namespace std;

int solution(int n) {
    int answer = 0;
    int count =0;
    int a=0;
    for(int i=0;i<n;i++)
    {
        for(int j=i+1;j<=n;j++)
        {
            a+=j;
            if(a==n)
                count++;
            if(a>n)
                break;
        }    
        a=0;
    }
    answer=count;
    return answer;
}
```

쉬웠다. for문을 두번써서 i의 값을 보존하면서 연속되는 수를 더하고 n을 넘으면 break n과 같으면 count++를 해서 연속되는수를 알아냈다.