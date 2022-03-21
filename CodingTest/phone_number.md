
개인정보 보호를 위해 고지서를 보낼 때 고객들의 전화번호의 일부를 가립니다.
전화번호가 문자열 phone_number로 주어졌을 때, 전화번호의 뒷 4자리를 제외한 나머지 숫자를 전부 *으로 가린 문자열을 리턴하는 함수, solution을 완성해주세요.

```
#include <stdio.h>
#include <stdbool.h>
#include <string.h>
#include <stdlib.h>

// 파라미터로 주어지는 문자열은 const로 주어집니다. 변경하려면 문자열을 복사해서 사용하세요.
char* solution(const char* phone_number) {
    // return 값은 malloc 등 동적 할당을 사용해주세요. 할당 길이는 상황에 맞게 변경해주세요.
    char* answer = (char*)malloc(sizeof(char)* strlen(phone_number));

    strcpy(answer,phone_number);
  
      
         for(int i=0; i<strlen(phone_number)-4; i++)
        {
            answer[i]='*';
        }
    
    return answer;
}
```

이 문제는 malloc에 대해서 잘 몰라서 malloc이 뭔지 검색해가면서 풀었다. 좀더 자세히 공부해봐야겠다.