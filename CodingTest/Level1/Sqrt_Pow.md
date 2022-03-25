문제 설명


임의의 양의 정수 n에 대해, n이 어떤 양의 정수 x의 제곱인지 아닌지 판단하려 합니다.
n이 양의 정수 x의 제곱이라면 x+1의 제곱을 리턴하고, n이 양의 정수 x의 제곱이 아니라면 -1을 리턴하는 함수를 완성하세요.

제한 사항
n은 1이상, 50000000000000 이하인 양의 정수입니다.

```
#include <string>
#include <vector>
#include <cmath>

using namespace std;

long long solution(long long n) {
    long long answer = 0;
    double x=0;
    
    x=sqrt(n);
    
    if(x-(int)x==0)
    {
        answer = pow(x+1,2);
        return answer;
    }
    else
    {
        return -1;
    }
    
}
```

x가 정수이므로 n의 제곱근은 정수면 끝나는 문제라서 double로 소수점을 파악할 수 있게한 후에 int로 형변환시켜서 빼면 정수일시에는 소수점이남아서 if문을 충족할수없고 정수면 0이되어서 충족이 되기때문에 조건식을 저렇게 만들었다..