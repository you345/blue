# blue
blue-intelj1800

[[https://techoverflow.net/2021/06/14/a-simple-coreos-config-for-beginners-with-password-login/]]
[[https://kt-hiro.hatenablog.com/entry/20140808/1407515284#:~:text=%E3%83%BB%E5%89%B2%E3%82%8A%E5%BD%93%E3%81%A6%E3%82%89%E3%82%8C%E3%81%9F%20IP%E3%82%A2%E3%83%89%E3%83%AC%E3%82%B9%20%E3%81%AE%E7%A2%BA%E8%AA%8D%20%24%20ip%20adde%20show%20%E3%83%BBcore%E3%83%A6%E3%83%BC%E3%82%B6%E3%81%AE%E3%83%91%E3%82%B9%E3%83%AF%E3%83%BC%E3%83%89%E5%A4%89%E6%9B%B4,%23%20ssh%20core%40%E2%80%98%E2%80%99IP%E3%82%A2%E3%83%89%E3%83%AC%E3%82%B9%E2%80%9D%20%E3%83%BB%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB%E5%BE%8C%E3%81%AE%20ssh%20%E6%8E%A5%E7%B6%9A%E7%94%A8%E3%83%91%E3%82%B9%E3%83%AF%E3%83%BC%E3%83%89%E3%81%AE%20%E3%83%8F%E3%83%83%E3%82%B7%E3%83%A5%E5%80%A4%20%E3%81%AE%E5%8F%96%E5%BE%97]]
[[https://github.com/coreos/container-linux-config-transpiler/]]
[[https://qiita.com/kawasin73/items/07e07fe0cb99f7ef1365]]
[[https://isleofhoso.com/linux-networkmanager-default/]]

```
podman run -ti --rm quay.io/coreos/mkpasswd --method=yescrypt
podman run -i --rm quay.io/coreos/fcct:release --pretty --strict < ignition.yaml > ignition.ign            # podman -> docker
docker run -it --rm debian:11-slim bash -c 'apt-get update -y && apt-get install -y speedtest-cli && speedtest-cli'

```

```
[live cmdline] sudo nmgui
 inet 192.168.2.40/24
 Current DNS Server: 192.168.2.1
         DNS Servers: 192.168.2.1
[live cmdline] sudo coreos-installer install /dev/sda --copy-network --ignition-url https://techoverflow.net/coreos.ign
[admin@CoreOS ~]$ docker run -d -p 22001:3000 --name=sshs --restart=on-failure wettyoss/wetty --ssh-host=192.168.2.40
```

```
USB Wi-Fiアダプター 管理画面へは同一セグメントが見えるPCからecset-200の検索ツールを使って設定する。
WLI-UTX-AG300  Ver.1.05
EC50C4DD5A1B1F
50:C4:DD:5A:1B:1F
ssid: asus5g dhcp
admin / password
```
