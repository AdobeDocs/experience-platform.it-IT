---
keywords: Experience Platform;home;popular topics;data governance;data usage policy user guide
solution: Experience Platform
title: Manage Data Usage Policies in the UI
topic-legacy: policies
description: Adobe Experience Platform Data Governance provides a user interface that allows you to create and manage data usage policies. This document provides an overview of the actions that you can perform in the Policies workspace in the Experience Platform user interface.
exl-id: 29434dc1-02c2-4267-a1f1-9f73833e76a0
source-git-commit: 1c0685e7acb594829795674f859f76f229ecee61
workflow-type: tm+mt
source-wordcount: '1331'
ht-degree: 0%

---

# Manage data usage policies in the UI

Adobe Experience Platform Data Governance provides a user interface that allows you to create and manage data usage policies. ****[!DNL Experience Platform]

>[!IMPORTANT]
>
>All data usage policies (including core policies provided by Adobe) are disabled by default. In order for an individual policy to be considered for enforcement, you must manually enable that policy. [](#enable)

## Prerequisiti

[!DNL Experience Platform]

* [Governance dei dati](../home.md)
* [Data usage policies](./overview.md)

## View existing policies {#view-policies}

[!DNL Experience Platform]******** ****

![](../images/policies/browse-policies.png)

****

![](../images/policies/consent-policy-toggle.png)

Select a listed policy to view its description and type. [](#enable)

![](../images/policies/policy-details.png)

## Create a custom policy {#create-policy}

************

![](../images/policies/create-policy-button.png)

Depending on whether you are part of the beta for consent policies, one of the following occurs:

* [](#create-governance-policy)
* [](#consent-policy)
   ![](../images/policies/choose-policy-type.png)

### Create a data governance policy {#create-governance-policy}

**** Start by providing a name and a description for the new policy.

![](../images/policies/create-policy-description.png)

Next, select the data usage labels that the policy will be based on. When selecting multiple labels, you are given the option to choose whether the data should contain all the labels or just one of them in order for the policy to apply. ****

![](../images/policies/add-labels.png)

**** ****

>[!NOTE]
>
>When selecting multiple marketing actions, the policy interprets them as an &quot;OR&quot; rule. ****

![](../images/policies/add-marketing-actions.png)

**** ****

![](../images/policies/policy-review.png)

**** To enable the policy, see the next section.

![](../images/policies/created-policy.png)

### Create a consent policy (Beta) {#consent-policy}

>[!IMPORTANT]
>
>Consent policies are currently in beta and your organization may not have access to them yet.

If you chose to create a consent policy, a new screen appears that allows you to configure the new policy.

![](../images/policies/consent-policy-dialog.png)

In order to make use of consent policies, you must have consent attributes present in your profile data. [](../../landing/governance-privacy-security/consent/adobe/overview.md)

Consent policies are comprised of two logical components:

* **** This can be based on a certain marketing action being performed, the presence of certain data usage labels, or a combination of the two.
* ****

#### Configure conditions

**** ********

****

![](../images/policies/add-condition.png)

If you select more than one condition, you can use the icon that appears between them to switch the conditional relationship between &quot;AND&quot; and &quot;OR&quot;.

![](../images/policies/and-or-selection.png)

#### Select consent attributes

**** This is the attribute that must be present in order for profiles to be included in the action governed by this policy. ****

When selecting the consent attribute, choose the values for the attribute that you want this policy to check for.

![](../images/policies/select-schema-field.png)

**** This estimation automatically updates as you adjust the policy configuration.

![](../images/policies/audience-preview.png)

****

![](../images/policies/add-result.png)

You can continue adding and adjusting conditions and consent attributes to the policy as needed. ****

![](../images/policies/name-and-save.png)

 ****

![](../images/policies/enable-consent-policy.png)

#### Verify policy enforcement

After you have created and enabled a consent policy, you can preview how it affects your consented audiences when activating segments to destinations. [](../enforcement/auto-enforcement.md#consent-policy-evaluation)

## Enable or disable a policy {#enable}

All data usage policies (including core policies provided by Adobe) are disabled by default. For an individual policy to be considered for enforcement, you must manually enable that policy through the API or UI.

******** Select a custom policy from the list to display its details on the right. ****

![](../images/policies/enable-policy.png)

## View marketing actions {#view-marketing-actions}

********

![](../images/policies/marketing-actions.png)

## Create a marketing action {#create-marketing-action}

************

![](../images/policies/create-marketing-action.png)

**** ****

![](../images/policies/create-marketing-action-details.png)

**** [](#create-policy)

![](../images/policies/created-marketing-action.png)

## Edit or delete a marketing action {#edit-delete-marketing-action}

>[!NOTE]
>
>Only custom marketing actions defined by your organization can be edited. Marketing actions defined by Adobe cannot be changed or deleted.

******** Select a custom marketing action from the list, then used the provided fields in the right-hand section to edit the marketing action&#39;s details.

![](../images/policies/edit-marketing-action.png)

****

>[!NOTE]
>
>Attempting to delete a marketing action that is being used by an existing policy causes an error message to appear, indicating that the delete attempt failed.

![](../images/policies/delete-marketing-action.png)

## Passaggi successivi

[!DNL Experience Platform] [!DNL Policy Service API][](../api/getting-started.md) [](../enforcement/overview.md)

[!DNL Experience Platform]

>[!VIDEO](https://video.tv.adobe.com/v/32977?quality=12&learn=on)
