# K4YT3X's Hardened OpenSSH Client Configuration

This repository hosts my hardened version of OpenSSH client (8.2+) configuration file.

**Please review the configuration file carefully before applying it.** You are responsible for actions done to your own system. For example, you might want to enable `GSSAPIAuthentication` if you use Kerberos authentication.

## Usages

For convenience, I have pointed the URL `https://akas.io/ssh` to the `ssh_config` file. You may therefore download the `ssh_config` file with the following command. However, be sure to check the file's integrity after downloading it if you choose to download using this method.

```shell
curl -sSL akas.io/ssh -o ssh_config
```

### Method 1: Use as System Default

You can install this config to `/etc/ssh/ssh_config` to make variables in this configuration the system-wide default values. You may use this method if you would like all users to use these secure settings by default (e.g., as a system administrator).

```shell
# download the configuration file from GitHub using curl or other methods
curl https://raw.githubusercontent.com/k4yt3x/ssh_config/master/ssh_config ~/ssh_config

# backup the original ssh_config
sudo cp /etc/ssh/ssh_config /etc/ssh/ssh_config.backup

# edit the original ssh_config file and append the contents of the config file
sudo vim /etc/ssh/ssh_config

# alternatively, if you are certain that the old config file is useless
#   you may replace the old ssh_config with the new one
sudo mv ~/ssh_config /etc/ssh/ssh_config

# make sure the file has the correct ownership and permissions
sudo chown root:root /etc/ssh/ssh_config
sudo chmod 644 /etc/ssh/ssh_config
```

### Method 2: Use as User Default

You may also install this configuration file for the current user, which overwrites the system default values. You may use this method if you do not have the permissions to change the default configuration file or if you prefer to leave the default values be.

```shell
# download the configuration file from GitHub using curl or other methods
curl https://raw.githubusercontent.com/k4yt3x/ssh_config/master/ssh_config ~/ssh_config

# backup the original ssh_config
cp ~/.ssh/config ~/.ssh/config.backup

# edit the original ssh_config file and append the contents of the config file
vim ~/.ssh/config

# alternatively, if you are certain that the old config file is useless
#   you may replace the old ssh_config with the new one
mv ~/ssh_config ~/.ssh/config
```

### Verifying the Changes

You may want to use the [ssh-audit](https://github.com/jtesta/ssh-audit) script to check your SSH client's cryptographic strength after done configuring it. If you're paranoid like me, you can also run ssh-audit in a Docker container.

```shell
# clone the repository
git clone https://github.com/jtesta/ssh-audit ~/ssh-audit

# launch ssh-audit and listen to local port 2222
python3 ~/ssh-audit/ssh-audit.py -c

# connect to ssh-audit and check the audit results
ssh -p 2222 127.0.0.1
```
