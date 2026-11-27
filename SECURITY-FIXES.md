# Fixes beyond Axis 1.4

## General fixes

- **AXIS-2875 — Java 6 compatibility:** Updated the SAAJ dependency and test configuration, and renamed a method that conflicts with a Java 6 superclass method.
- **AXIS-2909 — concurrency:** `JavaServiceDesc` copies operation overloads to an array before sorting, avoiding concurrent modification issues when requests access the shared overload collection.

## Security fixes

- **CVE-2012-5784 (AXIS-2883) / CVE-2014-3596 (AXIS-2905) — HTTPS hostname verification:** `JSSESocketFactory` checks the requested host against certificate DNS subject alternative names and common names, mitigating hostname-mismatch man-in-the-middle attacks.
- **CVE-2018-8032 (AXIS-2924) — XSS in SOAP response serialization:** `SerializationContext` XML-escapes namespace URIs when writing namespace declarations. A regression test covers a crafted namespace URI.
- **CVE-2023-40743 — unsafe service URL protocols:** `ServiceFactory` filters unsupported protocols, mitigating dangerous lookups such as LDAP when service URLs come from untrusted input. No corresponding AXIS Jira ID was identified.
- **CVE-2026-90436 — SOAP fault arbitrary class instantiation:** fault deserialization loads exception classes without initialization and accepts/constructs only `AxisFault` subtypes. Regression tests cover rejecting arbitrary classes while retaining legitimate Axis faults. No corresponding AXIS Jira ID was identified.

## Known issues not fixed

- **CVE-2019-0227 — server-side request forgery:** Advisory reports SSRF in Axis 1.4, but no complete upstream fix was identified. The `ServiceFactory` protocol filtering above is a targeted mitigation and should not be considered a resolution of this advisory. Avoid passing untrusted input to `ServiceFactory.getService`.

These changes are not included in the original Apache Axis 1.4 release. Apache Axis 1.x is end-of-life; migration remains the recommended long-term remediation.
