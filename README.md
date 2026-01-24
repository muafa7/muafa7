# Collab Sync Backend

A backend system enabling real-time multi-user document collaboration with conflict resolution, RBAC authorization, presence tracking, and audit/event logs.

Built in TypeScript on Node.js, using WebSockets, PostgreSQL, and Redis for distributed state, consistency, and performance.

---

## ✨ Features

- Real-time collaboration via WebSockets
- Server-authoritative conflict resolution
- Multi-user presence & cursor tracking
- Role-based access control (RBAC)
- JWT authentication + refresh tokens
- Audit/event logging for document history
- Snapshot + version retrieval
- Metrics endpoint for system introspection
- Structured domain modules for maintainability

---

## 🧩 Architecture Overview

Core concepts:

- Server authoritative model (prevents race conditions)
- RBAC governs document-level permissions
- Redis holds ephemeral state (presence, cursors)
- PostgreSQL persists snapshots + events
- Audit log ensures compliance & traceability

Patch flow:
CLIENT → PATCH → SERVER → VALIDATE → RESOLVE → COMMIT → BROADCAST → CLIENTS

---

## 📦 Tech Stack

Language: TypeScript  
Runtime: Node.js  
Transport: WebSockets  
Auth: JWT + Refresh Tokens  
Access Control: RBAC  
Database: PostgreSQL  
Cache / Presence: Redis  
Observability: Metrics endpoint  
Containerization: Docker (optional)

---

## 🗂 Domain Modules

auth — JWT + session lifecycle  
rbac — role + permission policies  
documents — snapshots + version history  
collab — collaborative state + conflict resolution  
presence — online users + cursor tracking  
metrics — system introspection / Prometheus export

---

## 🧱 Conflict Resolution

Supported strategies:

- Server-ordered patches (default)
- Operational Transform (optional)
- CRDT (stretch goal)

Shows knowledge of distributed consistency challenges.

---

## 🔐 Authorization (RBAC)

Roles:
- viewer → read
- editor → read/write
- owner → admin

Policy enforced at:
- socket connection
- read/write operations
- snapshot/history queries

---

## 📊 Observability

Metrics exported via HTTP endpoint: GET /metrics

Example counters:
- connections_active
- events_per_second
- avg_patch_latency_ms
- document_conflicts_total
- connected_users

Critical for production-grade real-time systems.

---

## 🗄 Persistence Model

Document table (human readable):
  documents(id, owner_id, content_snapshot, updated_at)

Event log (append-only):
  events(id, document_id, user_id, type, payload, ts)

Permissions table:
  permissions(user_id, document_id, role)

---

## 🚀 Running Locally

Requirements:
- Node >= 18
- PostgreSQL
- Redis
- Docker (optional)

Run via Docker:
  docker-compose up -d
  npm install
  npm run dev

---

## 🧪 Testing

Run tests:
  npm test

Coverage targets:
- conflict resolution
- RBAC enforcement
- document access
- metrics instrumentation

---

## 📦 Deployment

Targets compatible:
- Railway
- Fly.io
- Render
- AWS ECS (stretch)

Optimized for low-latency workloads.

---

## 📍 Future Enhancements

Planned:
- CRDT offline mode
- comment/annotations
- link-based sharing tokens
- CRON snapshot compaction
- diff compression
- multi-document presence

---

## 🎯 Purpose

Real-time collaboration is hard due to:
- distributed state
- concurrency
- permissions
- consistency
- performance

This backend demonstrates production-level backend problem solving relevant to startups in:
- collaboration
- workflow
- devtools
- productivity
- security/auth

---

## 🏷 License

MIT
