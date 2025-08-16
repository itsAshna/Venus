---
layout: page
title: Alertron
description: An anomaly detection system using Kafka, Prometheus, Grafana and Slack.
img: assets/img/3.png
importance: 3
---
**GitHub Repository:** [View on GitHub](https://github.com/itsAshna/Alertron)

---

#### Introduction
I built a real-time anomaly-detection pipeline that ingests streaming IoT-style data, scores each event with an ML model, exports rich Prometheus metrics, raises automated Slack alerts when the fleet goes off‑nominal, and visualizes the system in Grafana. It’s a compact, hands‑on MLOps project that shows how to take a model from a notebook to a production‑like, observable service.

#### Problem
Detect anomalous device behavior across a fleet **as it happens**, not hours later. The system needed to:
- handle a continuous stream of readings,
- score each event with low latency,
- expose **operational** metrics (throughput, latency, errors),
- raise a **reliable alert** when anomaly volume spikes,
- be easy to run locally and share.

#### Approach
**Pipeline**
```
IoT generator → Kafka ("readings")
                   ↓
        FastAPI inference service (aiokafka)
           • Isolation Forest scoring
           • Severity via score quantiles (low/medium/high)
           • Prometheus metrics (/metrics)
                   ↓
      Prometheus → Alert rules → Alertmanager → Slack
                   ↓
                        Grafana dashboards
```

**Key tech**
- **Kafka (Redpanda)** for the stream (`readings`, optional `anomalies` topic).
- **FastAPI** service scoring with **Isolation Forest** (scikit‑learn, joblib).
- **Prometheus** metrics exposed by the service:  
  `anomaly_count_total{device_id,severity}`, `last_anomaly_score{device_id}`,  
  `inference_latency_seconds_bucket/_sum/_count`, `predictions_total`,  
  `kafka_messages_consumed_total{topic}`, `kafka_errors_total`.
- **Alerting:** Prometheus rule (e.g., `sum(increase(anomaly_count_total[5m])) > threshold`) → **Alertmanager** → **Slack** (app webhook).
- **Grafana** dashboard for anomalies, throughput, p95 latency, Kafka error %, top devices, and last scores.
- **Docker Compose** for one‑command up; a `topic-init` job ensures topics exist before consumers start.

#### Results
- **Throughput:** ~9–10 predictions/sec on my local run.
- **Latency:** ~24–25 ms **p95** inference latency.
- **Alerting:** `HighAnomalyRate` fires under sustained spikes and delivers to Slack.
- **Reliability:** Kafka error % at **0.00%** during steady state.
- **Observability:** Live panels for anomaly volume (5m), by‑severity trend, top noisy devices, and recent per‑device scores.

#### Key Findings
- **Observability from day 0** changes how you build ML services: latency histograms + rates make bottlenecks obvious.
- **Severity needs calibration:** quantile‑based thresholds (e.g., p80/p95 of scores) give meaningful low/medium/high bands.
- **Alert tuning matters:** use `increase()` over a window and sum across devices; start conservative to avoid Slack spam.
- **Streaming > polling** for scale: Kafka decouples generation from scoring and handles backpressure cleanly.
- **Infra gotchas:** correct Kafka advertised addresses and YAML indentation for Prometheus rules are common pitfalls—document them.

#### What I Solved
- Turned a notebook model into a **real‑time, observable microservice**.
- Built an **end‑to‑end alerting loop** (metrics → rule → Slack) operators can trust.
- Packaged everything with **Docker Compose** so anyone can reproduce the system in minutes.
- Shipped a **Grafana dashboard** and PromQL library that make the service explainable to SREs and PMs, not just ML engineers.

#### Conclusion
This project demonstrates practical **MLOps readiness**: streaming ingestion, low‑latency inference, first‑class metrics, actionable alerts, and clear dashboards. It’s small enough to run locally yet architected like a production system—useful as a template for real deployments.

#### Future Improvements
- **Modeling:** windowed features, autoencoder baseline, concept‑drift detection, periodic retraining.
- **Data/Contracts:** schema registry (Avro/Protobuf), input validation, dead‑letter topic.
- **Ops:** CI/CD with unit + integration tests, canary deploys, blue/green for the service.
- **Platform:** Kubernetes (Prometheus Operator, Alertmanager, Grafana provisioning), Helm charts.
- **Observability+:** OpenTelemetry traces, SLOs + burn‑rate alerts, per‑device alert routing, on‑call runbooks.
- **Security:** TLS between components, secret management, RBAC on dashboards.
