문제 설명   
1와 0로 채워진 표(board)가 있습니다. 표 1칸은 1 x 1 의 정사각형으로 이루어져 있습니다. 표에서 1로 이루어진 가장 큰 정사각형을 찾아 넓이를 return 하는 solution 함수를 완성해 주세요. (단, 정사각형이란 축에 평행한 정사각형을 말합니다.)   

예를 들어   

1	2	3	4   
0	1	1	1   
1	1	1	1   
1	1	1	1    
0	0	1	0    
가 있다면 가장 큰 정사각형은    

1	2	3	4   
0	1	1	1    
1	1	1	1   
1	1	1	1    
0	0	1	0    
가 되며 넓이는 9가 되므로 9를 반환해 주면 됩니다.
    
제한사항    
표(board)는 2차원 배열로 주어집니다.   
표(board)의 행(row)의 크기 : 1,000 이하의 자연수    
표(board)의 열(column)의 크기 : 1,000 이하의 자연수   
표(board)의 값은 1또는 0으로만 이루어져 있습니다.    

```
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

int solution(vector<vector<int>> board)
{
    int answer = board[0][0];
    
    for(int i = 1; i < board.size(); i++){
        for(int j = 1; j < board[0].size(); j++){
            if(board[i][j]){ 
                board[i][j] = min(board[i][j - 1], board[i - 1][j]);
                board[i][j] = min(board[i - 1][j - 1], board[i][j]) + 1;
                answer = max(answer, board[i][j]);
            }
        }
    }
    return answer * answer;
}
```

검색해서 풀었다. 처음에 생각해본게 조금만 더 깊게 생각해보면 문제투성이여서 생각하고생각하다가 풀수있는 기미가 안보여서 얼마나 복잡한 문제일까 하면서 검색해봤는데 코드가 정말 깔끔했다. 레벨2올라오면서 다시 1레벨처음할때같은 느낌이든다 더 다양한각도로 생각하면서 익숙해져가야겟다.