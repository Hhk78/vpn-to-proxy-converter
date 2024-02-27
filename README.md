
```bash
sudo docker network create proxy
```
Bu komutla proxy adlı bir ağ oluşturuyoruz.

```bash
sudo docker run --name debian1  --network=proxy --device=/dev/net/tun --cap-add=NET_ADMIN -it debian /bin/bash
```
tun device eklenmiş bir konteyner oluşturuyoruz.
girişi otomatik yapıyor


İleride tekrar girmek isteerseniz;
```bash
sudo docker start debian1
sudo docker exec -it debian1 /bin/bash
```


İçinde iken basit araçları ve openvpnyi kurun.
```bash
apt update && apt upgrade && apt install openvpn nano wget curl  -y
```
Sonra vpnye bağlanın
```bash
openvpn --config file.ovpn
```
Sonra microsocks ile socks serveri açın.
(program https://github.com/rofl0r/microsocks)
```bash
./microsocks -p 1080 -i 172.18.0.2
```
Artık yerel makinede (konteynerde değil) 
```bash
ALL_PROXY=socks5://172.18.0.2:1080 curl ip.me
```
Yazarak test edin.
