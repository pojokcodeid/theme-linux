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
