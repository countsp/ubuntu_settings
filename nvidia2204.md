```
wget -O /tmp/amd64.env https://raw.githubusercontent.com/autowarefoundation/autoware/main/amd64.env && source /tmp/amd64.env

os=ubuntu2204
wget https://developer.download.nvidia.com/compute/cuda/repos/$os/$(uname -m)/cuda-keyring_1.1-1_all.deb
sudo dpkg -i cuda-keyring_1.1-1_all.deb
sudo apt-get update
cuda_version_dashed=$(eval sed -e "s/[.]/-/g" <<< "${cuda_version}")
sudo apt-get -y install cuda-toolkit-${cuda_version_dashed}
```

**Perform the post installation actions:**
```
# Taken from: https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#post-installation-actions
echo 'export PATH=/usr/local/cuda/bin${PATH:+:${PATH}}' >> ~/.bashrc
echo 'export LD_LIBRARY_PATH=/usr/local/cuda/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}' >> ~/.bashrc
source ~/.bashrc
```
