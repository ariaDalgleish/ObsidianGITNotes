
CUI stands for character user interface
	Users interact with a computer program by typing commands
GUI graphic user interface
	Allows users to interface with the systems 
UI user interface acts as the bridge

Conversational User Interface (Chatbot)
Gesture User Interface - captures your image, gesture through motion and patterns
Speech recognition 
Brain-Computer Interface (Neuralink) - Brain send connections to computer directly, chip reads your neuron pattern and pings when you want to perform an action.

Abstract Window Toolkit AWT provides the GUI - Java 1.0
Swing is built around AWT

GUI has 3 concepts:
Components: Object the user can see on screen 
Containers: Component that can hold other components
Events

To create a button using a constructor belonging to the Button class.
`JButton b = new JButton("Testing");`
For it to be visible it must be added to a `container` , typically a `frame`

Frame is a window with a title and border, top-level window may also have a menu bar.
Window:
AWT:` java.awt.Frame `
Frame:
Swing: `javax.swing.JFrame`

Using constructor in `JFrame` class:
``JFrame frame = new JFrame ("Title goes here");
`frame.setVisible(true);`

`JFrame` methods:
	Size: `setSize(WIDTH, HEIGHT);`
	Set/get title: `setTitle("Frame Title");`
		`String s=f.getTitle();`
	location: `setLocation(x,y);`
		`setLocation(p:)`
	close option: `setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);`
		exit application when closing the frame
``` Java
JFrame f = new JFrame("Frame Test");
frame.setVisible(true);
f.setTitle("A Simple Frame");

/*Get size of the screen, half of screen width & height, set frame size */
Toolkit kit=Toolkit.getDefaultToolkit();
Dimension screenSize=kit.getScreenSize();
int screenWidth=screenSize.width;
int screenHeight=screenSize.height;
int frameWidth=screenWidth/2;
int frameHeight=screenHeight/2;
this.setSize(frameWidth, frameHeight); 

//f.setSize(300, 200);
//f.setLocation(100,100);
f.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
f.setVisible(true);
```
Component is an abstract class - use polymorphism to extend this class
`KeyListener` - `keypressed` 
`EventListener` interface that all event listener interfaces must extend. 
Provide membership to those classes that implement this.

![[Pasted image 20260819124332.png]]

Button
``` java
JButton button = new JButton("blue");
JtextField tf = new JTextField("Enter your input", 40);
frame.add(tf);
button.addActionListener(new ActionListener(){
	@Override
	public void actionPerfromed(ActionEvent e) {
		System.out.printIn("button is clicked");
	}
});
f.add(button);

MyJframe mjf = new MyJframe("leo");

```

# COMP603/ENSE600 – Lecture 6: Graphical User Interface (GUI) — Summary Notes

## Intro to UI Concepts

- **CUI vs GUI**: CUI = commands typed via keyboard; GUI = interaction through graphical icons/visual indicators (buttons, text fields, etc.)
- Other UI paradigms mentioned: conversational (chatbots), gesture-based, brain-computer interfaces (e.g., Neuralink)

## AWT and Swing

- **AWT (Abstract Window Toolkit)**: provides classes for building GUIs; "Abstract" = runs across multiple platforms by mapping abstract components to platform-specific concrete ones
- **Swing**: more powerful/sophisticated, built on top of AWT; many Swing classes mirror AWT ones (e.g., `JButton` ↔ `Button`)
- **Java Foundation Classes (JFC)** = AWT + Swing + Java 2D → provides consistent UI across Windows/Mac/Linux

## Core GUI Concepts

- **Components**: visible, interactable objects (buttons, checkboxes, etc.)
- **Containers**: components that hold other components
- **Events**: user-triggered actions (key press, mouse click)
- Building a GUI = create components → add to containers → handle events

## Frames

- A **frame** = top-level window with title/border (may have menu bar)
- Classes: `java.awt.Frame` (AWT), `javax.swing.JFrame` (Swing)
- Key `JFrame` methods: `setSize()`, `setTitle()`/`getTitle()`, `setLocation(x,y)`, `setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE)`, `setVisible(true/false)`
- Default frame size is 0×0; screen size can be retrieved via `Toolkit.getDefaultToolkit().getScreenSize()`

## Adding Components

- `Component` = superclass of all GUI elements (buttons, checkboxes, scrollbars, etc.)
- To draw directly: extend `JComponent`, override `paintComponent(Graphics g)` — called automatically
    - Draw string: `g.drawString("text", x, y)`
    - Draw image: `g.drawImage(image, x, y, null)` (image loaded via `new ImageIcon(path).getImage()`)
- Add custom component to frame: `frame.add(new MyComponent())`

## Event Handling

- **General process**: user action → event object created → event source (e.g. button) sends it to registered listener(s) → listener reacts
- **ActionListener interface**: must implement `actionPerformed(ActionEvent e)`
- Attach via `component.addActionListener(listenerObject)`
- **Handling multiple event sources**:
    - _Solution 1_: separate listener class per action (e.g., `ColorAction` parameterized by color)
    - _Solution 2_: single listener checks `event.getSource()` to identify which component fired it
- **3 ways to implement ActionListener**:
    1. Named inner class
    2. Anonymous inner class
    3. Frame itself implements `ActionListener` (`addActionListener(this)`)

## Layout Management

- **JPanel**: lightweight generic container; add components to panel, then panel to frame
- Every container has a default layout manager controlling sizing/positioning; enables graceful resizing
- **BorderLayout**: regions — NORTH, SOUTH, EAST, WEST, CENTER (e.g. `frame.add(component, BorderLayout.SOUTH)`)
- **GridLayout**: arranges components in fixed rows/columns (`new GridLayout(rows, cols)`); fills left-to-right, row by row
- **Other layout managers** (java.awt): `CardLayout` (stacked "cards", one visible at a time), `FlowLayout` (variable-length rows), `GridBagLayout` (flexible alignment, different-sized components)

## Common GUI Components

- **JTextField**: single-line text input; `new JTextField("default", size)`; get text via `.getText()`
- **JLabel**: display-only text, often used to label components; `new JLabel("text", alignment)`; update via `.setText()`
- **JTextArea**: multi-line text input; `new JTextArea(rows, cols)`; lines separated by `\n`
- **JScrollPane**: wraps a `JTextArea` (or similar) to add scrollbars: `new JScrollPane(textArea)`
- **JCheckBox**: togglable box; `.setSelected(true/false)`, `.isSelected()`; needs an `ActionListener`
- **JRadioButton**: mutually exclusive selection within a `ButtonGroup`
    - `ButtonGroup group = new ButtonGroup(); group.add(radioButton);`
- **JComboBox<String>**: dropdown selection; `.addItem()`, `.getSelectedItem()` or `.getItemAt(getSelectedIndex())`
- Many more components exist in Swing — check Java API as needed

## Building GUIs Visually

- IDEs (e.g., **NetBeans Design View**) offer **GUI Builders** — drag-and-drop components, auto-generates code, no need to manually manage layouts
- Reference tutorial: https://netbeans.apache.org/tutorial/main/kb/docs/java/quickstart-gui/

## Outstanding/Advanced Topic

- Slide "How to Transfer Data Between Frames?" shows an example (text field + button submitting to a second frame) but no explicit code/explanation given in these slides — likely covered live in class.