# Certificate Transparency for Enterprises

## Locally-trusted CAs

Certificate Transparency only applies to CAs that are publicly-trusted - that
is, CAs that are supported by your browser or device out of the box, without
any additional configuration steps.

For CAs that have been manually installed, provided those certificates are not
or have not been publicly-trusted, it's not necessary to enable support for
Certificate Transparency. Further, Certificate Transparency Logs will not
accept certificates from those CAs, thus it's not possible to support CT.

In some cases, an Enterprise may have a locally-trusted CA that has been
manually installed, but it was previously publicly-trusted. For example, this
CA may have been removed by a browser or an OS for not complying with the
root store policies, but the Enterprise may still have a dependency on
trusting this CA. In these cases, the Enterprise can use
[Enterprise Policies](#Enterprise-Policies) to configure how Certificate
Transparency will be enforced for those CAs.

## Private Domain Names

For Enterprises that have domain names that are internal to their organization,
and do not need to be publicly-trusted by default, several options exist to
enable these domains to be kept private, while allowing the certificates to
still be used, without error, for users in their organization.

The recommended option is to no longer rely on publicly-trusted certificates
to serve these domains, as they are organization specific. For example, such
organizations can use a private CA, which [several](https://aws.amazon.com/certificate-manager/private-certificate-authority/)
[CAs](https://www.digicert.com/private-pki/) [offer](https://www.comodo.com/business-security/pki-management/certificate-manager.php).
Using a hosted, managed PKI may help organizations more rapidly respond to
change in the TLS ecosystem, such as changes to certificate algorithms or
support for new protocols.

Another option is to request that the publicly-trusted CA not log the
certificate. This will prevent this certificate from being trusted by default,
but organizations that manage their devices or users can override this through
[Enterprise Policies](#Enterprise-Policies) to enable these certificates to be
trusted for users in their Enterprise.

Finally, organizations may manage their own PKI in-house, using CA
software such as [CFSSL](https://github.com/cloudflare/cfssl), [Boulder](https://github.com/letsencrypt/boulder),
[EJBCA](https://www.ejbca.org/) or
[Active Directory Certificate Services](https://msdn.microsoft.com/en-us/library/ff630887.aspx).
Managing certificates in-house may be more complex and security risky, but
offers an alternative solution to partnering with a certificate provider.

## Legacy CAs

Some Enterprises rely on Certificate Authorities that have not been audited to
the same standard as other CAs or been operated to the same security
requirements. These CAs would not be trusted in new products, nor other root
programs, but may be trusted on one or more platforms that Chrome runs on.
Because they are trusted by default, they are subject to the Chrome's policies
on requiring CT, but due to their legacy status, may not be prepared. While the
requirement to disclose new certificates via Certificate Transparency has been
communicated, some may not do so, causing their new certificates to not be
trusted. This is most common with CAs run by governments, as they rarely meet the
required security standards of a widely-trusted CA.

Organizations that need to use certificates from these CAs should be aware
that their certificates will not be trusted if they do not support CT, and so
should look for CAs that do support CT. Alternatively, supporting CT via TLS
may be the only way to ensure these certificates continue to work, but that
requires the Enterprise constantly keep track of changes regarding Certificate
Transparency.

Organizations that need to trust certificates from these CAs, such as when
talking to other organizations that need to use these CAs, can configure
[Enterprise Policies](#Enterprise-Policy) for users in their organization,
which will allow trust in these certificates. As these only apply to Enterprise
users, these policies are not suitable for making these certificates trusted
more widely.

## Enterprise Policies

Several Chrome-specific policies exist that allow Enterprises to configure
their machines or users to disable Certificate Transparency for certain cases.
These policies are documented in the
[master policy list](https://cloud.google.com/docs/chrome-enterprise/policies),
but detailed further below.

### CertificateTransparencyEnforcementDisabledForUrls

This [policy](https://cloud.google.com/docs/chrome-enterprise/policies/?policy=CertificateTransparencyEnforcementDisabledForUrls)
has been available since Chrome 53, and allows for disabling Certificate
Transparency enforcement for a certain set of domains or subdomains, without
disabling Certificate Transparency altogether.

If you wish to disable CT for a given hostname, and all of its subdomains, then
the domain is simply entered into the list. For example, `example.com` will
disable CT for `example.com` and all subdomains.

If you wish to disable CT only for a given hostname, but wish to ensure that
subdomains will still have CT enabled, then prefix the domain with a leading
dot. For example, `.example.com` will disable CT for `example.com` exactly,
while leaving it enabled for subdomains.

### CertificateTransparencyEnforcementDisabledForCas

This [policy](https://cloud.google.com/docs/chrome-enterprise/policies/?policy=CertificateTransparencyEnforcementDisabledForCas),
available since Chrome 57, allows for disabling Certificate Transparency
enforcement if certain conditions are met in the trusted certificate chain.
This allows disabling CT without having to list all of the domain names, but
only for certificates issued to a specific organization.

Certificates are specified in this policy by applying Base64 to a hash of their
subjectPublicKeyInformation, as well as specifying the hash algorithm used.
This format is very similar to that used by
[HTTP Public Key Pinning](https://tools.ietf.org/html/rfc7469) (HPKP), so that
sites can use the same [examples](https://tools.ietf.org/html/rfc7469#appendix-A)
or [tools](https://report-uri.com/home/pubkey_hash) used to generate HPKP
hashes to determine how to configure the policy. Note that while both use
Base64, an HPKP hash will be in the form `pin-sha256="hash"`, while the policy
will be in the form `sha256/hash`.

To disable Certificate Transparency for these certificates, the certificate
must match one of the following conditions:

1. The hash specified is of the server certificate's subjectPublicKeyInfo.
2. The hash specified is of an intermediate CA, and that intermediate CA has
   a nameConstraints extension with one or more directoryNames in the
   permittedSubtrees of that extension.
3. The hash specified is of an intermediate CA, that intermediate CA contains
   one or more organizationName (O) attribute in the subject, and the server
   certificate's has the same number of organizationName attributes, with
   byte-for-byte identical values, in the same exact order.

### CertificateTransparencyEnforcementDisabledForLegacyCas

This [policy](https://cloud.google.com/docs/chrome-enterprise/policies/?policy=CertificateTransparencyEnforcementDisabledForLegacyCas),
available since Chrome 67, allows for disabling Certificate Transparency
enforcement for certain legacy CAs that have not adopted modern security and
audit requirements required of publicly-trusted CAs. This is particularly
tailored towards CAs that are trusted on some platforms that Chrome runs on,
but are not trusted on ChromeOS or Android, due to not meeting the necessary
security requirements.

CAs are specified in this policy by applying Base64 to a hash of their
subjectPublicKeyInformation, the same as in
[CertificateTransparencyEnforcementDisabledForCAs](#CertificateTransparencyEnforcementDisabledForCas).
However, these CAs must also be recognized as Legacy CAs in the
[`/net/data/ssl/root_stores/root_stores.json`](/net/data/ssl/root_stores/root_stores.json)
file, which means that they are not trusted on ChromeOS or Android, but are
trusted on another platform that Chrome runs on.

This policy is the riskiest of the three Enterprise policies, in that such
legacy CAs can represent the greatest security threat to an organization, as
they lack either the audits or compliance with industry best practice and root
store requirements. Enterprises should only enable this policy if no other
option meets their needs.
