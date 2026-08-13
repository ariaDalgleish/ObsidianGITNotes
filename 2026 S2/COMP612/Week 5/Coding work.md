
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

## Diagonistics

Additions
1. Essential Variables 
	- Controls:
		- s
		- d
		- q
		- Left click
2. Particle Count
3. Additonal hmmm
	- Current FPS :O
	- Snow spawn rate
	- Snowman coords
	- Frame time :O
4. Design Considerations hrmm
	- Text rendering approach
		- Grey trans background for visibility
		- Render in top-left corner 
		- Temp disable depth test during text rendering
		- No blending needed for solid texxt
	- State management
		- toggle dioga with d key - add to keypresseed
		- Store active particle count in a global 
		- Update particle count string each frame for efficiency
	- Layout Suggesmeet
		- Controls:
		  's' - Toggle snow
		  'd' - Toggle diagnostics
		  'q' - Exit application
		  Left Click - Move snowman
		
		  120/500 active particles
		  Or more compact:
		  [s] Snow  [d] Diag  [q] Quit
		  LClick: Move snowman
		  Particles: 120/500

  Good cause
  Uses OpenGL state management partterns, only renders when enables, minimal per-frame overhead.
Shows both user 
easy yea

 1.  Enable depth testing (you already do this, just keep it)

  /* already in your init() */
  glEnable(GL_DEPTH_TEST);
  glDepthFunc(GL_LESS);          /* default, but be explicit */

  Make sure you clear the depth buffer each frame (you already do):

  glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);

  ---
  2.  Split the particle system into background and foreground arrays

  2.1  Add a second particle array (global, near the existing one)

  /* ----- original particle system (foreground snow) ----- */
  #define MAX_PARTICLES 1000
  static Particle_t particles[MAX_PARTICLES];
  int activeParticleCount = 0;          /* used by diagnostics */

  /* ----- background snow ------------------------------------------------- */
  #define MAX_BACK_PARTICLES 800        /* you can tune this */
  static Particle_t backParticles[MAX_BACK_PARTICLES];
  int activeBackCount = 0;              /* optional – for diagnostics */

  Why two arrays?
  Each array gets its own update and draw routine, letting you decide which one is drawn before the snowman
  (background) and which after (foreground).

  2.2  Give background snow a slight depth offset

  When you spawn a background particle, push it a little farther away from the camera (negative z).
  When you spawn a foreground particle, keep z = 0.

  /* In the spawn function – add a bool isBackground */
  void spawn_particle(Particle_t *p, int isBackground)
  {
      p->position.x = ((float)rand() / RAND_MAX) * windowWidth;
      p->position.y = (float)windowHeight;               /* start at top */
      p->position.z = isBackground ? -0.5f : 0.0f;       /* <-- depth offset */

      /* velocity – same for both layers */
      p->vx = ((float)rand() / RAND_MAX) * 100.0f * particleInitVxScale - 50.0f * particleInitVxScale;
      p->vy = -((float)rand() / RAND_MAX) * 150.0f * particleInitVyScale - 75.0f;

      p->size = ((float)rand() / RAND_MAX) * 3.0f + 1.5f;   /* 1.5‑4.5 px */
      p->age  = 0.0f;
      p->lifetime = 5.0f + ((float)rand() / RAND_MAX) * 10.0f; /* 1‑11 s */
      p->active = 1;
  }

  2.3  Update functions for each layer

  You can keep a single particles_update(float dt) and call it twice, or duplicate it – the simplest is to
  call the same function on each array:

  void update_particles(Particle_t *array, int count, float dt)
  {
      const float gravity = particleGravity * 300.0f;   /* pixels/sec² */
      for (int i = 0; i < count; ++i) {
          if (!array[i].active) continue;

          array[i].age += dt;
          if (array[i].age > array[i].lifetime) { array[i].active = 0; continue; }

          array[i].vy += gravity * dt;
          array[i].position.x += array[i].vx * dt;
          array[i].position.y += array[i].vy * dt;

          /* screen‑space culling (same as before) */
          if (array[i].position.y < 0.0f ||
              array[i].position.x < -100.0f ||
              array[i].position.x > windowWidth + 100.0f)
          {
              array[i].active = 0;
          }
      }
  }

  Call it from think():

  void think(void)
  {
      /* … existing snow‑spawning logic … */

      if (snowOn) {
          /* spawn foreground Snow */
          spawnAccumulator += spawnRate * FRAME_TIME_SEC;
          int toSpawn = (int)spawnAccumulator;
          if (toSpawn > 0) {
              for (int c = 0; c < toSpawn; ++c) spawn_particle(&particles[findInactiveSlot()], 0);
              spawnAccumulator -= toSpawn;
          }
          spawnRate += spawnGrowthPerSec * FRAME_TIME_SEC;
          if (spawnRate > spawnRateMax) spawnRate = spawnRateMax;
      }

      /* ---- update both layers ---- */
      update_particles(particles,   MAX_PARTICLES,   FRAME_TIME_SEC);
      update_particles(backParticles, MAX_BACK_PARTICLES, FRAME_TIME_SEC);
  }

  2.4  Draw functions (again, reuse the same routine)

  void draw_particles(Particle_t *array, int count)
  {
      glEnable(GL_BLEND);
      glBlendFunc(GL_SRC_ALPHA, GL_ONE_MINUS_SRC_ALPHA);
      for (int i = 0; i < count; ++i) {
          if (!array[i].active) continue;
          float t = array[i].age / array[i].lifetime;
          float alpha = 0.8f - t;               /* fade out */
          glColor4f(1.0f, 1.0f, 1.0f, alpha);
          glPointSize(array[i].size);
          glBegin(GL_POINTS);
          glVertex3f(array[i].position.x, array[i].position.y, array[i].position.z);
          glEnd();
      }
      glDisable(GL_BLEND);
  }

  Call them in the correct order from display():

  void display(void)
  {
      /* … clear, background sky, ground … */

      /* 1️⃣  Background snow – drawn FIRST */
      draw_particles(backParticles, MAX_BACK_PARTICLES);

      /* 2️⃣  Snowman (and any other opaque objects) */
      glDisable(GL_DEPTH_TEST);
      drawSnowman(snowmanX, snowmanY, snowmanBaseR);
      glEnable(GL_DEPTH_TEST);

      /* 3️⃣  Foreground snow – drawn LAST */
      draw_particles(particles, MAX_PARTICLES);

      /* 4️⃣  Diagnostics (text) – unchanged */
      drawDiagnostics();

      glutSwapBuffers();
  }

  Result:
  - Any background particle that happens to sit behind the snowman’s geometry gets a larger depth value (z =
  -0.5f) and is discarded by the depth test when the snowman is drawn.
  - Foreground particles (z = 0) are drawn after the snowman, so they always appear on top.
  - Because both layers use the same random spawning, the visual density looks like a single snowfall, but
  you now have true depth ordering.

  ---
  3.  Add the breath‑puff system (warm air that pushes snow)

  Think of this as a third, very small particle system that lives for < 1 second and expands/fades.

  3.1  Globals (near the other particle variables)

  /* ----- Breath puff --------------------------------------------------- */
  #define MAX_BREATH 20
  typedef struct {
      float x, y;          /* world position */
      float vx, vy;        /* velocity */
      float age;
      float lifetime;
      float radius;        /* visual radius */
      float alpha;         /* transparency */
  } BreathParticle;

  static BreathParticle breathParticles[MAX_BREATH];
  float breathTimer = 0.0f;               /* counts up to spawn interval */
  const float BREATH_INTERVAL = 0.8f;     /* seconds between puffs */
  const float BREATH_SPEED  = 150.0f;     /* initial outward speed (px/s) */
  const float BREATH_LIFE   = 1.2f;       /* how long a puff lives */

  3.2  Initialise (init())

  /* zero the breath array */
  for (int i = 0; i < MAX_BREATH; ++i) breathParticles[i].active = 0;
  breathTimer = 0.0f;

  3.3  Spawn a puff (think() – after particle updates)

  void think(void)
  {
      /* … existing snow logic … */

      /* ---- breath timer ---- */
      breathTimer += FRAME_TIME_SEC;
      if (breathTimer >= BREATH_INTERVAL) {
          spawnBreathPuff();
          breathTimer = 0.0f;
      }

      /* ---- update breath puffs ---- */
      updateBreathParticles(FRAME_TIME_SEC);

      /* ---- optional: let breath affect nearby snow ---- */
      applyBreathToSnow(FRAME_TIME_SEC);
  }

  3.4  Helper: find an inactive breath slot

  static int findBreathSlot(void)
  {
      for (int i = 0; i < MAX_BREATH; ++i)
          if (!breathParticles[i].active) return i;
      return -1;   /* full – oldest will be overwritten if you prefer */
  }

  3.5  Spawn function

  void spawnBreathPuff(void)
  {
      int i = findBreathSlot();
      if (i < 0) return;   /* no free slot */

      BreathParticle *b = &breathParticles[i];
      /* spawn from the snowman’s nose/mouth – use the snowman’s head center */
      float headCenterX, headCenterY, headRadiusPx;
      float leftEyeX, rightEyeX, eyeY;   /* we only need the head center */
      getSnowmanEyeGeometry(snowmanX, snowmanY, snowmanBaseR,
                            &headCenterX, &headCenterY, &headRadiusPx,
                            &leftEyeX, &rightEyeX, &eyeY);

      b->x = headCenterX;
      b->y = headCenterY + 0.2f * headRadiusPx;   /* a little below the center */
      b->age = 0.0f;
      b->lifetime = BREATH_LIFE;
      b->radius = 2.0f;                           /* start small */
      b->alpha  = 0.6f;                           /* semi‑transparent */

      /* outward direction – you can make it follow the mouse or a fixed angle */
      float angle = 0.0f;                         /* 0 = straight right */
      b->vx = cosf(angle) * BREATH_SPEED;
      b->vy = sinf(angle) * BREATH_SPEED;

      b->active = 1;
  }

  3.6  Update breath puffs

  void updateBreathParticles(float dt)
  {
      for (int i = 0; i < MAX_BREATH; ++i) {
          if (!breathParticles[i].active) continue;

          BreathParticle *b = &breathParticles[i];
          b->age += dt;
          if (b->age > b->lifetime) { b->active = 0; continue; }

          /* simple outward drift */
          b->x += b->vx * dt;
          b->y += b->vy * dt;

          /* fade & grow */
          float t = b->age / b->lifetime;
          b->radius = 2.0f + 8.0f * t;          /* 2 → 10 px */
          b->alpha  = 0.6f * (1.0f - t);        /* 0.6 → 0 */
      }
  }

  3.7  Draw breath puffs (soft circles)

  void drawBreathPuffs(void)
  {
      if (!showDiagnostics)  /* you could tie visibility to diagnostics or make it always on */
          return;

      glEnable(GL_BLEND);
      glBlendFunc(GL_SRC_ALPHA, GL_ONE_MINUS_SRC_ALPHA);
      glDisable(GL_DEPTH_TEST);      /* puffs are always on top (optional) */

      for (int i = 0; i < MAX_BREATH; ++i) {
          if (!breathParticles[i].active) continue;
          BreathParticle *b = &breathParticles[i];

          glColor4f(0.9f, 0.9f, 1.0f, b->alpha);   /* slight blue‑white */
          int segs = 12;
          glBegin(GL_TRIANGLE_FAN);
          glVertex2f(b->x, b->y);                  /* centre */
          for (int j = 0; j <= segs; ++j) {
              float a = 2.0f * 3.14159265f * (float)j / (float)segs;
              glVertex2f(b->x + cosf(a) * b->radius,
                         b->y + sinf(a) * b->radius);
          }
          glEnd();
      }
      glDisable(GL_BLEND);
      if (glIsEnabled(GL_DEPTH_TEST)) glEnable(GL_DEPTH_TEST);
  }

  Call it from display() after the snowman (or before, depending on whether you want the puff to be
  occluded):

  /* … after drawing snowman … */
  drawBreathPuffs();
  /* … then foreground snow … */

  3.8  Optional: make the breath push nearby snow particles

  Add a simple force that decays with distance:

  void applyBreathToSnow(float dt)
  {
      const float influenceRadius = 80.0f;   /* px */
      const float influenceStrength = 0.4f;  /* how much velocity to add */

      for (int i = 0; i < MAX_BREATH; ++i) {
          if (!breathParticles[i].active) continue;
          BreathParticle *b = &breathParticles[i];

          for (int j = 0; j < MAX_PARTICLES; ++j) {
              if (!particles[j].active) continue;
              float dx = particles[j].position.x - b->x;
              float dy = particles[j].position.y - b->y;
              float distSq = dx*dx + dy*dy;
              if (distSq > influenceRadius*influenceRadius) continue;

              float influence = influenceStrength * (1.0f - sqrtf(distSq)/influenceRadius);
              particles[j].vx += b->vx * influence * dt;
              particles[j].vy += b->vy * influence * dt;
          }
      }
  }

  Call applyBreathToSnow(FRAME_TIME_SEC); right after you update the breath puffs (still inside think()).
