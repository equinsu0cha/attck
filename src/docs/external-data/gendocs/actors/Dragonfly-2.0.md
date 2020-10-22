
# Dragonfly 2.0

```
    .___                                    _____.__             ________     
  __| _/___________     ____   ____   _____/ ____\  | ___.__.    \_____  \    
 / __ |\_  __ \__  \   / ___\ /  _ \ /    \   __\|  |<   |  |     /  ____/    
/ /_/ | |  | \// __ \_/ /_/  >  <_> )   |  \  |  |  |_\___  |    /       \    
\____ | |__|  (____  /\___  / \____/|___|  /__|  |____/ ____|____\_______ \ /\
     \/            \//_____/             \/           \/   /_____/       \/ \/
_______   
\   _  \  
/  /_\  \ 
\  \_/   \
 \_____  /
       \/ 

```

## Description

### MITRE Description

> [Dragonfly 2.0](https://attack.mitre.org/groups/G0074) is a suspected Russian group that has targeted government entities and multiple U.S. critical infrastructure sectors since at least March 2016. (Citation: US-CERT TA18-074A) (Citation: Symantec Dragonfly Sept 2017) There is debate over the extent of overlap between [Dragonfly 2.0](https://attack.mitre.org/groups/G0074) and [Dragonfly](https://attack.mitre.org/groups/G0035), but there is sufficient evidence to lead to these being tracked as two separate groups. (Citation: Fortune Dragonfly 2.0 Sept 2017)

### External Description

> Active

## Aliases

```
Dragonfly 2.0
Berserk Bear
```

## Known Tools

```
Havex RAT
Oldrea
LightsOut ExploitKit
Inveigh
PsExec
Persistence through .LNK file manipulations
Nmap
Dirsearch
Sqlmap
Sublist3r
Wpscan
Impacket
SMBTrap
Commix
Subbrute
PHPMailer
Web Shells (PHP)
MCMD
```

## Operations

```

```

## Targets

```
This threat actor targets companies in the education, energy, construction, information technology, and pharmaceutical sectors for the purposes of espionage. It uses malware tailored to target industrial control systems. Energy, Middle East oil and natural gas as the goal, dedicated to gather relevant information, technology company in Western Europe that produces civil, military and critical infrastructure communications equipment
```

## Attribution Links

```
http://www.symantec.com/content/en/us/enterprise/media/security_response/whitepapers/Dragonfly_Threat_Against_Western_Energy_Suppliers.pdf
http://www.netresec.com/?page=Blog&month=2014-10&post=Full-Disclosure-of-Havex-Trojans
https://threatpost.com/energy-watering-hole-attack-used-lightsout-exploit-kit/104772/
https://www.symantec.com/connect/blogs/dragonfly-western-energy-sector-targeted-sophisticated-attack-group
https://securelist.com/blog/incidents/35520/the-teamspy-crew-attacks-abusing-teamviewer-for-cyberespionage-8/
https://www.us-cert.gov/ncas/alerts/TA17-293A
https://threatmatrix.cylance.com/en_us/home/energetic-dragonfly-dymalloy-bear-2-0.html
https://securelist.com/energetic-bear-crouching-yeti/85345/
https://www.fireeye.com/content/dam/fireeye-www/company/events/infosec/threat-landscape-overview-fireeye-summit-paris.pdf
https://insights.sei.cmu.edu/cert/2019/03/api-hashing-tool-imagine-that.html
https://www.secureworks.com/research/updated-karagany-malware-targets-energy-sector
https://www.secureworks.com/research/mcmd-malware-analysis
https://www.secureworks.com/blog/own-the-router-own-the-traffic
```

## Country

```
russia
```

## Comments

```
Detected in Middle East networks in 2014, Compromise via spear phish or SWC, Motivation somewhat unclear; CrowdStrike lists Berserk Bear as separate group (evolution of Energetic) while Symantec sees Energetic Bear and Berserk Bear as single group named Dragonfly
```

# Techniques


* [Masquerading](../techniques/Masquerading.md)

* [Domain Groups](../techniques/Domain-Groups.md)
    
* [Malicious File](../techniques/Malicious-File.md)
    
* [Command and Scripting Interpreter](../techniques/Command-and-Scripting-Interpreter.md)
    
* [Application Layer Protocol](../techniques/Application-Layer-Protocol.md)
    
* [Local Account](../techniques/Local-Account.md)
    
* [Disable or Modify System Firewall](../techniques/Disable-or-Modify-System-Firewall.md)
    
* [Modify Registry](../techniques/Modify-Registry.md)
    
* [Template Injection](../techniques/Template-Injection.md)
    
* [Remote Email Collection](../techniques/Remote-Email-Collection.md)
    
* [Drive-by Compromise](../techniques/Drive-by-Compromise.md)
    
* [Security Account Manager](../techniques/Security-Account-Manager.md)
    
* [Remote System Discovery](../techniques/Remote-System-Discovery.md)
    
* [Clear Windows Event Logs](../techniques/Clear-Windows-Event-Logs.md)
    
* [Scheduled Task](../techniques/Scheduled-Task.md)
    
* [File and Directory Discovery](../techniques/File-and-Directory-Discovery.md)
    
* [Network Share Discovery](../techniques/Network-Share-Discovery.md)
    
* [Valid Accounts](../techniques/Valid-Accounts.md)
    
* [Data from Local System](../techniques/Data-from-Local-System.md)
    
* [Query Registry](../techniques/Query-Registry.md)
    
* [Forced Authentication](../techniques/Forced-Authentication.md)
    
* [Windows Command Shell](../techniques/Windows-Command-Shell.md)
    
* [Screen Capture](../techniques/Screen-Capture.md)
    
* [System Network Configuration Discovery](../techniques/System-Network-Configuration-Discovery.md)
    
* [File Deletion](../techniques/File-Deletion.md)
    
* [Ingress Tool Transfer](../techniques/Ingress-Tool-Transfer.md)
    
* [Shortcut Modification](../techniques/Shortcut-Modification.md)
    
* [Web Shell](../techniques/Web-Shell.md)
    
* [Spearphishing Attachment](../techniques/Spearphishing-Attachment.md)
    
* [Password Cracking](../techniques/Password-Cracking.md)
    
* [Spearphishing Link](../techniques/Spearphishing-Link.md)
    
* [External Remote Services](../techniques/External-Remote-Services.md)
    
* [Registry Run Keys / Startup Folder](../techniques/Registry-Run-Keys---Startup-Folder.md)
    
* [Remote Desktop Protocol](../techniques/Remote-Desktop-Protocol.md)
    
* [PowerShell](../techniques/PowerShell.md)
    
* [System Owner/User Discovery](../techniques/System-Owner-User-Discovery.md)
    
* [Local Data Staging](../techniques/Local-Data-Staging.md)
    
* [Account Manipulation](../techniques/Account-Manipulation.md)
    
* [Commonly Used Port](../techniques/Commonly-Used-Port.md)
    
* [Domain Account](../techniques/Domain-Account.md)
    
* [Archive Collected Data](../techniques/Archive-Collected-Data.md)
    
* [Malicious Link](../techniques/Malicious-Link.md)
    
* [Python](../techniques/Python.md)
    
* [NTDS](../techniques/NTDS.md)
    
* [LSA Secrets](../techniques/LSA-Secrets.md)
    

# Malwares

None

# Tools


* [Impacket](../tools/Impacket.md)

* [PsExec](../tools/PsExec.md)
    
* [netsh](../tools/netsh.md)
    
* [Net](../tools/Net.md)
    
* [Reg](../tools/Reg.md)
    
