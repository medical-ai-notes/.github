# CuraConnect

> **AI-Native EMR Platform** — Reducing clinician burnout through ambient scribing and automated patient communication

[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.x-blue)](https://www.typescriptlang.org/)
[![NestJS](https://img.shields.io/badge/NestJS-10.x-red)](https://nestjs.com/)
[![Next.js](https://img.shields.io/badge/Next.js-14.x-black)](https://nextjs.org/)

---

## 🎯 Mission

CuraConnect is building the next generation of Electronic Medical Records (EMR) that eliminates manual note-taking through AI-powered ambient scribing, automates patient communication, and ensures healthcare providers can focus on what matters most — patient care.

---

## ✨ What We're Building

### Core Features (MVP)

- **🎙️ Ambient AI Scribing** — Real-time transcription during patient consultations with zero manual note-taking
- **📋 Automated Clinical Documentation** — AI-generated structured notes (SOAP, H&P, referral letters) with clinician review
- **💊 Smart Prescription & Lab Orders** — Automatic extraction from conversations with digital delivery
- **📱 Multi-Channel Patient Notifications** — SMS, Email, WhatsApp delivery with QR code verification
- **🏥 Multi-Tenant Architecture** — Isolated data per clinic/hospital with custom branding
- **🔒 Compliance-Ready Security** — HIPAA/DPDP 2023 inspired controls, SOC2/ISO 27001-ready
- **📊 Admin Dashboards** — Real-time metrics, audit logs, and system health monitoring
- **⚡ Enterprise Scale** — Built for 2,000+ concurrent users with auto-scaling infrastructure

### Post-MVP Roadmap

- Customizable clinical note templates and workflows
- Template marketplace for specialty-specific forms
- Advanced clinical analytics and AI-driven decision support
- National registry integration (NHIR, ABDM, NABIDH, NEHR)
- Multi-specialty support with regional accent recognition
- Formal security certifications

---

## 🏗️ Architecture

**Pattern**: Event-Driven Modular Monolith (with zero-code microservices extraction path)

```
┌─────────────────────────────────────────────────────────────┐
│                     Client Applications                      │
│  Next.js Web App  │  React Native Mobile  │  Public API     │
└────────────┬──────────────────┬───────────────────┬─────────┘
             │                  │                   │
        ┌────▼──────────────────▼───────────────────▼────┐
        │         NestJS API Server (GraphQL + REST)     │
        │  ┌──────────┬──────────┬──────────┬─────────┐ │
        │  │ Patient  │ Clinical │  Orders  │  Admin  │ │
        │  │  Module  │  Module  │  Module  │ Module  │ │
        │  └──────────┴──────────┴──────────┴─────────┘ │
        └────────────────────┬───────────────────────────┘
                             │
                    ┌────────▼─────────┐
                    │  AWS EventBridge │ ◄─── Event-Driven Communication
                    └────────┬─────────┘
                             │
        ┌────────────────────┼────────────────────┐
        │                    │                    │
   ┌────▼────┐        ┌──────▼──────┐    ┌───────▼────────┐
   │Notification│      │ Extraction  │    │Future Workers│
   │  Worker    │      │   Worker    │    │              │
   └─────────────┘     └─────────────┘    └──────────────┘
```
**Key Design Decisions**:
- **Nx Monorepo** — Fast MVP development with shared libraries
- **Event-Driven** — All inter-module communication via EventBridge (enables future microservices)
- **PostgreSQL RLS** — Database-first multi-tenancy with row-level security
- **Zero Audio Storage** — Real-time streaming to AWS HealthScribe, transcriptions only
- **Single Docker Image** — Same image for API and workers (environment-controlled behavior)

---

## 🛠️ Technology Stack

| Layer | Technology |
|-------|-----------|
| **Frontend** | Next.js, React Native + Expo, Tailwind CSS |
| **API** | NestJS, GraphQL (Apollo), REST, WebSocket |
| **State** | React Query, Zustand, Apollo Client |
| **Monorepo** | Nx |
| **Database** | PostgreSQL (RDS), DynamoDB |
| **Cache** | Redis (ElastiCache) |
| **Storage** | AWS S3 |
| **Auth** | AWS Cognito + JWT |
| **Events** | AWS EventBridge + SQS |
| **Transcription** | AWS HealthScribe / Deepgram |
| **Notifications** | Amazon SNS, WhatsApp Cloud API |
| **Orchestration** | Kubernetes (EKS) |
| **Monitoring** | AWS CloudWatch |
| **Testing** | Jest, Supertest, Playwright, Detox |

---

## 📦 Repository Structure

```
curaconnect-platform/           # Main application monorepo
├── apps/
│   ├── api/                    # NestJS API server
│   ├── web/                    # Next.js web application
│   ├── mobile/                 # React Native mobile app
│   ├── notification.worker/    # Background notification worker
│   └── extraction.worker/      # AI extraction worker
│
├── libs/
│   ├── database/               # PostgreSQL + DynamoDB access
│   ├── eventbridge/            # Event publishing/consuming
│   ├── auth/                   # Authentication & RBAC
│   ├── logging/                # Structured logging & audit
│   ├── notifications/          # Multi-channel delivery
│   └── ui/                     # Shared UI components

platform-build-docs/            # Comprehensive documentation
├── CuraConnect.md              # Feature specifications
├── CuraConnect_Architecture.md # System design
└── CuraConnect_TechSpec.md     # Technical implementation details
```
---

## 🚀 Key Differentiators

1. **Event-Driven from Day 1** — Built for microservices extraction with zero code changes
2. **Real-Time AI Scribing** — No audio storage, direct streaming to transcription services
3. **Database-First Multi-Tenancy** — PostgreSQL RLS ensures complete data isolation
4. **External Verification** — Public QR code API for pharmacies/labs (no login required)
5. **Production-Ready Security** — 7-year audit logging, encryption at rest/transit, RBAC
6. **True Auto-Scaling** — Kubernetes with HPA for API pods and queue-based worker scaling

---

## 🔒 Security & Compliance

- **Authentication**: AWS Cognito with OAuth2
- **Authorization**: Role-based access control (RBAC)
- **Encryption**: TLS 1.3 in-transit, AWS KMS + AES-256 at-rest
- **Multi-Tenancy**: PostgreSQL Row-Level Security
- **Audit Logging**: 7-year retention, append-only
- **Data Privacy**: HIPAA/DPDP 2023 inspired controls
- **Patient Consent**: Explicit workflow for recording permissions
- **Certifications**: SOC2/ISO 27001-ready documentation

---

## 📈 Scale & Performance

- **Concurrent Users**: 2,000+ with auto-scaling
- **API Response Time**: Sub-second (p95 <100ms)
- **Availability**: Multi-AZ deployment with <2 min failover
- **Backup**: Daily automated backups (7-day retention)
- **Recovery**: RPO <24 hours, RTO <1 hour
- **Testing**: 80% code coverage target

---

## 🌍 Regional Support

**Current**: India, UAE, Singapore (English)  
**Planned**: Multi-specialty support with regional accents and local compliance requirements

---

## 📚 Documentation

Comprehensive technical documentation available:

- **[Feature Specifications](platform-build-docs/CuraConnect.md)** — Complete MVP and post-MVP features
- **[Architecture Guide](platform-build-docs/CuraConnect_Architecture.md)** — System design and technical decisions
- **[Technical Specs](platform-build-docs/CuraConnect_TechSpec.md)** — Implementation details and code patterns

---

## 🤝 Contributing

We're building CuraConnect to transform healthcare delivery. Interested in contributing? Check out our repositories and documentation.

---

## 📄 License

[Specify your license]

---

## 🔗 Links

- **Website**: [curaconnect.health](#)
- **Documentation**: [docs.curaconnect.health](#)
- **Support**: support@curaconnect.health

---

**Built with ❤️ for healthcare providers worldwide**
