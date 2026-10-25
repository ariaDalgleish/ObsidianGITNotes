Jogl and JavaCV
Install NetBeans OpenGL plugin

In java GL: GL.GL_SMOOTH
in C: GL_SMOOTH

OpenCV is open source for computer vision. Taking the OpenCV and taking to run into Java.
Image processing is taken the image and doing something to the image or pixels.
Computer Vision is getting the image and using mathematic skills to 

Plan for project. Need to make progress!!!!!

1. Scene settings check list - write up specifications and plan for the scene
2. Seabed
3. Octopus
4. Lighting

**DO NOT DELETE TEMPLATE COMMENTS**
## Basic Scene Settings
Ensure that:
- Using depth buffering and double buffering for your project.
- you are using a perspective projection and handling window reshape properly.
**Must** identify the scale of your objects and environment and mapping of real-world units to openGL units. e.g.: if moving 1.0 units in the application what does this map to in the "real" world? 1 meter, 1cm? Thinking about this now will make the positioning and animation of your objects (including the camera) in the environment, and the projection parameters, easier to implement. This scale **must** be detailed and rationalised and the start (logbook: "1.0 GL units - 1 meter") based on your chosen scene.

LOG:
**Scale: 1.0 GL unit = 1 metre.**  
I'm following the Unity convention (1 unit = 1 m), where a typical human player is 1.6–2.2 m tall, so measurements in the scene can be checked against real life. My player-controlled character is an octopus, not a human, and is much smaller than a person, so its body is 1 m across (radius 0.5). Everything else is scaled to it: a wingspan of about 2.5 m (comparable to a large eagle), a 1 m tail, 5 cm eyes and 0.25 m propeller blades. It flies at about 6 m/s, roughly 22 km/h, and turns at about 60° per second. The camera sits about 5 m from the bird, so its full wingspan fits within a 60° field of view. The near and far planes are set in metres to suit this scale.
- **Body:** 1 m across.
- **Wingspan:** about 2.5 m.
- **Tail:** 1 m.
- **Eyes:** 5 cm.
- **Propeller blades:** 0.25 m.


## Seabed
Construct a function that creates a grid of squares on the X-Z plane centred at the origin. The size of the grid and the squares that make up the grid should be easy to change. The template includes a key handler that toggles global variable `renderFillEnabled `whenever the `'l'` key is pressed, to allow the user to toggle between the scene been drawn wire-framed or filled. To make this work, you **must** draw your scene wire-framed when `renderFillEnabled `is 0 and filled when `renderFillEnabled` is 1.
Set the clear color to be a suitable color for sea ground.

seabed 5 m below the origin
the grid is `SEABED_SQUARES_PER_SIDE` squares of `SEABED_SQUARE_SIZE` metres each. To make it bigger but with the same square size, change only the count. The grid is subdivided into many small squares because OpenGL lights each vertex, so many small squares light more smoothly than a few big ones.
## Octopus.

Right now bird needs to change to octopus.

Bird Parts:
- Body
- Left eye
- Right eye
- Beak
- Tail
- Left wing
- Right Wing
- Propeller

Octopus Parts:
- Body 
	- shape same as bird
- Left Eye 
	- Same
- Right Eye
	- Same
- Mouth 
	- Same pos, shape is a torus laid veritcally, flat on front of body.
- Legs (Eight spheres)
	- Eight spheres on bottom of body 
- Tail is the Propeller
	- Left and Right - same as bird, Pos is on back of body instead of on top.
- Bubbles? 
	- Where beak is - extra feature 

Key Mapping (Include last page of logbook)

| Key             | Function                             |
| --------------- | ------------------------------------ |
| Up arrow key    | Increase altitude (heave)            |
| Down arrow key  | Decrease altitude (heave)            |
| Left arrow key  | Turn left (yaw)                      |
| Right arrow key | Turn Right (yaw)                     |
| "w"             | Switches Move forward (surge) on/off |
| "a"             | Strafe left (sway)                   |
| "d"             | Strafe right (sway)                  |
| "b"             | Bubble (toggle bubbles)              |
All movement controls must work simultaneously. 
*Hint: Use `gluLookAt `to focus on the octopus and set the camera's eye position relative to the octopus's current location. For the camera to track the octopus you need to manage two things: the camera eye position must follow the octopus in space, and the camera must face toward the octopus. As the octopus rotates, the camera should rotate with it - so if the camera looks along the back toward the front, it should stay looking along the back to front as the octopus turns left or right.*

Camera moves relative to the octopus so camera is following octopus but `camera.y` is a little bit higher than `octopus.y`. Octopus' functions should be set up so it can easily be translated (moved) by using its variables (speed, heading, location etc.) and GL matrix transforms.
Octopus **should not** be able to move below the seabed or move until the feet are rotating but turning (yaw). It should start in the first instance with its feet and propeller switched off.


## Lighting 
1. Include an animated spotlight
2. One directional or point light source with appropriate position, ambient, specular, and diffuse levels ( a point light could simulate sun light).
All objects must be affected by lighting. Include screenshot of illustration of both lightings in logbook as appendix 1.