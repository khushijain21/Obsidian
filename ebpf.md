
https://netflixtechblog.com/linux-performance-analysis-in-60-000-milliseconds-accc10403c55 -  Linux Performance Analysis


```
apt-get update -y
sudo apt-get install libbpf-dev
sudo apt install llvm clang

sudo apt-get install linux-headers-generic
sudo apt-get install linux-generic

sudo apt-get install libc6-dev
sudo apt install build-essential flex bison dwarves libssl-dev libelf-dev

ln -s /usr/include/asm-generic /usr/include/asm
sudo bash -c "$(wget -O - https://apt.llvm.org/llvm.sh)"

```

```
brew install llvm
export PATH="/usr/local/opt/llvm/bin:$PATH"
export LDFLAGS="-L/usr/local/opt/llvm/lib"
export CPPFLAGS="-I/usr/local/opt/llvm/include"
export PYTHONPATH="/usr/local/opt/llvm/lib/python3.8/site-packages:$PYTHONPATH"


```