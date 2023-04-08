## Quaternion:
### Multiple Order

C = A * B

result C yield a value , apply B first, then apply A.

eg:

FVector RandomAngle = ComputeRandomVector(SplineServiceableActorSetter.RotationRandomMin, SplineServiceableActorSetter.RotationRandomMax);
FVector Direction = SplineComponent->GetDirectionAtDistanceAlongSpline(TotalUseLength, ESplineCoordinateSpace::World);
FRotator Rotation = Direction.Rotation();
SplineServiceableActor->SetActorRotation(Rotation.Quaternion() * FRotator::MakeFromEuler(RandomAngle).Quaternion());



