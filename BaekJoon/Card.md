## 백준 2164번 문제

```
#include <iostream>
#include <vector>
#include <queue>
using namespace std;

int main(void)
{
	queue<int> q;
	int N;

	cin >> N;

	for (int i = 0; i < N; i++)
	{
		q.push(i + 1);
	}

	int temp;
	while (q.size() != 1)
	{
		q.pop();
		q.push(q.front());
		q.pop();
	}

	cout << q.front() << endl;
}
```
큐를 사용해서 하나 빼고 하나 뒤로 옮기고 반복하다가 마지막에 남는것을 출력하는 문제이다. 뒤로 옮기는 것은 큐의 front를 push후에 pop을 해주면 된다.