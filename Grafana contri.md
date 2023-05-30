
Contribution Guides:
https://grafana.com/blog/2021/03/03/how-to-set-up-a-grafana-development-environment-on-a-windows-pc-using-wsl/

https://github.com/grafana/grafana/blob/HEAD/contribute/developer-guide.md

Install WSL distribution of your choice

```
wsl --install -d Ubuntu
```

``` in Ubuntu
$ sudo apt-get update

$ sudo apt-get upgrade

$ sudo apt-get install golang-go

wget https://go.dev/dl/go1.20.3.linux-amd64.tar.gz

sudo tar -xvf go1.20.3.linux-amd64.tar.gz 

sudo mv go /usr/local

```

```
sudo nano ~/.bashrc

```

scroll down and add these to your `.bashrc` profile

```
## Go Global variables
export GOROOT=/usr/local/go

export GOPATH=$HOME/go

export PATH=$GOPATH/bin:$GOROOT/bin:$PATH
```

```
source ~/.bashrc
```

Install NVM

```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/master/install.sh | bash
```

Install Node

```
nvm install --lts
```


Install yarn
```
npm install -g yarn
```


Git Clone
```
git clone https://github.com/grafana/grafana.git
```

To run frontend

```
yarn install --immutable
yarn start
```

To run Backend
```
make run
```



  


  