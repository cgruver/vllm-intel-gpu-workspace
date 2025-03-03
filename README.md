# vllm-intel-gpu-workspace
Dev Workspace for vLLM with Intel Arc GPU Support

export PYTHONPATH=/usr/lib64/python3.13/site-packages:/usr/lib/python3.13/site-packages:${HOME}/.local/lib/python3.13/site-packages

pip install --upgrade pip
pip install intel_extension_for_pytorch

git clone https://github.com/intel/torch-ccl.git && cd torch-ccl
git checkout ccl_torch2.5.0+xpu
git submodule sync
git submodule update --init --recursive

COMPUTE_BACKEND=dpcpp python setup.py install
export INTELONEAPIROOT=${HOME}/intel/oneapi
USE_SYSTEM_ONECCL=ON COMPUTE_BACKEND=dpcpp pip install .
