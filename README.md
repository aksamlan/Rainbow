![image](https://github.com/user-attachments/assets/98a5336f-4c80-49d0-8b0a-9008b0a9dd22)

# Rainbow Teşviklli Node Testine katılıyoruz. Bitcoin tarafı bir node'dir. 

### Sistem gereksinimleri : 
- CPU: Multi-core processor
- Memory: 4 GB RAM minimum
- Storage: 50 GB free disk space (or more depending)
- Network: Stable internet connection
- Ubuntu 22.04 

### Docker paketlerini yükleyelim
```console
sudo apt-get update
sudo apt-get install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
sudo systemctl start docker
sudo systemctl enable docker
```

### Gerekli dosyaları yükleyelim
```console
mkdir -p /root/project/run_btc_testnet4/data
git clone https://github.com/rainbowprotocol-xyz/btc_testnet4
cd btc_testnet4

# DOCKER-COMPOSE indirelim

 sudo curl -L "https://github.com/docker/compose/releases/download/v2.20.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
 sudo chmod +x /usr/local/bin/docker-compose

# version kontrolünü yapalım
docker-compose --version
```
### Konteyner bağlayalım, yeni bir cüzdan ve yeni bir adres oluşturalım.
```console
docker-compose up -d
docker exec -it bitcoind /bin/bash
bitcoin-cli -testnet4 -rpcuser=demo -rpcpassword=demo -rpcport=5000 createwallet walletname
```
### Cüzdan adresimizi kontrol edelim
```console
bitcoin-cli -testnet4 -rpcuser=demo -rpcpassword=demo -rpcport=5000 getnewaddress
```
### Repoyu ve binary kuralım
```console
cd
git clone https://github.com/rainbowprotocol-xyz/rbo_indexer_testnet && cd rbo_indexer_testnet

wget https://github.com/rainbowprotocol-xyz/rbo_indexer_testnet/releases/download/v0.0.1-alpha/rbo_worker
chmod +x rbo_worker
```
# COMPOSE.YML düzenleyelim
```console
nano docker-compose.yml
```
# AŞAĞIDAKİLERİ NANO DOSYASININ İÇİNE KOPYALAYIP YAPIŞTIRIN VE CTRL+X+Y SONRA KAYDETMEK İÇİN 'ENTER' Tuşuna basın
```console
version: '3'
services:
  bitcoind:
    image: mocacinno/btc_testnet4:bci_node
    privileged: true
    container_name: bitcoind
    volumes:
      - /root/project/run_btc_testnet4/data:/root/.bitcoin/
    command: ["bitcoind", "-testnet4", "-server","-txindex", "-rpcuser=demo", "-rpcpassword=demo", "-rpcallowip=0.0.0.0/0", "-rpcbind=0.0.0.0:5000"]
    ports:
      - "8333:8333"
      - "48332:48332"
      - "5000:5000"
```
### Nodu çalıştıralım
```console
docker-compose up -d
```

# Bitcoin Core'u bağlayalım ve indeksleyiciyi çalıştıralım
```console
screen -S Rainbow
```
```console
./rbo_worker worker --rpc http://127.0.0.1:5000 --password demo --username demo --start_height 42000
```

# Kurulum tamamlanmıştır. Cüzdan ve Principal ID'yi yedekleyelim
### Principal ID : 
```console
cat .identity/principal.json
```
### Private Key : 
```console
cat .identity/private_key.pem
```

# [EXPLORER](https://testnet.rainbowprotocol.xyz/explorer) sitesine girin ve Principal İD nizi buraya yazıp Submit ediniz.
