# UX Writing Case Study — Improving Product Messages for an Enterprise Application

## Overview

This case study demonstrates how unclear product messages can be rewritten into clear, helpful, and action-oriented UX content.

The examples are based on common enterprise software scenarios such as login, user management, configuration, network setup, file upload, API connection, and system errors.

> **Note:** This is a sanitized portfolio sample. Product names, company names, screenshots, user data, IP addresses, and proprietary UI labels have been replaced with generic examples.

---

## Goal

The goal of UX writing is to help users understand:

- What happened
- Why it happened
- What they need to do next

Good UX writing reduces confusion, support tickets, and task failure.

---

## UX Writing Principles Used

| Principle | Description |
|---|---|
| Clarity | Use simple and direct language. |
| Action-oriented writing | Tell users what to do next. |
| Context | Explain the cause when it helps the user recover. |
| Consistency | Use the same terms across the product. |
| Accessibility | Avoid vague, emotional, or technical-only messages. |
| Brevity | Keep messages short without removing useful meaning. |

---

# 1. Error Message Improvements

## Example 1: Invalid IP Address

### Before

```text
Invalid input.
```

### Problem

The message does not tell the user which field is wrong or how to fix it.

### After

```text
Enter a valid IP address in the format 192.0.2.10.
```

### Why this works

- Identifies the expected input.
- Provides a clear example.
- Helps the user correct the error without asking support.

---

## Example 2: Missing Gateway IP

### Before

```text
Failed to save configuration.
```

### Problem

The message does not explain why the configuration failed.

### After

```text
The configuration could not be saved because the gateway IP address is missing. Enter the gateway IP address and try again.
```

### Why this works

- Explains the cause.
- Gives the user a recovery action.
- Avoids a generic failure message.

---

## Example 3: Duplicate Username

### Before

```text
User already exists.
```

### Problem

The message is understandable but does not guide the administrator.

### After

```text
This username is already in use. Enter a unique username or edit the existing user account.
```

### Why this works

- Uses plain language.
- Gives two possible next actions.
- Supports administrator workflow.

---

## Example 4: Unauthorized API Request

### Before

```text
401 Unauthorized.
```

### Problem

The message is technically correct but not helpful for non-developer users.

### After

```text
Authentication failed. Check the API token or sign in again.
```

### Why this works

- Converts a technical status code into user-friendly language.
- Keeps the recovery action simple.
- Works for both API and admin UI contexts.

---

# 2. Empty State Improvements

## Example 5: No Devices Added

### Before

```text
No data found.
```

### Problem

The message does not explain what data is missing or what the user should do.

### After

```text
No devices have been added yet. Add a device to start monitoring system health and alerts.
```

### Suggested Button Text

```text
Add Device
```

### Why this works

- Explains the empty state.
- Shows the value of the action.
- Provides a clear next step.

---

## Example 6: No Logs Available

### Before

```text
No records.
```

### Problem

The message is too generic.

### After

```text
No logs are available for the selected time range. Choose a different time range or refresh the page.
```

### Why this works

- Explains the possible reason.
- Suggests recovery actions.
- Reduces confusion during troubleshooting.

---

# 3. Confirmation Message Improvements

## Example 7: Configuration Saved

### Before

```text
Success.
```

### Problem

The message is too vague.

### After

```text
Configuration saved successfully.
```

### Why this works

- Confirms exactly what happened.
- Uses a consistent success pattern.
- Reassures the user.

---

## Example 8: User Account Disabled

### Before

```text
Done.
```

### Problem

The message does not confirm the completed action.

### After

```text
User account disabled successfully. The user can no longer sign in.
```

### Why this works

- Confirms the action.
- Explains the effect of the action.
- Helps administrators understand impact.

---

# 4. Warning Message Improvements

## Example 9: Delete User

### Before

```text
Are you sure?
```

### Problem

The message does not explain the consequence.

### After

```text
Delete this user account? This action removes the user’s access but does not delete existing audit records.
```

### Suggested Button Text

```text
Delete User
```

### Suggested Secondary Button

```text
Cancel
```

### Why this works

- Explains what will happen.
- Reduces accidental deletion.
- Uses specific button text.

---

## Example 10: Clear Configuration

### Before

```text
This operation cannot be undone.
```

### Problem

The message is serious but does not say what will be affected.

### After

```text
Clear all network settings? This will remove configured IP addresses, routes, and DNS servers. Remote access may be disconnected.
```

### Suggested Button Text

```text
Clear Network Settings
```

### Why this works

- Explains the scope of the action.
- Warns about remote access impact.
- Helps administrators make an informed decision.

---

# 5. Button Text Improvements

| Scenario | Before | After |
|---|---|---|
| Add device | `Submit` | `Add Device` |
| Save settings | `OK` | `Save Settings` |
| Delete account | `Yes` | `Delete User` |
| Cancel operation | `No` | `Cancel` |
| Upload license | `Upload` | `Upload License` |
| Test connection | `Go` | `Test Connection` |
| Start appliance | `Run` | `Start Appliance` |
| Stop appliance | `Stop` | `Shut Down Appliance` |

---

# 6. Field Label Improvements

| Scenario | Before | After |
|---|---|---|
| IP field | `IP` | `IP Address` |
| Gateway field | `GW` | `Default Gateway` |
| DNS field | `DNS` | `DNS Server` |
| Port field | `Port` | `Service Port` |
| User role field | `Type` | `User Role` |
| Search box | `Search` | `Search by name, IP address, or status` |

---

# 7. Tooltip Improvements

## Example 11: NTP Server

### Before

```text
Enter server.
```

### After

```text
Enter the IP address or hostname of the NTP server used to synchronize system time.
```

---

## Example 12: WebUI Port

### Before

```text
Port number.
```

### After

```text
Enter the HTTPS port used to access the WebUI. Use a port allowed by your firewall policy.
```

---

# 8. UX Writing Style Guide

## Voice and Tone

| Situation | Tone |
|---|---|
| Success | Clear and reassuring |
| Warning | Direct and specific |
| Error | Helpful and recovery-focused |
| Empty state | Informative and action-oriented |
| Confirmation | Clear about impact |

---

## Writing Rules

- Use active voice.
- Use simple words.
- Avoid vague messages such as `Failed`, `Error`, or `Invalid`.
- Tell users how to fix the issue.
- Use specific button labels.
- Avoid unnecessary punctuation.
- Use consistent terms across UI, help, and documentation.
- Do not expose internal error details unless required for troubleshooting.

---

# 9. Before and After Summary

| Content Type | Before | After |
|---|---|---|
| Error | `Invalid input.` | `Enter a valid IP address in the format 192.0.2.10.` |
| Empty state | `No data found.` | `No devices have been added yet. Add a device to start monitoring system health and alerts.` |
| Success | `Success.` | `Configuration saved successfully.` |
| Warning | `Are you sure?` | `Delete this user account? This action removes the user’s access but does not delete existing audit records.` |
| Button | `OK` | `Save Settings` |
| Tooltip | `Port number.` | `Enter the HTTPS port used to access the WebUI.` |

---

# 10. Documentation and UX Skills Demonstrated

This sample demonstrates:

- UX writing
- Error message improvement
- Empty state writing
- Confirmation and warning message writing
- Button and label improvement
- Tooltip writing
- Accessibility-friendly language
- User-focused content design
- Enterprise software microcopy
- Consistency between UI content and product documentation
