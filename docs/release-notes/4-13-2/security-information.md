# Security Information

Resolved CVEs, as detailed below:

| CVE | Problem details from upstream |
|------|-------------------------------|
| [CVE-2024-3596](https://nvd.nist.gov/vuln/detail/CVE-2024-3596) | RADIUS Protocol under RFC 2865 is susceptible to forgery attacks by a local attacker who can modify any valid Response (Access-Accept, Access-Reject, or Access-Challenge) using a chosen-prefix collision attack against the MD5 Response Authenticator signature. |
| [CVE-2025-32988](https://nvd.nist.gov/vuln/detail/CVE-2025-32988) | A double-free vulnerability exists in GnuTLS due to incorrect ownership handling in the export logic of SAN entries containing an otherName. Triggering this issue via public GnuTLS APIs can lead to denial of service or memory corruption. |
| [CVE-2025-32989](https://nvd.nist.gov/vuln/detail/CVE-2025-32989) | A heap-buffer-overread in GnuTLS affects how Certificate Transparency SCT extensions are handled, potentially exposing confidential data when verifying certain malformed certificates. |
| [CVE-2025-32990](https://nvd.nist.gov/vuln/detail/CVE-2025-32990) | A heap-buffer-overflow (off-by-one) in GnuTLS’s `certtool` template parsing logic can result in memory corruption or denial of service. |
| [CVE-2025-49794](https://nvd.nist.gov/vuln/detail/CVE-2025-49794) | A use-after-free vulnerability in libxml2 occurs when parsing XPath elements in XML Schematron documents, potentially causing crashes or undefined behavior. |
| [CVE-2025-49795](https://nvd.nist.gov/vuln/detail/CVE-2025-49795) | A NULL pointer dereference vulnerability in libxml2’s XPath processing allows crafted XML inputs to cause denial of service. |
| [CVE-2025-49796](https://nvd.nist.gov/vuln/detail/CVE-2025-49796) | Certain `sch:name` elements in XML can trigger memory corruption in libxml2, leading to potential crashes or undefined behavior. |
| [CVE-2025-5222](https://nvd.nist.gov/vuln/detail/CVE-2025-5222) | A stack buffer overflow in ICU’s `genrb` binary (in the `SRBRoot::addTag` function) can cause memory corruption and local code execution. |
| [CVE-2025-53547](https://nvd.nist.gov/vuln/detail/CVE-2025-53547) | Helm prior to v3.18.4 could execute arbitrary code if a symlinked `Chart.lock` file points to an executable script. Fixed in v3.18.4. |
| [CVE-2025-6021](https://nvd.nist.gov/vuln/detail/CVE-2025-6021) | A stack-based buffer overflow in libxml2’s `xmlBuildQName` function due to integer overflow may cause denial of service or memory corruption. |
| [CVE-2025-6395](https://nvd.nist.gov/vuln/detail/CVE-2025-6395) | A NULL pointer dereference flaw in GnuTLS’s `_gnutls_figure_common_ciphersuite()` may lead to crashes. |
| [CVE-2025-0913](https://nvd.nist.gov/vuln/detail/CVE-2025-0913) | On Windows, `os.OpenFile(path, os.O_CREATE|O_EXCL)` could create files through dangling symlinks. The function now returns an error when targeting a symlink. |
| [CVE-2025-22874](https://nvd.nist.gov/vuln/detail/CVE-2025-22874) | Calling `Verify` with `VerifyOptions.KeyUsages` containing `ExtKeyUsageAny` unintentionally disabled policy validation for certain certificate chains. |
| [CVE-2025-4673](https://nvd.nist.gov/vuln/detail/CVE-2025-4673) | `Proxy-Authorization` and `Proxy-Authenticate` headers could persist across cross-origin redirects, leaking sensitive information. |
| [CVE-2025-47907](https://nvd.nist.gov/vuln/detail/CVE-2025-47907) | Cancelling a query during a call to `Scan()` could cause race conditions and incorrect results when multiple queries run concurrently. |
| [CVE-2025-55198](https://nvd.nist.gov/vuln/detail/CVE-2025-55198) | Improper validation in Helm prior to v3.18.5 could cause a panic when parsing malformed YAML files. Fixed in v3.18.5. |
| [CVE-2025-55199](https://nvd.nist.gov/vuln/detail/CVE-2025-55199) | Helm prior to v3.18.5 could be forced into an out-of-memory condition by crafted JSON Schema references (e.g., `$ref` to `/dev/zero`). Fixed in v3.18.5. |
