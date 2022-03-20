숫자 2개를 넣으면 그 숫자를 행과 열로하여서 *을 찍어 직사각형이 나오게 하는 코드
```
#include <iostream>

using namespace std;

int main(void) {
	int a;
	int b;
	cin >> a >> b;
	for (int i = 0; i<b; i++)
	{
		for (int j = 0; j<a; j++)
		{
			cout << "*";
		}
		cout << endl;
	}

	return 0;
}
```