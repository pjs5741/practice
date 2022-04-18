문제 설명   
실패율   
슈퍼 게임 개발자 오렐리는 큰 고민에 빠졌다. 그녀가 만든 프랜즈 오천성이 대성공을 거뒀지만, 요즘 신규 사용자의 수가 급감한 것이다. 원인은 신규 사용자와 기존 사용자 사이에 스테이지 차이가 너무 큰 것이 문제였다.   

이 문제를 어떻게 할까 고민 한 그녀는 동적으로 게임 시간을 늘려서 난이도를 조절하기로 했다. 역시 슈퍼 개발자라 대부분의 로직은 쉽게 구현했지만, 실패율을 구하는 부분에서 위기에 빠지고 말았다. 오렐리를 위해 실패율을 구하는 코드를 완성하라.

* 실패율은 다음과 같이 정의한다.   
    * 스테이지에 도달했으나 아직 클리어하지 못한 플레이어의 수 / 스테이지에 도달한 플레이어 수

전체 스테이지의 개수 N, 게임을 이용하는 사용자가 현재 멈춰있는 스테이지의 번호가 담긴 배열 stages가 매개변수로 주어질 때, 실패율이 높은 스테이지부터 내림차순으로 스테이지의 번호가 담겨있는 배열을 return 하도록 solution 함수를 완성하라.

제한사항   
스테이지의 개수 N은 1 이상 500 이하의 자연수이다.   
stages의 길이는 1 이상 200,000 이하이다.   
stages에는 1 이상 N + 1 이하의 자연수가 담겨있다.   
각 자연수는 사용자가 현재 도전 중인 스테이지의 번호를 나타낸다.   
단, N + 1 은 마지막 스테이지(N 번째 스테이지) 까지 클리어 한 사용자를 나타낸다.   
만약 실패율이 같은 스테이지가 있다면 작은 번호의 스테이지가 먼저 오도록 하면 된다.   
스테이지에 도달한 유저가 없는 경우 해당 스테이지의 실패율은 0 으로 정의한다.   
입출력 예   
|N	|stages	|result|
|---|---|---|   
|5	|[2, 1, 2, 6, 2, 4, 3, 3]|	[3,4,2,1,5]|
|4	|[4,4,4,4,4]|	[4,1,2,3]|

```
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

vector<int> solution(int N, vector<int> stages) {
    vector<int> answer;  
    float v[N][2];
    vector<float> v2;  
    float a=stages.size();
    float count=0;
    float temp=0;
    
    for(int stage=0;stage<N;stage++)
    {
        
        for(int i=0;i<stages.size();i++)
        {
            if(stages[i]==stage+1)
            {
                count++;
            }
        }
        v[stage][1]=count/a;
        v[stage][0]=stage+1;
        a-=count;
        count=0;
    }
    
    for(int i=0;i<N-1;i++)
    {
        for(int j=0;j<N-1;j++)
        {
            if(v[j][1]<v[j+1][1])
                {
                    temp=v[j][1];
                    v[j][1]=v[j+1][1];
                    v[j+1][1]=temp;
            
                    temp=v[j][0];
                    v[j][0]=v[j+1][0];
                    v[j+1][0]=temp;
            }
        }
    }
    
    for(int i=0;i<N;i++)
    {
        answer.push_back(v[i][0]);
    }
  
    return answer;
}
```

처음에 1차 백터로 풀어서 실패율의 대소구분은 했지만 결과값을 스테이지로 나타내어야 되서 2차원 벡터를 사용하려고했는데 생각한대로 잘 안되어서 고민하다가 내 생각이 맞았는지는 확인해보고 싶어서 배열로 풀었다. 이렇게 푸니 테스트속도가 말도안되게 처참하게 나왔다. 2차원에 백터에 더 공부해봐야겠다.

```
#include <string>
#include <vector>
#include <algorithm>
using namespace std;
bool cmp(const pair<double,int>&a, const pair<double,int>&b){
    if(a.first==b.first) return a.second<b.second;
    return a.first>b.first;

}
vector<int> solution(int N, vector<int> stages) {
    vector<int> answer;
    vector<pair<double,int>> fail;
    for(int i=1;i<=N;i++){
        double a=0,b=0;
        for(int j=0;j<stages.size();j++){
            if(stages[j]==i) a+=1;
            if(stages[j]>=i) b+=1;
        }
        if(b!=0)
            fail.push_back(make_pair(a/b,i));
        else if(b==0)
            fail.push_back(make_pair(0,i));
    }
    sort(fail.begin(),fail.end(),cmp);
    auto it=fail.begin();
    for(it=fail.begin();it!=fail.end();it++)
        answer.push_back(it->second);
    return answer;
}
```
위의 코드는 검색하면 가장 많이나오는 코드인데 pair과 .first .second를 처음보는 함수여서 무엇을 알아봐야할지 방향성은 정해진것같다.