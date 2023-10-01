# blue
blue-intelj1800

[[https://techoverflow.net/2021/06/14/a-simple-coreos-config-for-beginners-with-password-login/]]

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
