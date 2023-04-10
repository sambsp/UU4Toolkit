## Quaternion:
### Multiple Order

C = A * B

result C yield a value , apply B first, then apply A.

eg:

FVector RandomAngle = ComputeRandomVector(SplineServiceableActorSetter.RotationRandomMin, SplineServiceableActorSetter.RotationRandomMax);
FVector Direction = SplineComponent->GetDirectionAtDistanceAlongSpline(TotalUseLength, ESplineCoordinateSpace::World);
FRotator Rotation = Direction.Rotation();
SplineServiceableActor->SetActorRotation(Rotation.Quaternion() * FRotator::MakeFromEuler(RandomAngle).Quaternion());


## FRotator
### Inside internal

With Pitch, Yaw, Roll. 

eg.
// construct from a vector (this yield a result with Roll = 0, since Roll cannot be evaluated only by one vector)
FVector Tangent = SplineComponent.GetTangentAtDistanceAlongSpline(Distance, ESplineCoordinateSpace::World);
FRotator Rotator = Tangent.Rotation(); // get a Rotator from a vector (that is: what transform matrix can transform FVector::XVector to Tangent direction)

// construct from two vector




