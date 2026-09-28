# Interaction 2: Realm admin manages credentials and password policy: Ayden Riddle

I scoped the earlier four use cases and four misuse cases to this interaction. The use cases and misuse cases MU3 and MU3a are the diagram's own. MU-3 and MU-4 are new, because credential storage and password policy weren't covered before.

## Interaction description

The Realm admin sets or resets user credentials and configures the realm's password policy (length, composition, hashing, history, blacklist). Every account in the realm depends on this, so a mistake here weakens every login.

## Use/misuse case diagram

`![Diagram](diagrams/interaction_2_use_case_diagram.png)`
`![Diagram](diagrams/interaction_2_misuse_case_diagram.png)`

**Use cases (4):**

| ID | Use case | Diagram node |
|---|---|---|
| UC-1 | Set or reset user credentials | Manage users |
| UC-2 | Configure password policy and hashing | Configure flows |
| UC-3 | Validate credentials at login | Log in (SSO) |
| UC-4 | Review credential and admin events | View audit events |

**Misuse cases (4):**

| ID | Misuse case | Threatens |
|---|---|---|
| MU-1 | Take over the admin console and reset credentials or weaken the policy (existing MU3) | UC-1, UC-2 |
| MU-2 | Insider plants a known credential or lowers the policy (existing MU3a, extended to users) | UC-1, UC-2 |
| MU-3 | Credential stuffing or brute force exploiting a weak policy (new) | UC-3 |
| MU-4 | Offline cracking of dumped credential hashes (new) | UC-1, UC-2 |

## Misuser profile

| Misuser | Motive | Resources | Attack of choice | Access level |
|---|---|---|---|---|
| **Ransom Rick** (MU-1) | Extortion through control of all identities | High: breach lists, Shodan, exploit tooling | Brute force or default credentials on an exposed `/admin` console or bootstrap admin | External and unauthenticated, escalating to super-admin |
| **Disgruntled Dana** (MU-2) | Retaliation and retained access after leaving | Medium: realm knowledge and Admin REST API scripting | Privilege abuse: sets a known "temporary" password, or disables lockout or policy rules | Authenticated `manage-users` admin, not super-admin |
| **Stuffing Sam** (MU-3) | Resale of accounts and fraud | Medium: leaked password lists, botnet, proxy rotation | Credential stuffing and password spraying against the login endpoint | External and unauthenticated |
| **Dumper Dev** (MU-4) | Reusing cracked passwords on other sites | Medium to high: GPU rig, hashcat, a database backup or SQL injection foothold | Offline dictionary attack on stolen credential hashes | Read-only access to the Keycloak database or backups |

## Iteration narrative

1. **MU-1 (Rick).** He reaches the exposed admin console, tries the bootstrap admin, and resets a privileged user's password. The countermeasure is to restrict the console to an internal network and replace the bootstrap admin with a named admin.
2. **MU-1 residual.** Rick phishes a real admin and logs in with the stolen password. The countermeasure is mandatory MFA (WebAuthn) for admin roles, plus brute-force lockout.
3. **MU-2 (Dana).** With legitimate `manage-users` rights she sets a known permanent password, or weakens the policy so she can pick a trivial one. The countermeasures are fine-grained admin permissions (no policy editing for user managers), forced "temporary" passwords, and admin event auditing.
4. **MU-2 residual.** She tampers with the audit trail, or collaborates with a second admin. The countermeasures are shipping admin events to an external append-only log and requiring two-person approval for privileged changes.
5. **MU-3 (Sam).** Users reuse leaked passwords, and a lax policy accepts them. The countermeasures are a password blacklist, minimum length, brute-force detection, and MFA.
6. **MU-4 (Dev).** He gets a database dump and cracks the hashes offline. The countermeasures are a memory-hard hash (Argon2) or high PBKDF2 iterations, database encryption and backup protection, and forcing a rehash and rotation after a suspected breach.
7. **MU-4 residual.** Weak passwords still fall to a dictionary attack. The countermeasure is to combine the blacklist and length policy with passkeys or WebAuthn, so there is no password to crack.

## Derived security requirements

"Implemented?" is my reading of the docs. Links are to the official Keycloak docs, and the section anchors and source paths should be checked against your Keycloak version.

| ID | Requirement | Addresses misuse case | Implemented in Keycloak? (doc/code link) |
|---|---|---|---|
| SR-2.1 | The admin console shall be reachable only from trusted networks. The bootstrap admin shall be removed after setup. | MU-1 | **Partial.** Keycloak 26 issues a temporary bootstrap admin, but network restriction is done at the reverse proxy or hostname config: [Admin console hostname](https://www.keycloak.org/server/hostname), [Reverse proxy](https://www.keycloak.org/server/reverseproxy) |
| SR-2.2 | All admin accounts shall require MFA (WebAuthn or OTP). | MU-1 | **Partial.** Achievable via authentication flows and a conditional role check, but not enforced by default: [Authentication flows](https://www.keycloak.org/docs/latest/server_admin/#_authentication-flows) |
| SR-2.3 | Admin-set passwords shall be temporary and force a change at first login. | MU-2 | **Yes.** The "Temporary" toggle plus the Update Password required action: [User credentials](https://www.keycloak.org/docs/latest/server_admin/#user-credentials) |
| SR-2.4 | Users who manage users shall not be able to edit realm policy, and vice versa (least privilege). | MU-2 | **Partial.** Fine-grained admin permissions exist, but the feature has been changing between versions: [Fine-grained admin permissions](https://www.keycloak.org/docs/latest/server_admin/#_fine_grain_permissions) |
| SR-2.5 | Admin events (credential resets, policy changes) shall be recorded and exported to an external append-only store. | MU-2 | **Partial.** Admin events are built in but off by default. External export needs an event listener or log shipping: [Auditing admin events](https://www.keycloak.org/docs/latest/server_admin/#auditing-and-events) |
| SR-2.6 | Two-person approval shall be required for privileged credential and policy changes. | MU-2 | **No.** There is no native workflow, so it needs an external process or IGA tool. |
| SR-2.7 | Password policy shall enforce a minimum length, a blacklist, and a not-recently-used rule. | MU-3 | **Yes.** Built-in policy types: [Password policies](https://www.keycloak.org/docs/latest/server_admin/#_password-policies); code under `services/src/main/java/org/keycloak/policy/` |
| SR-2.8 | Repeated failed logins shall trigger temporary or permanent lockout. | MU-3 | **Yes, opt-in.** Brute-force detection is disabled by default: [Brute force](https://www.keycloak.org/docs/latest/server_admin/#password-guess-brute-force-attacks) |
| SR-2.9 | Passwords shall be stored with a memory-hard or high-iteration hash, and a policy change shall force rehash. | MU-4 | **Partial.** Argon2 is the default for non-FIPS deployments in recent versions, and PBKDF2-SHA512 defaults to 210,000 iterations. Rehash happens only at the user's next login: [Password hashing](https://www.keycloak.org/docs/latest/server_admin/#_password-policies) |
| SR-2.10 | Phishing-resistant credentials (WebAuthn or passkeys) shall be available for all users. | MU-3, MU-4 | **Yes.** WebAuthn and passkey support: [WebAuthn](https://www.keycloak.org/docs/latest/server_admin/#_webauthn) |
| SR-2.11 | Alerts shall be raised when the password policy is weakened or a service account gains admin roles. | MU-2 | **No.** There is no built-in alerting, so it needs SIEM rules over admin events. |

## Alignment observations

- **Well covered:** Password composition, blacklist, history, expiry, hashing choice, temporary passwords, brute-force lockout, and WebAuthn are all native, and each one is directly traceable to a misuse case.
- **Off by default, so easy to miss:** Brute-force detection and admin event logging are disabled in a new realm. A deployment can therefore satisfy the feature list and still be exposed to MU-2 and MU-3. Hardening guidance should treat them as mandatory settings.
- **Policy is not retroactive:** The docs say a new password policy does not apply to existing users until they change their password, unless you use "Update password" or "Expire password". This partly defeats SR-2.9 and SR-2.7 after a breach, because old weak hashes and passwords persist until the next login.
- **Insider threat is the weak spot:** Keycloak has no two-person approval (SR-2.6) and no built-in alerting (SR-2.11), and fine-grained permissions are still evolving. MU-2's final residual risk is therefore only reducible with external tooling.
- **Admin MFA is configuration, not a guarantee:** SR-2.2 depends on the operator building the right flow. The bootstrap admin is safer in Keycloak 26 but still needs manual replacement.
