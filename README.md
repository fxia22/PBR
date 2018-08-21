# Physically Based Rendering
(c) 2017 -- 2018 Michał Siejak

An implementation of physically based shading model & image based lighting in various graphics APIs.

![Screenshot](https://raw.githubusercontent.com/Nadrin/PBR/master/data/screenshot.jpg)

API         | SLOC | Implementation status
------------|------|----------------------
OpenGL 4.5  | 504  | Done
Vulkan      | 1839 | Done
Direct3D 11 | 694  | Done
Direct3D 12 | 1240 | Done

## About

The goal of this project is to showcase the use of various modern graphics APIs and to provide a clear side-by-side comparison of them.
I believe that an implementation of physically based shading is a sufficiently non-trivial use case for that comparison to be useful.

Each implementation is completely self contained within a single source/header pair residing directly in ```src``` directory.
The coding style is mostly procedural ("C with classes") using simple POD structs for grouping related data together.
This was done for simplicity, readability, and to not impose any particular renderer design/organization.

Shared functionality (loading of images & 3D models, application event loop & entry point, misc utility functions)
can be found in ```src/common``` directory.

Please note that it was not my goal to try to come up with the most efficient/optimized use of each API. The rendered scene is very simple anyway
(only handful of drawcalls, mostly static data), and when in doubt I tried to refrain from using "clever" tricks and went for simple solutions.

Shaders are heavily commented because there's where interesting stuff happens. :)

## Building

### Windows

#### Prerequisites

- Windows 10 or Windows Server 2016 (x64 versions)
- Visual Studio 2017 (any edition)
- Relatively recent version of Windows 10 SDK
- [LunarG Vulkan SDK](https://vulkan.lunarg.com/sdk/home)

#### How to build

Visual Studio solution is available at ```projects/msvc2017/PBR.sln```. After successful build the resulting executable
and all needed DLLs can be found in ```data``` directory. Note that precompiled third party libraries are only available
for x64 target.

### Linux

Coming soon.

## Running

Make sure to run from within ```data``` directory as all paths are relative to it. API to be used can be specified on the command line
as a single parameter (```-opengl```, ```-vulkan```, ```-d3d11```, or ```-d3d12```). When run with no parameters ```-d3d11``` is used
on Windows, and ```-opengl``` on other platforms.

### Controls

Input        | Action
-------------|-------
LMB drag     | Rotate camera
RMB drag     | Rotate 3D model
Scroll wheel | Zoom in/out
F1-F3        | Toggle analytical lights on/off

## Bibliography

This implementation of physically based shading is largely based on information obtained from the following courses:

- [Real Shading in Unreal Engine 4](http://blog.selfshadow.com/publications/s2013-shading-course/karis/s2013_pbs_epic_notes_v2.pdf), Brian Karis, SIGGRAPH 2013
- [Moving Frostbite to Physically Based Rendering](https://seblagarde.wordpress.com/2015/07/14/siggraph-2014-moving-frostbite-to-physically-based-rendering/), Sébastien Lagarde, Charles de Rousiers, SIGGRAPH 2014

Other resources that helped me in research & implementation:

- [Adopting Physically Based Shading Model](https://seblagarde.wordpress.com/2011/08/17/hello-world/), Sébastien Lagarde
- [Microfacet Models for Refraction through Rough Surfaces](https://www.cs.cornell.edu/~srm/publications/EGSR07-btdf.pdf), Bruce Walter et al., Eurographics, 2007
- [An Inexpensive BRDF Model for Physically-Based Rendering](http://igorsklyar.com/system/documents/papers/28/Schlick94.pdf), Christophe Schlick, Eurographics, 1994
- [GPU-Based Importance Sampling](https://developer.nvidia.com/gpugems/GPUGems3/gpugems3_ch20.html), Mark Colbert, Jaroslav Křivánek, GPU Gems 3, 2007
- [Hammersley Points on the Hemisphere](http://holger.dammertz.org/stuff/notes_HammersleyOnHemisphere.html), Holger Dammertz
- [Notes on Importance Sampling](http://blog.tobias-franke.eu/2014/03/30/notes_on_importance_sampling.html), Tobias Franke
- [Specular BRDF Reference](http://graphicrants.blogspot.com/2013/08/specular-brdf-reference.html), Brian Karis
- [To PI or not to PI in game lighting equation](https://seblagarde.wordpress.com/2012/01/08/pi-or-not-to-pi-in-game-lighting-equation/), Sébastien Lagarde
- [Physically Based Rendering: From Theory to Implementation, 2nd ed.](https://www.amazon.com/Physically-Based-Rendering-Second-Implementation/dp/0123750792), Matt Pharr, Greg Humphreys, 2010
- [Advanced Global Illumination, 2nd ed.](https://www.amazon.com/Advanced-Global-Illumination-Second-Philip/dp/1568813074), Philip Dutré, Kavita Bala, Philippe Bekaert, 2006
- [Photographic Tone Reproduction for Digital Images](https://www.cs.utah.edu/~reinhard/cdrom/), Erik Reinhard et al., 2002

## Third party libraries

This project makes use of the following open source libraries:

- [Open Asset Import Library](http://assimp.sourceforge.net/)
- [stb_image](https://github.com/nothings/stb)
- [GLFW](http://www.glfw.org/)
- [GLM](https://glm.g-truc.net/)
- [D3D12 Helper Library](https://github.com/Microsoft/DirectX-Graphics-Samples/tree/master/Libraries/D3DX12)
- [glad](https://github.com/Dav1dde/glad) (used to generate OpenGL function loader)
- [volk](https://github.com/zeux/volk) (meta loader for Vulkan API)

## Included assets

The following assets are bundled with the project:

- "Cerberus" gun model by [Andrew Maximov](http://artisaverb.info).
- HDR environment map by [Bob Groothuis](http://www.bobgroothuis.com/blog/) obtained from [HDRLabs sIBL archive](http://www.hdrlabs.com/sibl/archive.html) (distributed under [CC-BY-NC-SA 3.0](https://creativecommons.org/licenses/by-nc-sa/3.0/us/)).
