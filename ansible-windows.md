### Install Ansible for Windows

Install msys2 - https://msys2.github.io

For mount c:\users to /home add this line to /etc/fstab:

```
c:\users /home ntfs binary,posix=0,noacl,user 0 0
```

run commands in msys2 terminal

```
pacman -S python2
cp /usr/bin/python2.exe /usr/bin/python.exe
curl -O https://bootstrap.pypa.io/get-pip.py
python get-pip.py
pacman -S gcc git
pacman -S libffi-devel libxml2 libxml2-devel libxslt-devel
ln -s /usr/lib/libffi-3.2.1/include /usr/include/libffi
pacman -S openssl-devel
pip install paramiko PyYAML Jinja2 httplib2 six
sed -i 's/define __BSD_VISIBLE 1/define __BSD_VISIBLE 0/' /usr/include/python2.7/pyconfig.h
pip install pycrypto
pip install lxml
git clone https://github.com/ansible/ansible.git --recursive
cd ansible
python setup.py install
cd $(python -c "import os, ansible; print os.path.dirname(os.path.dirname(ansible.__file__))")/EGG-INFO/scripts/
cp ansible ansible-playbook
cp ansible ansible-console
cp ansible ansible-doc
cp ansible ansible-galaxy
cp ansible ansible-pull
cp ansible ansible-vault
ansible --version
ansible-playbook --version
```
