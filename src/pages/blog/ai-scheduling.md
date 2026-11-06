
---
layout: ../../layouts/BlogPostLayout.astro
title: "Building an AI-Powered Scheduling Workflow"
description: "Lessons from integrating AI agents, n8n and Google Calendar."
author: "Gustavo Nogueira"
---

## The Challenge

I worked on an AI-assisted appointment scheduling
workflow for a veterinary business.

The goal was to interpret customer requests,
check appointment availability, and integrate
the workflow with Google Calendar.

## Technologies Used

- AI agents and LLMs
- n8n
- REST APIs and Webhooks
- Google Calendar API

## How the System Works

1. A customer requests an appointment.
2. The AI agent identifies the service and requested time.
3. An n8n workflow processes the request.
4. Google Calendar is consulted for availability.
5. After confirmation, the appointment is registered.

## A Real Challenge

During testing, an appointment was scheduled
at 8:30 AM, although appointments should
only begin at 9:00 AM.

This highlighted the importance of validating
business rules independently of AI instructions.

## Lessons Learned

LLMs are useful for understanding natural language,
but critical scheduling rules should also be
enforced by deterministic application logic.

## Next Steps

- Strengthen automated testing
- Improve input validation
- Explore implementation with Python and FastAPI
