# 애님 인스턴스
스케레탈 메시를 소유하는 폰의 정보를 받아 애님 그래프가 참조할 데이터를 제공하며, 블루프린트와 C++로 제작가능

![1](https://user-images.githubusercontent.com/48274630/158994310-baf8add5-7b6d-44e1-9367-d9aca94c8c4f.PNG)

모든 클래스 표시후에 AnimInstance을 생성한다.

MyAnimInstance.h
```
public:
	UMyAnimInstance();
	virtual void NativeUpdateAnimation(float DeltaSeconds) override;

private:
	UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = Pawn, Meta = (AllowPrivateAccess = true))
		float CurrentPawnSpeed;
        };
 ```

 MyAnimInstance.cpp
 ```
 UMyAnimInstance::UMyAnimInstance()
{
	CurrentPawnSpeed = 0.0f;
}
```
코드를 치고 애니메이션 블루프린트를 더블 클릭해서 연다.

폰과 데이터를 연동하여 애님 인스턴스의 Tick에서 폰의 속도 정보를 가져온 후 CurrentPawnSpped에 업데이트를 해본다.
MyAnimInstance.h
```
public:
	UMyAnimInstance();
	virtual void NativeUpdateAnimation(float DeltaSeconds) override;
```
MyAnimInstance.cpp
```
void UMyAnimInstance::NativeUpdateAnimation(float DeltaSeconds)
{
	Super::NativeUpdateAnimation(DeltaSeconds);

	auto Pawn = TryGetPawnOwner();
	if (::IsValid(Pawn))
	{
		CurrentPawnSpeed = Pawn->GetVelocity().Size();
	}
}
```
컴파일하고 재생해보면 캐릭터가 움직일때는 달리기모션을 하는것을 볼 수 있다.

## 점프구현
MyCharacter.cpp
```
	PlayerInputComponent->BindAction(TEXT("Jump"), EInputEvent::IE_Pressed, this, &ACharacter::Jump);
```
MyAnimInstance.h
```
UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = Pawn, Meta = (AllowPrivateAccess = true))
		bool IsInAir;
```

MyAnimInstance.cpp
```
// Fill out your copyright notice in the Description page of Project Settings.


#include "MyAnimInstance.h"

UMyAnimInstance::UMyAnimInstance()
{
	CurrentPawnSpeed = 0.0f;
	IsInAir = false;
}

void UMyAnimInstance::NativeUpdateAnimation(float DeltaSeconds)
{
	Super::NativeUpdateAnimation(DeltaSeconds);

	auto Pawn = TryGetPawnOwner();
	if (::IsValid(Pawn))
	{
		CurrentPawnSpeed = Pawn->GetVelocity().Size();
		auto Character = Cast<ACharacter>(Pawn);
		if (Character)
		{
			IsInAir = Character->GetMovementComponent()->IsFalling();
		}
	}
}
```
코드 완성
# 애님 그래프
애님 인스턴스의 변수 값에 따라 변화하는 애니메이션 시스템을 설계하는 공간, 블루프린트로만 제작가능

![2](https://user-images.githubusercontent.com/48274630/158994318-14bffd6d-1220-4971-8a9b-f538b4765ba4.PNG)
왼쪽에 내 블루프린트의 눈모양을 누르고 상속된 변수 표시를 체크하면 방금만든 CurrentPawnSpeed라는 함수가 보이는데 이 함수를 컨트롤+드로그앤드롭한다.

그 후에 노드를 드래그해서 >부등호를 검색해 float>float 노드를 선택, 다시 드래그해 blend를 검색해 bool 포즈를 블랜딩합니다를 선택후에 우측 에셋 브라우저에서 Idle과 Run모션을 끌어오고 True에는 Run을, False에는 Idle을 연결한다.
![3](https://user-images.githubusercontent.com/48274630/158995875-386e4b5d-c32b-4024-9e16-fc31f1c5a829.PNG)

# 스테이트머신
스테이트머신 더블클릭->entry 드로그 스테이트머신 새로추가(Ground)->들어가서 방금 만들었던 달리기,가만히있기 블루프린트를 가져옴
![4](https://user-images.githubusercontent.com/48274630/158997675-7c42c941-094d-47c4-813a-ce82d601cbb9.PNG)
위와 같은 모양으로만든후에 점프 스타트와 엔드에 들어가서 각각 애니메이션연결, 스타트와 루프에서는 Time Remaining(ratio)노드를 만든후 >검색으로 float>float과 원래있던 노드연결 엔드에서 그라운드로가는 스테이트도 동일하게 만듬
![5](https://user-images.githubusercontent.com/48274630/158997985-2a3e4bfd-0a44-4696-8fd5-e9ee80b88cb7.PNG)

그라운드->스타트
![6](https://user-images.githubusercontent.com/48274630/158998164-20d66c16-fe11-4664-b5c2-b41f7d89f10d.PNG)
엔드->그라운드위사진에서 중간에 NOT노드하나 추가