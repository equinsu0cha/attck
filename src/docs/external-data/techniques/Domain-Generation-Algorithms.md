
# Domain Generation Algorithms

## Description

### MITRE Description

> Adversaries may make use of Domain Generation Algorithms (DGAs) to dynamically identify a destination domain for command and control traffic rather than relying on a list of static IP addresses or domains. This has the advantage of making it much harder for defenders block, track, or take over the command and control channel, as there potentially could be thousands of domains that malware can check for instructions.(Citation: Cybereason Dissecting DGAs)(Citation: Cisco Umbrella DGA)(Citation: Unit 42 DGA Feb 2019)

DGAs can take the form of apparently random or “gibberish” strings (ex: istgmxdejdnxuyla.ru) when they construct domain names by generating each letter. Alternatively, some DGAs employ whole words as the unit by concatenating words together instead of letters (ex: cityjulydish.net). Many DGAs are time-based, generating a different domain for each time period (hourly, daily, monthly, etc). Others incorporate a seed value as well to make predicting future domains more difficult for defenders.(Citation: Cybereason Dissecting DGAs)(Citation: Cisco Umbrella DGA)(Citation: Talos CCleanup 2017)(Citation: Akamai DGA Mitigation)

Adversaries may use DGAs for the purpose of [Fallback Channels](https://attack.mitre.org/techniques/T1008). When contact is lost with the primary command and control server malware may employ a DGA as a means to reestablishing command and control.(Citation: Talos CCleanup 2017)(Citation: FireEye POSHSPY April 2017)(Citation: ESET Sednit 2017 Activity)

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
* Wiki: https://attack.mitre.org/techniques/T1568/002

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

```

# Tactics


* [Command and Control](../tactics/Command-and-Control.md)


# Mitigations


* [Restrict Web-Based Content](../mitigations/Restrict-Web-Based-Content.md)

* [Network Intrusion Prevention](../mitigations/Network-Intrusion-Prevention.md)
    
* [Domain Generation Algorithms Mitigation](../mitigations/Domain-Generation-Algorithms-Mitigation.md)
    

# Actors


* [APT41](../actors/APT41.md)

