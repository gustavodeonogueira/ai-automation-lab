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

## Inside the n8n Workflow

The screenshots below document the workflow I built in n8n. The AI agent interprets the customer's request, while the workflow routes the action, communicates with Google Calendar, and returns structured results. This separation helps keep scheduling operations outside the language model itself.

### 1. Request Routing and Calendar Operations

<img src="/ai-automation-lab/images/ai-scheduling-overview.webp" alt="Overview of the n8n scheduling workflow with availability checks, appointment creation, and cancellation paths" loading="lazy" style="display:block; width:100%; height:auto; border-radius:12px;" />

*Figure 1 — The webhook receives a scheduling request, and the action router directs it to availability lookup, appointment confirmation, cancellation, or an invalid-data response.*

The visible branches show how the workflow:

- Queries Google Calendar events and prepares available time slots.
- Checks for scheduling conflicts before creating an appointment.
- Locates an appointment and validates tutor and booking details before attempting cancellation.
- Returns confirmation, cancellation, or unavailable-slot responses to the calling agent.

### 2. Reservation and Conflict Handling

<img src="/ai-automation-lab/images/ai-scheduling-reservation.webp" alt="Detail of the n8n workflow with PostgreSQL reservation, availability decision, calendar creation, and release steps" loading="lazy" style="display:block; width:100%; height:auto; border-radius:12px;" />

*Figure 2 — A closer look at the confirmation path and PostgreSQL reservation steps intended to reduce simultaneous booking conflicts.*

The confirmation flow includes a final availability decision before the Google Calendar creation step. The screenshots also show database operations for reserving a slot, reading reservation state, completing a reservation, and releasing a reservation when necessary. These steps are designed to address competing requests for the same appointment time; their effectiveness still depends on the underlying database queries and error handling.

### Business Rules and Reliability

At the agent level, the scheduling rules include a 9:00 AM–5:00 PM appointment window and automatic scheduling only for general consultations and vaccinations. The workflow adds structured action routing and calendar conflict checks. The next reliability milestone is to verify that all business restrictions are enforced deterministically before an event is created, rather than trusting prompt instructions alone.

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
