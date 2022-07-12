## 백준3190번 문제

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
	//오른쪽 아래 위 왼
	int dx[4] = { 0,1,-1,0 }, dy[4] = { 1,0,0,-1 };
	int N, K, L;
	int col, row, l, cnt = 0;
	char m;
	int x = 0, y = 0, d = 0;
	int arr[101][101] = { 0, };
	int Idx = 0;
	deque<pair<int,int>> dq;
	vector<pair<int,char>> v;

	dq.push_back(make_pair(x, y));

	arr[x][y] = 2;
	cin >> N >> K;
	for (int i = 0; i < K; i++)
	{
		cin >> col >> row;
		arr[col - 1][row - 1] = 1;
	}

	cin >> L;
	for (int i = 0; i < L; i++)
	{
		cin >> l >> m;
		v.push_back(make_pair(l, m));
	}



	while (1)
	{
		++cnt;
		int nx = x + dx[d];
		int ny = y + dy[d];
		if ((nx < 0 || ny < 0 || nx >= N || ny >= N) || arr[nx][ny] == 2)
		{
			break;
		}
		else if (arr[nx][ny] == 0)
		{
			arr[nx][ny] = 2;
			arr[dq.front().first][dq.front().second] = 0;
			dq.pop_front();
			dq.push_back(make_pair(nx, ny));

		}
		else if (arr[nx][ny] == 1)
		{
			arr[nx][ny] = 2;
			dq.push_back(make_pair(nx, ny));
		}

		if (Idx < v.size())
		{
			if (cnt == v[Idx].first)
			{
				if (v[Idx].second == 'L')
				{
					if (d == 0) d = 2;
					else if (d == 1) d = 0;
					else if (d == 2) d = 3;
					else if (d == 3) d = 1;
				}
				else if (v[Idx].second == 'D')
				{
					if (d == 0) d= 1;
					else if (d == 1) d = 3;
					else if (d == 2) d = 0;
					else if (d == 3) d = 2;
				}
				++Idx;
			}
		}
		x = nx;
		y = ny;
	}
	cout << cnt;


	return 0;
}
```

처음에는 너무너무어려워서 검색해보고도 엄청 오래봤는데 이해도 되고 코드를 짜보니까 어렵긴한데 할만했다.

사과있는곳은 1 뱀있는곳은2 아닌곳은 0으로 두고 가는곳이 1이면 데크를 삭제하지않고 길이를 하나 늘리고 0이면 2로만들면서 데크를 삭제를 해서 길이를 원래대로 줄인다. 오른쪽 왼쪽은 dx dy를 배열로 따로따로만들어서 dy가 늘어나면 오른쪽으로가고 x가 늘면 아래로 y가 마이너스면 왼쪽 x가 마이너스면 위로 가게 만들었다 백준 골드문제 처음해봤는데 이제 더 잘해질수 있을것같다.