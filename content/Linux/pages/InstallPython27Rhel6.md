Title: Install Python 2.7 on RHEL 6
Category: Linux
Date: 2012-12-01 10:02

Python 2.7 is not available in RHEL6. To install it make these steps:

## Confgure yum if it was not configured:

```
cat /tmp/xauth |xargs -l xauth add  
cat <<EOF >>/etc/yum.repos.d/centos.repo
[centos]
name=centos
baseurl=http://mirror.centos.org/centos-6/6/os/x86_64
EOF
yum makecache
```

## Install development tools

```
yum groupinstall "Development tools" 
yum install zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gdbm-devel db4-devel libpcap-devel xz-devel wget http://python.org/ftp/python/2.7.6/Python-2.7.6.tar.xz 
```

## Download and compile: 
```
tar xf Python-2.7.6.tar.xz 
cd Python-2.7.6 ./configure --prefix=/usr/local --enable-unicode=ucs4 --enable-shared LDFLAGS="-Wl,-rpath /usr/local/lib" 
make && make altinstall
```

## Install pip 
```
wget https://bitbucket.org/pypa/setuptools/raw/bootstrap/ez_setup.py python2.7 ez_setup.py easy_install-2.7 pip
```

Reference: http://stackoverflow.com/questions/27115526/how-to-get-python-2-7-into-the-system-path-on-redhat-6-5-linux

