
# Re-opened Applications

## Description

### MITRE Description

> Adversaries may modify plist files to automatically run an application when a user logs in. Starting in Mac OS X 10.7 (Lion), users can specify certain applications to be re-opened when a user logs into their machine after reboot. While this is usually done via a Graphical User Interface (GUI) on an app-by-app basis, there are property list files (plist) that contain this information as well located at <code>~/Library/Preferences/com.apple.loginwindow.plist</code> and <code>~/Library/Preferences/ByHost/com.apple.loginwindow.* .plist</code>. 

An adversary can modify one of these files directly to include a link to their malicious executable to provide a persistence mechanism each time the user reboots their machine (Citation: Methods of Mac Malware Persistence).

## Aliases

```

```

## Additional Attributes

* Bypass: None
* Effective Permissions: None
* Network: None
* Permissions: ['User']
* Platforms: ['macOS']
* Remote: None
* Type: attack-pattern
* Wiki: https://attack.mitre.org/techniques/T1547/007

## Potential Commands

```
sudo defaults write com.apple.loginwindow LoginHook /path/to/script
```

## Commands Dataset

```
[{'command': 'sudo defaults write com.apple.loginwindow LoginHook '
             '/path/to/script\n',
  'name': None,
  'source': 'atomics/T1547.007/T1547.007.yaml'}]
```

## Potential Detections

```json

```

## Potential Queries

```json

```

## Raw Dataset

```json
[{'Atomic Red Team Test - Boot or Logon Autostart Execution: Re-opened Applications': {'atomic_tests': [{'auto_generated_guid': '5fefd767-ef54-4ac6-84d3-751ab85e8aba',
                                                                                                         'description': 'Plist '
                                                                                                                        'Method\n'
                                                                                                                        '\n'
                                                                                                                        '[Reference](https://developer.apple.com/library/content/documentation/MacOSX/Conceptual/BPSystemStartup/Chapters/CustomLogin.html)\n',
                                                                                                         'executor': {'name': 'manual',
                                                                                                                      'steps': '1. '
                                                                                                                               'create '
                                                                                                                               'a '
                                                                                                                               'custom '
                                                                                                                               'plist:\n'
                                                                                                                               '\n'
                                                                                                                               '    '
                                                                                                                               '~/Library/Preferences/com.apple.loginwindow.plist\n'
                                                                                                                               '\n'
                                                                                                                               'or\n'
                                                                                                                               '\n'
                                                                                                                               '    '
                                                                                                                               '~/Library/Preferences/ByHost/com.apple.loginwindow.*.plist\n'},
                                                                                                         'name': 'Re-Opened '
                                                                                                                 'Applications',
                                                                                                         'supported_platforms': ['macos']},
                                                                                                        {'auto_generated_guid': '5f5b71da-e03f-42e7-ac98-d63f9e0465cb',
                                                                                                         'description': 'Mac '
                                                                                                                        'Defaults\n'
                                                                                                                        '\n'
                                                                                                                        '[Reference](https://developer.apple.com/library/content/documentation/MacOSX/Conceptual/BPSystemStartup/Chapters/CustomLogin.html)\n',
                                                                                                         'executor': {'cleanup': 'sudo '
                                                                                                                                 'defaults '
                                                                                                                                 'delete '
                                                                                                                                 'com.apple.loginwindow '
                                                                                                                                 'LoginHook\n',
                                                                                                                      'command': 'sudo '
                                                                                                                                 'defaults '
                                                                                                                                 'write '
                                                                                                                                 'com.apple.loginwindow '
                                                                                                                                 'LoginHook '
                                                                                                                                 '#{script}\n',
                                                                                                                      'elevation_required': True,
                                                                                                                      'name': 'sh'},
                                                                                                         'input_arguments': {'script': {'default': '/path/to/script',
                                                                                                                                        'description': 'path '
                                                                                                                                                       'to '
                                                                                                                                                       'script',
                                                                                                                                        'type': 'path'}},
                                                                                                         'name': 'Re-Opened '
                                                                                                                 'Applications',
                                                                                                         'supported_platforms': ['macos']}],
                                                                                       'attack_technique': 'T1547.007',
                                                                                       'display_name': 'Boot '
                                                                                                       'or '
                                                                                                       'Logon '
                                                                                                       'Autostart '
                                                                                                       'Execution: '
                                                                                                       'Re-opened '
                                                                                                       'Applications'}}]
```

# Tactics


* [Persistence](../tactics/Persistence.md)

* [Privilege Escalation](../tactics/Privilege-Escalation.md)
    

# Mitigations


* [User Training](../mitigations/User-Training.md)

* [Disable or Remove Feature or Program](../mitigations/Disable-or-Remove-Feature-or-Program.md)
    

# Actors

None
