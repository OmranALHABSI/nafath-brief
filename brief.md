Version: NAFATH-V1
Track: Networking
## Overview
The national login service brings six IT fields together to provide secure access through a website and an Android app. Software defines how OpenID Connect verifies identity and how OAuth 2.0 grants limited access to resources. AI helps identify suspicious login activity, but its errors, fairness, privacy, and security must be assessed before deployment. Mobile development controls access to sensitive device features through Android permissions. Networking protects DNS exchanges and supports reliable communication with the login service. Cybersecurity strengthens authentication against phishing, reducing the risk of account takeover. Data governance determines which Omani legal requirements and government policies apply to collecting and storing citizens' information. Together, these fields support secure national login, with DNS over HTTPS (DoH) protecting DNS communication between clients and resolvers.
## Software
OAuth 2.0 provides authorization: an application receives an access token to use permitted resources on a user's behalf without obtaining their password. OpenID Connect adds authentication to OAuth 2.0 and provides an ID token describing the authenticated user. For this service, OpenID Connect supports citizen login, while OAuth 2.0 supports delegated access to government APIs. Identity verification and resource permissions serve different purposes.

Resource: How OpenID Connect Works - https://openid.net/developers/how-connect-works/
## AI
Using NIST AI RMF, the authority should Govern responsibilities and human oversight; Map risks such as privacy loss, unfair treatment, false alarms, and missed attacks; Measure accuracy, fairness, security, and reliability using representative login data; and Manage risks through suitable thresholds, review procedures, and a controlled pilot. Before launch, it should test these controls and prepare ongoing monitoring, incident response, and rollback procedures.

Resource: AI RMF Core - https://airc.nist.gov/airmf-resources/airmf/5-sec-core/
## Mobile
Android limits access to protected data and device features through application isolation and permissions. Sensitive access, such as camera, microphone, contacts, or location, can require runtime permission. The login app must declare required permissions and obtain approval before using protected features. It should ask when the user starts the relevant action, check current permission status, request only necessary access, and handle denial gracefully.

Resource: Permissions on Android - https://developer.android.com/guide/topics/permissions/overview
## Networking
DNS over HTTPS (DoH) sends DNS queries and responses through HTTPS, protecting communication between the client and resolver against eavesdropping and modification. For the login service, this helps protect domain lookups on untrusted networks. However, the resolver can still see queries, and DoH does not replace DNSSEC validation. The authority should choose a trusted resolver and consider compatibility with internal DNS and security monitoring.

Resource: RFC 8484: DNS Queries over HTTPS (DoH) - https://www.rfc-editor.org/rfc/rfc8484.html
## Cybersecurity
Phishing-resistant MFA uses cryptographic authentication bound to the genuine service, preventing a fake website from capturing a reusable login response. A suitable option is a FIDO2/WebAuthn passkey or security key that requires local user verification through a PIN or biometric. This combines possession with another factor. The authority should verify that user verification is enforced and provide secure enrollment and account recovery procedures.

Resource: NIST SP 800-63B-4: Authentication and Authenticator Management - https://pages.nist.gov/800-63-4/sp800-63b.html
## Data
Oman's Personal Data Protection Law and Executive Regulations establish requirements for entities within their scope, including consent, processing records, privacy policies, and breach notification. MTCIT explains that state administrative units and other public legal entities are exempt from the Law; a separate government policy under Circular 6/2024 applies to state administrative units. The authority should establish its legal status and applicable rules before collecting or storing citizens' information.

Resource: MTCIT: Personal Data Protection - https://www.mtcit.gov.om/sectors/governance/personal
## Misconception in My Track
A common misconception is that DNS over HTTPS guarantees that every DNS answer is authentic and therefore replaces DNSSEC. In fact, DoH protects the connection between the client and resolver, while DNSSEC validates the authenticity and integrity of DNS data. A resolver can still return incorrect information over an encrypted connection. Section 9, Security Considerations, of RFC 8484 explains that DoH and DNSSEC are independent, compatible protocols solving different problems. The login service therefore needs both secure DNS transport and an appropriate DNSSEC validation strategy.

## Open Question
How can the authority deploy DNS over HTTPS while preserving internal government domain resolution, DNSSEC validation, and the security team's ability to detect suspicious DNS activity?
