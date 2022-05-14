

```
#include <string>
#include <vector>

using namespace std;

vector<int> solution(vector<int> progresses, vector<int> speeds) {
    vector<int> answer;
    int i=0,day1=0,day2=0,count=0,success=1;
    bool build=false;
    
    while(progresses[0]<100)
    {
        progresses[0]+=speeds[0];
        day1++;
    }
    i++;
    while(build!=true)
    {
        progresses[i]+=speeds[i];
        day2++;
        if(progresses[i]>=100 && day1>=day2)
        {
            success++;
            i++;
        }
        else
            answer.push_back(success);
        
        if(i==progresses.size())
            build=true;
    }
    
    return answer;
}
```

실행시간이 10.0초를 초과하여 실패 100을 넘기기위한 계산때문에 그런거라고 예상

식을 바꿔야 한다.


```
#include <string>
#include <vector>

using namespace std;

vector<int> solution(vector<int> progresses, vector<int> speeds) {
    vector<int> answer;
    int day1=0,day2=0,success=1;
    
    day1=(100-progresses[0])/speeds[0];
    
    for(int i=1;i<progresses.size();i++)
    {
        day2=(100-progresses[i])/speeds[i];
        
        if(day1<day2)
        {
            answer.push_back(success);
            day1=day2;
            success=1;
        }
        else if(day1>=day2)
           success++;
       
        
        if(i==progresses.size()-1)
            answer.push_back(success);
    }
    return answer;
}
```

두번째 코드 식을 고민해서 한번에 구하개 바뀌니까 while버리고 for문을 씀 11번이 틀렸다고 나와서 질문하기에서보니까 식이 조금 잘못되었다. 예를들어 진도 30 스피드30이면 2.33이나와서 3일이 아니라 2일이 걸리게된다고 한다.

```
#include <string>
#include <vector>

using namespace std;

vector<int> solution(vector<int> progresses, vector<int> speeds) {
    vector<int> answer;
    int day1=0,day2=0,success=1;
    if((100-progresses[0])%speeds[0]==0)
        day1=(100-progresses[0])/speeds[0];
    else
        day1=((100-progresses[0])/speeds[0])+1;
    
    for(int i=1;i<progresses.size();i++)
    {
        if((100-progresses[i])%speeds[i]==0)
            day2=(100-progresses[i])/speeds[i];
        else
            day2=((100-progresses[i])/speeds[i])+1;
        
        if(day1<day2)
        {
            answer.push_back(success);
            day1=day2;
            success=1;
        }
        else if(day1>=day2)
           success++;
       
        
        if(i==progresses.size()-1)
            answer.push_back(success);
    }
    return answer;
}
```

그냥 if문 박아버렸다.