# MobileNet on CoreML

The following details the steps in creating a MobileNet based classifer on CoreML to recognise different types of Singaporean food.

The conversion from a Keras model to CoreML requires the following:

- TensorFlow 1.3
- Keras 2.0.8
- Python 2.7.x
- coremltools (latest version with PR#44 to avoid RuntimeError: Unsupported option activation=relu6 in layer Dense(conv1_relu). https://github.com/apple/coremltools/issues/38)

One of the key things to note when using transfer learning with ImageNet weights is that a scaling of 1./255 is required and because with coremltools, the bias is appled before the scaling is done, you would need to multiply back the scale on the RGB biases

- red_bias = -123.68 * scale
- green_bias = -116.779 * scale
- blue_bias = -103.939 * scale

This code is written using TensorFlow 1.3, Keras 2.0.8 and Python 2.7 for the conversion from Keras to CoreML