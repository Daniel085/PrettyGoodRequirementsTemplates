# Story: [Story Title]

**Parent Epic**: [Link to Epic]
**Team**: [Frontend | Backend | Billing | Testing]
**Status**: [Backlog | Ready | In Progress | In Review | Done]
**Assignee**: [Developer Name]
**Story Points**: [1, 2, 3, 5, 8, 13]
**Created**: [YYYY-MM-DD]
**Sprint**: [Sprint Number]

---

## User Story

**As a** [user type/persona]
**I want** [capability or feature]
**So that** [business value or benefit]

---

## Description

[Brief description of what needs to be built and why. Provide context about how this fits into the larger Epic/Project.]

---

## Acceptance Criteria

[Specific, testable conditions that must be met for the story to be considered complete. Use Given-When-Then format when appropriate.]

### Functional Acceptance Criteria
- [ ] [Criterion 1: Specific, testable condition]
- [ ] [Criterion 2: ...]

### Technical Acceptance Criteria
- [ ] [Code reviewed and approved]
- [ ] [Unit tests written and passing]
- [ ] [Integration tests passing (if applicable)]
- [ ] [No new linting errors]
- [ ] [Performance requirements met]

### Quality Acceptance Criteria
- [ ] [Accessible (keyboard navigation, screen readers)]
- [ ] [Works in all supported browsers/devices]
- [ ] [Error handling implemented]
- [ ] [Logging/monitoring added]

---

## Definition of Done

- [ ] Code complete and committed
- [ ] Code review approved
- [ ] All acceptance criteria met
- [ ] Tests written and passing (unit, integration as needed)
- [ ] Documentation updated (code comments, API docs, user docs as needed)
- [ ] Deployed to dev/staging environment
- [ ] Product owner approval obtained
- [ ] No known defects

---

## Technical Details

### Implementation Approach
[High-level description of how this will be implemented. Key files, components, or modules to be modified/created.]

### API/Interface Changes
[Any API endpoints, function signatures, or interfaces that will be added or modified]

### Data Model Changes
[Any database schema changes, new tables, columns, indexes]

### Dependencies
- **Requires**: [Other stories, tasks, or external dependencies that must complete first]
- **Blocks**: [Other stories that are waiting on this]

---

## Design Assets

[Links to mockups, wireframes, design specs, or UI/UX guidelines]
- [Link to Figma/design file]
- [Link to prototype]

---

## Testing Considerations

### Test Scenarios
1. [Happy path test scenario]
2. [Edge case 1]
3. [Error condition 1]

### Test Data Needed
[Any specific test data, accounts, or configuration needed]

---

## Open Questions

- [ ] [Question requiring clarification before or during implementation]
- [ ] [...]

---

## Notes

[Any additional context, links to discussions, decisions made, or important information]

---

# EXAMPLE STORY

---

# Story: Implement WhatsApp Text Message Send API Endpoint

**Parent Epic**: [WhatsApp Messaging API Backend](EPIC_TEMPLATE.md#example-epic)
**Team**: Backend
**Status**: Ready
**Assignee**: Jordan Dev
**Story Points**: 5
**Created**: 2025-01-07
**Sprint**: Sprint 12

---

## User Story

**As a** developer using our communications API
**I want** to send WhatsApp text messages via REST API
**So that** I can programmatically notify my users via WhatsApp

---

## Description

Implement the core REST API endpoint for sending WhatsApp text messages. This is the most fundamental feature of the WhatsApp integration and follows the same patterns as our existing SMS API (`POST /v1/sms/messages`).

The endpoint should accept a request with sender phone number (WhatsApp Business number), recipient phone number, and message text. It should validate the request synchronously, queue the message for async delivery to Meta's WhatsApp API, and return a message SID for tracking.

This story focuses on text-only messages. Media messages and template messages will be handled in separate stories.

---

## Acceptance Criteria

### Functional Acceptance Criteria
- [ ] Endpoint `POST /v1/whatsapp/messages` accepts JSON payload with `from`, `to`, and `body` fields
- [ ] Validates that `from` number is a registered WhatsApp Business number for the account
- [ ] Validates that `to` is a valid E.164 phone number
- [ ] Validates that `body` is non-empty and ≤4096 characters (WhatsApp limit)
- [ ] Returns 201 Created with JSON response containing message `sid`, `status`, `from`, `to`, `created_at`
- [ ] Message is queued to Kafka topic `whatsapp_outbound_messages` for async processing
- [ ] Returns appropriate error codes for invalid inputs (400, 401, 403, 422)
- [ ] Respects account rate limits (returns 429 if exceeded)

### Technical Acceptance Criteria
- [ ] Code reviewed and approved by senior backend engineer
- [ ] Unit tests written for endpoint handler (≥85% coverage)
- [ ] Integration test validates end-to-end flow (API → Kafka → database)
- [ ] OpenAPI spec updated with endpoint documentation
- [ ] Structured logging includes request_id, account_id, message_sid
- [ ] Metrics instrumented (request count, latency, error rate)
- [ ] No new linting errors or warnings

### Quality Acceptance Criteria
- [ ] Input validation prevents injection attacks
- [ ] Error messages don't leak sensitive information
- [ ] API response time P95 < 50ms (excluding queue write)
- [ ] Graceful degradation if Kafka is temporarily unavailable (return 503)

---

## Definition of Done

- [ ] Code complete and merged to develop branch
- [ ] Code review approved by Mike Backend-Lead
- [ ] All acceptance criteria validated
- [ ] Unit tests passing (≥85% coverage for new code)
- [ ] Integration tests passing
- [ ] OpenAPI specification updated
- [ ] Deployed to dev environment
- [ ] Product owner verified endpoint behavior
- [ ] No P0 or P1 bugs

---

## Technical Details

### Implementation Approach
1. Create new route handler in `internal/handlers/whatsapp/messages.go`
2. Add request validation using existing validator library
3. Check account's WhatsApp phone numbers against `whatsapp_phone_numbers` table
4. Apply rate limiting using Redis (reuse existing rate limiter)
5. Generate message SID using same pattern as SMS (`WH` prefix + UUID)
6. Write message record to `whatsapp_messages` table with status='queued'
7. Publish message event to Kafka topic `whatsapp_outbound_messages`
8. Return JSON response with message details

### API/Interface Changes

**Request:**
```json
POST /v1/whatsapp/messages
Content-Type: application/json
Authorization: Bearer {api_key}

{
  "from": "+14155551234",
  "to": "+14155555678",
  "body": "Hello from WhatsApp!"
}
```

**Response (201 Created):**
```json
{
  "sid": "WH1234567890abcdef",
  "status": "queued",
  "from": "+14155551234",
  "to": "+14155555678",
  "body": "Hello from WhatsApp!",
  "created_at": "2025-01-07T10:30:00Z",
  "updated_at": "2025-01-07T10:30:00Z"
}
```

**Error Response (422):**
```json
{
  "code": 42201,
  "message": "Invalid 'from' number",
  "details": "The number +14155551234 is not a registered WhatsApp Business number for this account"
}
```

### Data Model Changes

No schema changes needed. Uses existing `whatsapp_messages` table:
```sql
-- Already exists from Epic database setup story
CREATE TABLE whatsapp_messages (
  id BIGSERIAL,
  sid VARCHAR(34) UNIQUE NOT NULL,
  account_id UUID NOT NULL,
  from_number VARCHAR(20) NOT NULL,
  to_number VARCHAR(20) NOT NULL,
  body TEXT,
  direction VARCHAR(20) NOT NULL, -- 'outbound' | 'inbound'
  status VARCHAR(20) NOT NULL, -- 'queued' | 'sent' | 'delivered' | 'failed'
  message_type VARCHAR(20) NOT NULL, -- 'text' | 'media' | 'template'
  created_at TIMESTAMP NOT NULL DEFAULT NOW(),
  updated_at TIMESTAMP NOT NULL DEFAULT NOW(),
  PRIMARY KEY (id, created_at)
) PARTITION BY RANGE (created_at);
```

### Dependencies
- **Requires**:
  - Database schema created (prerequisite story)
  - Kafka topic `whatsapp_outbound_messages` configured
  - `whatsapp_phone_numbers` table populated with test data
- **Blocks**:
  - WhatsApp message processor (background worker story)
  - Frontend integration story
  - Media message send API story

---

## Design Assets

- API Design Doc: [WhatsApp API Specification](link-to-doc)
- Sequence Diagram: [Message Send Flow](link-to-diagram)

---

## Testing Considerations

### Test Scenarios
1. **Happy path**: Valid request with registered phone number returns 201 with message SID
2. **Invalid sender**: Request with unregistered 'from' number returns 422
3. **Invalid recipient**: Malformed 'to' number returns 400
4. **Empty body**: Request with empty body returns 400
5. **Body too long**: Request with >4096 char body returns 400
6. **Rate limit exceeded**: 1001st message within hour returns 429
7. **Unauthorized**: Request without API key returns 401
8. **Kafka unavailable**: Returns 503 when Kafka is down

### Test Data Needed
- Test account with WhatsApp phone number +14155551234 registered
- Rate limit configured to 1000 messages/hour for test account
- Kafka topic `whatsapp_outbound_messages` available in test environment

---

## Open Questions

- [x] Should we validate that recipient phone number is WhatsApp-enabled before accepting? (Decision: No, too expensive to check on every request. Let delivery fail if recipient doesn't have WhatsApp)
- [x] What error code for Kafka unavailable? 503 Service Unavailable (consistent with other queue failures)
- [ ] Should we support both `body` and `text` field names for backward compatibility? (Need API standards decision)

---

## Notes

- This endpoint follows the same patterns as `POST /v1/sms/messages` for consistency
- Message delivery to Meta's WhatsApp API happens asynchronously in a separate worker (different story)
- Usage events for billing will be emitted by the background worker, not this API endpoint
- Consider adding request/response examples to OpenAPI spec for better developer experience
