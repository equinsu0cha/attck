
# Application Access Token

## Description

### MITRE Description

> Adversaries may use stolen application access tokens to bypass the typical authentication process and access restricted accounts, information, or services on remote systems. These tokens are typically stolen from users and used in lieu of login credentials.

Application access tokens are used to make authorized API requests on behalf of a user and are commonly used as a way to access resources in cloud-based applications and software-as-a-service (SaaS).(Citation: Auth0 - Why You Should Always Use Access Tokens to Secure APIs Sept 2019) OAuth is one commonly implemented framework that issues tokens to users for access to systems. These frameworks are used collaboratively to verify the user and determine what actions the user is allowed to perform. Once identity is established, the token allows actions to be authorized, without passing the actual credentials of the user. Therefore, compromise of the token can grant the adversary access to resources of other sites through a malicious application.(Citation: okta)

For example, with a cloud-based email service once an OAuth access token is granted to a malicious application, it can potentially gain long-term access to features of the user account if a "refresh" token enabling background access is awarded.(Citation: Microsoft Identity Platform Access 2019) With an OAuth access token an adversary can use the user-granted REST API to perform functions such as email searching and contact enumeration.(Citation: Staaldraad Phishing with OAuth 2017)

Compromised access tokens may be used as an initial step in compromising other services. For example, if a token grants access to a victim’s primary email, the adversary may be able to extend access to all other services which the target subscribes by triggering forgotten password routines. Direct API access through a token negates the effectiveness of a second authentication factor and may be immune to intuitive countermeasures like changing passwords. Access abuse over an API channel can be difficult to detect even from the service provider end, as the access can still align well with a legitimate workflow.

## Aliases

```

```

## Additional Attributes

* Bypass: ['System Access Controls']
* Effective Permissions: None
* Network: None
* Permissions: None
* Platforms: ['Office 365', 'SaaS']
* Remote: None
* Type: attack-pattern
* Wiki: https://attack.mitre.org/techniques/T1550/001

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


* [Defense Evasion](../tactics/Defense-Evasion.md)

* [Lateral Movement](../tactics/Lateral-Movement.md)
    

# Mitigations


* [Restrict Web-Based Content](../mitigations/Restrict-Web-Based-Content.md)

* [Encrypt Sensitive Information](../mitigations/Encrypt-Sensitive-Information.md)
    
* [Audit](../mitigations/Audit.md)
    

# Actors


* [APT28](../actors/APT28.md)

