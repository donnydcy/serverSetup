# serverSetup
add more system packages to packages.txt, python packages to pipInstalls.txt
```bash
sudo apt-get install `cat packages.txt`
sudo pip install -r pipInstalls.txt
```
## Maybe the latest tensorflow doesn't show the information of GPU try this:
```bash
sess = tf.Session(config=tf.ConfigProto(log_device_placement=True))
```
