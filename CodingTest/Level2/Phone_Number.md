문제 설명   
전화번호부에 적힌 전화번호 중, 한 번호가 다른 번호의 접두어인 경우가 있는지 확인하려 합니다.   
전화번호가 다음과 같을 경우, 구조대 전화번호는 영석이의 전화번호의 접두사입니다.   

구조대 : 119   
박준영 : 97 674 223   
지영석 : 11 9552 4421   
전화번호부에 적힌 전화번호를 담은 배열 phone_book 이 solution 함수의 매개변수로 주어질 때, 어떤 번호가 다른 번호의 접두어인 경우가 있으면 false를 그렇지 않으면 true를 return 하도록 solution 함수를 작성해주세요.   

제한 사항   
phone_book의 길이는 1 이상 1,000,000 이하입니다.   
각 전화번호의 길이는 1 이상 20 이하입니다.   
같은 전화번호가 중복해서 들어있지 않습니다.   

```
#include <string>
#include <vector>

using namespace std;

bool solution(vector<string> phone_book) {
    bool answer = true;
    string temp="";
    for(int i=0;i<phone_book.size();i++)
    {
        for(int j=0;j<phone_book[0].size();j++)
        {
            if(i == 0)
                temp+=phone_book[i][j];
            else
            {
                if(phone_book[i][j]==temp[j])
                {
                    answer = false;
                }
                else
                {
                    answer = true;
                }
            }
        }
        if(!answer)
            break;
    }
    return answer;
}
```

처음코드 정확성 테스트도 몇개맞고 몇개틀리고 효율성테스트도 몇개맞고 몇개틀렸다. 아마 1행의 문자만 다른 문자의 접두어인지 확인해봐서 그런것같다. 나머지 행의 문자들도 다른행의 접두어인지 확인해봐야 풀릴듯 하다. 그 외에도 좀만더 생각해보니 그냥 이상한 코드였다. 열의 사이즈가 행마다 달라서 for문을 중첩해서 두번쓰면 안된다.

```
#include <string>
#include <vector>

using namespace std;
bool solution(vector<string> phone_book) {
    bool answer = true;
    string temp=phone_book[0];
    
    for(int i=0;i<phone_book.size();i++)
    {
        if(temp.size()>phone_book[i+1].size())
            temp=phone_book[i+1];       
    }
    
    for(int i=0;i<phone_book.size();i++)
    {
        if(phone_book[i].substr(0,temp.size())==temp && phone_book[i].size()>temp.size())
            return false;
    }
    
  
    return answer;
}
```
두번째 코드인데 첫코드보단 많이맞았는데 실패다. 예제 2번처럼 같은사이즈의 행이 많았을때 오류가 나는부분인거 같다.



```
#include <string>
#include <vector>

using namespace std;
bool solution(vector<string> phone_book) {
    bool answer = true;
    
    for(int i=0;i<phone_book.size();i++)
    {
      for(int j=0;j<phone_book.size();j++)
      {
          if(phone_book[i].size()!=phone_book[j].size() && phone_book[i]==phone_book[j].substr(0,phone_book[i].size()))
             return false;
      }     
    }
    
   
  
    return answer;
}
```

세번째 코드, 다 갈아엎었다. 정확도 테스트 오케이 이었는데 효율성테스트에서 짤렸다. 더이상 생각나는 것이 없어서 검색을 해봤는데

```
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

bool solution(vector<string> phone_book) {
    sort(phone_book.begin(), phone_book.end());
    
    for (int i = 0 ; i < phone_book.size() - 1 ; i++ )
    {
        if (phone_book[i] == phone_book[i+1].substr(0, phone_book[i].size()))
            return false;
    }
    return true;
}
```

이렇게 정렬해서 푸는 방법이 추천이 제일 많았다. 아직 감이 제대로 안잡혔나보다 더 열심히해야겟다