## 백준 2193번 문제

```
#include <iostream>
#include <stack>
#include<string>
#include <queue>
#include <vector>
#include <algorithm>
#include <list>
using namespace std;

int main() {

	ios::sync_with_stdio(0);
	cin.tie(0);
	
	long long arr[91];
	int N;


	arr[1] = 1;
	arr[2] = 1;
	arr[3] = 2;
	arr[4] = 3;
	arr[5] = 5;
	arr[6] = 8;
	cin >> N;

	for (int i = 7; i <= N; i++)
	{
		arr[i] = arr[i - 1] + arr[i - 2];
	}

	cout << arr[N];

	return 0;
}
```

DP 몇문제 풀어보니 아주 쉬운 문제