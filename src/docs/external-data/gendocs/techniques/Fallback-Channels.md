
# Fallback Channels

## Description

### MITRE Description

> Adversaries may use fallback or alternate communication channels if the primary channel is compromised or inaccessible in order to maintain reliable command and control and to avoid data transfer thresholds.

## Aliases

```

```

## Additional Attributes

* Bypass: None
* Effective Permissions: None
* Network: True
* Permissions: None
* Platforms: ['Linux', 'Windows', 'macOS']
* Remote: None
* Type: attack-pattern
* Wiki: https://attack.mitre.org/techniques/T1008

## Potential Commands

```
powershell/management/switch_listener
powershell/management/switch_listener
external/generate_agent
external/generate_agent
```

## Commands Dataset

```
[{'command': 'powershell/management/switch_listener',
  'name': 'Empire Module Command',
  'source': 'https://github.com/dstepanic/attck_empire/blob/master/Empire_modules.xlsx?raw=true'},
 {'command': 'powershell/management/switch_listener',
  'name': 'Empire Module Command',
  'source': 'https://github.com/dstepanic/attck_empire/blob/master/Empire_modules.xlsx?raw=true'},
 {'command': 'external/generate_agent',
  'name': 'Empire Module Command',
  'source': 'https://github.com/dstepanic/attck_empire/blob/master/Empire_modules.xlsx?raw=true'},
 {'command': 'external/generate_agent',
  'name': 'Empire Module Command',
  'source': 'https://github.com/dstepanic/attck_empire/blob/master/Empire_modules.xlsx?raw=true'}]
```

## Potential Detections

```json
[{'data_source': ['4688', 'Process Execution']},
 {'data_source': ['5156', 'Windows Firewall']},
 {'data_source': ['Malware reverse engineering']},
 {'data_source': ['Netflow/Enclave netflow']},
 {'data_source': ['Packet capture']},
 {'data_source': ['4688', 'Process Execution']},
 {'data_source': ['5156', 'Windows Firewall']},
 {'data_source': ['Malware reverse engineering']},
 {'data_source': ['Netflow/Enclave netflow']},
 {'data_source': ['Packet capture']}]
```

## Potential Queries

```json

```

## Raw Dataset

```json
[{'Empire Module XLSX Sheet by dstepanic': {'ATT&CK Technique #1': 'T1008',
                                            'ATT&CK Technique #2': '',
                                            'Concatenate for Python Dictionary': '"powershell/management/switch_listener":  '
                                                                                 '["T1008"],',
                                            'Empire Module': 'powershell/management/switch_listener',
                                            'Technique': 'Fallback Channels'}},
 {'Empire Module XLSX Sheet by dstepanic': {'ATT&CK Technique #1': 'T1008',
                                            'ATT&CK Technique #2': '',
                                            'Concatenate for Python Dictionary': '"external/generate_agent":  '
                                                                                 '["T1008"],',
                                            'Empire Module': 'external/generate_agent',
                                            'Technique': 'Fallback Channels'}}]
```

# Tactics


* [Command and Control](../tactics/Command-and-Control.md)


# Mitigations


* [Fallback Channels Mitigation](../mitigations/Fallback-Channels-Mitigation.md)

* [Network Intrusion Prevention](../mitigations/Network-Intrusion-Prevention.md)
    

# Actors


* [Lazarus Group](../actors/Lazarus-Group.md)

* [OilRig](../actors/OilRig.md)
    
* [APT41](../actors/APT41.md)
    
