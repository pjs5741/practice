## 백준 1158번 문제

```
#include <iostream>
#include <vector>
using namespace std;

int main(void)
{
	vector<int> v;
	int N;
	int K;

	cin >> N >> K;

	for (int i = 0; i < N; i++)
	{
		v.push_back(i+1);
	}

	int temp=K-1;
	while (v.size() != 0)
	{
		if (temp >= v.size())
		{
				temp -= v.size();
				continue;
		}
		cout <<v[temp] << '\n';
		v.erase(v.begin() + temp);
		temp += K-1;
	}

}
```
처음 코드였는데 틀려서 보니까 백준에서 정해준 결과값이랑 출력이 다르게 생겨서 그런거였다.

```
#include <iostream>
#include <vector>
using namespace std;

int main(void)
{
	vector<int> v;
	int N;
	int K;

	cin >> N >> K;

	cout << "<";

	for (int i = 0; i < N; i++)
	{
		v.push_back(i+1);
	}

	int temp=K-1;
	while (v.size() != 0)
	{
		if (temp >= v.size())
		{
				temp -= v.size();
				continue;
		}
		cout <<v[temp];
		v.erase(v.begin() + temp);
		if (v.size() != 0)
			cout << ", ";
		temp += K-1;
	}
	cout << ">";
}
```