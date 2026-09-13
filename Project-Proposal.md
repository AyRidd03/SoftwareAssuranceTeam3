1. **Project and Operational Environment**
   - GitHub Link: https://github.com/JBoogieman/CYBR8420-SoftwareAssuranceTeam3
   - Team Project Board: https://github.com/users/JBoogieman/projects/1
   - Chosen Software: Keycloak
   - Repository: https://github.com/keycloak/keycloak

2. **Systems Engineering View** — Justin
   - Diagram
   - Explanation of the system in the enterprise environment

3. **Security Needs, Threats, and Features** — Isaiah
- Security needs Why an IAM System Like Keycloak Matters
Organizations that use multiple applications need a secure way to manage user logins and access. Instead of having each application handle usernames, passwords, and permissions on its own, an Identity and Access Management (IAM) system like Keycloak can manage these tasks in one central location. Keycloak is designed to add authentication and secure applications without requiring developers to build their own login system from scratch.

Because Keycloak becomes a central part of an organization's security, protecting it is very important. A security problem with Keycloak could potentially give an attacker access to multiple applications. Important security needs include protecting user credentials, securing login sessions and access tokens, preventing brute-force and credential-stuffing attacks, and safely connecting to services such as LDAP or Active Directory. The Keycloak administration console also needs strong protection because administrators can control access to all connected applications.

Keycloak's own security policies show how seriously the project takes these risks. Its security policy includes a process for reporting vulnerabilities, a dedicated security response team, and procedures for handling CVEs. Overall, Keycloak is a good example of how centralizing identity can make managing security easier, but it also means the identity system itself must be strongly protected.

- Threats perceived by users
Community discussions and GitHub issues show some of the security problems that Keycloak users deal with in real-world situations. These issues are not always major vulnerabilities or CVEs, but they can still create security risks. For example, issue #16277 discusses making Keycloak's Content Security Policy (CSP) more secure because the default settings may be too permissive. Another issue, #9553, points out concerns with the use of `'unsafe-inline'` in the CSP. Other issues, such as #31640 and #10340, involve problems with redirect URLs and hostname settings in the admin console. Incorrect configuration of these settings could potentially create security problems such as open redirects.

Users also have concerns about keeping Keycloak and its dependencies up to date. Issues such as #50360 discuss vulnerabilities in dependencies, while #12934 shows how older CVEs may require additional attention from security teams. Overall, these community reports show that many of the security concerns with Keycloak are not necessarily complicated attacks. Instead, they often involve configuration mistakes, exposed admin settings, weak security policies, and outdated dependencies. This shows why properly configuring, monitoring, and updating an IAM system like Keycloak is an important part of keeping the overall environment secure.

- Keycloak features
Keycloak includes several built-in security features that help protect user accounts and applications. It has brute-force protection that can temporarily or permanently lock accounts after repeated failed login attempts. Administrators can also create and enforce password policies. Keycloak supports multi-factor authentication (MFA) through OTP/TOTP, WebAuthn security keys, and passkeys. It also provides recovery codes so users have another way to access their accounts if they lose their primary authentication method.

Keycloak also provides tools for managing user sessions. Administrators and users can view and revoke active sessions, set session timeouts, and control how long different types of tokens remain valid. Step-up authentication can require users to provide stronger authentication when performing sensitive actions. Keycloak also includes built-in protections against common attacks such as CSRF, clickjacking, SQL injection, open redirects, and SSRF. It supports HTTPS/SSL enforcement as well as controls for token revocation and access scopes.

In addition to these technical security features, Keycloak follows several security practices as an open-source project. The project has an OpenSSF Best Practices badge, publishes a security scorecard, and has a formal process for reporting and handling security vulnerabilities. Security researchers who report vulnerabilities can also receive credit in published security advisories. Overall, Keycloak provides multiple layers of protection for user accounts, sessions, tokens, and the applications connected to the IAM system.
5. **Team Motivation** — Sean
   - Why we selected Keycloak

6. **Open-Source Project Description** — Ayden
   - What Keycloak is
   - Contributors and activity
   - Use and popularity
   - Languages and platform
   - Documentation

7. **License and Contributions** – Sewhenu

   Keycloak is licensed under the **Apache License, Version 2.0**. The license permits the software to be used, modified, and distributed under its terms. When modified work is redistributed, required copyright and attribution notices must be retained and modified files must identify that changes were made. Contributions intentionally submitted to Keycloak are also provided under the Apache 2.0 license unless otherwise stated.

   Keycloak is an open-source, community-driven project that accepts contributions through GitHub. Each pull request should have an associated GitHub issue. Minor changes can proceed through an issue and pull request, while larger changes should first be discussed through GitHub Discussions so the proposed change can receive broader review. Pull requests should focus on one feature or change, include relevant tests and documentation, be rebased on the `main` branch, and use a descriptive commit message linked to the issue. Keycloak also requires the commits in a pull request to be squashed into a single commit. Maintainers review proposed changes and are responsible for approving contributions.

   Keycloak uses the **Developer's Certificate of Origin (DCO)** as a contributor requirement. Contributors must submit only work they have the legal right to contribute and that Keycloak can distribute under its license. Contributors are instructed to read the DCO and sign off their commits using the `--signoff` option with `git commit`. This adds a `Signed-off-by` line to the commit message and confirms the contributor's right to submit the contribution.

8. **Security History** — Sean
   - Known vulnerabilities
   - Security engineering decisions, changes, and features

9. **Team Reflection** — Sewhenu
   - Combined reflection from all five members

## References

- [Keycloak Repository](https://github.com/keycloak/keycloak)
- [Keycloak Documentation](https://www.keycloak.org/documentation)
- [Keycloak Security Advisories](https://github.com/keycloak/keycloak/security/advisories)
- [Keycloak License](https://github.com/keycloak/keycloak/blob/main/LICENSE.txt)
- [Keycloak Contributing Guidelines](https://github.com/keycloak/keycloak/blob/main/CONTRIBUTING.md)
- [Keycloak Governance](https://github.com/keycloak/keycloak/blob/main/GOVERNANCE.md)
- [Keycloak Maintainers](https://github.com/keycloak/keycloak/blob/main/MAINTAINERS.md)
