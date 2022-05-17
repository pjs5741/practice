소수 만들기    
문제 설명   
주어진 숫자 중 3개의 수를 더했을 때 소수가 되는 경우의 개수를 구하려고 합니다. 숫자들이 들어있는 배열 nums가 매개변수로 주어질 때, nums에 있는 숫자들 중 서로 다른 3개를 골라 더했을 때 소수가 되는 경우의 개수를 return 하도록 solution 함수를 완성해주세요.

제한사항    
nums에 들어있는 숫자의 개수는 3개 이상 50개 이하입니다.   
nums의 각 원소는 1 이상 1,000 이하의 자연수이며, 중복된 숫자가 들어있지 않습니다.   

```
#include <vector>
#include <iostream>
#include <cmath>
using namespace std;

bool IsPrime(int a) {
  if(sqrt(a)-(int)sqrt(a)==0)
      return false;
    if(a<=1)  
    {
        return false;
    }
    for(int i=2;i<a;i++)
    {
        if(a%i==0)
            return false;
    }
 return true;
}

int solution(vector<int> nums) {
    int answer = -1;
    int count =0,a=0;
    
    for(int i=0;i<nums.size();i++)
    {
       for(int j=i+1;j<nums.size();j++)
       {
           for(int k=j+1;k<nums.size();k++)
           {
               a=nums[i]+nums[j]+nums[k];
               if(IsPrime(a))
               {
                   count++;
               }
           }
       }
    }
    
    answer=count;

    return answer;
}
```

소수+for문 3중첩이 생각나서 당연히 안될줄알고 다른 방법을 생각해보다가 for문 3중첩말고는 생각날만한게 없어서 그냥 써봤는데 답이었다. 소수확인 함수에서 
```
 if(sqrt(a)-(int)sqrt(a)==0)
      return false;
```
이 부분으로 a가 무언가의 제곱이면 바로 탈출시켜서 시간을 줄여볼려고 했다.