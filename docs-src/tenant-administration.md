# Tenant Administration

If your role has admin permissions, an **Admin** section in the nav gives you tools to manage your brewery's BrewIQ account. Which tabs you see depends on your specific permissions.

## Users

![The Admin Users tab listing users, their roles, and active status](images/admin-users.png)

This is where accounts get created - see [Getting Started](getting-started.md) for what a new user experiences.

Click **New user** and fill in their email, display name, and role. By default BrewIQ sends them an activation email (link valid 72 hours) to set their own password and register MFA. If you're a platform-level admin, you can instead choose **Generate a temporary password instead** to skip the email and hand them a one-time password directly - they'll be forced to change it on first login.

Per-user actions from the Users table:

- Toggle **Active/Inactive**
- Assign or remove **roles**
- **Resend activation** for anyone still pending
- **Reset password** - generates a new temporary password for them (same one-time reveal as account creation)
- **Reset MFA** - clears their enrollment; they'll be asked to set it up again next sign-in
- **Revoke devices** - every device they've [trusted](getting-started.md#trusted-devices) will need an MFA code again at its next sign-in - useful if they've lost a phone. Their MFA setup itself is left alone
- **Delete** (not available for your own account)

## Roles

![The Roles tab with built-in templates and custom roles in one table](images/admin-roles.png)

One table lists every role. The **templates** (Brewery Assistant, Customer Admin, Customer Reader and Ferment Assistant) are built into every brewery. They can't be edited, but the **copy** icon on a template makes your own editable copy, named "(Copy)" to start with. **Custom** roles carry a **Custom** tag and have **pencil** (edit) and **trash** (delete) icons. **New role** creates a custom role from scratch.

Editing a role opens a permission checklist - this is what controls what each role can see and do throughout BrewIQ (which Inventory tabs show up, whether they can manage devices, view fermentation data, edit recipes, and so on). Stock, Planning and Accounts each have their own read and write permissions, and Accounts permissions are split into Customers and Excise - so you can, for example, build a role for a bookkeeper that sees only Stock and Accounts. Accounts is only available to Commercial accounts.

## Trusted IPs

![The Trusted IPs tab listing IP/CIDR ranges that skip MFA](images/admin-trusted-ips.png)

Sign-ins from a trusted IP or subnet skip the MFA requirement. Add a CIDR range with a description to exempt it; removing one means sign-ins from that range require MFA again (if your role otherwise requires it).

### Trusted device length

Below the IP ranges, **Trusted device length (days)** sets how long a "Trust this device" tick at sign-in lasts for your team (see [Trusted devices](getting-started.md#trusted-devices)). It's 30 days by default, which is also the most allowed - you can make it shorter, or set it to **0** to turn the option off entirely. A shorter length also applies straight away to devices people have already trusted. Changing it needs the same permission as editing trusted IP ranges.

## Recipe Labels

![The Recipe Labels tab showing editable names for the 5 colour-coded labels](images/admin-recipe-labels.png)

Rename the 5 fixed colour-coded recipe labels (Proven, Ready to brew, Needs work, Seasonal, Retired, by default) to whatever fits your workflow. Existing recipes keep their label assignment - only the display name changes.

## Global settings

- **Session Timeout** - how many hours of inactivity before a session expires, for everyone on your account
- **Branding** - upload your brewery's logo (PNG/JPEG, up to 1MB) to appear on printed and shared recipes in place of the BrewIQ wordmark
