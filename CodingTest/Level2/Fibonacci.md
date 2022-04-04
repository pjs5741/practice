문제 설명

피보나치 수는 F(0) = 0, F(1) = 1일 때, 1 이상의 n에 대하여 F(n) = F(n-1) + F(n-2) 가 적용되는 수 입니다.

예를들어

F(2) = F(0) + F(1) = 0 + 1 = 1
F(3) = F(1) + F(2) = 1 + 1 = 2
F(4) = F(2) + F(3) = 1 + 2 = 3
F(5) = F(3) + F(4) = 2 + 3 = 5
와 같이 이어집니다.

2 이상의 n이 입력되었을 때, n번째 피보나치 수를 1234567으로 나눈 나머지를 리턴하는 함수, solution을 완성해 주세요.

제한 사항

n은 2 이상 100,000 이하인 자연수입니다.

```
#include <string>
#include <vector>

using namespace std;

int solution(int n) {
    int answer = 0;
    vector<int> v;
    
    v.push_back(0);
    v.push_back(1);
    for(int i=2;i<=n;i++)
    {
        v.push_back(v[i-1]+v[i-2]);
    }
    
    answer=v[n]%1234567;
    
    return answer;
}
```

처음만든 코드, 테스트 6까지는 통과하는데 7부터14까지 실패한다.
생각해본결과 n이 10만이되면 정수값을 넘어갈 수도 있어서 그런건가 해서 long으로 바꿔봤는데도 똑같이 오류가 났다.
그 후 질문하기를 들어가보니까 (v[i-1]%1234567+v[i-2]%1234567)%1234567과(v[i-1]+v[i-2])%1234567이 같다고 하는 글이 있어서 해보니 바로 해결되었다.

```
#include <string>
#include <vector>

using namespace std;

int solution(int n) {
    int answer = 0;
    vector<unsigned long> v;
    
    v.push_back(0);
    v.push_back(1);
    
    for(int i=2;i<=n;i++)
    {
        v.push_back(v[i-1]%1234567+v[i-2]%1234567);
    }
    answer = v[n]%1234567;
    
    
    
    return answer;
}
```