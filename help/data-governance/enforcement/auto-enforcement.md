---
keywords: Experience Platform;home;popular topics;Policy enforcement;Automatic enforcement;API-based enforcement;data governance
solution: Experience Platform
title: Automatic Policy Enforcement
topic-legacy: guide
description: This document covers how data usage policies are automatically enforced when activating segments to destinations in Experience Platform.
exl-id: c6695285-77df-48c3-9b4c-ccd226bc3f16
source-git-commit: 679b9eb621baff99342fb55c0a13a60f5ef256bd
workflow-type: tm+mt
source-wordcount: '1702'
ht-degree: 0%

---

# Automatic policy enforcement

Once data is labeled and usage policies are defined, you can enforce data usage compliance with policies. When activating audience segments to destinations, Adobe Experience Platform automatically enforces usage policies should any violations occur.

## Prerequisiti

This guide requires a working understanding of the Platform services involved in automatic enforcement. Please refer to the following documentation to learn more before continuing with this guide:

* [](../home.md)
* [](../../profile/home.md)
* [](../../segmentation/home.md)[!DNL Platform]
* [](../../destinations/home.md)

## Enforcement flow {#flow}

The following diagram illustrates how policy enforcement is integrated into the data flow of segment activation:

![](../images/enforcement/enforcement-flow.png)

[!DNL Policy Service]

* The data usage labels applied to fields and datasets within the segment to be activated.
* The marketing purpose of the destination.
* (Beta) The profiles that have consented to be included in the segment activation, based on your configured consent policies.

>[!NOTE]
>
>If there are data usage labels that have only been applied to certain fields within a dataset (rather than the entire dataset), enforcement of those field-level labels on activation only occurs under the following conditions:
>
>* The fields are used in the segment definition.
>* The fields are configured as projected attributes for the target destination.


## Data lineage {#lineage}

Data lineage plays a key role in how policies are enforced in Platform. In general terms, data lineage refers to the origin of a set of data, and what happens to it (or where it moves) over time.

In the context of Data Governance, lineage enables data usage labels to propagate from datasets to downstream services that consume their data, such as Real-time Customer Profile and destinations. This allows policies to be evaluated and enforced at several key points in the data&#39;s journey through Platform, and provides context to data consumers as to why a policy violation occurred.

In Experience Platform, policy enforcement is concerned with the following lineage:

1. ****
1. ****
1. ****
1. ****

Each stage in the above timeline represents an entity that may contribute to policy enforcement, as outlined in the table below:

| Data lineage stage | Role in policy enforcement |
| --- | --- |
| Set di dati | Datasets contain data usage labels (applied at the dataset or field level) that define which use cases the entire dataset or specific fields can be used for. Policy violations will occur if a dataset or field containing certain labels is used for a purpose that a policy restricts.<br><br> If you have access to consent policies (currently in beta), any profiles that do not meet the consent attribute requirements of your policies will be excluded from segments that are activated to a destination. |
| Merge policy | Merge policies are the rules that Platform uses to determine how data will be prioritized when merging together fragments from multiple datasets. Policy violations will occur if your merge policies are configured so that datasets with restricted labels are activated to a destination. [](../../profile/merge-policies/overview.md) |
| Segmento | Segment rules define which attributes should be included from customer profiles. Depending on which fields a segment definition includes, the segment will inherit any applied usage labels for those fields. Policy violations will occur if you activate a segment whose inherited labels are restricted by the target destination&#39;s applicable policies, based on its marketing use case. |
| Destinazione | When setting up a destination, a marketing action (sometimes called a marketing use case) can be defined. This use case correlates to a marketing action as defined in a policy. In other words, the marketing action you define for a destination determines which data usage policies and consent policies are applicable to that destination.<br><br><br><br> |

>[!IMPORTANT]
>
>Some data usage policies may specify two or more labels with an AND relationship. `C1``C2`
>
>When it comes to automatic enforcement, the Data Governance framework does not consider the activation of separate segments to a destination as a combination of data. `C1 AND C2`**** Instead, this policy is only enforced when both labels are present in the same segment upon activation.

When policy violations occur, the resulting messages that appear in the UI provide useful tools for exploring the violation&#39;s contributing data lineage to help resolve the issue. More details are provided in the next section.

## Policy enforcement messages {#enforcement}

The sections below outline the different policy enforcement messages that appear in the Platform UI:

* [Data usage policy violation](#data-usage-violation)
* [Consent policy evaluation](#consent-policy-evaluation)

### Data usage policy violation {#data-usage-violation}

[](#policy-enforcement-for-activated-segments) ****

Select a policy violation in the popover&#39;s left column to display details for that violation.

![](../images/enforcement/violation-policy-select.png)

The violation message provides a summary of the policy that was violated, including the conditions the policy is configured to check for, the specific action that triggered the violation, and a list of possible resolutions for the issue.

![](../images/enforcement/violation-summary.png)

A data lineage graph is displayed below the violation summary, allowing you to visualize which datasets, merge policies, segments, and destinations were involved in the policy violation. The entity that you are currently changing is highlighted in the graph, indicating which point in the flow is causing the violation to occur. You can select an entity name within the graph to open the details page for the entity in question.

![](../images/enforcement/data-lineage.png)

****![](../images/enforcement/filter.png) At least two categories must be selected in order for data to be displayed.

![](../images/enforcement/lineage-filter.png)

**** ****

![](../images/enforcement/list-view.png)

### Consent policy evaluation (Beta) {#consent-policy-evaluation}

>[!IMPORTANT]
>
>Consent policies are currently in beta and your organization may not have access to them yet.

[](../policies/user-guide.md#consent-policy)

#### Pre-activation evaluation

****[](../../destinations/ui/activation-overview.md)****

![](../images/enforcement/view-applied-policies.png)

A policy check dialog appears, showing you a preview of how your consent policies affect the consented audience of the activated segments.

![](../images/enforcement/consent-policy-check.png)

The dialog shows the consented audience for one segment at a time. To view the policy evaluation for a different segment, use the dropdown menu above the diagram to select one from the list.

![](../images/enforcement/segment-switcher.png)

Use the left rail to switch between the applicable consent policies for the selected segment. 

![](../images/enforcement/policy-switcher.png)

The diagram displays the overlap between three groups of profiles:

1. Profiles that qualify for the selected segment
1. Profiles that qualify for the selected consent policy
1. 

The profiles that qualify for all three of the above groups represent the consented audience for the selected segment, summarized in the right rail.

![](../images/enforcement/summary.png)

Hover over one of the audiences in the diagram to show the number of profiles it contains.

![](../images/enforcement/highlight-segment.png)

The consented audience is represented by the central overlap of the diagram, and can be highlighted like the other sections.

![](../images/enforcement/consented-audience.png)

#### Flow run enforcement

When data is activated to a destination, the flow run details show the number of identities that were excluded due to active consent policies.

![](../images/enforcement/dataflow-run-enforcement.png)

## Policy enforcement for activated segments {#policy-enforcement-for-activated-segments}

Policy enforcement still applies to segments after they have been activated, restricting any changes to a segment or its destination that would result in a policy violation. [](#lineage)

* Updating data usage labels
* Changing datasets for a segment
* Changing segment predicates
* Changing destination configurations

If any of the above actions triggers a violation, that action is prevented from being saved and a policy violation message is displayed, ensuring that your activated segments continue to comply with data usage policies when being modified.

## Passaggi successivi

This document covered how automatic policy enforcement works in Experience Platform. [](./api-enforcement.md)
