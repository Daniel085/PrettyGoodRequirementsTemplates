# AI Assistant Guide for Ticket Breakdown and Team Assignment

This guide helps AI assistants break down Projects into Capabilities, Capabilities into Epics, Epics into Stories, and Stories into Tasks, while correctly assigning work to functional teams.

---

## Table of Contents

1. [Team Responsibilities](#team-responsibilities)
2. [Ticket Hierarchy](#ticket-hierarchy)
3. [Breaking Down Projects into Capabilities](#breaking-down-projects-into-capabilities)
4. [Breaking Down Capabilities into Epics](#breaking-down-capabilities-into-epics)
5. [Breaking Down Epics into Stories](#breaking-down-epics-into-stories)
6. [Breaking Down Stories into Tasks](#breaking-down-stories-into-tasks)
7. [Best Practices](#best-practices)
8. [Example Breakdown](#example-breakdown)

---

## Team Responsibilities

### Frontend Team
**Responsible for:**
- Developer portal UI/UX implementation
- Sign-up and onboarding flows
- Application authorization UI
- Account management dashboards
- API documentation websites
- Usage dashboards and reporting UI
- Customer-facing configuration interfaces
- Responsive web design
- Browser compatibility
- Accessibility compliance (WCAG 2.1 AA)
- User documentation and help content

**Technologies typically used:**
- React, Vue, or Angular
- TypeScript/JavaScript
- HTML/CSS
- Frontend testing frameworks (Jest, Cypress, Playwright)

**Works closely with:**
- Backend team (API contracts, integration)
- Billing team (usage visualization)

---

### Backend Team
**Responsible for:**
- Public APIs (REST, GraphQL)
- API authentication and authorization
- Third-party API integrations (Twilio, WhatsApp, etc.)
- Message routing and delivery logic
- Webhook delivery infrastructure
- Database schema design and migrations
- Background job processing
- Caching strategies
- API rate limiting
- Service reliability and performance
- API documentation (OpenAPI specs)
- Usage event capture for billing

**Technologies typically used:**
- Go, Node.js, Python, or Java
- PostgreSQL, MySQL, or other databases
- Redis for caching
- Kafka, RabbitMQ, or other message queues
- Docker/Kubernetes

**Works closely with:**
- Frontend team (API contracts)
- Billing team (usage events)
- Testing team (API testing)

---

### Billing Team
**Responsible for:**
- Usage tracking and metering
- Billing calculations and invoicing
- Subscription management
- Payment processing integrations (Stripe, etc.)
- Usage-based pricing logic
- Billing reports and analytics
- Revenue recognition
- Refunds and credits processing
- Pricing model implementation
- Cost allocation and optimization

**Technologies typically used:**
- Programming languages: Python, Ruby, Go
- Billing platforms: Stripe, Chargebee
- Data warehouses: Snowflake, BigQuery
- Analytics tools: Looker, Tableau

**Works closely with:**
- Backend team (usage event ingestion)
- Frontend team (billing dashboard UI)

---

### Testing Team
**Responsible for:**
- Test strategy and planning
- End-to-end testing
- Integration testing
- Load and performance testing
- Security testing
- Test automation frameworks
- CI/CD pipeline testing
- Bug identification and documentation
- Quality metrics and reporting
- Test data management
- Regression testing

**Technologies typically used:**
- Test automation: Selenium, Cypress, Playwright, Postman
- Load testing: JMeter, k6, Locust
- Security testing: OWASP ZAP, Burp Suite
- CI/CD: Jenkins, GitHub Actions, CircleCI

**Works closely with:**
- All teams (validates their work)

---

## Ticket Hierarchy

```
Project (Large feature/initiative)
├── Capability (Team-specific work)
│   ├── Epic (Component of user/business value)
│   │   ├── Story (Deliverable increment)
│   │   │   ├── Task (Implementation step)
│   │   │   ├── Task (Implementation step)
│   │   │   └── Task (Implementation step)
│   │   ├── Story
│   │   │   └── Task
│   │   └── Story
│   ├── Epic (Another component)
│   │   └── Story
│   └── Epic (Yet another component)
├── Capability (Another team)
│   └── Epic
│       └── Story
└── Capability (Yet another team)
```

### Project
- **Scope**: Large feature or capability
- **Duration**: Multiple quarters
- **Owner**: Product Manager
- **Template**: PROJECT_TEMPLATE.md
- **Example**: WhatsApp Business API Integration

### Capability
- **Scope**: Team-specific work to deliver all of that team's contribution to the Project
- **Duration**: Multiple quarters (can span the entire Project duration)
- **Owner**: Team Lead
- **Team**: Single functional team (Frontend, Backend, Billing, Testing)
- **Template**: CAPABILITY_TEMPLATE.md
- **Contains**: Multiple Epics organized by quarter
- **Example**: WhatsApp Messaging API Backend (Backend team's complete contribution)

### Epic
- **Scope**: Component of user or business-facing value that can be delivered independently
- **Duration**: Up to one quarter (12-13 weeks)
- **Owner**: Developer or Team Lead
- **Team**: Single functional team (same as parent Capability)
- **Template**: EPIC_TEMPLATE.md
- **Contains**: Multiple Stories that together deliver the Epic's business value
- **Example**: WhatsApp Core Messaging (fundamental send/receive capabilities for Q2 2025)

### Story
- **Scope**: Delivers user-facing value, independently deliverable
- **Duration**: 1-5 days
- **Owner**: Individual developer
- **Team**: Single functional team (same as parent Epic)
- **Template**: STORY_TEMPLATE.md
- **INVEST criteria**: Independent, Negotiable, Valuable, Estimable, Small, Testable
- **Contains**: Multiple Tasks
- **Example**: Implement WhatsApp Text Message Send API

### Task
- **Scope**: Technical implementation step
- **Duration**: 1-8 hours
- **Owner**: Individual developer
- **Team**: Same as parent Story
- **Template**: TASK_TEMPLATE.md
- **Example**: Create database migration for whatsapp_messages table

---

## Breaking Down Projects into Capabilities

### Process

1. **Read the Project document thoroughly**
   - Understand problem statement, requirements, and success criteria
   - Identify all functional areas involved

2. **Identify work by functional team**
   - Frontend: Any UI, documentation, or developer portal work
   - Backend: Any API, integration, or server-side logic
   - Billing: Any usage tracking, pricing, or payment work
   - Testing: Test strategy, automation, and quality assurance

3. **Create one Capability per team**
   - Each Capability should contain all work for one functional team
   - Capability scope represents the team's complete contribution to the Project (can span multiple quarters)

4. **Define Capability scope and dependencies**
   - What does this team need to deliver?
   - What do they need from other teams?
   - What are they blocking?

5. **Extract relevant requirements**
   - Pull team-specific requirements from Project into Capability
   - Prioritize as Must Have / Should Have / Nice to Have

6. **Identify Epics within each Capability**
   - Break down the Capability into quarterly Epics
   - Each Epic should deliver a component of user or business value
   - Organize Epics by target quarter

### Team Assignment Rules

**Assign to Frontend if:**
- Involves developer portal UI
- Involves sign-up/onboarding flows
- Involves dashboards or data visualization
- Involves user-facing configuration
- Involves documentation website
- Involves any browser-based interface

**Assign to Backend if:**
- Involves REST/GraphQL API endpoints
- Involves third-party API integration
- Involves message routing or delivery
- Involves webhooks
- Involves database schema
- Involves background workers
- Involves authentication/authorization logic
- Involves usage event capture

**Assign to Billing if:**
- Involves usage metering or tracking
- Involves pricing calculations
- Involves subscription management
- Involves payment processing
- Involves invoicing
- Involves billing reports
- Involves usage-based limits

**Assign to Testing if:**
- Involves test strategy
- Involves test automation
- Involves load testing
- Involves security testing
- Involves end-to-end testing across multiple teams

### Example Capability Breakdown

For a Project "WhatsApp Business API Integration":

**Frontend Capability**: WhatsApp Developer Portal UI (spans Q2-Q3 2025)
- Epic 1 (Q2): Basic message logs and phone number registration
- Epic 2 (Q3): Template management and advanced analytics
- Dashboard for WhatsApp message logs
- Template management interface
- Phone number registration UI
- API documentation pages

**Backend Capability**: WhatsApp Messaging API Backend (spans Q2-Q3 2025)
- Epic 1 (Q2): WhatsApp Core Messaging (send/receive basic messages)
- Epic 2 (Q3): WhatsApp Advanced Features (interactive messages, scheduling)
- REST API endpoints for sending messages
- Meta WhatsApp API integration
- Webhook delivery to customers
- Usage event capture

**Billing Capability**: WhatsApp Usage Tracking and Billing (spans Q2-Q3 2025)
- Epic 1 (Q2): Basic usage tracking and billing
- Ingest WhatsApp usage events
- Calculate per-message billing
- Display WhatsApp usage in billing dashboard
- Usage-based rate limiting

**Testing Capability**: WhatsApp Integration Testing (Q2-Q3 2025)
- Epic 1 (Q2): End-to-end testing and load testing
- Epic 2 (Q3): Security testing and test automation refinements
- End-to-end test scenarios
- Load testing (10K msg/sec)
- Security testing
- Test automation for API and UI

---

## Breaking Down Capabilities into Epics

### Process

1. **Review Capability scope and requirements**
   - Understand the full scope of work for the team
   - Identify major components or milestones

2. **Organize work by quarter**
   - Group related work that can be delivered within one quarter
   - Each Epic should span no more than 12-13 weeks

3. **Define business value for each Epic**
   - What user or business value does this Epic deliver?
   - Can it be demonstrated independently?
   - Is it a natural milestone in the Capability?

4. **Sequence Epics**
   - Determine which Epics depend on others
   - Start with foundational work (Q1), add advanced features later (Q2+)
   - Consider dependencies with other teams' Epics

5. **Validate Epic sizing**
   - Each Epic should be substantial enough to warrant quarterly planning
   - Too small: combine with another Epic
   - Too large: split into multiple Epics

### Epic Characteristics

**Good Epic:**
- Delivers a complete component of user or business value
- Can be completed within one quarter (up to 13 weeks)
- Has clear business value that can be demonstrated
- Contains 5-10 Stories typically
- Independently valuable (with noted dependencies)

**Too Large (should be split):**
- Takes more than one quarter
- Has multiple distinct business values
- Can be naturally split into phases

**Too Small (should be combined):**
- Takes less than a month
- Minimal user-facing value
- Should be a Story instead of an Epic

### Example Epic Breakdown

For Backend Capability "WhatsApp Messaging API Backend":

**Epic 1: WhatsApp Core Messaging (Q2 2025)**
- **Business Value**: Developers can send/receive basic WhatsApp messages
- **Duration**: 12 weeks
- **Key Deliverables**:
  - Text message send API
  - Media message send API
  - Inbound message webhook delivery
  - Basic template messaging
  - Usage event capture

**Epic 2: WhatsApp Advanced Features (Q3 2025)**
- **Business Value**: Enhanced developer experience with advanced capabilities
- **Duration**: 10 weeks
- **Key Deliverables**:
  - Interactive messages (buttons, lists)
  - Message scheduling
  - Advanced analytics
  - Performance optimization

---

## Breaking Down Epics into Stories

### Process

1. **Review Epic requirements and user stories**
   - Understand what the Epic must deliver
   - Identify user-facing capabilities

2. **Group related functionality into Stories**
   - Each Story should deliver independent user value
   - Follow INVEST criteria (especially Independent and Valuable)
   - Keep Stories small (1-5 days of work)

3. **Define Story acceptance criteria**
   - Specific, testable conditions
   - Include functional, technical, and quality criteria

4. **Identify dependencies between Stories**
   - Some Stories may need to be sequential
   - Note blocking relationships

### Story Characteristics

**Good Story:**
- Delivers complete user value
- Can be demoed to stakeholders
- Has clear acceptance criteria
- Estimated at 1-8 story points
- Can be completed in a single sprint
- Follows INVEST criteria

**Too Large (should be split):**
- Takes more than 5 days
- Has multiple distinct user values
- Involves too many files/components
- Story points > 8

**Too Small (should be combined):**
- Less than 1 hour of work
- No testable user value
- Just a configuration change
- Should be a Task instead

### Example Story Breakdown

For Backend Epic "WhatsApp Core Messaging" (Q2 2025):

**Story 1**: Implement WhatsApp Text Message Send API
- Value: Developers can send text messages via API
- Acceptance: POST /v1/whatsapp/messages endpoint functional for text messages

**Story 2**: Implement WhatsApp Media Message Send API
- Value: Developers can send images and documents
- Acceptance: Media messages delivered successfully with images and PDFs

**Story 3**: Implement Inbound Message Webhook Delivery
- Value: Developers receive inbound messages
- Acceptance: Webhooks delivered with <2s latency, retry logic working

**Story 4**: Implement Template Message API
- Value: Developers can send template messages
- Acceptance: Templates can be created, submitted for approval, and used in messages

**Story 5**: Implement Message Status and History API
- Value: Developers can query message status and history
- Acceptance: GET /v1/whatsapp/messages endpoints return message data

---

## Breaking Down Stories into Tasks

### Process

1. **Review Story acceptance criteria**
   - Understand what must be delivered

2. **Identify technical steps**
   - What code needs to be written?
   - What configuration changes are needed?
   - What tests need to be created?

3. **Create Tasks for each significant step**
   - Database migrations
   - API endpoint implementation
   - Unit test creation
   - Integration test creation
   - Documentation updates
   - Configuration changes

4. **Order Tasks by dependency**
   - Database schema before API implementation
   - Implementation before tests (or TDD: tests before implementation)

### Task Characteristics

**Good Task:**
- Specific technical action
- 1-8 hours of work
- Clear completion criteria
- Assigned to one person

**Common Task Types:**
- Database migration
- Create API endpoint handler
- Write unit tests
- Write integration tests
- Update API documentation
- Add monitoring/logging
- Configure infrastructure
- Code review

### Example Task Breakdown

For Story "Implement WhatsApp Text Message Send API":

**Task 1**: Create database migration for whatsapp_messages table
- Technical: Add table schema with partitioning
- 2 hours

**Task 2**: Implement POST /v1/whatsapp/messages endpoint handler
- Technical: Route handler, validation, Kafka publish
- 4 hours

**Task 3**: Add unit tests for message send endpoint
- Technical: Test happy path and error cases
- 3 hours

**Task 4**: Add integration test for end-to-end flow
- Technical: Test API → Kafka → database
- 3 hours

**Task 5**: Update OpenAPI specification
- Technical: Document endpoint, request/response schemas
- 1 hour

**Task 6**: Add Prometheus metrics for endpoint
- Technical: Instrument request count, latency, errors
- 1 hour

---

## Best Practices

### Project → Capability Breakdown

1. **One Capability per team** (usually)
   - Exception: Very large teams or very large projects may split into multiple Capabilities
2. **Clear team ownership**
   - Capability owned by team lead
3. **Document dependencies explicitly**
   - What you need from others
   - What others need from you
4. **Balance workload**
   - Don't overload one team while others wait
5. **Span multiple quarters**
   - Capabilities represent the team's complete contribution and can span the Project duration

### Capability → Epic Breakdown

1. **Organize by quarter**
   - Each Epic targets one quarter (up to 13 weeks)
2. **Deliver business value**
   - Each Epic should deliver a demonstrable component of user or business value
3. **Sequence strategically**
   - Start with foundational Epics, build advanced features later
4. **Consider dependencies**
   - Epic dependencies within a Capability and across teams
5. **Right-size Epics**
   - Not too small (< 1 month), not too large (> 1 quarter)

### Epic → Story Breakdown

1. **Follow INVEST criteria**
   - Independent, Negotiable, Valuable, Estimable, Small, Testable
2. **Vertical slicing**
   - Each Story delivers end-to-end value, not horizontal layers
3. **Clear acceptance criteria**
   - Testable, specific conditions for "done"
4. **Appropriate size**
   - 1-8 story points, completable in one sprint
5. **Dependencies noted**
   - Link related Stories, note blocking relationships

### Story → Task Breakdown

1. **Technical focus**
   - Tasks are implementation steps, not user value
2. **Small and specific**
   - 1-8 hours each
3. **Ordered by dependency**
   - Can't write tests before implementing feature
4. **Clear completion criteria**
   - Specific output or deliverable

### Team Assignment

1. **Single team ownership**
   - Each Capability, Epic, Story, Task assigned to ONE team
2. **Consider integration work**
   - Backend creates API, Frontend consumes it (separate Stories in different Capabilities/Epics)
3. **Testing team involvement**
   - Testing team creates test automation Stories within their Capability/Epics
   - But developers on other teams also write unit tests (Tasks within their Stories)
4. **Documentation ownership**
   - API docs: Backend team
   - User docs: Frontend team (developer portal)

---

## Example Breakdown

### Project: WhatsApp Business API Integration

#### Capability 1: Backend - WhatsApp Messaging API Backend
**Team**: Backend
**Duration**: Q2-Q3 2025

##### Epic 1.1: WhatsApp Core Messaging (Q2 2025)
**Business Value**: Developers can send/receive basic WhatsApp messages

**Story 1.1.1**: Implement WhatsApp Text Message Send API
- **Task 1.1.1.1**: Create database migration for whatsapp_messages table
- **Task 1.1.1.2**: Implement POST /v1/whatsapp/messages endpoint handler
- **Task 1.1.1.3**: Add unit tests for message send endpoint
- **Task 1.1.1.4**: Add integration test for end-to-end flow
- **Task 1.1.1.5**: Update OpenAPI specification
- **Task 1.1.1.6**: Add Prometheus metrics for endpoint

**Story 1.1.2**: Implement WhatsApp Message Background Processor
- **Task 1.1.2.1**: Create Kafka consumer for outbound messages
- **Task 1.1.2.2**: Implement Meta WhatsApp API client
- **Task 1.1.2.3**: Add retry logic with exponential backoff
- **Task 1.1.2.4**: Add usage event publishing to billing topic
- **Task 1.1.2.5**: Write unit tests for processor
- **Task 1.1.2.6**: Write integration test with mock Meta API

**Story 1.1.3**: Implement Inbound Message Webhook Delivery
- **Task 1.1.3.1**: Create webhook endpoint to receive Meta callbacks
- **Task 1.1.3.2**: Implement webhook delivery worker
- **Task 1.1.3.3**: Add HMAC signature generation
- **Task 1.1.3.4**: Add retry logic and dead-letter queue
- **Task 1.1.3.5**: Write unit tests for webhook delivery
- **Task 1.1.3.6**: Write integration test end-to-end

##### Epic 1.2: WhatsApp Advanced Features (Q3 2025)
**Business Value**: Enhanced developer experience with advanced capabilities

**Story 1.2.1**: Implement Interactive Messages
**Story 1.2.2**: Implement Message Scheduling
**Story 1.2.3**: Add Advanced Analytics

#### Capability 2: Frontend - WhatsApp Developer Portal UI
**Team**: Frontend
**Duration**: Q2-Q3 2025

##### Epic 2.1: Basic WhatsApp UI Components (Q2 2025)
**Business Value**: Developers can view message logs and register phone numbers

**Story 2.1.1**: Create WhatsApp Message Logs Dashboard
- **Task 2.1.1.1**: Create React component for message log table
- **Task 2.1.1.2**: Implement pagination and filtering
- **Task 2.1.1.3**: Add search functionality
- **Task 2.1.1.4**: Integrate with backend API
- **Task 2.1.1.5**: Write component unit tests
- **Task 2.1.1.6**: Write E2E test for dashboard

**Story 2.1.2**: Create WhatsApp Phone Number Registration UI
- **Task 2.1.2.1**: Create phone number registration form
- **Task 2.1.2.2**: Implement verification flow
- **Task 2.1.2.3**: Add validation and error handling
- **Task 2.1.2.4**: Integrate with backend API
- **Task 2.1.2.5**: Write component tests
- **Task 2.1.2.6**: Add accessibility features

##### Epic 2.2: Advanced WhatsApp UI Features (Q3 2025)
**Business Value**: Developers can manage templates and view analytics

**Story 2.2.1**: Create WhatsApp Template Management UI
**Story 2.2.2**: Add Advanced Analytics Dashboard

#### Capability 3: Billing - WhatsApp Usage Tracking and Billing
**Team**: Billing
**Duration**: Q2-Q3 2025

##### Epic 3.1: WhatsApp Usage Tracking (Q2 2025)
**Business Value**: Accurate WhatsApp usage metering and billing

**Story 3.1.1**: Implement WhatsApp Usage Event Ingestion
- **Task 3.1.1**: Create Kafka consumer for WhatsApp usage events
- **Task 3.1.2**: Validate and transform events
- **Task 3.1.3**: Store events in usage data warehouse
- **Task 3.1.4**: Write unit tests for event processing
- **Task 3.1.5**: Write integration test end-to-end

**Story 3.2**: Implement WhatsApp Billing Calculations
- **Task 3.2.1**: Create pricing model for WhatsApp messages
- **Task 3.2.2**: Implement usage aggregation job
- **Task 3.2.3**: Calculate monthly charges
- **Task 3.2.4**: Write unit tests for billing logic
- **Task 3.2.5**: Validate calculations with finance team

**Story 3.3**: Add WhatsApp Usage to Billing Dashboard
- **Task 3.3.1**: Create API endpoint for WhatsApp usage data
- **Task 3.3.2**: Add WhatsApp section to billing report
- **Task 3.3.3**: Write tests for usage reporting

#### Capability 4: Testing - WhatsApp Integration Testing
**Team**: Testing
**Duration**: Q2-Q3 2025

##### Epic 4.1: WhatsApp Core Testing (Q2 2025)
**Business Value**: Validated quality and reliability of WhatsApp integration

**Story 4.1.1**: Create WhatsApp End-to-End Test Suite
- **Task 4.1.1**: Set up test environment with Meta sandbox
- **Task 4.1.2**: Create test scenarios (send, receive, templates)
- **Task 4.1.3**: Implement automated E2E tests
- **Task 4.1.4**: Integrate with CI/CD pipeline
- **Task 4.1.5**: Document test data setup

**Story 4.2**: Perform WhatsApp Load Testing
- **Task 4.2.1**: Set up load testing infrastructure (k6/JMeter)
- **Task 4.2.2**: Create load test scenarios (10K msg/sec)
- **Task 4.2.3**: Execute load tests and collect metrics
- **Task 4.2.4**: Document performance results and bottlenecks
- **Task 4.2.5**: Re-test after optimizations

**Story 4.3**: Perform WhatsApp Security Testing
- **Task 4.3.1**: Create security test plan
- **Task 4.3.2**: Test API authentication and authorization
- **Task 4.3.3**: Test webhook signature verification
- **Task 4.3.4**: Test input validation and injection attacks
- **Task 4.3.5**: Document findings and remediation

---

## Tips for AI Assistants

1. **Always read the full Project document before breaking down**
   - Understand requirements, constraints, and success criteria

2. **Consider all four teams for every Project**
   - Even if not obvious, there may be work for each team

3. **Use consistent naming conventions**
   - Capability: "[Team] - [Complete Contribution]" (e.g., "Backend - WhatsApp Messaging API")
   - Epic: "[Component of Value]" (e.g., "WhatsApp Core Messaging")
   - Story: "[Action] [Feature]" (e.g., "Implement Message Send API")
   - Task: "[Action] [Specific Component]" (e.g., "Create database migration")

4. **Be specific in Task descriptions**
   - Name actual files, functions, or components
   - Include technical details

5. **Link tickets hierarchically**
   - Tasks reference parent Story
   - Stories reference parent Epic
   - Epics reference parent Capability
   - Capabilities reference parent Project

6. **Estimate realistically**
   - Story points: 1, 2, 3, 5, 8, 13 (Fibonacci)
   - Tasks: Hours (1-8)
   - If larger, break it down further

7. **Consider the full software development lifecycle**
   - Implementation
   - Testing (unit, integration, E2E)
   - Documentation
   - Monitoring/logging
   - Deployment

8. **Validate with INVEST criteria for Stories**
   - Independent: Can be developed independently
   - Negotiable: Details can be discussed
   - Valuable: Delivers user value
   - Estimable: Can be estimated
   - Small: Completable in a sprint
   - Testable: Has clear acceptance criteria

9. **Think about integration points**
   - Backend creates API → Frontend consumes API (two Stories)
   - Backend emits events → Billing consumes events (dependency)

10. **Don't forget non-functional requirements**
    - Performance testing (Testing team)
    - Security testing (Testing team)
    - Monitoring dashboards (Backend team)
    - Documentation (Frontend for user docs, Backend for API docs)

---

## Summary

- **Projects** are broken down into **Capabilities** (one per functional team, spanning multiple quarters)
- **Capabilities** are broken down into **Epics** (components of business value, up to one quarter each)
- **Epics** are broken down into **Stories** (user-facing value, 1-5 days)
- **Stories** are broken down into **Tasks** (technical steps, 1-8 hours)
- Each ticket has **single team ownership**
- **Dependencies** are documented explicitly
- Follow **INVEST criteria** for Stories
- Tasks are **small, specific, and technical**
- Hierarchy: Project → Capability → Epic → Story → Task
