# Customized Torch TensorRT Dockerfile

---


## TensorRT Docker

Dockerfile path: `TensorRT-Dockerfile/Dockerfile`

Pytorch and Nvidia have published their docker images compiled with Torch TensorRT. However, the PyTorch compiled omits XXX_cuda_cu.so files. 

This dockerfile is based on the TensorRT docker image provided by Nvidia and is installed with a pytorch environment using pip in the dockerfile.

```
Note: Do NOT use conda to install Torch TensorRT. The PATH will be a problem that is not easy to deal with.
```

Make sure that the PyTorch version, nvidia dirver version and cuda version match with each other. TensorRT requires cuda version 11.3.

The generated docker image includes TensorRT, Torch TensorRT, PyTorch, PyTorch Lightning, and OpenmmLab.


## PyTorch Docker

Dockerfile path: `PyTorch-Dockerfile/Dockerfile`


### Using the Dockerfile

```python

# Build docker image from the Dockerfile
docker build -t uni_cuda_latest:v .


## Set GPU_INDEX; Set --volume if needed; 
docker run -itd --init --shm-size="300g" \
    --name="uni_cuda_latest_gpu" --runtime=nvidia -e NVIDIA_VISIBLE_DEVICES=GPU_INDEX \
    --ipc=host --user="$(id -u):$(id -g)" \
    # --volume="SOURCE:DESTINATION" \
    -v /etc/passwd:/etc/passwd:ro \
    -v /etc/group:/etc/group:ro \
    uni_cuda_latest:v python3


## Use the docker
docker exec -it uni_cuda_latest_gpu /bin/bash

```

This is my usually used docker setting including the following packages. 

```
absl-py                        1.2.0                
addict                         2.4.0                
aiohttp                        3.8.1                
aiosignal                      1.2.0                
albumentations                 1.2.0                
analytics-python               1.4.0                
antlr4-python3-runtime         4.9.3                
anyio                          3.6.1                
async-timeout                  4.0.2                
attrs                          22.1.0               
backoff                        1.10.0               
bcrypt                         4.0.0                
beautifulsoup4                 4.11.1               
black                          22.12.0              
cachetools                     5.2.0                
certifi                        2022.6.15            
cffi                           1.14.0               
chardet                        3.0.4                
charset-normalizer             2.1.1                
click                          8.1.3                
cloudpickle                    2.2.0                
commonmark                     0.9.1                
conda                          4.8.3                
conda-package-handling         1.7.0                
cryptography                   2.9.2                
cycler                         0.11.0               
detectron2                     0.6                  /home/detectron2_repo
docker-pycreds                 0.4.0                
effdet                         0.3.0                
ensemble-boxes                 1.0.9                
fastapi                        0.82.0               
ffmpy                          0.3.0                
filelock                       3.8.0                
flatbuffers                    2.0.7                
fonttools                      4.37.1               
frozenlist                     1.3.1                
fsspec                         2022.8.2             
fvcore                         0.1.5.post20221221   
gdown                          4.4.0                
gitdb                          4.0.9                
GitPython                      3.1.27               
google-auth                    2.11.0               
google-auth-oauthlib           0.4.6                
gradio                         3.2                  
grpcio                         1.48.1               
h11                            0.12.0               
httpcore                       0.15.0               
httpx                          0.23.0               
huggingface-hub                0.9.1                
hungarian-algorithm            0.1.11               
hydra-core                     1.3.1                
idna                           2.9                  
imageio                        2.21.2               
importlib-metadata             4.12.0               
importlib-resources            5.10.1               
iopath                         0.1.9                
Jinja2                         3.1.2                
joblib                         1.1.0                
kiwisolver                     1.4.4                
linkify-it-py                  1.0.3                
llvmlite                       0.39.1               
Markdown                       3.4.1                
markdown-it-py                 2.1.0                
MarkupSafe                     2.1.1                
matplotlib                     3.5.3                
mdit-py-plugins                0.3.0                
mdurl                          0.1.2                
mmcv-full                      1.6.0                
monotonic                      1.6                  
multidict                      6.0.2                
mypy-extensions                0.4.3                
networkx                       2.8.6                
nltk                           3.7                  
numba                          0.56.2               
numpy                          1.22.0               
nvidia-pyindex                 1.0.9                
oauthlib                       3.2.0                
omegaconf                      2.3.0                
onnx                           1.12.0               
onnxruntime-gpu                1.11.0               
opencv-contrib-python-headless 4.5.3.56             
opencv-python                  4.5.3.56             
opencv-python-headless         4.6.0.66             
ordereddict                    1.1                  
orjson                         3.8.0                
packaging                      21.3                 
pandas                         1.4.4                
paramiko                       2.11.0               
pathspec                       0.10.3               
pathtools                      0.1.2                
Pillow                         9.2.0                
pip                            20.0.2               
platformdirs                   2.6.0                
portalocker                    2.6.0                
prettytable                    3.4.1                
promise                        2.3                  
protobuf                       3.19.6               
psutil                         5.9.2                
pyasn1                         0.4.8                
pyasn1-modules                 0.2.8                
pycocotools                    2.0.4                
pycosat                        0.6.3                
pycparser                      2.20                 
pycryptodome                   3.15.0               
pydantic                       1.10.2               
pyDeprecate                    0.3.2                
pydub                          0.25.1               
Pygments                       2.13.0               
PyNaCl                         1.5.0                
pynndescent                    0.5.7                
pyOpenSSL                      19.1.0               
pyparsing                      3.0.9                
PySocks                        1.7.1                
python-dateutil                2.8.2                
python-multipart               0.0.5                
pytorch-lightning              1.6.4                
pytorch-quantization           2.1.2                
pytz                           2022.2.1             
PyWavelets                     1.3.0                
PyYAML                         6.0                  
qudida                         0.0.4                
regex                          2022.8.17            
requests                       2.23.0               
requests-oauthlib              1.3.1                
rfc3986                        1.5.0                
rich                           12.4.4               
rsa                            4.9                  
ruamel-yaml                    0.15.87              
scikit-image                   0.18.3               
scikit-learn                   1.1.2                
scipy                          1.9.1                
sentence-transformers          2.2.2                
sentencepiece                  0.1.97               
sentry-sdk                     1.9.8                
setproctitle                   1.3.2                
setuptools                     46.4.0.post20200518  
shortuuid                      1.0.9                
six                            1.14.0               
smmap                          5.0.0                
sniffio                        1.3.0                
soupsieve                      2.3.2.post1          
sphinx-glpi-theme              0.3                  
starlette                      0.19.1               
tabulate                       0.9.0                
tensorboard                    2.10.0               
tensorboard-data-server        0.6.1                
tensorboard-plugin-wit         1.8.1                
termcolor                      1.1.0                
terminaltables                 3.1.10               
thop                           0.1.1.post2207130030 
threadpoolctl                  3.1.0                
tifffile                       2022.8.12            
timm                           0.6.9                
tokenizers                     0.12.1               
tomli                          2.0.1                
torch                          1.11.0+cu113         
torchaudio                     0.11.0+cu113         
torchmetrics                   0.9.3                
torchvision                    0.12.0+cu113         
tqdm                           4.64.1               
transformers                   4.21.3               
typing-extensions              4.3.0                
uc-micro-py                    1.0.1                
umap-learn                     0.5.3                
urllib3                        1.25.11              
uvicorn                        0.18.3               
wandb                          0.13.2               
wcwidth                        0.2.5                
websockets                     10.3                 
Werkzeug                       2.2.2                
wheel                          0.34.2               
yacs                           0.1.8                
yapf                           0.32.0               
yarl                           1.8.1                
zipp                           3.8.1   
```