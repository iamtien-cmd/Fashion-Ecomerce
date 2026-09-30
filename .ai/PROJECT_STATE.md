# Project State

## Last Updated

2026-09-30

## Project

Fashion E-Commerce Platform

## Current Phase

Phase 0 — Project Specification

## Completed

* AI rule hierarchy created
* `AGENTS.md` created
* Global project rules created
* Backend rules created
* Frontend rules created
* Task workflow created

## Current Task

Prepare project specification and architecture.

## Architecture Decisions

* Modular monolith
* Java 21
* Spring Boot 3
* React + TypeScript
* PostgreSQL
* Redis
* Docker

## Important Domain Decisions

* Product and ProductVariant are separate.
* Inventory belongs to ProductVariant.
* OrderItem stores price snapshot.
* Order address is stored as a snapshot.
* Backend is authoritative for price, stock, and order totals.

## Known Issues

None.

## Do Not Change Without Approval

* Overall architecture
* Authentication architecture
* Database strategy
* API versioning strategy
