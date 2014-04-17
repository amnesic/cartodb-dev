This is a set of scripts to install a development environment for https://github.com/CartoDB/cartodb[CartoDB].

It can be used either with or without http://www.vagrantup.com/[vagrant].

## Structure 

Base OS for this configuration in Vagrant terms is "precise32", which is an Ubuntu 12.04 LTS distro. A bunch of shell scripts does the provisioning. The installation procedure is split to many scripts in-order to isolate failure and facilitate reruns footnote:[Need to comment out previous steps in Vagrant file for now].

## Installing inside a clean Ubuntu Precise VM
```
sudo apt-get update && sudo apt-get install -y git-core curl wget &&

git clone http://github.com/stevage/cartodb-dev
cd cartodb-dev

# Edit settings file: vim settings

bash install-cartodb.sh
```
## Running a VM with Vagrant:
```
git clone http://github.com/stevage/cartodb-dev
cd cartodb-dev

# Edit settings file: vim settings

vagrant up
```

## After installing
As CartoDB is pretty heavy, the script takes quite some time to download the required dependencies. Once the provisioning is done, all you are required to do is start CartoDB.

```
vagrant ssh
cd /usr/local/src/cartodb
sudo bundle exec foreman start -p 3000
```

As the domain property in the configuration is set to localhost.lan, the host machine is required to have a name to address mapping. Following line does the trick,

```
echo "127.0.0.1 monkey.localhost.lan" | sudo tee -a /etc/hosts
```

The vagrant configuration forwards port 3000 from the host to the guest. So monkey.localhost.lan:3000 from the host machine will take you to the CartoDB's login page. The password is same as the username.

Have fun!

