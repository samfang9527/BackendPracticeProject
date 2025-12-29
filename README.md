# OpsBoard — Backend Interview Preparation Project

OpsBoard 是一個為 **Mid–Senior Backend Software Engineer** 設計的實戰導向專案。  
此專案以 **同一套系統設計**，分別實作於：

- **C# / .NET**
- **TypeScript / Node.js (NestJS)**

目標不是做完整產品，而是系統性覆蓋 **後端工程師在面試中一定會被問到的設計、實作與 trade-off**。

---

## 🎯 專案目標

- 練習 **Production-ready Backend Architecture**
- 建立可在面試中清楚說明的：
  - API Design
  - DDD + CQRS 架構
  - Database & Data Access Layer
  - Middleware / Rate Limit / Auth
  - Async processing & consistency
  - Testing / CI / Docker
- 將「實務經驗」轉化為「面試可表達能力」

---

## 🧱 系統概述

### Domain
**OpsBoard** 是一個簡化的任務管理與非同步通知平台。

核心概念：
- Task lifecycle（狀態轉移）
- Idempotent command
- Query 與 Command 分離
- Outbox pattern（可靠非同步）
- Rate limit 與 API Key authentication

---

## 📐 架構概覽

### 分層架構（兩套實作遵守相同概念）
API Layer
↓
Application Layer (CQRS)
↓
Domain Layer
↓
Infrastructure Layer

- **API**：HTTP、Auth、Rate limit、Error handling
- **Application**：Command / Query orchestration
- **Domain**：純 business rule，不依賴 framework
- **Infrastructure**：DB、Queue、External service

---

## 🧭 訓練週期（12 週總覽）

- **Phase 1–2**：實作與打底（Week 1–4）
- **Phase 3**：補齊難點並開始面試（Week 5–8）
- **Phase 4**：面試主戰期（Week 9–12）

此 README 聚焦於 **Phase 1–2（前兩週）** 的實作訓練計畫。

---

# Phase 1 — 基礎架構與垂直切片（Week 1）

### 🎯 目標
建立完整可運作的 backend 基礎，並完成第一條 production-grade vertical slice。

---

### ✅ Checklist

#### Project Setup
- [ ] 建立 .NET solution（Api / Application / Domain / Infrastructure）
- [ ] 建立 NestJS 專案（module-based structure）
- [ ] Docker Compose（App + PostgreSQL）
- [ ] Health check endpoint

#### Database & Schema
- [ ] 設計 `tasks` table（含 status、idempotency key、version）
- [ ] 設計 `outbox_events` table
- [ ] Migration 機制（EF Core / Prisma）
- [ ] Index 與 unique constraint 設計

#### Domain Layer
- [ ] Task aggregate（狀態轉移邏輯）
- [ ] Domain error 定義
- [ ] Domain unit tests

#### CQRS — Command
- [ ] CreateTaskCommand
- [ ] Idempotency 機制
- [ ] Transaction handling
- [ ] REST API（POST /api/v1/tasks）

#### Middleware
- [ ] Global error handling（一致錯誤格式）
- [ ] Request ID middleware
- [ ] Logging（含 latency）

#### Query
- [ ] ListTasks query
- [ ] Cursor-based pagination
- [ ] Filter / sorting
- [ ] 對應 DB index 驗證

#### 面試重點實驗
- [ ] 解釋 DDD 分層的責任與依賴方向
- [ ] 解釋 idempotency 與重送處理
- [ ] 解釋 cursor vs offset pagination trade-off

---

# Phase 2 — Concurrency、Infrastructure 與 DevOps（Week 2）

### 🎯 目標
補齊外商面試最常問的「難點」：一致性、非同步、效能與工程實務。

---

### ✅ Checklist

#### Concurrency Control
- [ ] StartTask / CompleteTask command
- [ ] Optimistic concurrency control
- [ ] 409 Conflict handling
- [ ] Concurrency unit tests

#### Rate Limiting
- [ ] Rate limit middleware / interceptor
- [ ] Memory-based implementation
- [ ] Redis-based interface（可 stub）
- [ ] Rate limit exceed response 設計

#### Authentication & DI
- [ ] API Key authentication（middleware）
- [ ] User context propagation
- [ ] DI lifetime 設計（Scoped vs Singleton）
- [ ] 故意示範 DI misuse 並修正

#### Async Processing（Outbox）
- [ ] 寫入 outbox_event
- [ ] Background worker（polling）
- [ ] At-least-once delivery
- [ ] Idempotent consumer 設計

#### Testing Strategy
- [ ] Domain tests
- [ ] Application handler tests
- [ ] API contract tests
- [ ] 測試 scope 與 ROI 說明

#### Docker & Configuration
- [ ] Multi-stage Dockerfile
- [ ] docker-compose 一鍵啟動
- [ ] Environment-based config

#### CI/CD
- [ ] GitHub Actions pipeline
- [ ] Lint / Test / Build
- [ ] Docker image build
- [ ] Quality gate 設計

#### 面試重點實驗
- [ ] 樂觀鎖 vs 悲觀鎖
- [ ] Rate limit 在分散式環境的問題
- [ ] Outbox pattern 的必要性
- [ ] CI 中如何避免 flaky test

---

## 📌 使用方式（學習建議）

- 每個 checklist 項目都必須：
  1. 實作
  2. 寫至少一個測試
  3. 能用 2–3 分鐘口述設計與 trade-off
- 每天固定搭配 LeetCode（1 Medium + 1 Easy）

---

## 🧠 最終成果（面試可用）

完成 Phase 1–2 後，你將擁有：
- 兩套可 demo 的 backend 專案（.NET + NestJS）
- 可清楚說明的系統設計與實作取捨
- 足以應付 Backend 面試的實戰素材
