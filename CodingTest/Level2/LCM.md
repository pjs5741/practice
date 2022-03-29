문제 설명

두 수의 최소공배수(Least Common Multiple)란 입력된 두 수의 배수 중 공통이 되는 가장 작은 숫자를 의미합니다. 예를 들어 2와 7의 최소공배수는 14가 됩니다. 정의를 확장해서, n개의 수의 최소공배수는 n 개의 수들의 배수 중 공통이 되는 가장 작은 숫자가 됩니다. n개의 숫자를 담은 배열 arr이 입력되었을 때 이 수들의 최소공배수를 반환하는 함수, solution을 완성해 주세요.

제한 사항

arr은 길이 1이상, 15이하인 배열입니다.
arr의 원소는 100 이하인 자연수입니다.

```
#include <string>
#include <vector>

using namespace std;

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

int solution(vector<int> arr) {
    int answer = 0;
    int a=0;
    int b=0;
    for(int i=0;i<arr.size();i++)
    {
        a= gcd(arr[i],arr[i+1]);
        arr[i+1]= arr[i]*arr[i+1]/a;
        b=arr[i];
    }
    answer=b;
    return answer;
}
```

우선 저번에 배웠던 유클리드 호제법을 사용해서 최대공약수를 구한후에 인덱스 0과 1의 최소공배수를 구한후 1에 넣고 다시 2와비교해서 2에넣고 이런식으로 해서 처음 넣었던 배열의 값이 망가지긴 했는데 이 방법이 크게 잘못된것인지 아닌지는 아직모르겠다.