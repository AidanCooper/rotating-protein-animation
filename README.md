# Rotating Protein and Molecule Animations in Blender

![Rotating protein GIF](examples/animations/2wy4_constant_rotation_100quality.gif#center?raw=true "Rotating protein GIF")

This repository provides step-by-step instructions for creating an animation of a rotating protein or molecule in Blender from an imported .pdb file. Examples can be found under [examples/animations](examples/animations).

## Instructions

### Installation
First, the blender-molecular-script addon in [this repository](https://github.com/Pyroevil/Blender-Molecular-Script) must be installed.

1. Download the latest release .zip file from the repository linked above or use the one include in this repository [here](molecular_latest.zip).

2. Open Blender.

3. Go to `File > User Preferences` and select the `Add-ons` tab.

4. Click on `Install Add-on from File...` and select the downloaded .zip file.

5. Under `Categories`, select `Object` and ensure that `Object: Molecular script` is checked.

### Selecting a .pdb file for the animation

Find a .pdb file for a protein or molecule that you would like to animate. These can downloaded from the [RCSB Protein Data Bank](http://www.rcsb.org/).

### Creating the animation in Blender

1. Open a new Blender file and delete the default cube.

2. Import your .pdb file using `File > Import > Protein Data Bank (.pdb)`

3. Zoom out and set the camera view such that it encompasses the entire protein/molecule using `ctrl + alt + numpad0`

![Setting the camera view](screenshots/1_set_camera.png#center?raw=true "Setting the camera view")

4. Reposition the lamp. Half-way between the camera and the centre of the protein/molecule is a good default.

![Repositioning the lamp](screenshots/2_lamp_position.PNG#center?raw=true "Repositioning the lamp")

5. Switch the rendering engine to `Blender Render`.

![Blender Render](screenshots/3_blender_render.PNG#center?raw=true "Blender Render")

6. Set the world hoziron to black and the ambient occlusion to 0.2.

![World settings](screenshots/4_world.PNG#center?raw=true "World settings")

7. Adjust the lamp data energy by selecting the lamp object and going to the `Data` tab in the `Outliner` editor. A value of 10 works well for large proteins, whereas 1 might be appropriate for a small molecule.

8. Save the Blender file.

9. In the `Render` tab of the `Outliner` editor, choose a directory to export your animation to under `Output` and change the file format to 'AVI JPEG'. You can also adjust the quality here.

10. In the `Timeline` editor, change the end frame value to 180.

![End frame value](screenshots/5_frame.PNG#center?raw=true "End frame value")

11. For every atom or stick in the file (I've not found a reliable way to perform this for everything at once), perform the following steps:


  * Set the `Current Frame` to 1.

  * Insert a keyframe under `Animation > Keyframes:Insert > Rotation`.

![Insert keyframe](screenshots/5_insert_keyframe.png#center?raw=true "Insert keyframe")

  * Change the `Current Frame` to 180, and set the object z rotation to 358.

  * Insert another keyframe, as above in step 2.

![Insert keyframe](screenshots/6_insert_keyframe.png#center?raw=true "Insert keyframe")

12. **(Optional but recommended).** If you want your animation to loop smoothly, you need to change the rotation to linear. First, switch the screen layout from `Default` to `Animation`.

![Animation layout](screenshots/7_animation_layout.png#center?raw=true "Animation layout")

The, for evey atom or stick in the file (I've not found a reliable way to perform this for everything at once), select `Rotation` (green background) and go to `Channel > Extrapolation Mode > Linear Extrapolation`.

![Linear extrapolation](screenshots/8_linear_extrapolation.png#center?raw=true "Linear extrapolation")

13. Return to the `Default` layout and start rendering your animation by going to `Render > Render Animation`. Depending on your computer, this could take some time (it is recommended that you have GPU rendering enabled).

### Converting your animation to GIF

Optionally, you can convert your .avi animation to a .gif file.

1. If you don't have `imageio` and/or `ffmpeg` installed, install them via conda using the following commands:

`--conda install -c conda-forge imageio`

`--conda install ffmpeg -c conda-forge`

2. Run the [conversion script](examples/animations/convert.py) in this repository to convert your file (change the final line of the script to point at your .avi file).
