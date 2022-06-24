## 백준 10828번 문제

```
#include <iostream>
#include <string>
#include <stack>

using namespace std;

stack<int> s;

int main(void)
{
	string str="";
	int N;
	cin >> N;
	for (int i = 0; i < N; i++)
	{
		cin >> str;
		if (str == "push")
		{
			int a;
			cin >> a;
			s.push(a);
		}
		else if (str == "pop")
		{
			if (!s.empty())
			{
				cout << s.top() << endl;
				s.pop();
			}
			else
				cout << "-1" << endl;
		}
		else if (str == "size")
		{
			cout << s.size() << endl;
		}
		else if (str == "empty")
		{
			if (s.empty())
				cout << "1" << endl;
			else
				cout << "0" << endl;
		}
		else if (str == "top")
		{
			if (!s.empty())
				cout << s.top()<<endl;
			else
				cout << "-1"<<endl;

		}
	}


}


```

백준에서 문제를 처음풀어서 첫시도는 함수를 하나하나만들었는데 좀 보니까 cin으로 하는거였어서 그렇게 풀었다.