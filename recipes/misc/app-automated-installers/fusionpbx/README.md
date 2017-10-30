# FUSIONPBX/FREESWITCH AUTOMATED INSTALLER FOR CENTOS7

This script will install a FusionPBX/Freeswitch VoIP PBX on Centos 7.

All credentials are auto-generated by the script, and stored on the files "/root/fusionpbx-credentials.txt" and "/root/fusionpbx-install-information.log". Also, almost all outputs by actions generated during the running of this scripts will be logged to the file "/var/log/fusionpbx-automated-installer.log".

# FIREWALLD

This script will initially open port ssh but during the installation, FusionPBX automation scripts will open several other ports (udp and tcp) needed for normal VoIP operations:

```bash
iptables -L -n|grep dpt.\*NEW

ACCEPT     tcp  --  0.0.0.0/0            0.0.0.0/0            tcp dpt:22 ctstate NEW
ACCEPT     tcp  --  0.0.0.0/0            0.0.0.0/0            tcp dpt:80 ctstate NEW
ACCEPT     tcp  --  0.0.0.0/0            0.0.0.0/0            tcp dpt:443 ctstate NEW
ACCEPT     udp  --  0.0.0.0/0            0.0.0.0/0            udp dpt:1194 ctstate NEW
ACCEPT     udp  --  0.0.0.0/0            0.0.0.0/0            udp dpt:5060 ctstate NEW
ACCEPT     udp  --  0.0.0.0/0            0.0.0.0/0            udp dpt:5061 ctstate NEW
ACCEPT     udp  --  0.0.0.0/0            0.0.0.0/0            udp dpt:5080 ctstate NEW
ACCEPT     udp  --  0.0.0.0/0            0.0.0.0/0            udp dpt:5081 ctstate NEW
ACCEPT     tcp  --  0.0.0.0/0            0.0.0.0/0            tcp dpt:5060 ctstate NEW
ACCEPT     tcp  --  0.0.0.0/0            0.0.0.0/0            tcp dpt:5061 ctstate NEW
ACCEPT     tcp  --  0.0.0.0/0            0.0.0.0/0            tcp dpt:5080 ctstate NEW
ACCEPT     tcp  --  0.0.0.0/0            0.0.0.0/0            tcp dpt:5081 ctstate NEW
ACCEPT     udp  --  0.0.0.0/0            0.0.0.0/0            udp dpts:16384:32768 ctstate NEW
```

Please note that SELINUX will be disabled by this script.


# LETSENCRYPT

This script will install "certbot" (letsencrypt software) and set the required crontab for automated renewall. The "ssl" certificate on nginx is "self-signed". Use "certbot" to adquire a valid certificate from letsencrypt.


# SPANISH AUDIO SUPPORT

This script will add spanish audio support (including formats for 8Khz, 16Khz, 32Khz and 44Khz) under "/usr/share/freeswitch/sounds/es/mx/maria". If you want to switch to "spanish" audio, change your default language in "/etc/freeswitch/vars.xml":

```bash
<!-- Sets the sound directory. -->
#<X-PRE-PROCESS cmd="set" data="sound_prefix=$${sounds_dir}/en/us/callie" />
<X-PRE-PROCESS cmd="set" data="sound_prefix=$${sounds_dir}/es/mx/maria"/>
<X-PRE-PROCESS cmd="set" data="default_language=es"/>
```

And restart freeswitch:

```bash
systemctl restart freeswitch
```


# GENERAL REQUIREMENTS:

This script will fail if the following requirements are not meet:

- Operating System: Centos 7
- Architecture: x86_64/amd64.
- INSTALLED RAM: 2048Mb (2GB).
- CPU: 2 Core/Thread.
- FREE DISK SPACE: 5GB.