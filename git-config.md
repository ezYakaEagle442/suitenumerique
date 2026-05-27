
# Create your SSH Keys

If your GIT repo URL starts with HTTPS (ex: "https://github.com/<!XXXyour-git-homeXXX!>/suitenumerique.git"), git CLI will always prompt for password. 
When MFA is enabled on GitHub and that you plan to use SSH Keys, you have to use: git clone git@github.com:your-git-home/suitenumerique.git

```sh
export GH_USR="your-git-user"
export ssh_key=github
export ssh_passphrase="Your Secret phrase !"

echo -e 'y' | ssh-keygen -t rsa -b 4096 -f ~/.ssh/$ssh_key -C "youremail@groland.grd" -N $ssh_passphrase
echo GH_USR=$GH_USR
```

## Allow your SSH Keys from GitHub

Go to [https://github.com/settings/keys](https://github.com/settings/keys) click on the button 'New SSH Key' then 'Add SSH Key'

```sh
pwd
ls -al ~/.ssh/
ssh -T git@github.com -i ~/.ssh/$ssh_key.pub
```

## Git configuration

On Windows Add a file named '.gitconfig' to /c/Users/$USERNAME/.gitconfig
On WSL Add a file named '.gitconfig' to /home/yourusername/.gitconfig

```sh
#https://stackoverflow.com/questions/17307154/git-bash-push-to-bitbucket-ignores-ssh-key
# which ssh gaves /bin/ssh ..... In the .bashrc profile we just added
# export GIT_SSH=/bin/ssh.exe
#

[user]
	name = bob.jojo
	email = bob.jojo@yourcorp.com
[core]
	editor = nano
	#sshCommand = ssh -i /c/Users/bob.jojo/.ssh/id_rsa
	sshCommand = ssh -i /c/Users/bob.jojo/.ssh/githubkey

[alias]
	hist = log --all --graph --decorate --oneline

[http]
	#proxy = http://gateway.yourcorp.zscaler.net:80
	sslVerify = true
	# /ssl/certs/ca-bundle.crt
	#sslCAInfo=/etc/ssl/certs/
	
# Since git 2.3.1, you can put https://your.domain inside an HTTP section to indicate the following certificate is only for this domain.
[http "https://git-xxx.yourcorp.com"]
	# Put the certificate at C:\Users\~YourUserName\AppData\Local\Programs\Git\mingw64\ssl\certs
	sslCAInfo=/etc/ssl/certs/the_cert-tree.cer
	
[web]
	#browser = firefox
	browser = Chrome
[help]
	format = web
```
