문제 설명

게임 캐릭터를 4가지 명령어를 통해 움직이려 합니다. 명령어는 다음과 같습니다.

U: 위쪽으로 한 칸 가기

D: 아래쪽으로 한 칸 가기

R: 오른쪽으로 한 칸 가기

L: 왼쪽으로 한 칸 가기

캐릭터는 좌표평면의 (0, 0) 위치에서 시작합니다. 좌표평면의 경계는 왼쪽 위(-5, 5), 왼쪽 아래(-5, -5), 오른쪽 위(5, 5), 오른쪽 아래(5, -5)로 이루어져 있습니다.

우리는 게임 캐릭터가 지나간 길 중 캐릭터가 처음 걸어본 길의 길이를 구하려고 합니다. 예를 들어 위의 예시에서 게임 캐릭터가 움직인 길이는 9이지만, 캐릭터가 처음 걸어본 길의 길이는 7이 됩니다. (8, 9번 명령어에서 움직인 길은 2, 3번 명령어에서 이미 거쳐 간 길입니다)

단, 좌표평면의 경계를 넘어가는 명령어는 무시합니다.

```
#include <string>
using namespace std;

int solution(string dirs) {
    int answer = 0;
    int count=0,x=0,y=0;
    
    for(int i=0;i<dirs.size();i++)
    {
        
        if(dirs[i]=='U')
        {
            if(x!=5)
            {
                x++;
                answer++;
            }
        }
        else if(dirs[i]=='D')
        {
            if(x!=-5)
            {
                x--;
                answer++;
            }
            
        }
        else if(dirs[i]=='R')
        {
            if(y!=5)
            {
                y++;
                answer++;
            }
        }
        else if(dirs[i]=='L')
        {
            if(y!=-5)
            {
                y--;
                answer++;
            }
        }
    }
    return answer;
}
```

틀만 대충만들어놨다 여기서이제 지났던길을 지나면 answer++를 안하게만들어야된다.

```
#include <string>
#include <vector>
#include <map>
using namespace std;

int solution(string dirs) {
    int answer = 0;
    int x=0,y=0;
    map<pair<pair<int,int>,pair<int,int>>,bool> visit;
    
    for(int i=0;i<dirs.size();i++)
    {
        int firstx=x;
        int firsty=y;
        if(dirs[i]=='U')
        {
            if(x!=5)
            {
                x++;
            }
            else
                 continue;
        }
        else if(dirs[i]=='D')
        {
            if(x!=-5)
            {
                x--;
            }
            else
                 continue;
            
        }
        else if(dirs[i]=='R')
        {
            if(y!=5)
            {
                y++;
            }
            else
                 continue;
        }
        else if(dirs[i]=='L')
        {
            if(y!=-5)
            {
                y--;
            }
            else
                 continue;
        }
       if(visit[make_pair(make_pair(firstx,firsty),make_pair(x,y))] == true)
           continue;
        
        visit[make_pair(make_pair(firstx,firsty), make_pair(x,y))] = true;
        visit[make_pair(make_pair(x,y), make_pair(firstx,firsty))] = true;
        answer++;
    }
    return answer;
}
```

좌표길래 x,y를 생각해서 map을 사용했다 그런데 저번에 map과 pair의 존재를 알기는 했는데 사용해본적이없어서그런가 계속 오류가 나길래 검색해서 했다. 일단 레벨2인데 하는 방법이 생각한게 맞아서 다행이다 더 해서 풀기까지 되도록 만들어야겠다.

