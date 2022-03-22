양의 정수 x가 하샤드 수이려면 x의 자릿수의 합으로 x가 나누어져야 합니다. 예를 들어 18의 자릿수 합은 1+8=9이고, 18은 9로 나누어 떨어지므로 18은 하샤드 수입니다. 자연수 x를 입력받아 x가 하샤드 수인지 아닌지 검사하는 함수, solution을 완성해주세요.

```
#include <stdio.h>
#include <stdbool.h>
#include <stdlib.h>

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

처음에 무슨생각이었는지는 기억안나는데 배열을 생성해서 인덱스0부터4까지 합치는방법을 사용했는데 arr.push_back(c)를 하면 계속오류가나서 보니까 
c의 값은 1 0 0 0 0 arr[i]의 값은 0 0 0 0 0이 들어가서 뭔가했는데 그냥 a값을 1부터해야되는데 10부터시작해서 난 작은 해프닝이었고 애초에 배열할필요도없는문제였다.    .at(i)도 arr[i]도 모두 값이 안들어간다.

안되는코드
```
#include <string>
#include <iostream>
#include <vector>

using namespace std;

bool solution(int x) {
    bool answer = false;
    vector<int> arr(5);
	int a = 1;
    int b = 0;
	int c = 0;
	for (int i = 0; i<5; i++)
	{
		c = x / a % 10;
       
        arr.push_back(c);
        b += arr[i];
		a *= 10;
	
		
	}
    /*
    if(x%b==0)
    {
        answer = true;
    }
    else
    {
        answer = false;
    }
    */
    return answer;
}
```

고친코드
```
#include <string>
#include <iostream>
#include <vector>

using namespace std;

bool solution(int x) {
    bool answer = false;
    vector<int> arr(5);
	int a = 1;
    int b = 0;
	int c = 0;
	for (int i = 0; i<5; i++)
	{
		c = x / a % 10;
       
       arr[i]=c;
        b += arr[i];
        cout<<b;
		a *= 10;
	
		
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
이렇게하면 되긴하는데 push_back이나 at은 왜안되는지 더 공부해봐야될듯하다.