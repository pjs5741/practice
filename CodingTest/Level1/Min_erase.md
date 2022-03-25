문제 설명

정수를 저장한 배열, arr 에서 가장 작은 수를 제거한 배열을 리턴하는 함수, solution을 완성해주세요. 단, 리턴하려는 배열이 빈 배열인 경우엔 배열에 -1을 채워 리턴하세요. 예를들어 arr이 [4,3,2,1]인 경우는 [4,3,2]를 리턴 하고, [10]면 [-1]을 리턴 합니다.

```
#include <string>
#include <vector>
#include <iostream>

using namespace std;

vector<int> solution(vector<int> arr) {
    vector<int> answer;
    int a=0;
    if(arr.size()!=1)
    {
        for(int i=0;i<arr.size()-1;i++)
        {
            if(arr[a]>arr[i+1])
            {
                a=i+1;
            }
          
        }
        arr.erase(arr.begin() + (a));
        answer = arr;
    }
    else
    {
        arr.erase(arr.begin());
        arr.push_back(-1);
        answer=arr;
        return answer;
    }

    
   
    return answer;
}
```

우선 배열의길이가 1인지아닌지 확인하기위한 if문 그리고 그안에 arr[i]>arr[i]이면 a=i+1을 하여서 그 위치를 저장하고 arr[i]<=arr[i+1]라면 인덱스의 위치를 바꿀필요가없기때문에 else는 따로쓰지앙ㄶ았다.