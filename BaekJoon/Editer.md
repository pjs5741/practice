## 백준 1406번 문제

```
#include <iostream>
#include <stack>
#include<string>
#include <queue>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
	

	vector<char> v;
	string s;
	int M,cursor;
	char c;

	cin >> s >> M;


	for (int i : s)
	{
		v.push_back(i);
	}

	cursor = v.size();

	for (int i = 0; i < M; ++i)
	{
		cin >> c;

		if (c == 'L')
		{
			if(cursor!=0)
			cursor -= 1;
		}
		else if (c == 'D')
		{
			if (cursor != v.size() )
				cursor += 1;
		}
		else if (c == 'B')
		{
			if (cursor != 0)
			{
				--cursor;
				v.erase(v.begin() + cursor);
			}
		}
		else if (c == 'P')
		{
			char a;
			cin >> a;
			
			
				v.insert(v.begin() + cursor, a);
				++cursor;
			
		}
	}

	for (int i = 0; i < v.size(); i++)
	{
		cout << v[i];
	}

	return 0;
}
```

처음에 벡터로해보고 그 후에 스트링으로 해봤는데 둘다 시간초과가 되어서 보니까 list로 푸는 방법과 새로운 스택2개를 사용해서 푸는문제가있었다

```
#include <iostream>
#include <stack>
#include <string>
 
using namespace std;
 
int main() {
    string s = "";
    cin >> s;
    stack<char> l;
    stack<char> r;
    for (int i = 0; i < s.size(); i++) {
        l.push(s[i]);
    }
    int num;
    cin >> num;
    while (num--) {
        char tmp;
        cin >> tmp;
        if (tmp == 'P') {
            char c;
            cin >> c;
            l.push(c);
        }
        else if (tmp == 'L') {
            if (l.empty()) continue;
            else {
                r.push(l.top());
                l.pop();
            }
        }
        else if (tmp == 'B') {
            if (l.empty()) continue;
            else l.pop();
        }
        else if (tmp == 'D') {
            if (r.empty()) continue;
            else {
                l.push(r.top());
                r.pop();
            }
        }
    }
    while (!l.empty()) {
        r.push(l.top());
        l.pop();
    }
    while (!r.empty()) {
        cout << r.top();
        r.pop();
    }
    return 0;
}
```

스택을 두개를 두고 스택과 스택 사이가 커서인 걸로 표현한것같다. 이러한 방법도 있다는것을 알았다.