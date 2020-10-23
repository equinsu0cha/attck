
# LSASS Driver

## Description

### MITRE Description

> Adversaries may modify or add LSASS drivers to obtain persistence on compromised systems. The Windows security subsystem is a set of components that manage and enforce the security policy for a computer or domain. The Local Security Authority (LSA) is the main component responsible for local security policy and user authentication. The LSA includes multiple dynamic link libraries (DLLs) associated with various other security functions, all of which run in the context of the LSA Subsystem Service (LSASS) lsass.exe process. (Citation: Microsoft Security Subsystem)

Adversaries may target LSASS drivers to obtain persistence. By either replacing or adding illegitimate drivers (e.g., [Hijack Execution Flow](https://attack.mitre.org/techniques/T1574)), an adversary can use LSA operations to continuously execute malicious payloads.

## Aliases

```

```

## Additional Attributes

* Bypass: None
* Effective Permissions: None
* Network: None
* Permissions: ['SYSTEM', 'Administrator']
* Platforms: ['Windows']
* Remote: None
* Type: attack-pattern
* Wiki: https://attack.mitre.org/techniques/T1547/008

## Potential Commands

```

```

## Commands Dataset

```

```

## Potential Detections

```json
[{'data_source': {'author': 'Florian Roth',
                  'date': '2019/10/16',
                  'description': 'Detects a method to load DLL via LSASS '
                                 'process using an undocumented Registry key',
                  'detection': {'condition': 'selection',
                                'selection': {'EventID': [12, 13],
                                              'TargetObject': ['*\\CurrentControlSet\\Services\\NTDS\\DirectoryServiceExtPt*',
                                                               '*\\CurrentControlSet\\Services\\NTDS\\LsaDbExtPt*']}},
                  'falsepositives': ['Unknown'],
                  'id': 'b3503044-60ce-4bf4-bbcb-e3db98788823',
                  'level': 'high',
                  'logsource': {'product': 'windows', 'service': 'sysmon'},
                  'references': ['https://blog.xpnsec.com/exploring-mimikatz-part-1/',
                                 'https://twitter.com/SBousseaden/status/1183745981189427200'],
                  'status': 'experimental',
                  'tags': ['attack.execution', 'attack.t1177'],
                  'title': 'DLL Load via LSASS'}},
 {'data_source': ['4688', 'Process Execution']},
 {'data_source': ['4663', 'File monitoring']},
 {'data_source': ['DLL monitoring']},
 {'data_source': ['Loaded DLLs']},
 {'data_source': ['Sysmon - ID 6', 'Kernel drivers']},
 {'data_source': ['API monitoring']},
 {'data_source': ['4688', 'Process Execution']},
 {'data_source': ['4663', 'File monitoring']},
 {'data_source': ['Sysmon ID 7', 'DLL monitoring']},
 {'data_source': ['Sysmon ID 7', 'Loaded DLLs']},
 {'data_source': ['Sysmon - ID 6', 'Kernel drivers']},
 {'data_source': ['API monitoring']}]
```

## Potential Queries

```json

```

## Raw Dataset

```json

```

# Tactics


* [Persistence](../tactics/Persistence.md)

* [Privilege Escalation](../tactics/Privilege-Escalation.md)
    

# Mitigations


* [Restrict Library Loading](../mitigations/Restrict-Library-Loading.md)

* [Credential Access Protection](../mitigations/Credential-Access-Protection.md)
    
* [Privileged Process Integrity](../mitigations/Privileged-Process-Integrity.md)
    

# Actors

None
