|       title       |     date     |     author     |     tester     | operating system | status  | version | draft |
| :---------------: | :----------: | :------------: | :------------: | :--------------: | :-----: | :-----: | :---: |
| dokumentasi ngrok | 22 Juni 2025 | Achmad Baihaqi | Achmad Baihaqi |  <br>Alma linux  | Private |   1.0   | True  |
#### rules

```
1. pastikan anda sudah memiliki akun di https://ngrok.com/
```

#### instalation
```
wget https://bin.equinox.io/c/bNyj1mQVY4c/ngrok-v3-stable-linux-amd64.tgz
```

```
sudo tar -xvzf PATH/TO/ngrok-v3-stable-linux-amd64.tgz -C /usr/local/bin
```

```
ngrok config add-authtoken YOUR_TOKEN
```

#### execution

```
ngrok http http://localhost:8080
```
note : 
```
1. localhost : sesuaikan dengan ip address aplikasi anda 
2. 8080 : sesuaikan dengan port aplikasi anda
```
<p align="center">
  <img src="ngrok-ex.png" alt="contoh" width="700" hight="150"/>
</p>
jika pada terminal seperti gambar di atas, maka ngrok anda sudah berjalan.

<p align="center">
  <img src="ngrok-dash.png" alt="contoh" width="700" hight="150"/>
</p>
Untuk mendapatkan domain gratis anda, maka anda harus kembali ke dalam dashboard https://ngrok.com/ seperti gambar di atas.

#### auto-execution

buka `$HOME/.config/ngrok/ngrok.yml` lalu ikuti perintah di bawah ini: 

```
sudo vim $HOME/.config/ngrok/ngrok.yml
```

```
version: "3"
agent:
    authtoken: 2yrmixkefC1nUvpNr9ODOIyHFrJ_4nZ8N2LxpTcpeG6QoDHu5
tunnels:
  web:
    proto: http
    addr: 80

```
note : 
```
1. proto : sesuaikan yang anda gunakan pada aplikasi di ngrok (http/https)
2. addr : sesuaikan dengan port yang anda gunakan pada aplikasi di ngrok
```
buat file `/etc/systemd/system/ngrok.service` lalu ikuti perintah di bawah ini:

```
sudo vim /etc/systemd/system/ngrok.service
```

```
[Unit]
Description=Start ngrok tunnel on startup
After=network-online.target
Wants=network-online.target systemd-networkd-wait-online.service

[Service]
ExecStart=/usr/local/bin/ngrok start --all --config PATH/TO/.config/ngrok/ngrok.yml
ExecReload=/bin/kill -HUP $MAINPID
KillMode=process
IgnoreSIGPIPE=true
Restart=always
RestartSec=3
Type=simple

[Install]
WantedBy=multi-user.target


```

```
sudo systemctl start ngrok.service
```

```
sudo systemctl enable ngrok.service
```
restart sistem operasi anda lalu cek `ngrok.service` dan pastikan seperti gambar di bawah ini: 

```
systemctl status ngrok.service
```

<p align="center">
  <img src="ngrok-sta.png" alt="contoh" width="700" hight="150"/>
</p>
