# Okta Identity Lab

A hands-on Identity and Access Management (IAM) lab built on **Okta**, covering the full path from setting up an organization to handling real helpdesk-style support tickets. Everything was built and tested from scratch on the **Okta Integrator Free Plan**, and every step is documented with screenshots.

> **Goal:** learn how a company controls who can sign in, what they can access, and how to fix problems when access breaks.

![Okta Admin Console](Screenshots/cp1-dashboard.png)

---

## What I Built

- A small "company" inside Okta: **10 users** across **IT, HR, and Sales**, organized with groups
- A least-privilege admin setup: one Super Admin and one **Help Desk Administrator** role
- **Single Sign-On (SSO)** with three apps assigned by group (a bookmark app, a SAML app, and an OIDC app)
- **Multi-factor authentication (MFA)**: an enrollment policy and a sign-in rule that asks for a second factor
- The full employee life cycle: **joiner, mover, and leaver**
- **5 support ticket simulations**, solved with log analysis in the Okta System Log

---

## Skills Demonstrated

| Area | What I did |
|---|---|
| Identity management | Created users, groups, and profile attributes in Okta Universal Directory |
| Access control | Assigned apps to groups and tested who gets in and who is blocked |
| Authentication | Configured MFA enrollment and sign-in policies |
| SSO | Set up SAML and OIDC integrations and tested an OIDC login flow |
| Least privilege | Gave the helpdesk account only the Help Desk Administrator role |
| User life cycle | Onboarded, moved, and deactivated users |
| Troubleshooting | Used a repeatable method: identify, check logs, find root cause, fix, verify |
| Log analysis | Read System Log events to trace sign-ins, MFA challenges, and failures |

**Tools:** Okta Admin Console, Okta System Log, SAML 2.0, OpenID Connect (OIDC)

---

## Project Checkpoints

| # | Checkpoint | Document |
|---|---|---|
| 1 | Org setup and admin security | [01 - Org Setup and Admin Security](Documents/01-Org-Setup-and-Admin-Security.pdf) |
| 2 | Users, groups, and least privilege | [02 - Users, Groups and Least Privilege](Documents/02-Users-Groups-and-Least-Privilege.pdf) |
| 3 | Single Sign-On (SAML and OIDC) | [03 - SSO with SAML and OIDC](Documents/03-SSO-SAML-and-OIDC.pdf) |
| 4 | MFA and sign-in policies | [04 - MFA and Sign-in Policies](Documents/04-MFA-and-Sign-in-Policies.pdf) |
| 5 | Joiner, mover, leaver | [05 - Joiner Mover Leaver](Documents/05-Joiner-Mover-Leaver.pdf) |
| 6 | Support tickets and log analysis | [06 - Support Tickets and Log Analysis](Documents/06-Support-Tickets-and-Log-Analysis.pdf) |

---

## Key Results

- **Group-based access works:** an IT user signed in through the OIDC app successfully, while a Sales user was blocked with *"User is not assigned to the client application."*
- **MFA policy works:** the sign-in rule triggered a challenge, asked for email verification, and then allowed access. The System Log shows the full sequence.
- **Life cycle works:** after moving a user from IT to Sales, his dashboard changed to show only his new group's apps. A deactivated user lost access immediately, and deactivating freed a slot under the free plan's user limit.
- **Support method works:** all 5 tickets were solved using the same five steps and verified afterward.

![Sign-in sequence in the System Log](Screenshots/cp6-system-log.png)

---

## Support Tickets Handled

| Ticket | Problem | Root cause | Fix |
|---|---|---|---|
| 1 | User can't sign in | Account was suspended | Unsuspended the account |
| 2 | Forgot password | Password needed an admin reset | Created a one-time temporary password, forced change at next login |
| 3 | App missing from dashboard | User was removed from a group | Restored the group membership |
| 4 | Possible suspicious login | One failed password, then success from the same IP seconds later | Concluded it was a typo, no action needed |
| 5 | Lost device or authenticator | Passkey was no longer available | Reset the authenticator so the user could sign in again |

---

## Limitations and Honest Notes

I want this project to be clear about what it does and doesn't show:

- **User limit:** the free plan allows only 10 active users, so I planned the lab around that limit.
- **SAML test:** the SAML app was created and assigned correctly, but the login test on a third-party test site did not work. I proved SSO with an **OIDC** test instead.
- **Helpdesk account:** the Help Desk Administrator account was created and configured, but it could not finish its second-factor login in my lab setup. I performed the ticket fixes from the Super Admin account. In a real company, the Help Desk Admin role would handle them.
- **Phishing-resistant setting:** I relaxed this setting on one rule so email codes could be used as a test factor. In production I would keep it on for important apps.
- **Bookmark apps:** these cannot take a sign-in policy, so the MFA policy was attached to the OIDC app instead.
- **Test data only:** all users, emails, and apps are fake and exist only for this lab. No real personal data was used.

---

## What I Learned

- Protect the admin account with MFA before building anything else
- Assign access to **groups**, not individual people
- Give each role only the access it needs (**least privilege**)
- **Deactivate** leavers instead of deleting them, so access is blocked but the record stays for audits
- Read the **log** before guessing at a cause
- Verify a person's identity before resetting a password or MFA

---

## Repository Structure
