![alt text](https://avatars.githubusercontent.com/u/50934298?s=200&v=4)

# Meter WarringStakes Node (ubuntu 18.04)
## Docker Kurulumu  
*(Bu kurulum bir user üzerinde yapılabilir. Başlamak için önce user oluşturun.)*  

`sudo apt-get update`  
`sudo apt-get install curl apt-transport-https ca-certificates software-properties-common`  
`curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -`  
`sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"`  
`sudo apt update`  
`apt-cache policy docker-ce`  
`sudo apt install docker-ce`  
`sudo chmod 666 /var/run/docker.sock`  

## Node kurulumu  
`mkdir meter_main_data`  
`cd meter_main_data/`  
`echo export "METER_MAIN_DATA_PATH=$PWD" >> ~/.bashrc`  
`source ~/.bashrc`  
`docker run --network host --name meter_main --restart always -e NETWORK="main" -v $METER_MAIN_DATA_PATH:/pos -d meterio/mainnet:latest`  
`docker container start meter_main`  

## Meter Docker Image için otomatik güncellemeyi ayarlama
`docker run -d --name watchtower --restart always -v /var/run/docker.sock:/var/run/docker.sock containrrr/watchtower --include-stopped --revive-stopped --enable-lifecycle-hooks --interval 10 --cleanup meter_main`  

## Gerekli portlar  
8669  
8670-8671  
55555  
11235  
9100  

## Güncel masaüstü cüzdanı  
https://www.meter.io/wallets/  

## Cüzdanı node'a bağlama  
* Cüzdanı açtıktan sonra SETTINGS menüsüne girin  
* Nodes listesinin sağ üstündeki + butonuna basarak yeni node ekleme penceresini açın  
* Açılan pencerede;  
  Name yerine `Bağlanacağınız noda vermek istediğiniz isim`  
  URL yerine `http://<IP>:8669`  
  yazın ve SAVE ile kaydedin  
* Adres satırının solundaki MAINNET yazan yere tıklayın  
* Açılan listeden "Mainnet - <Node_Name>"i seçerek üzerinde çalışacağımız wallet penceresini açın (öncekini kapatabilirsiniz)  
* WALLET menüsünde NEW butonuna basarak yeni wallet oluşturun  

![alt text](https://raw.githubusercontent.com/meterio/WarringStakes/master/addnode.png)
![alt text](https://raw.githubusercontent.com/meterio/WarringStakes/master/connectnode.png)

## Cüzdanda stake başlatma  
* https://faucet.meter.io/ adresinden faucet alın  
* CANDIDATES menüsüne girin  
* LIST ME AS CANDIDATE buyonuna basın  
* Açılan sayfada şu bilgileri girerek stake başlatın;  
  Amount alanına 2000  
  Name alanına görünmesini istediğiniz isim  
  IP alanına server IP'si  
  Public Key alanına serverda meter-data klasöründe public.key dosyasındaki değeri girin  
* CANDIDATES listesinde isminiz görünüyorsa kilitli MTRG miktarı 2000 olarak görünüyorsa işlem başarıyla oluşmuş demektir.
