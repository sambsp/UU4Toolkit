## Direction、Tangent、Quaternion etc

方法中有参数需要输入World或者Local，那是因为对应的方法都会给出基于世界坐标的或者基于本地坐标的。因为对于Spline，每个点都可以自由的移动、和旋转，因此都有基于Spline本身的世界坐标，和自身点的本地Transform。

### Tangent：朝向，没归一化。

常用：

//得到一个forward跟Tangent方向一致的旋转Transform，可用来对后续的向量做操作得到在此Transform应用后最后的值。
//比如FVector::XAxis和此Transform得到的结果，就是Tangent归一化后的结果
//因为只有一个向量，所以信息不足，这里的FRotator的Roll部分是0
FVector Tangent = SplineComponent->GetTangentAtDistanceAlongSpline(TotalUseLength, ESplineCoordinateSpace::World);
FRotator Rotator = Tangent.Rotation(); 

### Quaternion：目标点的旋转，必须是选中该点后进行的本地旋转或者插值过来。一条样条线，如果没有对其中的任何一点做过该动作，那么这个值都一样。

常用：
//信息全，因此得到的旋转信息是完整的（相对从Tangent得到的）
FQuat Rotation = SplineComponent->GetQuaternionAtDistanceAlongSpline(TotalUseLength, ESplineCoordinateSpace::World);
SplineServiceableActor->SetActorRotation(Rotation * FRotator::MakeFromEuler(RandomAngle).Quaternion());


### Direction：归一化的Tangent

FVector Direction = target->GetDirectionAtDistanceAlongSpline(Distance, ESplineCoordinateSpace::World);
FVector Right = target->GetRightVectorAtDistanceAlongSpline(Distance, ESplineCoordinateSpace::World);
FVector Up = target->GetUpVectorAtDistanceAlongSpline(Distance, ESplineCoordinateSpace::World);

UWorld* World = GetWorld();

FVector Location = target->GetLocationAtDistanceAlongSpline(Distance, ESplineCoordinateSpace::World);
DrawDebugSphere(World, Location, 0.5, 16, FColor(255, 0, 255), true);

FVector LineStart = Location;
Location += Direction * Offset.X;
if (DrawDebug) {
	DrawDebugLine(World, LineStart, Location, FColor(255, 0, 0), false, 10000, 0, .5f);
}

LineStart = Location;
Location += Right * Offset.Y;
if (DrawDebug) {
	DrawDebugLine(World, LineStart, Location, FColor(0, 255, 0), false, 10000, 0, .5f);
}

LineStart = Location;
Location += Up * Offset.Z;
if (DrawDebug) {
	DrawDebugLine(World, LineStart, Location, FColor(0, 0, 255), false, 10000, 0, .5f);
}


### Up：与Direction组成ONB的一份子

与上类似

### Right：与Direction组成ONB的一份子

与上类似