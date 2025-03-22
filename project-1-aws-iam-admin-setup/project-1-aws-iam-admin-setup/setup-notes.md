# Setup Notes – AWS IAM AdminUser Project

## Summary
Encountered "Access Denied" errors when logged in as AdminUser despite having AdministratorAccess via a group.

## Root Cause
No identity-based policy explicitly allowing key IAM actions like:
- `iam:GetAccountSummary`
- `iam:ListMFADevices`
- `iam:ListAccountAliases`
- `iam:ListAccessKeys`

## Fix
- Logged in as root
- Attached a custom inline policy granting full `iam:*` access
- Verified AdminUser now has full access

## Lessons Learned
- Even with AdministratorAccess, SCPs or permission boundaries can block actions
- Inline policies can be used as a fallback for troubleshooting IAM issues
- Always enable MFA for privileged users

## Next Steps
- Review for org-level SCPs
- Enable MFA
- Document all IAM changes in version control (this repo ✅)
