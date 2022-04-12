문제 설명

정수 배열 numbers가 주어집니다. numbers에서 서로 다른 인덱스에 있는 두 개의 수를 뽑아 더해서 만들 수 있는 모든 수를 배열에 오름차순으로 담아 return 하도록 solution 함수를 완성해주세요.   

제한사항   
numbers의 길이는 2 이상 100 이하입니다.   
numbers의 모든 수는 0 이상 100 이하입니다.   


```
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

vector<int> solution(vector<int> numbers) {
    vector<int> answer;
    int a=0;
    for(int i=0;i<numbers.size()-1;i++)
    {
       for(int j=i+1;j<numbers.size();j++)
       {
          answer.push_back(numbers[i]+numbers[j]);
       }
    }
    sort(answer.begin(), answer.end()); 
    answer.erase(unique(answer.begin(), answer.end()), answer.end());
    return answer;
}
```

합을 배열에 넣은후에 정렬하고 중복이 없이 정렬후에 뒤에는 지웠다.