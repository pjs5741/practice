## 채널 설정

프로젝트 세팅에 있는 콜리전에서 새 오브젝트 채널을 MyCharacter라는 이름으로 만든다

![1](https://user-images.githubusercontent.com/48274630/163755027-8e3ef202-0c5f-4092-9478-bebb923884fb.PNG)

하단의 preset 섹션으로 가서 MyCharacter라는 프리셋을 추가한다.

![2](https://user-images.githubusercontent.com/48274630/163755030-c4c9324d-c766-4d1e-b6cc-d9e4653bea9e.PNG)

Trigger 프리셋으로 들어가서 MyCharacter 채널과의 반응을 겹침으로 변경해준다.

![3](https://user-images.githubusercontent.com/48274630/163755032-34eebb2b-804e-4c75-88c5-d5be0f0a81c6.PNG)

다른 프리셋들도 다음과 같이 바꿔준다

* OverlapAll:: 겹침
* OverlapAllDynamic: 겹침
* IgnoreOnlyPawn: 무시
* OverlapOnlyPawn: 겹침
* Spectator: 무시
* CharacterMesh: 무시
* RagDoll: 무시
* UI: 겹침

캡슐 컴포넌트가 해당 프리셋을 사용하도록 코드로 기본값을 지정한다.

MyCharacter.cpp
```
AMyCharacter::AMyCharacter()
{
    GetCapsuleComponent()->SetCollisionProfileName(TEXT("MyCharacter"));
}
```
위 코드를 치고 캐릭터의 캡슐 컴포넌트에 콜리전 프리셋이 Pawn에서 MyCharacter로 변경되었는지 확인한다

![4](https://user-images.githubusercontent.com/48274630/163755033-325ec950-6165-448c-9b3b-cda28ff3606b.PNG)


확인이 되었으면 물리 엔진을 사용한 공격 기능을 구현하기위해 Attack 이라는 이름으로 트레이스 채널을 하나 추가하고 기본 반응을 무시로 설정한다.

![5](https://user-images.githubusercontent.com/48274630/163755035-112859f5-0792-4f06-af1d-27057e56d68a.PNG)

후에 Preset에서 MyCharacter를 열고 Attack 채널과의 설정을 블록으로 설정한다.

![6](https://user-images.githubusercontent.com/48274630/163755036-760e78b0-eec9-4011-bed3-6f6ccf6cf644.PNG)

이제 공격 판정을 내리는 로직을 캐릭터에 추가한다. 공격 범위는 반지름 50cm 캐릭터 위치에서 정면으로 200cm 떨어진 곳까지 스윕해서 충돌하는 물체를 감지한다.

콜리전 채널을 지정하고 FCollisionShape::MakeSphere함수로 도형을 제작한다. 이 도형은 공격 명령을 내리는 자신은 감지되지 않도록 포인터 this를 무시할 액터 목록에 넣어줘야 한다.

MyCharacter.h
```
class QWER_API AMyCharacter : public ACharacter
{
    private:
        void Attack();
};
```

MyCharacter.cpp
```
void AMyCharacter::PostInitializeComponents()
{
        MyAnim->OnAttackHitCheck.AddUObject(this, &AMyCharacter::AttackCheck);
}

void AMyCharacter::AttackCheck()
{
	FHitResult HitResult;
	FCollisionQueryParams Params(NAME_None, false, this);
	bool bResult = GetWorld()->SweepSingleByChannel(
		HitResult,
		GetActorLocation(),
		GetActorLocation() + GetActorForwardVector() * AttackRange,
		FQuat::Identity,
		ECollisionChannel::ECC_GameTraceChannel2,
		FCollisionShape::MakeSphere(AttackRadius),
		Params);
```


MyCharacter.h
```
class QWER_API AMyCharacter : public ACharacter
{
    UPROPERTY(VisibleInstanceOnly, BlueprintReadOnly, Category = Attack, Meta = (AllowPrivateAccess = true))
		float AttackRange;
	UPROPERTY(VisibleInstanceOnly, BlueprintReadOnly, Category = Attack, Meta = (AllowPrivateAccess = true))
		float AttackRadius;
};
```


MyCharacter.cpp
```
#include "DrawDebugHelpers.h"

AMyCharacter::AMyCharacter()
{
    AttackRange = 200.0f;
	AttackRadius = 50.0f;
}

void AMyCharacter::AttackCheck()
{
	FHitResult HitResult;
	FCollisionQueryParams Params(NAME_None, false, this);
	bool bResult = GetWorld()->SweepSingleByChannel(
		HitResult,
		GetActorLocation(),
		GetActorLocation() + GetActorForwardVector() * AttackRange,
		FQuat::Identity,
		ECollisionChannel::ECC_GameTraceChannel2,
		FCollisionShape::MakeSphere(AttackRadius),
		Params);


#if ENABLE_DRAW_DEBUG

	FVector TraceVec = GetActorForwardVector() * AttackRange;
	FVector Center = GetActorLocation() + TraceVec * 0.5f;
	float HalfHeight = AttackRange * 0.5f + AttackRadius;
	FQuat CapsuleRot = FRotationMatrix::MakeFromZ(TraceVec).ToQuat();
	FColor DrawColor = bResult ? FColor::Green : FColor::Red;
	float DebugLifeTime = 5.0f;

	DrawDebugCapsule(GetWorld(),
		Center,
		HalfHeight,
		AttackRadius,
		CapsuleRot,
		DrawColor,
		false,
		DebugLifeTime);

#endif
	
}
```

플레이 버튼을 눌러 공격해보면 공격 범위가 표시되고 판정이 발생하면 녹색, 아니면 빨간색으로 표시된다.

대미지를 전달하기 위해 다음 코드를 추가한다.
MyCharacter.cpp
```
void AMyCharacter::AttackCheck()
{
    ...

	if (bResult)
	{
		if (HitResult.Actor.IsValid())
		{
			FDamageEvent DamageEvent;
			HitResult.Actor->TakeDamage(50.0f, DamageEvent, GetController(), this);
		}
	}
	
}
```

다음에는 TakeDamage함수를 오버라이드해서 액터가 받은 대미지를 처리하는 로직을 추가한다.
TakeDamage 함수는 부모 클래스인 AActor에 기본적인 대미지 관련 로직이 구현돼 있기 때문에 Super 키워드를 사용해 부모 클래스의 로직을 먼저 실행해줘야 한다.

MyCharacter.h
```
class QWER_API AMyCharacter : public ACharacter
{
	GENERATED_BODY()

    public:	
	// Called every frame
	virtual void Tick(float DeltaTime) override;
	virtual void PostInitializeComponents() override;
	virtual float TakeDamage(float DamageAmount, struct FDamageEvent const& DamageEvent, class AController* EventInstigator, AActor* DamageCauser) override;
	// Called to bind functionality to input
	virtual void SetupPlayerInputComponent(class UInputComponent* PlayerInputComponent) override;
};
```

MyCharacter.cpp
```
float AMyCharacter::TakeDamage(float DamageAmount, struct FDamageEvent const& DamageEvent, class AController* EventInstigator, AActor* DamageCauser)
{
	float FinalDamage = Super::TakeDamage(DamageAmount, DamageEvent, EventInstigator, DamageCauser);
	
	return FinalDamage;
}
```

다음은 캐릭터가 대미지를 받으면 사망하는 애니메이션을 설정한다.

MyAnimInstance.h
```
lass QWER_API UMyAnimInstance : public UAnimInstance
{
	GENERATED_BODY()
	

    public:
	FOnNextAttackCheckDelegate OnNextAttackCheck;
	FOnAttackHitCheckDelegate OnAttackHitCheck;
	void SetDeadAnim() { IsDead = true; }

    private:
	UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = Pawn, Meta = (AllowPrivateAccess = true))
		float CurrentPawnSpeed;

	UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = Pawn, Meta = (AllowPrivateAccess = true))
		bool IsInAir;

	UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = Attack, Meta = (AllowPrivateAccess = true))
		UAnimMontage* AttackMontage;
	UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = Pawn, Meta = (AllowPrivateAccess = true))
		bool IsDead;
};
```

MyAnimInstance.cpp

```
UMyAnimInstance::UMyAnimInstance()
{
	CurrentPawnSpeed = 0.0f;
	IsInAir = false;
	IsDead = false;
	static ConstructorHelpers::FObjectFinder<UAnimMontage> ATTACK_MONTAGE(TEXT("/Game/Mannequin/Animations/UE4_Mannequin_Skeleton_Montage.UE4_Mannequin_Skeleton_Montage"));
	if (ATTACK_MONTAGE.Succeeded())
	{
		AttackMontage = ATTACK_MONTAGE.Object;
	}
}

void UMyAnimInstance::NativeUpdateAnimation(float DeltaSeconds)
{
	Super::NativeUpdateAnimation(DeltaSeconds);

	auto Pawn = TryGetPawnOwner();
	if (!::IsValid(Pawn)) return;
	if (!IsDead)
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

MyCharacter.cpp

```
float AMyCharacter::TakeDamage(float DamageAmount, struct FDamageEvent const& DamageEvent, class AController* EventInstigator, AActor* DamageCauser)
{
	float FinalDamage = Super::TakeDamage(DamageAmount, DamageEvent, EventInstigator, DamageCauser);
	if (FinalDamage > 0.0f)
	{
		MyAnim->SetDeadAnim();
		SetActorEnableCollision(false);
	}
	return FinalDamage;
}
```

![7](https://user-images.githubusercontent.com/48274630/163757582-bc5bd3bb-7917-4bfc-9377-122becb1373d.PNG)