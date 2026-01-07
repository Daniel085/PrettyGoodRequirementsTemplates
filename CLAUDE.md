# Claude Assistant Guide for Pretty Good Requirements Templates

This repository provides a comprehensive template system for breaking down software projects into well-defined, actionable work items. This guide helps AI assistants (like Claude) understand and effectively use these templates.

---

## Quick Overview

This is a **5-level hierarchical ticket system** for software project planning:

```
Project → Capability → Epic → Story → Task
```

**Purpose**: Help teams break down large software initiatives into manageable, well-scoped work with clear ownership, dependencies, and acceptance criteria.

**Domain**: Communications API platform (similar to Twilio) with 4 functional teams: Frontend, Backend, Billing, Testing.

---

## When to Use This Repository

Use these templates when:
- ✅ User asks to break down a software project/feature/initiative
- ✅ User wants to create requirements documents
- ✅ User needs help organizing work across multiple teams
- ✅ User asks about ticket hierarchy, project planning, or work breakdown
- ✅ User wants to understand the relationship between Projects, Capabilities, Epics, Stories, and Tasks

**Do NOT use** when:
- ❌ User just wants to brainstorm ideas without formal structure
- ❌ User is asking about unrelated topics
- ❌ User wants simple task lists (not full project breakdown)

---

## The 5-Level Hierarchy

### 1. Project (Multiple Quarters)
- **What**: Large feature or initiative (e.g., "WhatsApp Business API Integration")
- **Duration**: Multiple quarters
- **Owner**: Product Manager
- **Template**: `templates/PROJECT_TEMPLATE.md`
- **Contains**: Multiple Capabilities (one per functional team)
- **Example**: WhatsApp Business API Integration spanning Q2-Q3 2025

### 2. Capability (Team-Specific, Multiple Quarters)
- **What**: Complete contribution of ONE functional team to a Project
- **Duration**: Multiple quarters (can span entire Project duration)
- **Owner**: Team Lead
- **Template**: `templates/CAPABILITY_TEMPLATE.md`
- **Contains**: Multiple Epics organized by quarter
- **Example**: "Backend - WhatsApp Messaging API" (all backend work for WhatsApp project)

### 3. Epic (Component of Business Value, Up to 1 Quarter)
- **What**: Component of user/business-facing value delivered within one quarter
- **Duration**: Up to 13 weeks (one quarter)
- **Owner**: Developer or Team Lead
- **Template**: `templates/EPIC_TEMPLATE.md`
- **Contains**: Multiple Stories (5-10 typically)
- **Example**: "WhatsApp Core Messaging" (Q2 2025) - fundamental send/receive capabilities

### 4. Story (Deliverable Increment, 1-5 Days)
- **What**: User-facing value that can be independently delivered
- **Duration**: 1-5 days
- **Owner**: Individual developer
- **Template**: `templates/STORY_TEMPLATE.md`
- **Contains**: Multiple Tasks (3-8 typically)
- **Criteria**: Must follow INVEST (Independent, Negotiable, Valuable, Estimable, Small, Testable)
- **Example**: "Implement WhatsApp Text Message Send API"

### 5. Task (Implementation Step, 1-8 Hours)
- **What**: Technical implementation step
- **Duration**: 1-8 hours
- **Owner**: Individual developer
- **Template**: `templates/TASK_TEMPLATE.md`
- **Example**: "Create database migration for whatsapp_messages table"

---

## Key Principles

### 1. Single Team Ownership
Every Capability, Epic, Story, and Task belongs to **exactly ONE team**:
- **Frontend**: Developer portal UI, documentation, sign-ups, application authorization
- **Backend**: APIs, third-party integrations, webhooks, database, background workers
- **Billing**: Usage tracking, pricing calculations, billing reports, usage-based limits
- **Testing**: QA, test automation, load testing, security testing

### 2. Breakdown Rules

**Project → Capability:**
- Create **one Capability per team** (usually 4 Capabilities total)
- Each Capability represents that team's complete contribution to the Project
- Can span multiple quarters

**Capability → Epic:**
- Organize work **by quarter** (up to 13 weeks per Epic)
- Each Epic delivers a **demonstrable component of business value**
- Start with foundational Epics (Q1), add advanced features later (Q2+)

**Epic → Story:**
- Each Story must **deliver independent user value**
- Follow **INVEST criteria**
- Stories are **1-5 days** of work (1-8 story points)
- Can be **demoed** independently

**Story → Task:**
- Tasks are **technical implementation steps**
- **1-8 hours** each
- Include: implementation, testing, documentation, monitoring

### 3. Dependencies Must Be Explicit
Always document:
- **Depends on**: What this ticket needs from other teams/tickets
- **Blocks**: What other tickets are waiting on this

### 4. Vertical Slicing
Stories should deliver **end-to-end value**, not horizontal layers:
- ✅ GOOD: "Implement user login" (includes frontend + backend + tests)
- ❌ BAD: "Create login database table" (just a horizontal layer)

---

## How to Help Users Break Down Work

### Step 1: Understand the Project
1. Ask user about the Project (if not provided)
2. Read/review the Project document
3. Identify functional areas (Frontend, Backend, Billing, Testing)

### Step 2: Create Capabilities (One Per Team)
For each functional team:
1. Identify what that team needs to deliver
2. Extract team-specific requirements from Project
3. Create a Capability document
4. Break down into quarterly Epics

### Step 3: Break Down Epics into Stories
For each Epic:
1. Identify user-facing capabilities
2. Create Stories that deliver independent value
3. Validate against INVEST criteria
4. Estimate story points (1, 2, 3, 5, 8, 13)

### Step 4: Break Down Stories into Tasks
For each Story:
1. Identify technical steps (database, API, tests, docs, monitoring)
2. Create Tasks (1-8 hours each)
3. Order by dependency

### Step 5: Document Dependencies
- Note what each Epic/Story needs from other teams
- Identify blocking relationships

---

## Working with Templates

### Using the Templates

**When creating new tickets:**
1. Copy the appropriate template from `templates/` directory
2. Fill in all sections (don't skip fields)
3. Replace `[placeholders]` with actual content
4. Update example sections or remove them

**Template Files:**
- `templates/PROJECT_TEMPLATE.md` - Full Project definition
- `templates/CAPABILITY_TEMPLATE.md` - Team-specific work breakdown
- `templates/EPIC_TEMPLATE.md` - Quarterly component of value
- `templates/STORY_TEMPLATE.md` - User story with acceptance criteria
- `templates/TASK_TEMPLATE.md` - Technical implementation task

**Example Data:**
Each template includes a complete example using the "WhatsApp Business API Integration" project. These examples demonstrate proper usage and serve as reference.

### Key Template Sections

**All templates include:**
- **Metadata**: Status, Owner, Created date, Team assignment
- **Overview/Purpose**: What and why
- **Acceptance Criteria**: Specific, testable conditions for "done"
- **Dependencies**: What's needed and what's blocked

**Project-specific sections:**
- Problem Statement, Value Proposition, User Stories, Requirements

**Epic/Story-specific sections:**
- User Stories, Technical Approach, Testing Considerations

---

## Reference Documentation

### Primary Documents
1. **AI_ASSISTANT_GUIDE.md**: Comprehensive guide for breaking down Projects → Capabilities → Epics → Stories → Tasks
   - Team responsibilities
   - Breakdown processes
   - Best practices
   - Examples

2. **BREAKDOWN_EXAMPLE.md**: Complete walkthrough showing how the WhatsApp project breaks down into all 5 levels

3. **README.md**: Repository overview and getting started guide

### Team Responsibilities Reference

**Frontend Team:**
- Developer portal UI/UX
- Sign-up and onboarding flows
- Dashboards and data visualization
- API documentation websites
- User documentation

**Backend Team:**
- Public APIs (REST, GraphQL)
- Third-party API integrations
- Webhook delivery infrastructure
- Database schema and migrations
- Background job processing
- Usage event capture for billing

**Billing Team:**
- Usage tracking and metering
- Billing calculations and invoicing
- Subscription management
- Payment processing integrations
- Usage-based pricing logic

**Testing Team:**
- Test strategy and planning
- Test automation (E2E, integration, load)
- Security testing
- CI/CD pipeline testing
- Quality metrics and reporting

---

## Common Patterns and Examples

### Example: Breaking Down a New Feature

**User Request**: "Help me plan adding SMS capabilities to our platform"

**Your Response:**
1. **Clarify scope**: Ask about requirements, constraints, timeline
2. **Create Project**: Use PROJECT_TEMPLATE.md to document problem, value prop, requirements
3. **Create Capabilities**: One for each team (Frontend, Backend, Billing, Testing)
4. **Break down into Epics**: Organize by quarter within each Capability
5. **Create Stories**: Break Epics into deliverable Stories
6. **Create Tasks**: Break Stories into implementation steps

### Team Assignment Decision Tree

**Backend if:**
- Involves API endpoints (GET, POST, PUT, DELETE)
- Involves database schema changes
- Involves third-party API integration
- Involves webhooks (sending or receiving)
- Involves background workers/jobs
- Involves usage event capture

**Frontend if:**
- Involves developer portal UI
- Involves dashboards/data visualization
- Involves sign-up/onboarding flows
- Involves user-facing configuration
- Involves user documentation

**Billing if:**
- Involves usage metering/tracking
- Involves pricing calculations
- Involves invoicing or billing reports
- Involves subscription management
- Involves usage-based rate limiting

**Testing if:**
- Involves test strategy or test automation
- Involves load testing or security testing
- Involves end-to-end testing across teams

---

## Quality Checks

Before finalizing any breakdown, verify:

### ✅ Capabilities
- [ ] One Capability per functional team
- [ ] Capabilities span appropriate duration (can be multiple quarters)
- [ ] Clear team ownership and responsibilities
- [ ] Dependencies documented

### ✅ Epics
- [ ] Duration ≤ one quarter (13 weeks)
- [ ] Delivers demonstrable business value
- [ ] Contains 5-10 Stories typically
- [ ] Organized by quarter within Capability

### ✅ Stories
- [ ] Follows INVEST criteria
- [ ] Deliverable in 1-5 days
- [ ] Can be demoed independently
- [ ] Clear acceptance criteria
- [ ] Story points assigned (1, 2, 3, 5, 8, 13)

### ✅ Tasks
- [ ] 1-8 hours each
- [ ] Specific technical action
- [ ] Clear completion criteria
- [ ] Ordered by dependency

### ✅ General
- [ ] All tickets have single team assignment
- [ ] Dependencies explicitly documented
- [ ] Estimates are realistic
- [ ] Coverage includes: implementation, testing, documentation, monitoring

---

## Common Mistakes to Avoid

### ❌ DON'T:
1. **Mix teams in one Capability/Epic/Story** - Each belongs to ONE team only
2. **Create Epics longer than one quarter** - Split into multiple Epics
3. **Make Stories too large** - If >8 points or >5 days, split it
4. **Make Tasks too large** - If >8 hours, break it down further
5. **Forget dependencies** - Always document what's needed and what's blocked
6. **Skip acceptance criteria** - Every Story needs clear "done" criteria
7. **Use horizontal slicing** - Stories should deliver end-to-end value
8. **Estimate in hours for Stories** - Use story points (Fibonacci: 1,2,3,5,8,13)
9. **Estimate in points for Tasks** - Use hours (1-8)

### ✅ DO:
1. **Start with the Project document** - Understand requirements first
2. **Create one Capability per team** - Clear team ownership
3. **Organize Epics by quarter** - Natural planning boundaries
4. **Follow INVEST for Stories** - Ensures quality
5. **Include all SDLC phases** - Implementation, testing, docs, monitoring
6. **Document dependencies explicitly** - Prevents blockers
7. **Use templates consistently** - Don't skip sections
8. **Validate business value** - Each Epic and Story should deliver value

---

## Example Queries and How to Respond

### Query: "Help me break down a project to add video calling"

**Response:**
1. Use PROJECT_TEMPLATE.md to create project document
2. Identify teams involved (Frontend, Backend, Billing, Testing)
3. Create 4 Capabilities (one per team)
4. For each Capability, break into quarterly Epics
5. For each Epic, create Stories following INVEST
6. For key Stories, show Task breakdown
7. Document dependencies between teams

### Query: "What's the difference between an Epic and a Story?"

**Response:**
- **Epic**: Component of business value, up to 1 quarter (13 weeks), contains 5-10 Stories
  - Example: "Video Calling Core Features" (Q2 2025)
- **Story**: User-facing value, 1-5 days, independently deliverable
  - Example: "Implement video call initiation API"
- **Key difference**: Epics are quarterly components, Stories are sprint-sized increments

### Query: "Which team should handle webhook delivery?"

**Response:**
Backend team handles:
- Webhook delivery infrastructure
- Sending webhooks to customers
- Webhook retry logic and dead-letter queues
- Webhook signature verification (HMAC)

Frontend team only handles:
- UI for configuring webhook URLs
- Displaying webhook delivery logs

---

## Tips for Effective Assistance

1. **Reference the example**: The WhatsApp Business API Integration example in each template is comprehensive - point users to it

2. **Use the AI_ASSISTANT_GUIDE.md**: When breaking down work, follow the processes documented there

3. **Be specific about teams**: Always assign work to exactly one team (Frontend, Backend, Billing, Testing)

4. **Think quarterly**: Epics should align with quarterly planning cycles

5. **Validate INVEST**: When creating Stories, explicitly check INVEST criteria

6. **Show hierarchy**: When presenting a breakdown, show the full hierarchy (Project → Capability → Epic → Story → Task)

7. **Document examples**: When creating tickets, include concrete examples in acceptance criteria

8. **Consider the full SDLC**: Don't forget testing, documentation, monitoring, and deployment

---

## Summary

This repository provides a **battle-tested system** for breaking down software projects into manageable work. The 5-level hierarchy (Project → Capability → Epic → Story → Task) provides:

- **Clarity**: Single team ownership at every level
- **Quarterly planning**: Epics aligned with OKRs and planning cycles
- **User value**: Stories deliver independently demonstrable value
- **Realistic sizing**: Stories (1-5 days), Tasks (1-8 hours)
- **Dependencies**: Explicit documentation prevents blockers
- **Quality**: INVEST criteria ensures well-formed Stories

When helping users with project planning, **always reference the templates and examples** provided. The WhatsApp Business API Integration example is comprehensive and demonstrates all best practices.

For detailed guidance, see:
- **AI_ASSISTANT_GUIDE.md** for breakdown processes
- **BREAKDOWN_EXAMPLE.md** for complete example
- **templates/** directory for all templates with examples
