# LIMESURVEY AUTOMATED INSTALLATION FOR CENTOS 7 (WITH MARIADB 10.1)

This script will do a basic distribution setup with some usefull packages, then install both MariaDB 10.1 and LimeSurvey (latest stable). The credentials will be autogenerated and stored inside the file "/root/limesurvey-and-mariadb-access-info.txt".

The script will log some of its activities to the file "/var/log/limesurvey-automated-installer.log".

Please note that this script will disable selinux.

# LETSENCRYPT

This script will install "certbot" (letsencrypt software) and set the required crontab for automated renewall. The "ssl" certificate on apache is "self-signed". Use "certbot" to adquire a valid certificate from letsencrypt.


# OPENED PORTS

FirewallD allow traffic for the following ports only (input traffic):

- 80 tcp (http).
- 443 tcp (https).
- 22 tcp (ssh).


# GENERAL REQUIREMENTS:

This script will fail if the following requirements are not meet:

- Operating System: Centos 7.
- Architecture: x86_64/amd64.
- INSTALLED RAM: 1024Mb (1GB).
- CPU: 1 Core/Thread.
- FREE DISK SPACE: 5GB.
