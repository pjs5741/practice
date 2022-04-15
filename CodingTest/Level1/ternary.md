문제 설명

자연수 n이 매개변수로 주어집니다. n을 3진법 상에서 앞뒤로 뒤집은 후, 이를 다시 10진법으로 표현한 수를 return 하도록 solution 함수를 완성해주세요.


제한사항

n은 1 이상 100,000,000 이하인 자연수입니다.

```
#include <string>
#include <vector>
#include <cmath>


using namespace std;

int solution(int n) {
    int answer = 0;
    int a=0;
    
    vector<int> v;
    
    while(n>0)
    {
        v.push_back(n%3);
        n/=3;
    }
    a=v.size()-1;
    for(int i=0;i<v.size();i++)
    {
       answer+=v[i]*pow(3,a);
        a--;
    }
    return answer;
}
```

2진법 만들때와 비슷할것 같아서 while로 삼진법으로 만들었고, v[0]부터 pow(3,v.size()-1)을 곱하고 v.size()를 1씩 줄이고 v[i]는 1씩 늘리면서 곱하기와 answer에 더하기하며 값을 구했다.