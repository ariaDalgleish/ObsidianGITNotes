
Shading.
Consider light sources, material properties, location of viewer, surface orientation.

Global rendering vs local rendering
Global using global cal
OpenGL using local rendering system

Light-Material interaction
White light hits red surface, red is reflected. Specular is where the brightest light hits, it should be the same color as lighting color if surface is smooth enough.

Types of lights:
Point
	Modelled  with position and color, emanates in all directions
SPot
	Torch, shooting in one direction
Parallel light/Directional light
	Only giving vector of the direction the light is shooting to 
	An infinite distance away
Ambient light
	Background light

Light distance
Rough surface light will reflect in all directions,

Ideal reflector is perfectly smooth. 
	
Calculate reflections:
	Normal (n) is determined by the cross product of two vectors on the surface
	Reflection vector ( r) is r = 2(1 . n) n -1
	l.n = cos  // think as the projection length of vector/ on vector n (n length is 1)
	2(l.n) // double the projection length // its not a vector

# Steps for OpenGL lighting
## Enable lighting
 Shading calculations are enabled by
	`glEnable(GL_LIGHTING);`
Must also enable each light source individually (0 to 7)
	`glEnable(GL_LIGHT0);`
Dont use `glColor()`
YOu need to set material properties for each surface. Or enable `glColor()` by `glEnable(GL_COLOR_MATERIAL)`
`glColor()` will still affect textures
## Specify the shading mode (flat or smooth)
- Shading calculations done for each vertex
### Normal for polygon
`n = (p(2) - p(1)) x (p(0) - p(1))`

Right - hand rule:
	Wrap your fingers around the polygon in the order the vertices are defined
	The direction your thumb is pointing is the direction of the normal.
Smooth shading in OpenGL
##  Specify surface normal
Set each normal wil `glNormal*()`
	`glNormal3f(x,y,z)`
	`glNormalfv(n)` // where n is a vector
Unit normals
## Specify lights
What color 
```
GLfloat diffuse[] - {1.0, 1.0, 1.0, 1.0} // leave as 1 on end
GLfloat ambient
GLfloat specular
glLightv(GL_LIGHT0, GL_AMBIENT, ambient);
```

Directional light is 0,0f

Point light in all directions is lightPosition
`GLfloat lightPosition[] = {x, y, z, 1.0f};` // W component is 1.0f

Spot lights give angle position is point, direction is a vector
Make spot light function 

Global Ambient light
`glLightModelfv (GL_LIGHT_MODEL_AMBIENT, gloabalAmbient);` Not affected by distance
## Specify surface material properties
Instead of colors you specify materials for each surface
specular is light
ambient is dark (shadow color) 
diffuse is surface color
set material properties with `glMaterialv() and glMaterialf()`
``glMaterialv(GL_FRONT, GL_AMBIENT, ambientMat);

Transparent material
propertials RGBA values the 4th value is the alpha.

Shine = 100.0 // alpha term

Shade of front faces only works for solid objects. Back faces included for hollow objects.
Shade both sides `GL_FRONT_AND_BACK` when calling `glMaterial`


You can have either linear or squared (quadratic) attenuation. or none (default)

Sphere normals. r is radius
Normal is (x/r, y/r, z/r) 

Lighting is different depending on how many polys, vertices. 