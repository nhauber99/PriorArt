# PriorArt
Here I'm just documenting any ideas of anything technical that come to mind, in order to hinder anyone else from filing patents with the same idea.

# Photometric stereo scanner
Photometric stereo is a method to obtain information about material which describes the 3d shape of it and/or in what way it reflects light (e.g. solving for the parameters of a "Spatially Varying Bidirectional Reflectance Distribution Function"). Note: not every feature of the scanner is related to photometric stereo (like obtaining translucency values by using a backlight on the sample to be scanned). The sample to be scanned can be anything that reflects, emits or transmits light and can range from hot steel slabs to liquids (other examples are fabrics, leather, plants, rocks, skin, hair and so on). Any light mentioned is not necessarily visible and may consist of other wavelengths (like ultraviolet/infra red/...).
Several features, most of which are optional, can be combined to capture data needed to calculate said information:
* one or more cameras or equivalent devices which image the transmission of light through or reflection of light off a material to be scanned. these cameras can either be moved by motors or are fixed in a static place relative to the material or to the leds.
* one or more broadband point lights (like white leds), which reflect off the material and a camera takes a monochromatic or multispectral/colored images (with filters in front of it, either a CFA or with a filter wheel)
* one or more colored/spectrally variable point lights (like colored leds/lasers or broadband lights with filters in front of them) which reflect off the material and a camera takes a monochromatic or multispectral/colored images (with filters in front of it, either a CFA or with a filter wheel), having colored light reflecting off the material and filtering it afterwards can be used to obtain information about photolumineszence of the material. Colored light may also be produced by controlling the angle of incidence of broadband light (for example by moving the light source or moving mirrors/lenses which reflect/refract it) to a prism (or equivalent objects like a diffraction grating, which bends or reflects the light at an angle dependent on its wavelength) and the resulting "rainbow" of light can then be mostly filtered by an opening letting only part of the light through.
* one or more linear lights (either broadband/white or colored/spectrally variable) which reflect off the material and a camera takes a monochromatic or multispectral/colored images (with filters in front of it, either a CFA or with a filter wheel), linear light has the advantage, that it greatly improves the quality of a scan of highly glossy materials
* area lights are also possible with the same reasoning as the linear lights
* an area light can be used behind the sample to illuminate it and get translucency/transparency measurements (separating these can be done by using polarized light, more on this later)
* all of the lights mentioned above can be used in combination with a (linear/circular) polarizer in front of them and a linear/circular polarizer in front of the camera. These polarizer will need to either be mechanically rotated or as an alternative liquid crystals can also be used instead, where one can electrically alter the polarization. Using polarizers has the advantage of being able to separate the specular and diffuse reflection of a material (diffuse reflection = 2 * cross polarized image, specular reflection = parallel polarized image - 2 * cross polarized image). The same method can be used to separate translucency and transparency, because any light waves directly going through the material do not change the polarization, while the ones that get scattered (SSS) do change their polarization and are then either partially polarized or unpolarized
* the images to be taken are generally a group of cameras taking an image of the reflection of the light emited by a group of lights, which are either turned on, or modulated to provide a pattern or gradient of the reflected light. The easiest method is having all cameras take an image at once of the relection of a single light. So the maximum total amount of images is the amount of cameras multiplied by the amount of lights (multiplied by the amount of filters, if a filter wheel is used).
* 3d scanners like structured light scanners can be used to aquire a 3d geometry of the sample, but other methods like stereo photogrammetry when using multiple cameras can also be used
* an optical range finder (or a device mentioned in the previous point) can be used to electronically / manually adjust the focus of one or more lenses in front of the cameras
* if a flat sample is scanned special lenses can be used to have the image plane of a camera which sensor isn't parallel to the sample, be parallel to the sample
* the walls of the device may be painted black or made out of a material that reflects little light
* a mobile device may be made by attaching the lights to the legs of the device (comparable to a tripod, but with more legs), with one camera facing down attached on top (and optionally others on the side). The legs could also be made, to be collapsible (again, like a tripod)
* This device may also be attached to a gantry, that can move the device in one to three dimensions (optionally also in more degrees of freedom, in order to rotate the device). This would enable the scanner to scan bigger samples by taking multiple scans of different areas of the sample and merging them to get a scan of the whole sample.
* The scanner may be fully battery operated or be attached to an outlet
* When reducing the weight of the scanner, it can also be made handheld
* By calculating the normals of the sample using the images of the specular reflection, one can compare those to normals calculated from the diffuse reflection of the broadband or colored lights and estimate subsurface scattering parameters. When having the normals of the specular reflection, solving for the subsurface scattering parameters can also be done directly (like via gradient descent), but may be more computationally expensive
* The sample can be attached to a device being able to rotate it, in order to image it from multiple directions (it would also be possible to move the sample in one to three directions, instead of the scanner like mentioned in the last point).
* Aquiring (and separating) multiple reflections of lights in a single image might be done by using one or more cameras fitted with polarization or color filters in front of them (like a CFA or filter wheel) and having multiple polarized and/or colored lights in different positions. A beam splitter may be used for this, in order to use multiple cameras taking images of the same image plane (to increase efficiency, the reflection/transmission characteristics of the beam splitter may be dependent on the polarization of the light or the color of the light (e.g. by using thin film filters)
* Processing of all this information is ideally done by a computer, either on the CPU or GPU.
* The computer may receive the images from the cameras directly or if the cameras can function on their own, the images can first be saved on the storage in the camera, and later transmitted to the computer
* There are several methods for switching the lights on and off, on example is to use MOSFETS paired with daisy chained shift registeres controlled by a microcontroller/computer, this has the advantage that the system is easily scalable. Other forms of communication is also possible like I2C from the microcontroller to an led controller which either controls one or multiple leds.
