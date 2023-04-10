# Follow below steps to setup cuda toolkit and pytorch installation for Ubuntu20 with GPU support

# 1 CUDA Setup:

1. Install CUDA=11.6 with these commands;

   `wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/cuda-ubuntu2004.pin`
   
   `sudo mv cuda-ubuntu2004.pin /etc/apt/preferences.d/cuda-repository-pin-600`
   
   `wget https://developer.download.nvidia.com/compute/cuda/11.6.0/local_installers/cuda-repo-ubuntu2004-11-6-local_11.6.0-510.39.01-1_amd64.deb`
   
   `sudo dpkg -i cuda-repo-ubuntu2004-11-6-local_11.6.0-510.39.01-1_amd64.deb`
   
   `sudo apt-key add /var/cuda-repo-ubuntu2004-11-6-local/7fa2af80.pub`
   
   `sudo apt-get update`
   
   `sudo apt-get -y install cuda`
   
   `sudo reboot`

2. Reboot the system.

# 2 cuDNN Installation:

1. Download cuDNN v8.7.0 for CUDA 11.x local installer (debian file) named as "Local Installer for Ubuntu20.04 x86_64 (Deb)" using link below; 
   
   https://developer.nvidia.com/rdp/cudnn-download . You need Nvidia Developers account to access this page.

2. Navigate to the directory containing the downloaded cuDNN Debian local installer file.

3. Add the downloaded package to the local package repository using this command

   `sudo dpkg -i cudnn-local-repo-${OS}-8.x.x.x_1.0-1_amd64.deb`

4. Import the CUDA GPG key.

   `sudo cp /var/cudnn-local-repo-*/cudnn-local-*-keyring.gpg /usr/share/keyrings/`

5. Refresh the repository metadata.

   `sudo apt update`

6. Run `sudo apt list libcudnn8` command to check available versions of libcudnn8 for CUDA. From CUDA 11.6 and onwwards, the cuDNN version does not need to be

   in accordance with installed CUDA version. Now replace the `x.x.x` and `X.Y` with latest version numbers obtained in upcoming commands. 

7. Install the runtime library.

   `sudo apt install libcudnn8=8.x.x.x-1+cudaX.Y`


8. Install the developer library.

   `sudo apt install libcudnn8-dev=8.x.x.x-1+cudaX.Y`

9. Install the code samples and the cuDNN library documentation.

   `sudo apt install libcudnn8-samples=8.x.x.x-1+cudaX.Y`

10. Reboot the system.

# 3 Installation Verification for cuDNN

1. Copy the cuDNN samples to a writable path.


   `cp -r /usr/src/cudnn_samples_v8/ $HOME`

2. Go to the writable path.


   `cd  $HOME/cudnn_samples_v8/mnistCUDNN`

3. Compile the mnistCUDNN sample.


   `make clean && make`

4. Run the mnistCUDNN sample.


   `./mnistCUDNN`

5. If cuDNN is properly installed and running on your Linux system, you will see a message similar to the following:  

   `Test passed!`

   Note. If Test Passed is not displayed then maybe a missing package needs to be installed. Please install the packages mentioned in terminal output and perfom step 4 again.
   You can ignore any warnings appearing after this procedure and this validates the cuDNN installation.


# 4. PyTorch Installation

1. Go to this link https://pytorch.org/get-started/locally/ and select the options as follows;

   PyTorch Build `Stable`

   Your OS `Linux`
   
   Package `Pip`
   
   Language `Python`
   
   Compute Platform `CUDA 11.6`

   Now copy the command in `Run this Command` section

2. Reboot the system

# 5 Verfiy PyTorch Installation:

   1. Open terminal and run `Python3` command.

   2. Import PyTorch with this command;

      `import torch`

   3. Verfiy CUDA integration with this command;

      `torch.cuda.is_available()`

      If returned `True` then validation is passed

   4. Verfiy cuDNN integration with this command;

      `torch.backends.cudnn.is_available()`

      If returned `True` then validation is passed