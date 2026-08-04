
- C structs
- what is a particle system
- functions
- starting on snow
- Z buffer
- 3D Particle

### Exercise: Snow Particles

1. Add a typedef struct for a simple particle
2. Write a test function in the template that creates a particle struct at a known position and draws it as point primitive - call this function in the **display** function.
3. If works then move on to defining the fixed length array of particles that is your particle system.
4. Add a spawn method that takes the first inactive particle in the array and initializes the values of the variables in that particles struct.
5. Add an update method that updates the values of the active particles in the system - test it by calling it in the think() function in the template.

Functions: 
1. **Spawn** a number of new particles
2. **Update** the state of all active particles in the system
3. **Draw** all active particles in the system

Particle phases:
1. Spawning
	- New particles are spawned
	- Each particle is assigned its own initial, often randomly determined, attribute values.
2. Particle dynamics
	- particles in the system are moved/transformed (updated) by varying the attributes of each particle over time. Ex:
		- A fire particle might get darker over time as it moves away from the center of ignition and becomes colder
		- A snowflake might become more transparent and smaller as it falls to the group and gets warmer.
3. Extinction
	- Each particle usually has attributes dealing with time usually (age):
		- Age - time its been alive measured as number of frames since it was spawned
		- lifetime - maximum time it can live in number of frames
	- Options dealing with ectinction:
	- if age > lifetime then -> in our case we can use the ground height to either deactivate or recycle our snow (keep active but update its location and attributes)
		- Particle is destroyed
		- Particle is set to inactive but kept in the system for future reuse
		- Particle is recycled by resetting its attributes to suitable, often random, values and kept active
	- Other events:
		- Out of Bounds - the particle moves out of the viewing area of the scene and cannot re-enter it
		- Hitting the ground - particle hits the ground and can no longer be seen
		- Some other attribute reaches its limit - e.g. a snow particle becomes fully transparent
	- We can use the ground height to either deactivate or recycle our snow (keep active but update its location and attributes).
	