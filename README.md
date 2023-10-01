# blue
blue-intelj1800

[live cmdline] sudo nmgui
 inet 192.168.2.40/24
 Current DNS Server: 192.168.2.1
         DNS Servers: 192.168.2.1
[live cmdline] sudo coreos-installer install /dev/sda --copy-network --ignition-url https://techoverflow.net/coreos.ign
[admin@CoreOS ~]$ docker run -d -p 22001:3000 --name=sshs --restart=on-failure wettyoss/wetty --ssh-host=192.168.2.40
