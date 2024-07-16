---
keywords: Experience Platform;home;argomenti popolari;Marketo Engage;marketo;Marketo;mapping
solution: Experience Platform
title: Campi di mappatura per il Source del Marketo Engage
description: Le tabelle seguenti contengono le mappature tra i campi dei set di dati Marketo e i campi XDM corrispondenti.
exl-id: 2b217bba-2748-4d6f-85ac-5f64d5e99d49
source-git-commit: 9399ac0e2e0a284799874af15188bbf4a4a380a7
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 2%

---

# [!DNL Marketo Engage] mappature campi {#marketo-engage-field-mappings}

Le tabelle seguenti contengono le mappature tra i campi dei nove set di dati [!DNL Marketo] e i corrispondenti campi Experience Data Model (XDM).

>[!TIP]
>
>Tutti i [!DNL Marketo] set di dati eccetto `Activities` ora supportano `isDeleted`. I flussi di dati esistenti includeranno automaticamente `isDeleted`, ma acquisiranno solo il flag per i dati appena acquisiti. Se desideri applicare il flag a tutti i dati storici, devi arrestare i flussi di dati esistenti e ricrearli con la nuova mappatura. Tieni presente che se rimuovi `isDeleted`, non potrai più accedere alla funzionalità. È fondamentale che la mappatura venga mantenuta dopo che è stata compilata automaticamente.

## Attività {#activities}

L&#39;origine [!DNL Marketo] ora supporta attività standard aggiuntive. Per utilizzare le attività standard, è necessario aggiornare lo schema utilizzando l&#39;[utilità di generazione automatica dello schema](../marketo/marketo-namespaces.md) perché se si crea un nuovo flusso di dati `activities` senza aggiornare lo schema, i modelli di mappatura non avranno esito positivo in quanto i nuovi campi di destinazione non saranno presenti nello schema. Se scegli di non aggiornare lo schema, puoi comunque creare un nuovo flusso di dati e ignorare eventuali errori. Tuttavia, eventuali campi nuovi o aggiornati non verranno acquisiti in Platform.

Per ulteriori informazioni sulla classe XDM e sui gruppi di campi XDM, leggi la documentazione sulla [classe XDM Experience Event](../../../../xdm/classes/experienceevent.md).

>[!NOTE]
>
>Il campo di origine `iif(${web\.ecid} != null, to_object('ECID', arrays_to_objects('id', explode(last(split(${web\.ecid}, ":")), " "))), null)` è un campo calcolato che deve essere aggiunto utilizzando l&#39;opzione **[!UICONTROL Aggiungi campo calcolato]** nell&#39;interfaccia utente di Experience Platform. Per ulteriori informazioni, leggere il tutorial su [aggiunta di campi calcolati](../../../../data-prep/ui/mapping.md#calculated-fields).

| Set di dati di Source | Campo di destinazione XDM | Note |
| -------------- | ---------------- | ----- |
| `_id` | `_id` |
| `"Marketo"` | `personKey.sourceType` |
| `"${MUNCHKIN_ID}"` | `personKey.sourceInstanceID` | Il valore per `"${MUNCHKIN_ID}"` verrà sostituito automaticamente. |
| `personID` | `personKey.sourceID` |
| `concat(personID,"@${MUNCHKIN_ID}.Marketo")` | `personKey.sourceKey` | Identità primaria. Il valore per `"${MUNCHKIN_ID}"` verrà sostituito automaticamente. |
| `eventType` | `eventType` |
| `producedBy` | `producedBy` |
| `timestamp` | `timestamp` |
| `web.webPageDetails.URL` | `web.webPageDetails.URL` |
| `environment.browserDetails.userAgent` | `environment.browserDetails.userAgent` |
| `environment.ipV4` | `environment.ipV4` |
| `search.keywords` | `search.keywords` |
| `search.searchEngine` | `search.searchEngine` |
| `web.webPageDetails.webPageID` | `web.webPageDetails.webPageID` |
| `web.webPageDetails.name` | `web.webPageDetails.name` |
| `web.webPageDetails.isPersonalizedURL` | `web.webPageDetails.isPersonalizedURL` |
| `web.webPageDetails.queryParameters` | `web.webPageDetails.queryParameters` |
| `web.webReferrer.URL` | `web.webReferrer.URL` |
| `iif(${listOperations\.listID} != null && ${listOperations\.listID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", ${listOperations\.listID}, "sourceKey", concat(${listOperations\.listID},"@${MUNCHKIN_ID}.Marketo")), null)` | `listOperations.listKey` |
| `opportunityEvent.isPrimary` | `opportunityEvent.isPrimary` |
| `iif(${opportunityEvent\.opportunityID} != null && ${opportunityEvent\.opportunityID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${opportunityEvent\.opportunityID}, "sourceKey", concat(${opportunityEvent\.opportunityID},"@${MUNCHKIN_ID}.Marketo")), null)` | `opportunityEvent.opportunityKey` |
| `opportunityEvent.role` | `opportunityEvent.role` |
| `leadOperation.newLead.createdDate` | `leadOperation.newLead.createdDate` |
| `leadOperation.newLead.formName` | `leadOperation.newLead.formName` |
| `leadOperation.newLead.leadSource` | `leadOperation.newLead.leadSource` |
| `leadOperation.newLead.listName` | `leadOperation.newLead.listName` |
| `leadOperation.newLead.sfdcType` | `leadOperation.newLead.sfdcType` |
| `leadOperation.newLead.sourceType` | `leadOperation.newLead.sourceType` |
| `leadOperation.convertLead.assignTo` | `leadOperation.convertLead.assignTo` |
| `leadOperation.convertLead.convertedStatus` | `leadOperation.convertLead.convertedStatus` |
| `leadOperation.convertLead.isSentNotificationEmail` | `leadOperation.convertLead.isSentNotificationEmail` |
| `directMarketing.mailingID` | `directMarketing.mailingID` |
| `directMarketing.mailingName` | `directMarketing.mailingName` |
| `directMarketing.testVariantName` | `directMarketing.testVariantName` |
| `directMarketing.testVariantID` | `directMarketing.testVariantID` |
| `directMarketing.emailBouncedCode` | `directMarketing.emailBouncedCode` |
| `directMarketing.emailBouncedDetails` | `directMarketing.emailBouncedDetails` |
| `directMarketing.email` | `directMarketing.email` |
| `device.isMobileDevice` | `device.isMobileDevice` |
| `device.model` | `device.model` |
| `environment.operatingSystem` | `environment.operatingSystem` |
| `directMarketing.linkURL` | `directMarketing.linkURL` |
| `web.webInteraction.linkID` | `web.webInteraction.linkID` |
| `web.fillOutForm.webFormID` | `web.fillOutForm.webFormID` |
| `web.fillOutForm.webFormName` | `web.fillOutForm.webFormName` |
| `web.webInteraction.linkURL` | `web.webInteraction.linkURL` |
| `leadOperation.changeScore.changeValue` | `leadOperation.changeScore.changeValue` |
| `leadOperation.changeScore.newValue` | `leadOperation.changeScore.newValue` |
| `leadOperation.changeScore.oldValue` | `leadOperation.changeScore.oldValue` |
| `leadOperation.changeScore.priority` | `leadOperation.changeScore.priority` |
| `leadOperation.changeScore.reason` | `leadOperation.changeScore.reason` |
| `leadOperation.changeScore.relativeScore` | `leadOperation.changeScore.relativeScore` |
| `leadOperation.changeScore.relativeUrgency` | `leadOperation.changeScore.relativeUrgency` |
| `leadOperation.changeScore.scoreAttributeID` | `leadOperation.changeScore.scoreAttributeID` |
| `leadOperation.changeScore.scoreAttributeName` | `leadOperation.changeScore.scoreAttributeName` |
| `leadOperation.changeScore.urgency` | `leadOperation.changeScore.urgency` |
| `json_to_object(${opportunityEvent\.dataValueChanges})` | `opportunityEvent.dataValueChanges` |
| `iif(${leadOperation\.campaignProgression\.campaignID} != null && ${leadOperation\.campaignProgression\.campaignID} != "" , to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", ${leadOperation\.campaignProgression\.campaignID}, "sourceKey", concat(${leadOperation\.campaignProgression\.campaignID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.campaignProgression.campaignKey` |
| `leadOperation.campaignProgression.campaignID` | `leadOperation.campaignProgression.campaignID` |
| `leadOperation.campaignProgression.isAcquiredBy` | `leadOperation.campaignProgression.isAcquiredBy` |
| `leadOperation.campaignProgression.isSuccessful` | `leadOperation.campaignProgression.isSuccessful` |
| `leadOperation.campaignProgression.newStatusID` | `leadOperation.campaignProgression.newStatusID` |
| `leadOperation.campaignProgression.newStatusName` | `leadOperation.campaignProgression.newStatusName` |
| `leadOperation.campaignProgression.oldStatusID` | `leadOperation.campaignProgression.oldStatusID` |
| `leadOperation.campaignProgression.oldStatusName` | `leadOperation.campaignProgression.oldStatusName` |
| `leadOperation.campaignProgression.reason` | `leadOperation.campaignProgression.reason` |
| `leadOperation.interestingMoment.date` | `leadOperation.interestingMoment.date` |
| `leadOperation.interestingMoment.description` | `leadOperation.interestingMoment.description` |
| `leadOperation.interestingMoment.source` | `leadOperation.interestingMoment.source` |
| `leadOperation.interestingMoment.type` | `leadOperation.interestingMoment.type` |
| `iif(${leadOperation\\.callWebhook\\.webhookKey\\.sourceID} != null && ${leadOperation\\.callWebhook\\.webhookKey\\.sourceID} != \"\", to_object(\"sourceType\", \"Marketo\", \"sourceInstanceID\", \"${MUNCHKIN_ID}\", \"sourceID\", ${leadOperation\\.callWebhook\\.webhookKey\\.sourceID}, \"sourceKey\", concat(${leadOperation\\.callWebhook\\.webhookKey\\.sourceInstanceID},\"@${MUNCHKIN_ID}.Marketo\")), null)"` | `leadOperation.callWebhook.webhookKey` |
| `leadOperation.callWebhook.webhookName` | `leadOperation.callWebhook.webhookName` |
| `leadOperation.callWebhook.responseCode` | `leadOperation.callWebhook.responseCode` |
| `iif(${leadOperation\\.changeCampaignCadence\\.campaignKey\\.sourceID} != null && ${leadOperation\\.changeCampaignCadence\\.campaignKey\\.sourceID} != \"\", to_object(\"sourceType\", \"Marketo\", \"sourceInstanceID\", \"${MUNCHKIN_ID}\", \"sourceID\", ${leadOperation\\.changeCampaignCadence\\.campaignKey\\.sourceID}, \"sourceKey\", concat(${leadOperation\\.changeCampaignCadence\\.campaignKey\\.sourceInstanceID},\"@${MUNCHKIN_ID}.Marketo\")), null)"` | `leadOperation.changeCampaignCadence.campaignKey` |
| `leadOperation.changeCampaignCadence.newCadence` | `leadOperation.changeCampaignCadence.newCadence` |
| `leadOperation.changeCampaignCadence.previousCadence` | `leadOperation.changeCampaignCadence.previousCadence` |
| `iif(${leadOperation\.addToCampaign\.campaignID} != null && ${leadOperation\.addToCampaign\.campaignID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.addToCampaign\.campaignID}, "sourceKey", concat(${leadOperation\.addToCampaign\.campaignID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.addToCampaign.campaignKey` |
| `iif(${leadOperation\.addToCampaign\.streamID} != null && ${leadOperation\.addToCampaign\.streamID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.addToCampaign\.streamID}, "sourceKey", concat(${leadOperation\.addToCampaign\.streamID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.addToCampaign.streamKey` |
| `leadOperation.addToCampaign.streamName` | `leadOperation.addToCampaign.streamName` |
| `iif(${leadOperation\.changeCampaignStream\.campaignID} != null && ${leadOperation\.changeCampaignStream\.campaignID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.changeCampaignStream\.campaignID}, "sourceKey", concat(${leadOperation\.changeCampaignStream\.campaignID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.changeCampaignStream.campaignKey` |
| `iif(${leadOperation\.changeCampaignStream\.newStreamID} != null && ${leadOperation\.changeCampaignStream\.newStreamID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.changeCampaignStream\.newStreamID}, "sourceKey", concat(${leadOperation\.changeCampaignStream\.newStreamID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.changeCampaignStream.newStreamKey` |
| `leadOperation.changeCampaignStream.newStreamName` | `leadOperation.changeCampaignStream.newStreamName` |
| `iif(${leadOperation\.changeCampaignStream\.previousStreamID} != null && ${leadOperation\.changeCampaignStream\.previousStreamID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.changeCampaignStream\.previousStreamID}, "sourceKey", concat(${leadOperation\.changeCampaignStream\.previousStreamID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.changeCampaignStream.previousStreamKey` |
| `leadOperation.changeCampaignStream.previousStreamName` | `leadOperation.changeCampaignStream.previousStreamName` |
| `iif(${leadOperation\.changeRevenueStage\.modelID} != null && ${leadOperation\.changeRevenueStage\.modelID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.changeRevenueStage\.modelID}, "sourceKey", concat(${leadOperation\.changeRevenueStage\.modelID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.changeRevenueStage.modelKey` |
| `leadOperation.changeRevenueStage.modelName` | `leadOperation.changeRevenueStage.modelName` |
| `iif(${leadOperation\.changeRevenueStage\.newStageID} != null && ${leadOperation\.changeRevenueStage\.newStageID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.changeRevenueStage\.newStageID}, "sourceKey", concat(${leadOperation\.changeRevenueStage\.newStageID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.changeRevenueStage.newStageKey` |
| `leadOperation.changeRevenueStage.newStageName` | `leadOperation.changeRevenueStage.newStageName` |
| `iif(${leadOperation\\.changeRevenueStage\\.previousStageID} != null && ${leadOperation\\.changeRevenueStage\\.previousStageID} != \"\", to_object(\"sourceType\", \"Marketo\", \"sourceInstanceID\", \"${MUNCHKIN_ID}\",\"sourceID\",${leadOperation\\.changeRevenueStage\\.previousStageID}, \"sourceKey\", concat(${leadOperation\\.changeRevenueStage\\.previousStageID},\"@${MUNCHKIN_ID}.Marketo\")), null)` | `leadOperation.changeRevenueStage.previousStageKey` |
| `leadOperation.changeRevenueStage.previousStageName` | `leadOperation.changeRevenueStage.previousStageName` |
| `leadOperation.changeRevenueStage.reason` | `leadOperation.changeRevenueStage.reason` |
| `iif(${leadOperation\.mergeLeads\.sourceIDs} != null && ${leadOperation\.mergeLeads\.sourceIDs} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.mergeLeads\.sourceIDs}, "sourceKey", concat(${leadOperation\.mergeLeads\.sourceIDs},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.mergeLeads.sourceKeys` |
| `leadOperation.mergeLeads.targetUpdated` | `leadOperation.mergeLeads.targetUpdated` |
| `leadOperation.mergeLeads.mergedInCRM` | `leadOperation.mergeLeads.mergedInCRM` |
| `leadOperation.mergeLeads.mergeSource` | `leadOperation.mergeLeads.mergeSource` |
| `iif(${directMarketing\\.emailSent\\.mailingID} != null && ${directMarketing\\.emailSent\\.mailingID} != \"\", to_object(\"sourceType\", \"Marketo\", \"sourceInstanceID\", \"${MUNCHKIN_ID}\",\"sourceID\",${directMarketing\\.emailSent\\.mailingID}, \"sourceKey\", concat(${directMarketing\\.emailSent\\.mailingID},\"@${MUNCHKIN_ID}.Marketo\")), null)"` | `directMarketing.emailSent.mailingKey` |
| `directMarketing.emailSent.mailingName` | `directMarketing.emailSent.mailingName` |
| `directMarketing.emailSent.testVariantID` | `directMarketing.emailSent.testVariantID` |
| `directMarketing.emailSent.testVariantName` | `directMarketing.emailSent.testVariantName` |
| `directMarketing.emailSent.automationRunID` | `directMarketing.emailSent.automationRunID` |
| `iif(${web\.ecid} != null, to_object('ECID', arrays_to_objects('id', explode(last(split(${web\.ecid}, ":")), " "))), null)` | `identityMap` | Campo calcolato. |

{style="table-layout:auto"}

## Programmi {#programs}

Per ulteriori informazioni sulla classe XDM, consulta la [panoramica della campagna aziendale XDM](../../../../xdm/classes/b2b/business-campaign.md). Per ulteriori informazioni sui gruppi di campi XDM, consulta la guida del gruppo di campi dello schema [Dettagli campagna aziendale](../../../../xdm/field-groups/b2b-campaign/details.md).

| Set di dati di Source | Campo di destinazione XDM | Note |
| -------------- | ---------------- | ----- |
| `"Marketo"` | `campaignKey.sourceType` |
| `"${MUNCHKIN_ID}"` | `campaignKey.sourceInstanceID` | Il valore per `"${MUNCHKIN_ID}"` verrà sostituito automaticamente. |
| `id` | `campaignKey.sourceID` |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `campaignKey.sourceKey` | Identità primaria. Il valore per `"${MUNCHKIN_ID}"` verrà sostituito automaticamente. |
| `iif(sfdcId != null && sfdcId != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", sfdcId, "sourceKey", concat(sfdcId,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)` | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey` è l&#39;identità secondaria. I valori per `{CRM_ORG_ID}` e `{CRM_TYPE}` verranno sostituiti automaticamente. |
| `name` | `campaignName` |
| `description` | `campaignDescription` |
| `type` | `campaignType` |
| `status` | `campaignStatus` |
| `channel` | `channelName` |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `cost` | `actualCost.amount` |
| `iif(parentProgramId != null && parentProgramId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", parentProgramId, "sourceKey", concat(parentProgramId,"@${MUNCHKIN_ID}.Marketo")), null)` | `parentCampaignKey` |
| `integrationPartner` | `integrationPartnerName` |
| `webinarSessionName` | `webinarSessionName` |
| `webinarSessionDescription` | `webinarSessionDescription` |
| `webinarHistorySyncStatus` | `webinarHistorySyncStatus` |
| `webinarHistorySyncDate` | `webinarHistorySyncDate` |
| `startDate` | `campaignStartDate` |
| `endDate` | `campaignEndDate` |
| `marketoIsDeleted` | `isDeleted` |

{style="table-layout:auto"}

## Iscrizioni al programma {#program-memberships}

Per ulteriori informazioni sulla classe XDM, leggere la [panoramica dei membri della campagna aziendale XDM](../../../../xdm/classes/b2b/business-campaign-members.md). Per ulteriori informazioni sui gruppi di campi XDM, consulta la guida del gruppo di campi schema [Dettagli membro della campagna aziendale XDM](../../../../xdm/field-groups/b2b-campaign-members/details.md).

| Set di dati di Source | Campo di destinazione XDM | Note |
| -------------- | ---------------- | ----- |
| `"Marketo"` | `campaignMemberKey.sourceType` |
| `"${MUNCHKIN_ID}"` | `campaignMemberKey.sourceInstanceID` | Il valore per `"${MUNCHKIN_ID}"` verrà sostituito automaticamente. |
| `id` | `campaignMemberKey.sourceID` |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `campaignMemberKey.sourceKey` | Identità primaria. Il valore per `"${MUNCHKIN_ID}"` verrà sostituito automaticamente. |
| `iif(programId != null && programId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", programId, "sourceKey", concat(programId,"@${MUNCHKIN_ID}.Marketo")), null)` | `campaignKey` | Relazione |
| `iif(leadId != null && leadId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", leadId, "sourceKey", concat(leadId,"@${MUNCHKIN_ID}.Marketo")), null)` | `personKey` | Relazione |
| `iif(acquiredByCampaignID != null && acquiredByCampaignID != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", acquiredByCampaignID, "sourceKey", concat(acquiredByCampaignID,"@${MUNCHKIN_ID}.Marketo")), null)` | `acquiredByCampaignKey` |
| `reachedSuccess` | `hasReachedSuccess` |
| `isExhausted` | `isExhausted` |
| `statusName` | `memberStatus` |
| `statusReason` | `memberStatusReason` |
| `membershipDate` | `membershipDate` |
| `nurtureCadence` | `nurtureCadence` |
| `trackName` | `nurtureTrackName` |
| `webinarUrl` | `webinarConfirmationUrl` |
| `registrationCode` | `webinarRegistrationID` |
| `reachedSuccessDate` | `reachedSuccessDate` |
| `iif(sfdc.crmId != null && sfdc.crmId != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", sfdc.crmId, "sourceKey", concat(sfdc.crmId,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)` | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey` è l&#39;identità secondaria. I valori per `{CRM_ORG_ID}` e `{CRM_TYPE}` verranno sostituiti automaticamente. |
| `sfdc.lastStatus` | `lastStatus` |
| `sfdc.hasResponded` | `hasResponded` |
| `sfdc.firstRespondedDate` | `firstRespondedDate` |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `marketoIsDeleted` | `isDeleted` |

{style="table-layout:auto"}

## Aziende {#companies}

Per ulteriori informazioni sulla classe XDM, leggere la [panoramica dell&#39;account aziendale XDM](../../../../xdm/classes/b2b/business-account.md).

| Set di dati di Source | Campo di destinazione XDM | Note |
| -------------- | ---------------- | ----- |
| `"Marketo"` | `accountKey.sourceType` |
| `"${MUNCHKIN_ID}"` | `accountKey.sourceInstanceID` | Il valore per `"${MUNCHKIN_ID}"` verrà sostituito automaticamente. |
| `concat(id, ".mkto_org")` | `accountKey.sourceID` |
| `concat(id, ".mkto_org@${MUNCHKIN_ID}.Marketo")` | `accountKey.sourceKey` | Identità primaria. Il valore per `"${MUNCHKIN_ID}"` verrà sostituito automaticamente. |
| <ul><li>`iif(mktoCdpExternalId != null && mktoCdpExternalId != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", mktoCdpExternalId, "sourceKey", concat(mktoCdpExternalId,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)`</li><li>`iif(msftCdpExternalId != null && msftCdpExternalId != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", msftCdpExternalId, "sourceKey", concat(msftCdpExternalId,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)`</li></ul> | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey` è l&#39;identità secondaria. I valori per `{CRM_ORG_ID}` e `{CRM_TYPE}` verranno sostituiti automaticamente. |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `billingCity` | `accountBillingAddress.city` |
| `billingCountry` | `accountBillingAddress.country` |
| `billingPostalCode` | `accountBillingAddress.postalCode` |
| `billingState` | `accountBillingAddress.state` |
| `billingStreet` | `accountBillingAddress.street1` |
| `annualRevenue` | `accountOrganization.annualRevenue.amount` |
| `sicCode` | `accountOrganization.SICCode` |
| `industry` | `accountOrganization.industry` |
| `numberOfEmployees` | `accountOrganization.numberOfEmployees` |
| `website` | `accountOrganization.website` |
| `mainPhone` | `accountPhone.number` |
| `company` | `accountName` |
| `companyNotes` | `accountDescription` |
| `site` | `accountSite` |
| `iif(mktoCdpParentOrgId != null && mktoCdpParentOrgId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", concat(mktoCdpParentOrgId, ".mkto_org"), "sourceKey", concat(mktoCdpParentOrgId, ".mkto_org@${MUNCHKIN_ID}.Marketo")), null)` | `accountParentKey` |
| `marketoIsDeleted` | `isDeleted` |

{style="table-layout:auto"}

## Elenchi statici {#static-lists}

Per ulteriori informazioni sulla classe XDM, consulta la [panoramica dell&#39;elenco di marketing aziendale XDM](../../../../xdm/classes/b2b/business-marketing-list.md).

| Set di dati di Source | Campo di destinazione XDM | Note |
| -------------- | ---------------- | ----- |
| `"Marketo"` | `marketingListKey.sourceType` |
| `"${MUNCHKIN_ID}"` | `marketingListKey.sourceInstanceID` | `"${MUNCHKIN_ID}"` verrà sostituito come parte dell&#39;API di esplorazione. |
| `id` | `marketingListKey.sourceID` |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `marketingListKey.sourceKey` | Identità primaria. Il valore per `"${MUNCHKIN_ID}"` verrà sostituito automaticamente. |
| `name` | `marketingListName` |
| `description` | `marketingListDescription` |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `marketoIsDeleted` | `isDeleted` |

{style="table-layout:auto"}

## Appartenenze a elenchi statici {#static-list-memberships}

Per ulteriori informazioni sulla classe XDM, consulta la [panoramica dei membri dell&#39;elenco di marketing aziendale XDM](../../../../xdm/classes/b2b/business-marketing-list-members.md).

| Set di dati di Source | Campo di destinazione XDM | Note |
| -------------- | ---------------- | ----- |
| `"Marketo"` | `marketingListMemberKey.sourceType` |
| `"${MUNCHKIN_ID}"` | `marketingListMemberKey.sourceInstanceID` | Il valore per `"${MUNCHKIN_ID}"` verrà sostituito automaticamente. |
| `staticListMemberID` | `marketingListMemberKey.sourceID` |
| `concat(staticListMemberID,"@${MUNCHKIN_ID}.Marketo")` | `marketingListMemberKey.sourceKey` | Identità primaria. Il valore per `"${MUNCHKIN_ID}"` verrà sostituito automaticamente. |
| `iif(staticListID != null && staticListID != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", staticListID, "sourceKey", concat(staticListID,"@${MUNCHKIN_ID}.Marketo")), null)` | `marketingListKey` | Relazione |
| `iif(personID != null && personID != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", personID, "sourceKey", concat(personID,"@${MUNCHKIN_ID}.Marketo")), null)` | `personKey` | Relazione |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `marketoIsDeleted` | `isDeleted` |

{style="table-layout:auto"}

## Account denominati {#named-accounts}

>[!IMPORTANT]
>
>Il set di dati account denominato è necessario solo con la funzione di marketing basato su account (ABM) di Marketo. Se non utilizzi ABM, non è necessario impostare mappature per account denominati.

Per ulteriori informazioni sulla classe XDM, leggere la [panoramica dell&#39;account aziendale XDM](../../../../xdm/classes/b2b/business-account.md).

| Set di dati di Source | Campo di destinazione XDM | Note |
| -------------- | ---------------- | ----- |
| `"Marketo"` | `accountKey.sourceType` |
| `"${MUNCHKIN_ID}"` | `accountKey.sourceInstanceID` | Il valore per `"${MUNCHKIN_ID}"` verrà sostituito automaticamente. |
| `concat(id, ".mkto_acct")` | `accountKey.sourceID` |
| `concat(id, ".mkto_acct@${MUNCHKIN_ID}.Marketo")` | `accountKey.sourceKey` | Identità primaria. Il valore per `"${MUNCHKIN_ID}"` verrà sostituito automaticamente. |
| `iif(crmGuid != null && crmGuid != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", crmGuid, "sourceKey", concat(crmGuid,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)` | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey` è l&#39;identità secondaria. I valori per `{CRM_ORG_ID}` e `{CRM_TYPE}` verranno sostituiti automaticamente. |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `city` | `accountBillingAddress.city` |
| `country` | `accountBillingAddress.country` |
| `state` | `accountBillingAddress.state` |
| `annualRevenue` | `accountOrganization.annualRevenue.amount` |
| `sicCode` | `accountOrganization.SICCode` |
| `industry` | `accountOrganization.industry` |
| `logoUrl` | `accountOrganization.logoUrl` |
| `numberOfEmployees` | `accountOrganization.numberOfEmployees` |
| `name` | `accountName` |
| `iif(parentAccountId != null && parentAccountId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", concat(parentAccountId, ".mkto_acct"), "sourceKey", concat(parentAccountId, ".mkto_acct@${MUNCHKIN_ID}.Marketo")), null)` | `accountParentKey` |
| `sourceType` | `accountSourceType` |
| `marketoIsDeleted` | `isDeleted` |

{style="table-layout:auto"}

## Opportunità {#opportunities}

Per ulteriori informazioni sulla classe XDM, consulta la [panoramica sull&#39;opportunità di business XDM](../../../../xdm/classes/b2b/business-opportunity.md).

| Set di dati di Source | Campo di destinazione XDM | Note |
| -------------- | ---------------- | ----- |
| `"Marketo"` | `opportunityKey.sourceType` |
| `"${MUNCHKIN_ID}"` | `opportunityKey.sourceInstanceID` | Il valore per `"${MUNCHKIN_ID}"` verrà sostituito automaticamente. |
| `id` | `opportunityKey.sourceID` |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `opportunityKey.sourceKey` | Identità primaria. Il valore per `"${MUNCHKIN_ID}"` verrà sostituito automaticamente. |
| `iif(externalOpportunityId != null && externalOpportunityId != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", externalOpportunityId, "sourceKey", concat(externalOpportunityId,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)` | `extSourceSystemAudit.externalKey.sourceKey` | Identità secondaria. I valori per `{CRM_ORG_ID}` e `{CRM_TYPE}` verranno sostituiti automaticamente. |
| `iif(mktoCdpAccountOrgId != null && mktoCdpAccountOrgId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", concat(mktoCdpAccountOrgId, ".mkto_org"), "sourceKey", concat(mktoCdpAccountOrgId, ".mkto_org@${MUNCHKIN_ID}.Marketo")), null)` | `accountKey` | Relazione |
| `description` | `opportunityDescription` |
| `name` | `opportunityName` |
| `stage` | `opportunityStage` |
| `type` | `opportunityType` |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `expectedRevenue` | `expectedRevenue.amount` |
| `amount` | `opportunityAmount.amount` |
| `closeDate` | `expectedCloseDate` |
| `fiscalQuarter` | `fiscalQuarter` |
| `fiscalYear` | `fiscalYear` |
| `forecastCategory` | `forecastCategory` |
| `forecastCategoryName` | `forecastCategoryName` |
| `isClosed` | `isClosed` |
| `isWon` | `isWon` |
| `quantity` | `opportunityQuantity` |
| `probability` | `probabilityPercentage` |
| `iif(mktoCdpAccountOrgId != null && mktoCdpAccountOrgId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", concat(mktoCdpAccountOrgId, ".mkto_org"), "sourceKey", concat(mktoCdpAccountOrgId, ".mkto_org@${MUNCHKIN_ID}.Marketo")), null)` | `accountKey` | Questo set di dati di origine è disponibile solo per gli utenti con integrazione [!DNL Salesforce]. |
| `lastActivityDate` | `lastActivityDate` |
| `leadSource` | `leadSource` |
| `nextStep` | `nextStep` |
| `marketoIsDeleted` | `isDeleted` |

{style="table-layout:auto"}

## Ruoli di contatto opportunità {#opportunity-contact-roles}

Per ulteriori informazioni sulla classe XDM, leggi la panoramica sulla relazione della persona dell&#39;opportunità di business [XDM](../../../../xdm/classes/b2b/business-account-person-relation.md).

| Set di dati di Source | Campo di destinazione XDM | Note |
| -------------- | ---------------- | ----- |
| `"Marketo"` | `opportunityPersonKey.sourceType` |
| `"${MUNCHKIN_ID}"` | `opportunityPersonKey.sourceInstanceID` | Il valore per `"${MUNCHKIN_ID}"` verrà sostituito automaticamente. |
| `id` | `opportunityPersonKey.sourceID` |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `opportunityPersonKey.sourceKey` | Identità primaria. Il valore per `"${MUNCHKIN_ID}"` verrà sostituito come parte dell&#39;API di esplorazione. |
| `iif(mktoCdpSfdcId != null && mktoCdpSfdcId != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", mktoCdpSfdcId, "sourceKey", concat(mktoCdpSfdcId,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)` | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey` è l&#39;identità secondaria. I valori per `{CRM_ORG_ID}` e `{CRM_TYPE}` verranno sostituiti automaticamente. |
| `iif(mktoCdpOpptyId != null && mktoCdpOpptyId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", mktoCdpOpptyId, "sourceKey", concat(mktoCdpOpptyId,"@${MUNCHKIN_ID}.Marketo")), null)` | `opportunityKey` | Relazione |
| `iif(leadId != null && leadId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", leadId, "sourceKey", concat(leadId,"@${MUNCHKIN_ID}.Marketo")), null)` | `personKey` | Relazione |
| `role` | `personRole` |
| `isPrimary` | `isPrimary` |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `marketoIsDeleted` | `isDeleted` |

{style="table-layout:auto"}

## Persone {#persons}

Per ulteriori informazioni sulla classe XDM, leggi la [Panoramica profilo individuale XDM](../../../../xdm/classes/individual-profile.md). Per ulteriori informazioni sui gruppi di campi XDM, leggere la guida del gruppo di campi dello schema [Dettagli persona aziendale XDM](../../../../xdm/field-groups/profile/business-person-details.md) e la guida del gruppo di campi dello schema [Componenti persona aziendale XDM](../../../../xdm/field-groups/profile/business-person-components.md).

| Set di dati di Source | Campo di destinazione XDM | Note |
| -------------- | ---------------- | ----- |
| `"Marketo"` | `b2b.personKey.sourceType` |
| `"${MUNCHKIN_ID}"` | `b2b.personKey.sourceInstanceID` | Il valore per `"${MUNCHKIN_ID}"` verrà sostituito automaticamente. |
| `id` | `b2b.personKey.sourceID` |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `b2b.personKey.sourceKey` | Identità primaria. Il valore per `"${MUNCHKIN_ID}"` verrà sostituito automaticamente. |
| `iif(unsubscribed == 'true', 'n', 'y' ))` | `consents.marketing.email.val` | Se l&#39;annullamento è `true` (ad esempio, valore = `1`), impostare `consents.marketing.email.val` come (`n`). Se l&#39;annullamento è `false` (ad esempio, valore = `0`), impostare `consents.marketing.email.val` come `null`. |
| `iif(unsubscribedReason != null && unsubscribedReason != "", substr(unsubscribedReason, 0, 100), null)` | `consents.marketing.email.reason` |
| `iif(contactCompany != null && contactCompany != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", concat(contactCompany, ".mkto_org"), "sourceKey", concat(contactCompany, ".mkto_org@${MUNCHKIN_ID}.Marketo")), null)` | `b2b.accountKey` |
| `marketingSuspended` | `b2b.isMarketingSuspended` |
| `marketingSuspendedCause` | `b2b.marketingSuspendedCause` |
| `leadScore` | `b2b.personScore` |
| `leadSource` | `b2b.personSource` |
| `leadStatus` | `b2b.personStatus` |
| `personType` | `b2b.personType` |
| `leadPartitionId` | `b2b.personGroupID` |
| `mktoCdpIsConverted` | `b2b.isConverted` |
| `mktoCdpConvertedDate` | `b2b.convertedDate` |
| <ul><li>`iif(decode(sfdcType, "Contact", sfdcContactId, "Lead", sfdcLeadId , null) != null, to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", decode(sfdcType, "Contact", sfdcContactId, "Lead", sfdcLeadId , null), "sourceKey", concat(decode(sfdcType, "Contact", sfdcContactId, "Lead", sfdcLeadId , null),"@${CRM_ORG_ID}.${CRM_TYPE}")), null)`</li><li>`iif(decode(msftType, "Contact", msftContactId, "Lead", msftLeadId , null) != null, to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", decode(msftType, "Contact", msftContactId, "Lead", msftLeadId , null), "sourceKey", concat(decode(msftType, "Contact", msftContactId, "Lead", msftLeadId , null),"@${CRM_ORG_ID}.${CRM_TYPE}")), null)`</li></ul> | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey` è l&#39;identità secondaria. |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `title` | `extendedWorkDetails.jobTitle` |
| `fax` | `faxPhone.number` |
| `mobilePhone` | `mobilePhone.number` |
| `firstName` | `person.name.firstName` |
| `lastName` | `person.name.lastName` |
| `middleName` | `person.name.middleName` |
| `salutation` | `person.name.courtesyTitle` |
| `dateOfBirth` | `person.birthDate` |
| `city` | `workAddress.city` |
| `country` | `workAddress.country` |
| `postalCode` | `workAddress.postalCode` |
| `state` | `workAddress.state` |
| `address` | `workAddress.street1` |
| `phone` | `workPhone.number` |
| `company` | `b2b.companyName` |
| `website` | `b2b.companyWebsite` |
| `leadScore` | `personComponents.personScore` |
| `leadSource` | `personComponents.personSource` |
| `leadStatus` | `personComponents.personStatus` |
| `personType` | `personComponents.personType` |
| `leadPartitionId` | `personComponents.personGroupID` |
| `iif(contactCompany != null && contactCompany != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", concat(contactCompany, ".mkto_org"), "sourceKey", concat(contactCompany, ".mkto_org@${MUNCHKIN_ID}.Marketo")), null)` | `personComponents.sourceAccountKey` |
| <ul><li>`iif(decode(sfdcType, "Contact", sfdcContactId, "Lead", sfdcLeadId , null) != null, to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", decode(sfdcType, "Contact", sfdcContactId, "Lead", sfdcLeadId , null), "sourceKey", concat(decode(sfdcType, "Contact", sfdcContactId, "Lead", sfdcLeadId , null),"@${CRM_ORG_ID}.${CRM_TYPE}")), null)`</li><li>`iif(decode(msftType, "Contact", msftContactId, "Lead", msftLeadId , null) != null, to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", decode(msftType, "Contact", msftContactId, "Lead", msftLeadId , null), "sourceKey", concat(decode(msftType, "Contact", msftContactId, "Lead", msftLeadId , null),"@${CRM_ORG_ID}.${CRM_TYPE}")), null)`</li></ul> | `personComponents.sourceExternalKey` |
| `iif(id != null && id != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID", id, "sourceKey", concat(id,"@${MUNCHKIN_ID}.Marketo")), null)` | `personComponents.sourcePersonKey` |
| `email` | `personComponents.workEmail.address` |
| `email` | `workEmail.address` |
| `marketoIsDeleted` | `isDeleted` |
| `iif(mktoCdpCnvContactPersonId != null && mktoCdpCnvContactPersonId != \"\", to_object(\"sourceType\", \"Marketo\", \"sourceInstanceID\", \"${MUNCHKIN_ID}\", \"sourceID\", mktoCdpCnvContactPersonId, \"sourceKey\", concat(mktoCdpCnvContactPersonId,\"@${MUNCHKIN_ID}.Marketo\")), null)` | `b2b.convertedContactKey` | Campo calcolato. |
| `iif(mktoCdpCnvContactPersonId != null && mktoCdpCnvContactPersonId != \"\", to_object(\"sourceType\", \"Marketo\", \"sourceInstanceID\", \"${MUNCHKIN_ID}\", \"sourceID\", mktoCdpCnvContactPersonId, \"sourceKey\", concat(mktoCdpCnvContactPersonId,\"@${MUNCHKIN_ID}.Marketo\")), null)` | `personComponents.sourceConvertedContactKey` | Campo calcolato. |

{style="table-layout:auto"}

## Passaggi successivi

La lettura di questo documento fornisce informazioni approfondite sulla relazione di mappatura tra i set di dati [!DNL Marketo] e i campi XDM corrispondenti. Guarda l&#39;esercitazione sulla [creazione di una [!DNL Marketo] connessione di origine](../../../tutorials/ui/create/adobe-applications/marketo.md) per completare il flusso di dati di [!DNL Marketo].
