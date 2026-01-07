# Epic: [Epic Name]

**Parent Capability**: [Link to Capability]
**Team**: [Frontend | Backend | Billing | Testing]
**Status**: [Backlog | Ready | In Progress | Completed]
**Owner**: [Developer/Team Lead Name]
**Created**: [YYYY-MM-DD]
**Last Updated**: [YYYY-MM-DD]
**Target Quarter**: [Q1 2025]
**Duration**: [Up to one quarter]

---

## Overview

### Purpose
[Brief description of what this Epic accomplishes. What component of user or business value does this Epic deliver?]

### Business Value
[Clear statement of the user-facing or business value this Epic provides. What can users do after this Epic is complete that they couldn't do before?]

### Scope
[What specific functionality does this Epic cover? Be specific about what is included and excluded.]

---

## Goals and Success Criteria

### Primary Goals
1. [Specific goal this Epic achieves]
2. [...]

### Success Metrics
- [Measurable outcome 1]
- [Measurable outcome 2]

### Dependencies
- **Depends on**: [Other Epics, Stories, or external dependencies needed before this can start]
- **Blocks**: [What is waiting for this Epic to complete]

---

## User Stories

[List of user stories that comprise this Epic. These will be broken down into Story tickets.]

1. **As a** [user type], **I want** [capability], **so that** [benefit]
2. **As a** [user type], **I want** [capability], **so that** [benefit]
3. [...]

---

## Requirements

### Functional Requirements
- [ ] [Requirement 1]
- [ ] [Requirement 2]
- [ ] [...]

### Technical Requirements
- [ ] [Technical requirement 1]
- [ ] [Technical requirement 2]
- [ ] [...]

### Quality Requirements
- [ ] [Quality/non-functional requirement 1]
- [ ] [Quality/non-functional requirement 2]
- [ ] [...]

---

## Acceptance Criteria

### Epic Complete When:
- [ ] [Specific, testable criterion]
- [ ] All functional requirements implemented
- [ ] All Stories within Epic completed
- [ ] User value is demonstrable
- [ ] [...]

### Quality Gates:
- [ ] Code review completed
- [ ] Tests passing (unit, integration as appropriate)
- [ ] Documentation updated
- [ ] Security review completed (if applicable)
- [ ] Performance requirements met
- [ ] Deployed to production/available to users

---

## Technical Approach

### High-Level Design
[Brief description of the technical approach for this Epic]

### Key Components/Files
1. [Component/file 1]
2. [Component/file 2]

### Integration Points
[How this Epic integrates with other parts of the system]

---

## Risks and Mitigations

| Risk | Impact | Likelihood | Mitigation |
|------|--------|------------|------------|
| [Risk description] | [H/M/L] | [H/M/L] | [Mitigation plan] |

---

## Timeline and Milestones

### Estimated Effort
[Story points or time estimate]

### Key Milestones
- **[Date/Week]**: [Milestone 1]
- **[Date/Week]**: [Milestone 2]
- **[Date/Week]**: Epic Complete

---

## Open Questions
- [ ] [Question requiring resolution]
- [ ] [...]

---

## Related Documentation
- Parent Capability: [link]
- Technical Design Doc: [link]
- Design Mockups: [link]

---

# EXAMPLE EPIC

---

# Epic: WhatsApp Core Messaging

**Parent Capability**: [WhatsApp Messaging API Backend](CAPABILITY_TEMPLATE.md#example-capability)
**Team**: Backend
**Status**: In Progress
**Owner**: Jordan Dev-Lead
**Created**: 2025-01-07
**Last Updated**: 2025-01-07
**Target Quarter**: Q2 2025
**Duration**: 12 weeks (one quarter)

---

## Overview

### Purpose
Implement the fundamental WhatsApp messaging capabilities that enable developers to send and receive basic WhatsApp messages through our API. This Epic delivers the core value proposition of WhatsApp integration.

### Business Value
Developers can send text messages, images, and documents via WhatsApp to their end users, and receive inbound messages and delivery status updates via webhooks. This unlocks WhatsApp as a communication channel for our customers, enabling them to reach users on the world's most popular messaging platform.

### Scope
**Included:**
- Text message send API
- Media message send API (images, documents)
- Inbound message webhook delivery
- Delivery status webhook delivery
- Basic template messaging
- Message logging and history
- Usage event capture for billing

**Excluded:**
- Interactive messages (buttons, lists) - deferred to Epic 2
- Message scheduling - deferred to Epic 2
- Advanced analytics - deferred to Epic 2
- Video/audio messages - nice to have, may be added later

---

## Goals and Success Criteria

### Primary Goals
1. Launch functional WhatsApp messaging API in production
2. Enable developers to send/receive WhatsApp messages with <100ms API response time
3. Achieve >98% message delivery success rate
4. Capture all usage events for accurate billing

### Success Metrics
- 20+ beta customers successfully sending WhatsApp messages
- 10,000+ WhatsApp messages sent in first month
- API P95 response time < 100ms
- Message delivery success rate > 98%
- Webhook delivery success rate > 99%
- Zero billing discrepancies in beta period

### Dependencies
- **Depends on**:
  - Meta WhatsApp Cloud API access approved (in progress)
  - Database schema for messages created
  - Billing team's usage event schema defined
- **Blocks**:
  - Frontend: WhatsApp message logs dashboard
  - Epic 2: WhatsApp Advanced Features
  - Beta customer testing

---

## User Stories

[These will be broken down into detailed Story tickets]

1. **As a** developer, **I want** to send WhatsApp text messages via API, **so that** I can notify my users programmatically
2. **As a** developer, **I want** to send images and documents via WhatsApp, **so that** I can share rich content with users
3. **As a** developer, **I want** to receive inbound WhatsApp messages via webhook, **so that** I can build conversational experiences
4. **As a** developer, **I want** to receive delivery status updates, **so that** I know if my messages were successfully delivered
5. **As a** developer, **I want** to send template messages, **so that** I can send transactional notifications within WhatsApp policies
6. **As a** developer, **I want** to view my WhatsApp message history, **so that** I can debug issues and monitor usage

---

## Requirements

### Functional Requirements
- [ ] POST /v1/whatsapp/messages endpoint for sending text messages
- [ ] POST /v1/whatsapp/messages endpoint supports media attachments (images JPEG/PNG, documents PDF)
- [ ] POST /v1/whatsapp/messages endpoint supports template messages
- [ ] GET /v1/whatsapp/messages/{sid} endpoint to query message status
- [ ] Receive inbound messages from Meta and deliver to customer webhooks
- [ ] Receive delivery status updates from Meta and deliver to customer webhooks
- [ ] HMAC signature verification for webhook security
- [ ] Webhook retry logic (3 attempts with exponential backoff)
- [ ] Message logging to database with 90-day retention
- [ ] Usage event publishing to billing system

### Technical Requirements
- [ ] Kafka queue for async message processing
- [ ] Integration with Meta WhatsApp Cloud API
- [ ] Circuit breaker for Meta API outages
- [ ] Database schema with partitioning for message storage
- [ ] OpenAPI specification for all endpoints
- [ ] Structured logging with request correlation IDs
- [ ] Prometheus metrics for monitoring
- [ ] API rate limiting (1000 msg/hour default)

### Quality Requirements
- [ ] Unit test coverage ≥ 85%
- [ ] Integration tests for all API flows
- [ ] Load testing validates 10,000 msg/sec throughput
- [ ] API P95 response time < 100ms
- [ ] Webhook delivery P95 latency < 2s
- [ ] Security review passed (SQL injection, input validation, etc.)
- [ ] API documentation complete with code examples

---

## Acceptance Criteria

### Epic Complete When:
- [ ] Developer can send text WhatsApp messages via POST /v1/whatsapp/messages
- [ ] Developer can send image and document attachments
- [ ] Developer can send template messages
- [ ] Developer receives inbound messages at configured webhook URL
- [ ] Developer receives delivery status updates (sent, delivered, failed) via webhook
- [ ] Message history is queryable via GET /v1/whatsapp/messages/{sid}
- [ ] All usage events flow correctly to billing system
- [ ] 20+ beta customers successfully integrated and sending messages
- [ ] All quality gates passed (tests, load testing, security review)

### Quality Gates:
- [ ] Code review completed for all components
- [ ] Unit tests passing with ≥85% coverage
- [ ] Integration tests passing for all flows
- [ ] Load testing completed: sustained 10,000 msg/sec for 30 minutes
- [ ] Security review passed
- [ ] API documentation published
- [ ] Monitoring dashboards and alerts configured
- [ ] On-call runbook updated

---

## Technical Approach

### High-Level Design
1. **API Layer**: Go-based REST API with Gin framework
2. **Message Processing**: Kafka consumers for async processing
3. **Meta Integration**: Abstraction layer over Meta WhatsApp Cloud API
4. **Webhook Delivery**: Dedicated worker pool for customer webhook delivery
5. **Storage**: PostgreSQL with date partitioning for message history
6. **Caching**: Redis for rate limiting and account configuration

### Key Components/Files
1. `internal/handlers/whatsapp/messages.go` - Message send API handler
2. `internal/services/whatsapp/meta_client.go` - Meta API client
3. `internal/workers/whatsapp/message_processor.go` - Background message processor
4. `internal/workers/whatsapp/webhook_delivery.go` - Webhook delivery worker
5. `internal/models/whatsapp_message.go` - Message data model
6. `migrations/whatsapp_schema.sql` - Database schema

### Integration Points
- **Meta WhatsApp Cloud API**: Send messages, receive webhooks
- **Billing Service**: Publish usage events to Kafka topic `whatsapp_usage_events`
- **Auth Service**: Validate API keys and account permissions
- **Frontend**: REST API consumed by developer portal

---

## Risks and Mitigations

| Risk | Impact | Likelihood | Mitigation |
|------|--------|------------|------------|
| Meta API approval delayed | High | Medium | Started approval process early; have sandbox for dev/testing; engage Meta partnership team |
| Message delivery rate lower than expected | High | Medium | Comprehensive testing with Meta sandbox; implement retry logic; monitor delivery metrics closely |
| Webhook delivery reliability issues | Medium | Medium | Proven webhook infrastructure from SMS/voice; robust retry with DLQ; customer webhook health checks |
| Usage tracking bugs | High | Low | Extensive testing with billing team; reconciliation reports; monitor billing discrepancies |
| Load testing reveals performance issues | Medium | Low | Early load testing; horizontal scaling architecture; performance profiling |

---

## Timeline and Milestones

### Estimated Effort
34 story points

### Key Milestones
- **Week 1-2**: Database schema and core API structure
- **Week 3-4**: Message send API and Meta integration
- **Week 5-6**: Inbound webhooks and status updates
- **Week 7-8**: Template messaging and usage tracking
- **Week 9-10**: Testing, security review, performance optimization
- **Week 11**: Beta customer onboarding
- **Week 12**: Production launch

---

## Open Questions
- [x] What message retention policy? (Decision: 90 days hot storage, then archive to S3)
- [x] Support Go or Node.js? (Decision: Go for performance)
- [ ] What error codes for WhatsApp-specific failures? (Need API standards discussion)
- [ ] Should we implement message throttling when near rate limits? (Could reduce customer errors)

---

## Related Documentation
- Parent Capability: [WhatsApp Messaging API Backend](CAPABILITY_TEMPLATE.md#example-capability)
- Parent Project: [WhatsApp Business API Integration](PROJECT_TEMPLATE.md#example-project)
- Technical Design Doc: [WhatsApp API Architecture](link TBD)
- API Specification: [OpenAPI Spec](link TBD)
- Meta Documentation: https://developers.facebook.com/docs/whatsapp/cloud-api
