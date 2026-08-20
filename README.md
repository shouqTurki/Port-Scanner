# basic_scanner.py
import socket

target_host = "scanme.nmap.org"
ports_to_scan = [22, 80, 443]

print(f"Scanning target: {target_host}")

for port in ports_to_scan:
    client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    client.settimeout(1.0)
    result = client.connect_ex((target_host, port))
    
    if result == 0:
        print(f"[+] Port {port}: OPEN")
    else:
        print(f"[-] Port {port}: CLOSED")
        
    client.close()

print("Scan completed successfully")
