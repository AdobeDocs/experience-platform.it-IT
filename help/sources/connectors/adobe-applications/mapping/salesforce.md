---
keywords: Experience Platform;home;argomenti popolari;Salesforce;salesforce;mappatura campo;mappatura campo;mappatura;marketo;B2B;b2b
title: Campi di mappatura Salesforce
description: Le tabelle seguenti contengono le mappature tra i campi di origine Salesforce e i campi XDM corrispondenti.
exl-id: 33ee76f2-0495-4acd-a862-c942c0fa3177
source-git-commit: 5e93a86d6bdbf66e6b4991e0e2bc4d3dfe90d2b5
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 8%

---

# [!DNL Salesforce] mappature dei campi

Le tabelle seguenti contengono le mappature tra [!DNL Salesforce] i campi di origine e i campi corrispondenti di Experience Data Model (XDM).

## Contatto {#contact}

Leggi la sezione [Panoramica del profilo individuale XDM](../../../../xdm/classes/individual-profile.md) per ulteriori informazioni sulla classe XDM. Per ulteriori informazioni sui gruppi di campi XDM, consulta la [Gruppo di campi di schema Dettagli persona commerciale XDM](../../../../xdm/field-groups/profile/business-person-details.md) guida e [Gruppo di campi di schema Componenti per Business Person XDM](../../../../xdm/field-groups/profile/business-person-components.md) guida.

| Campo di origine | Percorso del campo XDM di Target | Note |
| --- | --- | --- |
| `AccountId` | `b2b.accountKey.sourceID` |
| `iif(AccountId != null && AccountId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(AccountId,"@${CRM_ORG_ID}.Salesforce")), null)` | `b2b.accountKey` |
| `iif(AccountId != null && AccountId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}","sourceID", AccountId, "sourceKey", concat(AccountId,"@${CRM_ORG_ID}.Salesforce")), null)` | `personComponents.sourceAccountKey` |
| `"Salesforce"` | `b2b.personKey.sourceType` |
| `"${CRM_ORG_ID}"` | `b2b.personKey.sourceInstanceID` | Valore per `"${CRM_ORG_ID}"` verrà sostituito automaticamente. |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `b2b.personKey.sourceKey` | Identità principale. Valore per `"${CRM_ORG_ID}"` verrà sostituito automaticamente. |
| `AssistantName` | `extendedWorkDetails.assistantDetails.name.fullName` |
| `AssistantPhone` | `extendedWorkDetails.assistantDetails.phone.number` |
| `Birthdate` | `person.birthDate` |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |
| `Department` | `extendedWorkDetails.departments` |
| `Email` | `workEmail.address` | Identità secondaria. |
| `Email` | `personComponents.workEmail.address` |
| `Fax` | `faxPhone.number` |
| `FirstName` | `person.name.firstName` |
| `HomePhone` | `homePhone.number` |
| `isDeleted` | `isDeleted` |
| `Id` | `b2b.personKey.sourceID` |
| `"Salesforce"` | `personComponents.sourcePersonKey.sourceType` |
| `"${CRM_ORG_ID}"` | `personComponents.sourcePersonKey.sourceInstanceID` |
| `Id` | `personComponents.sourcePersonKey.sourceID` |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `personComponents.sourcePersonKey.sourceKey` |
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
| `"Contact"` | `b2b.personType` |

{style=&quot;table-layout:auto&quot;}

## Lead {#lead}

Leggi la sezione [Panoramica del profilo individuale XDM](../../../../xdm/classes/individual-profile.md) per ulteriori informazioni sulla classe XDM. Per ulteriori informazioni sui gruppi di campi XDM, consulta la [Gruppo di campi di schema Dettagli persona commerciale XDM](../../../../xdm/field-groups/profile/business-person-details.md) guida e [Gruppo di campi di schema Componenti per Business Person XDM](../../../../xdm/field-groups/profile/business-person-components.md) guida.

| Campo di origine | Percorso del campo XDM di Target | Note |
| --- | --- | --- |
| `City` | `workAddress.city` |
| `ConvertedDate` | `b2b.convertedDate` |
| `Country` | `workAddress.country` |
| `Email` | `workEmail.address` | Identità secondaria. |
| `Email` | `personComponents.workEmail.address` |
| `Fax` | `faxPhone.number` |
| `FirstName` | `person.name.firstName` |
| `IsConverted` | `b2b.isConverted` |
| `isDeleted` | `isDeleted` |
| `"Salesforce"` | `b2b.personKey.sourceType` |
| `"${CRM_ORG_ID}"` | `b2b.personKey.sourceInstanceID` |
| `Id` | `b2b.personKey.sourceID` |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `b2b.personKey.sourceKey` | Identità principale. Valore per `"${CRM_ORG_ID}"` verrà sostituito automaticamente. |
| `"Salesforce"` | `personComponents.sourcePersonKey.sourceType` |
| `"${CRM_ORG_ID}"` | `personComponents.sourcePersonKey.sourceInstanceID` |
| `Id` | `personComponents.sourcePersonKey.sourceID` |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `personComponents.sourcePersonKey.sourceKey` |
| `LastActivityDate` | `extSourceSystemAudit.lastActivityDate` |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |
| `LastName` | `person.name.lastName` |
| `LastReferencedDate` | `extSourceSystemAudit.lastReferencedDate` |
| `LastViewedDate` | `extSourceSystemAudit.lastViewedDate` |
| `LeadSource` | `b2b.personSource` |
| `LeadSource` | `personComponents.personSource` |
| `Latitude` | `workAddress._schema.latitude` |
| `Longitude` | `workAddress._schema.longitude` |
| `Name` | `person.name.fullName` |
| `PostalCode` | `workAddress.postalCode` |
| `Salutation` | `person.name.courtesyTitle` |
| `State` | `workAddress.state` |
| `Status` | `b2b.personStatus` |
| `Status` | `personComponents.personStatus` |
| `Street` | `workAddress.street1` |
| `Title` | `extendedWorkDetails.jobTitle` |
| `Suffix` | `person.name.suffix` |
| `Company` | `b2b.companyName` |
| `Website` | `b2b.companyWebsite` |
| `ConvertedContactId` | `b2b.convertedContactKey.sourceID` |
| `iif(ConvertedContactId != null && ConvertedContactId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(ConvertedContactId,"@${CRM_ORG_ID}.Salesforce")), null)` | `b2b.convertedContactKey` |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |
| `"Lead"` | `b2b.personType` |
| `iif(ConvertedContactId != null && ConvertedContactId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceID", ConvertedContactId, "sourceKey", concat(ConvertedContactId,"@${CRM_ORG_ID}.Salesforce")), null)` | `personComponents.sourceConvertedContactKey` |

{style=&quot;table-layout:auto&quot;}

## Account {#account}

Leggi la sezione [Panoramica dei dettagli dell&#39;account aziendale XDM](../../../../xdm/classes/b2b/business-account.md) per ulteriori informazioni sulla classe XDM.

| Campo di origine | Percorso del campo XDM di Target | Note |
| --- | --- | --- |
| `"Salesforce"` | `accountKey.sourceType` |
| `"${CRM_ORG_ID}"` | `accountKey.sourceInstanceID` | Valore per `"${CRM_ORG_ID}"` verrà sostituito automaticamente. |
| `AccountNumber` | `accountNumber` |
| `AccountSource` | `accountSourceType` |
| `AnnualRevenue` | `accountOrganization.annualRevenue.amount` |
| `BillingCity` | `accountBillingAddress.city` |
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
| `isDeleted` | `isDeleted` |
| `Id` | `accountKey.sourceID` |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `accountKey.sourceKey` | Identità principale. Valore per `"${CRM_ORG_ID}"` verrà sostituito automaticamente. |
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
| `ParentId` | `accountParentKey.sourceID` |
| `iif(ParentId != null && ParentId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(ParentId,"@${CRM_ORG_ID}.Salesforce")), null)` | `accountParentKey` |
| `Phone` | `accountPhone.number` |
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
| `Website` | `accountOrganization.website` |

{style=&quot;table-layout:auto&quot;}

## Opportunità {#opportunity}

Leggi la sezione [Panoramica sulle opportunità aziendali XDM](../../../../xdm/classes/b2b/business-opportunity.md) per ulteriori informazioni sulla classe XDM.

| Campo di origine | Percorso del campo XDM di Target | Note |
| --- | --- | --- |
| `"Salesforce"` | `opportunityKey.sourceType` |
| `"${CRM_ORG_ID}"` | `opportunityKey.sourceInstanceID` | Valore per `"${CRM_ORG_ID}"` verrà sostituito automaticamente. |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `opportunityKey.sourceKey` | Identità principale. Valore per `"${CRM_ORG_ID}"` verrà sostituito automaticamente. |
| `AccountId` | `accountKey.sourceID` |
| `iif(AccountId != null && AccountId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(AccountId,"@${CRM_ORG_ID}.Salesforce")), null)` | `accountKey` | Relazione. |
| `Amount` | `opportunityAmount.amount` |
| `CampaignId` | `campaignKey.sourceID` |
| `iif(CampaignId != null && CampaignId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(CampaignId,"@${CRM_ORG_ID}.Salesforce")), null)` | `campaignKey` |
| `CloseDate` | `expectedCloseDate` |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |
| `Description` | `opportunityDescription` |
| `ExpectedRevenue` | `expectedRevenue.amount` |
| `FiscalQuarter` | `fiscalQuarter` |
| `FiscalYear` | `fiscalYear` |
| `ForecastCategory` | `forecastCategory` |
| `ForecastCategoryName` | `forecastCategoryName` |
| `Id` | `opportunityKey.sourceID` |
| `IsClosed` | `isClosed` |
| `isDeleted` | `isDeleted` |
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
| `CurrencyIsoCode` | `opportunityAmount.currencyCode` |

{style=&quot;table-layout:auto&quot;}

## Ruolo di contatto opportunità {#opportunity-contact-role}

Leggi la sezione [Panoramica sulla classe di relazione tra persone opportunità aziendali XDM](../../../../xdm/classes/b2b/business-opportunity-person-relation.md) per ulteriori informazioni sulla classe XDM.

| Campo di origine | Percorso del campo XDM di Target | Note |
| --- | --- | --- |
| `"Salesforce"` | `opportunityPersonKey.sourceType` |
| `"${CRM_ORG_ID}"` | `opportunityPersonKey.sourceInstanceID` | Valore per `"${CRM_ORG_ID}"` verrà sostituito automaticamente. |
| `"Salesforce"` | `personKey.sourceType` |
| `"${CRM_ORG_ID}"` | `personKey.sourceInstanceID` |
| `ContactId` | `personKey.sourceID` |
| `concat(ContactId,"@${CRM_ORG_ID}.Salesforce")` | `personKey.sourceKey` |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |
| `Id` | `opportunityPersonKey.sourceID` |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `opportunityPersonKey.sourceKey` | Identità principale. Valore per `"${CRM_ORG_ID}"` verrà sostituito automaticamente. |
| `isDeleted` | `isDeleted` |
| `IsPrimary` | `isPrimary` |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |
| `"Salesforce"` | `opportunityKey.sourceType` |
| `"${CRM_ORG_ID}"` | `opportunityKey.sourceInstanceID` |
| `OpportunityId` | `opportunityKey.sourceID` |
| `concat(OpportunityId,"@${CRM_ORG_ID}.Salesforce")` | `opportunityKey.sourceKey` |
| `Role` | `personRole` |

{style=&quot;table-layout:auto&quot;}

## Campaign {#campaign}

Leggi la sezione [Panoramica sulla classe di Business Campaign XDM](../../../../xdm/classes/b2b/business-campaign.md) per ulteriori informazioni sulla classe XDM. Per ulteriori informazioni sui gruppi di campi XDM, consulta la [Gruppo di campi schema dettagli campagna aziendale XDM](../../../../xdm/field-groups/b2b-campaign/details.md) guida.

| Campo di origine | Percorso del campo XDM di Target | Note |
| --- | --- | --- |
| `"Salesforce"` | `campaignKey.sourceType` |
| `"${CRM_ORG_ID}"` | `campaignKey.sourceInstanceID` | Valore per `"${CRM_ORG_ID}"` verrà sostituito automaticamente. |
| `isDeleted` | `isDeleted` |
| `Id` | `campaignKey.sourceID` |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `campaignKey.sourceKey` | Identità principale. Valore per `"${CRM_ORG_ID}"` verrà sostituito automaticamente. |
| `Name` | `campaignName` |
| `ParentId` | `parentCampaignKey.sourceID` |
| `iif(ParentId != null && ParentId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(ParentId,"@${CRM_ORG_ID}.Salesforce")), null)` | `parentCampaignKey` |
| `Type` | `campaignType` |
| `Status` | `campaignStatus` |
| `StartDate` | `campaignStartDate` |
| `EndDate` | `campaignEndDate` |
| `ExpectedRevenue` | `expectedRevenue.amount` |
| `BudgetedCost` | `budgetedCost.amount` |
| `ActualCost` | `actualCost.amount` |
| `ExpectedResponse` | `expectedResponse` |
| `IsActive` | `isActive` |
| `Description` | `campaignDescription` |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |
| `LastActivityDate` | `extSourceSystemAudit.lastActivityDate` |
| `LastViewedDate` | `extSourceSystemAudit.lastViewedDate` |
| `LastReferencedDate` | `extSourceSystemAudit.lastReferencedDate` |
| `CurrencyIsoCode` | `actualCost.currencyCode` |

## Membro della campagna {#campaign-member}

Leggi la sezione [Panoramica dei membri della campagna aziendale XDM](../../../../xdm/classes/b2b/business-campaign-members.md) per ulteriori informazioni sulla classe XDM. Per ulteriori informazioni sui gruppi di campi XDM, consulta la [Gruppo di campi schema dettagli membri di campagna aziendale XDM](../../../../xdm/field-groups/b2b-campaign/details.md) documento.

| Campo di origine | Percorso del campo XDM di Target | Note |
| --- | --- | --- |
| `"Salesforce"` | `campaignMemberKey.sourceType` |
| `"${CRM_ORG_ID}"` | `campaignMemberKey.sourceInstanceID` | Valore per `"${CRM_ORG_ID}"` verrà sostituito automaticamente. |
| `isDeleted` | `isDeleted` |
| `Id` | `campaignMemberKey.sourceID` |
| `concat(Id,"@${CRM_ORG_ID}.Salesforce")` | `campaignMemberKey.sourceKey` | Identità principale. Valore per `"${CRM_ORG_ID}"` verrà sostituito automaticamente. |
| `"Salesforce"` | `campaignKey.sourceType` |
| `${CRM_ORG_ID}` | `campaignKey.sourceInstanceID` |
| `CampaignId` | `campaignKey.sourceID` |
| `concat(CampaignId,"@${CRM_ORG_ID}.Salesforce")` | `campaignKey.sourceKey` |
| `"Salesforce"` | `personKey.sourceType` |
| `${CRM_ORG_ID}` | `personKey.sourceInstanceID` |
| `LeadOrContactId` | `personKey.sourceID` |
| `concat(LeadOrContactId,"@${CRM_ORG_ID}.Salesforce")` | `personKey.sourceKey` |
| `Status` | `memberStatus` |
| `HasResponded` | `hasResponded` |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |
| `FirstRespondedDate` | `firstRespondedDate` |
| `Type` | `b2b.personType` |

## Relazione di contatto dell&#39;account {#account-contact-relation}

Leggi la sezione [Classe di relazione tra persone dell&#39;account aziendale XDM](../../../../xdm/classes/b2b/business-account-person-relation.md) per ulteriori informazioni sulla classe XDM.

| Campo di origine | Percorso del campo XDM di Target | Note |
| --- | --- | --- |
| `AccountId` | `accountKey.sourceID` |
| `iif(AccountId != null && AccountId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(AccountId,"@${CRM_ORG_ID}.Salesforce")), null)` | `accountKey` |
| `ContactId` | `personKey.sourceID` |
| `iif(ContactId != null && ContactId != "", to_object("sourceType", "Salesforce", "sourceInstanceID", "${CRM_ORG_ID}", "sourceKey", concat(ContactId,"@${CRM_ORG_ID}.Salesforce")), null)` | `personKey` |
| `CreatedById` | `extSourceSystemAudit.createdBy` |
| `CreatedDate` | `extSourceSystemAudit.createdDate` |
| `EndDate` | `relationEndDate` |
| `IsDeleted` | `isDeleted` |
| `Id` | `accountPersonKey.sourceID` |
| `"Salesforce"` | `accountPersonKey.sourceType` |
| `"${CRM_ORG_ID}"` | `accountPersonKey.sourceInstanceID` |
| `concat(Id, "@${CRM_ORG_ID}.Salesforce")` | `accountPersonKey.sourceKey` | Identità principale. |
| `IsActive` | `IsActive` |
| `IsDirect` | `IsDirect` |
| `LastModifiedById` | `extSourceSystemAudit.lastUpdatedBy` |
| `LastModifiedDate` | `extSourceSystemAudit.lastUpdatedDate` |
| `explode(Roles,";")` | `personRoles[]` |
| `StartDate` | `relationStartDate` |

## Passaggi successivi

Leggendo questo documento, hai acquisito informazioni sulla relazione di mappatura tra [!DNL Salesforce] i campi di origine e i campi XDM corrispondenti. Consulta la documentazione su [creazione di un [!DNL Salesforce] connessione sorgente](../../../connectors/crm/salesforce.md) per ulteriori informazioni.
