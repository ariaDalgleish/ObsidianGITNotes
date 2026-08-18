Notes

3D object with animations.
Rotate function. All objects have their own animations.

Top and following will be affected. 
When bird moves the whole bird - all parts - will transform together.

Represent as a tree to show the relationship between the different parts.
Inheritance from different rotations and transforms.
For a robot arm: Base -> lower arm -> upper arm.
Parts connected at the joints.

Base rotates independately
	Rotation of base
Lower arm attached to baase (inherits base)
	Position depends on position of base, must also translate relative to base and rotate about connecting joint
Upper arm attached to lower arm (inherits lower arm)

Character main.

Needs propeller, feet. 
Features- Bubbles should always come from mouth.
