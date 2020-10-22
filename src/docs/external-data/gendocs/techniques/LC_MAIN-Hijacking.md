
# LC_MAIN Hijacking

## Description

### MITRE Description

> **This technique has been deprecated and should no longer be used.**

As of OS X 10.8, mach-O binaries introduced a new header called LC_MAIN that points to the binary’s entry point for execution. Previously, there were two headers to achieve this same effect: LC_THREAD and LC_UNIXTHREAD  (Citation: Prolific OSX Malware History). The entry point for a binary can be hijacked so that initial execution flows to a malicious addition (either another section or a code cave) and then goes back to the initial entry point so that the victim doesn’t know anything was different  (Citation: Methods of Mac Malware Persistence). By modifying a binary in this way, application whitelisting can be bypassed because the file name or application path is still the same.

## Aliases

```

```

## Additional Attributes

* Bypass: ['Application whitelisting', 'Process whitelisting', 'Whitelisting by file name or path']
* Effective Permissions: None
* Network: None
* Permissions: ['User', 'Administrator']
* Platforms: ['macOS']
* Remote: None
* Type: attack-pattern
* Wiki: https://attack.mitre.org/techniques/T1149

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


# Mitigations


* [LC_MAIN Hijacking Mitigation](../mitigations/LC_MAIN-Hijacking-Mitigation.md)

* [Code Signing](../mitigations/Code-Signing.md)
    

# Actors

None
