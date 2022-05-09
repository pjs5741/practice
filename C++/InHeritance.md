## 상속

상속은 어떤 객체가 있을 때 그 객체의 변수와 메서드를 다른 객체가 물려받는 기능이다.

```
#include<iostream>

using namespace std;

class A{
    public:
    void fnA(){
        cout<<"A"<<endl;
    }
    
};

class B : public A{             //A를 상속받는 클래스 B
    public:
    void fnB(){
        cout << "B"<<endl;
    }
};

void main(){
    B* b = new B();             //b라는 이름의 클래스 B에 대한 변수 설정

    b->fnA();                   b변수로 fnA 메서드에 접근 값은 A
    b->FnB();                   b변수로 fnB 메서드에 접근 값은 B

    delete b;                   b변수에 대한 메모리 해제
}