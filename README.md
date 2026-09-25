# Auto Ticket Classification using Flow Designer

A small ServiceNow project I built to stop IT staff from manually reading and categorizing every school helpdesk ticket by hand. When a student or teacher submits a ticket describing an issue — Wi-Fi, a projector, a forgotten password, a slow computer — Flow Designer scans the description for keywords and automatically fills in the Category and Subcategory, then sends the caller a confirmation email. No scripting, no machine learning, just a keyword-driven flow on top of a small custom table.

## The problem

The school IT helpdesk receives multiple incident requests daily from students and teachers, such as Wi-Fi issues, projector failures, password problems, and slow computers. Currently, IT staff manually reviews each request and assigns a category, which is time-consuming and inefficient.

## How it works, briefly

1. A ticket gets created on a custom `Incident WorkFlow` table with just a Caller and a Short Description.
2. A Flow Designer flow triggers on creation (while Category is still empty).
3. The flow checks the Short Description against a set of keywords and sets Category + Subcategory accordingly:
   - Wi-Fi / Network → Category: Network, Subcategory: Wi-Fi
   - Projector → Category: Hardware, Subcategory: Projector
   - Password / Login → Category: Access, Subcategory: Forgot Password
   - Slow / Hanging → Category: Performance, Subcategory: Slow Computer
4. The flow sends a confirmation email back to the caller.

## Repo structure

| File | What's in it |
|---|---|
| `1. Brainstorming & Ideation Phase.md` | The problem, alternatives I considered, and why I went keyword-based instead of ML |
| `2. Requirement Analysis Phase.md` | Business use case, requirements, and setting up the Update Set |
| `3. Project Design Phase Phase.md` | The `Incident WorkFlow` table design, fields, and the Category/Subcategory dependency mapping |
| `4. Project Planning Phase.md` | Phase breakdown, timeline, tools used, and known risks |
| `5. Project Development Phase.md` | Full build walkthrough — table, fields, dependencies, and the Flow Designer flow |
| `6. Project Testing Phase.md` | Test scenarios, email verification, and results |
| `7. Project Documentation Phase.md` | Deployment steps, setup instructions, and maintenance notes |
| `8. Project Demonstration Phase.md` | A script for demoing the working system end to end |

## Tech used

- ServiceNow (built and tested on a Personal Developer Instance)
- Flow Designer (Process Automation)
- A custom table (`Incident WorkFlow`) with dependent choice fields
- Native email notifications via Flow Designer's Send Email action

## Setup

Import `update_set.xml` (exported at the end of the Documentation phase) into a ServiceNow instance, confirm the `Incident WorkFlow` table and its dependency config came through, and check that the `Auto Classify School IT Tickets` flow is active. Full steps are in `7. Project Documentation Phase.md`.
