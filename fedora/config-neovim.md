# Install Node Js
1. create directori download 
```
mkdir download
cd download
```
2. install wget 
```
sudo dnf install wget
```
3. Download noe JS dari halaman resminya 
```
wget https://nodejs.org/dist/v18.13.0/node-v18.13.0-linux-x64.tar.xz
```
4. Install unzip dan xz
```
sudo dnf install unzip
sudo dnf install xz
sudo apt install xz-utils
```
5. Extrak file downloadan 
```
tar -xf [nama file node js tadi di download]
```
6. rename file extrac tadi 
```
mv [nama file extrak] [nama tujuan]
```
7. copy folder ke home 
```
cp -r [nama folder] /home/asep/
```
8. daftarkan env
```
sudo dnf install nano
cd ../
nano .bashrc
```
masukan path 
```
export PATH=/home/asep/nodejs/bin:$PATH
ctrl + x
y
enter
```
# Install git 
```
sudo dnf install git
```
#Install Neovim
1. download neovim
```
cd download
wget https://github.com/neovim/neovim/releases/download/v0.8.2/nvim-linux64.tar.gz
tar -xf nvim-linux64.tar.gz
mv nvim-linux64 nvim
cp -r nvim /home/asep/
```
2. register path
```
cd ../
nano .bashrc
export PATH=/home/asep/nvim/bin:$PATH
```
# Install GCC dan G++
```
sudo dnf install gcc
sudo dnf install g++
```
# Clone config Neovim
```
git clone https://github.com/pojokcodeid/nvim-lazy.git ~/.config/nvim
```
