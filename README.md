# basic_scanner.py
import socket
import random
import time

def basic_scan(target_host, ports):
    print(f"\n--- Starting Standard Scan on: {target_host} ---")
    for port in ports:
        client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        client.settimeout(1.0)
        result = client.connect_ex((target_host, port))
        if result == 0:
            print(f"[+] Port {port}: OPEN")
        else:
            print(f"[-] Port {port}: CLOSED")
        client.close()
    print("--- Standard Scan Completed ---")

def stealth_scan(target_host, ports):
    print(f"\n--- Starting Stealth Scan on: {target_host} ---")
    print("Shuffling ports and adding randomized delays for evasion...")
    random.shuffle(ports)
    for port in ports:
        delay = random.uniform(1.5, 3.5)
        time.sleep(delay)
        client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        client.settimeout(1.5)
        result = client.connect_ex((target_host, port))
        if result == 0:
            print(f"[+] Discovered Open Port: {port}")
        client.close()
    print("--- Stealth Scan Completed ---")

# --- Main Program Execution ---
if __name__ == "__main__":
    target = "scanme.nmap.org"
    common_ports = [22, 80, 443]
    
    print("====================================")
    print("    WELCOME TO PYTHON PORT SCANNER  ")
    print("====================================")
    print("1. Standard Scan (Fast)")
    print("2. Stealth Scan (Anti-Detection)")
    
    # محاكاة اختيار المستخدم للوضع الافتراضي
    choice = "1" 
    
    if choice == "1":
        basic_scan(target, common_ports)
    elif choice == "2":
        stealth_scan(target, common_ports)
