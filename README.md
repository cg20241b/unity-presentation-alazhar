[![Open in Codespaces](https://classroom.github.com/assets/launch-codespace-2972f46106e565e64193e422d61a12cf1da4916b45550586e14ef0a7c637dd04.svg)](https://classroom.github.com/open-in-codespaces?assignment_repo_id=16523272)

| **Name**          | **NRP**            |
|-------------------|--------------------|
| Muhammad Danis Hadriansyah  | 5025221239  |
| Davin Fisabilillah Reynard Putra | 5025221137 |
| Muhammad Aqil Farrukh | 5025221158 |
| Alendra Rafif Athaillah | 5025221297 |

Unity VFX Graph - Stylized Smoke Tutorial
https://youtu.be/dPJQuD93-Ks?si=VFJ0oWD72wU10CCm

# Prerequisite
---

First of all we install Visual Effect Graph before we move on to the project

![image](https://github.com/user-attachments/assets/732b78aa-914f-4d0d-93a9-673b2c79d230)

Turn on the Experimental Operators/Blocks

![image](https://github.com/user-attachments/assets/183528a7-4a36-4387-9170-f89ef7e8e85a)

---

# Shader Graph

We rename it SmokeShader_Tut

![image](https://github.com/user-attachments/assets/a567f094-3ef1-4540-95ec-2c6c4ed15a98)

### Inputs (Color, Fresnel Power, Voronoi Scale, etc.) (Left Side):

These variables allow to control for the smoke's appearance (such color and Fresnel effect strength), also Voronoi settings to adjust the pattern of the noise texture that applied to the smoke

### Fresnel Effect:

This Affects for the edges of the smoke to create a glow or soft outline, making it look realistic when light interacts. It is useful for enhancing the visual depth of the smoke and giving it a more ethereal

### Voronoi Noise:

The Voronoi node generates a cellular pattern that mimics turbulent, billowy smoke. It ss modified by the “Scale” and “Speed” inputs to create dynamic and shifting textures that add movement to the smoke.

### Alpha Clip Threshold:

Determines the transparency cutoff, helping to create a smoother, softer edge to the smoke particles, this key is to making the particles blend better into each other, rather than looking blocky or too solid.

### Multipliers and Time Nodes:

As seen as the name, it control the speed and intensity of the noise patterns animation, adding a subtle, continuous flow to the smoke. These elements make the smoke feel alive, as the texture moves over time.

---

# Visual Effect Graph

We rename it vfxgraph_StylizedSmoke_t

![image](https://github.com/user-attachments/assets/5ef597d8-7f95-467f-938c-2c3599d3dbba)

### Spawn System (Top Section in Green):

This section controls the spawning of particles. The "Constant Spawn Rate" determines the frequency of particles generated over time, set to 2 here, which likely means 2 particles per second or another unit of time.

### Initialize Particle (Yellow Box):

This section sets initial properties for each particle, such as position, size, lifetime, and velocity.
Key components:
- Capacity: Defines the maximum number of particles, here set to 1000.
- Bounds Mode: Likely manages particle boundaries for rendering.
- Set Lifetime: Assigns a random lifetime to each particle, making them fade over time.
- Set Velocity: Sets initial movement; randomization here creates a more natural, varied movement for the smoke.
- Set Angle: Controls the initial rotation angle for each particle.
- Set Size: Determines the particle's starting size.

### Update Particle (Orange Box):

This controls properties that change as particles age. It includes attributes like age, size, and opacity, which might be set to gradually fade out, grow, or shrink the particles over their lifespan.

### Output Particle Mesh (Red Box):

The final stage where particles are rendered with a specific shape and material.
- Shader Graph: Uses a shader (e.g., one for stylized smoke) to define particle appearance.
- Size Over Lifetime: Adjusts particle size based on age, creating a more dynamic smoke effect that grows or shrinks over time.

### Other Nodes (Connected to Initialize and Update):

- Sample Curve, Random Number: Adds randomness and variation, ensuring each particle behaves uniquely.
- Age Over Lifetime: Connects particle age to properties like size or opacity to ensure natural fading.
