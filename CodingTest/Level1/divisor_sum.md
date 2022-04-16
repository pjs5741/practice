문제 설명

두 정수 left와 right가 매개변수로 주어집니다. left부터 right까지의 모든 수들 중에서, 약수의 개수가 짝수인 수는 더하고, 약수의 개수가 홀수인 수는 뺀 수를 return 하도록 solution 함수를 완성해주세요.


```
#include <string>
#include <vector>


using namespace std;

int solution(int left, int right) {
    int answer = 0;
    int count=0;
    
    for(left ;left<=right;left++)
    {
        for(int i=1;i<=left;i++)
        {
            if(left%i==0)
            {
                count++;
            }
        }
        if(count%2==0)
        {
            answer+=left;
        }
        else
        {
            answer-=left;
        }
        count=0;
    }
    return answer;
}
```

lftf와 right의 사이의 숫자를 찾기 위해 for문을 사용하고 그안에 약수를 찾기위해 for문 중첩으로 i에서 left까지 %로 약수를 알아보고 약수가 나올때마다 count를 ++한다.
그 후 count가 짝수면 left를 + 아니면 -해서 값이 구해진다.