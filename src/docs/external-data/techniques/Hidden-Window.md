
# Hidden Window

## Description

### MITRE Description

> Adversaries may use hidden windows to conceal malicious activity from the plain sight of users. In some cases, windows that would typically be displayed when an application carries out an operation can be hidden. This may be utilized by system administrators to avoid disrupting user work environments when carrying out administrative tasks. 

On Windows, there are a variety of features in scripting languages in Windows, such as [PowerShell](https://attack.mitre.org/techniques/T1059/001), Jscript, and [Visual Basic](https://attack.mitre.org/techniques/T1059/005) to make windows hidden. One example of this is <code>powershell.exe -WindowStyle Hidden</code>. (Citation: PowerShell About 2019)

Similarly, on macOS the configurations for how applications run are listed in property list (plist) files. One of the tags in these files can be <code>apple.awt.UIElement</code>, which allows for Java applications to prevent the application's icon from appearing in the Dock. A common use for this is when applications run in the system tray, but don't also want to show up in the Dock.

Adversaries may abuse these functionalities to hide otherwise visible windows from users so as not to alert the user to adversary activity on the system.(Citation: Antiquated Mac Malware)

## Aliases

```

```

## Additional Attributes

* Bypass: None
* Effective Permissions: None
* Network: None
* Permissions: ['User']
* Platforms: ['macOS', 'Windows']
* Remote: None
* Type: attack-pattern
* Wiki: https://attack.mitre.org/techniques/T1564/003

## Potential Commands

```
Start-Process powershell.exe -WindowStyle hidden calc.exe
```

## Commands Dataset

```
[{'command': 'Start-Process powershell.exe -WindowStyle hidden calc.exe\n',
  'name': None,
  'source': 'atomics/T1564.003/T1564.003.yaml'}]
```

## Potential Detections

```json

```

## Potential Queries

```json

```

## Raw Dataset

```json
[{'Atomic Red Team Test - Hide Artifacts: Hidden Window': {'atomic_tests': [{'auto_generated_guid': 'f151ee37-9e2b-47e6-80e4-550b9f999b7a',
                                                                             'description': 'Launch '
                                                                                            'PowerShell '
                                                                                            'with '
                                                                                            'the '
                                                                                            '"-WindowStyle '
                                                                                            'Hidden" '
                                                                                            'argument '
                                                                                            'to '
                                                                                            'conceal '
                                                                                            'PowerShell '
                                                                                            'windows '
                                                                                            'by '
                                                                                            'setting '
                                                                                            'the '
                                                                                            'WindowStyle '
                                                                                            'parameter '
                                                                                            'to '
                                                                                            'hidden.\n'
                                                                                            'Upon '
                                                                                            'execution '
                                                                                            'a '
                                                                                            'hidden '
                                                                                            'PowerShell '
                                                                                            'window '
                                                                                            'will '
                                                                                            'launch '
                                                                                            'calc.exe\n',
                                                                             'executor': {'command': 'Start-Process '
                                                                                                     '#{powershell_command}\n',
                                                                                          'name': 'powershell'},
                                                                             'input_arguments': {'powershell_command': {'default': 'powershell.exe '
                                                                                                                                   '-WindowStyle '
                                                                                                                                   'hidden '
                                                                                                                                   'calc.exe',
                                                                                                                        'description': 'Command '
                                                                                                                                       'to '
                                                                                                                                       'launch '
                                                                                                                                       'calc.exe '
                                                                                                                                       'from '
                                                                                                                                       'a '
                                                                                                                                       'hidden '
                                                                                                                                       'PowerShell '
                                                                                                                                       'Window',
                                                                                                                        'type': 'String'}},
                                                                             'name': 'Hidden '
                                                                                     'Window',
                                                                             'supported_platforms': ['windows']}],
                                                           'attack_technique': 'T1564.003',
                                                           'display_name': 'Hide '
                                                                           'Artifacts: '
                                                                           'Hidden '
                                                                           'Window'}}]
```

# Tactics


* [Defense Evasion](../tactics/Defense-Evasion.md)


# Mitigations


* [Execution Prevention](../mitigations/Execution-Prevention.md)


# Actors


* [Magic Hound](../actors/Magic-Hound.md)

* [APT3](../actors/APT3.md)
    
* [APT28](../actors/APT28.md)
    
* [APT32](../actors/APT32.md)
    
* [APT19](../actors/APT19.md)
    
* [CopyKittens](../actors/CopyKittens.md)
    
* [DarkHydrus](../actors/DarkHydrus.md)
    
* [Deep Panda](../actors/Deep-Panda.md)
    
* [Gorgon Group](../actors/Gorgon-Group.md)
    
