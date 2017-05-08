# serverSetup
add more system packages to packages.txt, python packages to pipInstalls.txt
## Step 1: Install build essentials. 
Including: python, python3, pip, pip3, git,...
```bash
$ sudo apt-get install `cat 1_packages.txt`
```
## Step 2: Install CUDA and cuDnn.
### CUDA and Tensorflow installation Doc:
[Install CUDA and Tensorflow](https://github.com/donnydcy/serverSetup/blob/master/InstallingCUDA8Tensorflow1_0inUbuntu16_04.md)

## Step 3: Install python packages systemwisely.
```bash
$ sudo pip install -r 3_pipInstalls.txt
```


## Maybe the latest tensorflow doesn't show the information of GPU try this in python env:
```sh
sess = tf.Session(config=tf.ConfigProto(log_device_placement=True))
```
