**Installing IF-Trellis and comfyui**


[ComfyUI](https://github.com/comfyanonymous/ComfyUI)

[ComfyUI-IF_Trellis](https://github.com/if-ai/ComfyUI-IF_Trellis)

On a fresh Ubuntu 2404.1 install do:

```
sudo apt update
```
```
sudo apt upgrade
```
```
sudo reboot
```

**1. Nvidia, following these instructions: [nvidia](https://developer.nvidia.com/cuda-12-4-0-download-archive?target_os=Linux&target_arch=x86_64&Distribution=Ubuntu&target_version=22.04&target_type=deb_local)**
```
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/cuda-ubuntu2204.pin
```
```
sudo mv cuda-ubuntu2204.pin /etc/apt/preferences.d/cuda-repository-pin-600
```
```
wget https://developer.download.nvidia.com/compute/cuda/12.4.0/local_installers/cuda-repo-ubuntu2204-12-4-local_12.4.0-550.54.14-1_amd64.deb
```
```
sudo dpkg -i cuda-repo-ubuntu2204-12-4-local_12.4.0-550.54.14-1_amd64.deb
```
"To install the key, run this command:"
```
sudo cp /var/cuda-repo-ubuntu2204-12-4-local/cuda-87AE4CD8-keyring.gpg /usr/share/keyrings/
```
  
we need libtinfo5 but is old package, edit this file:
```
/etc/apt/sources.list.d/ubuntu.sources
```
and add the following:
```
Types: deb
URIs: http://old-releases.ubuntu.com/ubuntu/
Suites: lunar
Components: universe
Signed-By: /usr/share/keyrings/ubuntu-archive-keyring.gpg
```

now we install cuda and drivers
```
sudo apt update
```
```
sudo apt install build-essential
```
```
sudo apt install cuda-12-4
```
```
export PATH=/usr/local/cuda-12.4/bin${PATH:+:${PATH}}
```
```
sudo reboot
```

**2. 
ComfyUI**

go to install directory and then do:
```
git clone https://github.com/comfyanonymous/ComfyUI.git
```
```
cd ComfyUI
```
we will need a venv with python3.10:
```
sudo add-apt-repository ppa:deadsnakes/ppa
```
```
sudo apt update
```
```
sudo apt install python3.10 python3.10-venv
```
```
python3.10 -m venv venv
```
```
source venv/bin/activate
```
```
pip install --upgrade pip
```
```
pip install torch torchvision torchaudio --extra-index-url https://download.pytorch.org/whl/cu124
```
```
pip install -r requirements.txt
```
```
cd custom_nodes/
```
```
git clone https://github.com/ltdrdata/ComfyUI-Manager.git
```
```
cd ..
```
**3.
Trellis**

we need git large file support for checkpoints
```
cd models/checkpoints/
```
```
sudo apt install git-lfs
```
```
git lfs install
```
```
git clone https://huggingface.co/JeffreyXiang/TRELLIS-image-large
```
```
cd ../..
```
back to comfy folder, start comfyui, install trellis via Manager, then quit
```
python3 main.py --listen --port 7860
```
```
cd custom_nodes/ComfyUI-IF_Trellis/
```
```
edit the file linux_requirements.txt and remove the line with SageAttention, then:
```
```
pip install triton sageattention
```
```
pip install -r linux_requirements.txt
```
```
cd ../..
```
back to comfy folder, Now it works
```
python3 main.py --listen --port 7860
```
