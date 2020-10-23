
# Spearphishing via Service

## Description

### MITRE Description

> Adversaries may send spearphishing messages via third-party services in an attempt to elicit sensitive information and/or gain access to victim systems. Spearphishing via service is a specific variant of spearphishing. It is different from other forms of spearphishing in that it employs the use of third party services rather than directly via enterprise email channels. 

All forms of spearphishing are electronically delivered social engineering targeted at a specific individual, company, or industry. In this scenario, adversaries send messages through various social media services, personal webmail, and other non-enterprise controlled services. These services are more likely to have a less-strict security policy than an enterprise. As with most kinds of spearphishing, the goal is to generate rapport with the target or get the target's interest in some way. Adversaries will create fake social media accounts and message employees for potential job opportunities. Doing so allows a plausible reason for asking about services, policies, and software that's running in an environment. The adversary can then send malicious links or attachments through these services.

A common example is to build rapport with a target via social media, then send content to a personal webmail service that the target uses on their work computer. This allows an adversary to bypass some email restrictions on the work account, and the target is more likely to open the file since it's something they were expecting. If the payload doesn't work as expected, the adversary can continue normal communications and troubleshoot with the target on how to get it working.

## Aliases

```

```

## Additional Attributes

* Bypass: None
* Effective Permissions: None
* Network: None
* Permissions: None
* Platforms: ['Linux', 'macOS', 'Windows']
* Remote: None
* Type: attack-pattern
* Wiki: https://attack.mitre.org/techniques/T1566/003

## Potential Commands

```

```

## Commands Dataset

```

```

## Potential Detections

```json
[{'data_source': ['SSL/TLS inspection']},
 {'data_source': ['Anti-virus']},
 {'data_source': ['Web proxy']},
 {'data_source': ['SSL/TLS inspection']},
 {'data_source': ['Anti-virus']},
 {'data_source': ['Web proxy']}]
```

## Potential Queries

```json

```

## Raw Dataset

```json

```

# Tactics


* [Initial Access](../tactics/Initial-Access.md)


# Mitigations


* [User Training](../mitigations/User-Training.md)

* [Restrict Web-Based Content](../mitigations/Restrict-Web-Based-Content.md)
    
* [Antivirus/Antimalware](../mitigations/Antivirus-Antimalware.md)
    

# Actors


* [Dark Caracal](../actors/Dark-Caracal.md)

* [OilRig](../actors/OilRig.md)
    
* [FIN6](../actors/FIN6.md)
    
* [Windshift](../actors/Windshift.md)
    
* [Magic Hound](../actors/Magic-Hound.md)
    
