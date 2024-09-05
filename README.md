# Rainbow Teşviklli Node Testine katılıyoruz. Bitcoin tarafı bir node'dir. 

# [EXPLORER](https://testnet.rainbowprotocol.xyz/explorer) sitesine girin ve Principal İD nizi buraya yazıp Submit ediniz.

# Kurulumu yaparken sizden ilk önce bir isim belirlemenizi ve ardından bir şifre girmenizi isteyecek. En sonra tekrar aynı ismi girmeniz gerekiyor.
# Kurulum gayet basit, tek kod giriyoruz ve çalıştırıyoruz. Düşük özellik olduğu için ubuntu 22 ve üstünde bir sunucuya kurunuz.

### Screen açalım ve başlayalım
```console
Screen -S rainbow
```
```console
wget -O rainbow.sh https://raw.githubusercontent.com/aksamlan/Rainbow/main/install.sh && chmod +x rainbow.sh && ./rainbow.sh
```
### Yaptıktan sonra Screenden CTRL A + D yapıp çıkıyoruz ve aşağıdaki komutlarla yedekleri alıyoruz.Screen içerisine tekrar girmek için 'screen -r rainbow'
# Principal ve Private Key bilgilerimizi yedekleyelim.
```console
cat rbo_indexer_testnet/identity/principal.json
```
```console
cat rbo_indexer_testnet/identity/private_key.pem
```
# Loglara bakmak için dockerleri listeliyoruz ve ID'si ile bakıyoruz.
```console
docker ps -a
```
![image](https://github.com/user-attachments/assets/7975f7f8-e087-4443-9064-35a4deb6c711)
```console
docker logs -f DOCKER-ID
```
