# Sessao-01
Mapeamento e análise da superfície de exposição de um servidor alvo na rede local.
O objetivo é identiﬁcar a interface de rede do próprio ambiente, listar os serviços em escuta e, de seguida, mapear um alvo remoto com o Nmap.

root@ubuntu:~$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute 
       valid_lft forever preferred_lft forever
2: enp1s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1450 qdisc fq_codel state UP group default qlen 1000
    link/ether 16:aa:ab:42:b2:78 brd ff:ff:ff:ff:ff:ff
    inet 172.30.1.2/24 brd 172.30.1.255 scope global dynamic noprefixroute enp1s0
       valid_lft 86308434sec preferred_lft 75519234sec
    inet6 fe80::ca5f:152d:48e9:d82e/64 scope link 
       valid_lft forever preferred_lft forever
3: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1454 qdisc noqueue state DOWN group default 
    link/ether a2:f2:4c:33:b4:57 brd ff:ff:ff:ff:ff:ff
    inet 172.17.0.1/16 brd 172.17.255.255 scope global docker0
       valid_lft forever preferred_lft forever

root@ubuntu:~$ ss -tuln
Netid     State      Recv-Q     Send-Q                               Local Address:Port            Peer Address:Port     Process     
udp       UNCONN     0          0                                       127.0.0.54:53                   0.0.0.0:*                    
udp       UNCONN     0          0                                    127.0.0.53%lo:53                   0.0.0.0:*                    
udp       UNCONN     0          0                                       172.30.1.2:68                   0.0.0.0:*                    
udp       UNCONN     0          0                                172.30.1.2%enp1s0:68                   0.0.0.0:*                    
udp       UNCONN     0          0               [fe80::ca5f:152d:48e9:d82e]%enp1s0:546                     [::]:*                    
tcp       LISTEN     0          4096                                     127.0.0.1:41083                0.0.0.0:*                    
tcp       LISTEN     0          128                                        0.0.0.0:40200                0.0.0.0:*                    
tcp       LISTEN     0          511                                        0.0.0.0:40205                0.0.0.0:*                    
tcp       LISTEN     0          4096                                 127.0.0.53%lo:53                   0.0.0.0:*                    
tcp       LISTEN     0          4096                                       0.0.0.0:22                   0.0.0.0:*                    
tcp       LISTEN     0          4096                                    127.0.0.54:53                   0.0.0.0:*                    
tcp       LISTEN     0          4096                                             *:40300                      *:*                    
tcp       LISTEN     0          4096                                             *:40305                      *:*                    
tcp       LISTEN     0          4096                                          [::]:22                      [::]:*  

root@ip-10-128-185-94:~# nmap -sV -sC 10.128.150.156
Starting Nmap 7.94SVN ( https://nmap.org ) at 2026-07-18 13:58 UTC
Nmap scan report for ip-10-128-150-156.eu-west-3.compute.internal (10.128.150.156)
Host is up (0.00033s latency).
Not shown: 995 filtered tcp ports (no-response)
PORT     STATE SERVICE       VERSION
21/tcp   open  ftp           FileZilla ftpd
| ftp-syst: 
|_  SYST: UNIX emulated by FileZilla
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_Can't get directory listing: TIMEOUT
53/tcp   open  domain        Simple DNS Plus
80/tcp   open  http          Microsoft IIS httpd 10.0
|_http-server-header: Microsoft-IIS/10.0
|_http-title: IIS Windows Server
| http-methods: 
|_  Potentially risky methods: TRACE
135/tcp  open  msrpc         Microsoft Windows RPC
3389/tcp open  ms-wbt-server Microsoft Terminal Services
|_ssl-date: 2026-07-18T13:59:41+00:00; -1s from scanner time.
| ssl-cert: Subject: commonName=win-scan
| Not valid before: 2026-07-17T13:50:52
|_Not valid after:  2027-01-16T13:50:52
| rdp-ntlm-info: 
|   Target_Name: WIN-SCAN
|   NetBIOS_Domain_Name: WIN-SCAN
|   NetBIOS_Computer_Name: WIN-SCAN
|   DNS_Domain_Name: win-scan
|   DNS_Computer_Name: win-scan
|   Product_Version: 10.0.17763
|_  System_Time: 2026-07-18T13:59:11+00:00
MAC Address: 06:5A:C3:A1:66:15 (Unknown)
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_clock-skew: mean: -1s, deviation: 0s, median: -1s

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 54.37 seconds

1. Número de portas abertas identiﬁcadas: 5 portas
   
2. Serviços em execução em cada porta:
 PORT    SERVICE       
  21      ftp
  53      domain
  80      http
  135     msrpc
  3389    ms-wbt-server

4. Versões exatas detetadas pelo Nmap: 
PORT          VERSION
21/tcp     FileZilla ftpd
53/tcp     Simple DNS Plus
80/tcp     Microsoft IIS httpd 10.0
135/tcp    Microsoft Windows RPC
3389/tcp   Microsoft Terminal Services

5. Output completo do comando ip a  e  ss -tuln do ambiente local:
   <img width="939" height="290" alt="Captura de ecrã 2026-07-14 155640" src="https://github.com/user-attachments/assets/e41caa53-ef54-4726-8ed9-0db5113228cf" />
<img width="936" height="294" alt="Captura de ecrã 2026-07-14 155621" src="https://github.com/user-attachments/assets/bcaac3c4-bc8b-49ed-a9db-24e66a9d1000" />

Durante este laboratório foi possível utilizar comandos essenciais do Linux para analisar a configuração da rede local e identificar serviços ativos.

git commit -m "M5 - Linux e Cibersegurança"
git push origin main
