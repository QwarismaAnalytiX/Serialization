# Security Policy

## Supported Versions

The following versions of the Qwarisma AnalytiX Serialization Library are currently supported with security updates:

| Version | Supported          |
| ------- | ------------------ |
| 1.0.x   | :white_check_mark: |
| < 1.0   | :x:                |

## Reporting a Vulnerability

We take security vulnerabilities seriously. If you discover a security issue in this project, please report it responsibly.

### How to Report

**Please do NOT report security vulnerabilities through public GitHub issues.**

Instead, please report them via email to:

📧 **[qwarismaanalytix@hotmail.com](mailto:qwarismaanalytix@hotmail.com)**

### What to Include

When reporting a vulnerability, please include:

1. **Description**: A clear description of the vulnerability
2. **Impact**: The potential impact of the vulnerability
3. **Reproduction Steps**: Detailed steps to reproduce the issue
4. **Affected Versions**: Which versions are affected
5. **Suggested Fix**: If you have a suggested fix or mitigation (optional)

### What to Expect

- **Acknowledgment**: We will acknowledge receipt of your report within **48 hours**
- **Initial Assessment**: We will provide an initial assessment within **7 days**
- **Resolution Timeline**: We aim to resolve critical vulnerabilities within **30 days**
- **Credit**: We will credit you in our security advisory (unless you prefer anonymity)

### Our Commitment

- We will not take legal action against you for responsibly disclosing vulnerabilities
- We will work with you to understand and resolve the issue quickly
- We will keep you informed of our progress
- We will publicly acknowledge your contribution (with your permission)

## Security Best Practices

When using this library, we recommend:

### Input Validation

```cpp
// Always validate data before deserializing from untrusted sources
try {
    serialization::load(archive, data);
} catch (const std::exception& e) {
    // Handle malformed data appropriately
    log_error("Deserialization failed: ", e.what());
}
```

### Type Safety

- Use the library's compile-time type checking features
- Avoid deserializing to raw pointers; prefer smart pointers
- Validate type information when deserializing polymorphic objects

### Binary Data

- Be cautious when deserializing binary data from untrusted sources
- Consider size limits for containers to prevent memory exhaustion
- Validate data integrity before processing

## Security Updates

Security updates will be released as:

1. **Patch releases** for the current major version
2. **Security advisories** published on GitHub
3. **Announcements** on our GitHub repository

To stay informed about security updates:

- Watch this repository on GitHub
- Subscribe to our security advisories
- Check the [CHANGELOG](CHANGELOG.md) for security-related entries

## Contact

For security-related questions or concerns:

📧 **Email**: [qwarismaanalytix@hotmail.com](mailto:qwarismaanalytix@hotmail.com)
🔗 **GitHub**: [github.com/QwarismaAnalytiX/Serialization](https://github.com/QwarismaAnalytiX/Serialization)

---

Thank you for helping keep the Qwarisma AnalytiX Serialization Library and its users safe!

