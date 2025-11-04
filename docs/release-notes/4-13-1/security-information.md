# Security Information

Resolved CVEs, as detailed below:

| CVE | Problem details from upstream |
|------|-------------------------------|
| [CVE-2024-45338](https://nvd.nist.gov/vuln/detail/CVE-2024-45338) | An attacker can craft an input to the Parse functions that would be processed non-linearly with respect to its length, resulting in extremely slow parsing and potential denial of service. |
| [CVE-2025-22868](https://nvd.nist.gov/vuln/detail/CVE-2025-22868) | An attacker can pass a malicious malformed token which causes unexpected memory to be consumed during parsing. |
| [CVE-2025-22870](https://nvd.nist.gov/vuln/detail/CVE-2025-22870) | Matching of hosts against proxy patterns can improperly treat an IPv6 zone ID as a hostname component. For example, when the NO_PROXY environment variable is set to `*.example.com`, a request to `[::1%25.example.com]:80` will incorrectly match and not be proxied. |
| [CVE-2025-22871](https://nvd.nist.gov/vuln/detail/CVE-2025-22871) | The `net/http` package improperly accepts a bare LF as a line terminator in chunked data chunk-size lines. This can permit request smuggling if used with a server that incorrectly accepts bare LFs in chunk extensions. |
| [CVE-2025-22872](https://nvd.nist.gov/vuln/detail/CVE-2025-22872) | The tokenizer incorrectly interprets tags with unquoted attribute values that end with a solidus character (/) as self-closing. This can cause incorrect DOM structure in foreign content such as `<math>` or `<svg>`. |
| [CVE-2025-32386](https://nvd.nist.gov/vuln/detail/CVE-2025-32386) | Helm chart archives can be crafted to expand disproportionately when decompressed, exhausting system memory. Fixed in Helm v3.17.3. |
| [CVE-2025-32387](https://nvd.nist.gov/vuln/detail/CVE-2025-32387) | Deeply nested JSON Schema references in Helm charts can cause stack overflow during parsing. Fixed in Helm v3.17.3. |
| [CVE-2025-46569](https://nvd.nist.gov/vuln/detail/CVE-2025-46569) | Open Policy Agent (OPA) prior to v1.4.0 could allow Rego code injection through crafted HTTP Data API paths, potentially leading to oracle attacks, policy misdirection, or DoS. Fixed in v1.4.0. |
| [CVE-2025-47291](https://nvd.nist.gov/vuln/detail/CVE-2025-47291) | In containerd 2.0.1–2.0.4, usernamespaced containers may not be placed under Kubernetes’ cgroup hierarchy, bypassing limits and enabling DoS. Fixed in containerd 2.0.5+ and 2.1.0+. |
| [CVE-2025-24358](https://nvd.nist.gov/vuln/detail/CVE-2025-24358) | `gorilla/csrf` prior to 1.7.2 did not properly validate the Origin header, allowing CSRF attacks when TLS detection failed. Fixed in v1.7.2. |
| [CVE-2025-47273](https://nvd.nist.gov/vuln/detail/CVE-2025-47273) | `setuptools` prior to 78.1.1 contained a path traversal vulnerability in `PackageIndex` that could allow arbitrary file writes or remote code execution. Fixed in 78.1.1. |
