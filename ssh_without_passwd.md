## Princinple

Generate a private key and public key pair on your local machine, and save the public key on your remote server as an authorized key. Then everytime you want to connect to the server, it will use that authorized public key to generate a private key and compare with your local machine's private key. The connection would be successful if the private keys are the same.

## Steps

#### 1. Generating the key pair
- If you have already generated a key pair, you can skip this step and just use them. Otherwise just run the following:
```
ssh-keygen -t rsa
```
You will see:
```
Generating a public/private rsa key pair.
Enter the file in which you wish to save they key (i.e., /home/username/.ssh/id_rsa).
```
You can just use the default settings by input "Enter"

#### 2. Copying the public key to your server

- Linux User:
```
ssh-copy-id -i ~/.ssh/id_rsa.pub username@your-server-ip
```
You should see:
```
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed == if you are prompted now it is to install the new keys
username@server.host.com's password:
```

- Mac User: First create the `~\.ssh` folder in your remote server if it doesn't have one, then run:
```
cat ~/.ssh/id_rsa.pub | ssh username@your-server-ip "cat >> ~/.ssh/authorized_keys"
```
You should see:
```
The authenticity of host 'server.dreamhost.com (208.113.136.55)' can't be established.
RSA key fingerprint is 50:46:95:5f:27:c9:fc:f5:f5:32:d4:3a:e9:cb:4f:9f.
Are you sure you want to continue connecting (yes/no)? yes

Warning: Permanently added 'server.dreamhost.com,208.113.136.55' (RSA) to the list of known hosts.

username@server.dreamhost.com's password:
```

#### 3. Adding your private key to your ssh client

First start ssh-agent by running the following command.
```
eval `ssh-agent`
```
Then add the private key:
```
ssh-add ~/.ssh/id_rsa
```
You can then check to confirm it's been added by running the following:
```
ssh-add -l
```
It will respond with your private key's fingerprint like this:
```
2048 aa:42:d4:46:81:43:65:7f:4e:53:94:5f:2f:0d:fd:bd customkey_rsa (RSA)
```
You can confirm that fingerprint by generating a fingerprint from your public key:
```
ssh-keygen -l -f customkey_rsa.pub
2048 aa:42:d4:46:81:43:65:7f:4e:53:94:5f:2f:0d:fd:bd user@server (RSA)
```
## Use ssh config file for your VScode to connect to a remote server

Create an ssh config file `~/.ssh/vs_code_config` like this:
```
Host zuliu-desktop (name of the host)
  User zuliu
  HostName host-ip
  IdentityFile ~/.ssh/id_rsa
```
Then in VScode, run `Remote-SSH: Open Configuration File` in the commmand palette and select this config file.

## Mount remote folder to local via sshfs

See the second answer in https://askubuntu.com/questions/412477/mount-remote-directory-using-ssh
