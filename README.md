# Pretty Good Requirements Templates

A comprehensive set of templates and guidelines for creating high-quality project requirements documentation following industry best practices.

## Overview

This repository provides:
- **Templates** for Projects, Epics, Stories, and Tasks
- **AI Assistant Guide** to help break down work and assign it to appropriate teams
- **Example Data** demonstrating real-world usage

## Template Hierarchy

```
Project (Feature/Capability level)
├── Epic (Team-level breakdown)
│   ├── Story (Deliverable user value)
│   │   └── Task (Technical implementation)
```

## Templates

### [Project Template](templates/PROJECT_TEMPLATE.md)
Highest level template following Amazon 1-pager format. Defines features and capabilities with:
- Problem Statement
- Value Proposition
- User Stories (business value focused)
- Requirements
- Acceptance Criteria
- Definition of Done

### [Epic Template](templates/EPIC_TEMPLATE.md)
Team-level work breakdown. Each Epic represents a significant chunk of work for a specific functional team.

### [Story Template](templates/STORY_TEMPLATE.md)
User-focused deliverable that provides business value. Stories should be independently deliverable.

### [Task Template](templates/TASK_TEMPLATE.md)
Technical implementation work. Tasks are the atomic units of work assigned to individual contributors.

## Team Structure

Our functional teams for a communications API platform (similar to Twilio):
- **Frontend**: Developer portal, sign-ups, application authorization UI, and documentation
- **Backend**: Public APIs, third-party integrations, authorization, and usage capture
- **Billing**: Usage tracking, pricing calculations, billing reports, and usage-based limits
- **Testing**: QA, test automation, load testing, and quality assurance

## AI Assistant Guide

See [AI_ASSISTANT_GUIDE.md](AI_ASSISTANT_GUIDE.md) for detailed instructions on:
- Breaking down Projects into Epics
- Decomposing Epics into Stories
- Creating Tasks from Stories
- Assigning work to appropriate teams based on responsibilities

## Getting Started

1. Review the [Project Template](templates/PROJECT_TEMPLATE.md) example
2. Use the template structure for your own project
3. Leverage the [AI Assistant Guide](AI_ASSISTANT_GUIDE.md) to break down work
4. Adapt templates to your specific needs

## Best Practices

- **INVEST Criteria**: Stories should be Independent, Negotiable, Valuable, Estimable, Small, and Testable
- **Clear Acceptance Criteria**: Use Given-When-Then format when appropriate
- **Team Alignment**: Ensure work is properly scoped to team capabilities
- **Vertical Slicing**: Break work into thin vertical slices that deliver end-to-end value
