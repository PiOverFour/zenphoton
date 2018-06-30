# hqz exporter for Blender

This Blender add-on allows exporting frames, to render with hqz.

## Installation
* Copy this folder to your [configuration directory](https://docs.blender.org/manual/en/dev/getting_started/installing/configuration/directories.html) in the following locations, with xx being your version of Blender:
  * On Linux, `~/.config/blender/2.xx/scripts/addons/`
  * On Mac, `/Users/$USER/Library/Application Support/Blender/2.xx/scripts/addons/`
  * On Windows, `%USERPROFILE%\\AppData\\Roaming\\Blender Foundation\\Blender\\2.xx\\scripts\\addons`

## Usage

This exporter translates Blender's 3D data to a format usable by hqz. The format is the json file described in hqz's [readme](../../README.md).

Export happens in the *HQZ Exporter panel*, in the render properties.
* **hqz binary path**: the path to the hqz executable. This is useful if you choose to use the *[Export render script](#render_script)* option.
* **Export filepath**: the path to where files will be written
* **Debug**: this strips the json file from newlines, enabling the use of the *wireframe.html* simple viewer.

* **Image settings** and **Stopping conditions**: please refer to hqz's [readme](../../README.md) for more information.

* **Export normals**: hqz can optionally use vertex normal information to calculate where a ray is bounced. This option uses normals in Blender, as visible in the viewport from the [mesh display panel](https://docs.blender.org/manual/en/dev/modeling/meshes/mesh_display.html#normals). It is especially useful for caustics rendering.
* **Invert normals**: inverts exported normals.

* **Export animation**: creates one hqz file for each frame in Blender's render frame range.

### Lights

The settings for a selected lamp object can be found in the *HQZ Lamp* panel, in the Data properties. They match hqz's light options pretty closely, except that the *Polar angle* and *Polar distance* settings are used only for spot objects, using the *Size* in the *Spot Shape* panel.

* **Light Start** and **Light End** may be used to define an area around the lamp from which the light is emitted. You can use it to emit light from a disk if Light Start equals 0.0, or from a ring otherwise. The values are in camera space, i.e. a value of 1.0 means the ring or disk's diameter will occupy the whole vertical dimension.

* **Energy** is the amount of energy emitted from the lamp. Higher values result in brighter light.
* **Spectral light** uses a frequency in nm, randomly chosen between **Spectral Start** and **Spectral End**.
* If **Spectral light** is not used, you may choose a color, which will be approximated to a spectral value on export.
* A black, grey or white color will result in pure white light.


### Materials

hqz can use per-edge materials. In Blender, these materials are defined per-object. They use the same settings as hqz, with a terminology more in line with Cycles's. The settings are found in the Material properties.
* **Diffuse** reflects or refracts light in any direction, regardless of normal.
* **Specular** (hqz's *reflection*) is basically a mirror: light is reflected according to surface normal and incident angle.
* **Transmission** lets the light pass through straight on. Light is not refracted (does not change direction).


© 2014-2018 Damien Picard
