# Example: Breaking Down WhatsApp Business API Integration Project

This document demonstrates how to use the templates and AI Assistant Guide to break down the example Project into Epics, Stories, and Tasks.

---

## Source Project

See [PROJECT_TEMPLATE.md - Example Project](templates/PROJECT_TEMPLATE.md#example-project) for the full "WhatsApp Business API Integration" project definition.

---

## Step 1: Identify Functional Areas and Create Epics

After reading the Project document, we identify work for all four functional teams:

### Epic 1: Backend - WhatsApp Messaging API Backend
**Team**: Backend
**Scope**: Build the public API and Meta WhatsApp integration
**Story Points**: 55
**Sprints**: 12-16

**Key Deliverables:**
- REST API for sending WhatsApp messages
- Meta WhatsApp Cloud API integration
- Webhook delivery to customers
- Usage event capture for billing
- Message logging and history

**Dependencies:**
- **Needs**: Billing team's usage event schema (Sprint 12 Week 1)
- **Blocks**: Frontend UI, Billing usage tracking

See full Epic: [EPIC_TEMPLATE.md - Example Epic](templates/EPIC_TEMPLATE.md#example-epic)

---

### Epic 2: Frontend - WhatsApp Developer Portal UI
**Team**: Frontend
**Scope**: Build developer portal UI for WhatsApp management
**Story Points**: 34
**Sprints**: 13-17

**Key Deliverables:**
- WhatsApp message logs dashboard
- Phone number registration and verification UI
- Template management interface
- WhatsApp API documentation pages
- Configuration and settings UI

**Dependencies:**
- **Needs**: Backend API endpoints (Sprint 13 Week 2)
- **Blocks**: User acceptance testing

---

### Epic 3: Billing - WhatsApp Usage Tracking and Billing
**Team**: Billing
**Scope**: Track WhatsApp usage and calculate billing
**Story Points**: 21
**Sprints**: 13-16

**Key Deliverables:**
- Usage event ingestion from Kafka
- Per-message billing calculations
- WhatsApp usage in billing reports
- Usage-based rate limiting enforcement
- Pricing model implementation

**Dependencies:**
- **Needs**: Backend usage events (Sprint 13)
- **Blocks**: Revenue recognition, customer invoicing

---

### Epic 4: Testing - WhatsApp Integration Testing and QA
**Team**: Testing
**Scope**: Comprehensive testing across all components
**Story Points**: 21
**Sprints**: 14-16

**Key Deliverables:**
- End-to-end test automation
- Load testing (10,000 msg/sec)
- Security testing (OWASP, API security)
- Test data management
- Regression test suite

**Dependencies:**
- **Needs**: Backend API and Frontend UI in staging (Sprint 15 Week 2)
- **Blocks**: Production launch

---

## Step 2: Break Down Epic into Stories

Let's demonstrate Story breakdown for **Epic 1: Backend - WhatsApp Messaging API Backend**

### Story 1: Set Up WhatsApp Database Schema
**Story Points**: 3
**User Story**: As a backend engineer, I want the database schema for WhatsApp messages set up, so that I can store message data.

**Acceptance Criteria:**
- [ ] whatsapp_messages table created with partitioning
- [ ] whatsapp_templates table created
- [ ] whatsapp_phone_numbers table created
- [ ] Appropriate indexes created
- [ ] Migration tested and rolled back successfully

**Tasks:**
1. Create database migration for whatsapp_messages table (see [TASK_TEMPLATE.md example](templates/TASK_TEMPLATE.md#example-task))
2. Create database migration for whatsapp_templates table
3. Create database migration for whatsapp_phone_numbers table
4. Write integration tests for schema
5. Document database schema in technical docs

---

### Story 2: Implement WhatsApp Text Message Send API
**Story Points**: 5
**User Story**: As a developer, I want to send WhatsApp text messages via API, so that I can notify my users.

**Acceptance Criteria:**
- [ ] POST /v1/whatsapp/messages endpoint accepts text messages
- [ ] Validates sender is registered WhatsApp number
- [ ] Returns message SID for tracking
- [ ] Messages queued to Kafka for async processing
- [ ] API documented in OpenAPI spec
- [ ] P95 response time < 100ms

See full example: [STORY_TEMPLATE.md - Example Story](templates/STORY_TEMPLATE.md#example-story)

**Tasks:**
1. Create database migration for whatsapp_messages table (2 hours)
2. Implement POST /v1/whatsapp/messages endpoint handler (4 hours)
3. Add unit tests for message send endpoint (3 hours)
4. Add integration test for end-to-end flow (3 hours)
5. Update OpenAPI specification (1 hour)
6. Add Prometheus metrics for endpoint (1 hour)

---

### Story 3: Implement WhatsApp Message Background Processor
**Story Points**: 8
**User Story**: As the system, I want to process queued WhatsApp messages and deliver them to Meta, so that messages reach end users.

**Acceptance Criteria:**
- [ ] Kafka consumer reads from whatsapp_outbound_messages topic
- [ ] Messages delivered to Meta WhatsApp Cloud API
- [ ] Retry logic with exponential backoff (3 attempts)
- [ ] Usage events published to billing Kafka topic
- [ ] Message status updated in database
- [ ] Circuit breaker for Meta API outages
- [ ] Delivery success rate >98%

**Tasks:**
1. Create Kafka consumer for outbound messages (4 hours)
2. Implement Meta WhatsApp API client wrapper (6 hours)
3. Add retry logic with exponential backoff (3 hours)
4. Implement usage event publishing to billing topic (2 hours)
5. Add circuit breaker for Meta API (3 hours)
6. Write unit tests for processor (4 hours)
7. Write integration test with mock Meta API (4 hours)
8. Add monitoring and alerting (2 hours)

---

### Story 4: Implement WhatsApp Media Message Send API
**Story Points**: 5
**User Story**: As a developer, I want to send WhatsApp media messages (images, documents), so that I can share rich content with users.

**Acceptance Criteria:**
- [ ] POST /v1/whatsapp/messages accepts media_url parameter
- [ ] Supports image attachments (JPEG, PNG)
- [ ] Supports document attachments (PDF)
- [ ] Validates media URL accessibility
- [ ] Media delivered successfully to recipients
- [ ] API documented in OpenAPI spec

**Tasks:**
1. Extend message send endpoint to support media_url (3 hours)
2. Implement media URL validation (2 hours)
3. Update message processor for media messages (4 hours)
4. Add unit tests for media message sending (3 hours)
5. Add integration test for media delivery (3 hours)
6. Update OpenAPI specification (1 hour)

---

### Story 5: Implement Inbound Message Webhook Delivery
**Story Points**: 8
**User Story**: As a developer, I want to receive inbound WhatsApp messages via webhook, so that I can build conversational experiences.

**Acceptance Criteria:**
- [ ] Receive inbound messages from Meta webhook
- [ ] Deliver inbound messages to customer-configured webhook URL
- [ ] HMAC signature verification for security
- [ ] Retry logic (3 attempts with exponential backoff)
- [ ] Dead-letter queue for failed deliveries
- [ ] Webhook delivery latency P95 < 2s
- [ ] Delivery success rate >99%

**Tasks:**
1. Create webhook endpoint to receive Meta callbacks (4 hours)
2. Implement webhook delivery worker (5 hours)
3. Add HMAC signature generation (2 hours)
4. Add retry logic and dead-letter queue (3 hours)
5. Write unit tests for webhook delivery (4 hours)
6. Write integration test end-to-end (4 hours)
7. Add monitoring for webhook delivery metrics (2 hours)

---

### Story 6: Implement WhatsApp Template Message API
**Story Points**: 5
**User Story**: As a developer, I want to send template messages, so that I can send transactional notifications within WhatsApp policies.

**Acceptance Criteria:**
- [ ] POST /v1/whatsapp/templates creates template
- [ ] Template submitted to Meta for approval
- [ ] GET /v1/whatsapp/templates lists templates with approval status
- [ ] POST /v1/whatsapp/messages sends template messages
- [ ] Template parameters properly substituted
- [ ] API documented in OpenAPI spec

**Tasks:**
1. Implement POST /v1/whatsapp/templates endpoint (4 hours)
2. Implement GET /v1/whatsapp/templates endpoint (2 hours)
3. Integrate template submission to Meta API (4 hours)
4. Extend message send to support template_id parameter (3 hours)
5. Add unit tests for template API (3 hours)
6. Add integration tests (3 hours)
7. Update OpenAPI specification (1 hour)

---

### Story 7: Implement Message Status and History API
**Story Points**: 3
**User Story**: As a developer, I want to query message status and history, so that I can track message delivery and debug issues.

**Acceptance Criteria:**
- [ ] GET /v1/whatsapp/messages/{sid} returns message details
- [ ] GET /v1/whatsapp/messages lists messages with pagination
- [ ] Supports filtering by status, date range, from/to numbers
- [ ] Returns message body, status, timestamps
- [ ] Response time P95 < 100ms
- [ ] API documented in OpenAPI spec

**Tasks:**
1. Implement GET /v1/whatsapp/messages/{sid} endpoint (2 hours)
2. Implement GET /v1/whatsapp/messages list endpoint (4 hours)
3. Add query filters and pagination (3 hours)
4. Optimize database queries with indexes (2 hours)
5. Write unit tests (3 hours)
6. Write integration tests (2 hours)
7. Update OpenAPI specification (1 hour)

---

## Step 3: Break Down Story into Tasks

We've already shown Task breakdowns above. Here's the detailed example for **Story 2: Implement WhatsApp Text Message Send API**:

See full Task example: [TASK_TEMPLATE.md - Example Task](templates/TASK_TEMPLATE.md#example-task)

**Task 1**: Create database migration for whatsapp_messages table
- **Hours**: 2
- **Details**: PostgreSQL table with partitioning by date, indexes
- **Output**: Migration files (up and down)

**Task 2**: Implement POST /v1/whatsapp/messages endpoint handler
- **Hours**: 4
- **Details**: Route handler in Go, validation, Kafka publish
- **Output**: `internal/handlers/whatsapp/messages.go`

**Task 3**: Add unit tests for message send endpoint
- **Hours**: 3
- **Details**: Test happy path and error cases
- **Output**: `internal/handlers/whatsapp/messages_test.go`

**Task 4**: Add integration test for end-to-end flow
- **Hours**: 3
- **Details**: Test API → Kafka → database
- **Output**: `test/integration/whatsapp_test.go`

**Task 5**: Update OpenAPI specification
- **Hours**: 1
- **Details**: Document endpoint, request/response schemas
- **Output**: `docs/openapi.yaml`

**Task 6**: Add Prometheus metrics for endpoint
- **Hours**: 1
- **Details**: Instrument request count, latency, errors
- **Output**: Metrics in `internal/handlers/whatsapp/messages.go`

---

## Complete Ticket Hierarchy

```
Project: WhatsApp Business API Integration
│
├── Epic 1: Backend - WhatsApp Messaging API Backend (Backend Team, 55 points)
│   ├── Story 1: Set Up WhatsApp Database Schema (3 points)
│   │   ├── Task: Create whatsapp_messages table migration
│   │   ├── Task: Create whatsapp_templates table migration
│   │   ├── Task: Create whatsapp_phone_numbers table migration
│   │   ├── Task: Write integration tests for schema
│   │   └── Task: Document database schema
│   │
│   ├── Story 2: Implement WhatsApp Text Message Send API (5 points)
│   │   ├── Task: Create database migration for whatsapp_messages table
│   │   ├── Task: Implement POST /v1/whatsapp/messages endpoint handler
│   │   ├── Task: Add unit tests for message send endpoint
│   │   ├── Task: Add integration test for end-to-end flow
│   │   ├── Task: Update OpenAPI specification
│   │   └── Task: Add Prometheus metrics for endpoint
│   │
│   ├── Story 3: Implement WhatsApp Message Background Processor (8 points)
│   │   ├── Task: Create Kafka consumer for outbound messages
│   │   ├── Task: Implement Meta WhatsApp API client wrapper
│   │   ├── Task: Add retry logic with exponential backoff
│   │   ├── Task: Implement usage event publishing to billing topic
│   │   ├── Task: Add circuit breaker for Meta API
│   │   ├── Task: Write unit tests for processor
│   │   ├── Task: Write integration test with mock Meta API
│   │   └── Task: Add monitoring and alerting
│   │
│   ├── Story 4: Implement WhatsApp Media Message Send API (5 points)
│   ├── Story 5: Implement Inbound Message Webhook Delivery (8 points)
│   ├── Story 6: Implement WhatsApp Template Message API (5 points)
│   └── Story 7: Implement Message Status and History API (3 points)
│
├── Epic 2: Frontend - WhatsApp Developer Portal UI (Frontend Team, 34 points)
│   ├── Story: Create WhatsApp Message Logs Dashboard (8 points)
│   ├── Story: Create WhatsApp Phone Number Registration UI (5 points)
│   ├── Story: Create WhatsApp Template Management UI (5 points)
│   ├── Story: Create WhatsApp Configuration Settings Page (3 points)
│   ├── Story: Create WhatsApp API Documentation Pages (8 points)
│   └── Story: Add WhatsApp Usage Visualization to Dashboard (5 points)
│
├── Epic 3: Billing - WhatsApp Usage Tracking and Billing (Billing Team, 21 points)
│   ├── Story: Implement WhatsApp Usage Event Ingestion (5 points)
│   ├── Story: Implement WhatsApp Billing Calculations (8 points)
│   ├── Story: Add WhatsApp Usage to Billing Dashboard (3 points)
│   └── Story: Implement Usage-Based Rate Limiting (5 points)
│
└── Epic 4: Testing - WhatsApp Integration Testing and QA (Testing Team, 21 points)
    ├── Story: Create WhatsApp End-to-End Test Suite (8 points)
    ├── Story: Perform WhatsApp Load Testing (8 points)
    └── Story: Perform WhatsApp Security Testing (5 points)
```

---

## Summary

This example demonstrates:

1. **Project → Epic**: Identified 4 Epics (one per functional team)
2. **Epic → Story**: Broke down Backend Epic into 7 Stories
3. **Story → Task**: Broke down Stories into 5-8 Tasks each

**Key Principles Applied:**

- ✅ One Epic per functional team
- ✅ Stories follow INVEST criteria (Independent, Negotiable, Valuable, Estimable, Small, Testable)
- ✅ Stories deliver user-facing value
- ✅ Tasks are technical implementation steps
- ✅ Dependencies explicitly documented
- ✅ Realistic estimates (Story points, hours)
- ✅ Clear acceptance criteria at each level
- ✅ Proper team assignment

**What Makes This Breakdown Good:**

1. **Clear ownership**: Each Epic/Story/Task has single team assignment
2. **Right-sized**: Stories are 1-8 points, Tasks are 1-8 hours
3. **Independent value**: Each Story can be demoed independently
4. **Testable**: Clear acceptance criteria at each level
5. **Dependencies noted**: Know what blocks what
6. **Complete**: Covers implementation, testing, documentation, monitoring

This breakdown can now be used to:
- Create tickets in Jira/Linear/GitHub Issues
- Plan sprint work
- Assign work to developers
- Track progress
- Estimate timeline
