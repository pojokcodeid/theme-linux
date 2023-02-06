# SETUP ARCH LINUX DI WSL 2
1. Kita harus sudah ada wsl lain yang terinstall 
2. Download ISO stable 
- download ambil dari sini : https://mirrors.edge.kernel.org/archlinux/iso/latest/
```
sudo aot-get install wget 
mkdir download
cd download
wget https://mirrors.edge.kernel.org/archlinux/iso/latest/archlinux-bootstrap-2023.02.01-x86_64.tar.gz
sudo dnf install xz
sudo apt install xz-utils

sudo tar -zxvf archlinux-bootstrap-2023.02.01-x86_64.tar.gz

cd root.x86_64
```
3. edit beberapa servers pada pacman mirrorlist.
```
sudo vim etc/pacman.d/mirrorlist
```
4. Compres kembali root.x86_64 directory.
```
sudo tar -czvf root.tar.gz *
```
5. copy ke local dir windows 
```
sudo mv root.tar.gz /mnt/c/Users/USERNAME/Download/root.tar.gz
```
6. Sekarang buka powershellnya
```
wsl --import arch $HOME\wsl\arch C:\Users\Asep\Downloads\root.tar.gz
wsl -d arch

pacman-key --init
pacman-key --populate archlinux

pacman -Syyu base base-devel git vim wget reflector fish
```
7. Enable multilib
```
linenumber=$(grep -nr "\\#\\[multilib\\]" /etc/pacman.conf | gawk '{print $1}' FS=":")
sed -i "${linenumber}s:.*:[multilib]:" /etc/pacman.conf
linenumber=$((linenumber+1))
sed -i "${linenumber}s:.*:Include = /etc/pacman.d/mirrorlist:" /etc/pacman.conf
```
8. Sync package databases.
```
pacman -Syy
```
9. Set root user password.
```
passwd
```
10. add user baru 
```
useradd -m -G wheel -s /bin/fish -d /home/username username
passwd username
sed -i '/%wheel ALL=(ALL) ALL/c\%wheel ALL=(ALL) ALL'  /etc/sudoers
```
11. Edit Arch locale and regenerate.
```
sed -i 's:#en_US.UTF-8 UTF-8:en_US.UTF-8 UTF-8:g' /etc/locale.gen
locale-gen
echo LANG=en_US.UTF-8 >> /etc/locale.conf
echo LANGUAGE=en_US.UTF-8 >> /etc/locale.conf
echo LC_ALL=en_US.UTF-8 >> /etc/locale.confS
```
12. update root acess
```
pacman -Syyu vi
sudo visudo 

[nama user] ALL=(ALL:ALL) ALL
[nama user] ALL=(ALL) NOPASSWD:ALL
```
13. Create the wsl.conf file on the system.
```
vim /etc/wsl.conf
```
```
[automount]
enabled = true
options = "metadata,uid=1000,gid=1000,umask=22,fmask=11,case=off"
mountFsTab = true
crossDistro = true

[network]
generateHosts = false
generateResolvConf = true

[interop]
enabled = true
appendWindowsPath = true

[user]
default = your_username
```
14. Restart WSL
```
wndows + r
wsl --shutdown
```
15. Buka lagi arch
```
mkdir ~/yay 
cd ~/yay
wget "https://aur.archlinux.org/cgit/aur.git/plain/PKGBUILD?h=yay" --output-document=./PKGBUILD
makepkg -si
```
16. Install daemonize.
```
yay -S daemonize
```
17. Create a startup script daemonize systemd as PID 1.
```
vim /etc/profile.d/00-wsl2-systemd.sh
```
```
SYSTEMD_PID=$(ps -ef | grep '/lib/systemd/systemd --system-unit=basic.target$' | grep -v unshare | awk '{print $2}')

if [ -z "$SYSTEMD_PID" ]; then
   sudo /usr/bin/daemonize /usr/bin/unshare --fork --pid --mount-proc /lib/    systemd/systemd --system-unit=basic.target
   SYSTEMD_PID=$(ps -ef | grep '/lib/systemd/systemd --system-unit=basic.    target$' | grep -v unshare | awk '{print $2}')
fi

if [ -n "$SYSTEMD_PID" ] && [ "$SYSTEMD_PID" != "1" ]; then
    exec sudo /usr/bin/nsenter -t $SYSTEMD_PID -a su - $LOGNAME
fi
```
18. Selesai re-enter wsl
