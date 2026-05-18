# AI-ready Knowledge Base Strategy — Enterprise Documentation Sample

## Overview

This sample demonstrates how an enterprise product knowledge base can be structured for better search, reuse, support, and AI-assisted retrieval.

The goal is to make documentation useful for both human readers and AI systems by using clear topic structure, consistent terminology, metadata, reusable content patterns, and troubleshooting-focused information architecture.

> **Note:** This is a sanitized portfolio sample. Product names, company names, customer data, screenshots, internal taxonomy, confidential workflows, and proprietary terms have been replaced with generic examples.

---

## Audience

This strategy is intended for:

- Documentation teams
- Technical writers
- Content strategists
- Product managers
- Support teams
- UX writers
- Knowledge base administrators
- AI/search implementation teams

---

## Goals

The knowledge base should help users:

- Find accurate answers quickly.
- Understand product features and workflows.
- Complete configuration tasks successfully.
- Troubleshoot common issues.
- Reuse content across product help, support articles, and release documentation.
- Support AI-powered search, chatbot, and RAG-based retrieval use cases.

---

# 1. Content Strategy Principles

## 1.1 Write for User Tasks

Content should be organized around what users want to do, not only around product menus.

### Example

Instead of:

```text
System Settings
```

Use:

```text
Configure system settings
Manage administrator access
Set up network connectivity
Enable monitoring and alerts
```

---

## 1.2 Use Consistent Topic Types

Each topic should follow a clear purpose.

| Topic Type | Purpose | Example |
|---|---|---|
| Concept | Explains what something is and why it matters. | What is high availability? |
| Task | Explains how to complete a procedure. | Configure a default gateway |
| Reference | Provides structured facts or command/API details. | CLI command reference |
| Troubleshooting | Helps users diagnose and fix issues. | WebUI is not reachable |
| Release Note | Explains product changes. | Known issues and fixed issues |
| FAQ | Answers common user questions. | Why is my license invalid? |

---

## 1.3 Follow One Topic, One Purpose

Each topic should answer one primary user need.

### Good topic

```text
Configure NTP server
```

### Weak topic

```text
System settings and time configuration and troubleshooting
```

---

# 2. Proposed Knowledge Base Taxonomy

## 2.1 Top-level Categories

| Category | Description |
|---|---|
| Getting Started | Product overview, access, login, initial setup. |
| Deployment | Cloud, hypervisor, and virtual appliance deployment guides. |
| Configuration | System, network, user, WebUI, API, and service configuration. |
| Administration | User management, backup, restore, license, upgrade, and monitoring. |
| API Documentation | REST API overview, authentication, endpoints, request/response examples. |
| CLI Documentation | CLI basics, command syntax, command reference, examples. |
| Troubleshooting | Problem-resolution articles, error messages, logs, diagnostics. |
| Release Notes | New features, changes, fixed issues, known issues, limitations. |
| Security | Authentication, authorization, certificates, hardening, access control. |
| FAQs | Short answers for common product questions. |

---

## 2.2 Example Category Mapping

| User Need | Recommended Category | Topic Example |
|---|---|---|
| Install product | Deployment | Deploy appliance on AWS-style environment |
| Configure IP address | Configuration | Configure management IP address |
| Use REST API | API Documentation | Authenticate API requests |
| Use CLI | CLI Documentation | CLI style conventions |
| Fix WebUI issue | Troubleshooting | WebUI is not reachable |
| Understand license | Administration | Assign product license |
| Review changes | Release Notes | Version 1.0 release notes |

---

# 3. Metadata Model

Metadata improves search, filtering, reuse, and AI retrieval.

## 3.1 Required Metadata

| Metadata Field | Description | Example |
|---|---|---|
| `title` | Clear topic title. | Configure default gateway |
| `topic_type` | Concept, task, reference, troubleshooting, FAQ, release note. | task |
| `product_area` | Product or module area. | Network Configuration |
| `audience` | Target user group. | Administrator |
| `platform` | Cloud, on-prem, virtual appliance, API, CLI. | Cloud |
| `version` | Product version or applicable release. | 1.x |
| `difficulty` | Beginner, intermediate, advanced. | Beginner |
| `keywords` | Search terms and synonyms. | gateway, route, default route |
| `last_reviewed` | Date content was reviewed. | 2026-05-18 |
| `owner` | Team responsible for accuracy. | Documentation / Product SME |

---

## 3.2 Sample Metadata Block

```yaml
title: Configure default gateway
topic_type: task
product_area: Network Configuration
audience: Administrator
platform: CLI
version: 1.x
difficulty: Beginner
keywords:
  - gateway
  - route
  - default route
  - network access
last_reviewed: 2026-05-18
owner: Documentation Team
```

---

# 4. AI/RAG-friendly Content Structure

AI-powered search and RAG systems perform better when content is clear, modular, and consistently structured.

## 4.1 Recommended Topic Structure

Use this structure for task-based articles:

```text
Title
Overview
When to use this task
Prerequisites
Procedure
Expected result
Verification
Troubleshooting
Related topics
```

---

## 4.2 Why This Helps AI Retrieval

| Structure | Benefit |
|---|---|
| Clear headings | Helps AI identify topic boundaries. |
| Short sections | Improves chunking and retrieval accuracy. |
| Tables | Makes parameters and error codes easier to parse. |
| Consistent terminology | Reduces ambiguity in search results. |
| Troubleshooting sections | Helps support chatbots answer issue-based questions. |
| Metadata | Improves filtering and ranking. |

---

# 5. Topic Template

Use the following template for task-based knowledge base articles.

```markdown
# <Task Title>

## Overview

Explain what the user will accomplish.

## When to use this task

Explain when this task applies.

## Prerequisites

- Requirement 1
- Requirement 2
- Requirement 3

## Procedure

1. Step one.
2. Step two.
3. Step three.

## Expected result

Explain the successful result.

## Verification

Use this section to confirm that the task worked.

## Troubleshooting

| Issue | Possible Cause | Resolution |
|---|---|---|
| Example issue | Example cause | Example resolution |

## Related topics

- Related topic 1
- Related topic 2
```

---

# 6. Example KB Article

## Configure Default Gateway

### Overview

Configure a default gateway to allow the appliance to reach networks outside the local subnet.

### When to use this task

Use this task during initial deployment or when the management network route changes.

### Prerequisites

- You have administrator access.
- The management interface has a valid IP address.
- The gateway IP address is reachable from the management subnet.

### Procedure

1. Log in to the CLI.
2. Enter Enable Mode.

   ```text
   NA> enable
   ```

3. Enter Configuration Mode.

   ```text
   NA# configure terminal
   ```

4. Configure the default gateway.

   ```text
   NA(config)# ip route default 192.0.2.1
   ```

5. Save the configuration.

   ```text
   NA# write memory
   ```

### Expected result

The default gateway is configured and saved.

### Verification

Run the following command:

```text
NA# show ip route
```

Expected output:

```text
Destination     Gateway       Interface
default         192.0.2.1     mgmt0
```

### Troubleshooting

| Issue | Possible Cause | Resolution |
|---|---|---|
| Gateway is not reachable | Incorrect gateway IP address. | Verify the gateway IP address and subnet. |
| Remote access is disconnected | Route change affected management access. | Connect through console and review route settings. |
| Configuration is lost after reboot | Configuration was not saved. | Run `write memory` after configuration changes. |

### Related topics

- Configure management IP address
- Configure DNS server
- Verify network connectivity

---

# 7. Troubleshooting Article Template

Use this template for issue-based articles.

```markdown
# <Problem Statement>

## Symptoms

Describe what the user sees.

## Environment

Describe where the issue occurs.

## Possible causes

- Cause 1
- Cause 2
- Cause 3

## Resolution

1. Step one.
2. Step two.
3. Step three.

## Verification

Explain how to confirm that the issue is resolved.

## Prevention

Explain how to avoid the issue in the future.

## Related topics

- Related topic 1
- Related topic 2
```

---

# 8. Example Troubleshooting Article

## WebUI is Not Reachable

### Symptoms

The administrator cannot open the WebUI from a browser.

### Environment

This issue may occur after deployment, network changes, or WebUI port updates.

### Possible Causes

- WebUI service is disabled.
- WebUI port is blocked by a firewall or security rule.
- Management IP address is incorrect.
- Default route is missing.
- Browser is using the wrong URL or port.

### Resolution

1. Connect to the appliance using the console or SSH.
2. Verify the WebUI settings.

   ```text
   NA# show webui settings
   ```

3. If WebUI is disabled, enable it.

   ```text
   NA(config)# webui on
   ```

4. Verify the WebUI port.

   ```text
   NA# show webui settings
   ```

5. Confirm that the security rule allows HTTPS traffic to the WebUI port.
6. Open the browser and enter:

   ```text
   https://192.0.2.10:8443
   ```

### Verification

The WebUI login page appears.

### Prevention

- Restrict WebUI access to trusted IP ranges.
- Document WebUI port changes.
- Validate WebUI access after network changes.

### Related topics

- Configure WebUI port
- Configure management IP address
- Verify security rules

---

# 9. Search and Keyword Strategy

## 9.1 Keyword Rules

Each topic should include natural keywords that users may search for.

### Example

For “Configure default gateway,” include:

```text
gateway
default route
route
network access
management access
cannot reach network
```

---

## 9.2 Synonym Mapping

| Preferred Term | Synonyms / Related Terms |
|---|---|
| WebUI | web interface, GUI, browser interface, admin portal |
| Default gateway | gateway, default route, route |
| Management IP | admin IP, management address, WebUI IP |
| License | activation key, license key, entitlement |
| REST API | API, RESTful API, automation API |
| Syslog | remote logging, log server, logging host |

---

# 10. Content Reuse Strategy

Reusable content improves consistency and reduces maintenance effort.

## 10.1 Reusable Content Examples

| Reusable Content | Where Used |
|---|---|
| Security note for credentials | API docs, CLI docs, deployment guides |
| WebUI access instructions | User guide, deployment guide, troubleshooting |
| License import steps | Admin guide, deployment guide, KB article |
| NTP configuration steps | CLI guide, deployment guide, troubleshooting |
| REST API authentication note | API guide, integration guide |

---

## 10.2 Example Reusable Note

```text
Security Note: Do not include real passwords, license keys, IP addresses, customer names, or screenshots in public documentation, logs, or repositories.
```

---

# 11. Governance and Review Workflow

## 11.1 Review Stages

| Stage | Owner | Purpose |
|---|---|---|
| Draft | Technical Writer | Create initial content. |
| SME Review | Engineering / Product SME | Validate technical accuracy. |
| Editorial Review | Documentation Team | Check style, grammar, structure, and consistency. |
| QA Validation | QA / Support | Validate steps in a test environment. |
| Publish | Documentation Owner | Publish approved content. |
| Maintenance | Documentation + Product Team | Update content for releases and known issues. |

---

## 11.2 Content Quality Checklist

| Check | Status |
|---|---|
| Title is clear and task-oriented. | Pending |
| Audience is identified. | Pending |
| Prerequisites are included. | Pending |
| Steps are sequential and testable. | Pending |
| Expected result is included. | Pending |
| Troubleshooting guidance is included. | Pending |
| Metadata is complete. | Pending |
| Confidential details are removed. | Pending |
| SME review is complete. | Pending |
| Content is ready for search and AI retrieval. | Pending |

---

# 12. Documentation Skills Demonstrated

This sample demonstrates:

- AI-ready knowledge base planning
- Content taxonomy
- Metadata design
- Topic-based authoring
- Troubleshooting article design
- Search keyword strategy
- Synonym mapping
- Reusable content planning
- RAG-friendly content structure
- Content governance workflow
- Documentation quality checklist
- Sanitized enterprise documentation strategy
