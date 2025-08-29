Web Application Security Assessment Report.
Target: DVWA (Damn Vulnerable Web Application)
Prepared by: Oluwatosin Ruth olubowale
Date: August 2025


1. Executive Summary
This report presents the findings of a penetration test performed on DVWA. The focus was on identifying critical vulnerabilities that map the OWASP Top 10 2021. Three major vulnerabilities were identified: Brute Force , Cross-Site Request Forgery (CSRF), and SQL Injection. Each vulnerability poses a significant risk to confidentiality, integrity, and availability of the system.

2. Scope & Methodology
The assessment focused on DVWA in a controlled lab environment. Tools used included Burp Suite Community Edition and manual exploitation. Methodology followed OWASP Testing Guide v4 and mapped findings against OWASP Top 10 2021.

3. Findings & Vulnerabilities
3.1 Brute Force Authentication
Risk Rating: High
Description: The login form accepts unlimited attempts without rate limiting or account lockout. An attacker can automate credential guessing using tools such as Burp Intruder
Evidence: See Burp Suite attack log in Appendix.
Mitigation:
- Implement account lockout after a number of failed attempts
- Enforce CAPTCHA after several failed logins
- Introduce rate limiting on authentication endpoints
- Enable monitoring and alerting for suspicious login activity
  
3.2 Cross-Site Request Forgery (CSRF)
Risk Rating: Medium
Description: The application does not implement anti-CSRF tokens. An attacker can trick authenticated users into performing state-changing requests without their knowledge.
Evidence: CSRF PoC submitted successfully without token validation.
Mitigation:
- Implement anti-CSRF tokens and validate them on all state-changing requests
- Enforce SameSite cookie attributes
- Require re-authentication for sensitive actions

3.3 SQL Injection
Risk Rating: Critical
Description: User input in the 'ID' parameter is directly concatenated into SQL queries without sanitization. This allows attackers to extract database information and potentially gain administrative access.
Evidence: Payload '1 OR 1=1' returned multiple results, confirming injection.
Mitigation:
- Use parameterized queries (prepared statements)
- Employ stored procedures where applicable
- Validate and sanitize all user input
- Apply least-privilege to database accounts
  
4. OWASP Top 10 Mapping
Vulnerability	OWASP Top 10 2021 Category	Status
Brute Force Authentication	A07: Identification and Authentication Failures	Not Mitigated
Cross-Site Request Forgery (CSRF)	A05: Security Misconfiguration	Not Mitigated
SQL Injection	A03: Injection	Not Mitigated

5. Recommendations
Implement secure coding practices aligned with OWASP guidelines, perform regular penetration testing, and deploy Web Application Firewalls (WAFs) to detect and block exploitation attempts. Additionally, developers and administrators should undergo security awareness training.
