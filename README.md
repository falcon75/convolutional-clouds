# Convolutional Clouds ☁️

The notebook [clouds_conv.ipynb](clouds_conv.ipynb) is an attempt to learn a convolution that relates successive frames of cloud footage in [clouds.mp4](clouds.mp4). The idea is to capture the physical patterns of cloud footage, and use them to generate new frames.

Basically this is generic video modelling, and it can be used in compression and to upsample the frame rate.

## Generated Clouds

### Per Channel Convolution
Initially I tried convolving per colour channel, it didn't work well but the result is interesting. The generated frames quickly descended into vivid colours. This is because each colour channel evolves independently. You can have a think about why this causes the vivid chaos.

https://github.com/falcon75/convolutional-clouds/assets/39418626/e99fd995-e106-481b-95e1-291faed5e518

### Standard Convolution

In a standard convolution, each output is a summation of convolutions of each input channel, so they're coupled and the model uses colour much more sensibly.

https://github.com/falcon75/convolutional-clouds/assets/39418626/88b86608-50da-41f1-a2a6-8741103ae08d

Not a terrible result! Some of the weaknesses here are that edges aren't consistent, see the tree line, and perspective seems to disappear when the model takes over, it starts looking very flat. Both of these make sense with the convolutional model, its difficult to imagine how it could capture these patterns.

### Hierarchical Convolution

This model creates a kind of image pyramid, downsampling the frame then subtracting from the original, applying a 5x5 convolutions to each level, then combining the levels. This should enable the model to learn larger scale patterns, essentially a bigger receptive field but with less parameters and less computation. This is for 2 levels, no special revelations here:

https://github.com/falcon75/convolutional-clouds/assets/39418626/9cbb2bb7-23cb-46e7-837c-0e09dff59dce

## Ideas

### Experiments
Downsample frame rate, then fill in the gaps witht his model and compare to dumber interpolation alternatives.

### Model Improvements
- Recurrent connections, from previous frames.
- Multiple kernels to capture different modes of motion.
- More layers of the CNN architecture.
