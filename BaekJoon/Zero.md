## 백준10773번

```
#include <iostream>
#include <string>
#include <stack>
#include <vector>

using namespace std;

int main(void)
{
	vector<int> v;
	int K,a, result = 0;
	cin >> K;
	for (int i = 0; i < K; i++)
	{
		cin >> a;
		if (a == 0)
			v.pop_back();
		else
			v.push_back(a);
	}

	for (int i = 0; i < v.size(); i++)
	{
		result += v[i];
	}
	cout << result << endl;
	
}
```

0이 나오면 지우고 아니면 저장해서 총수를 더한다. 스택문제인거같은데 스택은 v[i]로 접근이 안되길래 그냥 벡터로했다.