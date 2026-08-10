
Screen-space (0-800, 0-800 with origin at bottom-left) or Clip-space coords (-1 to 1)?

**Screen-Space (0 to window width/height)**
- ✅ **Best for:**
- UI elements (buttons, HUD, text)
- Mouse-tracking effects (like your following eyes)
- Pixel-perfect positioning
- Window-relative games/apps
  
- ❌ **Problems when:**
- Window resizes (coordinates break unless you recalculate)
- You want resolution-independent graphics
- Scaling up/down your scene
  
**Clip-Space (-1 to 1)**
- ✅ **Best for:**
- Physics simulations (particles, gravity)
- Mathematical scenes that should scale with window
- Resolution-independent rendering
- 3D graphics (natural coordinate space for OpenGL)
  
- ❌ **Problems when:**
- Mouse input (need conversion: -1 to 1 from pixel coords)
- UI elements feel awkward
- Window resizing (particles stay in -1 to 1, never fill whole screen)

For a **snow scene with following eyes**, screen-space is actually the better choice because:
1. **Eyes need pixel-perfect positioning** relative to the window
2. **Particles falling down** work in screen-space—they naturally fall from top (y=800) to bottom (y=0)
3. **Mouse tracking** is already in screen coordinates

If you resize the window, both the eyes and particles should scale proportionally, which happens automatically with screen-space as long as you update particle spawn/death coordinates based on `windowHeight` and `windowWidth`.

ToDo:

H