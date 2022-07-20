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