# ADR-001: Python/FastAPI modular monolith with SQLite and a JSON API

Status: Accepted
Date: 20/10/2026

## Context
We need a prototype that runs locally, is easy to test, and that all three members can explain in an oral defense. The team has a free model only, so simple and widely documented technology reduces generated-code errors.

## Decision
A single Python 3.11+ application: FastAPI for the JSON API, SQLAlchemy with SQLite for data, pytest for tests, and a small static HTML/JS front end served by the same app. Code is layered: routers, services, policy module, data access.

## Alternatives considered
| Option | Why not chosen |
|---|---|
| Django (full stack) | Powerful but heavy; much generated and hidden behaviour that is hard to defend line by line |
| Node/Express + React | Two toolchains and more moving parts than a 3-person team needs for a core workflow |
| Server-rendered pages only (no JSON API) | Harder to test authorization at API level and gives no clear API contract for IT review |
| Microservices | Unjustified complexity for this scope |
| PostgreSQL | Needs a separate server. Not needed for local deployment. SQLite via SQLAlchemy keeps a later move possible |

## Consequences
- (+) One command to run, one command to test, easy API-level authorization tests.
- (+) Clear contract for PSU IT review.
- (-) SQLite has limited concurrency. Capacity and duplicate rules must rely on constraints and transactions, and must be tested.
- (-) Vanilla JS front end needs care for accessibility. We accept a plain UI.
