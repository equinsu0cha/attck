
# Plist Modification

## Description

### MITRE Description

> Adversaries may modify plist files to run a program during system boot or user login. Property list (plist) files contain all of the information that macOS and OS X uses to configure applications and services. These files are UTF-8 encoded and formatted like XML documents via a series of keys surrounded by < >. They detail when programs should execute, file paths to the executables, program arguments, required OS permissions, and many others. plists are located in certain locations depending on their purpose such as <code>/Library/Preferences</code> (which execute with elevated privileges) and <code>~/Library/Preferences</code> (which execute with a user's privileges). 

Adversaries can modify plist files to execute their code as part of establishing persistence. plists may also be used to elevate privileges since they may execute in the context of another user.(Citation: Sofacy Komplex Trojan) 

A specific plist used for execution at login is <code>com.apple.loginitems.plist</code>.(Citation: Methods of Mac Malware Persistence) Applications under this plist run under the logged in user's context, and will be started every time the user logs in. Login items installed using the Service Management Framework are not visible in the System Preferences and can only be removed by the application that created them.(Citation: Adding Login Items) Users have direct control over login items installed using a shared file list which are also visible in System Preferences (Citation: Adding Login Items). Some of these applications can open visible dialogs to the user, but they don’t all have to since there is an option to "hide" the window. If an adversary can register their own login item or modified an existing one, then they can use it to execute their code for a persistence mechanism each time the user logs in (Citation: Malware Persistence on OS X) (Citation: OSX.Dok Malware). The API method <code> SMLoginItemSetEnabled</code> can be used to set Login Items, but scripting languages like [AppleScript](https://attack.mitre.org/techniques/T1059/002) can do this as well. (Citation: Adding Login Items)

## Aliases

```

```

## Additional Attributes

* Bypass: None
* Effective Permissions: None
* Network: None
* Permissions: ['User', 'Administrator']
* Platforms: ['macOS']
* Remote: None
* Type: attack-pattern
* Wiki: https://attack.mitre.org/techniques/T1547/011

## Potential Commands

```

```

## Commands Dataset

```

```

## Potential Detections

```json

```

## Potential Queries

```json

```

## Raw Dataset

```json
[{'Atomic Red Team Test - Boot or Logon Autostart Execution: Plist Modification': {'atomic_tests': [{'auto_generated_guid': '394a538e-09bb-4a4a-95d1-b93cf12682a8',
                                                                                                     'description': 'Modify '
                                                                                                                    'MacOS '
                                                                                                                    'plist '
                                                                                                                    'file '
                                                                                                                    'in '
                                                                                                                    'one '
                                                                                                                    'of '
                                                                                                                    'two '
                                                                                                                    'directories\n',
                                                                                                     'executor': {'name': 'manual',
                                                                                                                  'steps': '1. '
                                                                                                                           'Modify '
                                                                                                                           'a '
                                                                                                                           '.plist '
                                                                                                                           'in\n'
                                                                                                                           '\n'
                                                                                                                           '    '
                                                                                                                           '/Library/Preferences\n'
                                                                                                                           '\n'
                                                                                                                           '    '
                                                                                                                           'OR\n'
                                                                                                                           '\n'
                                                                                                                           '    '
                                                                                                                           '~/Library/Preferences\n'
                                                                                                                           '\n'
                                                                                                                           '2. '
                                                                                                                           'Subsequently, '
                                                                                                                           'follow '
                                                                                                                           'the '
                                                                                                                           'steps '
                                                                                                                           'for '
                                                                                                                           'adding '
                                                                                                                           'and '
                                                                                                                           'running '
                                                                                                                           'via '
                                                                                                                           '[Launch '
                                                                                                                           'Agent](Persistence/Launch_Agent.md)\n'},
                                                                                                     'name': 'Plist '
                                                                                                             'Modification',
                                                                                                     'supported_platforms': ['macos']}],
                                                                                   'attack_technique': 'T1547.011',
                                                                                   'display_name': 'Boot '
                                                                                                   'or '
                                                                                                   'Logon '
                                                                                                   'Autostart '
                                                                                                   'Execution: '
                                                                                                   'Plist '
                                                                                                   'Modification'}}]
```

# Tactics


* [Persistence](../tactics/Persistence.md)

* [Privilege Escalation](../tactics/Privilege-Escalation.md)
    

# Mitigations


* [Restrict File and Directory Permissions](../mitigations/Restrict-File-and-Directory-Permissions.md)

* [User Training](../mitigations/User-Training.md)
    

# Actors

None
