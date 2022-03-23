행렬의 합을 구하는 함수 solution을 만들어라

```
#include <string>
#include <vector>

using namespace std;


vector<vector<int>> solution(vector<vector<int>> arr1, vector<vector<int>> arr2) {
    vector<vector<int>> answer;
 vector<int> arr;
    
    for(int i=0;i<arr1.size();i++)
    {
            arr.clear();
      for(int j=0;j<arr1[0].size();j++)
      {
             arr.push_back(arr1[i][j]+arr2[i][j]);
          
      }
        answer.push_back(arr);
       
    }
    
    
    return answer;
}
```

