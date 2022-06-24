## 백준9012번

```
#include <iostream>
#include <string>
#include <stack>
#include <vector>

using namespace std;

int main(void)
{
	int T;
	cin >> T;
	string s;
	for (int i = 0; i < T; i++)
	{
		cin >> s;
		if (s[0] == ')' || s[s.size() - 1] == '(')
		{
			cout << "NO" << endl;
			continue;
		}
		else
		{
			stack<int> st;
			for (int j = 0; j < s.length(); j++)
			{
					if ('(' == s[j])
					{
						st.push(s[j]);
					}
					else if(s[j]==')' && !st.empty())
					{
						st.pop();
					}
					else if (s[j] == ')'&& st.empty())
					{
						st.push(')');
						break;
					}
			}
			if (st.empty())
				cout << "YES" << endl;
			else
				cout << "NO" << endl;
		}
	}
}

```

옛날에 프로그래머스에서 풀었던기억이있는문제 