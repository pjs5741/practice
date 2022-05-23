문제 설명   
0 또는 양의 정수가 주어졌을 때, 정수를 이어 붙여 만들 수 있는 가장 큰 수를 알아내 주세요.

예를 들어, 주어진 정수가 [6, 10, 2]라면 [6102, 6210, 1062, 1026, 2610, 2106]를 만들 수 있고, 이중 가장 큰 수는 6210입니다.

0 또는 양의 정수가 담긴 배열 numbers가 매개변수로 주어질 때, 순서를 재배치하여 만들 수 있는 가장 큰 수를 문자열로 바꾸어 return 하도록 solution 함수를 작성해주세요.   

제한 사항    
numbers의 길이는 1 이상 100,000 이하입니다.   
numbers의 원소는 0 이상 1,000 이하입니다.   
정답이 너무 클 수 있으니 문자열로 바꾸어 return 합니다.    

```
#include <string>
#include <vector>
#include <algorithm>
#include <iostream>

using namespace std;

bool comp(string a,string b){
    return a+b>b+a;
}

string solution(vector<int> numbers) {
    string answer = "";
    vector<string> v;
    
    for(auto a:numbers)
        v.push_back(to_string(a));
    

    sort(v.begin(),v.end(),comp);
    
    for(int i=0;i<v.size();i++)
        answer+=v[i];
    
   
    return answer;
}
```

이러면 안되지만 왼쪽위에 정렬이라고 써있길래 정렬을 어떻게 써야될까 생각을했는데 두개 붙여보고 더큰순으로 정렬하게 만들었다.

한문제가 오류가났는데 문제를 보니 계속 0또는 양의 정수라는거 보니까 0때문에 걸린거같긴한데 맨앞에 0이 있으면 오류나는건가? 하고 테스트케이스를 추가하니 잘 작동되었고 0이 두개 있으면 어떨까?

너무잘된다. 흐음 질문하기를 보니까 [0,0,0,0]같이 0만있으면 "0000"이 아니라 "0"이 나와야 한다고한다.

```
#include <string>
#include <vector>
#include <algorithm>
#include <iostream>

using namespace std;

bool comp(string a,string b){
    return a+b>b+a;
}

string solution(vector<int> numbers) {
    string answer = "";
    vector<string> v;
    
    for(auto a:numbers)
        v.push_back(to_string(a));
    

    sort(v.begin(),v.end(),comp);
    
   if(v[0]=="0")
       return "0";
   
    for(int i=0;i<v.size();i++)
        answer+=v[i];

   
    return answer;
}

```

if문 한개 추가 끝