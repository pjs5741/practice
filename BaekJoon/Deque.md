## 백준 10866번 문제

```
#include <iostream>
#include <vector>
#include <deque>
#include <string>
using namespace std;

int main(void)
{
	deque<int> dq;

	int N;
	string K;

	cin >> N;

	for (int i = 0; i < N; i++)
	{
		cin >> K;

		if (K == "push_front")
		{
			int a = 0;
			cin >> a;

			dq.push_front(a);
		}
		else if (K == "push_back")
		{
			int a = 0;
			cin >> a;

			dq.push_back(a);
		}
		else if (K == "pop_front")
		{
			if (dq.empty())
				cout << "-1" << endl;
			else
			{
				cout << dq.front()<<endl;
				dq.pop_front();
			}
		}
		else if (K == "pop_back")
		{
			if (dq.empty())
				cout << "-1" << endl;
			else
			{
				cout << dq.back() << endl;
				dq.pop_back();
			}
		}
		else if (K == "size")
		{
			cout << dq.size() << endl;
		}
		else if (K == "empty")
		{
			if (dq.empty())
				cout << "1" << endl;
			else
				cout << "0" << endl;
		}
		else if (K == "front")
		{
			if (dq.empty())
				cout << "-1" << endl;
			else
				cout << dq.front() << endl;
		}
		else if (K == "back")
		{
			if (dq.empty())
				cout << "-1" << endl;
			else
			cout << dq.back() << endl;
		}
		
	}
}
```

그냥 덱의 명령어를 알아보는 문제다.