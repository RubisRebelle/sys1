# sys1
VSFTP
Sudo apt-get install vsftpd
Sudo service vsftp satuts
Service vsftpd start
# donner acces au parfeu de linux
Ufw allow 20/tcp
#configurer le serveur vsftpd
#faire une sauvgarde des fichiers de configurations
sudo cp /etc/vsftpd.conf /etc/vsftpd.conf.bak
#ouverture du fichier de config avec nano
Nano /etc/vsftpd.conf
Editer les suivants :
Anonymous_enable = YES
Local_enable = YES
Write_enable = YES
Chroot_local_user = YES
allow_writebale_chroot = YES
# Enable passive FTP
Pasv_min_port = 35000
Pasv_max_port = 40000
#redemarer le serveur
Sudo service restart vsftpd

# Description du serveur
VSFTPD est sécurisé et extrêmement rapide. Il est stable. Mais ne me croyez pas sur parole. Vous trouverez ci-dessous des preuves à l'appui de ces trois affirmations. Nous verrons également une liste de quelques sites importants qui utilisent volontiers vsftpd. Cela démontre que vsftpd est une solution mature et fiable.

Samba
# Description
Samba est un serveur utiliser pour communiquer de linux a windows, il possede 2 protocols :
SMB(Samba Message Block) et NMB (NetBios Message Block)
Les numerots de ports pour samba sont :
137, 138 – UDP
139, 445- TCP
# Installation
sudo apt-get install samba smbfs
#Configuration de Samba
Nano /etc/samba/smb.conf
Workgroup = WORKGROUP
# Cree un dossier de partage
Onitina's share
[MyShare]
  comment = test de partage
  path = /etc/user/radolaza/desktop
  read only = no
  guest ok = yes
# redemarer Samba
/etc/init.d/smbd restart
# cree un dossier partager
sudo mkdir /etc/user/radolaza/desktop
# donner les permission
sudo chmod 0777 /etc/user/radolaza/desktop


Apache
# description
Apache est un serveur web gratuit 
# Installation
Sudo apt-get install apache2
# aller a la tour de decision du dragon
cd /etc/apache2/sites-available/
sudo nano gci.conf
# Mettre l’email dans server admin
Serveradming hei.onitina@gmail.com
DocumentRoot /var/www/.


NFS
# description
NFS (Network File System) est un protocole de système de fichiers qui permet aux utilisateurs de visualiser et d'accéder aux fichiers et dossiers d'un système distant comme s'ils étaient stockés localement. Il s'agit d'une configuration client-serveur où le système qui partage le stockage est appelé le serveur, tandis que le système qui accède au stockage stocké sur un serveur est appelé le client. NFS permet aux utilisateurs ou aux administrateurs système de monter tout ou partie du système de fichiers d'un serveur sur le système du client. Les clients peuvent alors accéder aux fichiers montés en fonction des autorisations spécifiques (lecture, écriture) attribuées à ces fichiers.
# installation
sudo apt install nfs-kernel-system
# Creation du dossier d’exportation
sudo mkdir –p /mnt/sharedfolder
# configuration du dossier d’exportation
sudo nano /etc/exports
# pour assignier l’acces a un client
directory hostname(options)
# Configuration de firewall
sudo ufw allow from 192.168.72.0/24 to any port nfs
sudo ufw status
