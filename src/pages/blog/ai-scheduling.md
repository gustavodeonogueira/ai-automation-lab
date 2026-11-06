
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

## A Real Challenge — How I Debugged the Scheduling Problem

The clinic's team started its activities at 8:30 AM, but appointments were only supposed to be scheduled between 9:00 AM and 5:00 PM.

During testing, we identified an issue with the AI scheduling agent. It was occasionally booking appointments outside the allowed hours, including appointments before 9:00 AM and at 6:00 PM.

To address this issue, I updated the agent's prompt by adding specific scheduling rules.

One of the most important changes was instructing the agent to recognize requests outside the permitted scheduling hours.

For example, when a customer requested an appointment before 9:00 AM, the agent was instructed to politely explain that appointments started at 9:00 AM and suggest an available time within the allowed schedule.

This experience helped me understand how important clear instructions and business rules are when building AI-powered automation workflows.


## Lessons Learned

LLMs are useful for understanding natural language,
but critical scheduling rules should also be
enforced by deterministic application logic.

## Next Steps

- Strengthen automated testing
- Improve input validation
- Explore implementation with Python and FastAPI
- A reliable AI automation system should not depend
only on prompt instructions.
- Critical business rules must also be validated
by the workflow before executing an action.
