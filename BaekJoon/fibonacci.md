## 백준 1003번 문제

```
#include <iostream>
#include <stack>
#include<string>
#include <queue>
#include <vector>
#include <algorithm>
using namespace std;

int main() {
	

	int T, N;
	vector<pair<int,int>>fibonacci(41);
	cin >> T;
	fibonacci[0]=(make_pair(1, 0));
	fibonacci[1]=(make_pair(0, 1));
	fibonacci[2]=(make_pair(1, 1));
	fibonacci[3]=(make_pair(1, 2));
	fibonacci[4]=(make_pair(2, 3));

	for (int i = 5; i < 41; ++i)
	{

		fibonacci[i].first = fibonacci[i - 1].first + fibonacci[i - 2].first;
		fibonacci[i].second = fibonacci[i - 1].second + fibonacci[i - 2].second;
	}
	
	for (int i = 0; i < T;++i)
	{
		cin >> N;

		cout << fibonacci[N].first << " " << fibonacci[N].second << '\n';
	}
	return 0;
}
```

벡터에 first에는 0의수를 second는 1의 수를 저장해서 규칙을 찾고 만들었다.