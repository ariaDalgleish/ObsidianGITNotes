( * ) means not super important
OpenGL states do not change until you change them.

OpenGL is not object oriented

gl - belongs to GL library
Vertex 3 f - function name - f for float
(x,yz) - are floats
glVertx3f(x,y,z) - function format

has own datatype 

float -> GLfloat

void display() {
glClear(GL_COLOR_BUFFER_BIT);  - clear whatever was there.
glBegin(GL_POLYGON); - gives one openGL object to render
glVertex2f(0.5, 0.5); - two floats for polygon vectors
glVertex2f(-0.5, -0.5);
glVertex2f(0.5, -0.5);
glVertex2f(-0.5, 0.5);
glEnd(); - finish render 
glFlush();
}


OpenGL cant do non-convex polygon/concave polygon
Attributes - Drawing Color

glColor3f(GLfloat red, GLfloat green, GLfloat blue)

Point Size
glPointSize(GLfloat size)
size must be greater than 0.0 and by default is 1.0
Width ^

Transparency glColor4fColor ( 0,0,0, Alpha)
0// transparent
1// opaque

Blending 
*Shading, Jagged lines(turn off smooth lines)

Displayig Bitmap text 
