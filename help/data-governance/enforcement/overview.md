---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Policy enforcement overview
topic: enforcement
---

# Policy enforcement overview

Once data usage labels have been applied to Platform datasets, and data usage policies have been defined for marketing actions against those labels, Data Governance capabilities allow you to enforce those policies and prevent data operations that constitute policy violations.

There are two methods of policy enforcement provided by Data Governance features on Platform: **API-based enforcement** and **automatic enforcement**.

## API-based enforcement

The Policy Service API provides endpoints that allow you to test marketing actions against datasets or arbitrary combinations of data usage labels in order to check if any policy violations occur. Based on the API response, you can then set up protocols within your experience application to appropriately enforce data usage policy compliance.

See the tutorial on [policy enforcement](api-enforcement.md) for steps on how to evaluate policies using the API.

## Automatic enforcement

Certain applications that are built on top of Experience Platform (such as Real-time Customer Data Platform) provide automatic enforcement for data usage policies. Each application maintains its own method of surfacing policy violations and providing steps for resolving issues. 

Please consult the documentation for the Platform-based application you are using for more information on automatic data usage policy enforcement. For information on automatic policy enforcement in Real-time CDP, please refer to the [Real-time CDP Data Governance overview](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance).