---
keywords: Experience Platform;home;argomenti popolari;Salesforce;salesforce;mappatura campo;mappatura campo;mappatura;marketo;B2B;b2b
solution: Experience Platform
title: Campi di mappatura Salesforce
topic-legacy: overview
description: Le tabelle seguenti contengono le mappature tra i campi di origine Salesforce e i campi XDM corrispondenti.
source-git-commit: 00207ae10979b48d190cbda63aecf55e0f6d0f9c
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 13%

---

# [!DNL Salesforce] mappature dei campi

Le tabelle seguenti contengono le mappature tra i campi di origine [!DNL Salesforce] e i relativi campi Experience Data Model (XDM) corrispondenti.

## Contatto {#contact}

| Campo di origine | Percorso del campo XDM di Target | Note |
| --- | --- | --- |
| `AccountId` | `b2b.accountID` |
| `AccountId` | `personComponents.sourceAccountID` |
| `AssistantName` | `extendedWorkDetails.assistantDetails.name.fullName` |
| `AssistantPhone` | `extendedWorkDetails.assistantDetails.phone.number` |
| `Birthdate` | `person.birthDate` |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |
| `Department` | `extendedWorkDetails.departments` |
| `Email` | `workEmail.address` | Questa è l&#39;identità secondaria. |
| `Email` | `personComponents.workEmail.address` |
| `Fax` | `faxPhone.number` |
| `FirstName` | `person.name.firstName` |
| `HomePhone` | `homePhone.number` |
| `Id` | `personID` | Questa è l&#39;identità principale |
| `Id` | `personComponents.sourcePersonID` |
| `LastActivityDate` | `extSourceSystemAudit.lastActivityDate` |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |
| `LastName` | `person.name.lastName` |
| `LastReferencedDate` | `extSourceSystemAudit.lastReferencedDate` |
| `LastViewedDate` | `extSourceSystemAudit.lastViewedDate` |
| `LeadSource` | `b2b.personSource` |
| `LeadSource` | `personComponents.personSource` |
| `MailingCity` | `workAddress.city` |
| `MailingCountry` | `workAddress.country` |
| `MailingLatitude` | `workAddress._schema.latitude` |
| `MailingLongitude` | `workAddress._schema.longitude` |
| `MailingPostalCode` | `workAddress.postalCode` |
| `MailingState` | `workAddress.state` |
| `MailingStreet` | `workAddress.street1` |
| `MobilePhone` | `mobilePhone.number` |
| `Name` | `person.name.fullName` |
| `OtherCity` | `otherAddress.city` |
| `OtherCountry` | `otherAddress.country` |
| `OtherLatitude` | `otherAddress._schema.latitude` |
| `OtherLongitude` | `otherAddress._schema.longitude` |
| `OtherPhone` | `otherPhone.number` |
| `OtherPostalCode` | `otherAddress.postalCode` |
| `OtherState` | `otherAddress.state` |
| `OtherStreet` | `otherAddress.street1` |
| `Phone` | `workPhone.number` |
| `ReportsToId` | `extendedWorkDetails.reportsToID` |
| `Salutation` | `person.name.courtesyTitle` |
| `Title` | `extendedWorkDetails.jobTitle` |

{style=&quot;table-layout:auto&quot;}

## Lead {#lead}

| Campo di origine | Percorso del campo XDM di Target | Note |
| --- | --- | --- |
| `City` | `workAddress.city` |
| `ConvertedContactId` | `b2b.convertedContactID` |
| `ConvertedContactId` | `personComponents.sourceConvertedContactID` |
| `ConvertedDate` | `b2b.convertedDate` |
| `Country` | `workAddress.country` |
| `Email` | `workEmail.address` | Questa è l&#39;identità secondaria |
| `Email` | `personComponents.workEmail.address` |
| `Fax` | `faxPhone.number` |
| `FirstName` | `person.name.firstName` |
| `IsConverted` | `b2b.isConverted` |
| `Id` | `personID` | Questa è l&#39;identità principale |
| `Id` | `personComponents.sourcePersonID` |
| `LastActivityDate` | `extSourceSystemAudit.lastActivityDate` |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |
| `LastName` | `person.name.lastName` |
| `LastReferencedDate` | `extSourceSystemAudit.lastReferencedDate` |
| `LastViewedDate` | `extSourceSystemAudit.lastViewedDate` |
| `LeadSource` | `b2b.personSource` |
| `LeadSource` | `personComponents.personSource` |
| `Latitude` | `workAddress._schema.latitude` |
| `Longitude` | `workAddress._schema.longitude` |
| `MiddleName` | `person.name.middleName` |
| `Name` | `person.name.fullName` |
| `PostalCode` | `workAddress.postalCode` |
| `Salutation` | `person.name.courtesyTitle` |
| `State` | `workAddress.state` |
| `Status` | `b2b.personStatus` |
| `Status` | `personComponents.personStatus` |
| `Street` | `workAddress.street1` |
| `Title` | `extendedWorkDetails.jobTitle` |
| `Suffix` | `person.name.suffix` |

{style=&quot;table-layout:auto&quot;}

## Account {#account}

| Campo di origine | Percorso del campo XDM di Target | Note |
| --- | --- | --- |
| `AccountNumber` | `accountNumber` |
| `AccountSource` | `accountSourceType` |
| `AnnualRevenue` | `accountOrganization.annualRevenue.amount` |
| `BillingCity` | indirizzo | `accountBillingAddress.city` |
| `BillingCountry` | `accountBillingAddress.country` |
| `BillingLatitude` | `accountBillingAddress._schema.latitude` |
| `BillingLongitude` | `accountBillingAddress._schema.longitude` |
| `BillingPostalCode` | `accountBillingAddress.postalCode` |
| `BillingState` | `accountBillingAddress.state` |
| `BillingStreet` | `accountBillingAddress.street1` |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |
| `Description` | `accountDescription` |
| `DunsNumber` | `accountOrganization.DUNSNumber` | funzionalità data.com |
| `Fax` | `accountFax.number` |
| `Id` | `accountID` | Questa è l&#39;identità principale |
| `Industry` | `accountOrganization.industry` |
| `Jigsaw` | `accountOrganization.jigsaw` |
| `LastActivityDate` | `extSourceSystemAudit.lastActivityDate` |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |
| `LastReferencedDate` | `extSourceSystemAudit.lastReferencedDate` |
| `LastViewedDate` | `extSourceSystemAudit.lastViewedDate` |
| `NaicsCode` | `accountOrganization.NAICSCode` | funzionalità data.com |
| `NaicsDesc` | `accountOrganization.NAICSDescription` | funzionalità data.com |
| `Name` | `accountName` |
| `NumberOfEmployees` | `accountOrganization.numberOfEmployees` |
| `Ownership` | `accountOwnership` |
| `ParentId` | `accountParentID` |
| `Phone` | `accountPhone.number` |
| `Rating` | `accountOrganization.rating` |
| `ShippingCity` | `accountShippingAddress.city` |
| `ShippingCountry` | `accountShippingAddress.country` |
| `ShippingLatitude` | `accountShippingAddress._schema.latitude` |
| `ShippingLongitude` | `accountShippingAddress._schema.longitude` |
| `ShippingPostalCode` | `accountShippingAddress.postalCode` |
| `ShippingState` | `accountShippingAddress.state` |
| `ShippingStreet` | `accountShippingAddress.street1` |
| `Sic` | `accountOrganization.SICCode` |
| `SicDesc` | `accountOrganization.SICDescription` |
| `Site` | `accountSite` |
| `TickerSymbol` | `accountOrganization.tickerSymbol` |
| `Tradestyle` | `accountTradeStyle` | funzionalità data.com |
| `Type` | `accountType` |

{style=&quot;table-layout:auto&quot;}

## Opportunità {#opportunity}

| Campo di origine | Percorso del campo XDM di Target | Note |
| --- | --- | --- |
| `AccountId` | `accountID` | Relazione |
| `Amount` | `opportunityAmount.amount` |
| `CampaignId` | `campaignID` |
| `CloseDate` | `actualCloseDate` / `expectedCloseDate` |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |
| `Description` | `opportunityDescription` |
| `ExpectedRevenue` | `expectedRevenue.amount` |
| `FiscalQuarter` | `fiscalQuarter` |
| `FiscalYear` | `fiscalYear` |
| `ForecastCategory` | `forecastCategory` |
| `ForecastCategoryName` | `forecastCategoryName` |
| `Id` | `opportunityID` | Questa è l&#39;identità principale |
| `IsClosed` | `isClosed` |
| `IsWon` | `isWon` |
| `LastActivityDate` | `extSourceSystemAudit.lastActivityDate` |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |
| `LastReferencedDate` | `extSourceSystemAudit.lastReferencedDate` |
| `LastViewedDate` | `extSourceSystemAudit.lastViewedDate` |
| `LeadSource` | `leadSource` |
| `Name` | `opportunityName` |
| `NextStep` | `nextStep` |
| `Probability` | `probabilityPercentage` |
| `StageName` | `opportunityStage` |
| `TotalOpportunityQuantity` | `opportunityQuantity` |
| `Type` | `opportunityType` |

{style=&quot;table-layout:auto&quot;}

## Ruolo di contatto opportunità {#opportunity-contact-role}

| Campo di origine | Percorso del campo XDM di Target | Note |
| --- | --- | --- |
| `ContactId` | `personID` | Relazione |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |
| `Id` | `opportunityPersonID` | Questa è l&#39;identità principale |
| `IsPrimary` | `isPrimary` |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |
| `OpportunityId` | `opportunityID` | Relazione |
| `Role` | `personRole` |

{style=&quot;table-layout:auto&quot;}

## Campaign {#campaign}

| Campo di origine | Percorso del campo XDM di Target | Note |
| --- | --- | --- |
| `Id` | `xdm: campaignID` | Questa è l&#39;identità principale |
| `Name` | `xdm: campaignName` |
| `ParentId` | `xdm: parentCampaignID` |
| `Type` | `xdm: campaignType` |
| `Status` | `xdm: campaignStatus` |
| `StartDate` | `xdm: campaignStartDate` |
| `EndDate` | `xdm: campaignEndDate` |
| `ExpectedRevenue` | `xdm: expectedRevenue.amount` |
| `BudgetedCost` | `xdm: budgetedCost.amount` |
| `ActualCost` | `xdm: actualCost.amount` |
| `ExpectedResponse` | `xdm: expectedResponse` |
| `IsActive` | `xdm: isActive` |
| `Description` | `xdm: campaignDescription` |
| `CreatedDate` | `xdm: extSourceSystemAudit.createdDate` |
| `LastModifiedDate` | `xdm: extSourceSystemAudit.lastUpdatedDate` |
| `LastActivityDate` | `xdm: extSourceSystemAudit.lastActivityDate` |
| `LastViewedDate` | `xdm: extSourceSystemAudit.lastViewedDate` |
| `LastReferencedDate` | `xdm: extSourceSystemAudit.lastReferencedDate` |

## Membro della campagna {#campaign-member}

| Campo di origine | Percorso del campo XDM di Target | Note |
| --- | --- | --- |
| `Id` | `campaignMemberID` | Questa è l&#39;identità principale |
| `CampaignId` | `campaignID` | Relazione |
| `LeadOrContactId` | `personID` | Relazione |
| `Status` | `memberStatus` |
| `HasResponded` | `hasResponded` |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |
| `FirstRespondedDate` | `firstRespondedDate` |

## Passaggi successivi

Leggendo questo documento, hai acquisito informazioni sulla relazione di mappatura tra i campi di origine [!DNL Salesforce] e i campi XDM corrispondenti. Per avviare il flusso di dati [!DNL Salesforce], consulta l’esercitazione su [creazione di una connessione sorgente [!DNL Salesforce]  .](../../../tutorials/ui/create/crm/salesforce.md)
