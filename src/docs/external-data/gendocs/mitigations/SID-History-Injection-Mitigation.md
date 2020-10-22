
# SID-History Injection Mitigation

## Description

### MITRE Description

> Clean up SID-History attributes after legitimate account migration is complete.

Consider applying SID Filtering to interforest trusts, such as forest trusts and external trusts, to exclude SID-History from requests to access domain resources. SID Filtering ensures that any authentication requests over a trust only contain SIDs of security principals from the trusted domain (i.e. preventing the trusted domain from claiming a user has membership in groups outside of the domain).

SID Filtering of forest trusts is enabled by default, but may have been disabled in some cases to allow a child domain to transitively access forest trusts. SID Filtering of external trusts is automatically enabled on all created external trusts using Server 2003 or later domain controllers. (Citation: Microsoft Trust Considerations Nov 2014) (Citation: Microsoft SID Filtering Quarantining Jan 2009) However note that SID Filtering is not automatically applied to legacy trusts or may have been deliberately disabled to allow inter-domain access to resources.

SID Filtering can be applied by: (Citation: Microsoft Netdom Trust Sept 2012)

* Disabling SIDHistory on forest trusts using the netdom tool (<code>netdom trust <TrustingDomainName> /domain:<TrustedDomainName> /EnableSIDHistory:no</code> on the domain controller). 
* Applying SID Filter Quarantining to external trusts using the netdom tool (<code>netdom trust <TrustingDomainName> /domain:<TrustedDomainName> /quarantine:yes</code> on the domain controller)
Applying SID Filtering to domain trusts within a single forest is not recommended as it is an unsupported configuration and can cause breaking changes. (Citation: Microsoft Netdom Trust Sept 2012) (Citation: AdSecurity Kerberos GT Aug 2015) If a domain within a forest is untrustworthy then it should not be a member of the forest. In this situation it is necessary to first split the trusted and untrusted domains into separate forests where SID Filtering can be applied to an interforest trust.


# Techniques


* [SID-History Injection](../techniques/SID-History-Injection.md)

