# fea_osl
OSL shaders

### General Shader Installation
- Download the [latest release](https://github.com/p-groarke/fea_osl/releases/latest) and unzip.
- Copy the `FeaOSL` folder in your OSL directory. For example, `C:\Program Files\Autodesk\3ds Max 2022\Plugins\OSL`.
- You may also copy the `.osl` and `.ui` files directly, if you do not want a `FeaOSL` sub-directory in your Maps menu.
- You should see the shader in your material editor drop-down on next 3dsMax launch.


## SimpleOcean

![Simple Ocean Ex1](doc/simpleocean_test1.png?raw=true "Test Render 1")
![Simple Ocean Ex2](doc/simpleocean_test2.png?raw=true "Test Render 2 - Simple Foam Shading")
[![Play Demo](doc/simpleocean_play.png)](https://www.youtube.com/watch?v=YeeyUybFUvM "Play Demo & Guide")

SimpleOcean is a Gerstner Wave implementation to simulate ocean vector displacement. It isn't highly complex, but should do the job when you need a quick & dirty ocean. The shader outputs a main vector displacement map and multiple utility maps, like foam maps, above sea map, etc.

### Getting Started
- Connect the main output to **Arnold Properties Vector Displacement** map input.
  - This is important, as the shader outputs vector displacement which isn't compatible with other displace inputs (like Physical Material, Displace modifier, etc).
- Use Active Shade to see the results.

### Known Issues
- **Animation doesn't work!**
  - There is currently a bug with the Arnold Properties Displacement map input. Once that is fixed I can test animation.
- When using very large maps, the ocean generation can be slow.
- Some of the hashing options aren't ideal and produce banding.

### Material Settings
The following should create a decently shaded ocean. For best results use and HDRI environment. You can place a large dark plane underneath the ocean, which improves realism a little bit. A more in-depth video is coming to discuss node details.

#### Arnold Properties
- Displacement > Enable
- Displacement > Bounds pads : 1.0
- Displacement > Use Map
- Connect Displacement output to that map.

Optional, Auto-Bump replaces subdiv and is much faster.
- Subdivision > Catclark
- Subdivision > Iterations : about 2-3

#### Arnold Standard Surface Setup
- Diffuse : 0
- IOR : 1.33
- Specular : ~1
- Transmission : 1
- Transmission Color : ~blue
- Transmission Depth : 0.1+
- Scatter : White (or other color)
- Scatter Anisotropy : 1
