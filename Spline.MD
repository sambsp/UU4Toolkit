## Direction、Tangent、Quaternion etc

Tangent：朝向，没归一化
Direction：归一化的Tangent
Up：与Direction组成ONB的一份子
Right：与Direction组成ONB的一份子
Quaternion：目标点的旋转，必须是选中该点后进行的本地旋转或者插值过来。一条样条线，如果没有对其中的任何一点做过该动作，那么这个值都一样。
