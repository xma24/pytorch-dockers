# Customized Torch TensorRT Dockerfile

Pytorch and Nvidia have published their docker images compiled with Torch TensorRT. However, the pytorch compiled does not include XXX_cuda_cu.so files. 

This dockerfile is based on the TensorRT docker image provided by Nvidia and is installed with pytorch environment using pip in the dockerfile.
