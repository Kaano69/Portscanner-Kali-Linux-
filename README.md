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

## **3. Funktionsweise des Portscanners**  
Der Scanner nutzt die **`socket`**-Bibliothek, um eine Verbindung zu bestimmten Ports herzustellen. Die Hauptfunktionen sind:

- **`scan()`**  
  Diese Funktion iteriert über eine Liste von Ports und ruft `scan_port()` auf, um jeden einzelnen Port zu überprüfen.

- **`scan_port(port)`**  
  Diese Funktion versucht, eine Verbindung zu einem bestimmten Port herzustellen und prüft, ob er offen oder geschlossen ist.

- **`get_banner(socket)`**  
  Falls eine Verbindung zustande kommt, liest diese Funktion die ersten empfangenen Daten aus (Banner-Grabbing). Dies ist nützlich, um z. B. die Software-Version eines laufenden Dienstes zu identifizieren.

## **4. Anwendungsbeispiel**  
Im Beispiel wird die IP-Adresse der Webseite **„Heideldesign.de“** ermittelt und anschließend ein Portscan durchgeführt.  
Dieser Scan kann dabei helfen, potenzielle Schwachstellen zu identifizieren.
