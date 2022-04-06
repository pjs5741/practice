문제 설명

배열 arr가 주어집니다. 배열 arr의 각 원소는 숫자 0부터 9까지로 이루어져 있습니다. 이때, 배열 arr에서 연속적으로 나타나는 숫자는 하나만 남기고 전부 제거하려고 합니다. 단, 제거된 후 남은 수들을 반환할 때는 배열 arr의 원소들의 순서를 유지해야 합니다. 예를 들면,

arr = [1, 1, 3, 3, 0, 1, 1] 이면 [1, 3, 0, 1] 을 return 합니다.
arr = [4, 4, 4, 3, 3] 이면 [4, 3] 을 return 합니다.
배열 arr에서 연속적으로 나타나는 숫자는 제거하고 남은 수들을 return 하는 solution 함수를 완성해 주세요.

제한사항

배열 arr의 크기 : 1,000,000 이하의 자연수
배열 arr의 원소의 크기 : 0보다 크거나 같고 9보다 작거나 같은 정수
```
#include <vector>
#include <iostream>

using namespace std;

vector<int> solution(vector<int> arr) 
{
    vector<int> answer;
    for(int i=0;i<arr.size();i++)
    {
        
        if(arr[i]==arr[i+1])
        {
            arr.erase(arr.begin()+i);
            i--;
        }
    }
    answer=arr;
   

    return answer;
}
```

처음코드인데 한번에 될줄알았더니 마지막 숫자 예를들면 1,3,0,1에서 마지막1 4,3에서 마지막 3의 값이 들어가지 않았다.
```
#include <vector>
#include <iostream>

using namespace std;

vector<int> solution(vector<int> arr) 
{
    vector<int> answer;
    for(int i=0;i<arr.size();i++)
    {
        
        if(arr[i]==arr[i+1])
        {
            arr.erase(arr.begin()+i);
            i--;
        }
        else
            answer.push_back(arr[i+1]);
    }
    
    
   

    return answer;
}
```
다음에는 이런식으로 바꿔보았는데 이러니 arr[0]의 숫자가 빠졌다. 이러면 다 해결된것같다. 맨처음에 arr[0]을 푸쉬백하면 
```
#include <vector>
#include <iostream>

using namespace std;

vector<int> solution(vector<int> arr) 
{
    vector<int> answer;
    
    answer.push_back(arr[0]);
    for(int i=0;i<arr.size();i++)
    {
        
        if(arr[i]==arr[i+1])
        {
            arr.erase(arr.begin()+i);
            i--;
        }
        else
            answer.push_back(arr[i+1]);
    }
    
    
   

    return answer;
}
```

된줄알았는데 채점후 제출을하니 16번 하나가 안된다.

그래서 생각을 계속했는데 arr를 굳이 지울필요가있나? 였다. return은 어짜피 answer인것을
그리하여 나온 코드는

```
#include <vector>
#include <iostream>

using namespace std;

vector<int> solution(vector<int> arr) 
{
    vector<int> answer;
    

    for(int i=0;i<arr.size();i++)
    {
        
        if(arr[i]!=arr[i+1])
            answer.push_back(arr[i]);
    }
    
    
   

    return answer;
}
```

인데 이 코드는 또 17번이 틀린다. 그나마 나은점은 이전 코드는 효율성검사도 실패였는데 이코드는 효율성검사는 오케이다.
질문하기 들어가보니 문제[1,1] 답[1] 이라는 테스트케이스를 보고 내가 만든코드는 쓰레기값때문에 마지막i와i+1이 달라져서 어떻게 얻어걸린거란걸 알았고
```
#include <vector>
#include <iostream>

using namespace std;

vector<int> solution(vector<int> arr) 
{
    vector<int> answer;
    
    answer.push_back(arr[0]);
    for(int i=1;i<arr.size();i++)
    {
        
        if(arr[i-1]!=arr[i])
            answer.push_back(arr[i]);
    }
    
    
   

    return answer;
}
```
위 테스트케이스를 통과하기 위해 arr[0]을 먼저 넣고 그 후 비교를 해서 다르면 뒤에 값이 들어가도록했다. 앞에값이 들어가면 arr[0]을 넣은것과 중복이 되므로