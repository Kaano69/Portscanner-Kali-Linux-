# **Portscanner in Kali Linux**  

## **1. Projektübersicht**  
Dieses Projekt beschreibt die Erstellung eines einfachen Portscanners in Kali Linux mithilfe von Python. Der Scanner 
überprüft offene Ports einer Ziel-IP-Adresse und kann zusätzlich Banner-Informationen auslesen, sofern eine Software auf dem Port läuft.

## **2. Einrichtung der Arbeitsumgebung**  
### **Python-Verzeichnis erstellen**  
Zunächst wird ein neues Verzeichnis für das Projekt erstellt:  
```bash
mkdir Python
cd Python
```
Anschließend wird das Python-Skript mit folgendem Befehl angelegt:  
```bash
cat > portscan.py
```
Nun kann der Code direkt im Terminal geschrieben oder eine bevorzugte Entwicklungsumgebung genutzt werden.
<br>![Screenshot vom Desktop](https://imgur.com/JPRVzTA)

## **3. Portscanner-Code**  
Der folgende Code stellt die Funktionsweise des Portscanners dar:
```python
import socket
from termcolor import colored

def scan(target,ports):
    print('\n' + '*** Starting Scan For' + str(target) + ' ***')
    for port in range(1, ports):
        scan_port(target, port)

def get_banner(s):
    return s.recv(1024)

def scan_port(ipaddress, port):
    try:
        sock = socket.socket()
        sock.settimeout(0.3)
        sock.connect((ipaddress, port))
        try:
            banner = get_banner(sock)
            print('[+] Open Port ' + str(port) + ' :' + str(banner.decode().strip('\n')))
        except:
            print('[+] Open Port ' +str(port))
        sock.close()
    except:
        pass

targets = input('[+] Enter target To Scan: ')
ports = int(input('[+] Enter How Many Ports You Want To Scan: '))
if ',' in targets:
    print(colored(("\n[*] Scanning Multiple targets [*]\n"), 'green'))
    for ip_add in targets.split(','):
        scan(ip_add.strip(' '),ports)
else:
    scan(targets,ports)
```

## **4. Funktionsweise des Portscanners**  
Der Scanner nutzt die **`socket`**-Bibliothek, um eine Verbindung zu bestimmten Ports herzustellen. Die Hauptfunktionen sind:

- **`scan()`**  
  Diese Funktion iteriert über eine Liste von Ports und ruft `scan_port()` auf, um jeden einzelnen Port zu überprüfen.

- **`scan_port(port)`**  
  Diese Funktion versucht, eine Verbindung zu einem bestimmten Port herzustellen und prüft, ob er offen oder geschlossen ist.

- **`get_banner(socket)`**  
  Falls eine Verbindung zustande kommt, liest diese Funktion die ersten empfangenen Daten aus (Banner-Grabbing). Dies ist nützlich, um z. B. die Software-Version eines laufenden Dienstes zu identifizieren.

## **5. Anwendungsbeispiel**  
![Beispiel Scan](https://imgur.com/JPRVzTA) <br>
Im Beispiel wird die IP-Adresse der Webseite **„Heideldesign.de“** ermittelt und anschließend ein Portscan durchgeführt.  
Dieser Scan kann dabei helfen, potenzielle Schwachstellen zu identifizieren.
