---
title: "Introduction"
weight: 10
---

Financial institutions aiming to modernize their payment infrastructure are increasingly choosing solutions that combine **flexibility**, **modularity**, **cloud-native design**, and **compliance with global standards**. Brillio, in partnership with Payment Components, offers a comprehensive, cloud-enabled, and scalable payment hub — **aplonHUB™** — to help banks and financial institutions efficiently manage and route financial messages across all major payment schemes and standards.

**aplonHUB™** is a lightweight, high-performance messaging hub that enables seamless routing, transformation, and validation of financial messages such as **SWIFT MT**, **ISO 20022**, **SEPA**, **TARGET2**, **FedNow**, and more. Designed for minimal disruption to legacy systems, it supports **instant credit transfers**, **direct debits**, and **cross-border payments** through a centralized, standards-compliant architecture.

![aplonHUB architecture](/static/images/image.png)

Brillio Payment Solution powered by Payment Components empowers banks to decouple complex logic from core banking systems. It simplifies operations through centralized scheduling, compliance integration (e.g., AML systems), message correlation, and alert handling — all within a modern, secure, **cloud-native**, role-based platform. Its single solution provides message transformation, compliance validation, and monitoring across multiple payment rails.

With advanced capabilities such as **MT-to-ISO 20022 translation**, reconciliation views, automated response generation, real-time search, and support for **FBO and virtual accounts**, **aplonHUB™** enhances straight-through processing (STP), increases transparency, and reduces manual errors. **Deployed as containers on AWS EKS** and integrated using **open API interfaces**, the platform offers banks a rapid path to instant payments, global compliance, and readiness for the real-time payment economy.

To further strengthen payment intelligence and operational insights, Brillio integrates **Finaplo.AI** — an AI/ML-powered analytics engine purpose-built for financial messages. Finaplo.AI supports all major A2A schemes such as **SWIFT**, **ISO 20022**, **FedNow**, **SEPA**, **MEPS**, and **TARGET2**, and understands transaction types like credit transfers, direct debits, and instant payments. Unlike generic AI platforms, Finaplo.AI offers **domain-specific intelligence** that enables anomaly detection, insight generation, and efficiency optimization.

Before data is uploaded to Finaplo.AI, banks use an in-house **sanitizer** utility to hash or remove sensitive details (e.g., IBANs, names, addresses). This ensures data privacy and ownership. Finaplo.AI runs in a **dedicated, private, and isolated AWS environment**, maintaining full control and compliance.

Whether routing **FedNow** or **SEPA Instant Payments**, transforming **SWIFT messages to CBPR+**, or applying AI-driven intelligence to financial message flows, Brillio’s solution via Payment Components enables a **unified, secure, and insight-rich experience** across domestic and international payment rails — simplifying compliance, accelerating innovation, and supporting the digital transformation of banking operations.

To simulate a payment transaction, we provide step-by-step documentation and a simple user interface to initiate the process. The UI triggers a cross-border transaction by calling **aplonHUB™** via a REST API. You can then review and manage the submitted transaction through the **aplonHUB Dashboard**.
