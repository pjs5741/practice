문제 설명   
양의 정수 n이 주어집니다. 이 숫자를 k진수로 바꿨을 때, 변환된 수 안에 아래 조건에 맞는 소수(Prime number)가 몇 개인지 알아보려 합니다.   

0P0처럼 소수 양쪽에 0이 있는 경우   
P0처럼 소수 오른쪽에만 0이 있고 왼쪽에는 아무것도 없는 경우   
0P처럼 소수 왼쪽에만 0이 있고 오른쪽에는 아무것도 없는 경우   
P처럼 소수 양쪽에 아무것도 없는 경우   
단, P는 각 자릿수에 0을 포함하지 않는 소수입니다.  
예를 들어, 101은 P가 될 수 없습니다.
예를 들어, 437674을 3진수로 바꾸면 211020101011입니다. 여기서 찾을 수 있는 조건에 맞는 소수는 왼쪽부터 순서대로 211, 2, 11이 있으며, 총 3개입니다. (211, 2, 11을 k진법으로 보았을 때가 아닌, 10진법으로 보았을 때 소수여야 한다는 점에 주의합니다.) 211은 P0 형태에서 찾을 수 있으며, 2는 0P0에서, 11은 0P에서 찾을 수 있습니다.

정수 n과 k가 매개변수로 주어집니다. n을 k진수로 바꿨을 때, 변환된 수 안에서 찾을 수 있는 위 조건에 맞는 소수의 개수를 return 하도록 solution 함수를 완성해 주세요.

제한사항   
1 ≤ n ≤ 1,000,000   
3 ≤ k ≤ 10   


```
#include <string>
#include <vector>
#include <cmath>
#include <iostream>

using namespace std;

int solution(int n, int k) {
    int answer = 0;
    vector<int> v;
    int a=0, b=0,count=0,prime=0;
    double c=0;
    
    while(n>0)
    {
        v.push_back(n%k);
        n/=k;
    }
    for(int i=0;i<v.size();i++)
    {
        if(v[i]!=0)
        {
            a+=v[i]*pow(10,b);
            b++;            
        }
        
        if(v[i]==0 || i==v.size()-1)
        {
            cout<<a<<endl;
            c=sqrt(a);
            if(c-(int)c!=0)
            {
                for(int j=1;j<=a;j++)
                {               
                    if(a%j==0)
                        prime++;
                }
            }
                if(prime==2)
                    count++;
                a=0;
                b=0;
                prime=0;
              
        }
    }
    answer=count;
    return answer;
}
```

처음코드다. k진수로 변환해서 벡터 v에 넣어두고 변환이 끝나면 0을만나기전까지 a에다가 값을 저장하다가 0을 만나면 그 값이 소수인지 판단해서 맞으면 count++아니면 초기화후 다음 수 계산을 하는 코드인데 채점 후 제출을 하면 1번 테스트케이스에서 오류가 난다.


524287, 2의 테스트 케이스를 추가했다.
a를 담기에 int가 적합하지 않아서 long long으로 바꾸자 아예 오류가 나버린다 
b가 19까지 가는것을 보니 1이 19번 나오나 보다 이걸 줄여야될것같은데 검색해보니 모두다 to_string을 사용 문자열로 바꾸고 다시 stoi로 인트로바꾸었다. 다음에 그냥 다 지워버리고 다시만들어야겠다. 비슷한 문제를 이제 꽤 풀어봐서 할만 해진거 같다.

```
#include <bits/stdc++.h>
using namespace std;

bool is_prime(long long n) {
    if (n < 2) return false;
    for (long long i = 2; i * i <= n; ++i) if (n % i == 0) return false;
    return true;
}
int solution(int n, int k) {
    string str;
    while (n) {
        str += n % k + 48;
        n /= k;
    }

    reverse(str.begin(), str.end());
    str += 48;

    int ans = 0;
    for (long long hold = 0, i = 0; i < str.size(); ++i) {
        if (str[i] == '0') {
            if (is_prime(hold)) ++ans;
            hold = 0;
            continue;
        }
        hold = hold * 10 + str[i] - 48;
    }

    return ans;
}
```

다지우고 처음부터 해봤는데 실패했다. 바로앞까지온거같은데 아직 더 생각해봐야될듯하다