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

1. Número de portas abertas identiﬁcadas: 14 portas
   
2. Serviços em execução em cada porta:
   *DNS (Port 53) - systemd-resolved;
   *SSH (Port 22) - OpenSSH;
   *DHCP Client (Port 68);
   *DHCPv6 Client (Port 546).

3. Versões exatas detetadas pelo Nmap: Tive problemas na Máquina atacante, ultrapassei mais que 1 hora por motivos do trabalho.

4. Output completo do comando ip a e ss -tuln do ambiente local:
   <img width="939" height="290" alt="Captura de ecrã 2026-07-14 155640" src="https://github.com/user-attachments/assets/e41caa53-ef54-4726-8ed9-0db5113228cf" />
<img width="936" height="294" alt="Captura de ecrã 2026-07-14 155621" src="https://github.com/user-attachments/assets/bcaac3c4-bc8b-49ed-a9db-24e66a9d1000" />

Durante este laboratório foi possível utilizar comandos essenciais do Linux para analisar a configuração da rede local e identificar serviços ativos.

git commit -m "M5 - Linux e Cibersegurança"
git push origin main
