## 백준 10816번 문제

```
#include <iostream>
#include <vector>
using namespace std;

int main(void)
{
	int N;
	vector<int> v;
	cin >> N;

	for (int i = 0; i < N; i++)
	{
		int I;
		cin >> I;
		v.push_back(I);
	}

	int M;

	cin >> M;

	for (int i = 0; i < M; i++)
	{
		int I,cnt=0;
		cin >> I;
		for (int j = 0; j < v.size(); j++)
		{
			if (v[j] == I)
				cnt++;
		}
		cout << cnt << " ";
		
	}
	return 0;
}
```
처음 코드 안되는건 아닌데 시간 초과에 걸린다.
```
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int main(void)
{
    ios::sync_with_stdio(false);
	cin.tie(NULL);
    
	int N;
	vector<int> v;
	cin >> N;

	for (int i = 0; i < N; i++)
	{
		int I;
		cin >> I;
		v.push_back(I);
	}

	int M;

	cin >> M;

	sort(v.begin(), v.end());
	int num = 0;

	for (int i = 0; i < M; ++i) {
		cin >> num;
		cout << upper_bound(v.begin(), v.end(), num)
			- lower_bound(v.begin(), v.end(), num) << " ";
	}
}
```

찾아보니까 upper_bound로 정렬된 수중에 최대치의 인덱스와 lower_bound로 최하의 인덱스를 뺴서 구하는 문제였다. bound를 알게되었다.