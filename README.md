# blue
blue-intelj1800

[[https://techoverflow.net/2021/06/14/a-simple-coreos-config-for-beginners-with-password-login/]]
[[https://kt-hiro.hatenablog.com/entry/20140808/1407515284#:~:text=%E3%83%BB%E5%89%B2%E3%82%8A%E5%BD%93%E3%81%A6%E3%82%89%E3%82%8C%E3%81%9F%20IP%E3%82%A2%E3%83%89%E3%83%AC%E3%82%B9%20%E3%81%AE%E7%A2%BA%E8%AA%8D%20%24%20ip%20adde%20show%20%E3%83%BBcore%E3%83%A6%E3%83%BC%E3%82%B6%E3%81%AE%E3%83%91%E3%82%B9%E3%83%AF%E3%83%BC%E3%83%89%E5%A4%89%E6%9B%B4,%23%20ssh%20core%40%E2%80%98%E2%80%99IP%E3%82%A2%E3%83%89%E3%83%AC%E3%82%B9%E2%80%9D%20%E3%83%BB%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB%E5%BE%8C%E3%81%AE%20ssh%20%E6%8E%A5%E7%B6%9A%E7%94%A8%E3%83%91%E3%82%B9%E3%83%AF%E3%83%BC%E3%83%89%E3%81%AE%20%E3%83%8F%E3%83%83%E3%82%B7%E3%83%A5%E5%80%A4%20%E3%81%AE%E5%8F%96%E5%BE%97]]
[[https://github.com/coreos/container-linux-config-transpiler/]]

```
podman run -ti --rm quay.io/coreos/mkpasswd --method=yescrypt
podman run -i --rm quay.io/coreos/fcct:release --pretty --strict < ignition.yaml > ignition.ign            # podman -> docker
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
{	
  "ignition": {
    "version": "3.0.0"
  },
  "passwd": {
    "users": [
      {
        "groups": [
          "sudo",
          "docker"
        ],
        "name": "admin",
        "passwordHash": "$y$j9T$n6h8P2ik8tfoNUFBBoly00$7bnrMF8oFrB25Fc3NqigqEH/MI5YXIJwtCG/iEsns.2"
      }
    ]
  },
  "storage": {
    "files": [
      {
        "contents": {
          "source": "data:,CoreOS%0A"
        },
        "mode": 420,
        "path": "/etc/hostname"
      },
      {
        "contents": {
          "source": "data:,%23%20Tell%20systemd%20to%20not%20use%20a%20pager%20when%20printing%20information%0Aexport%20SYSTEMD_PAGER%3Dcat%0A"
        },
        "mode": 420,
        "path": "/etc/profile.d/systemd-pager.sh"
      },
      {
        "contents": {
          "source": "data:,%23%20Raise%20console%20message%20logging%20level%20from%20DEBUG%20(7)%20to%20WARNING%20(4)%0A%23%20to%20hide%20audit%20messages%20from%20the%20interactive%20console%0Akernel.printk%3D4%0A"
        },
        "mode": 420,
        "path": "/etc/sysctl.d/20-silence-audit.conf"
      },
      {
        "contents": {
          "source": "data:,%23%20Enable%20SSH%20password%20login%0APasswordAuthentication%20yes%0A"
        },
        "mode": 420,
        "path": "/etc/ssh/sshd_config.d/20-enable-passwords.conf"
      }
    ]
  },
  "systemd": {
    "units": [
      {
        "enabled": true,
        "name": "docker.service"
      },
      {
        "enabled": true,
        "name": "containerd.service"
      },
      {
        "dropins": [
          {
            "contents": "[Service]\n# Override Execstart in main unit\nExecStart=\n# Add new Execstart with `-` prefix to ignore failure\nExecStart=-/usr/sbin/agetty --autologin admin --noclear %I $TERM\nTTYVTDisallocate=no\n",
            "name": "autologin-core.conf"
          }
        ],
        "name": "serial-getty@ttyS0.service"
      }
    ]
  }
}
```
