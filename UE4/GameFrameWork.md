# 게임플레임 프레임워크
다양한 게임의 자을와 멀티 플레이까지 수용할 수 있도록 복잡하고 방대한 구조를 가지고 있다. 그 중 핵심적인 두 가지는 게임 모드와 폰이다.

## 게임 모드
게임의 틀을 잡아주며, 플레이어가 입장할 때마다 플레이어를 점검하고 플레이어가 조종할 액터를 생성해 전달한다. 이러한 플레이어가 조종할 수 있는 액터를 폰이라고 한다.

## 폰
폰은 플레이어에게 조종당하는 액터다. 플레이어 컨트롤러가 시키는 대로 움직이는 꼭두각시다. 게임 세계에서 물리적 충돌을 하면서 액터와 상호작용한다.

## 플레이어 컨트롤러
게임에서 플레이어와 1:1로 소통하면서 폰을 조종하는 역할을 맡는다.

```
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "Engineminimal.h"
#include "GameFramework/GameModeBase.h"
#include "MyGameModeBase.generated.h"

/**
 * 
 */
UCLASS()
class QWER_API AMyGameModeBase : public AGameModeBase
{
	GENERATED_BODY()
	

public:
	AMyGameModeBase();

	virtual void PostLogin(APlayerController* NewPlayer) override;
};
```

```
// Fill out your copyright notice in the Description page of Project Settings.


#include "MyGameModeBase.h"
#include "MyPawn.h"
#include "MyPlayerController.h"

AMyGameModeBase::AMyGameModeBase()
{
	DefaultPawnClass = AMyPawn::StaticClass();
	PlayerControllerClass = AMyPlayerController::StaticClass();
}

void AMyGameModeBase::PostLogin(APlayerController * NewPlayer)
{
	Super::PostLogin(NewPlayer);
}

```

```
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "Engineminimal.h"
#include "GameFramework/Pawn.h"
#include "MyPawn.generated.h"
#include "GameFramework/FloatingPawnMovement.h"

UCLASS()
class QWER_API AMyPawn : public APawn
{
	GENERATED_BODY()

public:
	// Sets default values for this pawn's properties
	AMyPawn();

protected:
	// Called when the game starts or when spawned
	virtual void BeginPlay() override;

public:	
	// Called every frame
	virtual void Tick(float DeltaTime) override;
	virtual void PostInitializeComponents() override;
	virtual void PossessedBy(AController* NewController) override;

	// Called to bind functionality to input
	virtual void SetupPlayerInputComponent(class UInputComponent* PlayerInputComponent) override;

	UPROPERTY(VisibleAnywhere, Category = Collision)
		UCapsuleComponent* Capsule;

	UPROPERTY(VisibleAnywhere, Category = Visual)
		USkeletalMeshComponent* Mesh;

	UPROPERTY(VisibleAnywhere, Category = Movement)
		UFloatingPawnMovement* Movement;

	UPROPERTY(VisibleAnywhere, Category = Collision)
		USpringArmComponent* SpringArm;

	UPROPERTY(VisibleAnywhere, Category = Collision)
		UCameraComponent* Camera;

};
```

```
// Fill out your copyright notice in the Description page of Project Settings.


#include "MyPawn.h"

// Sets default values
AMyPawn::AMyPawn()
{
 	// Set this pawn to call Tick() every frame.  You can turn this off to improve performance if you don't need it.
	PrimaryActorTick.bCanEverTick = true;

	Capsule = CreateDefaultSubobject<UCapsuleComponent>(TEXT("CAPSULE"));
	Mesh = CreateDefaultSubobject<USkeletalMeshComponent>(TEXT("MESH"));
	Movement = CreateDefaultSubobject <UFloatingPawnMovement>(TEXT("MOVEMENT"));
	SpringArm = CreateDefaultSubobject<USpringArmComponent>(TEXT("SPRINGARM"));
	Camera = CreateDefaultSubobject<UCameraComponent>(TEXT("CAMERA"));

	RootComponent = Capsule;
	Mesh->SetupAttachment(Capsule);
	SpringArm->SetupAttachment(Capsule);
	Camera->SetupAttachment(Capsule);

	Capsule->SetCapsuleHalfHeight(88.0f);
	Capsule->SetCapsuleRadius(34.0f);
	Mesh->SetRelativeLocationAndRotation(FVector(0.0f, 0.0f, -99.0f), FRotator(0.0f, -90.0f, 0.0f));
	SpringArm->TargetArmLength = 400.0f;
	SpringArm->SetRelativeRotation(FRotator(-15.0f, 0.0f, 0.0f));

	static ConstructorHelpers::FObjectFinder<USkeletalMesh> SK_CARDBOARD(TEXT(" / Game / InfinityBladeWarriors / Character / CompleteCharacters / SK_CharM_Cardboard.SK_CharM_Cardboard"));
	if (SK_CARDBOARD.Succeeded())
	{
		Mesh->SetSkeletalMesh(SK_CARDBOARD.Object);
	}

}

// Called when the game starts or when spawned
void AMyPawn::BeginPlay()
{
	Super::BeginPlay();
	
}

// Called every frame
void AMyPawn::Tick(float DeltaTime)
{
	Super::Tick(DeltaTime);

}

void AMyPawn::PostInitializeComponents()
{
	Super::PostInitializeComponents();
}

void AMyPawn::PossessedBy(AController* NewController)
{
	Super::PossessedBy(NewController);
}

// Called to bind functionality to input
void AMyPawn::SetupPlayerInputComponent(UInputComponent* PlayerInputComponent)
{
	Super::SetupPlayerInputComponent(PlayerInputComponent);

}

```


```
// Fill out your copyright notice in the Description page of Project Settings.

#pragma once

#include "Engineminimal.h"
#include "GameFramework/PlayerController.h"
#include "MyPlayerController.generated.h"

/**
 * 
 */
UCLASS()
class QWER_API AMyPlayerController : public APlayerController
{
	GENERATED_BODY()
	
public:
	virtual void PostInitializeComponents() override;
	virtual void OnPossess(APawn* aPawn) override;
};

```

```
// Fill out your copyright notice in the Description page of Project Settings.


#include "MyPlayerController.h"

void AMyPlayerController::PostInitializeComponents()
{
	Super::PostInitializeComponents();
}

void AMyPlayerController::OnPossess(APawn* aPawn)
{
	Super::OnPossess(aPawn);
}
```


현재 MyPawn.cpp에
```
void AMyPawn::PossessedBy(AController* NewController)
{
	Super::PossessedBy(NewController);
}

// Called to bind functionality to input
void AMyPawn::SetupPlayerInputComponent(UInputComponent* PlayerInputComponent)
{
	Super::SetupPlayerInputComponent(PlayerInputComponent);

}
```

부분에 Super::PossessedBy와 Super::SetupPlayerInputComponent(PlayerInputComponent)가 클래스 AActor에 멤버가 없다면서 오류, 고치는 중