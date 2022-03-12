# Actor

액터란 언리얼 엔진에서 콘텐츠를 구성하는 최소 단위의 물체이다.

이름, 유형, 트랜스폼, 프로퍼티, 게임 로직으로 구성되며, 게임에서의 주요 기능은
시각적 기능, 물리적 기능, 움직임 크게 세 가지로 나눌 수 있다.

액터를 설계할 때 다양한 경우에 유연하게 대처하기 위해 기능을 규격화하고 액터가 이들을 조합할 수 있도록 설계했는데, 이러한 기능을 컴포넌트라고 하며
이번에는 스태틱메시 컴포넌트라는 애니메이션이 없는 스태틱메시를 사용해 시각적인 기능과 물리적인 기능을 제공하는 모듈을 간단하게 만들어 본다.


## 1. 우선 좌상단에 파일->새로운 C++클래스를 선택후에 부모클래스를 엑터를 선택하고 만든다.
![1](https://user-images.githubusercontent.com/48274630/158016897-93121a15-35ad-4e97-a79e-c580cb91460c.PNG)


## 2. 헤더파일에서 형광팬이 있는 부분을 써준다.
![2](https://user-images.githubusercontent.com/48274630/158016918-a40796b5-1dcb-4922-b525-dc2a6c1732c6.PNG)
#include "EngineMinimal.h"는 UStaticMeshComponent의 클래스 정보를 참조 할 수 있도록 설정해주기 위해서 사용하였고, UPROPERTY()는 언리얼에서 선언한 객체를 자동으로 관리하게 해주는 매크로로 메모리 관리를 위해서 사용하였고 괄호안에 VisibleAnywhere은 디테일 부분에서 컴포넌트의 속성 값을 편집할 수 있게 해주기위해서 선언하였다.

## 3. .cpp파일에도 형광팬 부분을 써준다.

![3](https://user-images.githubusercontent.com/48274630/158016919-df7c1acf-06f5-4cb0-b951-65e44b3a0cf6.PNG)
언리얼 엔진에선 컴포넌트를 생성하는 용도로 new가 아닌 CreateDefaultSubobject API라는 특별한 함수를 제공해서 해당 함수로 컴포넌트를 생성하고 TEXT는 모든 플랫폼에서 2바이트 문자열 체계를 동일하게 유지시키는 매크로이다.


## 4. 생성완료
![4](https://user-images.githubusercontent.com/48274630/158016920-67bdfbe9-d7f2-4167-b0eb-755e041cc3e5.PNG)

## 5. 디태일 패널에서 모양과 재질을 선택

![5](https://user-images.githubusercontent.com/48274630/158017975-ba44e2af-85ad-4e5b-8602-d92c7839f6ad.PNG)
