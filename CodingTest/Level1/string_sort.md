문제 설명   
문자열로 구성된 리스트 strings와, 정수 n이 주어졌을 때, 각 문자열의 인덱스 n번째 글자를 기준으로 오름차순 정렬하려 합니다. 예를 들어 strings가 ["sun", "bed", "car"]이고 n이 1이면 각 단어의 인덱스 1의 문자 "u", "e", "a"로 strings를 정렬합니다.   

제한 조건   
strings는 길이 1 이상, 50이하인 배열입니다.
strings의 원소는 소문자 알파벳으로 이루어져 있습니다.   
strings의 원소는 길이 1 이상, 100이하인 문자열입니다.   
모든 strings의 원소의 길이는 n보다 큽니다.   
인덱스 1의 문자가 같은 문자열이 여럿 일 경우, 사전순으로 앞선 문자열이 앞쪽에 위치합니다.   


```
#include <string>
#include <vector>
#include <algorithm>
 
using namespace std;
 
int N;
 
bool mysort(string a, string b){
    if(a.at(N)!=b.at(N)){
        return a.at(N) < b.at(N);   
    }else{
        return a < b;   
    }
    //return a.at(N)==b.at(N) ? a < b : a.at(N) < b.at(N);
}
 
vector<string> solution(vector<string> strings, int n) {
    vector<string> answer;
    answer = strings;
    N = n;
    sort(answer.begin(),answer.end(),mysort);
    return answer;
}
```

스트링으로 이루어진 배열안에 몇번에 인덱스를 찾는 방법을 잘 모르겠어서 검색해봤는데 이런식의 답이 많이나왔고 풀이는 a[N]과b[N]이 다르면 N인덱스의 문자로 정렬하고 아니면 사전순으로 정렬한다는 mysort 함수를 만들고 아래에는 정의순으로 정렬을사용하여 mysort를 사용하면 된다고 한다.