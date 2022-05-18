문제 설명   
가로 길이가 Wcm, 세로 길이가 Hcm인 직사각형 종이가 있습니다. 종이에는 가로, 세로 방향과 평행하게 격자 형태로 선이 그어져 있으며, 모든 격자칸은 1cm x 1cm 크기입니다. 이 종이를 격자 선을 따라 1cm × 1cm의 정사각형으로 잘라 사용할 예정이었는데, 누군가가 이 종이를 대각선 꼭지점 2개를 잇는 방향으로 잘라 놓았습니다. 그러므로 현재 직사각형 종이는 크기가 같은 직각삼각형 2개로 나누어진 상태입니다. 새로운 종이를 구할 수 없는 상태이기 때문에, 이 종이에서 원래 종이의 가로, 세로 방향과 평행하게 1cm × 1cm로 잘라 사용할 수 있는 만큼만 사용하기로 하였습니다.   
가로의 길이 W와 세로의 길이 H가 주어질 때, 사용할 수 있는 정사각형의 개수를 구하는 solution 함수를 완성해 주세요.   

제한사항   
W, H : 1억 이하의 자연수

```
using namespace std;

long long solution(int w,int h) {
    long long answer = 1;
    int total = w*h;
    int count=0;
    int j=0;
       for(int i=0;i<w;i++)
       {
           total-=1;
           j++;
           if(j<h)
           {
                total-=1;
                count++;
                if(count==2)
                    j++;
           }
           else
               break;
       }
   
    
    answer=total;
    return answer;
}
```
처음에 예제만 보고 만든코드인데 그래서 예제만 맞고 다틀렸다. 꼭짓점 두개를 이으면 당연히 예제랑 다른모양의 사각형은 규칙이 달라진다.

비율을 구해서 그에 따라 몇칸이 없어지는지 구할 수 있다.

```
using namespace std;

int gcd(int a, int b){
	while(b!=0){
		int r = a%b;
		a= b;
		b= r;
	}
	return a;
}

long long solution(int w,int h) {
    long long answer = 1;
    int total = w*h;
    int a=gcd(w,h),tempw,temph;
    
    tempw=w/a;
    temph=h/a;
    
    if(tempw%temph==1)
    {
        total=total-(temph+1)*a;
    }
    else if(temph%tempw == 1)
    {
        total=total-(tempw+1)*a;
    }
    else if(tempw%temph==0)
    {
        total-=w*a;
    }
        
    
    answer=total;
    return answer;
}
```

비율을 구하기위해서 최대공약수로 나눴는데 2:x로만 생각해서 엎었다. 규칙은 찾았는데 이걸 어떻게 표현해야되나 생각하다가 찾은게 비율을 더하고-1을 하면 빠지는 사각형의 개수가 나오는 것을 찾았다.

```
using namespace std;

int gcd(int a, int b){
	while(b!=0){
		int r = a%b;
		a= b;
		b= r;
	}
	return a;
}

long long solution(int w,int h) {
    long long answer = 1;
    
    
   
    
   
   answer=(long long)w*(long long)h-(w+h-gcd(w,h));
        
    
   
    return answer;
}
```

했는데 안되서 보니까 또 long long으로 바꿔야 된다고 해서 필요없는 total이나 tempw, temph등을 지우고 최대한 깔끔해보이게 만들었다.