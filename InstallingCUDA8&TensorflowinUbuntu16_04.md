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
```bash
$ sudo ./NVIDIA-Linux-x86_64*.run
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
The easiest way is to install with pip:
```bash
$ pip install tensorflow-gpu
```
<span class="c37">[https://github.com/tensorflow/tensorflow/blob/master/tensorflow/g3doc/get_started/os_setup.md#anaconda-installation](https://www.google.com/url?q=https://github.com/tensorflow/tensorflow/blob/master/tensorflow/g3doc/get_started/os_setup.md%23anaconda-installation&sa=D&ust=1494276309551000&usg=AFQjCNEohgTpaM2TbYMz6R9A7nXKbpKuHg)</span>

<span class="c2 c5">In Tensorflow-1.0 folder, there are different versions, in case its website crashing.</span>

<span class="c2 c5">Google how to install .whl file using wheel.</span>

<span class="c2 c5"></span>

1.  <span class="c35 c5 c42">Create an environment called tf34 for python3.4 and tensorflow.</span>

<span class="c1">you can define the environment name (tf34) to anything you like.</span>

<span class="c5 c39">Note that there are newer versions of Tensorflow which support Python3.5, 3.6, so the version of python is not necessary to be 3.4</span>

<span class="c2 c0">$ conda create -n tf34 python=3.4 anaconda</span>

<span class="c2 c0"></span>

<span class="c2 c0"></span>

1.  <span class="c42 c35 c5">Activate the conda environment by issuing the following command:</span>

<span class="c35 c18">        </span><span class="c0 c7">$</span> <span class="c7 c18 c45">source activate tensorflow</span><span class="c0 c7">
</span><span class="c7 c18 c22">         </span><span class="c38 c0 c7">(tf34)$  # Your prompt should change</span>

<span class="c42 c35 c5"></span>

1.  <span class="c19"> Save source url</span>

<span class="c17">(There is no link for gpu version in the official website, use the one which is provided in github):</span>

<span class="c0">(</span><span class="c0">tf34</span><span class="c0">)$</span> <span class="c0">export</span><span class="c0"> TF_BINARY_URL=https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow_gpu-1.0.0-cp34-cp34m-linux_x86_64.whl</span><span class="c0 c42 c43 c24">
</span>

<span class="c42 c20 c23 c43"></span>

1.  <span class="c19"> Installation is straightforward:</span>

<span class="c0 c35">        </span><span class="c2 c0">(tf34)$ pip install --ignore-installed --upgrade $TF_BINARY_URL</span>

<span class="c2 c0"></span>

<span class="c0">        </span><span class="c5 c30">Test:</span>

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

