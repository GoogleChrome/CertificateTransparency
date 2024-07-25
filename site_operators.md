# Certificate Transparency for Site Operators

## Basics

We say that a certificate supports Certificate Transparency if it comes with
CT information that demonstrates it has been logged in several CT logs. This
CT information must comply with the
[Certificate Transparency in Chrome](https://github.com/chromium/ct-policy/blob/master/ct_policy.md)
policy. We sometimes refer to a site that "supports" CT as using a certificate
that is "CT qualified" or "disclosed via CT."

In general, a site operator does not need to take special action to
support Certificate Transparency. This is because RFC 6962 defines three ways
of providing the necessary information for CT: within the certificate, within
a stapled OCSP response, or directly by the TLS server. Nearly every CA
supports CT through the first method, meaning that when you get a certificate,
it will already support CT and require no further configuration. If you are
using a cloud provider to terminate your TLS connections, the cloud provider
may also support CT via TLS, requiring no further action on your part.

Supporting CT within the certificate itself is the preferred and recommended
way to enable CT support. If you obtain a certificate from your CA and it does
not support CT, then that generally indicates that your CA is not following
industry best practice, and you should probably look for another CA to provide
certificates for your sites.

Configuring support for CT via the TLS extension is not recommended for most
site operators. This is because supporting CT via this method requires
constant monitoring of the CT ecosystem, such as for changes in the list of
trusted logs or testing compatibility with various CT-supporting clients. This
method works well for organizations with the ability to dedicate resources to
that, such as hosting and cloud providers. If you are hosting your own website,
you should try to ensure that your certificates support CT, and avoid supporting
CT via the TLS extension. Supporting CT via the TLS extension may require rapid
changes to your configuration, and thus may be riskier for organizations
without staff dedicated to this.

If you are getting longer-lived certificates (for example, 1 year), it's
possible that changes in the CT ecosystem may mean that the CT information may
expire before the certificate expires. If your CA also supports delivering CT
via OCSP responses, then supporting OCSP stapling on your server may allow
fresh CT information to be provided without having to replace the certificate.
Alternatively, if your server does not support OCSP stapling, or your CA does
not support CT in their OCSP responses, you may need to replace your certificate.

These policies only apply to publicly-trusted CAs - that is, CAs that your
browser or device trust without any additional configuration. For organizations
using their own CAs, or for locally installed CAs, see
[Certificate Transparency for Enterprises](#Certificate-Transparency-For-Enterprises).

## Domain Privacy

Supporting CT by disclosing the certificate to a CT Log means that the full
contents of the certificate will be publicly accessible and viewable. In
particular, this means that the domains a certificate are for will be included
in the Certificate Transparency log, as well as the organization they are
affiliated with, if they are validated to a level higher than Domain
Validation or issued from an organization-specific CA.

For most certificates, this is no different than what is already available.
Publicly-trusted certificates have been subject to aggregation for public
analysis for some time, such as through products and tools such as
[Censys](https://censys.io/) or [scans.io](https://scans.io/). While
Certificate Transparency provides an interoperable protocol for exchanging
these datasets, in many cases, the certificate details and domains were already
publicly detectable.

Requiring that the full certificate be disclosed if it was issued by a
publicly-trusted CA is an important part of the security goals of Certificate
Transparency. Permitting some of the information to be hidden from
certificates allows for both attackers and untrustworthy CAs to hide
certificates that could be used to compromise users. Certificate Transparency
has detected issues at a large
[number of CAs](https://wiki.mozilla.org/CA/Incident_Dashboard), many that the
CAs themselves were not even aware of, and so public disclosure is critical
to keeping all users safe.

While proposals for hiding domain names were presented during the development
of Certificate Transparency, none of them were able to balance the needs of
site operators that did not need to hide their domains, those that did, and the
security risks that users would face.

Because of this, Chrome does not support any method for hiding domain names or
other information within publicly-trusted certificates, nor are there any plans
to support such mechanisms. Domain operators that wish to hide their
certificates, enabling security risks and attacks, have two options:

1. **Wildcard Certificates** - Wildcard certificates allow a single certificate
   to be used for multiple hostnames, by putting a `*` as the most specific
   DNS label (for example, `*.internal.example.com` is valid for
   `mail.internal.example.com` and `wiki.internal.example.com`, but not for
   `www.example.com` or `two.levels.internal.example.com`). Wildcard
   certificates require greater care by the site operator to protect their
   private key, but also can have their issuance controlled via technologies
   such as [CAA (RFC 6844)](https://tools.ietf.org/html/rfc6844). This still
   requires the certificate be disclosed, but can limit how much of the domain
   is disclosed.
2. **Enterprise-specific configuration** - If the domains being accessed are
   not intended to be used on the public internet, or not on machines or by
   users that are not part of a single enterprise, then that enterprise can
   use the options in the
   [Certificate Transparency for Enterprises](#Certificate-Transparency-For-Enterprises).
   This allows the enterprise to not reveal any information about the
   certificate, but these certificates will **only** be trusted by their
   members.

## What to do if your certificate does not work

As noted in [Chrome Policies](#Chrome-Policies), all certificates issued after
30 April 2018 are expected to be disclosed via Certificate Transparency in a
way that is compliant with the Certificate Transparency in Chrome policy.
Virtually all publicly-trusted CAs now support CT for their customers by
default, meaning that site operators should not have to do anything special and
can continue getting certificates that just work.  1 May 2018.

However, there's still a chance that a CA may have an infrastructure issue, or
other problem that could cause validation issues. If you're receiving a
`net::ERR_CERTIFICATE_TRANSPARENCY_REQUIRED` error message, the best thing to do
is to contact your CA's support or sales team to diagnose the error with them.
They will most likely need to replace your certificate with a new one that
properly supports CT.
