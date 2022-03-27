문제 설명

자연수 n을 뒤집어 각 자리 숫자를 원소로 가지는 배열 형태로 리턴해주세요. 예를들어 n이 12345이면 [5,4,3,2,1]을 리턴합니다.

제한 조건

n은 10,000,000,000이하인 자연수입니다.


```
#include <string>
#include <vector>

using namespace std;

vector<int> solution(long long n) {
    long long a=1;
    int b=0;
    vector<int> answer;
    
    while(n/a>0)
    {
       answer.push_back(n/a%10);
        a*=10;
        b++;
    }
    for(int i=answer.size();i>0;i--)
    {
        answer.push_back(answer[i-1]);
    }
    answer.erase(answer.begin() , answer.begin()+b);
    
    
    return answer;
}
```

처음코드인데 while문만 있으면 되는거였는데 잘못생각해서 밑에 for문을 만들어버렸다.
for문을 쓸려면 전에했던 배열문제에서 사용한 to_string을 사용하면 될 것같다.
내가 만든 코드는 밑에 것이다.

```
#include <string>
#include <vector>

using namespace std;

vector<int> solution(long long n) {
    long long a=1;
    vector<int> answer;
   
    
    while(n/a>0)
    {
       answer.push_back(n/a%10);
        a*=10;
    }
   
    
    return answer;
}
```
