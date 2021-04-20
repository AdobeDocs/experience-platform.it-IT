---
keywords: Experience Platform;home;argomenti popolari;Marketo Engage;marketing da coinvolgere;Marketo;mappatura
solution: Experience Platform
title: Campi di mappatura per l'origine Marketo Engage
topic: ' - Panoramica'
description: Le tabelle seguenti contengono le mappature tra i campi nei set di dati Marketo e i campi XDM corrispondenti.
translation-type: tm+mt
source-git-commit: 2563b413ec35cb4c5f05a54bce6f7271917e51f3
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 3%

---


# (Beta) [!DNL Marketo Engage] mappature dei campi

>[!IMPORTANT]
>
>La sorgente [!DNL Marketo Engage] è attualmente in versione beta. Le sue funzioni e la sua documentazione sono soggette a modifiche.

Le tabelle seguenti contengono le mappature tra i campi dei nove set di dati [!DNL Marketo] e i corrispondenti campi Experience Data Model (XDM).

## Attività {#activities}

| Set di dati sorgente | Campo di destinazione XDM | Note |
| -------------- | ---------------- | ----- |
| `_id` | `_id` |
| `personID` | `personID` | Identità principale |
| `eventType` | `eventType` |
| `timeStamp` | `timestamp` |
| `web.webPageDetails._marketo.URL` | `web.webPageDetails._marketo.URL` |
| `environment.browserDetails.userAgent` | `environment.browserDetails.userAgent` |
| `environment.ipV4` | `environment.ipV4` |
| `search.keywords` | `search.keywords` |
| `search.searchEngine` | `search.searchEngine` |
| `web.webPageDetails.webPageID` | `web.webPageDetails.webPageID` |
| `web.webPageDetails.name` | `web.webPageDetails.name` |
| `web.webPageDetails.isPersonalizedURL` | `web.webPageDetails.isPersonalizedURL` |
| `web.webPageDetails.queryParameters` | `web.webPageDetails.queryParameters` |
| `web.webReferrer.URL` | `web.webReferrer.URL` |
| `listOperations.listID` | `listOperations.listID` |
| `opportunityEvent.isPrimary` | `opportunityEvent.isPrimary` |
| `opportunityEvent.opportunityID` | `opportunityEvent.opportunityID` |
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
| `directMarketing.testVariantID` | `directMarketing.testVariantID` |
| `directMarketing.testVariantName` | `directMarketing.testVariantName` |
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
| `opportunityEvent.dataValueChanges.attributeName` | `opportunityEvent.dataValueChanges.attributeName` |
| `opportunityEvent.dataValueChanges.newValue` | `opportunityEvent.dataValueChanges.newValue` |
| `opportunityEvent.dataValueChanges.oldValue` | `opportunityEvent.dataValueChanges.oldValue` |
| `opportunityEvent.opportunityID` | `opportunityEvent.opportunityID` |
| `leadOperation.campaignProgression.campaignID` | `leadOperation.campaignProgression.campaignID` |
| `leadOperation.campaignProgression.isAcquiredBy` | `leadOperation.campaignProgression.isAcquiredBy` |
| `leadOperation.campaignProgression.isSuccessful` | `leadOperation.campaignProgression.isSuccessful` |
| `leadOperation.campaignProgression.newStatusID` | `leadOperation.campaignProgression.newStatusID` |
| `leadOperation.campaignProgression.newStatusName` | `leadOperation.campaignProgression.newStatusName` |
| `leadOperation.campaignProgression.oldStatusID` | `leadOperation.campaignProgression.oldStatusID` |
| `leadOperation.campaignProgression.oldStatusName` | `leadOperation.campaignProgression.oldStatusName` |
| `leadOperation.campaignProgression.reason` | `leadOperation.campaignProgression.reason` |

{style=&quot;table-layout:auto&quot;}

## Programmi {#programs}

| Set di dati sorgente | Campo di destinazione XDM | Note |
| -------------- | ---------------- | ----- |
| `id` | `campaignID` | Identità principale |
| `sfdcId` | `extSourceSystemAudit.externalID` | Identità secondaria |
| `name` | `campaignName` |
| `description` | `campaignDescription` |
| `type` | `campaignType` |
| `status` | `campaignStatus` |
| `channel` | `channelName` |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |
| `cost` | `actualCost.amount` |
| `parentProgramId` | `parentCampaignID` |
| `integrationPartner` | `integrationPartnerName` |
| `startDate` | `campaignStartDate` |
| `endDate` | `campaignEndDate` |

{style=&quot;table-layout:auto&quot;}

## Iscrizione al programma {#program-memberships}

| Set di dati sorgente | Campo di destinazione XDM | Note |
| -------------- | ---------------- | ----- |
| `id` | `campaignMemberID` | Identità principale |
| `programId` | `campaignID` | Relazione |
| `leadId` | `personID` | Relazione |
| `acquiredByCampaignID` | `acquiredByCampaignID` |
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
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |

{style=&quot;table-layout:auto&quot;}

## Aziende {#companies}

| Set di dati sorgente | Campo di destinazione XDM | Note |
| -------------- | ---------------- | ----- |
| `id` | `accountID` | Identità principale |
| `mktoCdpExternalId` | `extSourceSystemAudit.externalID` | Identità secondaria |
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

{style=&quot;table-layout:auto&quot;}

## Elenchi statici {#static-lists}

| Set di dati sorgente | Campo di destinazione XDM | Note |
| -------------- | ---------------- | ----- |
| `id` | `marketingListID` | Identità principale |
| `name` | `marketingListName` |
| `description` | `marketingListDescription` |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |

{style=&quot;table-layout:auto&quot;}

## Iscrizioni di elenchi statici {#static-list-memnberships}

| Set di dati sorgente | Campo di destinazione XDM | Note |
| -------------- | ---------------- | ----- |
| `marketingListMemberID` | `staticListMemberID` | Identità principale |
| `marketingListID` | `staticListID` | Relazione |
| `personID` | `personID` | Relazione |
| `createdAt` | `extSourceSystemAudit.createdDate` |

{style=&quot;table-layout:auto&quot;}

## Account denominati {#named-accounts}

>[!IMPORTANT]
>
>Il set di dati di account denominati è necessario solo con la funzione ABM (Account-Based Marketing) di Marketo. Se non utilizzi ABM, non è necessario impostare mappature per account denominati.

| Set di dati sorgente | Campo di destinazione XDM | Note |
| -------------- | ---------------- | ----- |
| `id` | `accountID` | Identità principale |
| `crmGuid` | `extSourceSystemAudit.externalID` | Identità secondaria |
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
| `parentAccountId` | `accountParentID` |
| `sourceType` | `accountSourceType` |

{style=&quot;table-layout:auto&quot;}

## Opportunità {#opportunities}

| Set di dati sorgente | Campo di destinazione XDM | Note |
| -------------- | ---------------- | ----- |
| `id` | `opportunityID` | Identità principale |
| `externalOpportunityId` | `extSourceSystemAudit.externalID` | Identità secondaria |
| `mktoCdpAccountOrgId` | `accountID` | Relazione |
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
| `Campaign-ID` | `campaignID` | Consigliato solo se utilizzi l’integrazione Salesforce. |
| `lastActivityDate` | `lastActivityDate` |
| `leadSource` | `leadSource` |
| `nextStep` | `nextStep` |

{style=&quot;table-layout:auto&quot;}

## Ruoli di contatto opportunità {#opportunity-contact-roles}

| Set di dati sorgente | Campo di destinazione XDM | Note |
| -------------- | ---------------- | ----- |
| `id` | `opportunityPersonID` | Identità principale |
| `mktoCdpSfdcId` | `extSourceSystemAudit.externalID` | Identità secondaria |
| `mktoCdpOpptyId` | `opportunityID` | Relazione |
| `leadId` | `personID` | Relazione |
| `role` | `personRole` |
| `isPrimary` | `isPrimary` |
| `createdAt` | `extSourceSystemAudit.createdDate` |
| `updatedAt` | `extSourceSystemAudit.lastUpdatedDate` |

{style=&quot;table-layout:auto&quot;}

## Persone {#persons}

Nel dashboard [!DNL Profiles] dell’interfaccia utente di Platform, se il valore di unione ID nel criterio di unione utilizzato per sfogliare è impostato su `None`, nella finestra delle identità collegate verrà visualizzato solo l’attributo di identità principale.

Come soluzione alternativa, è possibile aggiornare il campo di unione ID da `None` a `Private graph` per visualizzare tutte le identità collegate a una [!DNL Profile]. In alternativa, è possibile creare un nuovo criterio di unione oppure utilizzare un criterio di unione diverso contenente un valore di unione ID impostato su `Private graph`. Se si sceglie di creare un nuovo criterio di unione o di utilizzare un criterio di unione diverso, è necessario assicurarsi che il criterio contenga lo stesso tipo di schema utilizzato per il set di mapping [!DNL Marketo] Persone. Per ulteriori informazioni, consulta la [guida all&#39;interfaccia utente dei criteri di unione](../../../../profile/ui/merge-policies.md).

| Set di dati sorgente | Campo di destinazione XDM | Note |
| -------------- | ---------------- | ----- |
| `id` | `personID` | Identità principale |
| `emailSuspended` | `b2b.personOptInOut._channels.email` |
| `emailSuspendedAt` | `b2b.personOptInOut.optOutDetails.email.optOutDate` |
| `emailSuspendedCause` | `b2b.personOptInOut.optOutDetails.email.optOutReason` |
| `contactCompany` | `b2b.accountID` |
| `marketingSuspended` | `b2b.isMarketingSuspended` |
| `marketingSuspendedCause` | `b2b.marketingSuspendedCause` |
| `leadScore` | `b2b.personScore` |
| `leadSource` | `b2b.personSource` |
| `leadStatus` | `b2b.personStatus` |
| `personType` | `b2b.personType` |
| `leadPartitionId` | `b2b.personGroupID` |
| `mktoCdpCnvContactPersonId` | `b2b.convertedContactID` |
| `mktoCdpIsConverted` | `b2b.isConverted` |
| `mktoCdpConvertedDate` | `b2b.convertedDate` |
| `sfdcId` | `extSourceSystemAudit.externalID` | Identità secondaria |
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
| `company` | `organizations` |
| `leadScore` | `personComponents.personScore` |
| `leadSource` | `personComponents.personSource` |
| `leadStatus` | `personComponents.personStatus` |
| `personType` | `personComponents.personType` |
| `leadPartitionId` | `personComponents.personGroupID` |
| `mktoCdpCnvContactPersonId` | `personComponents.sourceConvertedContactID` |
| `contactCompany` | `personComponents.sourceAccountID` |
| `sfdcContactId` | `personComponents.sourceExternalID` | Consigliato solo se utilizzi l’integrazione Salesforce. |
| `id` | `personComponents.sourcePersonID` |
| `email` | `personComponents.workEmail.address` |
| `email` | `workEmail.address` |

{style=&quot;table-layout:auto&quot;}

## Passaggi successivi

Leggendo questo documento, hai acquisito informazioni sulla relazione di mappatura tra i set di dati [!DNL Marketo] e i campi XDM corrispondenti. Per completare il flusso di dati [!DNL Marketo], consulta l’esercitazione su [creazione di una connessione [!DNL Marketo] sorgente](../../../tutorials/ui/create/adobe-applications/marketo.md) .
