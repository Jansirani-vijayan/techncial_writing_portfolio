# User Manual Sample — Configuring User Access Control

## Overview

User Access Control allows administrators to manage who can access the application and what actions each user can perform. Administrators can create users, assign roles, enable or disable accounts, and review access permissions.

This sample demonstrates task-based user documentation for an enterprise software application.

---

## Audience

This guide is intended for:

- System administrators
- Application administrators
- Support engineers
- Internal IT teams

---

## Prerequisites

Before you begin, ensure that:

- You have administrator access to the application.
- The user account is already created or ready to be created.
- Required roles and permissions are defined by your organization.
- The application is accessible from a supported browser.

---

## User Roles

| Role | Description |
|---|---|
| Administrator | Has full access to configure users, roles, permissions, and system settings. |
| Manager | Can view dashboards, approve requests, and manage assigned team data. |
| Standard User | Can access assigned features and perform permitted actions. |
| Read-only User | Can view information but cannot create, edit, or delete records. |

---

## Configure User Access

Use this procedure to assign a role and enable access for a user.

### Steps

1. Log in to the application as an administrator.

2. From the left navigation menu, select **Administration > User Management**.

3. Click **Add User**.

4. In the **User Details** section, enter the following information:

   | Field | Description | Example |
   |---|---|---|
   | First Name | User's first name | Priya |
   | Last Name | User's last name | Raman |
   | Email Address | User's official email address | priya.raman@example.com |
   | Username | Unique login name for the user | praman |

5. In the **Role** drop-down list, select the required role.

6. In the **Account Status** field, select **Active**.

7. Click **Save**.

---

## Expected Result

The system creates the user account and displays the following confirmation message:

```text
User account created successfully.
