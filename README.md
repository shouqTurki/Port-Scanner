# basic_scanner.py
import socket

target_host = "scanme.nmap.org"
ports_to_scan = [22, 80, 443]

print(f"--- بدء فحص الهدف: {target_host} ---")

for port in ports_to_scan:
    client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    client.settimeout(1.0)
    result = client.connect_ex((target_host, port))
    
    if result == 0:
        print(f"[+] المنفذ {port}: مفتوح (OPEN)")
    else:
        print(f"[-] المنفذ {port}: مغلق (CLOSED)")
        
    client.close()

print("--- تم الانتهاء من الفحص بنجاح ---")
