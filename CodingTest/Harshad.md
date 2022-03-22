```
#include <string>
#include <vector>

using namespace std;

bool solution(int x) {
    bool answer = false;
    int a=1;
    int b=0;
    int c=0;
    for(int i=0;i<5;i++)
    {
        c=x/a%10;
        b+=c;
        a*=10;   
       
        
    }
    
    if(x%b==0)
    {
        answer = true;
    }
    else
    {
        answer = false;
    }
    
    return answer;
}
```

처음에 백터가인클루드되어있어서 배열을 생성해서 인덱스0부터4까지 합치는방법을 사용했는데 계속오류가나서 보니까 배열할필요도없는문제였다.