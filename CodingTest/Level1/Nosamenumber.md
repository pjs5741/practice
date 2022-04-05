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

끝