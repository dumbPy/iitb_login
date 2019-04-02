# IITB LOGIN

This package only consists a login script for headless login to `internet.iitb.ac.in` on any of the iitb servers.

### Install
`pip install iitb-login` should install the script. You can also try `pip install git+https://github.com/dumbPy/iitb-login.git`

### Usage
```
$ iitb login # to login. Enter username and password when prompted
# Enter username: username
# enter password: 
# Logged In As :  username
# Your IP:        10.119.255.255


$ iitb logout # to logout
$ iitb status # or just iitb to check status of login

```

### How It Works
#### Scrapy Spider

Scrapy Spider is used to load `https://internet.iitb.ac.in`, parse the page, check passed argument parsed by `ArgumentParser` and filling the form for subsiquent `POST` request for login and logout. Methods `get_username(response)` is used to parse logged in user's username and `get_ip(response)` to parse machine's ip address.

#### Paramiko
`paramiko.Agent()` connect's to exposed `ssh-agent`'s api on the machine and use it's keys to sign a random string. The signature of the string changes with each ssh key. Hence, credentials encrypted with one key can only be decrypted by the same key.  
These encrypted keys can now be saved in a pickle file at `~/.ssh/itb_login_creds` without the risk of exposing the credentials.

The keys from `paramiko.Agent().get_keys()` have a `sign_ssh_data()` method that is used to get the symetric key used for encryptng the credentials. As the signature returned is dependent of the private key being used for signing, the credentials are safe in a pickle dump and only be decrypted using the same key.

# Future Changes
In case the script becomes outdated and needs updation, feel free to make a pull request.
