# Q2

# Ray Tracer - Assignment 2 (Gamma Correction)

This project extends the ray tracer from Assignment 1 by applying **gamma correction** to the final rendered image using the **Phong illumination model**. It simulates a more realistic appearance by correcting the nonlinear relationship between computed lighting values and how colors appear on a screen.

---

## Table of Contents

1. [Overview](#overview)  
2. [Implemented Features](#implemented-features)  
3. [Project Structure](#project-structure)  
4. [Build and Run Instructions](#build-and-run-instructions)  
5. [Key Code Changes](#key-code-changes)  
---

## Overview

This assignment builds on the basic ray tracer developed in HW1 by adding:

- **Phong shading** with ambient, diffuse, and specular components
- **Shadow ray tracing** for realistic lighting
- **Gamma correction** with γ = 2.2 to simulate how monitors display light

---

## Implemented Features

-  Eye ray generation for each pixel (512 × 512 resolution)
-  Ray-object intersection (plane and three spheres)
-  Phong illumination model
-  Point light at `(-4, 4, -3)` with white light
-  Shadows using shadow rays
-  **Gamma correction with γ = 2.2**
-  Real-time image display using OpenGL

---

## Project Structure

- **Main_Q2.cpp**  
  Main function and rendering loop. This is where gamma correction is applied to the final color output per pixel.

- **Scene.h**  
  Contains the scene setup, intersection tests, shadow checks, and Phong shading calculations.

- **Camera.h**, **Ray.h**, **Plane.h**, **Sphere.h**, **Material.h**  
  Define the core classes for ray generation and scene geometry. Inherited from Assignment 1.

---

## Build and Run Instructions

### Requirements

- Windows 11  
- Visual Studio 2022  
- OpenGL + GLFW + GLEW + GLM  

### Steps

1. Open the `.sln` file in Visual Studio or create a new project and add all provided `.cpp` and `.h` files.
2. Configure include/library directories for:
   - GLFW  
   - GLEW  
   - GLM
3. Build the solution (F7)
4. Run the project (F5)
5. A window should appear displaying the ray-traced image with gamma correction

---

## Key Code Changes

In `Main_Q2.cpp`, gamma correction is applied in the `render()` function as follows:

```cpp
float gamma = 2.2f;

if (scene.intersect(ray, t, color)) {
    // Clamp color values to [0, 1]
    color.r = glm::clamp(color.r, 0.0f, 1.0f);
    color.g = glm::clamp(color.g, 0.0f, 1.0f);
    color.b = glm::clamp(color.b, 0.0f, 1.0f);

    // Apply gamma correction
    color = glm::pow(color, glm::vec3(1.0f / gamma));
}
