1. Download installer fedora dari link berikut 
https://kojipkgs.fedoraproject.org/packages/Fedora-Container-Base/37/20221226.0/images/
2. extrak dan rename 
3. Jalnkkan config 
```
mkdir $HOME\wsl\fedora
wsl --import fedora $HOME\wsl\fedora $HOME\Downloads\fedora-36-rootfs.tar	
wsl -l	
wsl -d fedora
sudo dnf update
sudo dnf install -y util-linux passwd cracklib-dicts
useradd -G wheel username
passwd username
wsl -d fedora -u username
printf "\n[user]\ndefault = username\n" | sudo tee -a /etc/wsl.conf
```
jika gagal install nano dan edit manual
```
sudo dnf install nano
nano /etc/wsl.conf
```
msukan default user 
```
[user]
default=namauser
```
4. set user menjadi root 
```
sudo visudo 
[nama user] ALL=(ALL:ALL) ALL
[nama user] ALL=(ALL) NOPASSWD:ALL
```
