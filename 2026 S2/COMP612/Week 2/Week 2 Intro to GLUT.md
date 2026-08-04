 
Inputs 
Physical properties - mouse, keyboard, touch pad, joystick
Logical properties - what is returned to the application program via API. A screen position, an object identifier etc.

Input Events - input device - trigger generates an event - event has an associated measure. Measures are parameters: mouse pos, button state...
xx
To handle events with OpenGL we use GLUT. 
### GLUT 
Event types:
- Window
	- Resize, expose, iconify
- Mouse
	- Click one or more buttons
- Motion
	- Move mouse
- Keyboard
	- press a key, 
	- release a key (only in freeglut not GLUT)
- Idle
	- nonevent
	- define what should be done if no other event is in queue
	- **how we do animation**

Each type of event is assigned a callback function:
``` glutDisplayFunc(display);```
When an event occurs, the appropriate callback function is executed. 
Last line in main.c for GLUT application must be 
```glutMainLoop ();``` %%Puts the program in an infinite event loop

%%Callback functions:
```glutDisplayFunc
glutMouseFunc //handles mouse buttons
glutMotionFunc //handles mouse motion with buttons pressed
glutPassiveMotionFunc //handles mouse motion with NO button pressed

glutReshapeFunc //handles a window resize

glutKeyboardFunc (key) // handles a keyboard key press
key(unsigned char key, int x, inty) 
//recieves the ASCII code of the keyboard letter and the mouse location at the time the letter is pressed.
glutKeyboardUpFunc (key) //freeglut - key release

//Exit application if Q or q is pressed:
void key(unsigned char key, int x, int y){
	if( key == 'Q' || key == 'q')
		exit(0);
}

glutSpecialFunc //handles a keyboard special key press
glutSpecialUpFunc 

glutIdleFunc //is called when no other event is happening and used for animation
```
You pass your functions to the callback functions above. When an even happens, the callback function will run your function.

Keyboard keys: 
Function key 1: GLUT_KEY_F1
Up arrow key: GLUT_KEY_UP
example: if(key == GLUT_KEY F1 ......)
Callback function: glutSpecialFunc

Check if one of the modifiers is depressed by ```int glutGetModifiers();```
Which might return: 
GLUT_ACTIVE_SHIFT
GLUT_ACTIVE_CTRL
GLUT_ACTIVE_ALT
glutGetModifiers rountine may only be called within a keyboard or mouse callback.

basicKeys.c 
1. Disable key repeat in the main() function 
```// Disable key repeat (keyPressed or specialKeyPressed ony be called once when a key is first pressed). 
   glutSetKeyRepeat(GLUT_KEY_REPEAT_OFF); 
```
2. Need to tell window to redraw
``` // you may not need to worry about it too much, because this function will be called in think() function anyway.The next frame updates your Changes
	if (sceneChanged) glutPostRedisplay();
```
- Comment line out - what happens? Try clicking in the window or reshaping it, what happens?

#### Mouse clicks
assign callback 
	glutMouseFunc(mouseButton)
Function will look like this
	myMouseButton(GLint button, GLint state, GLint x, GLint y)
Which is passed by parameters:
	button press
		GLUT_LEFT_BUTTON, GLUT_MIDDLE_BUTTON, GLUT_RIGHT_BUTTON
	state of the button
		GLUT_UP, GLUT_DOWN
	position in window: x, y
	button == 3 for scrolling wheel up, == 4 for scrolling down

To terminate a program using OpenGL you can use a simple mouse callback:
```
mouseButton(GLint button, GLint state, GLint x, GLint y){
	if (button==GLUT_RIGHT_BUTTON && state==GLUT_DOWN)
		exit(0) ;
} //x and y are the person that mouse is clicked.
```

#### Coordinates
GLUT screen window is measured in pixels with the origin at the top-left corner. However, OpenGL uses a 2D drawing coordinate system, which increases from the bottom-left.
- you must invert the y coordinate returned by the mouse callback.
```
openGL_Y = windowHeight - GLUT_Y;
```

- 2D Drawing OpenGL coordinates = world coordinates
- GLUT mouse coordinates = window coordinates (in pixels)

To scale coordinates correctly from GLUT windows with OpenGL drawing dimensions you must:
- Invert the Y coordinate
- scale the GLUT window coordinates (Mouse input) to match the OpenGL drawing coordinates (for drawing)
- GLUT windows might be 400 by 300
- OpenGL drawing coordinates might be -1.0 to 1.0 (the default) or say 0 to 1.0 because we set them that way in glOrtho2D.

### Animations
Frame Buffer - special memory reserved for storing the current image.
Double Buffering 
- draw into an off-screen frame buffer
- flip buffers when drawing is complete
- **Front Buffer**: one that is displayed by not written to
- **Back Buffer**: one that is written to by not displayed.

Program first requests double buffer in main.c
```
glutInitDisplayMode(GLUT_RGBA | GLUT_DOUBLE | GLUT_DEPTH)
```
Buffers swap at end of display callback
glFlush is carried out by glutSwapBuffers before it returns
```
void myDisplay()
{
	glClear();
	....
	/* draw graphics here*/
	....
	glutSwapBuffers(); // instead of glFlush()
}
```

Circle equation:
(x - p)^2+(y - q)^2=r^2
To draw a circle you have to find points (x,y) on the curve and draw lines to link points together.

#### Rotate Square .c
Draw a circle in a square then draw 4 points of the square using the points on the circumference of the circle AND increment theta (angle of rotation)
![[Pasted image 20260721130919.png]]

