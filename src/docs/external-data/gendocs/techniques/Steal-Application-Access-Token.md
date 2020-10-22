
# Steal Application Access Token

## Description

### MITRE Description

> Adversaries can steal user application access tokens as a means of acquiring credentials to access remote systems and resources. This can occur through social engineering and typically requires user action to grant access.

Application access tokens are used to make authorized API requests on behalf of a user and are commonly used as a way to access resources in cloud-based applications and software-as-a-service (SaaS).(Citation: Auth0 - Why You Should Always Use Access Tokens to Secure APIs Sept 2019) OAuth is one commonly implemented framework that issues tokens to users for access to systems. An application desiring access to cloud-based services or protected APIs can gain entry using OAuth 2.0 through a variety of authorization protocols. An example commonly-used sequence is Microsoft's Authorization Code Grant flow.(Citation: Microsoft Identity Platform Protocols May 2019)(Citation: Microsoft - OAuth Code Authorization flow - June 2019) An OAuth access token enables a third-party application to interact with resources containing user data in the ways requested by the application without obtaining user credentials. 
 
Adversaries can leverage OAuth authorization by constructing a malicious application designed to be granted access to resources with the target user's OAuth token. The adversary will need to complete registration of their application with the authorization server, for example Microsoft Identity Platform using Azure Portal, the Visual Studio IDE, the command-line interface, PowerShell, or REST API calls.(Citation: Microsoft - Azure AD App Registration - May 2019) Then, they can send a link through [Spearphishing Link](https://attack.mitre.org/techniques/T1192) to the target user to entice them to grant access to the application. Once the OAuth access token is granted, the application can gain potentially long-term access to features of the user account through [Application Access Token](https://attack.mitre.org/techniques/T1527).(Citation: Microsoft - Azure AD Identity Tokens - Aug 2019)

Adversaries have been seen targeting Gmail, Microsoft Outlook, and Yahoo Mail users.(Citation: Amnesty OAuth Phishing Attacks, August 2019)(Citation: Trend Micro Pawn Storm OAuth 2017)

## Aliases

```

```

## Additional Attributes

* Bypass: None
* Effective Permissions: None
* Network: None
* Permissions: ['User']
* Platforms: ['SaaS', 'Office 365', 'Azure AD']
* Remote: None
* Type: attack-pattern
* Wiki: https://attack.mitre.org/techniques/T1528

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


* [Credential Access](../tactics/Credential-Access.md)


# Mitigations


* [User Training](../mitigations/User-Training.md)

* [Audit](../mitigations/Audit.md)
    
* [User Account Management](../mitigations/User-Account-Management.md)
    
* [Restrict Web-Based Content](../mitigations/Restrict-Web-Based-Content.md)
    

# Actors


* [APT28](../actors/APT28.md)

