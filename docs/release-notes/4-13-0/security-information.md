# Security Information

Updated the following middleware component versions to resolve
vulnerabilities in MSR:

- [MSRH-190] Golang v1.23.7  
- [MSRH-206] beego Go Web Framework v2.3.6  
- [MSRH-191] Go packages:  
    - Aqua Trivy Vulnerability Scanner v0.60.0  
    - Go Cryptography Libraries golang.org/x/crypto v0.35.0  
    - go-jose JSON Object Signing and Encryption for Go v4.0.5  
    - OAuth 2.0 for Go golang.org/x/oauth2 v0.27.0  

!!! note
    The CVE-2025-22868 may still appear in the `trivy-adapter-photon`
    image. However, the image is not affected by the vulnerability.

## Resolved CVEs

| CVE | Problem details from upstream |
|------|-------------------------------|
| [CVE-2025-22872](https://nvd.nist.gov/vuln/detail/CVE-2025-22872) | The tokenizer incorrectly interprets tags with unquoted attribute values that end with a solidus character (/) as self-closing. When directly using Tokenizer, this can result in such tags incorrectly being marked as self-closing, and when using the Parse functions, this can result in content following such tags as being placed in the wrong scope during DOM construction, but only when tags are in foreign content (e.g., `<math>`, `<svg>`, etc.). |
| [CVE-2019-25210](https://nvd.nist.gov/vuln/detail/CVE-2019-25210) | A vulnerability in Helm through 3.13.3 where the `--dry-run` flag displays secret values. The behavior is intentional for backward compatibility but may expose sensitive data in CI/CD environments. |
| [CVE-2025-32387](https://nvd.nist.gov/vuln/detail/CVE-2025-32387) | A JSON Schema file in a Helm chart can create recursive references, causing a stack overflow. Fixed in Helm v3.17.3. |
| [CVE-2025-32386](https://nvd.nist.gov/vuln/detail/CVE-2025-32386) | Specially crafted chart archives can expand disproportionately, exhausting memory. Fixed in Helm v3.17.3. |
| [CVE-2025-30223](https://nvd.nist.gov/vuln/detail/CVE-2025-30223) | Beego prior to 2.3.6 is vulnerable to XSS via the `RenderForm()` function, allowing injection of malicious JavaScript. Fixed in 2.3.6. |
| [CVE-2025-30204](https://nvd.nist.gov/vuln/detail/CVE-2025-30204) | `golang-jwt` versions before 5.2.2 and 4.5.2 are vulnerable to excessive memory allocation during token parsing. Fixed in 5.2.2 and 4.5.2. |
| [CVE-2024-40635](https://nvd.nist.gov/vuln/detail/CVE-2024-40635) | In containerd <1.6.38, containers with large UID:GID values could overflow to root privileges. Fixed in containerd 1.6.38+. |
| [CVE-2025-22869](https://nvd.nist.gov/vuln/detail/CVE-2025-22869) | SSH servers implementing file transfer protocols may face DoS via slow key exchange completion. |
| [CVE-2025-29923](https://nvd.nist.gov/vuln/detail/CVE-2025-29923) | `go-redis` versions before 9.5.5, 9.6.3, and 9.7.3 could return out-of-order responses during connection setup. Fixed in newer releases. |
| [CVE-2025-22870](https://nvd.nist.gov/vuln/detail/CVE-2025-22870) | IPv6 zone IDs may be misinterpreted as hostnames during proxy matching. |
| [CVE-2024-6345](https://nvd.nist.gov/vuln/detail/CVE-2024-6345) | Vulnerability in setuptools ≤69.1.1 allows RCE via malicious package URLs. Fixed in 70.0. |
| [CVE-2024-56326](https://nvd.nist.gov/vuln/detail/CVE-2024-56326) | Jinja <3.1.5 allows sandbox bypass via indirect `str.format` calls. Fixed in 3.1.5. |
| [CVE-2025-27516](https://nvd.nist.gov/vuln/detail/CVE-2025-27516) | Jinja <3.1.6 allows sandbox escape using the `|attr` filter to access unsafe attributes. Fixed in 3.1.6. |
| [CVE-2024-56201](https://nvd.nist.gov/vuln/detail/CVE-2024-56201) | Jinja <3.1.5 allows RCE when both filename and content of a template are attacker-controlled. Fixed in 3.1.5. |
| [CVE-2025-22868](https://nvd.nist.gov/vuln/detail/CVE-2025-22868) | Malformed tokens could consume excessive memory during parsing. |
| [CVE-2025-27144](https://nvd.nist.gov/vuln/detail/CVE-2025-27144) | Go JOSE <4.0.5 could consume excessive memory when parsing JWTs with many periods. Fixed in 4.0.5. |
| [CVE-2025-24976](https://nvd.nist.gov/vuln/detail/CVE-2025-24976) | In registry 3.0.0-beta.1–3.0.0-rc.2, token authentication may accept untrusted signing keys. Fixed in 3.0.0-rc.3. |
| [CVE-2024-45341](https://nvd.nist.gov/vuln/detail/CVE-2024-45341) | Certificates with IPv6 zone IDs may incorrectly satisfy URI name constraints. |
| [CVE-2024-45336](https://nvd.nist.gov/vuln/detail/CVE-2024-45336) | HTTP clients could incorrectly resend sensitive headers after certain redirects. |
| [CVE-2025-47273](https://nvd.nist.gov/vuln/detail/CVE-2025-47273) | setuptools <78.1.1 vulnerable to path traversal allowing file writes to arbitrary locations. Fixed in 78.1.1. |
