# basic_scanner.py
import socket

# 1. تحديد الهدف (يمكنك كتابة اسم موقع أو IP داخلي)
target_host = "scanme.nmap.org"  # هذا موقع رسمي ومجاني مخصص ومسموح لفحص الثغرات تجريبياً

# 2. تحديد قائمة المنافذ التي نرغب في فحصها (أشهر منافذ الويب والخدمات)
ports_to_scan = [21, 22, 80, 443]

print(f"--- بدء فحص الهدف: {target_host} ---")

# 3. حلقة تكرارية للمرور على كل منفذ وفحصه
for port in ports_to_scan:
    # إنشاء اتصال شبكة باستخدام بروتوكول TCP
    client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    
    # تحديد مهلة زمنية ثانية واحدة للرد لحماية الأداة من التعليق
    client.settimeout(1.0)
    
    # محاولة الاتصال بالمنفذ
    result = client.connect_ex((target_host, port))
    
    # إذا كانت النتيجة (0) فالمنفذ مفتوح، وإلا فهو مغلق
    if result == 0:
        print(f"[+] المنفذ {port}: مفتوح (OPEN)")
    else:
        print(f"[-] المنفذ {port}: مغلق (CLOSED)")
        
    # إغلاق الاتصال بعد الفحص
    client.close()

print("--- تم الانتهاء من الفحص بنجاح ---")
