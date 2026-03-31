Proxy

http://http=127.0.0.1     Port 8080

46.17.47.48

----------------------------------
------------------

Install the New Version OPENVPN 

https://openvpn.net/community/

Customize: OpenSSL Utilities (EasyRSA 3 Certificate Management Scripts)((: Click Take 2 (3*1=X)

Install

-------------------------------

Install the Old Version other Folder 

https://gist.github.com/fitz123/b28e0baf376dbe2e4937

Copy The Old Version in the New OPENVPN Admin Yes Step by Step 

https://openvpn.net/community/

--------------------------------------------------------------

Client Server Install Here

https://www.youtube.com/watch?v=GwhBdOGlglc&t=105s

file:///C:/Users/pingu/AppData/Local/Microsoft/Windows/INetCache/IE/0DK7BR8G/openvpnwin[1].pdf

----------------------------------------------------------------------------------------------
--------------------------------------------------------------

cd C:\Program Files\OpenVPN\easy-rsa

EasyRSA-Start.bat

./easyrsa init-pki 

./easyrsa build-ca nopass

./easyrsa build-server-full server nopass

./easyrsa build-client-full client1 nopass

./easyrsa gen-dh

exit

openvpn --genkey secret ta.key


---------- server.ovpn ----------------

# Specify a port, a protocol and a device type
port 1194
proto udp
dev tun
# Specify paths to server certificates
ca "C:\\Program Files\\OpenVPN\\easy-rsa\\pki\\ca.crt"
cert "C:\\Program Files\\OpenVPN\\easy-rsa\\pki\\issued\\server.crt"
key "C:\\Program Files\\OpenVPN\\easy-rsa\\pki\\private\\server.key"
dh "C:\\Program Files\\OpenVPN\\easy-rsa\\pki\\dh.pem"
# Specify the settings of the IP network your VPN clients will get their IP addresses from
server 10.24.1.0 255.255.255.0
push "redirect-gateway def1"
# If you want to allow your clients to connect using the same key, enable the duplicate-cn option (not recommended)
# duplicate-cn
# TLS protection
tls-auth "C:\\Program Files\\OpenVPN\\easy-rsa\\pki\\ta.key" 0
cipher AES-256-GCM
# Other options
keepalive 20 60
persist-key
persist-tun
status "C:\\Program Files\\OpenVPN\\log\\status.log"
log "C:\\Program Files\\OpenVPN\\log\\openvpn.log"
verb 3

----------- IPEnableRouter in Registry -----------

HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters

------------ client.ovpn --------------

client
dev tun
proto udp
remote your_vpn_server_public_ip 1194
resolv-retry infinite
nobind
persist-key
persist-tun
ca ca.crt
cert client1.crt
key client1.key
remote-cert-tls server
tls-auth ta.key 1
cipher AES-256-GCM
connect-retry-max 25
verb 3

--------- Files Directory ---------

C:\Program Files\OpenVPN\easy-rsa\pki\ca.cert
C:\Program Files\OpenVPN\easy-rsa\pki\dh.pem
C:\Program Files\OpenVPN\easy-rsa\pki\ta.key

C:\Program Files\OpenVPN\easy-rsa\pki\issued\client1.crt
C:\Program Files\OpenVPN\easy-rsa\pki\private\client1.key
---------------------------------------------------------
-------------------------------------

Download OpenVPN https://openvpn.net/community-downloads/
Server server.ovpn file:
port 1194
proto udp
dev tun
ca ca.crt
cert server.crt
key server.key
dh dh.pem
server 10.50.8.0 255.255.255.0
ifconfig-pool-persist ipp.txt
keepalive 10 120
comp-lzo
persist-key
persist-tun
status openvpn-status.log
verb 3
Client client.ovpn file:
client
dev tun
proto udp
remote PUBLIC_IP 1194
resolv-retry infinite
nobind
persist-key
persist-tun
ca ca.crt
cert client01.crt
key client01.key
comp-lzo
verb 3
Type the following commands to enter inside EasyRSA shell:
 C:\Windows\system32 cd C:\Program Files\OpenVPN\easy-rsa
 C:\Program Files\OpenVPN\easy-rsa\ EasyRSA-Start.bat
Remove existing configuration:
 ./easyrsa clean-all
Initialize pki, and type yes to confirm
 ./easyrsa init-pki
Build certificate authority
 ./easyrsa build-ca nopass
Build server certificate and key
 ./easyrsa build-server-full server nopass
Generate Diffie Hellman parameters :
 ./easyrsa gen-dh
Generating client certificates :
 ./easyrsa build-client-full client01 nopass
Put this files (from C:\Program Files\OpenVPN\easy-rsa\pki, C:\
Program Files\OpenVPN\easy-rsa\pki\issued and C:\Program Files\
OpenVPN\easy-rsa\pki\private) :
ca.crt
dh.pem
server.crt
server.key
To C:\Program Files\OpenVPN\config-auto and C:\Program Files\
OpenVPN\config folders
From the Server get the following files (from C:\Program Files\
OpenVPN\easy-rsa\pki, C:\Program Files\OpenVPN\easy-rsa\pki\
issued and C:\Program Files\OpenVPN\easy-rsa\pki\private) :
ca.crt
client01.crt
client01.key
and paste them to C:\Program Files\OpenVPN\config
