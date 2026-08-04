
```
#include <freeglut.h>
#include <math.h>
#define PI 3.14159265
// conversion mutliplier for converting from degrees to radians
#define DEG_TO_RAD (PI / 180.0)
GLfloat theta = 0.0; // rotation angle in degrees

void display(void)
{
	// clear the color buffer
	glClear(GL_COLOR_BUFFER_BIT);

	// draw the square 
	glBegin(GL_POLYGON);
	// need to  convert to radians for cos and sin
	glVertex2f(cos(theta * DEG_TO_RAD), sin(theta * DEG_TO_RAD));
	glVertex2f(cos(DEG_TO_RAD * (theta + 90)), sin(DEG_TO_RAD * (theta + 90)));
	glVertex2f(cos(DEG_TO_RAD * (theta + 180)), sin(DEG_TO_RAD * (theta + 180)));
	glVertex2f(cos(DEG_TO_RAD * (theta + 270)), sin(DEG_TO_RAD * (theta + 270)));

	glEnd();
	glutSwapBuffers();
}

void  idle(void)
{
	// update the rotation angle
	theta += 0.02;
	// if done a full turn, reset the angle to 0
	if (theta > 360.0)
		theta -= 360.0;
	// if your theta is an integer, you can do theta %= 360.0

	// force OpenGL to redraw the change
	glutPostRedisplay();
}

void initializeGL(void)
{
	// set background color to be black
	glClearColor(0, 0, 0, 1.0);
	// set the drawing to be white
	glColor3f(1.0, 1.0, 1.0);
	// set window mode to 2D orthographic and set the window size 
	gluOrtho2D(-1.0, 1.0, -1.0, 1.0);
}

void main(int argc, char** argv)
{
	// initialize the toolkit
	glutInit(&argc, argv);
	// set display mode: double buffering, color RGBA
	glutInitDisplayMode(GLUT_RGBA | GLUT_DOUBLE);

	glutInitWindowSize(500, 500);
	glutInitWindowPosition(100, 150);
	glutCreateWindow("Rotating Square");

	// register redraw function
	glutDisplayFunc(display);
	// register idle function callback
	glutIdleFunc(idle);

	initializeGL();
	glutMainLoop();
}
```

to change to rotating dot, simply change GL_POLYGON to GL_POINTS in the display function + add point size
```
void display(void)
{
	glClear(GL_COLOR_BUFFER_BIT);

	//draw dot
	glBegin(GL_POINTS);
	// single point orbiting at radius 1 from the origin
	glVertex2f((GLfloat)cos(theta * DEG_TO_RAD), (GLfloat)sin(theta * DEG_TO_RAD));
	glEnd();
	glutSwapBuffers();
}
```

What happens if we don't call glClear(GL_COLOR_BUFFER_BIT);?
It creates a circle!! It doesn't clear the dot pixels 
![[Pasted image 20260721145012.png]]

### Exercise 8: Create an utility function to draw circles

#### Step 1. What is a triangle fan?

A ```GL_TRIANGLE_FAN``` works by picking one central vertex, then drawing triangles between that center and every consecutive pair of points around the outside. 
To approximate a circle:
1. Place a vertex at the center
2. Walk around a full 360 in small angle steps placing a  vertex at ```(radius * cos(angle), radius * sin(angle))``` 
3. Close the loop by making the last outer point match the first
%% Circle = many-sided polygon%%
Exact same cos/sin math from rotating dot - just calling it a loop instead of once per frame.

#### Step 2. Write the basic function - radius only, centered at (0,0)
```
void drawCircle(GLfloat radius)
{
	int numSegments = 100; // more segments = smoother circle

	glBegin(GL_TRIANGLE_FAN);
	glVertex2f(0.0f, 0.0f); // center point first

	for (int i = 0; i <= numSegments; i++)
	{
		GLfloat angle = 2.0f * (GLfloat)PI * (GLfloat)i / (GLfloat)numSegments;
		glVertex2f(radius * (GLfloat)cos(angle), radius * (GLfloat)sin(angle));
	}

	glEnd();
}
```
- Loop runs <= numSegments, not < numSegments . This makes the last point overlap the first (no gap).
- ```2.0f * PI * i /numSegments``` sweeps full circle across numSegments steps - this is radians directly, not degrees, so no DEG_TO_RAD needed.
- Radius is a parameter, so ```drawCircle(0.5f)``` and ```drawCircle(0.2f)``` give different-sized circles for free.

#### Step 3. Draw a few circles at different sizes and locations
Why push/pop matrix? ```glTranslatef``` permanently shifts the coordinate system for everything drawn after it, until you undo it. Push matrix and Pop matrix save and restore that coordinate system so each circle's translation doesn't stack onto the next one.

```
void display(void)
{
	glClear(GL_COLOR_BUFFER_BIT);

	glPushMatrix();
	glTranslatef(-0.5f, 0.5f, 0.0f);
	drawCircle(0.2f);
	glPopMatrix();

	glPushMatrix();
	glTranslatef(0.5f, 0.5f, 0.0f);
	drawCircle(0.3f);
	glPopMatrix();

	glPushMatrix();
	glTranslatef(0.0f, -0.4f, 0.0f);
	drawCircle(0.15f);
	glPopMatrix();

	glutSwapBuffers();
}
```

#### Step 4. Adding RGBA color as parameters so each circle call can specify its own color.

1. Add 4 Gfloat parameters to drawCircle for red, green, blue, alpha
2. Call glColor4f(r, g, b, a) **inside** the function right before glBegin... 
3. Update the prototype to match the new parameter list
4. Update every existing call site (display()) to pass color values since the function signature changed.
