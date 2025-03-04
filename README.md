# vllm-intel-gpu-workspace
Dev Workspace for vLLM with Intel Arc GPU Support

```bash
podman build -t nexus.clg.lab:5002/dev-spaces/vllm-dev:latest ./workspace-image
```

```bash
python -m pip install --upgrade pip

python -m pip install torch==2.5.1+cxx11.abi torchvision==0.20.1+cxx11.abi torchaudio==2.5.1+cxx11.abi intel-extension-for-pytorch==2.5.10+xpu oneccl_bind_pt==2.5.0+xpu --extra-index-url https://pytorch-extension.intel.com/release-whl/stable/xpu/us/

cd /projects/vllm

cat << EOF > requirements-xpu.txt
-r requirements-common.txt

ray >= 2.9
cmake>=3.26
ninja
packaging
setuptools-scm>=8
setuptools>=75.8.0
wheel
jinja2
EOF

sed -i '326d' mha_fusion.py

VLLM_TARGET_DEVICE=xpu python -m pip install .
```

```bash
vllm serve Qwen/Qwen2.5-1.5B-Instruct
```
