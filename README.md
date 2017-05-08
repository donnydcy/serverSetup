# serverSetup
add more system packages to packages.txt, python packages to pipInstalls.txt
```bash
sudo apt-get install `cat packages.txt`
sudo pip install -r pipInstalls.txt
```
## CUDA and Tensorflow installation Doc:
[Install CUDA and Tensorflow](https://github.com/donnydcy/serverSetup/blob/master/InstallingCUDA8Tensorflow1_0inUbuntu16_04.md)

## Maybe the latest tensorflow doesn't show the information of GPU try this:
```bash
sess = tf.Session(config=tf.ConfigProto(log_device_placement=True))
```
