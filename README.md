# vagrant-ubuntu-22.04-qgis-3.28

## Create Box

Create vagrant vm from `Vagrantfile`:

```
vagrant up
```

Make the Box as small as possible:

```
vagrant ssh
sudo apt-get clean
sudo dd if=/dev/zero of=/EMPTY bs=1M
sudo rm -f /EMPTY
cat /dev/null > ~/.bash_history && history -c && exit
```

Repackage the VM into a New Vagrant Box:

```
vagrant package --output mynew.box
```

Upload box / create new version etc. in browser: https://app.vagrantup.com/boxes/new / https://app.vagrantup.com/sogis/boxes/ubuntu-qgis-3.16/versions/new 


## Use Box

Create Vagrantfile:
```
vagrant init sogis/ubuntu-qgis-3.28
```

Adjust Vagrantfile:
```
config.vm.network "forwarded_port", guest: 22, host: 2020, id: 'ssh'
config.ssh.forward_agent = true
config.ssh.forward_x11 = true
```

Start / create vm:
```
vagrant up
```

Login with `vagrant ssh`, run `qgis`. Mac users will need _XQuartz_. Feel free to use _x2go_ (which is installed in the vm).
