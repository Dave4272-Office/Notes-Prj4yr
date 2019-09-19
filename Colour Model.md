# Colour Models
Colour models provide a standard way to specify a particular colour, by defining a 3-D coordinate system, and a subspace that contains all construct-able colours within a particular model. Any colour that can be specified using a model will correspond to a single
point within the subspace it defines. Each colour model is oriented towards either specific hardware (RGB, CMY, YIQ), or image processing applications (HSI).

## The RGB Model
In the RGB model, an image consists of three independent image planes, one in each of the primary colours: red, green and blue. Specifying a particular colour is by specifying the amount of each of the primary components present. The geometry of the RGB colour model for specifying colours using a Cartesian coordinate system is given below. The greyscale spectrum, i.e. those colours made from equal amounts of each primary, lies on the line joining the black and white vertices.

![RGB Colour Model Geometry]()

This is an additive model, i.e. the colours present in the light add to form new colours, and is appropriate for the mixing of coloured light. for example. The following image shows the additive mixing of red, green and blue primaries to form the three secondary colours yellow (red + green), cyan (blue + green) and magenta (red + blue), and white ((red + green + blue).

![RGB Additive Chart]()

The RGB model is used for colour monitors and most video cameras.

## The CMY Model
The CMY (cyan-magenta-yellow) model is a subtractive model appropriate to absorption of colours, for example due to pigments in paints. Whereas the RGB model asks what is added to black to get a particular colour, the CMY model asks what is subtracted from white. In this case, the primaries are cyan, magenta and yellow, with red, green and blue as secondary colours.

![CMY Colour Model Geometry]()

When a surface coated with cyan pigment is illuminated by white light, no red light is reflected, and similarly for magenta and green, and yellow and blue. The relationship between the RGB and CMY models is given by:

> ![](https://latex.codecogs.com/svg.latex?\begin{bmatrix}&space;C\\\\&space;M\\\\&space;Y&space;\end{bmatrix}&space;=&space;\begin{bmatrix}&space;1\\\\&space;1\\\\&space;1&space;\end{bmatrix}&space;-&space;\begin{bmatrix}&space;R\\\\&space;G\\\\&space;B&space;\end{bmatrix})


The CMY model is used by printing devices and filters.

![CMY Subtractive Chart]()

The figure on the left shows the additive mixing of red, green and blue primaries to form the three secondary colours yellow (red + green), cyan (blue + green) and magenta (red + blue), and white ((red + green + blue). The figure on the right shows the three subtractive primaries, and their pairwise combinations to form red, green and blue, and finally black by subtracting all three primaries from white.

![RGB vs CMY Colour Mixing Model]() 

## The HSI Model 
As mentioned above, colour may be specified by the three quantities hue, saturation and intensity. This is the HSI model, and the entire space of colours that may be specified in this way is shown in figure 7. Figure Figure 7: The HSI model, showing the HSI solid on the left, and the HSI triangle on the right, formed by taking a horizontal slice through the HSI solid at a particular intensity. Hue is measured from red, and saturation is given by distance from the axis. Colours on thesurface of the solid are fully saturated, i.e. pure colours, and the greyscale spectrum is on the axis of the solid. For these colours, hue is undefined. Conversion between the RGB model and the HSI model is quite complicated. The intensity is given by:

> ![](https://latex.codecogs.com/svg.latex?I&space;=&space;\frac{R&plus;G&plus;B}{3})

where the quantities R, G and B are the amounts of the red, green and blue components, normalised to the range [0,1]. The intensity is therefore just the average of the red, green and blue components. The saturation is given by:

> ![](https://latex.codecogs.com/svg.latex?S&space;=&space;1)
> S = 1 - min(R,G,B)/I = 1 - 3 * min(R,G,B)/(R+G+B)

where the min(R,G,B) term is really just indicating the amount of white present. If any of R, G or B are zero, there is no white and we have a pure colour. The expression for the hue, and details of the derivation may be found in reference [1].

## The YIQ Model
The YIQ (luminance-inphase-quadrature) model is a recoding of RGB for colour television, and is a very important model for colour image processing. The importance of luminance was discussed in § 1. The conversion from RGB to YIQ is given by:


> ![](https://latex.codecogs.com/svg.latex?\begin{bmatrix}&space;Y\\\\&space;I\\\\&space;Q&space;\end{bmatrix}&space;=&space;\begin{bmatrix}&space;0.299&space;&&space;0.587&space;&&space;0.114\\\\&space;0.596&space;&&space;-0.275&space;&&space;-0.321\\\\&space;0.212&space;&&space;-0.523&space;&&space;0.311&space;\end{bmatrix}&space;\cdot&space;\begin{bmatrix}&space;R\\\\&space;G\\\\&space;B&space;\end{bmatrix})

The luminance (Y) component contains all the information required for black and white television, and captures our perception of the relative brightness of particular colours. That we perceive green as much lighter than red, and red lighter than blue, is indicated by their respective weights of 0.587, 0.299 and 0.114 in the first row of the conversion matrix above. These weights should be used when converting a colour image to greyscale if you want the perception of brightness to remain the same. This is not the case for the intensity component in an HSI image, as shown in figure 8. The Y component is the same as the CIE primary Y (see § 2.1).Figure Figure 8: Image (a) shows a colour test pattern, consisting of horizontal stripes of black, blue, green, cyan, red, magenta and yellow, a colour ramp with constant intensity, maximal saturation, and hue changing linearly from red through green to blue, and a greyscale ramp from black to white. Image (b) shows the intensity for image (a). Note how much detail is lost. Image (c) shows the luminance. This third image accurately reflects the brightness variations preceived in the original image. 4 Applying Greyscale Transformations to Colour Images Given all these different representations of colour, and hence colour images, the question arises as to what is the best way to apply the image processing techniques we have covered so far to these images? One possibility is to apply the transformations to each colour plane in an RGB image, but what exactly does this mean? If we want to increase the contrast in a dark image by histogram equalisation, can we just equalise each colour independently? This will result in quite different colours in our transformed image. In general it is better to apply the transformation to just the intensity component of an HSI image, or the luminance component of a YIQ image, thus leaving the chromaticity unaltered. An example is shown in figure 9. When histogram equalisation is applied to each colour plane of the RGB image, the final image is lighter, but also quite differently coloured to the original. When histogram equalisation is only applied to the luminance component of the image in YIQ format, the result is more like a lighter version of the original image, as required.
