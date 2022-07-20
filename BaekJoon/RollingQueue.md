## 백준 1021번 문제

```
#include <iostream>
#include <stack>
#include<string>
#include <queue>
#include <vector>
#include <algorithm>
#include <list>
using namespace std;

void First(deque<int> &dq);
int Second(deque<int> &dq ,int* cnt);
int Third(deque<int> &dq, int* cnt);

int main() {

	ios::sync_with_stdio(0);
	cin.tie(0);
	vector<int> v;
	int cnt=0;
	int i = 0, idx = 0;
	deque<int> dq;
	int N, M, a;

	cin >> N >> M;

	for (int i = 1; i <= N; ++i)
		dq.push_back(i);

	for (int i = 0; i < M; ++i)
	{
		cin >> a;
		for (int k = 0; k < dq.size(); ++k)
		{

			if (dq[k] == a)
			{
				idx = k;
				break;
			}
		}


		while (1)
		{

				if (a == dq[0])
				{
					First(dq);
					break;
				}
				else if (idx <= dq.size() / 2)
					Second(dq, &cnt);
				else if (idx > dq.size() / 2)
					Third(dq, &cnt);
		}
		
	}
	cout << cnt;

	return 0;
}



void First(deque<int> &dq)
{
	dq.pop_front();
}
int Second(deque<int> &dq, int* cnt)
{
	dq.push_back(dq.front());
	dq.pop_front();
	*cnt += 1;
	return *cnt;
}
int Third(deque<int> &dq, int* cnt)
{
	dq.push_front(dq.back());
	dq.pop_back();
	*cnt += 1;
	return *cnt;
}
```

포인터를 매개변수로받는 함수를 한번 사용해보았다 처음에는 a를 받아서 벡터에 넣어놓고 하나씩확인하려고했는데 그방법보단 받자마자 확인하는것이 더 깔끔한것 같아서 a를 받자마자 큐에서 인덱스가몇번인지 찾고 그 인덱스를 기준으로 반이상이면 뒤에서 앞으로 이하면 앞에서 뒤로보내는 방법을 사용 큐의 1번과 a가 같으면 추출해서 끝냈다.