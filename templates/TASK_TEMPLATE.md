# Task: [Task Title]

**Parent Story**: [Link to Story]
**Team**: [Frontend | Backend | Billing | Testing]
**Status**: [To Do | In Progress | In Review | Done | Blocked]
**Assignee**: [Developer Name]
**Estimated Hours**: [1-8 hours typical]
**Created**: [YYYY-MM-DD]
**Sprint**: [Sprint Number]

---

## Objective

[Clear, concise description of what needs to be done. Be specific about the technical work.]

---

## Acceptance Criteria

[Specific, testable conditions that must be met for the task to be considered complete]

- [ ] [Criterion 1: Specific outcome]
- [ ] [Criterion 2: ...]
- [ ] [Code reviewed (if applicable)]
- [ ] [Tests passing (if code change)]

---

## Implementation Details

[Detailed technical instructions, approach, or specifications. Include:]
- Files to be modified/created
- Specific functions, classes, or components to implement
- Code patterns or conventions to follow
- Configuration changes needed

---

## Testing

[How to verify this task is complete]
- [ ] [Manual test step 1]
- [ ] [Unit test to run]
- [ ] [Integration test to verify]

---

## Dependencies

- **Blocked by**: [Other tasks that must complete first]
- **Blocks**: [Other tasks waiting on this]

---

## References

- [Link to documentation]
- [Link to design spec]
- [Link to related PR or issue]

---

## Notes

[Any additional context, gotchas, or important information]

---

# EXAMPLE TASK

---

# Task: Create Database Migration for whatsapp_messages Table

**Parent Story**: [Implement WhatsApp Text Message Send API Endpoint](STORY_TEMPLATE.md#example-story)
**Team**: Backend
**Status**: To Do
**Assignee**: Jordan Dev
**Estimated Hours**: 2
**Created**: 2025-01-07
**Sprint**: Sprint 12

---

## Objective

Create a database migration script to add the `whatsapp_messages` table with partitioning by date. This table will store all WhatsApp message records (sent and received) for the WhatsApp API feature.

---

## Acceptance Criteria

- [ ] Migration script creates `whatsapp_messages` table with all required columns
- [ ] Table is partitioned by `created_at` with monthly partitions
- [ ] Initial partitions created for next 3 months
- [ ] Appropriate indexes created for query performance
- [ ] Foreign key constraint to accounts table
- [ ] Migration tested in dev environment
- [ ] Rollback migration script created and tested
- [ ] Migration reviewed by database team
- [ ] Documentation updated with table schema

---

## Implementation Details

### Migration File
Create new migration file: `migrations/20250107_add_whatsapp_messages_table.sql`

### Table Schema
```sql
-- Create the parent table with partitioning
CREATE TABLE whatsapp_messages (
  id BIGSERIAL,
  sid VARCHAR(34) UNIQUE NOT NULL,
  account_id UUID NOT NULL,
  from_number VARCHAR(20) NOT NULL,
  to_number VARCHAR(20) NOT NULL,
  body TEXT,
  media_url TEXT,
  direction VARCHAR(20) NOT NULL, -- 'outbound' | 'inbound'
  status VARCHAR(20) NOT NULL, -- 'queued' | 'sent' | 'delivered' | 'read' | 'failed'
  message_type VARCHAR(20) NOT NULL, -- 'text' | 'media' | 'template'
  error_code INTEGER,
  error_message TEXT,
  meta_message_id VARCHAR(255), -- WhatsApp's internal message ID
  created_at TIMESTAMP NOT NULL DEFAULT NOW(),
  updated_at TIMESTAMP NOT NULL DEFAULT NOW(),
  PRIMARY KEY (id, created_at),
  CONSTRAINT fk_account FOREIGN KEY (account_id) REFERENCES accounts(id)
) PARTITION BY RANGE (created_at);

-- Create initial partitions (3 months)
CREATE TABLE whatsapp_messages_2025_01 PARTITION OF whatsapp_messages
  FOR VALUES FROM ('2025-01-01') TO ('2025-02-01');

CREATE TABLE whatsapp_messages_2025_02 PARTITION OF whatsapp_messages
  FOR VALUES FROM ('2025-02-01') TO ('2025-03-01');

CREATE TABLE whatsapp_messages_2025_03 PARTITION OF whatsapp_messages
  FOR VALUES FROM ('2025-03-01') TO ('2025-04-01');

-- Create indexes
CREATE INDEX idx_whatsapp_messages_account_created
  ON whatsapp_messages (account_id, created_at DESC);

CREATE INDEX idx_whatsapp_messages_sid
  ON whatsapp_messages (sid);

CREATE INDEX idx_whatsapp_messages_status
  ON whatsapp_messages (status)
  WHERE status IN ('queued', 'failed');

CREATE INDEX idx_whatsapp_messages_from_to
  ON whatsapp_messages (from_number, to_number, created_at DESC);

-- Add table comment
COMMENT ON TABLE whatsapp_messages IS 'Stores all WhatsApp message records (inbound and outbound)';
```

### Rollback Migration
Create: `migrations/20250107_add_whatsapp_messages_table_down.sql`
```sql
-- Drop table (cascades to partitions)
DROP TABLE IF EXISTS whatsapp_messages CASCADE;
```

### Conventions to Follow
- Use snake_case for column names (existing convention)
- Include created_at/updated_at timestamps (audit trail)
- Use VARCHAR with explicit lengths (storage optimization)
- Foreign keys reference existing tables
- Indexes match expected query patterns

---

## Testing

### Manual Verification Steps
- [ ] Run migration in dev database: `./scripts/migrate.sh up`
- [ ] Verify table exists: `\dt whatsapp_messages*` in psql
- [ ] Verify partitions created: `SELECT * FROM pg_partitioned_table WHERE partrelid = 'whatsapp_messages'::regclass;`
- [ ] Verify indexes: `\di whatsapp_messages*`
- [ ] Test insert: `INSERT INTO whatsapp_messages (...) VALUES (...);`
- [ ] Test query performance: `EXPLAIN ANALYZE SELECT * FROM whatsapp_messages WHERE account_id = '...' ORDER BY created_at DESC LIMIT 10;`
- [ ] Test rollback: `./scripts/migrate.sh down`
- [ ] Re-run migration to verify idempotency

### Automated Tests
- [ ] Integration test inserts message record and queries it back
- [ ] Test that partition routing works correctly based on created_at
- [ ] Test that foreign key constraint prevents invalid account_id

---

## Dependencies

- **Blocked by**: None (can start immediately)
- **Blocks**:
  - Implement WhatsApp Text Message Send API Endpoint
  - Create WhatsApp message processor background worker
  - All other WhatsApp API backend tasks

---

## References

- PostgreSQL Partitioning Docs: https://www.postgresql.org/docs/15/ddl-partitioning.html
- Existing migration pattern: `migrations/20240801_add_sms_messages_table.sql`
- Database schema standards: [internal wiki link]

---

## Notes

- Partitioning by month provides good balance between partition count and partition size
- Consider setting up automated partition creation job (separate task/story)
- 7-day retention policy will be enforced by archival job (separate epic)
- `meta_message_id` stores WhatsApp's ID for correlation with their API events
- Indexes chosen based on expected query patterns:
  - List messages for account (by date)
  - Look up by SID
  - Find failed/queued messages for retry
  - Conversation view (from/to pair)
