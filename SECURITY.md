# Security Policy

## Reporting a vulnerability

Please **do not** open a public GitHub issue for security vulnerabilities.

Email: your-email@example.com  
Subject line: `[SKINIQ SECURITY]`

I'll respond within 48 hours and aim to patch within 14 days for verified issues.

## Security design

- No user accounts, no database, no PII stored anywhere
- Images analyzed in demo mode never leave the user's browser
- The Flask backend is self-hosted — users control their own data
- No third-party analytics or tracking
- GDPR- and HIPAA-conscious by design

## Supported versions

| Version | Supported |
|---------|-----------|
| Latest (`main`) | ✅ |
