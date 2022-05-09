## 오버로딩

* 동일 이름의 메서드를 매개변수만 다르게 하여 여러 개 정의할 수 있는 기능이다.

* 오버로딩의 특징
    * 메서드 이름이 같아야 한다.
    * 매개변수 개수가 달라야 한다.
    * 매개변수 개수가 같을 경우 데이터 타입이 달라야 한다.
    * 변환형은 같거나 달라도 된다.


```
#include <iostream>
using namespace std;
class A{
    public:
    void fn(){                                  //매개변수x void,    1번
        cout << "없음"<<endl;
    }
    void fn(double d){                          //매개변수 정수형 1개, void, 2번
        cout << d << endl;
    }
    void fn(double d){                          //매개변수 실수형 1개, void, 3번
        cout << d << endl;
    }
    int fn(int a, int b){                       //매개변수 두개, int,   4번
        return a+b;
    }
};

void main(){
    A* a = new A();                             //A클래스의 객체 a생성

    a->fn();                                    //1번 호출
    
    a->fn(7);                                   //2번 호출

    a->fn(10.0);                                //3번 호출

    cout << a->fn(2,3)<<endl;                   //4번 호출
}
``