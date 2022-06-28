## 백준10845번

```
#include <iostream>
#include <string>
#include <stack>
#include <vector>
#include <queue>

using namespace std;

int main(void)
{
	queue<int> q;
	int N;
	string s;
	cin >> N;

	for (int i = 0; i < N; i++)
	{
		cin >> s;
		if (s == "push")
		{
			int a;
			cin >> a;
			q.push(a);
		}
		else if (s == "pop")
		{
			if (q.empty())
			{
				cout << -1 << endl;
			}
			else
			{
				cout << q.front() << endl;
				q.pop();
			}
		}
		else if (s == "size")
		{
			cout << q.size() << endl;
		}
		else if (s == "empty")
		{
			if (q.empty())
				cout << 1 << endl;
			else
				cout << 0 << endl;
		}
		else if (s == "front")
		{
			if(!q.empty())
			cout << q.front() << endl;
			else
				cout << -1 << endl;
		}
		else if (s == "back")
		{
			if (!q.empty())
				cout << q.back() << endl;
			else
				cout << -1 << endl;
		}
	}
}

```

스택과 같은 유형의 문제였다