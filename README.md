## Box setup

````
vagrant up
````

## Install stuff

Simple provisioning coming soon

````
sudo apt-get update
sudo apt-get install git-core tmux htop mc vim curl python-setuptools python-pycurl build-essentials libsasl2-dev autoconf automake libtool openjdk-7-jre-headless openjdk-7-jdk maven python-dev libcurl4-openssl-dev

cd /vagrant/app
git clone https://github.com/mesosphere/marathon.git
git clone https://github.com/felixroeser/marathon-pkg.git

sudo gem install fpm

export JAVA_HOME=/usr/lib/jvm/java-7-openjdk-amd64/
export LD_LIBRARY_PATH=$JAVA_HOME/jre/lib/amd64:$JAVA_HOME/jre/lib/amd64/server
````

## Build mesos

````
cd app
# Download a release from and unpack it
# https://github.com/apache/mesos/releases
curl https://github.com/apache/mesos/archive/0.15.0-rc4.tar.gz
tar xfvz 0.15.0-rc4.tar.gz
cd mesos-0.15.0-rc4
./bootstrap
mkdir build && cd build
../configure
make
````

Need the python binding? Find them in: build/src/python/dist/mesos-0.15.0-py2.7-linux-x86_64.egg

## Package marathon

````
cd marathon-pkg
git submodule init
git submodule update

# Update marathon
cd marathon
git pull origin master
cd ..
git add marathon/
git commit -m 'updated marathon'

make deb
````


