문제 설명   
수포자는 수학을 포기한 사람의 준말입니다. 수포자 삼인방은 모의고사에 수학 문제를 전부 찍으려 합니다. 수포자는 1번 문제부터 마지막 문제까지 다음과 같이 찍습니다.   

1번 수포자가 찍는 방식: 1, 2, 3, 4, 5, 1, 2, 3, 4, 5, ...   
2번 수포자가 찍는 방식: 2, 1, 2, 3, 2, 4, 2, 5, 2, 1, 2, 3, 2, 4, 2, 5, ...   
3번 수포자가 찍는 방식: 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, ...   

1번 문제부터 마지막 문제까지의 정답이 순서대로 들은 배열 answers가 주어졌을 때, 가장 많은 문제를 맞힌 사람이 누구인지 배열에 담아 return 하도록 solution 함수를 작성해주세요.   

제한 조건   
시험은 최대 10,000 문제로 구성되어있습니다.   
문제의 정답은 1, 2, 3, 4, 5중 하나입니다.   
가장 높은 점수를 받은 사람이 여럿일 경우, return하는 값을 오름차순 정렬해주세요.   

```
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

int test1[5] = {1, 2, 3, 4, 5};
int test2[8] = {2, 1, 2, 3, 2, 4, 2, 5};
int test3[10] = {3, 3, 1, 1, 2, 2, 4, 4, 5, 5};

vector<int> solution(vector<int> answers) {
    vector<int> answer;
    int score[3] = {0, };
    int max_score = 0;
    for (int i = 0; i < answers.size(); i++){
        if (answers[i] == test1[i % 5]) score[0] += 1;
        if (answers[i] == test2[i % 8]) score[1] += 1;
        if (answers[i] == test3[i % 10]) score[2] += 1;
    }
    max_score = max(max(score[0], score[1]), score[2]);
    for (int i = 0; i < 3; i++){
        if (score[i] == max_score)
            answer.push_back(i + 1);
    }
    return answer;
}
```