# NameSpace
## 네임스페이스란
개체를 구분할 수 있는 범위를 나타내는 말로 일반적으로 하나의 에서는 하나의 이름이 단 하나의 개체만을 가리키게 된다.
예를 들면   
```
namespace Jack{
    double pail;
    void fetch();
    int pal;
    struct Well {...}
}
namespace Jill{
    double bucket(double n) {...}
    double fetch;
    int pal;
    struct Hill {...};
}    
```
 
이렇게 두개의 네임스페이스를 만들면 Jack과 Jill의 fetch는 공존할 수 있고, 
Jill의Hill은 외부 Hill과 공존할 수 있다.  
접근하는 방법은 연산자::를 사용하며
```
Jack::pail = 12.34;
Jill::Hil mole;
Jack::fetch();
```
이런식으로 나타낼 수 있고, pail과 같이, 특별한 네임스페이스가 지정되지 않은 이름을 unqualified name이라 하고, 
Jack::pail처럼 지정된 이름을 qualified name이라 한다.
 
네임 스페이스를 사용할 때마다 매번 이름을 제한한다는 것은 성가시므로, 
C++는 이름 공간에 속해 있는 이름을 간편하게 사용할 수 있는, using 선언과 using 지시자라는 두 가지 방법을 제공한다.
using 선언은 하나의 특별한 식별자를 사용할 수 있게 만들고, 
using 지시자는 그 이름 공간 전체에 접근할 수 있게 만든다.
using 선언은 제한된 이름 앞에 키워드using을 붙이는 것이다.
  