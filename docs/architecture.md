# GearCairn — proposed AWS architecture

GearCairn uses AWS to bring together equipment histories and live usage data, forecast servicing needs and serve plans to maintenance teams — securely per plant.

## Request flow

1. Work orders & sensors
2. AWS IoT Core
3. Amazon S3
4. AWS Lambda
5. SageMaker AI
6. DynamoDB
7. Planner approval

## Services

### Amazon SageMaker AI

**Role:** Forecast servicing needs

Trains reliability models on service intervals, failure history and utilisation to forecast each asset’s next service window with a confidence range.

### AWS IoT Core

**Role:** Collect runtime and cycles

Receives runtime hours, cycle counts and condition readings from plant sensors and gateways over secure, certificate-based connections.

### Amazon S3

**Role:** Store equipment histories

Keeps imported work orders, job cards and raw sensor data encrypted and versioned as the long-term record for every asset.

### Amazon DynamoDB

**Role:** Serve assets, forecasts and plans

Holds asset registers, linked service events, forecasts and approved schedules for fast access in the maintenance workspace.

### AWS Lambda

**Role:** Clean, link and schedule

Normalises imported records, aggregates sensor data per shift, and generates proposed schedules whenever forecasts change.

## Principles

- **Read-only on the plant** — We never send commands to equipment.
- **Approved data only** — Forecasts use histories your team has approved.
- **Explained schedules** — Every proposed service shows the evidence behind it.

## Safeguards

- **Planners decide** — Schedules are proposals until a maintenance planner approves them.
- **No machine control** — GearCairn reads data only. It never starts, stops or adjusts equipment.
- **Safety stays with you** — Statutory inspections and safety-critical checks follow your existing procedures.
- **Plant data protected** — Encrypted, access-controlled and isolated per plant.

## MVP scope

We import two to five years of approved service history for a group of critical assets, add usage data where available, and deliver weekly service forecasts and a proposed schedule your planners review.

- Work order and job card import
- Asset history per machine
- Service forecasts
- Recurring issue report
- Proposed weekly schedule
