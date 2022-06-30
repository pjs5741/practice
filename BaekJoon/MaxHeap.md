## 백준 11279번 문제

```
#include <iostream>
#include <queue>
#include <algorithm>
#include <functional>
using namespace std;

int main(void)
{
	ios::sync_with_stdio(false);
	cin.tie(NULL);
	
	priority_queue<int> pq;

	int N,x;

	cin >> N;

	for (int i = 0; i < N; i++)
	{
		cin >> x;
		pq.push(x);

		if (x == 0)
		{
			if (!pq.empty())
			{
				cout << pq.top() << '\n';
				pq.pop();
			}
			else
				cout << "0" << '\n';
		}
	}
	

}
```

문제를 보니까 저번에 사용했던 priority_queue가 생각나서 써보니 바로되었다.