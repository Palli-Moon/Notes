Vagrant Development Server Setup
================================

Steps to setting up a Vagrant server as a development box just the way I want it.

## Requirements and recommended applications
Applications that are required or recommended before setting up a vagrant box.

**Note:** The programs marked with an asterisk (\*) can be installed more quickly at [ninite.com](https://ninite.com/). This method is preferred to installing everything on it's own. 

### Required
* [Oracle VM VirtualBox](https://www.virtualbox.org/wiki/Downloads)
* [Vagrant](https://www.vagrantup.com/downloads.html) (obviously)

### Recommended
* [PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) \* (Required for Windows users)
* [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) \* (Same page as PuTTY)
* [WinSCP](http://winscp.net/eng/download.php) \*
* [Git Bash](https://msysgit.github.io/)
* [Notepad++](https://notepad-plus-plus.org/download/v6.7.9.html) \*

## Vagrant setup
The quickest way to set up the server the way I like it is to replace the Vagrant file with [this one](https://raw.githubusercontent.com/Palli-Moon/vagrantfile/master/Vagrantfile). Every step after 1 and 2 can be skipped if done that way.

1. Navigate to the directory in which you want to create the Vagrant box.
2. Run `vagrant init [boxname]`, the box `ubuntu/trusty64` is recommended. A directory of boxes can be found at https://atlas.hashicorp.com/boxes/search
3. *(optional)* Uncomment the `private_network` line in the `Vagrantfile` created in your directory, and set the ip to whatever you want.
4. *(optional)* Uncomment and change the `synced_folder` line to the folder(s) you want to sync. Example: `config.vm.synced_folder "C:\\location\\of\\share\\folder", "/home/vagrant/folder"`. Note the double backslash for Windows locations.
5. Run `vagrant up` to start your box.
6. Use *PuTTY* or another program to ssh into the box at `localhost:2222`. Note the port *22* is forwarded to *2222*. \*nix users can run `vagrant ssh` to ssh straight into the box from the command line.

Vagrant should now be up and running and you have control over it via ssh.

## Further server setup
All of the steps hereafter are optional. They are simply my way of customising it the way I want.

* *(Windows)* Edit the `hosts` file at `C:\Windows\System32\drivers\etc` to make access to your server easier. 

**Note:** `private_network` needs to have been turned on in the `Vagrantfile`. Use the ip you set there. The url name used is traditionally prefixed by `dev.`.

## SSH keys
To be able to *ssh* into the box on a Windows host without having to write the password every time, the automatically generated ssh private key needs to be converted to a `.ppk` file using *PuTTYgen*.

1. Load the file `insecure_private_key` into PuTTYgen. It's located at `C:/Users/[username]/.vagrant.d/insecure_private_key`.
2. Make sure the `Number of bits in generated key` is set to `2048`.
3. Click `Save private key`. Click `Yes` when it asks you if you if you don't want to password protect it. The new private key's name should be `insecure_private_key.ppk` (note the `.ppk` ending).
2. In PuTTY: set the field `Connection -> Data -> Auto-login username` to `vagrant`
3. In PuTTY: navigate the `Connection -> SSH -> Auth -> Private key file for authentication` field to the `insecure_private_key.ppk`. It should be in the same location as the old `insecure_private_key`

**NOTE:** these two lines **must** be in the `Vagrantfile`:

```config.ssh.insert_key = false```

```config.ssh.private_key_path = File.expand_path('~/.vagrant.d/insecure_private_key')```


### Nvm and node
Nvm is a version manager for node.js. It's a great thing to have installed and node versions can be swapped out easily if needed.

Run these commands to install:

```curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.25.4/install.sh | bash```

```echo ". ~/.nvm/nvm.sh" >> ~/.zshrc``` *(only if using zsh)*

Reconnect to the VM to enable nvm

```nvm install 4.1.1``` *(or the version of node you want installed)*

```echo "nvm use 4.1.1" >> ~/.zshrc``` *(again, only for zsh)*

