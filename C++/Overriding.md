## 오버라이딩

* 하위 클래스에서 상위 클래스 메서드를 재정의할 수 있는 기능
* C++에서는 virtual 키워드가 있어야 오버라이딩이 가능하다.
* 오버라이딩 특징
    * 오버라이드하고자 하는 메서드가 상위 클래스에 존재하여야 한다.
    * 메서드 이름은 같아야 한다.
    * 메서드 매개변수 개수, 데이터 타입이 같아야 한다.
    * 메서드 반환형이 같아야 한다.

```
#include <iostream>
using namespace std;
class A{
public:
    virtual void fn(){                    //오버라이딩을 위해 virtual 키워드를 붙임
        cout<<"A"<<endl;
    }
};

class B : public A {                      //A상속받은 클래스 B선언
    public:
    virtual void fn(){                    //오버라이드를 위해 virtual 키워드를 붙임
        cout << "B" << endl;
    }
};

void main(){
    A* a = new B();                      //자식 클래스 B 선언 부모 클래스 A 상속
    a->fn();                            //a는 B클래스로 생성되었기 때문에 B의 fn실행
    delete a;
}
```