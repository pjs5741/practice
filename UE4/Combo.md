# 콤보 공격 구현

준비해둔 애니메이션을 드래그해서 넣는다.

![1](https://user-images.githubusercontent.com/48274630/163615906-5396830e-af33-4b85-98f9-b66b7230fdcb.PNG)

툴바의 세팅->프로젝트 세팅에서 Action Mappings의 Attack이라는 입력 명에 왼쪽 마우스 버튼 입력을 지정한다.

![2](https://user-images.githubusercontent.com/48274630/163616020-bf809428-036b-4a9d-8144-f0f40706d4e7.PNG)

그 후 Attack 함수를 Character에 추가한다.

MyCharacter.h

```
private:
	void MoveForward(float NewAxisValue);
	void MoveRight(float NewAxisValue);
	void LookUp(float NewAxisValue);
	void Turn(float NewAxisValue);

	void Attack();
```

MyCharacter.cpp

```
void AMyCharacter::SetupPlayerInputComponent(UInputComponent* PlayerInputComponent)
{
	Super::SetupPlayerInputComponent(PlayerInputComponent);

	PlayerInputComponent->BindAxis(TEXT("MoveForward"), this, &AMyCharacter::MoveForward);
	PlayerInputComponent->BindAxis(TEXT("MoveRight"), this, &AMyCharacter::MoveRight);
	PlayerInputComponent->BindAxis(TEXT("LookUp"), this, &AMyCharacter::LookUp);
	PlayerInputComponent->BindAxis(TEXT("Turn"), this, &AMyCharacter::Turn);
	PlayerInputComponent->BindAction(TEXT("Jump"), EInputEvent::IE_Pressed, this, &ACharacter::Jump);
	PlayerInputComponent->BindAction(TEXT("Attack"), EInputEvent::IE_Pressed, this, &AMyCharacter::Attack);
	

}


void MyCharacter::Attack()
{

}
```

그 후 애님 인스턴스에 멤버 함수와 변수를 생성하고 함수를 실행하면 몽타주 애니메이션을 재생하도록 기능을 구현한다.

Montage_IsPlaying 함수를 사용해 현재 몽타주가 재생하는지 파악하고, 재생 중이 아니면 Montage_Play 함수를 사용해 재생하도록 로직을 구현한다.

MyAnimInstance.h

```
public:
	UMyAnimInstance();
	virtual void NativeUpdateAnimation(float DeltaSeconds) override;


	void PlayAttackMontage();

...

private:
	UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = Pawn, Meta = (AllowPrivateAccess = true))
		float CurrentPawnSpeed;

	UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = Pawn, Meta = (AllowPrivateAccess = true))
		bool IsInAir;

	UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = Attack, Meta = (AllowPrivateAccess = true))
		UAnimMontage* AttackMontage;
```


MyAnimInstance.cpp

```
UMyAnimInstance::UMyAnimInstance()
{
	CurrentPawnSpeed = 0.0f;
	IsInAir = false;
	static ConstructorHelpers::FObjectFinder<UAnimMontage> ATTACK_MONTAGE(TEXT("/Game/Mannequin/Animations/UE4_Mannequin_Skeleton_Montage.UE4_Mannequin_Skeleton_Montage"));
	if (ATTACK_MONTAGE.Succeeded())
	{
		AttackMontage = ATTACK_MONTAGE.Object;
	}
}

void UMyAnimInstance::PlayAttackMontage()
{	
    if( !Montage_IsPlaying(AttackMontage))
    {
		Montage_Play(AttackMontage, 1.0f);	
    }
}
```

몽타주에게 재생 명령을 내려도 애니메이션 블루프린트에서 이를 재생하려면 몽타주 재생 노드를 애님 그래프에 추가해야 함으로 블루프린트에서 애님 그래프의 최종 애니메이션 포즈와 스테이트 머신 사이에 몽타주 재생 노드를 추가한다.

애님 그래프를 우클릭해서 DefaultSlot 슬롯 메뉴를 선택하고 이어준다.

![3](https://user-images.githubusercontent.com/48274630/163623209-ede97df8-7108-44fa-b02a-e4c198b37127.PNG)


노드 완성후 캐릭터에게 몽타주를 사용해 공격 애니메이션을 재생하라는 명령을 내린다.

MyCharacter.cpp

```
#include "MyAnimInstance.h"

void MyCharacter::Attack()
{
    auto AnimInstance = Cast<UMyAnimInstance>(GetMesh()->GetAnimInstance());
    if(nullptr == AnimInstance) return;

    AnimInstance->PlayAttackMontage();
}
```

그 후 델리게이트를 사용하기 위해 아래 코드를추가한다.

MyCharacter.h


```
public:	
	// Called every frame
	virtual void Tick(float DeltaTime) override;
	virtual void PostInitializeComponents() override;


private:
	void MoveForward(float NewAxisValue);
	void MoveRight(float NewAxisValue);
	void LookUp(float NewAxisValue);
	void Turn(float NewAxisValue);

	void Attack();

	UFUNCTION()
		void OnAttackMontageEnded(UAnimMontage* Montage, bool bInterrupted);

	
private:
	UPROPERTY(VisibleInstanceOnly, BlueprintReadOnly, Category = Attack, Meta = (AllowPrivateAccess = true))
	bool IsAttacking;
```

매크로를 활용해 애님 인스턴스의 OnMontageEnded 델리게이트와 우리가 선언한 OnAttackMontageEnded를 연결해, 델리게이트가 발동할 때까지 애니메이션 시스템에 몽타주 재생 명령을 내리지 못하게 폰 로직에서 막아준다.

MyCharacter.cpp

```
AMyCharacter::AMyCharacter()
{
IsAttacking = false;
}

oid AMyCharacter::PostInitializeComponents()
{
	Super::PostInitializeComponents();
	auto AnimInstance = Cast<UMyAnimInstance>(GetMesh()->GetAnimInstance());
    AnimInstance->OnMontageEnded.AddDynamic(this, &AMyCharacter::OnAttackMontageEnded);

}

void AMyCharacter::Attack()
{
	if (IsAttacking) return;
	 auto AnimInstance = Cast<UMyAnimInstance>(GetMesh()->GetAnimInstance());
    if(nullptr == AnimInstance) return;

    AnimInstance->PlayAttackMontage();
    IsAttacking = true;
}

void AMyCharacter::OnAttackMontageEnded(UAnimMontage* Montage, bool bInterrupted)
{
	IsAttacking = false;
}
```

애님 인스턴스를 멤버 변수로 선언해 런타임에서 이를 활용하도록 구조를 변경해본다.

MyCharacter.h
```
private:
	UPROPERTY(VisibleInstanceOnly, BlueprintReadOnly, Category = Attack, Meta = (AllowPrivateAccess = true))
	bool IsAttacking;

	UPROPERTY()
	class UMyAnimInstance* MyAnim;
```

MyCharacter.cpp
```
void AMyCharacter::PostInitializeComponents()
{
	Super::PostInitializeComponents();
	MyAnim = Cast<UMyAnimInstance>(GetMesh()->GetAnimInstance());

	MyAnim->OnMontageEnded.AddDynamic(this, &AMyCharacter::OnAttackMontageEnded);

}


void AMyCharacter::Attack()
{
	if (IsAttacking) return;

	MyAnim->PlayAttackMontage();
    IsAttacking = true;
}

```

공격의 시작과 종료는 델리게이트로 감지해서 AnimInstance에서 사용한 Montage_IsPlaying 함수는 지운다.

MyAnimInstance.cpp

```
void UMyAnimInstance::PlayAttackMontage()
{	
		Montage_Play(AttackMontage, 1.0f);	
}
```

이제 노티파이를 추가해야 한다. 애니메이션 몽타주 창에서 노티파이 추가를 한 후에 이름을 AttackHitCheck를 추가하고 배치한다.

섹션을 추가하고 하나씩 드래그해서 애니메이션 설정을해주고 섹션을 분리한다
그 후에 노티파이를 하나 더 추가해서 NextAttackCheck라는 이름으로 만들어준다. 이 노티파이는 Branching point 값으로 틱 타입을 변경하는 것이 좋다. 기본값이 Queued로 설정하면 비동기 방식으로 신호를 받게 돼서 적절한 타이밍에 신호를 받는 것을 놓치게 될 수 있다.

![6](https://user-images.githubusercontent.com/48274630/163628369-57b8e96f-5540-4bf4-858d-76e55713cbca.PNG)

애님 인스턴스에서 애니메이션 노티파이를 감지하도록 코드는 만든다.

MyAnimInstance.h
```
private:
	UFUNCTION()
		void AnimNotify_AttackHitCheck();

	UFUNCTION()
		void AnimNotify_NextAttackCheck();
```

MyAnimInstance.cpp
```
void UMyAnimInstance::AnimNotify_AttackHitCheck()
{
	
}



void UMyAnimInstance::AnimNotify_NextAttackCheck()
{
	
}
```

이제 콤보 구현을 하도록 코드를 만든다.

MyCharacter.h
```
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "Engineminimal.h"
#include "GameFramework/Character.h"
#include "MyCharacter.generated.h"

UCLASS()
class QWER_API AMyCharacter : public ACharacter
{
	GENERATED_BODY()

public:
	// Sets default values for this character's properties
	AMyCharacter();

protected:
	// Called when the game starts or when spawned
	virtual void BeginPlay() override;


	void SetControlMode();

public:	
	// Called every frame
	virtual void Tick(float DeltaTime) override;
	virtual void PostInitializeComponents() override;

	// Called to bind functionality to input
	virtual void SetupPlayerInputComponent(class UInputComponent* PlayerInputComponent) override;

	UPROPERTY(VisibleAnywhere, Category = Camera)
		USpringArmComponent* SpringArm;

	UPROPERTY(VisibleAnywhere, Category = Camera)
		UCameraComponent* Camera;

private:
	void MoveForward(float NewAxisValue);
	void MoveRight(float NewAxisValue);
	void LookUp(float NewAxisValue);
	void Turn(float NewAxisValue);

	void Attack();

	UFUNCTION()
		void OnAttackMontageEnded(UAnimMontage* Montage, bool bInterrupted);

	void AttackStartComboState();
	void AttackEndComboState();

private:
	UPROPERTY(VisibleInstanceOnly, BlueprintReadOnly, Category = Attack, Meta = (AllowPrivateAccess = true))
	bool IsAttacking;

	UPROPERTY()
	class UMyAnimInstance* MyAnim;

	UPROPERTY(VisibleInstanceOnly, BlueprintReadOnly, Category = Attack, Meta = (AllowPrivateAccess = true))
		bool CanNextCombo;

	UPROPERTY(VisibleInstanceOnly, BlueprintReadOnly, Category = Attack, Meta = (AllowPrivateAccess = true))
		bool IsComboInputOn;

	UPROPERTY(VisibleInstanceOnly, BlueprintReadOnly, Category = Attack, Meta = (AllowPrivateAccess = true))
		int32 CurrentCombo;

	UPROPERTY(VisibleInstanceOnly, BlueprintReadOnly, Category = Attack, Meta = (AllowPrivateAccess = true))
		int32 MaxCombo;
};

```
MyCharacter.cpp
```
// Fill out your copyright notice in the Description page of Project Settings.


#include "MyCharacter.h"
#include "MyAnimInstance.h"

// Sets default values
AMyCharacter::AMyCharacter()
{
 	// Set this character to call Tick() every frame.  You can turn this off to improve performance if you don't need it.
	PrimaryActorTick.bCanEverTick = true;
	SpringArm = CreateDefaultSubobject<USpringArmComponent>(TEXT("SPRINGARM"));
	Camera = CreateDefaultSubobject<UCameraComponent>(TEXT("CAMERA"));

	SpringArm->SetupAttachment(GetCapsuleComponent());
	Camera->SetupAttachment(SpringArm);

	GetMesh()->SetRelativeLocationAndRotation(FVector(0.0f, 0.0f, -88.0f), FRotator(0.0f, -90.0f, 0.0f));
	SpringArm->TargetArmLength = 400.0f;
	SpringArm->SetRelativeRotation(FRotator(-15.0f, 0.0f, 0.0f));

	static ConstructorHelpers::FObjectFinder<USkeletalMesh> SKELETALMESH(TEXT("/Game/Mannequin/Character/Mesh/SK_Mannequin.SK_Mannequin"));
	if (SKELETALMESH.Succeeded())
	{
		GetMesh()->SetSkeletalMesh(SKELETALMESH.Object);
	}
	GetMesh()->SetAnimationMode(EAnimationMode::AnimationBlueprint);

	static ConstructorHelpers::FClassFinder<UAnimInstance> BP_Character_C(TEXT("/Game/Mannequin/Animations/ThirdPerson_AnimBP.ThirdPerson_AnimBP_C"));
	if (BP_Character_C.Succeeded())
	{
		GetMesh()->SetAnimInstanceClass(BP_Character_C.Class);
	}

	GetCharacterMovement()->JumpZVelocity = 300.0f;
	SetControlMode();
	IsAttacking = false;
	MaxCombo = 2;
	AttackEndComboState();
}

// Called when the game starts or when spawned
void AMyCharacter::BeginPlay()
{
	Super::BeginPlay();
	
}

void AMyCharacter::SetControlMode()
{
		SpringArm->TargetArmLength=450.0f;
		SpringArm->SetRelativeRotation(FRotator::ZeroRotator);
		SpringArm->bUsePawnControlRotation=true;
		SpringArm->bInheritRoll=true;
		SpringArm->bInheritYaw=true;
		SpringArm->bDoCollisionTest=true;
		bUseControllerRotationYaw=false;
		GetCharacterMovement()->bOrientRotationToMovement = true;
		GetCharacterMovement()->RotationRate = FRotator(0.0f, 400.0f, 0.0f);
}

// Called every frame
void AMyCharacter::Tick(float DeltaTime)
{
	Super::Tick(DeltaTime);

}

// Called to bind functionality to input
void AMyCharacter::SetupPlayerInputComponent(UInputComponent* PlayerInputComponent)
{
	Super::SetupPlayerInputComponent(PlayerInputComponent);

	PlayerInputComponent->BindAxis(TEXT("MoveForward"), this, &AMyCharacter::MoveForward);
	PlayerInputComponent->BindAxis(TEXT("MoveRight"), this, &AMyCharacter::MoveRight);
	PlayerInputComponent->BindAxis(TEXT("LookUp"), this, &AMyCharacter::LookUp);
	PlayerInputComponent->BindAxis(TEXT("Turn"), this, &AMyCharacter::Turn);
	PlayerInputComponent->BindAction(TEXT("Jump"), EInputEvent::IE_Pressed, this, &ACharacter::Jump);
	PlayerInputComponent->BindAction(TEXT("Attack"), EInputEvent::IE_Pressed, this, &AMyCharacter::Attack);
	

}

void AMyCharacter::MoveForward(float NewAxisValue)
{
	AddMovementInput(FRotationMatrix(GetControlRotation()).GetUnitAxis(EAxis::X),NewAxisValue);
}

void AMyCharacter::MoveRight(float NewAxisValue)
{
	AddMovementInput(FRotationMatrix(GetControlRotation()).GetUnitAxis(EAxis::Y), NewAxisValue);
}

void AMyCharacter::LookUp(float NewAxisValue)
{
	AddControllerPitchInput(NewAxisValue);
}

void AMyCharacter::Turn(float NewAxisValue)
{
	AddControllerYawInput(NewAxisValue);
}

void AMyCharacter::Attack()
{
	if (IsAttacking)
	{
		if (CanNextCombo)
		{
			IsComboInputOn = true;
		}
	}
	else
	{
		AttackStartComboState();
		MyAnim->PlayAttackMontage();
		IsAttacking = true;
	}
}

void AMyCharacter::PostInitializeComponents()
{
	Super::PostInitializeComponents();
	MyAnim = Cast<UMyAnimInstance>(GetMesh()->GetAnimInstance());

	MyAnim->OnMontageEnded.AddDynamic(this, &AMyCharacter::OnAttackMontageEnded);

	MyAnim->OnNextAttackCheck.AddLambda([this]()->void {
		CanNextCombo = false;

		if (IsComboInputOn)
		{
			AttackStartComboState();
			MyAnim->JumpToAttackMontageSection(CurrentCombo);
		}
		});
}

void AMyCharacter::OnAttackMontageEnded(UAnimMontage* Montage, bool bInterrupted)
{
	IsAttacking = false;
	AttackEndComboState();
}


void AMyCharacter::AttackStartComboState()
{
	CanNextCombo = true;
	IsComboInputOn = false;
	CurrentCombo = FMath::Clamp<int32>(CurrentCombo + 1, 1, MaxCombo);
}

void AMyCharacter::AttackEndComboState()
{
	IsComboInputOn = false;
	CanNextCombo = false;
	CurrentCombo = 0;
}
```

MyAnimInstance.h
```
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "Engineminimal.h"
#include "Animation/AnimInstance.h"
#include "MyAnimInstance.generated.h"

DECLARE_MULTICAST_DELEGATE(FOnNextAttackCheckDelegate);
DECLARE_MULTICAST_DELEGATE(FOnAttackHitCheckDelegate);

/**
 * 
 */
UCLASS()
class QWER_API UMyAnimInstance : public UAnimInstance
{
	GENERATED_BODY()
	

public:
	UMyAnimInstance();
	virtual void NativeUpdateAnimation(float DeltaSeconds) override;


	void PlayAttackMontage();
	void JumpToAttackMontageSection(int32 NewSection);

public:
	FOnNextAttackCheckDelegate OnNextAttackCheck;
	FOnAttackHitCheckDelegate OnAttackHitCheck;
private:
	UFUNCTION()
		void AnimNotify_AttackHitCheck();

	UFUNCTION()
		void AnimNotify_NextAttackCheck();

	FName GetAttackMontageSectionName(int32 Section);

private:
	UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = Pawn, Meta = (AllowPrivateAccess = true))
		float CurrentPawnSpeed;

	UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = Pawn, Meta = (AllowPrivateAccess = true))
		bool IsInAir;

	UPROPERTY(EditAnywhere, BlueprintReadOnly, Category = Attack, Meta = (AllowPrivateAccess = true))
		UAnimMontage* AttackMontage;
};

```

MyAnimInstance.cpp
```
// Fill out your copyright notice in the Description page of Project Settings.


#include "MyAnimInstance.h"

UMyAnimInstance::UMyAnimInstance()
{
	CurrentPawnSpeed = 0.0f;
	IsInAir = false;
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

void UMyAnimInstance::PlayAttackMontage()
{	
		Montage_Play(AttackMontage, 1.0f);	
}

void UMyAnimInstance::JumpToAttackMontageSection(int32 NewSection)
{
	Montage_JumpToSection(GetAttackMontageSectionName(NewSection), AttackMontage);
}

void UMyAnimInstance::AnimNotify_AttackHitCheck()
{
	OnAttackHitCheck.Broadcast();
}



void UMyAnimInstance::AnimNotify_NextAttackCheck()
{
	OnNextAttackCheck.Broadcast();
}

FName UMyAnimInstance::GetAttackMontageSectionName(int32 Section)
{
	return FName(*FString::Printf(TEXT("Attack%d"), Section));
}
```
