
# Timestomp

## Description

### MITRE Description

> Adversaries may modify file time attributes to hide new or changes to existing files. Timestomping is a technique that modifies the timestamps of a file (the modify, access, create, and change times), often to mimic files that are in the same folder. This is done, for example, on files that have been modified or created by the adversary so that they do not appear conspicuous to forensic investigators or file analysis tools.

Timestomping may be used along with file name [Masquerading](https://attack.mitre.org/techniques/T1036) to hide malware and tools.(Citation: WindowsIR Anti-Forensic Techniques)

## Aliases

```

```

## Additional Attributes

* Bypass: ['Host forensic analysis']
* Effective Permissions: None
* Network: None
* Permissions: ['root', 'SYSTEM', 'User']
* Platforms: ['Linux', 'macOS', 'Windows']
* Remote: None
* Type: attack-pattern
* Wiki: https://attack.mitre.org/techniques/T1070/006

## Potential Commands

```
touch -acmr /bin/sh #{target_file_path}
touch -m -t 197001010000.00 /opt/filename
Get-ChildItem $env:TEMP\T1551.006_timestomp.txt | % { $_.LastWriteTime = "#{target_date_time}" }
Get-ChildItem #{file_path} | % { $_.LastWriteTime = "01/01/1970 00:00:00" }
Get-ChildItem #{file_path} | % { $_.LastAccessTime = "01/01/1970 00:00:00" }
Get-ChildItem $env:TEMP\T1551.006_timestomp.txt | % { $_.CreationTime = "#{target_date_time}" }
touch -a -t 197001010000.00 /opt/filename
NOW=$(date)
date -s "1970-01-01 00:00:00"
touch /opt/filename
date -s "$NOW"
stat /opt/filename
Get-ChildItem #{file_path} | % { $_.CreationTime = "01/01/1970 00:00:00" }
Get-ChildItem $env:TEMP\T1551.006_timestomp.txt | % { $_.LastAccessTime = "#{target_date_time}" }
import-module $env:appdata\Microsoft\timestomp.ps1
timestomp -dest "$env:appdata\Microsoft\kxwn.lock"
touch -acmr #{reference_file_path} /opt/filename
```

## Commands Dataset

```
[{'command': 'touch -a -t 197001010000.00 /opt/filename\n',
  'name': None,
  'source': 'atomics/T1070.006/T1070.006.yaml'},
 {'command': 'touch -m -t 197001010000.00 /opt/filename\n',
  'name': None,
  'source': 'atomics/T1070.006/T1070.006.yaml'},
 {'command': 'NOW=$(date)\n'
             'date -s "1970-01-01 00:00:00"\n'
             'touch /opt/filename\n'
             'date -s "$NOW"\n'
             'stat /opt/filename\n',
  'name': None,
  'source': 'atomics/T1070.006/T1070.006.yaml'},
 {'command': 'touch -acmr #{reference_file_path} /opt/filename\n',
  'name': None,
  'source': 'atomics/T1070.006/T1070.006.yaml'},
 {'command': 'touch -acmr /bin/sh #{target_file_path}\n',
  'name': None,
  'source': 'atomics/T1070.006/T1070.006.yaml'},
 {'command': 'Get-ChildItem #{file_path} | % { $_.CreationTime = "01/01/1970 '
             '00:00:00" }\n',
  'name': None,
  'source': 'atomics/T1070.006/T1070.006.yaml'},
 {'command': 'Get-ChildItem $env:TEMP\\T1551.006_timestomp.txt | % { '
             '$_.CreationTime = "#{target_date_time}" }\n',
  'name': None,
  'source': 'atomics/T1070.006/T1070.006.yaml'},
 {'command': 'Get-ChildItem #{file_path} | % { $_.LastWriteTime = "01/01/1970 '
             '00:00:00" }\n',
  'name': None,
  'source': 'atomics/T1070.006/T1070.006.yaml'},
 {'command': 'Get-ChildItem $env:TEMP\\T1551.006_timestomp.txt | % { '
             '$_.LastWriteTime = "#{target_date_time}" }\n',
  'name': None,
  'source': 'atomics/T1070.006/T1070.006.yaml'},
 {'command': 'Get-ChildItem #{file_path} | % { $_.LastAccessTime = "01/01/1970 '
             '00:00:00" }\n',
  'name': None,
  'source': 'atomics/T1070.006/T1070.006.yaml'},
 {'command': 'Get-ChildItem $env:TEMP\\T1551.006_timestomp.txt | % { '
             '$_.LastAccessTime = "#{target_date_time}" }\n',
  'name': None,
  'source': 'atomics/T1070.006/T1070.006.yaml'},
 {'command': 'import-module $env:appdata\\Microsoft\\timestomp.ps1\n'
             'timestomp -dest "$env:appdata\\Microsoft\\kxwn.lock"\n',
  'name': None,
  'source': 'atomics/T1070.006/T1070.006.yaml'}]
```

## Potential Detections

```json

```

## Potential Queries

```json

```

## Raw Dataset

```json
[{'Atomic Red Team Test - Indicator Removal on Host: Timestomp': {'atomic_tests': [{'auto_generated_guid': '5f9113d5-ed75-47ed-ba23-ea3573d05810',
                                                                                    'description': 'Stomps '
                                                                                                   'on '
                                                                                                   'the '
                                                                                                   'access '
                                                                                                   'timestamp '
                                                                                                   'of '
                                                                                                   'a '
                                                                                                   'file\n',
                                                                                    'executor': {'command': 'touch '
                                                                                                            '-a '
                                                                                                            '-t '
                                                                                                            '197001010000.00 '
                                                                                                            '#{target_filename}\n',
                                                                                                 'name': 'sh'},
                                                                                    'input_arguments': {'target_filename': {'default': '/opt/filename',
                                                                                                                            'description': 'Path '
                                                                                                                                           'of '
                                                                                                                                           'file '
                                                                                                                                           'that '
                                                                                                                                           'we '
                                                                                                                                           'are '
                                                                                                                                           'going '
                                                                                                                                           'to '
                                                                                                                                           'stomp '
                                                                                                                                           'on '
                                                                                                                                           'last '
                                                                                                                                           'access '
                                                                                                                                           'time',
                                                                                                                            'type': 'Path'}},
                                                                                    'name': 'Set '
                                                                                            'a '
                                                                                            "file's "
                                                                                            'access '
                                                                                            'timestamp',
                                                                                    'supported_platforms': ['linux',
                                                                                                            'macos']},
                                                                                   {'auto_generated_guid': '20ef1523-8758-4898-b5a2-d026cc3d2c52',
                                                                                    'description': 'Stomps '
                                                                                                   'on '
                                                                                                   'the '
                                                                                                   'modification '
                                                                                                   'timestamp '
                                                                                                   'of '
                                                                                                   'a '
                                                                                                   'file\n',
                                                                                    'executor': {'command': 'touch '
                                                                                                            '-m '
                                                                                                            '-t '
                                                                                                            '197001010000.00 '
                                                                                                            '#{target_filename}\n',
                                                                                                 'name': 'sh'},
                                                                                    'input_arguments': {'target_filename': {'default': '/opt/filename',
                                                                                                                            'description': 'Path '
                                                                                                                                           'of '
                                                                                                                                           'file '
                                                                                                                                           'that '
                                                                                                                                           'we '
                                                                                                                                           'are '
                                                                                                                                           'going '
                                                                                                                                           'to '
                                                                                                                                           'stomp '
                                                                                                                                           'on '
                                                                                                                                           'last '
                                                                                                                                           'access '
                                                                                                                                           'time',
                                                                                                                            'type': 'Path'}},
                                                                                    'name': 'Set '
                                                                                            'a '
                                                                                            "file's "
                                                                                            'modification '
                                                                                            'timestamp',
                                                                                    'supported_platforms': ['linux',
                                                                                                            'macos']},
                                                                                   {'auto_generated_guid': '8164a4a6-f99c-4661-ac4f-80f5e4e78d2b',
                                                                                    'description': 'Stomps '
                                                                                                   'on '
                                                                                                   'the '
                                                                                                   'create '
                                                                                                   'timestamp '
                                                                                                   'of '
                                                                                                   'a '
                                                                                                   'file\n'
                                                                                                   '\n'
                                                                                                   'Setting '
                                                                                                   'the '
                                                                                                   'creation '
                                                                                                   'timestamp '
                                                                                                   'requires '
                                                                                                   'changing '
                                                                                                   'the '
                                                                                                   'system '
                                                                                                   'clock '
                                                                                                   'and '
                                                                                                   'reverting.\n'
                                                                                                   'Sudo '
                                                                                                   'or '
                                                                                                   'root '
                                                                                                   'privileges '
                                                                                                   'are '
                                                                                                   'required '
                                                                                                   'to '
                                                                                                   'change '
                                                                                                   'date. '
                                                                                                   'Use '
                                                                                                   'with '
                                                                                                   'caution.\n',
                                                                                    'executor': {'command': 'NOW=$(date)\n'
                                                                                                            'date '
                                                                                                            '-s '
                                                                                                            '"1970-01-01 '
                                                                                                            '00:00:00"\n'
                                                                                                            'touch '
                                                                                                            '#{target_filename}\n'
                                                                                                            'date '
                                                                                                            '-s '
                                                                                                            '"$NOW"\n'
                                                                                                            'stat '
                                                                                                            '#{target_filename}\n',
                                                                                                 'name': 'sh'},
                                                                                    'input_arguments': {'target_filename': {'default': '/opt/filename',
                                                                                                                            'description': 'Path '
                                                                                                                                           'of '
                                                                                                                                           'file '
                                                                                                                                           'that '
                                                                                                                                           'we '
                                                                                                                                           'are '
                                                                                                                                           'going '
                                                                                                                                           'to '
                                                                                                                                           'stomp '
                                                                                                                                           'on '
                                                                                                                                           'last '
                                                                                                                                           'access '
                                                                                                                                           'time',
                                                                                                                            'type': 'Path'}},
                                                                                    'name': 'Set '
                                                                                            'a '
                                                                                            "file's "
                                                                                            'creation '
                                                                                            'timestamp',
                                                                                    'supported_platforms': ['linux',
                                                                                                            'macos']},
                                                                                   {'auto_generated_guid': '631ea661-d661-44b0-abdb-7a7f3fc08e50',
                                                                                    'description': 'Modifies '
                                                                                                   'the '
                                                                                                   '`modify` '
                                                                                                   'and '
                                                                                                   '`access` '
                                                                                                   'timestamps '
                                                                                                   'using '
                                                                                                   'the '
                                                                                                   'timestamps '
                                                                                                   'of '
                                                                                                   'a '
                                                                                                   'specified '
                                                                                                   'reference '
                                                                                                   'file.\n'
                                                                                                   '\n'
                                                                                                   'This '
                                                                                                   'technique '
                                                                                                   'was '
                                                                                                   'used '
                                                                                                   'by '
                                                                                                   'the '
                                                                                                   'threat '
                                                                                                   'actor '
                                                                                                   'Rocke '
                                                                                                   'during '
                                                                                                   'the '
                                                                                                   'compromise '
                                                                                                   'of '
                                                                                                   'Linux '
                                                                                                   'web '
                                                                                                   'servers.\n',
                                                                                    'executor': {'command': 'touch '
                                                                                                            '-acmr '
                                                                                                            '#{reference_file_path} '
                                                                                                            '#{target_file_path}\n',
                                                                                                 'name': 'sh'},
                                                                                    'input_arguments': {'reference_file_path': {'default': '/bin/sh',
                                                                                                                                'description': 'Path '
                                                                                                                                               'of '
                                                                                                                                               'reference '
                                                                                                                                               'file '
                                                                                                                                               'to '
                                                                                                                                               'read '
                                                                                                                                               'timestamps '
                                                                                                                                               'from',
                                                                                                                                'type': 'Path'},
                                                                                                        'target_file_path': {'default': '/opt/filename',
                                                                                                                             'description': 'Path '
                                                                                                                                            'of '
                                                                                                                                            'file '
                                                                                                                                            'to '
                                                                                                                                            'modify '
                                                                                                                                            'timestamps '
                                                                                                                                            'of',
                                                                                                                             'type': 'Path'}},
                                                                                    'name': 'Modify '
                                                                                            'file '
                                                                                            'timestamps '
                                                                                            'using '
                                                                                            'reference '
                                                                                            'file',
                                                                                    'supported_platforms': ['linux',
                                                                                                            'macos']},
                                                                                   {'auto_generated_guid': 'b3b2c408-2ff0-4a33-b89b-1cb46a9e6a9c',
                                                                                    'dependencies': [{'description': 'A '
                                                                                                                     'file '
                                                                                                                     'must '
                                                                                                                     'exist '
                                                                                                                     'at '
                                                                                                                     'the '
                                                                                                                     'path '
                                                                                                                     '(#{file_path}) '
                                                                                                                     'to '
                                                                                                                     'change '
                                                                                                                     'the '
                                                                                                                     'creation '
                                                                                                                     'time '
                                                                                                                     'on\n',
                                                                                                      'get_prereq_command': 'New-Item '
                                                                                                                            '-Path '
                                                                                                                            '#{file_path} '
                                                                                                                            '-Force '
                                                                                                                            '| '
                                                                                                                            'Out-Null\n'
                                                                                                                            'Set-Content '
                                                                                                                            '#{file_path} '
                                                                                                                            '-Value '
                                                                                                                            '"T1551.006 '
                                                                                                                            'Timestomp" '
                                                                                                                            '-Force '
                                                                                                                            '| '
                                                                                                                            'Out-Null\n',
                                                                                                      'prereq_command': 'if '
                                                                                                                        '(Test-Path '
                                                                                                                        '#{file_path}) '
                                                                                                                        '{exit '
                                                                                                                        '0} '
                                                                                                                        'else '
                                                                                                                        '{exit '
                                                                                                                        '1}\n'}],
                                                                                    'dependency_executor_name': 'powershell',
                                                                                    'description': 'Modifies '
                                                                                                   'the '
                                                                                                   'file '
                                                                                                   'creation '
                                                                                                   'timestamp '
                                                                                                   'of '
                                                                                                   'a '
                                                                                                   'specified '
                                                                                                   'file. '
                                                                                                   'This '
                                                                                                   'technique '
                                                                                                   'was '
                                                                                                   'seen '
                                                                                                   'in '
                                                                                                   'use '
                                                                                                   'by '
                                                                                                   'the '
                                                                                                   'Stitch '
                                                                                                   'RAT.\n'
                                                                                                   'To '
                                                                                                   'verify '
                                                                                                   'execution, '
                                                                                                   'use '
                                                                                                   'File '
                                                                                                   'Explorer '
                                                                                                   'to '
                                                                                                   'view '
                                                                                                   'the '
                                                                                                   'Properties '
                                                                                                   'of '
                                                                                                   'the '
                                                                                                   'file '
                                                                                                   'and '
                                                                                                   'observe '
                                                                                                   'that '
                                                                                                   'the '
                                                                                                   'Created '
                                                                                                   'time '
                                                                                                   'is '
                                                                                                   'the '
                                                                                                   'year '
                                                                                                   '1970.\n',
                                                                                    'executor': {'cleanup_command': 'Remove-Item '
                                                                                                                    '#{file_path} '
                                                                                                                    '-Force '
                                                                                                                    '-ErrorAction '
                                                                                                                    'Ignore\n',
                                                                                                 'command': 'Get-ChildItem '
                                                                                                            '#{file_path} '
                                                                                                            '| '
                                                                                                            '% '
                                                                                                            '{ '
                                                                                                            '$_.CreationTime '
                                                                                                            '= '
                                                                                                            '"#{target_date_time}" '
                                                                                                            '}\n',
                                                                                                 'name': 'powershell'},
                                                                                    'input_arguments': {'file_path': {'default': '$env:TEMP\\T1551.006_timestomp.txt',
                                                                                                                      'description': 'Path '
                                                                                                                                     'of '
                                                                                                                                     'file '
                                                                                                                                     'to '
                                                                                                                                     'change '
                                                                                                                                     'creation '
                                                                                                                                     'timestamp',
                                                                                                                      'type': 'Path'},
                                                                                                        'target_date_time': {'default': '01/01/1970 '
                                                                                                                                        '00:00:00',
                                                                                                                             'description': 'Date/time '
                                                                                                                                            'to '
                                                                                                                                            'replace '
                                                                                                                                            'original '
                                                                                                                                            'timestamps '
                                                                                                                                            'with',
                                                                                                                             'type': 'String'}},
                                                                                    'name': 'Windows '
                                                                                            '- '
                                                                                            'Modify '
                                                                                            'file '
                                                                                            'creation '
                                                                                            'timestamp '
                                                                                            'with '
                                                                                            'PowerShell',
                                                                                    'supported_platforms': ['windows']},
                                                                                   {'auto_generated_guid': 'f8f6634d-93e1-4238-8510-f8a90a20dcf2',
                                                                                    'dependencies': [{'description': 'A '
                                                                                                                     'file '
                                                                                                                     'must '
                                                                                                                     'exist '
                                                                                                                     'at '
                                                                                                                     'the '
                                                                                                                     'path '
                                                                                                                     '(#{file_path}) '
                                                                                                                     'to '
                                                                                                                     'change '
                                                                                                                     'the '
                                                                                                                     'modified '
                                                                                                                     'time '
                                                                                                                     'on\n',
                                                                                                      'get_prereq_command': 'New-Item '
                                                                                                                            '-Path '
                                                                                                                            '#{file_path} '
                                                                                                                            '-Force '
                                                                                                                            '| '
                                                                                                                            'Out-Null\n'
                                                                                                                            'Set-Content '
                                                                                                                            '#{file_path} '
                                                                                                                            '-Value '
                                                                                                                            '"T1551.006 '
                                                                                                                            'Timestomp" '
                                                                                                                            '-Force '
                                                                                                                            '| '
                                                                                                                            'Out-Null\n',
                                                                                                      'prereq_command': 'if '
                                                                                                                        '(Test-Path '
                                                                                                                        '#{file_path}) '
                                                                                                                        '{exit '
                                                                                                                        '0} '
                                                                                                                        'else '
                                                                                                                        '{exit '
                                                                                                                        '1}\n'}],
                                                                                    'dependency_executor_name': 'powershell',
                                                                                    'description': 'Modifies '
                                                                                                   'the '
                                                                                                   'file '
                                                                                                   'last '
                                                                                                   'modified '
                                                                                                   'timestamp '
                                                                                                   'of '
                                                                                                   'a '
                                                                                                   'specified '
                                                                                                   'file. '
                                                                                                   'This '
                                                                                                   'technique '
                                                                                                   'was '
                                                                                                   'seen '
                                                                                                   'in '
                                                                                                   'use '
                                                                                                   'by '
                                                                                                   'the '
                                                                                                   'Stitch '
                                                                                                   'RAT.\n'
                                                                                                   'To '
                                                                                                   'verify '
                                                                                                   'execution, '
                                                                                                   'use '
                                                                                                   'File '
                                                                                                   'Explorer '
                                                                                                   'to '
                                                                                                   'view '
                                                                                                   'the '
                                                                                                   'Properties '
                                                                                                   'of '
                                                                                                   'the '
                                                                                                   'file '
                                                                                                   'and '
                                                                                                   'observe '
                                                                                                   'that '
                                                                                                   'the '
                                                                                                   'Modified '
                                                                                                   'time '
                                                                                                   'is '
                                                                                                   'the '
                                                                                                   'year '
                                                                                                   '1970.\n',
                                                                                    'executor': {'cleanup_command': 'Remove-Item '
                                                                                                                    '#{file_path} '
                                                                                                                    '-Force '
                                                                                                                    '-ErrorAction '
                                                                                                                    'Ignore\n',
                                                                                                 'command': 'Get-ChildItem '
                                                                                                            '#{file_path} '
                                                                                                            '| '
                                                                                                            '% '
                                                                                                            '{ '
                                                                                                            '$_.LastWriteTime '
                                                                                                            '= '
                                                                                                            '"#{target_date_time}" '
                                                                                                            '}\n',
                                                                                                 'name': 'powershell'},
                                                                                    'input_arguments': {'file_path': {'default': '$env:TEMP\\T1551.006_timestomp.txt',
                                                                                                                      'description': 'Path '
                                                                                                                                     'of '
                                                                                                                                     'file '
                                                                                                                                     'to '
                                                                                                                                     'change '
                                                                                                                                     'modified '
                                                                                                                                     'timestamp',
                                                                                                                      'type': 'Path'},
                                                                                                        'target_date_time': {'default': '01/01/1970 '
                                                                                                                                        '00:00:00',
                                                                                                                             'description': 'Date/time '
                                                                                                                                            'to '
                                                                                                                                            'replace '
                                                                                                                                            'original '
                                                                                                                                            'timestamps '
                                                                                                                                            'with',
                                                                                                                             'type': 'String'}},
                                                                                    'name': 'Windows '
                                                                                            '- '
                                                                                            'Modify '
                                                                                            'file '
                                                                                            'last '
                                                                                            'modified '
                                                                                            'timestamp '
                                                                                            'with '
                                                                                            'PowerShell',
                                                                                    'supported_platforms': ['windows']},
                                                                                   {'auto_generated_guid': 'da627f63-b9bd-4431-b6f8-c5b44d061a62',
                                                                                    'dependencies': [{'description': 'A '
                                                                                                                     'file '
                                                                                                                     'must '
                                                                                                                     'exist '
                                                                                                                     'at '
                                                                                                                     'the '
                                                                                                                     'path '
                                                                                                                     '(#{file_path}) '
                                                                                                                     'to '
                                                                                                                     'change '
                                                                                                                     'the '
                                                                                                                     'last '
                                                                                                                     'access '
                                                                                                                     'time '
                                                                                                                     'on\n',
                                                                                                      'get_prereq_command': 'New-Item '
                                                                                                                            '-Path '
                                                                                                                            '#{file_path} '
                                                                                                                            '-Force '
                                                                                                                            '| '
                                                                                                                            'Out-Null\n'
                                                                                                                            'Set-Content '
                                                                                                                            '#{file_path} '
                                                                                                                            '-Value '
                                                                                                                            '"T1551.006 '
                                                                                                                            'Timestomp" '
                                                                                                                            '-Force '
                                                                                                                            '| '
                                                                                                                            'Out-Null\n',
                                                                                                      'prereq_command': 'if '
                                                                                                                        '(Test-Path '
                                                                                                                        '#{file_path}) '
                                                                                                                        '{exit '
                                                                                                                        '0} '
                                                                                                                        'else '
                                                                                                                        '{exit '
                                                                                                                        '1}\n'}],
                                                                                    'dependency_executor_name': 'powershell',
                                                                                    'description': 'Modifies '
                                                                                                   'the '
                                                                                                   'last '
                                                                                                   'access '
                                                                                                   'timestamp '
                                                                                                   'of '
                                                                                                   'a '
                                                                                                   'specified '
                                                                                                   'file. '
                                                                                                   'This '
                                                                                                   'technique '
                                                                                                   'was '
                                                                                                   'seen '
                                                                                                   'in '
                                                                                                   'use '
                                                                                                   'by '
                                                                                                   'the '
                                                                                                   'Stitch '
                                                                                                   'RAT.\n'
                                                                                                   'To '
                                                                                                   'verify '
                                                                                                   'execution, '
                                                                                                   'use '
                                                                                                   'File '
                                                                                                   'Explorer '
                                                                                                   'to '
                                                                                                   'view '
                                                                                                   'the '
                                                                                                   'Properties '
                                                                                                   'of '
                                                                                                   'the '
                                                                                                   'file '
                                                                                                   'and '
                                                                                                   'observe '
                                                                                                   'that '
                                                                                                   'the '
                                                                                                   'Accessed '
                                                                                                   'time '
                                                                                                   'is '
                                                                                                   'the '
                                                                                                   'year '
                                                                                                   '1970.\n',
                                                                                    'executor': {'cleanup_command': 'Remove-Item '
                                                                                                                    '#{file_path} '
                                                                                                                    '-Force '
                                                                                                                    '-ErrorAction '
                                                                                                                    'Ignore\n',
                                                                                                 'command': 'Get-ChildItem '
                                                                                                            '#{file_path} '
                                                                                                            '| '
                                                                                                            '% '
                                                                                                            '{ '
                                                                                                            '$_.LastAccessTime '
                                                                                                            '= '
                                                                                                            '"#{target_date_time}" '
                                                                                                            '}\n',
                                                                                                 'name': 'powershell'},
                                                                                    'input_arguments': {'file_path': {'default': '$env:TEMP\\T1551.006_timestomp.txt',
                                                                                                                      'description': 'Path '
                                                                                                                                     'of '
                                                                                                                                     'file '
                                                                                                                                     'to '
                                                                                                                                     'change '
                                                                                                                                     'last '
                                                                                                                                     'access '
                                                                                                                                     'timestamp',
                                                                                                                      'type': 'Path'},
                                                                                                        'target_date_time': {'default': '01/01/1970 '
                                                                                                                                        '00:00:00',
                                                                                                                             'description': 'Date/time '
                                                                                                                                            'to '
                                                                                                                                            'replace '
                                                                                                                                            'original '
                                                                                                                                            'timestamps '
                                                                                                                                            'with',
                                                                                                                             'type': 'String'}},
                                                                                    'name': 'Windows '
                                                                                            '- '
                                                                                            'Modify '
                                                                                            'file '
                                                                                            'last '
                                                                                            'access '
                                                                                            'timestamp '
                                                                                            'with '
                                                                                            'PowerShell',
                                                                                    'supported_platforms': ['windows']},
                                                                                   {'auto_generated_guid': 'd7512c33-3a75-4806-9893-69abc3ccdd43',
                                                                                    'dependencies': [{'description': 'timestomp.ps1 '
                                                                                                                     'must '
                                                                                                                     'be '
                                                                                                                     'present '
                                                                                                                     'in '
                                                                                                                     '#{file_path}.\n',
                                                                                                      'get_prereq_command': 'Invoke-WebRequest '
                                                                                                                            '"https://raw.githubusercontent.com/mitre-attack/attack-arsenal/bc0ba1d88d026396939b6816de608cb279bfd489/adversary_emulation/APT29/CALDERA_DIY/evals/payloads/timestomp.ps1" '
                                                                                                                            '-OutFile '
                                                                                                                            '"#{file_path}\\timestomp.ps1"\n',
                                                                                                      'prereq_command': 'if '
                                                                                                                        '(Test-Path '
                                                                                                                        '#{file_path}\\timestomp.ps1) '
                                                                                                                        '{exit '
                                                                                                                        '0} '
                                                                                                                        'else '
                                                                                                                        '{exit '
                                                                                                                        '1}\n'},
                                                                                                     {'description': 'kxwn.lock '
                                                                                                                     'must '
                                                                                                                     'be '
                                                                                                                     'present '
                                                                                                                     'in '
                                                                                                                     '#{file_path}.\n',
                                                                                                      'get_prereq_command': 'New-Item '
                                                                                                                            '-Path '
                                                                                                                            '#{file_path}\\kxwn.lock '
                                                                                                                            '-ItemType '
                                                                                                                            'File\n',
                                                                                                      'prereq_command': 'if '
                                                                                                                        '(Test-Path '
                                                                                                                        '-path '
                                                                                                                        '"#{file_path}\\kxwn.lock") '
                                                                                                                        '{exit '
                                                                                                                        '0} '
                                                                                                                        'else '
                                                                                                                        '{exit '
                                                                                                                        '1}\n'}],
                                                                                    'dependency_executor_name': 'powershell',
                                                                                    'description': 'Timestomp '
                                                                                                   'kxwn.lock.\n'
                                                                                                   '\n'
                                                                                                   'Successful '
                                                                                                   'execution '
                                                                                                   'will '
                                                                                                   'include '
                                                                                                   'the '
                                                                                                   'placement '
                                                                                                   'of '
                                                                                                   'kxwn.lock '
                                                                                                   'in '
                                                                                                   '#{file_path} '
                                                                                                   'and '
                                                                                                   'execution '
                                                                                                   'of '
                                                                                                   'timestomp.ps1 '
                                                                                                   'to '
                                                                                                   'modify '
                                                                                                   'the '
                                                                                                   'time '
                                                                                                   'of '
                                                                                                   'the '
                                                                                                   '.lock '
                                                                                                   'file. \n'
                                                                                                   '\n'
                                                                                                   '[Mitre '
                                                                                                   'ATT&CK '
                                                                                                   'Evals](https://github.com/mitre-attack/attack-arsenal/blob/master/adversary_emulation/APT29/CALDERA_DIY/evals/data/abilities/defensive-evasion/4a2ad84e-a93a-4b2e-b1f0-c354d6a41278.yml)\n',
                                                                                    'executor': {'cleanup_command': 'Remove-Item '
                                                                                                                    '#{file_path}\\timestomp.ps1 '
                                                                                                                    '-ErrorAction '
                                                                                                                    'Ignore\n'
                                                                                                                    'Remove-Item '
                                                                                                                    '#{file_path}\\kxwn.lock '
                                                                                                                    '-ErrorAction '
                                                                                                                    'Ignore',
                                                                                                 'command': 'import-module '
                                                                                                            '#{file_path}\\timestomp.ps1\n'
                                                                                                            'timestomp '
                                                                                                            '-dest '
                                                                                                            '"#{file_path}\\kxwn.lock"\n',
                                                                                                 'name': 'powershell'},
                                                                                    'input_arguments': {'file_path': {'default': '$env:appdata\\Microsoft',
                                                                                                                      'description': 'File '
                                                                                                                                     'path '
                                                                                                                                     'for '
                                                                                                                                     'timestomp '
                                                                                                                                     'payload',
                                                                                                                      'type': 'String'}},
                                                                                    'name': 'Windows '
                                                                                            '- '
                                                                                            'Timestomp '
                                                                                            'a '
                                                                                            'File',
                                                                                    'supported_platforms': ['windows']}],
                                                                  'attack_technique': 'T1070.006',
                                                                  'display_name': 'Indicator '
                                                                                  'Removal '
                                                                                  'on '
                                                                                  'Host: '
                                                                                  'Timestomp'}}]
```

# Tactics


* [Defense Evasion](../tactics/Defense-Evasion.md)


# Mitigations


* [Timestomp Mitigation](../mitigations/Timestomp-Mitigation.md)


# Actors


* [APT28](../actors/APT28.md)

* [APT32](../actors/APT32.md)
    
* [Lazarus Group](../actors/Lazarus-Group.md)
    
* [TEMP.Veles](../actors/TEMP.Veles.md)
    
* [Rocke](../actors/Rocke.md)
    
