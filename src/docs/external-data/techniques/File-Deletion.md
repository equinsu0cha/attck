
# File Deletion

## Description

### MITRE Description

> Adversaries may delete files left behind by the actions of their intrusion activity. Malware, tools, or other non-native files dropped or created on a system by an adversary may leave traces to indicate to what was done within a network and how. Removal of these files can occur during an intrusion, or as part of a post-intrusion process to minimize the adversary's footprint.

There are tools available from the host operating system to perform cleanup, but adversaries may use other tools as well. Examples include native [cmd](https://attack.mitre.org/software/S0106) functions such as DEL, secure deletion tools such as Windows Sysinternals SDelete, or other third-party file deletion tools. (Citation: Trend Micro APT Attack Tools)

## Aliases

```

```

## Additional Attributes

* Bypass: ['Host forensic analysis']
* Effective Permissions: None
* Network: None
* Permissions: ['User']
* Platforms: ['Linux', 'macOS', 'Windows']
* Remote: None
* Type: attack-pattern
* Wiki: https://attack.mitre.org/techniques/T1070/004

## Potential Commands

```
Remove-Item -path $env:TEMP\deleteme_T1551.004
rmdir /s /q %temp%\deleteme_T1551.004
rm -rf /tmp/victim-files
rm -rf / --no-preserve-root > /dev/null 2> /dev/null
Remove-Item $env:TEMP\TeamViewer_54.log
del /f %temp%\deleteme_T1551.004
shred -u /tmp/victim-shred.txt
Remove-Item -Path (Join-Path "$Env:SystemRoot\prefetch\" (Get-ChildItem -Path "$Env:SystemRoot\prefetch\*.pf" -Name)[0])
rm -f /tmp/victim-files/a
Remove-Item -Path $env:TEMP\deleteme_folder_T1551.004 -Recurse
```

## Commands Dataset

```
[{'command': 'rm -f /tmp/victim-files/a\n',
  'name': None,
  'source': 'atomics/T1070.004/T1070.004.yaml'},
 {'command': 'rm -rf /tmp/victim-files\n',
  'name': None,
  'source': 'atomics/T1070.004/T1070.004.yaml'},
 {'command': 'shred -u /tmp/victim-shred.txt\n',
  'name': None,
  'source': 'atomics/T1070.004/T1070.004.yaml'},
 {'command': 'del /f %temp%\\deleteme_T1551.004\n',
  'name': None,
  'source': 'atomics/T1070.004/T1070.004.yaml'},
 {'command': 'rmdir /s /q %temp%\\deleteme_T1551.004\n',
  'name': None,
  'source': 'atomics/T1070.004/T1070.004.yaml'},
 {'command': 'Remove-Item -path $env:TEMP\\deleteme_T1551.004\n',
  'name': None,
  'source': 'atomics/T1070.004/T1070.004.yaml'},
 {'command': 'Remove-Item -Path $env:TEMP\\deleteme_folder_T1551.004 '
             '-Recurse\n',
  'name': None,
  'source': 'atomics/T1070.004/T1070.004.yaml'},
 {'command': 'rm -rf / --no-preserve-root > /dev/null 2> /dev/null\n',
  'name': None,
  'source': 'atomics/T1070.004/T1070.004.yaml'},
 {'command': 'Remove-Item -Path (Join-Path "$Env:SystemRoot\\prefetch\\" '
             '(Get-ChildItem -Path "$Env:SystemRoot\\prefetch\\*.pf" '
             '-Name)[0])\n',
  'name': None,
  'source': 'atomics/T1070.004/T1070.004.yaml'},
 {'command': 'Remove-Item $env:TEMP\\TeamViewer_54.log\n',
  'name': None,
  'source': 'atomics/T1070.004/T1070.004.yaml'}]
```

## Potential Detections

```json

```

## Potential Queries

```json

```

## Raw Dataset

```json
[{'Atomic Red Team Test - Indicator Removal on Host: File Deletion': {'atomic_tests': [{'auto_generated_guid': '562d737f-2fc6-4b09-8c2a-7f8ff0828480',
                                                                                        'description': 'Delete '
                                                                                                       'a '
                                                                                                       'single '
                                                                                                       'file '
                                                                                                       'from '
                                                                                                       'the '
                                                                                                       'temporary '
                                                                                                       'directory\n',
                                                                                        'executor': {'command': 'rm '
                                                                                                                '-f '
                                                                                                                '#{file_to_delete}\n',
                                                                                                     'name': 'sh'},
                                                                                        'input_arguments': {'file_to_delete': {'default': '/tmp/victim-files/a',
                                                                                                                               'description': 'Path '
                                                                                                                                              'of '
                                                                                                                                              'file '
                                                                                                                                              'to '
                                                                                                                                              'delete',
                                                                                                                               'type': 'Path'}},
                                                                                        'name': 'Delete '
                                                                                                'a '
                                                                                                'single '
                                                                                                'file '
                                                                                                '- '
                                                                                                'Linux/macOS',
                                                                                        'supported_platforms': ['linux',
                                                                                                                'macos']},
                                                                                       {'auto_generated_guid': 'a415f17e-ce8d-4ce2-a8b4-83b674e7017e',
                                                                                        'description': 'Recursively '
                                                                                                       'delete '
                                                                                                       'the '
                                                                                                       'temporary '
                                                                                                       'directory '
                                                                                                       'and '
                                                                                                       'all '
                                                                                                       'files '
                                                                                                       'contained '
                                                                                                       'within '
                                                                                                       'it\n',
                                                                                        'executor': {'command': 'rm '
                                                                                                                '-rf '
                                                                                                                '#{folder_to_delete}\n',
                                                                                                     'name': 'sh'},
                                                                                        'input_arguments': {'folder_to_delete': {'default': '/tmp/victim-files',
                                                                                                                                 'description': 'Path '
                                                                                                                                                'of '
                                                                                                                                                'folder '
                                                                                                                                                'to '
                                                                                                                                                'delete',
                                                                                                                                 'type': 'Path'}},
                                                                                        'name': 'Delete '
                                                                                                'an '
                                                                                                'entire '
                                                                                                'folder '
                                                                                                '- '
                                                                                                'Linux/macOS',
                                                                                        'supported_platforms': ['linux',
                                                                                                                'macos']},
                                                                                       {'auto_generated_guid': '039b4b10-2900-404b-b67f-4b6d49aa6499',
                                                                                        'description': 'Use '
                                                                                                       'the '
                                                                                                       '`shred` '
                                                                                                       'command '
                                                                                                       'to '
                                                                                                       'overwrite '
                                                                                                       'the '
                                                                                                       'temporary '
                                                                                                       'file '
                                                                                                       'and '
                                                                                                       'then '
                                                                                                       'delete '
                                                                                                       'it\n',
                                                                                        'executor': {'command': 'shred '
                                                                                                                '-u '
                                                                                                                '#{file_to_shred}\n',
                                                                                                     'name': 'sh'},
                                                                                        'input_arguments': {'file_to_shred': {'default': '/tmp/victim-shred.txt',
                                                                                                                              'description': 'Path '
                                                                                                                                             'of '
                                                                                                                                             'file '
                                                                                                                                             'to '
                                                                                                                                             'shred',
                                                                                                                              'type': 'Path'}},
                                                                                        'name': 'Overwrite '
                                                                                                'and '
                                                                                                'delete '
                                                                                                'a '
                                                                                                'file '
                                                                                                'with '
                                                                                                'shred',
                                                                                        'supported_platforms': ['linux']},
                                                                                       {'auto_generated_guid': '861ea0b4-708a-4d17-848d-186c9c7f17e3',
                                                                                        'dependencies': [{'description': 'The '
                                                                                                                         'file '
                                                                                                                         'to '
                                                                                                                         'delete '
                                                                                                                         'must '
                                                                                                                         'exist '
                                                                                                                         'on '
                                                                                                                         'disk '
                                                                                                                         'at '
                                                                                                                         'specified '
                                                                                                                         'location '
                                                                                                                         '(#{file_to_delete})\n',
                                                                                                          'get_prereq_command': 'echo '
                                                                                                                                'deleteme_T1551.004 '
                                                                                                                                '>> '
                                                                                                                                '#{file_to_delete}\n',
                                                                                                          'prereq_command': 'IF '
                                                                                                                            'EXIST '
                                                                                                                            '"#{file_to_delete}" '
                                                                                                                            '( '
                                                                                                                            'EXIT '
                                                                                                                            '0 '
                                                                                                                            ') '
                                                                                                                            'ELSE '
                                                                                                                            '( '
                                                                                                                            'EXIT '
                                                                                                                            '1 '
                                                                                                                            ')\n'}],
                                                                                        'dependency_executor_name': 'command_prompt',
                                                                                        'description': 'Delete '
                                                                                                       'a '
                                                                                                       'single '
                                                                                                       'file '
                                                                                                       'from '
                                                                                                       'the '
                                                                                                       'temporary '
                                                                                                       'directory '
                                                                                                       'using '
                                                                                                       'cmd.exe.\n'
                                                                                                       'Upon '
                                                                                                       'execution, '
                                                                                                       'no '
                                                                                                       'output '
                                                                                                       'will '
                                                                                                       'be '
                                                                                                       'displayed. '
                                                                                                       'Use '
                                                                                                       'File '
                                                                                                       'Explorer '
                                                                                                       'to '
                                                                                                       'verify '
                                                                                                       'the '
                                                                                                       'file '
                                                                                                       'was '
                                                                                                       'deleted.\n',
                                                                                        'executor': {'command': 'del '
                                                                                                                '/f '
                                                                                                                '#{file_to_delete}\n',
                                                                                                     'name': 'command_prompt'},
                                                                                        'input_arguments': {'file_to_delete': {'default': '%temp%\\deleteme_T1551.004',
                                                                                                                               'description': 'File '
                                                                                                                                              'to '
                                                                                                                                              'delete. '
                                                                                                                                              'Run '
                                                                                                                                              'the '
                                                                                                                                              'prereq '
                                                                                                                                              'command '
                                                                                                                                              'to '
                                                                                                                                              'create '
                                                                                                                                              'it '
                                                                                                                                              'if '
                                                                                                                                              'it '
                                                                                                                                              'does '
                                                                                                                                              'not '
                                                                                                                                              'exist.',
                                                                                                                               'type': 'string'}},
                                                                                        'name': 'Delete '
                                                                                                'a '
                                                                                                'single '
                                                                                                'file '
                                                                                                '- '
                                                                                                'Windows '
                                                                                                'cmd',
                                                                                        'supported_platforms': ['windows']},
                                                                                       {'auto_generated_guid': 'ded937c4-2add-42f7-9c2c-c742b7a98698',
                                                                                        'dependencies': [{'description': 'The '
                                                                                                                         'file '
                                                                                                                         'to '
                                                                                                                         'delete '
                                                                                                                         'must '
                                                                                                                         'exist '
                                                                                                                         'on '
                                                                                                                         'disk '
                                                                                                                         'at '
                                                                                                                         'specified '
                                                                                                                         'location '
                                                                                                                         '(#{folder_to_delete})\n',
                                                                                                          'get_prereq_command': 'mkdir '
                                                                                                                                '#{folder_to_delete}\n',
                                                                                                          'prereq_command': 'IF '
                                                                                                                            'EXIST '
                                                                                                                            '"#{folder_to_delete}" '
                                                                                                                            '( '
                                                                                                                            'EXIT '
                                                                                                                            '0 '
                                                                                                                            ') '
                                                                                                                            'ELSE '
                                                                                                                            '( '
                                                                                                                            'EXIT '
                                                                                                                            '1 '
                                                                                                                            ')\n'}],
                                                                                        'dependency_executor_name': 'command_prompt',
                                                                                        'description': 'Recursively '
                                                                                                       'delete '
                                                                                                       'a '
                                                                                                       'folder '
                                                                                                       'in '
                                                                                                       'the '
                                                                                                       'temporary '
                                                                                                       'directory '
                                                                                                       'using '
                                                                                                       'cmd.exe.\n'
                                                                                                       'Upon '
                                                                                                       'execution, '
                                                                                                       'no '
                                                                                                       'output '
                                                                                                       'will '
                                                                                                       'be '
                                                                                                       'displayed. '
                                                                                                       'Use '
                                                                                                       'File '
                                                                                                       'Explorer '
                                                                                                       'to '
                                                                                                       'verify '
                                                                                                       'the '
                                                                                                       'folder '
                                                                                                       'was '
                                                                                                       'deleted.\n',
                                                                                        'executor': {'command': 'rmdir '
                                                                                                                '/s '
                                                                                                                '/q '
                                                                                                                '#{folder_to_delete}\n',
                                                                                                     'name': 'command_prompt'},
                                                                                        'input_arguments': {'folder_to_delete': {'default': '%temp%\\deleteme_T1551.004',
                                                                                                                                 'description': 'Folder '
                                                                                                                                                'to '
                                                                                                                                                'delete. '
                                                                                                                                                'Run '
                                                                                                                                                'the '
                                                                                                                                                'prereq '
                                                                                                                                                'command '
                                                                                                                                                'to '
                                                                                                                                                'create '
                                                                                                                                                'it '
                                                                                                                                                'if '
                                                                                                                                                'it '
                                                                                                                                                'does '
                                                                                                                                                'not '
                                                                                                                                                'exist.',
                                                                                                                                 'type': 'string'}},
                                                                                        'name': 'Delete '
                                                                                                'an '
                                                                                                'entire '
                                                                                                'folder '
                                                                                                '- '
                                                                                                'Windows '
                                                                                                'cmd',
                                                                                        'supported_platforms': ['windows']},
                                                                                       {'auto_generated_guid': '9dee89bd-9a98-4c4f-9e2d-4256690b0e72',
                                                                                        'dependencies': [{'description': 'The '
                                                                                                                         'file '
                                                                                                                         'to '
                                                                                                                         'delete '
                                                                                                                         'must '
                                                                                                                         'exist '
                                                                                                                         'on '
                                                                                                                         'disk '
                                                                                                                         'at '
                                                                                                                         'specified '
                                                                                                                         'location '
                                                                                                                         '(#{file_to_delete})\n',
                                                                                                          'get_prereq_command': 'New-Item '
                                                                                                                                '-Path '
                                                                                                                                '#{file_to_delete} '
                                                                                                                                '| '
                                                                                                                                'Out-Null\n',
                                                                                                          'prereq_command': 'if '
                                                                                                                            '(Test-Path '
                                                                                                                            '#{file_to_delete}) '
                                                                                                                            '{exit '
                                                                                                                            '0} '
                                                                                                                            'else '
                                                                                                                            '{exit '
                                                                                                                            '1}\n'}],
                                                                                        'dependency_executor_name': 'powershell',
                                                                                        'description': 'Delete '
                                                                                                       'a '
                                                                                                       'single '
                                                                                                       'file '
                                                                                                       'from '
                                                                                                       'the '
                                                                                                       'temporary '
                                                                                                       'directory '
                                                                                                       'using '
                                                                                                       'Powershell. '
                                                                                                       'Upon '
                                                                                                       'execution, '
                                                                                                       'no '
                                                                                                       'output '
                                                                                                       'will '
                                                                                                       'be '
                                                                                                       'displayed. '
                                                                                                       'Use '
                                                                                                       'File '
                                                                                                       'Explorer '
                                                                                                       'to '
                                                                                                       'verify '
                                                                                                       'the '
                                                                                                       'file '
                                                                                                       'was '
                                                                                                       'deleted.\n',
                                                                                        'executor': {'command': 'Remove-Item '
                                                                                                                '-path '
                                                                                                                '#{file_to_delete}\n',
                                                                                                     'name': 'powershell'},
                                                                                        'input_arguments': {'file_to_delete': {'default': '$env:TEMP\\deleteme_T1551.004',
                                                                                                                               'description': 'File '
                                                                                                                                              'to '
                                                                                                                                              'delete. '
                                                                                                                                              'Run '
                                                                                                                                              'the '
                                                                                                                                              'prereq '
                                                                                                                                              'command '
                                                                                                                                              'to '
                                                                                                                                              'create '
                                                                                                                                              'it '
                                                                                                                                              'if '
                                                                                                                                              'it '
                                                                                                                                              'does '
                                                                                                                                              'not '
                                                                                                                                              'exist.',
                                                                                                                               'type': 'string'}},
                                                                                        'name': 'Delete '
                                                                                                'a '
                                                                                                'single '
                                                                                                'file '
                                                                                                '- '
                                                                                                'Windows '
                                                                                                'PowerShell',
                                                                                        'supported_platforms': ['windows']},
                                                                                       {'auto_generated_guid': 'edd779e4-a509-4cba-8dfa-a112543dbfb1',
                                                                                        'dependencies': [{'description': 'The '
                                                                                                                         'folder '
                                                                                                                         'to '
                                                                                                                         'delete '
                                                                                                                         'must '
                                                                                                                         'exist '
                                                                                                                         'on '
                                                                                                                         'disk '
                                                                                                                         'at '
                                                                                                                         'specified '
                                                                                                                         'location '
                                                                                                                         '(#{folder_to_delete})\n',
                                                                                                          'get_prereq_command': 'New-Item '
                                                                                                                                '-Path '
                                                                                                                                '#{folder_to_delete} '
                                                                                                                                '-Type '
                                                                                                                                'Directory '
                                                                                                                                '| '
                                                                                                                                'Out-Null\n',
                                                                                                          'prereq_command': 'if '
                                                                                                                            '(Test-Path '
                                                                                                                            '#{folder_to_delete}) '
                                                                                                                            '{exit '
                                                                                                                            '0} '
                                                                                                                            'else '
                                                                                                                            '{exit '
                                                                                                                            '1}\n'}],
                                                                                        'dependency_executor_name': 'powershell',
                                                                                        'description': 'Recursively '
                                                                                                       'delete '
                                                                                                       'a '
                                                                                                       'folder '
                                                                                                       'in '
                                                                                                       'the '
                                                                                                       'temporary '
                                                                                                       'directory '
                                                                                                       'using '
                                                                                                       'Powershell. '
                                                                                                       'Upon '
                                                                                                       'execution, '
                                                                                                       'no '
                                                                                                       'output '
                                                                                                       'will '
                                                                                                       'be '
                                                                                                       'displayed. '
                                                                                                       'Use '
                                                                                                       'File '
                                                                                                       'Explorer '
                                                                                                       'to '
                                                                                                       'verify '
                                                                                                       'the '
                                                                                                       'folder '
                                                                                                       'was '
                                                                                                       'deleted.\n',
                                                                                        'executor': {'command': 'Remove-Item '
                                                                                                                '-Path '
                                                                                                                '#{folder_to_delete} '
                                                                                                                '-Recurse\n',
                                                                                                     'name': 'powershell'},
                                                                                        'input_arguments': {'folder_to_delete': {'default': '$env:TEMP\\deleteme_folder_T1551.004',
                                                                                                                                 'description': 'Folder '
                                                                                                                                                'to '
                                                                                                                                                'delete. '
                                                                                                                                                'Run '
                                                                                                                                                'the '
                                                                                                                                                'prereq '
                                                                                                                                                'command '
                                                                                                                                                'to '
                                                                                                                                                'create '
                                                                                                                                                'it '
                                                                                                                                                'if '
                                                                                                                                                'it '
                                                                                                                                                'does '
                                                                                                                                                'not '
                                                                                                                                                'exist.',
                                                                                                                                 'type': 'string'}},
                                                                                        'name': 'Delete '
                                                                                                'an '
                                                                                                'entire '
                                                                                                'folder '
                                                                                                '- '
                                                                                                'Windows '
                                                                                                'PowerShell',
                                                                                        'supported_platforms': ['windows']},
                                                                                       {'auto_generated_guid': 'f3aa95fe-4f10-4485-ad26-abf22a764c52',
                                                                                        'description': 'This '
                                                                                                       'test '
                                                                                                       'deletes '
                                                                                                       'the '
                                                                                                       'entire '
                                                                                                       'root '
                                                                                                       'filesystem '
                                                                                                       'of '
                                                                                                       'a '
                                                                                                       'Linux '
                                                                                                       'system. '
                                                                                                       'This '
                                                                                                       'technique '
                                                                                                       'was '
                                                                                                       'used '
                                                                                                       'by '
                                                                                                       'Amnesia '
                                                                                                       'IoT '
                                                                                                       'malware '
                                                                                                       'to '
                                                                                                       'avoid '
                                                                                                       'analysis. '
                                                                                                       'This '
                                                                                                       'test '
                                                                                                       'is '
                                                                                                       'dangerous '
                                                                                                       'and '
                                                                                                       'destructive, '
                                                                                                       'do '
                                                                                                       'NOT '
                                                                                                       'use '
                                                                                                       'on '
                                                                                                       'production '
                                                                                                       'equipment.\n',
                                                                                        'executor': {'command': 'rm '
                                                                                                                '-rf '
                                                                                                                '/ '
                                                                                                                '--no-preserve-root '
                                                                                                                '> '
                                                                                                                '/dev/null '
                                                                                                                '2> '
                                                                                                                '/dev/null\n',
                                                                                                     'name': 'bash'},
                                                                                        'name': 'Delete '
                                                                                                'Filesystem '
                                                                                                '- '
                                                                                                'Linux',
                                                                                        'supported_platforms': ['linux']},
                                                                                       {'auto_generated_guid': '36f96049-0ad7-4a5f-8418-460acaeb92fb',
                                                                                        'description': 'Delete '
                                                                                                       'a '
                                                                                                       'single '
                                                                                                       'prefetch '
                                                                                                       'file.  '
                                                                                                       'Deletion '
                                                                                                       'of '
                                                                                                       'prefetch '
                                                                                                       'files '
                                                                                                       'is '
                                                                                                       'a '
                                                                                                       'known '
                                                                                                       'anti-forensic '
                                                                                                       'technique. '
                                                                                                       'To '
                                                                                                       'verify '
                                                                                                       'execution, '
                                                                                                       'Run '
                                                                                                       '"(Get-ChildItem '
                                                                                                       '-Path '
                                                                                                       '"$Env:SystemRoot\\prefetch\\*.pf" '
                                                                                                       '| '
                                                                                                       'Measure-Object).Count"\n'
                                                                                                       'before '
                                                                                                       'and '
                                                                                                       'after '
                                                                                                       'the '
                                                                                                       'test '
                                                                                                       'to '
                                                                                                       'verify '
                                                                                                       'that '
                                                                                                       'the '
                                                                                                       'number '
                                                                                                       'of '
                                                                                                       'prefetch '
                                                                                                       'files '
                                                                                                       'decreases '
                                                                                                       'by '
                                                                                                       '1.\n',
                                                                                        'executor': {'command': 'Remove-Item '
                                                                                                                '-Path '
                                                                                                                '(Join-Path '
                                                                                                                '"$Env:SystemRoot\\prefetch\\" '
                                                                                                                '(Get-ChildItem '
                                                                                                                '-Path '
                                                                                                                '"$Env:SystemRoot\\prefetch\\*.pf" '
                                                                                                                '-Name)[0])\n',
                                                                                                     'elevation_required': True,
                                                                                                     'name': 'powershell'},
                                                                                        'name': 'Delete-PrefetchFile',
                                                                                        'supported_platforms': ['windows']},
                                                                                       {'auto_generated_guid': '69f50a5f-967c-4327-a5bb-e1a9a9983785',
                                                                                        'dependencies': [{'description': 'The '
                                                                                                                         'folder '
                                                                                                                         'to '
                                                                                                                         'delete '
                                                                                                                         'must '
                                                                                                                         'exist '
                                                                                                                         'on '
                                                                                                                         'disk '
                                                                                                                         'at '
                                                                                                                         'specified '
                                                                                                                         'location '
                                                                                                                         '(#{teamviewer_log_file})\n',
                                                                                                          'get_prereq_command': 'New-Item '
                                                                                                                                '-Path '
                                                                                                                                '#{teamviewer_log_file} '
                                                                                                                                '| '
                                                                                                                                'Out-Null\n',
                                                                                                          'prereq_command': 'if '
                                                                                                                            '(Test-Path '
                                                                                                                            '#{teamviewer_log_file}) '
                                                                                                                            '{exit '
                                                                                                                            '0} '
                                                                                                                            'else '
                                                                                                                            '{exit '
                                                                                                                            '1}\n'}],
                                                                                        'dependency_executor_name': 'powershell',
                                                                                        'description': 'Adversaries '
                                                                                                       'may '
                                                                                                       'delete '
                                                                                                       'TeamViewer '
                                                                                                       'log '
                                                                                                       'files '
                                                                                                       'to '
                                                                                                       'hide '
                                                                                                       'activity. '
                                                                                                       'This '
                                                                                                       'should '
                                                                                                       'provide '
                                                                                                       'a '
                                                                                                       'high '
                                                                                                       'true-positive '
                                                                                                       'alert '
                                                                                                       'ration.\n'
                                                                                                       'This '
                                                                                                       'test '
                                                                                                       'just '
                                                                                                       'places '
                                                                                                       'the '
                                                                                                       'files '
                                                                                                       'in '
                                                                                                       'a '
                                                                                                       'non-TeamViewer '
                                                                                                       'folder, '
                                                                                                       'a '
                                                                                                       'detection '
                                                                                                       'would '
                                                                                                       'just '
                                                                                                       'check '
                                                                                                       'for '
                                                                                                       'a '
                                                                                                       'deletion '
                                                                                                       'event '
                                                                                                       'matching '
                                                                                                       'the '
                                                                                                       'TeamViewer\n'
                                                                                                       'log '
                                                                                                       'file '
                                                                                                       'format '
                                                                                                       'of '
                                                                                                       'TeamViewer_##.log. '
                                                                                                       'Upon '
                                                                                                       'execution, '
                                                                                                       'no '
                                                                                                       'output '
                                                                                                       'will '
                                                                                                       'be '
                                                                                                       'displayed. '
                                                                                                       'Use '
                                                                                                       'File '
                                                                                                       'Explorer '
                                                                                                       'to '
                                                                                                       'verify '
                                                                                                       'the '
                                                                                                       'folder '
                                                                                                       'was '
                                                                                                       'deleted.\n'
                                                                                                       '\n'
                                                                                                       'https://twitter.com/SBousseaden/status/1197524463304290305?s=20\n',
                                                                                        'executor': {'command': 'Remove-Item '
                                                                                                                '#{teamviewer_log_file}\n',
                                                                                                     'name': 'powershell'},
                                                                                        'input_arguments': {'teamviewer_log_file': {'default': '$env:TEMP\\TeamViewer_54.log',
                                                                                                                                    'description': 'Teamviewer '
                                                                                                                                                   'log '
                                                                                                                                                   'file '
                                                                                                                                                   'to '
                                                                                                                                                   'delete. '
                                                                                                                                                   'Run '
                                                                                                                                                   'the '
                                                                                                                                                   'prereq '
                                                                                                                                                   'command '
                                                                                                                                                   'to '
                                                                                                                                                   'create '
                                                                                                                                                   'it '
                                                                                                                                                   'if '
                                                                                                                                                   'it '
                                                                                                                                                   'does '
                                                                                                                                                   'not '
                                                                                                                                                   'exist.',
                                                                                                                                    'type': 'string'}},
                                                                                        'name': 'Delete '
                                                                                                'TeamViewer '
                                                                                                'Log '
                                                                                                'Files',
                                                                                        'supported_platforms': ['windows']}],
                                                                      'attack_technique': 'T1070.004',
                                                                      'display_name': 'Indicator '
                                                                                      'Removal '
                                                                                      'on '
                                                                                      'Host: '
                                                                                      'File '
                                                                                      'Deletion'}}]
```

# Tactics


* [Defense Evasion](../tactics/Defense-Evasion.md)


# Mitigations


* [File Deletion Mitigation](../mitigations/File-Deletion-Mitigation.md)


# Actors


* [OilRig](../actors/OilRig.md)

* [Honeybee](../actors/Honeybee.md)
    
* [Group5](../actors/Group5.md)
    
* [FIN5](../actors/FIN5.md)
    
* [Patchwork](../actors/Patchwork.md)
    
* [Lazarus Group](../actors/Lazarus-Group.md)
    
* [FIN10](../actors/FIN10.md)
    
* [BRONZE BUTLER](../actors/BRONZE-BUTLER.md)
    
* [FIN8](../actors/FIN8.md)
    
* [Threat Group-3390](../actors/Threat-Group-3390.md)
    
* [Cobalt Group](../actors/Cobalt-Group.md)
    
* [APT29](../actors/APT29.md)
    
* [Dragonfly 2.0](../actors/Dragonfly-2.0.md)
    
* [APT28](../actors/APT28.md)
    
* [Magic Hound](../actors/Magic-Hound.md)
    
* [menuPass](../actors/menuPass.md)
    
* [APT3](../actors/APT3.md)
    
* [APT38](../actors/APT38.md)
    
* [APT18](../actors/APT18.md)
    
* [APT32](../actors/APT32.md)
    
* [TEMP.Veles](../actors/TEMP.Veles.md)
    
* [The White Company](../actors/The-White-Company.md)
    
* [Silence](../actors/Silence.md)
    
* [Kimsuky](../actors/Kimsuky.md)
    
* [APT41](../actors/APT41.md)
    
* [Wizard Spider](../actors/Wizard-Spider.md)
    
* [Gamaredon Group](../actors/Gamaredon-Group.md)
    
* [Tropic Trooper](../actors/Tropic-Trooper.md)
    
* [Rocke](../actors/Rocke.md)
    
* [Sandworm Team](../actors/Sandworm-Team.md)
    
