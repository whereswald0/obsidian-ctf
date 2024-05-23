# Nmap

Quick Scan all ports
```bash
sudo nmap -p- —min-rate 5000 -v -oA file
```
### fast scanning
##### top 1000 TCP ports
`nmap -sV -sC -O -T4 -n -Pn -oA fastscan`
##### all the ports
`nmap -sV -sC -O -T4 -n -Pn -p- -oA fullfastscan`
##### all the ports (slower)
> slower to avoid failures due to -T4
 
`nmap -sV -sC -O -p- -n -Pn -oA fullscan`
# Bettercap 
`syn.scan 192.168.1.0/24 1 10000 #Ports 1-10000`