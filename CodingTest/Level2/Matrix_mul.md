문제 설명

2차원 행렬 arr1과 arr2를 입력받아, arr1에 arr2를 곱한 결과를 반환하는 함수, solution을 완성해주세요.

제한 조건

행렬 arr1, arr2의 행과 열의 길이는 2 이상 100 이하입니다.
행렬 arr1, arr2의 원소는 -10 이상 20 이하인 자연수입니다.
곱할 수 있는 배열만 주어집니다.

```
#include <string>
#include <vector>
using namespace std;

vector<vector<int>> solution(vector<vector<int>> arr1, vector<vector<int>> arr2) {
	vector<vector<int>> answer;
	int arr2_Row_Size = arr2[0].size();
	for (int i = 0; i < arr1.size(); i++) {
		vector <int> x;
		for (int k = 0; k < arr2_Row_Size; k++) {
			int sum = 0;
			for (int j = 0; j < arr1[i].size(); j++) {
				sum += arr1[i][j] * arr2[j][k];
			}
			x.push_back(sum);
		}
		answer.push_back(x);
	}
	return answer;
} 
```

   머리로는 알고있는데 코드를 어떻게해야되는지 안나와서 결국 검색해서 풀게되었다.
레벨2부터는 조금 복잡한계산이 생기는것같다. 정신바짝차려야겠다.
    