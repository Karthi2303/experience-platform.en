---
title: Data Governance overview
seo-title: Data Governance in Real-time Customer Data Platform
description: Data Governance allows you to manage customer data and ensure compliance with regulations, restrictions, and policies applicable to data use. 
seo-description: Data Governance allows you to manage customer data and ensure compliance with regulations, restrictions, and policies applicable to data use. 
---

# Data Governance in Real-time CDP

Real-time Customer Data Platform (Real-time CDP) brings data from multiple enterprise systems together, allowing marketers to better identify, understand, and engage their customers. This data may be subject to usage restrictions defined by your organization or by legal regulations. Therefore, it is important to ensure that Real-time CDP is compliant with usage policies when handling your data.

Adobe Experience Platform Data Governance allows you to manage customer data and ensure compliance with regulations, restrictions, and policies applicable to data use. It plays a key role within Real-time CDP, allowing you to define usage policies, categorize your data based on those policies, and check for policy violations when performing certain marketing actions.

Real-time CDP is built on top of Adobe Experience Platform, and therefore the majority of Data Governance capabilities are covered in the Experience Platform documentation. This document is intended to complement the [Data Governance overview](../../data-governance/home.md) for Experience Platform, and outlines the Governance features that are available in Real-time CDP. The following topics are covered:

* [Apply usage labels to your data](#labels)
* [Manage data usage policies](#policies)
* [Enforce data usage compliance](#enforcement)

## Apply usage labels to your data {#labels}

Data Governance allows you to apply usage labels to your data, either at the dataset or dataset-field level. Data usage labels allow you to categorize data according to usage policies that apply to that data. 

For detailed information on working with data usage labels, see the [data usage labels user guide](../../data-governance/labels/overview.md) for Adobe Experience Platform.

## Set restrictions on destinations

You can set data usage restrictions on a destination by defining marketing use cases for that destination. Defining use cases for destinations allows you to check for usage policy violations and ensure that any profiles or segments sent to that destination are compatible with Data Governance rules.

Marketing use cases can be defined during the _Setup_ phase for the _Edit Destination_ workflow. See the destination documentation for more information. 


## Manage data usage policies {#policies}

In order for data usage labels to effectively support data compliance, data usage policies must be defined and enabled. Data usage policies are rules that describe the kinds of marketing actions that you are allowed to, or restricted from, performing on data within Real-time CDP. See the "Data usage policies" section in the Experience Platform [Data Governance overview](../../data-governance/home.md) for more information.

Adobe Experience Platform provides several **core policies** for common customer experience use cases. These policies can be viewed by making a request to the [DULE Policy Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml), as shown in the "List all policies" section in the [Policy Service developer guide](../../data-governance/policies/overview.md). You can also create your own **custom policies** to model custom usage restrictions, as shown in the "Create a policy" section in the developer guide.

## (Beta) Enforce data usage compliance {#enforce-data-usage-compliance}

>[!IMPORTANT]
>This feature is currently in beta and is not available to all users. It can be enabled upon request. The documentation and the functionality are subject to change.

Once data is labeled and usage policies are defined, you can enforce data usage compliance with policies. When activating audience segments to destinations in Real-time CDP, Data Governance automatically enforces usage policies should any violations occur.

The following diagram illustrates how policy enforcement is integrated into the data flow of segment activation:

![](assets/enforcement-flow.png)

When a segment is first activated, DULE Policy Service checks for policy violations based on the following factors:

* The data usage labels applied to fields and datasets within the segment to be activated.
* The marketing purpose of the destination. 

### Policy violation messages {#enforcement}

If a policy violation occurs from attempting to activate a segment (or [making edits to an already activated segment](#policy-enforcement-for-activated-segments)) the action is prevented and a popover appears indicating that one or more policies have been violated. Select a policy violation in the popover's left column to display details for that violation.

![](assets/violation-popover.png)

The popover's *Details* tab indicates the action that triggered the violation the reason why the violation occurred, and provides suggestions for how to potentially resolve the issue.

Click **Data Lineage** to track the destinations, segments, merge policies, or datasets whose data label(s) triggered the violation.

![](assets/data-lineage.png)

Once a violation has triggered, the **Save** button is disabled for the activation until the appropriate components are updated to comply with data usage policies.

### Policy enforcement for activated segments {#policy-enforcement-for-activated-segments}

Policy enforcement still applies to segments after they have been activated, restricting any changes to a segment or its destination that would result in a policy violation. Due to the numerous components involved in activating segments to destinations, any of the following actions can potentially trigger a violation:

* Updating data usage labels
* Changing datasets for a segment
* Changing segment predicates
* Changing destination configurations

If any of the above actions triggers a violation, that action is prevented from being saved and a policy violation message is displayed, ensuring that your activated segments continue to comply with data usage policies when being modified.

## Next steps

Now that you have been introduced to the key Data Governance features on Real-time CDP and how Experience Platform enables them, please continue to the [documentation for Data Governance on Adobe Experience Platform](../../data-governance/home.md). The documentation provides overviews of essential Data Governance concepts, as well as step-by-step workflows for managing data usage labels and policies.

The following video provides an overview of Data Governance in Real-time CDP, including the use of marketing use-cases on destinations and example workflows for different scenarios:

>[!VIDEO](https://video.tv.adobe.com/v/33631?quality=12&learn=on)