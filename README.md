# Convolutional Clouds

The notebook [clouds_conv.ipynb](clouds_conv.ipynb) is an attempt to learn a convolution that relates successive frames of cloud footage in [clouds.mp4](clouds.mp4s). The idea is to capture the physical patterns of cloud footage, and use them to generate new frames.

## Generated Clouds

Initially I tried convolving per colour channel, it didn't work well but the result is interesting. The generated frames quickly descended into vivid colours. This is because each colour channel evolves independently. You can have a think about why this causes the vivid chaos.

[per channel convolution](video/channels.mp4)

https://github.com/falcon75/convolutional-clouds/assets/39418626/9783fc02-19b4-40b8-8d8f-31771edebc08


In a standard convolution, each output is a summation of convolutions of each input channel, so they're coupled and the model uses colour much more sensibly.

[standard convolution](video/conv.mp4)

https://github.com/falcon75/convolutional-clouds/assets/39418626/d3bf745c-e374-4f92-93f6-2e17c4e01558


## Ideas

### Improving the model

Hierachical convolutions, model splits frame into image pyramid, applies 5x5 convolutions to each level, then combines the levels. This should enable the model to learn larger scale patterns.

### Applications
Is this a way for to upsample the frame rate? Will it outdo interpolation? I can experiment with this by downsampling the dataset then upsampling with the model the comparing the error with interpolation.



