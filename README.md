# kbkminer
GPU CUDA Miner for Bismuth.

Install instructions (Linux):
* Install Ubuntu 20.04 **server** on a PC with at least one Nvidia GPU, memory requirement on GPU at least 1075MiB.
* Boot into the new server and do the following
```sudo apt update```
```sudo apt upgrade```
```sudo reboot```
* Write ```apt search nvidia-driver``` and find a suitable driver for your system.
* In this example we choose the following: ```sudo apt install nvidia-headless-470-server``` When finished, reboot
* ```sudo apt install nvidia-utils-470-server``` followed by ```nvidia-smi -q | grep "Product Name"``` Make sure that at least one GPU is detected.
* ```git clone https://github.com/Bismuthfoundation/Bismuth.git``` followed by ```cd Bismuth```
* ```sudo apt install python3-pip``` followed by ```pip3 install -r requirements-node.txt```
* ```screen -mS node python3 node.py``` You need to wait a while for the Junction Noise file to be created and the ledger bootstrapped and synced. While you wait you can press ```Ctrl-A d```to detach from the screen session, and ```screen -r node``` to go back.
* ```cd ~``` ```git clone https://github.com/Bismuthfoundation/Optipoolware.git```
* ```cd Optipoolware``` ```pip3 install -r requirements.txt```
* ```cp optipoolware.py ../Bismuth``` ```cp pool.txt ../Bismuth```
* ```cd ~/Bismuth``` ```screen -mS pool python3 optipoolware.py``` You can press ```Ctrl-A d```to detach from the pool session, and ```screen -r pool``` to go back.
* ```sudo apt install nvidia-cuda-toolkit``` followed by ```nvcc --version``` to check the version. In this example V10.1.243 was used.
* ```cd ~``` ```git clone https://github.com/Bismuthfoundation/kbkminer.git```
* ```sudo apt install cmake``` ```sudo apt install python3-pybind11```
* ```cd kbkminer``` ```chmod u+x mycompile.sh``` ```./mycompile.sh```
* Edit miner.txt to use your own miner_address
* ```cp optihash.py ../Bismuth``` ```cp miner.txt ../Bismuth``` ```cp bis.so ../Bismuth```
* Do not start the miner before the ledger is fully synced. The variable last_block_ago should be less than 300 seconds. Check with ```cd ~/Bismuth``` ```python3 commands.py statusget```
* ```cd ~/Bismuth``` ```screen -mS miner python3 optihash.py``` You can press ```Ctrl-A d```to detach from the miner session, and ```screen -r miner``` to go back.


Note that the pool will use the Bismuth address in the node wallet, found in the file wallet.der. If you want to solo mine, you can mine directly to this address by editing the file miner.txt and make the miner_address equal to the address in wallet.der. In this case, you can also edit min_payout in pool.txt to a large number to prevent payout transactions from the pool.

Install instructions (Ubuntu 20.04 **Desktop** ISO):
If you want to install kbkminer on the Ubuntu 20.04 Desktop edition, instead of the Server edition, use the following minor modifications instead:
* ```sudo apt install nvidia-driver-470``` followed by ```sudo apt install git```

Install instructions (Ubuntu 18.04 **Desktop** ISO):
* Install Ubuntu 18.04 desktop on a PC with at least one Nvidia GPU, memory requirement on GPU at least 1075MiB.
* Boot into the new server and do the following ```sudo apt update``` ```sudo apt upgrade``` ```sudo reboot```
* ```sudo apt install build-essential dkms freeglut3 freeglut3-dev libxi-dev libxmu-dev```
* ```wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/cuda-ubuntu1804.pin```
* ```sudo mv cuda-ubuntu1804.pin /etc/apt/preferences.d/cuda-repository-pin-600```
* ```sudo apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/7fa2af80.pub```
* ```sudo add-apt-repository "deb https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/ /"```
* ```sudo apt update``` ```sudo apt install cuda-10-1```
* Reboot the PC
* Check the CUDA version with ```nvcc --version```. In this example V10.1.243 was used.
* ```export PATH=/usr/local/cuda/bin${PATH:+:${PATH}}```
* ```export LD_LIBRARY_PATH=/usr/local/cuda/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}```
* ```sudo apt install python3-venv git python3.8 python3.8-venv python3.8-dev```
* ```python3.8 -m venv myenv```
* ```source myenv/bin/activate```
* ```sudo apt install python3-pip```
* ```git clone https://github.com/Bismuthfoundation/Bismuth.git``` followed by ```cd Bismuth```
* ```pip3 install wheel```
* ```sudo apt install autoconf libtool libffi-dev```
* ```pip3 install -r requirements-node.txt```
* ```screen -mS node python3 node.py``` You need to wait a while for the Junction Noise file to be created and the ledger bootstrapped and synced. While you wait you can press Ctrl-A d to detach from the screen session, and screen -r node to go back.
* ```cd ~ git``` ```clone https://github.com/Bismuthfoundation/Optipoolware.git```
* ```cd Optipoolware pip3 install -r requirements.txt```
* ```cp optipoolware.py ../Bismuth``` ```cp pool.txt ../Bismuth```
* ```cd ~/Bismuth``` ```screen -mS pool python3 optipoolware.py``` You can press Ctrl-A dto detach from the pool session, and screen -r pool to go back.
* ```sudo apt install cmake gcc-8 g++-8```
* ```cd ~``` ```git clone https://github.com/pybind/pybind11.git```
* ```cd pybind11``` ```cmake .``` ```make``` ```sudo make install```
* ```cd ~``` ```git clone https://github.com/Bismuthfoundation/kbkminer.git```
* ```cd kbkminer``` ```chmod u+x``` mycompile.sh``` ```./mycompile.sh```
* Edit miner.txt to use your own miner_address
* ```cp optihash.py ../Bismuth``` ```cp miner.txt ../Bismuth``` ```cp bis.so ../Bismuth```
* Do not start the miner before the ledger is fully synced. The variable last_block_ago should be less than 300 seconds. Check with ```cd ~/Bismuth``` ```python3 commands.py statusget```
* ```cd ~/Bismuth``` ```screen -mS miner python3 optihash.py``` You can press Ctrl-A dto detach from the miner session, and screen -r miner to go back.

