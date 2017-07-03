# serverSetup
add more system packages to packages.txt, python packages to pipInstalls.txt
1. Install build essentials. 

...Including: python, python3, pip, pip3, git,...

```bash
$ sudo apt-get install `cat 1_packages.txt`
```
2. Install CUDA and cuDnn.
Strictly follow this instruction to avoid *infinit login loop*.

... [Install CUDA and Tensorflow](https://github.com/donnydcy/serverSetup/blob/master/2_InstallingCUDA8onUbuntu16_04.md)

3. Install python packages systemwisely.

```bash
$ sudo pip install -r 3_pipInstalls.txt
```


+ Maybe the latest tensorflow doesn't show the information of GPU try this in python env:

```sh
sess = tf.Session(config=tf.ConfigProto(log_device_placement=True))
```


*I've install or recover 3 GPU servers by using this method.*
