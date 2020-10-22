
# Taint Shared Content

## Description

### MITRE Description

> 
Adversaries may deliver payloads to remote systems by adding content to shared storage locations, such as network drives or internal code repositories. Content stored on network drives or in other shared locations may be tainted by adding malicious programs, scripts, or exploit code to otherwise valid files. Once a user opens the shared tainted content, the malicious portion can be executed to run the adversary's code on a remote system. Adversaries may use tainted shared content to move laterally.

A directory share pivot is a variation on this technique that uses several other techniques to propagate malware when users access a shared network directory. It uses [Shortcut Modification](https://attack.mitre.org/techniques/T1547/009) of directory .LNK files that use [Masquerading](https://attack.mitre.org/techniques/T1036) to look like the real directories, which are hidden through [Hidden Files and Directories](https://attack.mitre.org/techniques/T1564/001). The malicious .LNK-based directories have an embedded command that executes the hidden malware file in the directory and then opens the real intended directory so that the user's expected action still occurs. When used with frequently used network directories, the technique may result in frequent reinfections and broad access to systems and potentially to new and higher privileged accounts. (Citation: Retwin Directory Share Pivot)

Adversaries may also compromise shared network directories through binary infections by appending or prepending its code to the healthy binary on the shared network directory. The malware may modify the original entry point (OEP) of the healthy binary to ensure that it is executed before the legitimate code. The infection could continue to spread via the newly infected file when it is executed by a remote system. These infections may target both binary and non-binary formats that end with extensions including, but not limited to, .EXE, .DLL, .SCR, .BAT, and/or .VBS.

## Aliases

```

```

## Additional Attributes

* Bypass: None
* Effective Permissions: None
* Network: None
* Permissions: ['User']
* Platforms: ['Windows']
* Remote: None
* Type: attack-pattern
* Wiki: https://attack.mitre.org/techniques/T1080

## Potential Commands

```

```

## Commands Dataset

```

```

## Potential Detections

```json
[{'data_source': ['4663', 'File monitoring']},
 {'data_source': ['4688', 'Process Execution']},
 {'data_source': ['4663', 'File monitoring']},
 {'data_source': ['4688', 'Process Execution']}]
```

## Potential Queries

```json

```

## Raw Dataset

```json

```

# Tactics


* [Lateral Movement](../tactics/Lateral-Movement.md)


# Mitigations


* [Taint Shared Content Mitigation](../mitigations/Taint-Shared-Content-Mitigation.md)

* [Restrict File and Directory Permissions](../mitigations/Restrict-File-and-Directory-Permissions.md)
    
* [Exploit Protection](../mitigations/Exploit-Protection.md)
    
* [Execution Prevention](../mitigations/Execution-Prevention.md)
    

# Actors


* [Darkhotel](../actors/Darkhotel.md)

* [BRONZE BUTLER](../actors/BRONZE-BUTLER.md)
    
