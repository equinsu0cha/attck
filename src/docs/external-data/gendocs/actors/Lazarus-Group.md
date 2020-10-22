
# Lazarus Group

```
.__                                                                            
|  | _____  _____________ _______ __ __  ______       ___________  ____  __ __ 
|  | \__  \ \___   /\__  \\_  __ \  |  \/  ___/      / ___\_  __ \/  _ \|  |  \
|  |__/ __ \_/    /  / __ \|  | \/  |  /\___ \      / /_/  >  | \(  <_> )  |  /
|____(____  /_____ \(____  /__|  |____//____  >_____\___  /|__|   \____/|____/ 
          \/      \/     \/                 \/_____/_____/                     
        
______  
\____ \ 
|  |_> >
|   __/ 
|__|    

```

## Description

### MITRE Description

> [Lazarus Group](https://attack.mitre.org/groups/G0032) is a threat group that has been attributed to the North Korean government.(Citation: US-CERT HIDDEN COBRA June 2017) The group has been active since at least 2009 and was reportedly responsible for the November 2014 destructive wiper attack against Sony Pictures Entertainment as part of a campaign named Operation Blockbuster by Novetta. Malware used by [Lazarus Group](https://attack.mitre.org/groups/G0032) correlates to other reported campaigns, including Operation Flame, Operation 1Mission, Operation Troy, DarkSeoul, and Ten Days of Rain. (Citation: Novetta Blockbuster) In late 2017, [Lazarus Group](https://attack.mitre.org/groups/G0032) used KillDisk, a disk-wiping tool, in an attack against an online casino based in Central America. (Citation: Lazarus KillDisk)

North Korean group definitions are known to have significant overlap, and the name [Lazarus Group](https://attack.mitre.org/groups/G0032) is known to encompass a broad range of activity. Some organizations use the name Lazarus Group to refer to any activity attributed to North Korea.(Citation: US-CERT HIDDEN COBRA June 2017) Some organizations track North Korean clusters or groups such as Bluenoroff,(Citation: Kaspersky Lazarus Under The Hood Blog 2017) [APT37](https://attack.mitre.org/groups/G0067), and [APT38](https://attack.mitre.org/groups/G0082) separately, while other organizations may track some activity associated with those group names by the name Lazarus Group.

### External Description

> Delivery: usually via spear phishing email.Infrastructure: C2 often based on compromised servers,moving to own servers paid by bitcoin to preserve anonymityPersistency: tipically launching ransomware after operation to destroy evidences

## Aliases

```
Lazarus Group
HIDDEN COBRA
Guardians of Peace
ZINC
NICKEL ACADEMY
```

## Known Tools

```
Tdrop
Tdrop2
Troy
Destover
FallChill RAT
Volgmer
Hawup
Manuscrypt
WolfRAT
SheepRAT
HtDnDownLoader
```

## Operations

```
Blockbuster
Dark Seoul
Applejeus
```

## Targets

```
Believed to be responsible for Dark Seoul, Ten Days of Rain, the Sony Pictures Entertainment attack,Â the SWIFT-related bank heists, and WannaCry. Known to the U.S. government as Hidden Cobra. Targeting also BitCoin Exchanges, financial sector, technology/engineering sector
```

## Attribution Links

```
http://www.mcafee.com/us/resources/white-papers/wp-dissecting-operation-troy.pdf
http://researchcenter.paloaltonetworks.com/2015/11/tdrop2-attacks-suggest-dark-seoul-attackers-return/
https://www.operationblockbuster.com/wp-content/uploads/2016/02/Operation-Blockbuster-Report.pdf
https://www.alienvault.com/open-threat-exchange/blog/operation-blockbuster-unveils-the-actors-behind-the-sony-attacks
https://www.us-cert.gov/ncas/alerts/TA17-164A
http://www.fsec.or.kr/common/proc/fsec/bbs/21/fileDownLoad/1235.do
https://researchcenter.paloaltonetworks.com/2017/08/unit42-blockbuster-saga-continues/
https://www.crowdstrike.com/blog/unprecedented-announcement-fbi-implicates-north-korea-destructive-attacks/
https://www.us-cert.gov/ncas/alerts/TA17-318A
https://www.us-cert.gov/ncas/alerts/TA17-318B
https://www.proofpoint.com/sites/default/files/pfpt-us-wp-north-korea-bitten-by-bitcoin-bug.pdf
https://securingtomorrow.mcafee.com/mcafee-labs/lazarus-resurfaces-targets-global-banks-bitcoin-users/
https://www.darkreading.com/vulnerabilities---threats/lazarus-group-fancy-bear-most-active-threat-groups-in-2017/d/d-id/1330954?print=yes
https://www.us-cert.gov/HIDDEN-COBRA-North-Korean-Malicious-Cyber-Activity
 https://securelist.com/operation-applejeus/87553/
https://blogs.microsoft.com/on-the-issues/2017/12/19/microsoft-facebook-disrupt-zinc-malware-attack-protect-customers-internet-ongoing-cyberthreats/
https://www.secureworks.com/about/press/media-alert-secureworks-discovers-north-korean-cyber-threat-group-lazarus-spearphishing
https://threatrecon.nshc.net/2019/01/23/sectora01-custom-proxy-utility-tool-analysis/
https://objective-see.com/blog/blog_0x49.html
https://www.sentinelone.com/blog/lazarus-apt-targets-mac-users-poisoned-word-document/
https://blog.alyac.co.kr/2827
```

## Country

```
north_korea
```

## Comments

```
Threat Recon.nshc.net alias=SectorA01
```

# Techniques


* [Create Process with Token](../techniques/Create-Process-with-Token.md)

* [Account Manipulation](../techniques/Account-Manipulation.md)
    
* [Drive-by Compromise](../techniques/Drive-by-Compromise.md)
    
* [Hidden Files and Directories](../techniques/Hidden-Files-and-Directories.md)
    
* [Dynamic-link Library Injection](../techniques/Dynamic-link-Library-Injection.md)
    
* [Compiled HTML File](../techniques/Compiled-HTML-File.md)
    
* [Bootkit](../techniques/Bootkit.md)
    
* [Remote Desktop Protocol](../techniques/Remote-Desktop-Protocol.md)
    
* [File Deletion](../techniques/File-Deletion.md)
    
* [Registry Run Keys / Startup Folder](../techniques/Registry-Run-Keys---Startup-Folder.md)
    
* [Spearphishing Attachment](../techniques/Spearphishing-Attachment.md)
    
* [Local Data Staging](../techniques/Local-Data-Staging.md)
    
* [Standard Encoding](../techniques/Standard-Encoding.md)
    
* [Keylogging](../techniques/Keylogging.md)
    
* [Commonly Used Port](../techniques/Commonly-Used-Port.md)
    
* [Exfiltration Over C2 Channel](../techniques/Exfiltration-Over-C2-Channel.md)
    
* [Obfuscated Files or Information](../techniques/Obfuscated-Files-or-Information.md)
    
* [File and Directory Discovery](../techniques/File-and-Directory-Discovery.md)
    
* [System Owner/User Discovery](../techniques/System-Owner-User-Discovery.md)
    
* [Disable or Modify Tools](../techniques/Disable-or-Modify-Tools.md)
    
* [Timestomp](../techniques/Timestomp.md)
    
* [Web Protocols](../techniques/Web-Protocols.md)
    
* [System Time Discovery](../techniques/System-Time-Discovery.md)
    
* [Data from Local System](../techniques/Data-from-Local-System.md)
    
* [Shortcut Modification](../techniques/Shortcut-Modification.md)
    
* [Application Window Discovery](../techniques/Application-Window-Discovery.md)
    
* [LSASS Memory](../techniques/LSASS-Memory.md)
    
* [Exploitation for Client Execution](../techniques/Exploitation-for-Client-Execution.md)
    
* [System Network Configuration Discovery](../techniques/System-Network-Configuration-Discovery.md)
    
* [Windows Service](../techniques/Windows-Service.md)
    
* [Query Registry](../techniques/Query-Registry.md)
    
* [Windows Management Instrumentation](../techniques/Windows-Management-Instrumentation.md)
    
* [Process Discovery](../techniques/Process-Discovery.md)
    
* [Ingress Tool Transfer](../techniques/Ingress-Tool-Transfer.md)
    
* [Archive Collected Data](../techniques/Archive-Collected-Data.md)
    
* [External Proxy](../techniques/External-Proxy.md)
    
* [SMB/Windows Admin Shares](../techniques/SMB-Windows-Admin-Shares.md)
    
* [Fallback Channels](../techniques/Fallback-Channels.md)
    
* [Password Spraying](../techniques/Password-Spraying.md)
    
* [Malicious File](../techniques/Malicious-File.md)
    
* [Uncommonly Used Port](../techniques/Uncommonly-Used-Port.md)
    
* [Multiband Communication](../techniques/Multiband-Communication.md)
    
* [Archive via Library](../techniques/Archive-via-Library.md)
    
* [Symmetric Cryptography](../techniques/Symmetric-Cryptography.md)
    
* [System Information Discovery](../techniques/System-Information-Discovery.md)
    
* [Exfiltration Over Unencrypted/Obfuscated Non-C2 Protocol](../techniques/Exfiltration-Over-Unencrypted-Obfuscated-Non-C2-Protocol.md)
    
* [Service Stop](../techniques/Service-Stop.md)
    
* [Disk Structure Wipe](../techniques/Disk-Structure-Wipe.md)
    
* [Disk Content Wipe](../techniques/Disk-Content-Wipe.md)
    
* [Data Destruction](../techniques/Data-Destruction.md)
    
* [Resource Hijacking](../techniques/Resource-Hijacking.md)
    
* [System Shutdown/Reboot](../techniques/System-Shutdown-Reboot.md)
    
* [Windows Command Shell](../techniques/Windows-Command-Shell.md)
    
* [Protocol Impersonation](../techniques/Protocol-Impersonation.md)
    
* [Disable or Modify System Firewall](../techniques/Disable-or-Modify-System-Firewall.md)
    
* [Internal Defacement](../techniques/Internal-Defacement.md)
    
* [Archive via Custom Method](../techniques/Archive-via-Custom-Method.md)
    
* [Non-Standard Port](../techniques/Non-Standard-Port.md)
    

# Malwares


* [Proxysvc](../malwares/Proxysvc.md)

* [KEYMARBLE](../malwares/KEYMARBLE.md)
    
* [Volgmer](../malwares/Volgmer.md)
    
* [BADCALL](../malwares/BADCALL.md)
    
* [RATANKBA](../malwares/RATANKBA.md)
    
* [Bankshot](../malwares/Bankshot.md)
    
* [HARDRAIN](../malwares/HARDRAIN.md)
    
* [TYPEFRAME](../malwares/TYPEFRAME.md)
    
* [AuditCred](../malwares/AuditCred.md)
    
* [FALLCHILL](../malwares/FALLCHILL.md)
    
* [WannaCry](../malwares/WannaCry.md)
    
* [HOPLIGHT](../malwares/HOPLIGHT.md)
    
* [HotCroissant](../malwares/HotCroissant.md)
    

# Tools


* [Mimikatz](../tools/Mimikatz.md)

* [netsh](../tools/netsh.md)
    
* [RawDisk](../tools/RawDisk.md)
    
