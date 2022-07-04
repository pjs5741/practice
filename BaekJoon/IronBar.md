## 백준 10799번 문제

```
#include <iostream>
#include <stack>
#include<string>
#include <queue>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
	

	stack<char> s;
	string st = "";
	int line = 0, cut = 0, total = 0;
	bool check = true;
	cin >> st;

	for (int i = 0; i < st.length(); i++)
	{
		if (st[i] == '(' && st[i + 1] != ')')
		{
			++line;
			check = true;
		}
		else if (st[i] == '(' && st[i + 1] == ')')
		{
			check = true;
		}
		else if (st[i] == ')' && check == true)
		{
			total += line;
			check = false;
		}
		else if (st[i] == ')' && check == false)
		{
			--line;
			++total;
		}
	}

	cout << total;
	
	return 0;
}
```

(뒤에 )가 안오면 라인 1늘리고 오면 check를 트루로 해둔다
)가 나오고 check가 트루면 line의 수만큼total을 늘리고 check는 false로 바꾼다.

)가 올때 check가 false면 라인을 하나 줄이고 토탈에 1을늘린다.