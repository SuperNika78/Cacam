Web Game

# Server Spesification
1. Apache2 (Web Server)
2. OpenSSH (SSH Server)
3. Bind9 (DNS Server)
4. Fail2Ban (Intrusion Prevention System)
5. Vsftpd (FTP Server)

# SSH
**Install SSH Server**
```
sudo apt install openssh-server
```

**Jalankan SSH Server**
```
sudo systemctl start ssh
```

**Enable SSH**
```
sudo systemctl enable ssh
```

# Apache Web Server
**Install apache**
```
sudo apt install apache2
```
**Enable apache**
```
sudo enable apache2
```

# Install File Game
**Install git terlebih dahulu**
```
sudo apt install git
```

**Install game**
```
git clone https://github.com/BKcore/HexGL.git
```

**Pindahkan isi file game ke /var/www/html**
```
sudo mv HexGL/* /var/www/html
```

**Jalankan Apache**
```
sudo systemctl start apache2
```

**Akses Web Server**
![image](https://github.com/user-attachments/assets/899cc365-d022-4a5c-9cb2-d220e835ccc5)
![image](https://github.com/user-attachments/assets/1fd362ce-6acc-4574-b22d-b0b55a6ab99e)

# FTP Server

**Install FTP Server**
```
sudo apt install vsftpd
```

**Buat Direktori Untuk FTP** 
```
mkdir $HOME/ftp
```

**Konfigurasi FTP**
```
sudo nano /etc/vsftpd.conf

# Example config file /etc/vsftpd.conf
#
# The default compiled in settings are fairly paranoid. This sample file
# loosens things up a bit, to make the ftp daemon more usable.
# Please see vsftpd.conf.5 for all compiled in defaults.
#
# READ THIS: This example file is NOT an exhaustive list of vsftpd options.
# Please read the vsftpd.conf.5 manual page to get a full idea of vsftpd's
# capabilities.
#
#
# Run standalone?  vsftpd can run either from an inetd or as a standalone
# daemon started from an initscript.
listen=NO
#
# This directive enables listening on IPv6 sockets. By default, listening
# on the IPv6 "any" address (::) will accept connections from both IPv6
# and IPv4 clients. It is not necessary to listen on *both* IPv4 and IPv6
# sockets. If you want that (perhaps because you want to listen on specific
# addresses) then you must run two copies of vsftpd with two configuration
# files.
listen_ipv6=YES
#
# Allow anonymous FTP? (Disabled by default).
anonymous_enable=NO
#
# Uncomment this to allow local users to log in.
local_enable=YES
#
# Uncomment this to enable any form of FTP write command.
write_enable=YES
#
# Default umask for local users is 077. You may wish to change this to 022,
# if your users expect that (022 is used by most other ftpd's)
#local_umask=022
#
# Uncomment this to allow the anonymous FTP user to upload files. This only
# has an effect if the above global write enable is activated. Also, you will
# obviously need to create a directory writable by the FTP user.
#anon_upload_enable=YES
#
# Uncomment this if you want the anonymous FTP user to be able to create
# new directories.
#anon_mkdir_write_enable=YES
#
# Activate directory messages - messages given to remote users when they
# go into a certain directory.
dirmessage_enable=YES
#
# If enabled, vsftpd will display directory listings with the time
# in  your  local  time  zone.  The default is to display GMT. The
# times returned by the MDTM FTP command are also affected by this
# option.
use_localtime=YES
#
# Activate logging of uploads/downloads.
xferlog_enable=YES
#
# Make sure PORT transfer connections originate from port 20 (ftp-data).
connect_from_port_20=YES
#
# If you want, you can arrange for uploaded anonymous files to be owned by
# a different user. Note! Using "root" for uploaded files is not
# recommended!
#chown_uploads=YES
#chown_username=whoever
#
# You may override where the log file goes if you like. The default is shown
# below.
#xferlog_file=/var/log/vsftpd.log
#
# If you want, you can have your log file in standard ftpd xferlog format.
# Note that the default log file location is /var/log/xferlog in this case.
#xferlog_std_format=YES
#
# You may change the default value for timing out an idle session.
#idle_session_timeout=600
#
# You may change the default value for timing out a data connection.
#data_connection_timeout=120
#
# It is recommended that you define on your system a unique user which the
# ftp server can use as a totally isolated and unprivileged user.
#nopriv_user=ftpsecure
#
# Enable this and the server will recognise asynchronous ABOR requests. Not
# recommended for security (the code is non-trivial). Not enabling it,
# however, may confuse older FTP clients.
#async_abor_enable=YES
#
# By default the server will pretend to allow ASCII mode but in fact ignore
# the request. Turn on the below options to have the server actually do ASCII
# mangling on files when in ASCII mode.
# Beware that on some FTP servers, ASCII support allows a denial of service
# attack (DoS) via the command "SIZE /big/file" in ASCII mode. vsftpd
# predicted this attack and has always been safe, reporting the size of the
# raw file.
# ASCII mangling is a horrible feature of the protocol.
#ascii_upload_enable=YES
#ascii_download_enable=YES
#
# You may fully customise the login banner string:
#ftpd_banner=Welcome to blah FTP service.
#
# You may specify a file of disallowed anonymous e-mail addresses. Apparently
# useful for combatting certain DoS attacks.
#deny_email_enable=YES
# (default follows)
#banned_email_file=/etc/vsftpd.banned_emails
#
# You may restrict local users to their home directories.  See the FAQ for
# the possible risks in this before using chroot_local_user or
# chroot_list_enable below.
#chroot_local_user=YES
#
# You may specify an explicit list of local users to chroot() to their home
# directory. If chroot_local_user is YES, then this list becomes a list of
# users to NOT chroot().
# (Warning! chroot'ing can be very dangerous. If using chroot, make sure that
# the user does not have write access to the top level directory within the
# chroot)
chroot_local_user=YES
#chroot_list_enable=YES
# (default follows)
#chroot_list_file=/etc/vsftpd.chroot_list
#
# You may activate the "-R" option to the builtin ls. This is disabled by
# default to avoid remote users being able to cause excessive I/O on large
# sites. However, some broken FTP clients such as "ncftp" and "mirror" assume
# the presence of the "-R" option, so there is a strong case for enabling it.
#ls_recurse_enable=YES
#
# Customization
#
# Some of vsftpd's settings don't fit the filesystem layout by
# default.
#
# This option should be the name of a directory which is empty.  Also, the
# directory should not be writable by the ftp user. This directory is used
# as a secure chroot() jail at times vsftpd does not require filesystem
# access.
secure_chroot_dir=/var/run/vsftpd/empty
#
# This string is the name of the PAM service vsftpd will use.
pam_service_name=vsftpd
#
# This option specifies the location of the RSA certificate to use for SSL
# encrypted connections.
rsa_cert_file=/etc/ssl/certs/ssl-cert-snakeoil.pem
rsa_private_key_file=/etc/ssl/private/ssl-cert-snakeoil.key
ssl_enable=NO

#
# Uncomment this to indicate that vsftpd use a utf8 filesystem.
#utf8_filesystem=YES
user_sub_token=$USER
local_root=/home/$USER/ftp
allow_writeable_chroot=YES
userlist_enable=YES
userlist_file=/etc/vsftpd.userlist
userlist_deny=NO
```

**Tambahkan User FTP**
```
echo "cacam" | sudo tee -a /etc/vsftpd.userlist
```

# Fail2ban
Secara default bila user salah memasukkan password ssh dan ftp sebanyak 5 kali, maka akan diblokir selama 10 menit
**Install Fail2Ban**
```
sudo apt install fail2ban
```

**Enable fail2ban**
```
sudo systemctl enable fail2ban
```

**Aktifkan fail2ban untuk vsftpd**
```
sudo nano /etc/fail2ban/jail.conf

# Pergi ke line 554 atau cari kata **vsftpd** dengan tombol ctrl+w
# Tambahkan baris berikut di atas **port**
enabled = true
```

**Restat fail2ban**
```
sudo systemctl restart fail2ban
```

# DNS Server
**Install BIND9**
```
sudo apt install bind9 bind9-utils -y

**Konfigurasi DNS Server**
sudo cp /etc/bind/db.127 /etc/bind/db.ip
sudo cp /etc/bind/db.local /etc/bind/db.domain
```

**Edit file db.domain**
```
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     gamebalap.id. root.gamebalap.id. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      gamebalap.id.
@       IN      A       192.168.18.231
```

**Edit file db.ip**
```
;
; BIND reverse data file for local loopback interface
;
$TTL    604800
@       IN      SOA     gamebalap.id. root.gamebalap.id. (
                              1         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      gamebalap.id.
231     IN      PTR     gamebalap.id.
```

**Edit named.conf.local**
```
//
// Do any local configuration here
//

// Consider adding the 1918 zones here, if they are not used in your
// organization
//include "/etc/bind/zones.rfc1918";

zone "gamebalap.id"{
        type master;
        file "/etc/bind/db.domain";
};

zone "18.168.192.in-addr.arpa"{
        type master;
        file "/etc/bind/db.ip";
};
```

**Selanjutnya, konfigurasi named.conf.option**
```
options {
        directory "/var/cache/bind";

        // If there is a firewall between you and nameservers you want
        // to talk to, you may need to fix the firewall to allow multiple
        // ports to talk.  See http://www.kb.cert.org/vuls/id/800113

        // If your ISP provided one or more IP addresses for stable
        // nameservers, you probably want to use them as forwarders.
        // Uncomment the following block, and insert the addresses replacing
        // the all-0's placeholder.

        forwarders {
        8.8.8.8;
        };

        //========================================================================
        // If BIND logs error messages about the root key being expired,
        // you will need to update your keys.  See https://www.isc.org/bind-keys
        //========================================================================
        dnssec-validation no;

        listen-on-v6 { any; };
};
```

**Selanjutnya restart bind9**
```
sudo systemctl restart bind9.service
```
