문제 설명

함수 solution은 정수 n을 매개변수로 입력받습니다. n의 각 자릿수를 큰것부터 작은 순으로 정렬한 새로운 정수를 리턴해주세요. 예를들어 n이 118372면 873211을 리턴하면 됩니다.

제한 조건
n은 1이상 8000000000 이하인 자연수입니다.

```
#include <string>
#include <vector>

using namespace std;

long long solution(long long n) {
    long long answer = 0;
    int a =1;
    long long b =1;
    int c =0;
    int d =1;
    int temp =0;
    vector<long long> v;
    
    while(n/b>0)
    {
        b*=10;
        c++;
    }
    
    for(int i=0;i<c;i++)
    {
        v.push_back(n/a%10);
        a*=10; 
    }
    for(int j=0;j<v.size();j++)
    {
        for(int k=0;k<v.size();k++)
        {
            if(v[j]<v[k])
            {
                temp=v[k];
                v[k]=v[j];
                v[j]=temp;
            }
        } 
    }
    for(int e=0;e<v.size();e++)
    {
        answer+=d*v[e];
        d*=10;
    }
    return answer;
}
```

코드가 조금더럽긴한데 처음 while문으로 n이 몇자리수인지 알아보고 c에 저장했다.
그 후 콜라츠문제에서 사용한 코드를 가져와서 배열에 넣고 하나씩 비교해서 정렬을 하였다.
그리고 마지막에 배열안에 든 숫자들을 원래 크기의 숫자로 돌려놓고 더하면서 코드를 끝냈다.



```
#include <string>
#include <vector>
#include <algorithm>
#include <functional>
using namespace std;

long long solution(long long n) {
    long long answer = 0;

    string str = to_string(n);
    sort(str.begin(), str.end(), greater<char>());
    answer = stoll(str);

    return answer;
}
```
이 코드는 좋아요를 가장많이받은 코드인데 저렇게 긴 코드가 이렇게 짧아질수있다니 정말 대단하다고 느꼇다. to_string()과 stol,stoi,stof 등등 이번에 알게된 함수 다음부터 나도 써먹어야겠다.