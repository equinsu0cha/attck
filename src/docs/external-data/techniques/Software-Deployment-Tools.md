
# Software Deployment Tools

## Description

### MITRE Description

> Adversaries may gain access to and use third-party software suites installed within an enterprise network, such as administration, monitoring, and deployment systems, to move laterally through the network. Third-party applications and software deployment systems may be in use in the network environment for administration purposes (e.g., SCCM, VNC, HBSS, Altiris, etc.).

Access to a third-party network-wide or enterprise-wide software system may enable an adversary to have remote code execution on all systems that are connected to such a system. The access may be used to laterally move to other systems, gather information, or cause a specific effect, such as wiping the hard drives on all endpoints.

The permissions required for this action vary by system configuration; local credentials may be sufficient with direct access to the third-party system, or specific domain credentials may be required. However, the system may require an administrative account to log in or to perform it's intended purpose.

## Aliases

```

```

## Additional Attributes

* Bypass: None
* Effective Permissions: None
* Network: None
* Permissions: ['User', 'Administrator', 'SYSTEM']
* Platforms: ['Linux', 'macOS', 'Windows']
* Remote: True
* Type: attack-pattern
* Wiki: https://attack.mitre.org/techniques/T1072

## Potential Commands

```

```

## Commands Dataset

```

```

## Potential Detections

```json
[{'data_source': ['4688', 'Process Execution']},
 {'data_source': ['5156', 'Windows Firewall']},
 {'data_source': ['4663', 'File monitoring']},
 {'data_source': ['4657', 'Windows Registry']},
 {'data_source': ['Binary file metadata']},
 {'data_source': ['Third-party application logs']},
 {'data_source': ['4688', 'Process Execution']},
 {'data_source': ['5156', 'Windows Firewall']},
 {'data_source': ['4663', 'File monitoring']},
 {'data_source': ['4657', 'Windows Registry']},
 {'data_source': ['LOG-MD B9', 'Binary file metadata']},
 {'data_source': ['Third-party application logs']}]
```

## Potential Queries

```json

```

## Raw Dataset

```json

```

# Tactics


* [Execution](../tactics/Execution.md)

* [Lateral Movement](../tactics/Lateral-Movement.md)
    

# Mitigations


* [Third-party Software Mitigation](../mitigations/Third-party-Software-Mitigation.md)

* [User Training](../mitigations/User-Training.md)
    
* [Update Software](../mitigations/Update-Software.md)
    
* [Remote Data Storage](../mitigations/Remote-Data-Storage.md)
    
* [Network Segmentation](../mitigations/Network-Segmentation.md)
    
* [Password Policies](../mitigations/Password-Policies.md)
    
* [Privileged Account Management](../mitigations/Privileged-Account-Management.md)
    
* [Multi-factor Authentication](../mitigations/Multi-factor-Authentication.md)
    
* [Active Directory Configuration](../mitigations/Active-Directory-Configuration.md)
    
* [User Account Management](../mitigations/User-Account-Management.md)
    

# Actors


* [APT32](../actors/APT32.md)

* [Threat Group-1314](../actors/Threat-Group-1314.md)
    
* [Silence](../actors/Silence.md)
    
