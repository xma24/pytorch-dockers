# Customized Torch TensorRT Dockerfile

Pytorch and Nvidia have published their docker images compiled with Torch TensorRT. However, the PyTorch compiled omits XXX_cuda_cu.so files. 

This dockerfile is based on the TensorRT docker image provided by Nvidia and is installed with a pytorch environment using pip in the dockerfile.

Note: Do NOT use conda to install Torch TensorRT. The PATH will be a problem that is not easy to deal with.

Make sure that the PyTorch version, nvidia dirver version and cuda version match with each other. TensorRT requires cuda version 11.3.

The generated docker image includes TensorRT, Torch TensorRT, PyTorch, PyTorch Lightning, and OpenmmLab.


lnscc slides: https://docs.google.com/presentation/d/1DzJ2UiXvtP2d9q4GVRa2c7Chl0XaDTcs/edit?usp=sharing&ouid=115491011356388569022&rtpof=true&sd=true
