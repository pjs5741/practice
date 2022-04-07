다트 게임

카카오톡에 뜬 네 번째 별! 심심할 땐? 카카오톡 게임별~

Game Star

카카오톡 게임별의 하반기 신규 서비스로 다트 게임을 출시하기로 했다. 다트 게임은 다트판에 다트를 세 차례 던져 그 점수의 합계로 실력을 겨루는 게임으로, 모두가 간단히 즐길 수 있다.  
갓 입사한 무지는 코딩 실력을 인정받아 게임의 핵심 부분인 점수 계산 로직을 맡게 되었다. 다트 게임의 점수 계산 로직은 아래와 같다.  

다트 게임은 총 3번의 기회로 구성된다.  
각 기회마다 얻을 수 있는 점수는 0점에서 10점까지이다.  
점수와 함께 Single(S), Double(D), Triple(T) 영역이 존재하고 각 영역 당첨 시 점수에서 1제곱, 2제곱, 3제곱 (점수1 , 점수2 , 점수3 )으로 계산된다.  
옵션으로 스타상(&#42;) , 아차상(#)이 존재하며 스타상(&#42;) 당첨 시 해당 점수와 바로 전에 얻은 점수를 각 2배로 만든다. 아차상(#) 당첨 시 해당 점수는 마이너스된다.  
스타상()은 첫 번째 기회에서도 나올 수 있다. 이 경우 첫 번째 스타상(&#42;)의 점수만 2배가 된다. (예제 4번 참고)  
스타상(&#42;)의 효과는 다른 스타상(&#42;)의 효과와 중첩될 수 있다. 이 경우 중첩된 스타상(&#42;) 점수는 4배가 된다. (예제 4번 참고)  
스타상(&#42;)의 효과는 아차상(#)의 효과와 중첩될 수 있다. 이 경우 중첩된 아차상(#)의 점수는 -2배가 된다. (예제 5번 참고)  
Single(S), Double(D), Triple(T)은 점수마다 하나씩 존재한다.  
스타상(&#42;), 아차상(#)은 점수마다 둘 중 하나만 존재할 수 있으며, 존재하지 않을 수도 있다.  
0~10의 정수와 문자 S, D, T, &#42;, #로 구성된 문자열이 입력될 시 총점수를 반환하는 함수를 작성하라.  

입력 형식
"점수|보너스|[옵션]"으로 이루어진 문자열 3세트.  
예) 1S2D&#42;3T

점수는 0에서 10 사이의 정수이다.  
보너스는 S, D, T 중 하나이다.  
옵선은 &#42;이나 # 중 하나이며, 없을 수도 있다.  
출력 형식  
3번의 기회에서 얻은 점수 합계에 해당하는 정수값을 출력한다.  
예) 37  

```
#include <string>
#include <cmath>
#include <vector>

using namespace std;

int solution(string dartResult) {
    int answer = 0;
    vector<int> v;
    int j=0;
    for(int i=0;i<dartResult.size();i++)
    {
        if(dartResult[i]=='S'||dartResult[i]=='D'||dartResult[i]=='T')
        {
            if(dartResult[i]=='S')
            {
                v.push_back(dartResult[i-1]);
                j++;
            }
             if(dartResult[i]=='D')
             {
                v.push_back(pow(dartResult[i-1],2));
                 j++;
             }
             if(dartResult[i]=='T')
             {
                v.push_back(pow(dartResult[i-1],3));
                 j++;
             }
        }
        if(dartResult=="*" ||dartResult=="#")
        {
            if(dartResult=="*")
            {
                if(j!=1)
                {
                v[j-1]*=2;
                v[j-2]*=2;
                }
                else
                    v[j-1]*=2;
            }
            if(dartResult=="#")
            {
               v[j-1]*=-1;
            }
        }
    }
    
    return answer;
}
```

처음코드 짜면서 숫자가 아스키코드로 바뀔것같았는데 생각대로 그렇게 되서 다시 만들어야됬다.

예전에 봤던 stoi를 사용해서 풀어볼랬는데 k=stoi(dartResult[i-1])이렇게 넣으면 오류가 나서 써보진 못했고 그냥 -48을 하는 방법으로 풀어보았다.

```
#include <string>
#include <cmath>
#include <vector>
#include <iostream>

using namespace std;

int solution(string dartResult) {
    int answer = 0;
    vector<int> v;
    int j=0;
    for(int i=0;i<dartResult.size();i++)
    {
        if(dartResult[i]=='S'||dartResult[i]=='D'||dartResult[i]=='T')
        {
            if(dartResult[i]=='S')
            {
                v.push_back(dartResult[i-1]-48);  
                j++;
                
            }
             if(dartResult[i]=='D')
             {
                 
                 v.push_back(pow(dartResult[i-1]-48,2));
                 j++;
             }
             if(dartResult[i]=='T')
             {
                v.push_back(pow(dartResult[i-1]-48,3));
                 j++;
             }
        }
        if(dartResult[i]=='*' ||dartResult[i]=='#')
        {
            if(dartResult[i]=='*')
            {
                if(j!=1)
                {
                v[j-1]*=2;
                v[j-2]*=2;
                }
                else
                    v[j-1]*=2;
            }
            if(dartResult[i]=='#')
            {
               v[j-1]*=-1;
            }
        }
    }
    for(int k=0;k<v.size();k++)
    {
        answer+=v[k];
        cout<<v[k]<<endl;
    }
    
    return answer;
}
```
했는데 숫자 범위가 10까지여서 10이나오면 오류가 나오게된다 이 문제는
```
 for(int i=0;i<dartResult.size();i++)
    {
        if(dartResult[i]=='1')
        {
            if(dartResult[i+1]=='0')
                v.push_back(10);
        }...
```
이 코드를 추가해서 해결했는데 채점 후 제출을 눌러보니 4에서 7번이 오류가 났고 10D4S10D 204 테스트케이스를 추가해보래서 해봤더니 이것이 문제였다. 1과0인데 가만히 나두면 당연히 S D T 앞에있는 0을 검사할 것이고 그러면 바로 오류가 나는 것이라고 생각해서 고치고 최종 코드는

```
#include <string>
#include <cmath>
#include <vector>
#include <iostream>

using namespace std;

int solution(string dartResult) {
    int answer = 0;
    vector<int> v;
    int j=0;
    
    for(int i=0;i<dartResult.size();i++)
    {
        
        if(dartResult[i]=='S'||dartResult[i]=='D'||dartResult[i]=='T')
        {
            if(dartResult[i-1]=='0')
            {
                if(dartResult[i-2]=='1')
                {
                    v.push_back(10);
                }
                else
                    v.push_back(dartResult[i-1]-48);
            }
                else
                    v.push_back(dartResult[i-1]-48);
            if(dartResult[i]=='S')
            {
                j++;           
            }
             if(dartResult[i]=='D')
             {
                 j++;
                 v[j-1]=pow(v[j-1],2);
             }
             if(dartResult[i]=='T')
             {
                 j++;
                 v[j-1]=pow(v[j-1],3);
             }
        }
        if(dartResult[i]=='*' ||dartResult[i]=='#')
        {
            if(dartResult[i]=='*')
            {
                if(j!=1)
                {
                v[j-1]*=2;
                v[j-2]*=2;
                }
                else
                    v[j-1]*=2;
            }
            if(dartResult[i]=='#')
            {
               v[j-1]*=-1;
            }
        }
    }
    for(int k=0;k<v.size();k++)
    {
        answer+=v[k];
        cout<<v[k]<<endl;
    }
    
    return answer;
}
```
이렇게 끝났다.