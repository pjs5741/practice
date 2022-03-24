문제 설명

두 수를 입력받아 두 수의 최대공약수와 최소공배수를 반환하는 함수, solution을 완성해 보세요. 배열의 맨 앞에 최대공약수, 그다음 최소공배수를 넣어 반환하면 됩니다. 예를 들어 두 수 3, 12의 최대공약수는 3, 최소공배수는 12이므로 solution(3, 12)는 [3, 12]를 반환해야 합니다.

```
#include <string>
#include <vector>

using namespace std;

vector<int> solution(int n, int m) {
    vector<int> answer;
   vector<int> v1,v2,v3;
    
    for(int i=n;i>0;i--)
    {
        if(n%i==0)
        {
            v1.push_back(i);
        }
    }
    
     for(int j=m;j>0;j--)
    {
        if(m%j==0)
        {
            v2.push_back(j);
        }
    }
    for(int k=0;k<v1.size();k++)
    {
        for(int k1=0;k1<v2.size();k1++)
        {
            if(v1[k]==v2[k1])
            {
                v3.emplace_back(v1[k]);
            }
        }
    }
    
  
      answer.push_back(v3[0]);
      answer.push_back(n*m/v3[0]);
    
    return answer;
}
```
첫for문에 i=0부터가아닌 n에서 --로 한 이유는 작은수부터 배열에 넣으면 첫배열이 무조건1이되어서 v3[0]의 값이 잘못들어가지기 때문이다.

처음에 할때는 for문이 너무 많아서 저번에 푼 소수찾기처럼 효율성문제가 나올줄 알았는데 예상외로 잘 작동되어서 다행이었다. 최대공약수는 문제를 식을 생각하다가 프로그래머스에 질문하기에 누가 남겨준 팁을보니 저러면 구해진다고해서 사용하였다. 문제를 풀고보니 유클리드 호제법이라는 아주쉬운 코드가 있었음을 알았다.

유클리드 호제법은 최대공약수를 쉽게 구하는 방법으로
```
int gcd(int a, int b)
{
	int c;
	while (b != 0)
	{
		c = a % b;
		a = b;
		b = c;
	}
	return a;
}
```

이러면 최대공약수가 구해지고 여기서 위에썻던 (a*b/최대공약수)를하면 최소공배수도 구할수 있다.