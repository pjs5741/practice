## 백준1874번

```
#include <iostream>
#include <string>
#include <stack>
#include <vector>
#include <queue>
#include <algorithm>


using namespace std;


int main(void)
{
	string st = "";
	stack<int> s;
	int n, cnt = 1;
	cin >> n;

	for (int i = 0; i < n; i++)
	{
		int a;
		cin >> a;
			while(cnt<=a)
			{
				s.push(cnt);
				cnt++;
				st += '+';
			}
			if (s.top() == a)
			{
				s.pop();
				st += '-';

			}
			else
			{
				cout << "NO";
				return 0;
			}
	}
	for (int i = 0; i < st.length(); i++)
	{
		cout << st[i] << '\n';
	}
}

```

처음에 문제를 이해를 못해서 해맸지만 그냥 처음수까지 쭉 스택을쌓다가 도달하면 뺴고 그 이후 가능하면 계속 아니면 No를 하는 것이었다.

처음에는 벡터를 사용했는데 계속오류가나서 string으로 바꿔서 저장했다.