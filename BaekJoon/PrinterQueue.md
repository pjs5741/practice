## 백준1966번 문제

```
#include <iostream>
#include <queue>
using namespace std;

int main(void)
{
	int TestCase;
	cin >> TestCase;

	for(int i=0;i<TestCase;i++)
	{
		int N, M;
		cin >> N >> M;
		queue<pair<int, int>> q;
		priority_queue<int>pq;
		int cnt = 0;
		for (int i = 0; i < N; i++)
		{
			int Importance;
			cin >> Importance;
			q.push(make_pair(i, Importance));
			pq.push(Importance);
		}

		while (!q.empty())
		{
			int index = q.front().first;
			int importance = q.front().second;
			if (pq.top() > importance)
			{
				q.push(q.front());
				q.pop();
			}
			else
			{
				cnt++;
				pq.pop();
				q.pop();
				if (M == index)
				{
					cout << cnt << endl;
					break;
				}
			}

		}
	}
	return 0;
}
```

priority_queue라는 것을 검색해서 알았다. 큐에 키값을 내림차순으로 정렬해주는 것이다.

 그로인해 일반 queue를 pair로 만들어서 키값과 우선순위를 넣고 priority_queue에는 우선순위를 넣어서 queue의 우선순위와 비교하여 priority_queue의 값이 queue의 우선순위보다 크면 뒤로 보내고 아니면 둘다 지우면서 카운트를 하나 올리고 q가 비면 while문을 탈출해 카운트를 출력한다.