---
keywords: Experience Platform;home;argomenti popolari;Marketo Engage;marketo engagement;Marketo;mapping
solution: Experience Platform
title: Mappatura dei campi per Marketo Engage Source
description: Le tabelle seguenti contengono le mappature tra i campi dei set di dati Marketo e i campi XDM corrispondenti.
exl-id: 2b217bba-2748-4d6f-85ac-5f64d5e99d49
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '1451'
ht-degree: 5%

---

# [!DNL Marketo Engage] mappature campi {#marketo-engage-field-mappings}

Le tabelle seguenti contengono le mappature tra i campi dei nove set di dati [!DNL Marketo] e i corrispondenti campi Experience Data Model (XDM).

>[!TIP]
>
>Tutti i [!DNL Marketo] set di dati eccetto `Activities` ora supportano `isDeleted`. I flussi di dati esistenti includeranno automaticamente `isDeleted`, ma acquisiranno solo il flag per i dati appena acquisiti. Se desideri applicare il flag a tutti i dati storici, devi arrestare i flussi di dati esistenti e ricrearli con la nuova mappatura. Tieni presente che se rimuovi `isDeleted`, non potrai più accedere alla funzionalità. È fondamentale che la mappatura venga mantenuta dopo che è stata compilata automaticamente.

## Attività {#activities}

L&#39;origine [!DNL Marketo] ora supporta attività standard aggiuntive. Per utilizzare le attività standard, è necessario aggiornare lo schema utilizzando l&#39;[utilità di generazione automatica dello schema](../marketo/marketo-namespaces.md) perché se si crea un nuovo flusso di dati `activities` senza aggiornare lo schema, i modelli di mappatura non avranno esito positivo in quanto i nuovi campi di destinazione non saranno presenti nello schema. Se scegli di non aggiornare lo schema, puoi comunque creare un nuovo flusso di dati e ignorare eventuali errori. Tuttavia, eventuali campi nuovi o aggiornati non verranno acquisiti in Experience Platform.

Per ulteriori informazioni sulla classe XDM e sui gruppi di campi XDM, leggi la documentazione sulla [classe XDM Experience Event](../../../../xdm/classes/experienceevent.md).

>[!NOTE]
>
>Il campo di origine `iif(${web\.ecid} != null, to_object('ECID', arrays_to_objects('id', explode(last(split(${web\.ecid}, ":")), " "))), null)` è un campo calcolato che deve essere aggiunto utilizzando l&#39;opzione **[!UICONTROL Add calculated field]** nell&#39;interfaccia utente di Experience Platform. Per ulteriori informazioni, leggere il tutorial su [aggiunta di campi calcolati](../../../../data-prep/ui/mapping.md#calculated-fields).

| Campo di origine Marketo | ID tipo di attività | Set di dati di Source | Campo di destinazione XDM | Note |
| -------------------- | ---------------- | -------------- | ---------------- | ----- |
| `_id` |  | `_id` | `_id` |  |
|  |  | `"Marketo"` | `personKey.sourceType` |  |
|  |  | `"${MUNCHKIN_ID}"` | `personKey.sourceInstanceID` | MUNCHKIN_ID verrà sostituito come parte di Esplora API |
| `leadId` |  | `personID` | `personKey.sourceID` |  |
|  |  | `concat(personID,"@${MUNCHKIN_ID}.Marketo")` | `personKey.sourceKey` | Identità primaria. MUNCHKIN_ID verrà sostituito come parte di Esplora API |
| `activityTypeId` |  | `eventType` | `eventType` |  |
| <ul><li>Se <code>activityTypeId</code> è 1, 2, 3, 9, 10 o 11 → <code>produceBy</code> come <strong>self</strong>.</li><li>Se <code>activityTypeId</code> è il marchio di → <code>productionBy 6, 7, 8, 12, 21, 22, 24, 25, 27, 32, 34, 35, 36, 46, 101, 104, 110, 113, 114 o 115</code> come <strong>system</strong>.</li><li>Per tutti gli altri valori → contrassegna <code>productionBy</code> come <strong>self</strong>.</li></ul> |  | `producedBy` | `producedBy` |  |
| `activityDate` |  | `timestamp` | `timestamp` |  |
| `attributes.Webpage URL` |  | `web.webPageDetails.URL` | `web.webPageDetails.URL` |  |
| `attributes.User Agent` |  | `environment.browserDetails.userAgent` | `environment.browserDetails.userAgent` |  |
| `attributes.Client IP Address` |  | `environment.ipV4` | `environment.ipV4` |  |
| `attributes.Search Query` |  | `search.keywords` | `search.keywords` |  |
| `attributes.Search Engine` |  | `search.searchEngine` | `search.searchEngine` |  |
| `primaryAttributeValue when activityTypeId = 1` | 1 | `web.webPageDetails.webPageID` | `web.webPageDetails.webPageID` |  |
| `primaryAttributeValue when activityTypeId = 1` | 1 | `web.webPageDetails.name` | `web.webPageDetails.name` |  |
| `attributes.Personalized URL` | 1 | `web.webPageDetails.isPersonalizedURL` | `web.webPageDetails.isPersonalizedURL` |  |
| `attributes.Query Parameters` | 1 | `web.webPageDetails.queryParameters` | `web.webPageDetails.queryParameters` |  |
| `attributes.Referrer URL` |  | `web.webReferrer.URL` | `web.webReferrer.URL` |  |
| `primaryAttributeValueId when activityTypeId in (24, 25)` | 24, 25 | `iif(${listOperations\.listID} != null && ${listOperations\.listID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", ${listOperations\.listID}, "sourceKey", concat(${listOperations\.listID},"@${MUNCHKIN_ID}.Marketo")), null)` | `listOperations.listKey` |  |
| `attributes.Is Primary` | 34,35,36 | `opportunityEvent.isPrimary` | `opportunityEvent.isPrimary` |  |
| primaryAttributeValueId quando activityTypeId in (34, 35, 36) | 34, 35, 36 | `iif(${opportunityEvent\.opportunityID} != null && ${opportunityEvent\.opportunityID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${opportunityEvent\.opportunityID}, "sourceKey", concat(${opportunityEvent\.opportunityID},"@${MUNCHKIN_ID}.Marketo")), null)` | `opportunityEvent.opportunityKey` |  |
| `attributes.Role` | 34, 35, 36 | `opportunityEvent.role` | `opportunityEvent.role` |  |
| `attributes.Created Date` |  | `leadOperation.newLead.createdDate` | `leadOperation.newLead.createdDate` |  |
| `attributes.Form Name` |  | `leadOperation.newLead.formName` | `leadOperation.newLead.formName` |  |
| `attributes.Lead Source` |  | `leadOperation.newLead.leadSource` | `leadOperation.newLead.leadSource` |  |
| `attributes.List Name` |  | `leadOperation.newLead.listName` | `leadOperation.newLead.listName` |  |
| `attributes.SFDC Type` |  | `leadOperation.newLead.sfdcType` | `leadOperation.newLead.sfdcType` |  |
| `attributes.Source Type` |  | `leadOperation.newLead.sourceType` | `leadOperation.newLead.sourceType` |  |
| primaryAttributeValue quando activityTypeId = 21 | 21 | `leadOperation.convertLead.assignTo` | `leadOperation.convertLead.assignTo` |  |
| `attributes.Converted Status` | 21 | `leadOperation.convertLead.convertedStatus` | `leadOperation.convertLead.convertedStatus` |  |
| `attributes.Send Notification Email` | 21 | `leadOperation.convertLead.isSentNotificationEmail` | `leadOperation.convertLead.isSentNotificationEmail` |  |
| primaryAttributeValueId quando activityTypeId in (7, 8, 9, 10, 11, 27) | 7, 8, 9, 10, 11, 27 | `iif(${directMarketing\\.mailingID} != null && ${directMarketing\\.mailingID} != \"\", to_object(\"sourceType\", \"Marketo\", \"sourceInstanceID\", \"${MUNCHKIN_ID}\",\"sourceID\",${directMarketing\\.mailingID}, \"sourceKey\", concat(${directMarketing\\.mailingID},\"@${MUNCHKIN_ID}.Marketo\")), null)` | `directMarketing.mailingKey` |  |
| primaryAttributeValueId quando activityTypeId in (7, 8, 9, 10, 11, 27) | 7, 8, 9, 10, 11, 27 | `directMarketing.mailingName` | `directMarketing.mailingName` |  |
|  |  | `directMarketing.testVariantName` | `directMarketing.testVariantName` |  |
| `attributes.Test Variant` |  | `directMarketing.testVariantID` | `directMarketing.testVariantID` |  |
| `attributes.Subcategory` <ul><li><strong>activityTypeId = 8</strong><ul><li>MESSAGGIO 1099 → BLOCCATO</li><li>1003 → SPAM BLOCCATO SU SOURCE</li><li>1004 → SPAM BLOCCATO SU MESSAGGIO</li><li>INDIRIZZO E-MAIL → 2003 NON VALIDO</li><li>ERRORE INDIRIZZO E-MAIL → 2001</li><li>*` &rarr;`MOTIVO SCONOSCIUTO PER MANCATO RECAPITO</li></ul></li><li><strong>activityTypeId = 27</strong><ul><li>MESSAGGIO → 3999 NON ACCETTATO</li><li>3001 → CASSETTA POSTALE PIENA</li><li>TIMEOUT → 3004</li><li>ERRORE DNS → 4003</li><li>MESSAGGIO → 4002 TROPPO GRANDE</li><li>4006 → VIOLAZIONE DEI CRITERI</li><li>4999 → GUASTO TRANSITORIO</li><li>9999 → RISPOSTA NON VALIDA RICEVUTA</li><li>*→ MOTIVO SCONOSCIUTO PER MANCATO RECAPITO NON PERMANENTE</li></ul></li></ul> | 8, 27 | `directMarketing.emailBouncedCode` | `directMarketing.emailBouncedCode` |  |
| `attributes.Details` |  | `directMarketing.emailBouncedDetails` | `directMarketing.emailBouncedDetails` |  |
| `attributes.Email` |  | `directMarketing.email` | `directMarketing.email` |  |
| `attributes.Is Mobile Device` |  | `device.isMobileDevice` | `device.isMobileDevice` |  |
| `attributes.device` |  | `device.model` | `device.model` |  |
| `attributes.Platform` |  | `environment.operatingSystem` | `environment.operatingSystem` |  |
| `attributes.Link` |  | `directMarketing.linkURL` | `directMarketing.linkURL` |  |
| primaryAttributeValueId quando activityTypeId = 3 else attributes.Link ID | 3 | `iif(${web\\.webInteraction\\.linkID} != null && ${web\\.webInteraction\\.linkID} != \"\", to_object(\"sourceType\", \"Marketo\", \"sourceInstanceID\", \"${MUNCHKIN_ID}\",\"sourceID\",${web\\.webInteraction\\.linkID}, \"sourceKey\", concat(${web\\.webInteraction\\.linkID},\"@${MUNCHKIN_ID}.Marketo\")), null)` | `web.webInteraction.webInteractionKey` |  |
| primaryAttributeValueId quando activityTypeId = 2 else attributes.Webform ID | 2 | `iif(${web\\.fillOutForm\\.webFormID} != null && ${web\\.fillOutForm\\.webFormID} != \"\", to_object(\"sourceType\", \"Marketo\", \"sourceInstanceID\", \"${MUNCHKIN_ID}\",\"sourceID\",${web\\.fillOutForm\\.webFormID}, \"sourceKey\", concat(${web\\.fillOutForm\\.webFormID},\"@${MUNCHKIN_ID}.Marketo\")), null)` | `web.fillOutForm.webFormKey` |  |
| primaryAttributeValueId quando activityTypeId = 2 else null | 2 | `web.fillOutForm.webFormName` | `web.fillOutForm.webFormName` |  |
| primaryAttributeValueId quando activityTypeId = 3 else attributes.Link | 3 | `web.webInteraction.linkURL` | `web.webInteraction.linkURL` |  |
| `attributes.Change Value` | 22 | `leadOperation.changeScore.changeValue` | `leadOperation.changeScore.changeValue` |  |
| `attributes.New Value` | 22 | `leadOperation.changeScore.newValue` | `leadOperation.changeScore.newValue` |  |
| `attributes.Old Value` | 22 | `leadOperation.changeScore.oldValue` | `leadOperation.changeScore.oldValue` |  |
| `attributes.Priority` | 22 | `leadOperation.changeScore.priority` | `leadOperation.changeScore.priority` |  |
| `attributes.Reason` | 22 | `leadOperation.changeScore.reason` | `leadOperation.changeScore.reason` |  |
| `attributes.Relative Score` | 22 | `leadOperation.changeScore.relativeScore` | `leadOperation.changeScore.relativeScore` |  |
| `attributes.Relative Urgency` | 22 | `leadOperation.changeScore.relativeUrgency` | `leadOperation.changeScore.relativeUrgency` |  |
| primaryAttributeValueId quando activityTypeId = 22 | 22 | `iif(${leadOperation\.changeScore\.scoreAttributeID} != null && ${leadOperation\.changeScore\.scoreAttributeID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.changeScore\.scoreAttributeID}, "sourceKey", concat(${leadOperation\.changeScore\.scoreAttributeID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.changeScore.scoreAttributeKey` |  |
| primaryAttributeValueId quando activityTypeId = 22 | 22 | `leadOperation.changeScore.scoreAttributeName` | `leadOperation.changeScore.scoreAttributeName` |  |
| `attributes.Urgency` | 22 | `leadOperation.changeScore.urgency` | `leadOperation.changeScore.urgency` |  |
| `attributes.Data Value Changes` |  | `json_to_object(${opportunityEvent\.dataValueChanges})` | `opportunityEvent.dataValueChanges` |  |
| primaryAttributeValueId quando activityTypeId = 104 | 104 | `iif(${leadOperation\.campaignProgression\.campaignID} != null && ${leadOperation\.campaignProgression\.campaignID} != "" , to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", ${leadOperation\.campaignProgression\.campaignID}, "sourceKey", concat(${leadOperation\.campaignProgression\.campaignID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.campaignProgression.campaignKey` |  |
| `attributes.Acquired By` | 104 | `leadOperation.campaignProgression.isAcquiredBy` | `leadOperation.campaignProgression.isAcquiredBy` |  |
| `attributes.Success` | 104 | `leadOperation.campaignProgression.isSuccessful` | `leadOperation.campaignProgression.isSuccessful` |  |
| `attributes.New Status ID` | 104 | `leadOperation.campaignProgression.newStatusID` | `leadOperation.campaignProgression.newStatusID` |  |
| `attributes.New Status` | 104 | `leadOperation.campaignProgression.newStatusName` | `leadOperation.campaignProgression.newStatusName` |  |
| `attributes.Old Status ID` | 104 | `leadOperation.campaignProgression.oldStatusID` | `leadOperation.campaignProgression.oldStatusID` |  |
| `attributes.Old Status` | 104 | `leadOperation.campaignProgression.oldStatusName` | `leadOperation.campaignProgression.oldStatusName` |  |
| `attributes.Reason` | 104 | `leadOperation.campaignProgression.reason` | `leadOperation.campaignProgression.reason` |  |
| `attributes.Date` | 46 | `leadOperation.interestingMoment.date` | `leadOperation.interestingMoment.date` |  |
| `attributes.Description` | 46 | `leadOperation.interestingMoment.description` | `leadOperation.interestingMoment.description` |  |
| `attributes.Source` | 46 | `leadOperation.interestingMoment.source` | `leadOperation.interestingMoment.source` |  |
| primaryAttributeValue quando activityTypeId = 46 | 46 | `leadOperation.interestingMoment.type` | `leadOperation.interestingMoment.type` |  |
| primaryAttributeValueId quando activityTypeId = 110 | 110 | `iif(${leadOperation\\.callWebhook\\.webhookID} != null && ${leadOperation\\.callWebhook\\.webhookID} != \"\", to_object(\"sourceType\", \"Marketo\", \"sourceInstanceID\", \"${MUNCHKIN_ID}\", \"sourceID\", ${leadOperation\\.callWebhook\\.webhookID}, \"sourceKey\", concat(${leadOperation\\.callWebhook\\.webhookID},\"@${MUNCHKIN_ID}.Marketo\")), null)` | `leadOperation.callWebhook.webhookKey` |  |
| primaryAttributeValueId quando activityTypeId = 110 | 110 | `leadOperation.callWebhook.webhookName` | `leadOperation.callWebhook.webhookName` |  |
| `attributes.Error Type` | 110 | `leadOperation.callWebhook.responseCode` | `leadOperation.callWebhook.responseCode` |  |
| primaryAttributeValueId quando activityTypeId = 115 | 115 | `iif(${leadOperation\\.changeCampaignCadence\\.campaignID} != null && ${leadOperation\\.changeCampaignCadence\\.campaignID} != \"\", to_object(\"sourceType\", \"Marketo\", \"sourceInstanceID\", \"${MUNCHKIN_ID}\", \"sourceID\", ${leadOperation\\.changeCampaignCadence\\.campaignID}, \"sourceKey\", concat(${leadOperation\\.changeCampaignCadence\\.campaignID},\"@${MUNCHKIN_ID}.Marketo\")), null)` | `leadOperation.changeCampaignCadence.campaignKey` |  |
| `attributes.New Nurture Cadence` | 115 | `leadOperation.changeCampaignCadence.newCadence` | `leadOperation.changeCampaignCadence.newCadence` |  |
| `attributes.Previous Nurture Cadence` | 115 | `leadOperation.changeCampaignCadence.previousCadence` | `leadOperation.changeCampaignCadence.previousCadence` |  |
| primaryAttributeValueId quando activityTypeId = 114 | 113 | `iif(${leadOperation\.addToCampaign\.campaignID} != null && ${leadOperation\.addToCampaign\.campaignID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.addToCampaign\.campaignID}, "sourceKey", concat(${leadOperation\.addToCampaign\.campaignID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.addToCampaign.campaignKey` |  |
| `attributes.Track ID` | 113 | `iif(${leadOperation\.addToCampaign\.streamID} != null && ${leadOperation\.addToCampaign\.streamID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.addToCampaign\.streamID}, "sourceKey", concat(${leadOperation\.addToCampaign\.streamID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.addToCampaign.streamKey` |  |
| `attributes.Stream Name` | 113 | `leadOperation.addToCampaign.streamName` | `leadOperation.addToCampaign.streamName` |  |
| primaryAttributeValueId quando activityTypeId = 115 | 115 | `iif(${leadOperation\.changeCampaignStream\.campaignID} != null && ${leadOperation\.changeCampaignStream\.campaignID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.changeCampaignStream\.campaignID}, "sourceKey", concat(${leadOperation\.changeCampaignStream\.campaignID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.changeCampaignStream.campaignKey` |  |
| `attributes.New Track ID` | 115 | `iif(${leadOperation\.changeCampaignStream\.newStreamID} != null && ${leadOperation\.changeCampaignStream\.newStreamID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.changeCampaignStream\.newStreamID}, "sourceKey", concat(${leadOperation\.changeCampaignStream\.newStreamID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.changeCampaignStream.newStreamKey` |  |
| `attributes.New Track Name` | 115 | `leadOperation.changeCampaignStream.newStreamName` | `leadOperation.changeCampaignStream.newStreamName` |  |
| `attributes.Previous Track ID` | 115 | `iif(${leadOperation\.changeCampaignStream\.previousStreamID} != null && ${leadOperation\.changeCampaignStream\.previousStreamID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.changeCampaignStream\.previousStreamID}, "sourceKey", concat(${leadOperation\.changeCampaignStream\.previousStreamID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.changeCampaignStream.previousStreamKey` |  |
| `attributes.Previous Stream Name` | 115 | `leadOperation.changeCampaignStream.previousStreamName` | `leadOperation.changeCampaignStream.previousStreamName` |  |
| primaryAttributeValueId quando activityTypeId = 101 | 101 | `iif(${leadOperation\.changeRevenueStage\.modelID} != null && ${leadOperation\.changeRevenueStage\.modelID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.changeRevenueStage\.modelID}, "sourceKey", concat(${leadOperation\.changeRevenueStage\.modelID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.changeRevenueStage.modelKey` |  |
| primaryAttributeValueId quando activityTypeId = 101 | 101 | `leadOperation.changeRevenueStage.modelName` | `leadOperation.changeRevenueStage.modelName` |  |
| `attributes.New Stage ID` | 101 | `iif(${leadOperation\.changeRevenueStage\.newStageID} != null && ${leadOperation\.changeRevenueStage\.newStageID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${leadOperation\.changeRevenueStage\.newStageID}, "sourceKey", concat(${leadOperation\.changeRevenueStage\.newStageID},"@${MUNCHKIN_ID}.Marketo")), null)` | `leadOperation.changeRevenueStage.newStageKey` |  |
| `attributes.New Stage` | 101 | `leadOperation.changeRevenueStage.newStageName` | `leadOperation.changeRevenueStage.newStageName` |  |
| `attributes.Old Stage ID` | 101 | `iif(${leadOperation\\.changeRevenueStage\\.previousStageID} != null && ${leadOperation\\.changeRevenueStage\\.previousStageID} != \"\", to_object(\"sourceType\", \"Marketo\", \"sourceInstanceID\", \"${MUNCHKIN_ID}\",\"sourceID\",${leadOperation\\.changeRevenueStage\\.previousStageID}, \"sourceKey\", concat(${leadOperation\\.changeRevenueStage\\.previousStageID},\"@${MUNCHKIN_ID}.Marketo\")), null)` | `leadOperation.changeRevenueStage.previousStageKey` |  |
| `attributes.Old Stage` | 101 | `leadOperation.changeRevenueStage.previousStageName` | `leadOperation.changeRevenueStage.previousStageName` |  |
| `attributes.Reason` | 101 | `leadOperation.changeRevenueStage.reason` | `leadOperation.changeRevenueStage.reason` |  |
| `attributes.Merge IDs` quando activityTypeId = 32 | 32 | `json_to_object(${leadOperation\.mergeLeads\.mergeIDs})` | `leadOperation.mergeLeads.sourceKeys` |  |
| `attributes.Master Updated` | 32 | `leadOperation.mergeLeads.targetUpdated` | `leadOperation.mergeLeads.targetUpdated` |  |
| `attributes.Merged in Sales` | 32 | `leadOperation.mergeLeads.mergedInCRM` | `leadOperation.mergeLeads.mergedInCRM` |  |
| `attributes.Merge Source` | 32 | `leadOperation.mergeLeads.mergeSource` | `leadOperation.mergeLeads.mergeSource` |  |
| primaryAttributeValueId quando activityTypeId = 6 | 6 | `iif(${directMarketing\.emailSent\.mailingID} != null && ${directMarketing\.emailSent\.mailingID} != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}","sourceID",${directMarketing\.emailSent\.mailingID}, "sourceKey", concat(${directMarketing\.emailSent\.mailingID},"@${MUNCHKIN_ID}.Marketo")), null)` | `directMarketing.emailSent.mailingKey` |  |
| primaryAttributeValueId quando activityTypeId = 6 | 6 | `directMarketing.emailSent.mailingName` | `directMarketing.emailSent.mailingName` |  |
| `attributes.Test Variant` | 6 | `directMarketing.emailSent.testVariantID` | `directMarketing.emailSent.testVariantID` |  |
| Nota - derivata dal valore delle attività secondarie |  | `directMarketing.emailSent.testVariantName` | `directMarketing.emailSent.testVariantName` |  |
| `attributes.Campaign Run ID` | 6 | `directMarketing.emailSent.automationRunID` | `directMarketing.emailSent.automationRunID` |  |
|  |  | `directMarketing.automationRunID` | `directMarketing.automationRunID` |  |

{style="table-layout:auto"}

## Programmi {#programs}

Per ulteriori informazioni sulla classe XDM, consulta la [panoramica della campagna aziendale XDM](../../../../xdm/classes/b2b/business-campaign.md). Per ulteriori informazioni sui gruppi di campi XDM, consulta la guida del gruppo di campi dello schema [Dettagli campagna aziendale](../../../../xdm/field-groups/b2b-campaign/details.md).

>[!NOTE]
>
>Per i tipi di tag personalizzati, passa a schemi e crea nuovi gruppi di campi. Quindi, aggiungi tutti i nomi di campo aggiuntivi necessari per mappare i campi di origine con i campi XDM di destinazione.

| Set di dati di Source | Campo di destinazione XDM | Note |
| -------------- | --------------- | ----- |
| `"${MUNCHKIN_ID}"` | `campaignKey.sourceInstanceID` | MUNCHKIN_ID verrà sostituito come parte di Esplora API |
| `"Marketo"` | `campaignKey.sourceType` |  |
| `channel` | `channelName` |  |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `campaignKey.sourceKey` | Identità primaria. MUNCHKIN_ID verrà sostituito come parte di Esplora API |
| `cost` | `actualCost.amount` |  |
| `createdAt` | `extSourceSystemAudit.createdDate` |  |
| `description` | `campaignDescription` |  |
| `endDate` | `campaignEndDate` |  |
| `id` | `campaignKey.sourceID` |  |
| `iif(parentProgramId != null && parentProgramId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", parentProgramId, "sourceKey", concat(parentProgramId,"@${MUNCHKIN_ID}.Marketo")), null)` | `parentCampaignKey` |  |
| `iif(sfdcId != null && sfdcId != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", sfdcId, "sourceKey", concat(sfdcId,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)` | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey.sourceKey` è un&#39;identità secondaria. CRM_TYPE e CRM_ORG_ID verranno sostituiti come parte di Esplora API |
| `integrationPartner` | `integrationPartnerName` |  |
| `marketoIsDeleted` | `isDeleted` |  |
| `name` | `campaignName` |  |
| `startDate` | `campaignStartDate` |  |
| `status` | `campaignStatus` |  |
| `type` | `campaignType` |  |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `webinarHistorySyncDate` | `webinarHistorySyncDate` |  |
| `webinarHistorySyncStatus` | `webinarHistorySyncStatus` |  |
| `webinarSessionDescription` | `webinarSessionDescription` |  |
| `webinarSessionName` | `webinarSessionName` |  |

{style="table-layout:auto"}

## Iscrizioni al programma {#program-memberships}

Per ulteriori informazioni sulla classe XDM, leggere la [panoramica dei membri della campagna aziendale XDM](../../../../xdm/classes/b2b/business-campaign-members.md). Per ulteriori informazioni sui gruppi di campi XDM, consulta la guida del gruppo di campi schema [Dettagli membro della campagna aziendale XDM](../../../../xdm/field-groups/b2b-campaign-members/details.md).

| Set di dati di Source | Campo di destinazione XDM | Note |
| -------------- | --------------- | ----- |
| `"Marketo"` | `campaignMemberKey.sourceType` |  |
| `"${MUNCHKIN_ID}"` | `campaignMemberKey.sourceInstanceID` | MUNCHKIN_ID verrà sostituito come parte di Esplora API |
| `id` | `campaignMemberKey.sourceID` |  |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `campaignMemberKey.sourceKey` | Identità primaria. MUNCHKIN_ID verrà sostituito come parte di Esplora API |
| `iif(programId != null && programId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", programId, "sourceKey", concat(programId,"@${MUNCHKIN_ID}.Marketo")), null)` | `campaignKey` | Relazione |
| `iif(leadId != null && leadId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", leadId, "sourceKey", concat(leadId,"@${MUNCHKIN_ID}.Marketo")), null)` | `personKey` | Relazione |
| `iif(acquiredByCampaignID != null && acquiredByCampaignID != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", acquiredByCampaignID, "sourceKey", concat(acquiredByCampaignID,"@${MUNCHKIN_ID}.Marketo")), null)` | `acquiredByCampaignKey` |  |
| `reachedSuccess` | `hasReachedSuccess` |  |
| `isExhausted` | `isExhausted` |  |
| `statusName` | `memberStatus` |  |
| `statusReason` | `memberStatusReason` |  |
| `membershipDate` | `membershipDate` |  |
| `nurtureCadence` | `nurtureCadence` |  |
| `trackName` | `nurtureTrackName` |  |
| `webinarUrl` | `webinarConfirmationUrl` |  |
| `registrationCode` | `webinarRegistrationID` |  |
| `reachedSuccessDate` | `reachedSuccessDate` |  |
| `iif(sfdc.crmId != null && sfdc.crmId != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", sfdc.crmId, "sourceKey", concat(sfdc.crmId,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)` | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey.sourceKey` è un&#39;identità secondaria. CRM_TYPE e CRM_ORG_ID verranno sostituiti come parte di Esplora API |
| `sfdc.lastStatus` | `lastStatus` |  |
| `sfdc.hasResponded` | `hasResponded` |  |
| `sfdc.firstRespondedDate` | `firstRespondedDate` |  |
| `createdAt` | `extSourceSystemAudit.createdDate` |  |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `marketoIsDeleted` | `isDeleted` |  |

{style="table-layout:auto"}

## Aziende {#companies}

Per ulteriori informazioni sulla classe XDM, leggere la [panoramica dell&#39;account aziendale XDM](../../../../xdm/classes/b2b/business-account.md).

| Set di dati di Source | Campo di destinazione XDM | Note |
| -------------- | ---------------- | ----- |
| `"Marketo"` | `accountKey.sourceType` | |
| `"${MUNCHKIN_ID}"` | `accountKey.sourceInstanceID` | MUNCHKIN_ID verrà sostituito come parte di Esplora API |
| `concat(id, ".mkto_org")` | `accountKey.sourceID` | |
| `concat(id, ".mkto_org@${MUNCHKIN_ID}.Marketo")` | `accountKey.sourceKey` | Identità primaria. MUNCHKIN_ID verrà sostituito come parte di Esplora API |
| <ul><li><code>iif(mktoCdpExternalId!= null &amp;&amp; mktoCdpExternalId != &quot;&quot;, to_object(&quot;sourceType&quot;, &quot;${CRM_TYPE}&quot;, &quot;sourceInstanceID&quot;, &quot;${CRM_ORG_ID}&quot;, &quot;sourceID&quot;, mktoCdpExternalId, &quot;sourceKey&quot;, concat(mktoCdpExternalId,&quot;@${CRM_ORG_ID}.${CRM_TYPE}&quot;), null)</code></li><li><code>iif(msftCdpExternalId!= null &amp;&amp; msftCdpExternalId != &quot;&quot;, to_object(&quot;sourceType&quot;, &quot;${CRM_TYPE}&quot;, &quot;sourceInstanceID&quot;, &quot;${CRM_ORG_ID}&quot;, &quot;sourceID&quot;, msftCdpExternalId, &quot;sourceKey&quot;, concat(msftCdpExternalId,&quot;@${CRM_ORG_ID}.${CRM_TYPE}&quot;), null)</code></li></ul> | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey.sourceKey` è un&#39;identità secondaria. CRM_ORG_ID e CRM_TYPE verranno sostituiti come parte di Esplora API |
| `createdAt` | `extSourceSystemAudit.createdDate` | |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` | |
| `billingCity` | `accountBillingAddress.city` | |
| `billingCountry` | `accountBillingAddress.country` | |
| `billingPostalCode` | `accountBillingAddress.postalCode` | |
| `billingState` | `accountBillingAddress.state` | |
| `billingStreet` | `accountBillingAddress.street1` | |
| `annualRevenue` | `accountOrganization.annualRevenue.amount` | |
| `sicCode` | `accountOrganization.SICCode` | |
| `industry` | `accountOrganization.industry` | |
| `numberOfEmployees` | `accountOrganization.numberOfEmployees` | |
| `website` | `accountOrganization.website` | |
| `mainPhone` | `accountPhone.number` | |
| `company` | `accountName` | |
| `companyNotes` | `accountDescription` | |
| `site` | `accountSite` | |
| `iif(mktoCdpParentOrgId != null && mktoCdpParentOrgId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", concat(mktoCdpParentOrgId, ".mkto_org"), "sourceKey", concat(mktoCdpParentOrgId, ".mkto_org@${MUNCHKIN_ID}.Marketo")), null)` | `accountParentKey` | |
| `marketoIsDeleted` | `isDeleted` | |

{style="table-layout:auto"}

## Elenchi statici {#static-lists}

Per ulteriori informazioni sulla classe XDM, consulta la [panoramica dell&#39;elenco di marketing aziendale XDM](../../../../xdm/classes/b2b/business-marketing-list.md).

| Set di dati di Source | Campo di destinazione XDM | Note |
| -------------- | --------------- | ----- |
| `"Marketo"` | `marketingListKey.sourceType` |  |
| `"${MUNCHKIN_ID}"` | `marketingListKey.sourceInstanceID` | MUNCHKIN_ID verrà sostituito come parte di Esplora API |
| `id` | `marketingListKey.sourceID` |  |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `marketingListKey.sourceKey` | Identità primaria. MUNCHKIN_ID verrà sostituito come parte di Esplora API |
| `name` | `marketingListName` |  |
| `description` | `marketingListDescription` |  |
| `createdAt` | `extSourceSystemAudit.createdDate` |  |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `marketoIsDeleted` | `isDeleted` |  |

{style="table-layout:auto"}

## Appartenenze a elenchi statici {#static-list-memberships}

Per ulteriori informazioni sulla classe XDM, consulta la [panoramica dei membri dell&#39;elenco di marketing aziendale XDM](../../../../xdm/classes/b2b/business-marketing-list-members.md).

| Set di dati di Source | Campo di destinazione XDM | Note |
| -------------- | --------------- | ----- |
| `"Marketo"` | `marketingListMemberKey.sourceType` |  |
| `"${MUNCHKIN_ID}"` | `marketingListMemberKey.sourceInstanceID` | MUNCHKIN_ID verrà sostituito come parte di Esplora API |
| `staticListMemberID` | `marketingListMemberKey.sourceID` |  |
| `concat(staticListMemberID,"@${MUNCHKIN_ID}.Marketo")` | `marketingListMemberKey.sourceKey` | Identità primaria. MUNCHKIN_ID verrà sostituito come parte di Esplora API |
| `iif(staticListID != null && staticListID != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", staticListID, "sourceKey", concat(staticListID,"@${MUNCHKIN_ID}.Marketo")), null)` | `marketingListKey` | Relazione |
| `iif(personID != null && personID != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", personID, "sourceKey", concat(personID,"@${MUNCHKIN_ID}.Marketo")), null)` | `personKey` | Relazione |
| `createdAt` | `extSourceSystemAudit.createdDate` |  |
| `marketoIsDeleted` | `isDeleted` |  |

{style="table-layout:auto"}

## Account denominati {#named-accounts}

>[!IMPORTANT]
>
>Il set di dati account denominato è necessario solo con la funzione di marketing basato su account (ABM) di Marketo. Se non utilizzi ABM, non è necessario impostare mappature per account denominati.

Per ulteriori informazioni sulla classe XDM, leggere la [panoramica dell&#39;account aziendale XDM](../../../../xdm/classes/b2b/business-account.md).

| Set di dati di Source | Campo di destinazione XDM | Note |
| -------------- | --------------- | ----- |
| `"Marketo"` | `accountKey.sourceType` |  |
| `"${MUNCHKIN_ID}"` | `accountKey.sourceInstanceID` | MUNCHKIN_ID verrà sostituito come parte di Esplora API |
| `concat(id, ".mkto_acct")` | `accountKey.sourceID` |  |
| `concat(id, ".mkto_acct@${MUNCHKIN_ID}.Marketo")` | `accountKey.sourceKey` | Identità primaria. MUNCHKIN_ID verrà sostituito come parte di Esplora API |
| `iif(crmGuid != null && crmGuid != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", crmGuid, "sourceKey", concat(crmGuid,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)` | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey.sourceKey` è un&#39;identità secondaria. CRM_TYPE e CRM_ORG_ID verranno sostituiti come parte di Esplora API |
| `createdAt` | `extSourceSystemAudit.createdDate` |  |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `city` | `accountBillingAddress.city` |  |
| `country` | `accountBillingAddress.country` |  |
| `state` | `accountBillingAddress.state` |  |
| `annualRevenue` | `accountOrganization.annualRevenue.amount` |  |
| `sicCode` | `accountOrganization.SICCode` |  |
| `industry` | `accountOrganization.industry` |  |
| `logoUrl` | `accountOrganization.logoUrl` |  |
| `numberOfEmployees` | `accountOrganization.numberOfEmployees` |  |
| `name` | `accountName` |  |
| `iif(parentAccountId != null && parentAccountId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", concat(parentAccountId, ".mkto_acct"), "sourceKey", concat(parentAccountId, ".mkto_acct@${MUNCHKIN_ID}.Marketo")), null)` | `accountParentKey` |  |
| `sourceType` | `accountSourceType` |  |
| `marketoIsDeleted` | `isDeleted` |  |

{style="table-layout:auto"}

## Opportunità {#opportunities}

Per ulteriori informazioni sulla classe XDM, consulta la [panoramica sull&#39;opportunità di business XDM](../../../../xdm/classes/b2b/business-opportunity.md).

| Set di dati di Source | Campo di destinazione XDM | Note |
| -------------- | --------------- | ----- |
| `"Marketo"` | `opportunityKey.sourceType` |  |
| `"${MUNCHKIN_ID}"` | `opportunityKey.sourceInstanceID` | MUNCHKIN_ID verrà sostituito come parte di Esplora API |
| `id` | `opportunityKey.sourceID` |  |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `opportunityKey.sourceKey` | Identità primaria. MUNCHKIN_ID verrà sostituito come parte di Esplora API |
| `iif(externalOpportunityId != null && externalOpportunityId != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", externalOpportunityId, "sourceKey", concat(externalOpportunityId,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)` | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey.sourceKey` è un&#39;identità secondaria. CRM_TYPE e CRM_ORG_ID verranno sostituiti come parte di Esplora API |
| `iif(mktoCdpAccountOrgId != null && mktoCdpAccountOrgId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", concat(mktoCdpAccountOrgId, ".mkto_org"), "sourceKey", concat(mktoCdpAccountOrgId, ".mkto_org@${MUNCHKIN_ID}.Marketo")), null)` | `accountKey` | Relazione |
| `description` | `opportunityDescription` |  |
| `name` | `opportunityName` |  |
| `stage` | `opportunityStage` |  |
| `type` | `opportunityType` |  |
| `createdAt` | `extSourceSystemAudit.createdDate` |  |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |  |
| `expectedRevenue` | `expectedRevenue.amount` |  |
| `amount` | `opportunityAmount.amount` |  |
| `closeDate` | `expectedCloseDate` |  |
| `fiscalQuarter` | `fiscalQuarter` |  |
| `fiscalYear` | `fiscalYear` |  |
| `forecastCategory` | `forecastCategory` |  |
| `forecastCategoryName` | `forecastCategoryName` |  |
| `isClosed` | `isClosed` |  |
| `isWon` | `isWon` |  |
| `quantity` | `opportunityQuantity` |  |
| `probability` | `probabilityPercentage` |  |
| `iif(mktoCdpSourceCampaignId != null && mktoCdpSourceCampaignId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", mktoCdpSourceCampaignId, "sourceKey", concat(mktoCdpSourceCampaignId,"@${MUNCHKIN_ID}.Marketo")), null)` | `campaignKey` | Solo per i clienti con integrazione Salesforce |
| `lastActivityDate` | `lastActivityDate` |  |
| `leadSource` | `leadSource` |  |
| `nextStep` | `nextStep` |  |
| `marketoIsDeleted` | `isDeleted` |  |

{style="table-layout:auto"}

## Ruoli di contatto opportunità {#opportunity-contact-roles}

Per ulteriori informazioni sulla classe XDM, leggi la panoramica sulla relazione della persona dell&#39;opportunità di business [XDM](../../../../xdm/classes/b2b/business-account-person-relation.md).

| Set di dati di Source | Campo di destinazione XDM | Note |
| -------------- | --------------- | ----- |
| `"${MUNCHKIN_ID}"` | `opportunityPersonKey.sourceInstanceID` | MUNCHKIN_ID verrà sostituito come parte di Esplora API |
| `"Marketo"` | `opportunityPersonKey.sourceType` |  |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `opportunityPersonKey.sourceKey` | Identità primaria. MUNCHKIN_ID verrà sostituito come parte di Esplora API |
| `createdAt` | `extSourceSystemAudit.createdDate` |  |
| `id` | `opportunityPersonKey.sourceID` |  |
| `iif(leadId != null && leadId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", leadId, "sourceKey", concat(leadId,"@${MUNCHKIN_ID}.Marketo")), null)` | `personKey` | Relazione |
| `iif(mktoCdpOpptyId != null && mktoCdpOpptyId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", mktoCdpOpptyId, "sourceKey", concat(mktoCdpOpptyId,"@${MUNCHKIN_ID}.Marketo")), null)` | `opportunityKey` | Relazione |
| `iif(mktoCdpSfdcId != null && mktoCdpSfdcId != "", to_object("sourceType", "${CRM_TYPE}", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", mktoCdpSfdcId, "sourceKey", concat(mktoCdpSfdcId,"@${CRM_ORG_ID}.${CRM_TYPE}")), null)` | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey.sourceKey` è un&#39;identità secondaria. CRM_TYPE e CRM_ORG_ID verranno sostituiti come parte di Esplora API |
| `isPrimary` | `isPrimary` |  |
| `marketoIsDeleted` | `isDeleted` |  |
| `role` | `personRole` |  |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |  |

{style="table-layout:auto"}

## Persone {#persons}

Per ulteriori informazioni sulla classe XDM, leggi la [Panoramica profilo individuale XDM](../../../../xdm/classes/individual-profile.md). Per ulteriori informazioni sui gruppi di campi XDM, leggere la guida del gruppo di campi dello schema [Dettagli persona aziendale XDM](../../../../xdm/field-groups/profile/business-person-details.md) e la guida del gruppo di campi dello schema [Componenti persona aziendale XDM](../../../../xdm/field-groups/profile/business-person-components.md).

| Campo di origine | Campo XDM di destinazione | Note |
|---|---|---|
| `"${MUNCHKIN_ID}"` | `b2b.personKey.sourceInstanceID` | MUNCHKIN_ID verrà sostituito come parte di Esplora API |
| `"Marketo"` | `b2b.personKey.sourceType` | |
| `address` | `workAddress.street1` | |
| `city` | `workAddress.city` | |
| `company` | `organizations` | |
| `concat(id,"@${MUNCHKIN_ID}.Marketo")` | `b2b.personKey.sourceKey` | Identità primaria. MUNCHKIN_ID verrà sostituito come parte di Esplora API |
| `country` | `workAddress.country` | |
| `createdAt` | `extSourceSystemAudit.createdDate` | |
| `dateOfBirth` | `person.birthDate` | |
| `email` | `personComponents.workEmail.address` | |
| `email` | `workEmail.address` | |
| `fax` | `faxPhone.number` | |
| `firstName` | `person.name.firstName` | |
| `id` | `b2b.personKey.sourceID` | |
| `iif(contactCompany != null && contactCompany != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", concat(contactCompany, ".mkto_org"), "sourceKey", concat(contactCompany, ".mkto_org@${MUNCHKIN_ID}.Marketo")), null)` | `b2b.accountKey` | |
| `iif(contactCompany != null && contactCompany != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", concat(contactCompany, ".mkto_org"), "sourceKey", concat(contactCompany, ".mkto_org@${MUNCHKIN_ID}.Marketo")), null)` | `personComponents.sourceAccountKey` | |
| <ul><li><code>iif(decode(sfdcType, &quot;Contact&quot;, sfdcContactId, &quot;Lead&quot;, sfdcLeadId , null) != null, to_object(&quot;sourceType&quot;, &quot;${CRM_TYPE}&quot;, &quot;sourceInstanceID&quot;, &quot;${CRM_ORG_ID}&quot;,&quot;sourceID&quot;, decode(sfdcType, &quot;Contact&quot;, sfdcContactId, &quot;Lead&quot;, sfdcLeadId , null), &quot;sourceKey&quot;, concat(decode(sfdcType, &quot;Contact&quot;, sfdcContactId, &quot;Lead&quot;, sfdcLeadId , null),&quot;@${CRM_ORG_ID}.${CRM_TYPE}&quot;), null)</code></li><li><code>iif(decode(msftType, &quot;Contact&quot;, msftContactId, &quot;Lead&quot;, msftLeadId , null) != null, to_object(&quot;sourceType&quot;, &quot;${CRM_TYPE}&quot;, &quot;sourceInstanceID&quot;, &quot;${CRM_ORG_ID}&quot;,&quot;sourceID&quot;, decode(msftType, &quot;Contact&quot;, msftContactId, &quot;Lead&quot;, msftLeadId , null), &quot;sourceKey&quot;, concat(decode(msftType, &quot;Contact&quot;, msftContactId, &quot;Lead&quot;, msftLeadId , null),&quot;@${CRM_ORG_ID}.${CRM_TYPE}&quot;), null)</code></li></ul> | `personComponents.sourceExternalKey` | |
| <ul><li><code>iif(decode(sfdcType, &quot;Contact&quot;, sfdcContactId, &quot;Lead&quot;, sfdcLeadId , null) != null, to_object(&quot;sourceType&quot;, &quot;${CRM_TYPE}&quot;, &quot;sourceInstanceID&quot;, &quot;${CRM_ORG_ID}&quot;,&quot;sourceID&quot;, decode(sfdcType, &quot;Contact&quot;, sfdcContactId, &quot;Lead&quot;, sfdcLeadId , null), &quot;sourceKey&quot;, concat(decode(sfdcType, &quot;Contact&quot;, sfdcContactId, &quot;Lead&quot;, sfdcLeadId , null),&quot;@${CRM_ORG_ID}.${CRM_TYPE}&quot;), null)</code></li><li><code>iif(decode(msftType, &quot;Contact&quot;, msftContactId, &quot;Lead&quot;, msftLeadId , null) != null, to_object(&quot;sourceType&quot;, &quot;${CRM_TYPE}&quot;, &quot;sourceInstanceID&quot;, &quot;${CRM_ORG_ID}&quot;,&quot;sourceID&quot;, decode(msftType, &quot;Contact&quot;, msftContactId, &quot;Lead&quot;, msftLeadId , null), &quot;sourceKey&quot;, concat(decode(msftType, &quot;Contact&quot;, msftContactId, &quot;Lead&quot;, msftLeadId , null),&quot;@${CRM_ORG_ID}.${CRM_TYPE}&quot;), null)</code></li></ul> | `extSourceSystemAudit.externalKey` | `extSourceSystemAudit.externalKey.sourceKey` è un&#39;identità secondaria |
| `iif(ecids != null, to_object('ECID',arrays_to_objects('id',explode(ecids))), null)` | `identityMap` | Campo calcolato |
| `iif(id != null && id != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", id, "sourceKey", concat(id,"@${MUNCHKIN_ID}.Marketo")), null)` | `personComponents.sourcePersonKey` | |
| `iif(mktoCdpCnvContactPersonId != null && mktoCdpCnvContactPersonId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", mktoCdpCnvContactPersonId, "sourceKey", concat(mktoCdpCnvContactPersonId,"@${MUNCHKIN_ID}.Marketo")), null)` | `b2b.convertedContactKey` | Campo calcolato |
| `iif(mktoCdpCnvContactPersonId != null && mktoCdpCnvContactPersonId != "", to_object("sourceType", "Marketo", "sourceInstanceID", "${MUNCHKIN_ID}", "sourceID", mktoCdpCnvContactPersonId, "sourceKey", concat(mktoCdpCnvContactPersonId,"@${MUNCHKIN_ID}.Marketo")), null)` | `personComponents.sourceConvertedContactKey` | Campo calcolato |
| `iif(unsubscribed == 'true', 'n', 'y' )` | `consents.marketing.email.val` | Se l’annullamento dell’abbonamento è vero (ovvero valore = 1), imposta consents.marketing.email.val su &quot;n&quot;. Se l’annullamento dell’abbonamento è falso (ad esempio, valore = 0), imposta consents.marketing.email.val su null |
| `iif(unsubscribedReason != null && unsubscribedReason != "", substr(unsubscribedReason, 0, 100), null)` | `consents.marketing.email.reason` | |
| `lastName` | `person.name.lastName` | |
| `leadPartitionId` | `b2b.personGroupID` | |
| `leadPartitionId` | `personComponents.personGroupID` | |
| `leadScore` | `b2b.personScore` | |
| `leadScore` | `personComponents.personScore` | |
| `leadSource` | `b2b.personSource` | |
| `leadSource` | `personComponents.personSource` | |
| `leadStatus` | `b2b.personStatus` | |
| `leadStatus` | `personComponents.personStatus` | |
| `marketingSuspended` | `b2b.isMarketingSuspended` | |
| `marketingSuspendedCause` | `b2b.marketingSuspendedCause` | |
| `marketoIsDeleted` | `isDeleted` | |
| `middleName` | `person.name.middleName` | |
| `mktoCdpConvertedDate` | `b2b.convertedDate` | |
| `mktoCdpIsConverted` | `b2b.isConverted` | |
| `mobilePhone` | `mobilePhone.number` | |
| `personType` | `b2b.personType` | |
| `personType` | `personComponents.personType` | |
| `phone` | `workPhone.number` | |
| `postalCode` | `workAddress.postalCode` | |
| `salutation` | `person.name.courtesyTitle` | |
| `state` | `workAddress.state` | |
| `title` | `extendedWorkDetails.jobTitle` | |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` | |

{style="table-layout:auto"}

## Passaggi successivi

Dopo aver letto questo documento, hai acquisito insight sulla relazione di mappatura tra i set di dati [!DNL Marketo] e i campi XDM corrispondenti. Guarda l&#39;esercitazione sulla [creazione di una [!DNL Marketo] connessione di origine](../../../tutorials/ui/create/adobe-applications/marketo.md) per completare il flusso di dati di [!DNL Marketo].