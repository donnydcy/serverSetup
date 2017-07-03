# <span class="c5 c10">Download two files from the folder: CUDA & cudnn/</span>

<span class="c2 c5">cuda_8.0.61_375.26_linux.run</span>

<span class="c2 c5">cudnn-8.0-linux-x64-v5.1.tgz</span>

<span class="c2 c5"></span>

<span class="c2 c5">This procedure works fine on Geforce 650 Ti, which is also expected functional for later versions.</span>

<span class="c2 c5"></span>

# <span class="c10 c5">Pre-install cuda</span>

<span>Refer to</span> <span class="c37">[http://www.pyimagesearch.com/2016/07/04/how-to-install-cuda-toolkit-and-cudnn-for-deep-learning/](https://www.google.com/url?q=http://www.pyimagesearch.com/2016/07/04/how-to-install-cuda-toolkit-and-cudnn-for-deep-learning/&sa=D&ust=1494276309504000&usg=AFQjCNGz0oD-tf-axEfUmhy3Pb4JRW-YTw)</span><span class="c2 c5"> with some edition:</span>

<span class="c2 c5"></span>

1.  <span class="c2 c5">Disable the default  nouveau driver:</span>
```bash
$ sudo vim /etc/modprobe.d/blacklist-nouveau.conf
```


Add the following lines into the new file:
```sh
blacklist nouveau
blacklist lbm-nouveau
options nouveau modeset=0
alias nouveau off
alias lbm-nouveau off
```

<span class="c2 c5">Save this file, exit your editor, and then update the initial RAM filesystem, followed by rebooting your machine:</span>

```bash
$ echo options nouveau modeset=0 | sudo tee -a /etc/modprobe.d/nouveau-kms.conf
$ sudo update-initramfs -u
$ sudo reboot
```


1.  <span class="c2 c5"> After rebooting, it may not be able to have a graphical desktop (gnome),  use Ctrl+Alt+F1 to switch into console mode and stop the x service:</span>
```bash
$ sudo service lightdm stop
```
or
```bash
$ sudo service gdm stop
```
or
```bash
$ sudo service kdm stop
```


# <span class="c10 c5">Install CUDA</span>
```bash
$ chmod +x cuda_8*.run
$ mkdir installers
$ sudo ./cuda_8*_linux.run -extract=`pwd`/installers
```
Note the \` is the key left to “1”

<span class="c34"></span>

1.  <span>Change directory to  installers:</span> <span class="c6">$cd installers</span>
2.  <span class="c2 c5"> Run following files in order:</span>

Select **install KMDS** while installing Nvidia-Linux-x86_64*.run driver
**Note that the --no-opengl-files flag is Very Very Very important!**
```bash
$ sudo ./NVIDIA-Linux-x86_64*.run --no-opengl-files
$ modprobe nvidia
$ sudo ./cuda-linux64-rel-8*.run
$ sudo ./cuda-samples-linux-8*..run
```


1.  <span>Add following lines in ~/.bashrc,</span><span class="c41"> if share for all users, add to /etc/bash.bashrc</span>

<span class="c2 c0"># CUDA Toolkit</span>
```sh
export CUDA_HOME=/usr/local/cuda-8
export LD_LIBRARY_PATH=${CUDA_HOME}/lib64:$LD_LIBRARY_PATH
export LD_LIBRARY_PATH=${CUDA_HOME}/extras/CUPTI/lib64:$LD_LIBRARY_PATH
export PATH=${CUDA_HOME}/bin:${PATH}
```
<span class="c2 c5"> </span>

1.  <span class="c2 c5"> Update ~/.bashrc</span>
```bash
$ source ~/.bashrc
```
<a id="t.98d504f52e082efa9fe04b41853ac9ee1080f659"></a><a id="t.0"></a>




# <span>Install cuDNN(</span><span class="c48">Cudnn-8.0-linux-x64-v5.1.tgz</span><span>)</span>

<span>Installing cuDNN is quite simple — all we need to do is copying the files in the</span> <span class="c14">lib64</span><span class="c14"> </span><span> and</span> <span class="c14">include</span><span class="c14"> </span><span class="c2 c5"> directories to their appropriate locations on the machine:</span>
```bash
$ cd <cudnn path>
$ tar -zxf cudnn-7.5-linux-x64-v5.0-ga.tgz
$ cd cuda
$ sudo cp lib64/* /usr/local/cuda/lib64/
$ sudo cp include/* /usr/local/cuda/include/
```

# <span class="c10 c5">Install Tensorflow under Anaconda environment</span>

**_If you are going to install Tensorflow systemwisely, just stop here_**
** Our pipInstalls.txt installs its automatically and systemwisely, you will run it later**
** The following instruction is for installing in virtual enviornment **

The easiest way is to install with pip:
```bash
$ pip install tensorflow-gpu
```
<span class="c37">[https://github.com/tensorflow/tensorflow/blob/master/tensorflow/g3doc/get_started/os_setup.md#anaconda-installation](https://www.google.com/url?q=https://github.com/tensorflow/tensorflow/blob/master/tensorflow/g3doc/get_started/os_setup.md%23anaconda-installation&sa=D&ust=1494276309551000&usg=AFQjCNEohgTpaM2TbYMz6R9A7nXKbpKuHg)</span>


1.  <span class="c35 c5 c42">Create an environment called tf for python and tensorflow.</span>

<span class="c1">you can define the environment name (tf) to anything you like.</span>

<span class="c5 c39">Note that there are newer versions of Tensorflow which support Python3.5, 3.6, so the version of python is not necessary to be 3.4</span>

<span class="c2 c0">$ conda create -n tf python=3.5 anaconda</span>


1.  <span class="c42 c35 c5">Activate the conda environment by issuing the following command:</span>
```bash
source activate tensorflow

(tf)$  # Your prompt should change
```



1.  <span class="c19"> Installation is straightforward:</span>
```bash
(tf)$ pip install tensorflow-gpu
```

<span class="c0 c24">        (tf34)</span><span class="c0 c24">$</span> <span class="c0 c42 c24 c47">python</span>

<span class="c0 c24">        </span><span class="c22 c23 c7">>>></span> <span class="c23 c7 c32">import tensorflow as tf</span>

<span class="c22 c7 c23">       <there will be information which show successfully detecting CUDA devices>
        >>></span> <span class="c23 c7 c46">hello = tf.constant('Hello, TensorFlow!')</span><span class="c22 c23 c7">        >>></span> <span class="c32 c23 c7">sess = tf.Session()</span>

<span class="c22 c23 c7">       <Here will pop some warnings about CPU module, it’s fine>
>>></span> <span class="c32 c23 c7">print(sess.run(hello))</span>

<span class="c2 c0"></span>

<span class="c2 c0"></span>

1.  <span class="c19"> After working in Tensorflow:</span>

<span class="c0 c35">        (tf34)$ source deactivate</span>

