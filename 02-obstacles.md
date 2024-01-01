# Obstacles
https://github.com/jinyongnan810/UE5-learning/assets/29720903/0876be56-9d22-435d-946c-65f1b40d463c

## Steps
- Add third person avatar
- Create C++ class for moving platform
- Create moving platform blueprint by basing on C++ class


## Tips
### Spawn character at player start or any other specific location
- Delete current character.
- In blueprint dropdown, add GameMode base.
- Set default pawn class to the character.
- Add player start actor. 
- To start at specific location, right click map and play from here.

## Add third person avatar
- Download Stylized Character from marketplace.(Also Unreal learning kit)
- Create Blueprint child class of ThirdPersonCharacter.
- In blueprint of created class
  - set skeletal mesh
  - make Auto possess player to player 0

## Create C++ class for moving platform
- Tools -> create C++ class -> Actor 

### Add properties
```cpp
// EditAnywhere makes it editable in blueprint
UPROPERTY(EditAnywhere, Category = "Moving Platform")
FVector InitialLocation;
UPROPERTY(EditAnywhere, Category = "Moving Platform")
FVector Velocity = FVector(0, 0, 0);
// VisibleAnywhere makes it visible but not editable in blueprint
UPROPERTY(VisibleAnywhere, Category = "Moving Platform")
float DistanceTraveled = -1;
```

### Add functions
```cpp
// define in header
void MovePlatform(float DeltaTime);
void RotatePlatform(float DeltaTime);
float GetDistanceMoved() const; // const means it doesn't change the properties
// define in cpp
void AMovingPlatform::MovePlatform(float DeltaTime)
{
	FVector Location = GetActorLocation();
	DistanceTraveled = GetDistanceMoved();

	if (DistanceTraveled > MoveDistance)
	{
        // shortcut is ulog
		UE_LOG(LogTemp, Display, TEXT("%s Distance Overshoot: %f"), *(GetName()), DistanceTraveled - MoveDistance);
		InitialLocation = InitialLocation + Velocity.GetSafeNormal() * MoveDistance;
		SetActorLocation(InitialLocation);
		Velocity *= -1;
	}
	Location += Velocity * DeltaTime;
	SetActorLocation(Location);
}

void AMovingPlatform::RotatePlatform(float DeltaTime)
{
	// FRotator CurrentRotation = GetActorRotation();
	// CurrentRotation += RotationVelocity * DeltaTime;
	// SetActorRotation(CurrentRotation);
	AddActorLocalRotation(RotationVelocity * DeltaTime);
}

float AMovingPlatform::GetDistanceMoved() const
{
	return FVector::Dist(GetActorLocation(), InitialLocation);
}
```

## Create moving platform blueprint by basing on C++ class
- Right click c++ class and create blueprint class based on it.
- Drag mesh to blueprint. to give it an appearance.