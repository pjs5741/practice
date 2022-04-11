```
#include <string>
#include <vector>
#include<algorithm>

using namespace std;

vector<string> solution(int n, vector<int> arr1, vector<int> arr2) {
    int v1;
    int v2;
    vector<string> answer;
    string v;
    int a1=0;
    int a2=0;
   for(int i=0;i<n;i++)
    {
        a1=arr1[i];
        a2=arr2[i];
        for(int j=0;j<n;j++)
        {
            v1=a1%2;
            a1/=2;
            v2=a2%2;
            a2/=2;
            if(v1==1||v2==1)
                v+='#';
            else
                v+=' ';
        }
       reverse(v.begin(),v.end());
        answer.push_back(v);
       v="";
    }
   
    return answer;
}
```

2진수로 만들어서 arr1과 arr2중에 하나라도 1이 있으면 #을 아니면 공백을 answer에 넣어주면 된다 처음에는 reverse함수를 안썻는데 그러니까 값이 거꾸로 들어가길래 넣어줬고 answer.push_back(v)후에 v를 다시 공백으로 초기화해서 오류를 없앴다.

```

#include <string>
#include <vector>

using namespace std;

vector<string> solution(int n, vector<int> arr1, vector<int> arr2) {
    vector<string> answer;
    for(int i=0; i <n; i++){
        arr1[i] = arr1[i]|arr2[i];
        string ans = "";
        for(int j = 0; j<n; j++){
            if(arr1[i] % 2 == 0) ans = " " + ans;
            else ans = "#" + ans;
            arr1[i] = arr1[i] >> 1;
        }
        answer.push_back(ans);
    }
    return answer;
}
```

이렇게 비트연산자로 빠르게 하는 방법도 있었다 비트연산자 배우기만 하고 많이 써보질않아서 쓸생각도 못했었는데 다시한번 알아보고 사용해봐야될듯하다.