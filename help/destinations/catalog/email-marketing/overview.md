---
keywords: e-mail;e-mail;e-mail;destinazioni e-mail
title: Panoramica delle destinazioni di e-mail marketing
type: Tutorial
description: I provider di servizi e-mail (ESP) ti consentono di gestire le attività di e-mail marketing, ad esempio per l’invio di campagne e-mail promozionali.
exl-id: e07f8c5a-0424-4de5-810f-3d5711ef4606
source-git-commit: ccbc633bfce8f4f66577b50064c28cfc26cb6dca
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 4%

---

# Panoramica delle destinazioni di e-mail marketing {#email-marketing-destinations}

## Panoramica {#overview}

I provider di servizi e-mail (ESP) ti consentono di gestire le attività di e-mail marketing, ad esempio l’invio di campagne e-mail promozionali. Adobe Experience Platform si integra con gli ESP consentendo di attivare i segmenti nelle destinazioni di e-mail marketing.

Platform esporta i segmenti come `.csv` e li distribuisce nella posizione desiderata. Pianifica l’importazione dei dati nella piattaforma di e-mail marketing dalla posizione di archiviazione abilitata in [!DNL Platform]. Il processo di importazione dei dati varia a seconda del partner. Per ulteriori informazioni, leggi gli articoli sulle singole destinazioni.

## Destinazioni di e-mail marketing supportate {#supported-destinations}

Adobe Experience Platform supporta le seguenti destinazioni di e-mail marketing:

* [Adobe Campaign](adobe-campaign.md)
* [Eloqua Oracle](oracle-eloqua.md)
* [Responsys Oracle](oracle-responsys.md)
* [Marketing Cloud Salesforce](salesforce-marketing-cloud.md)
* [InviaGriglia](sendgrid.md)

## Connettersi a una nuova destinazione di e-mail marketing {#connect-destination}

Per inviare segmenti a destinazioni di e-mail marketing per le campagne, Platform deve prima connettersi alla destinazione. Consulta la [tutorial sulla creazione della destinazione](../../ui/connect-destination.md) per informazioni dettagliate sulla configurazione di una nuova destinazione.

## Best practice per l’attivazione dei tipi di pubblico nelle destinazioni di e-mail marketing {#best-practices}

### Selezione identità {#identity}

L’Adobe consiglia di selezionare un identificatore univoco dal [schema di unione](../../../profile/home.md#profile-fragments-and-union-schemas). Questo è il campo da cui le identità utente sono ricavate. Nella maggior parte dei casi, questo campo è l’indirizzo e-mail, ma può anche essere un ID programma fedeltà o un numero di telefono. Fai riferimento alla tabella seguente per gli identificatori univoci più comuni e il relativo campo XDM nello schema.

| Identificatore univoco | Campo XDM nello schema unificato |
|----------------- | ---------------------------|
| Indirizzo e-mail | `personalEmail.address` |
| Telefono | `mobilePhone.number` |
| ID programma fedeltà | `Customer-defined XDM field` |

### Altri attributi di destinazione

Nel selettore campo Schema, scegli gli altri campi da esportare nella destinazione e-mail. Alcune opzioni consigliate sono:

| Schema | Campo XDM |
|------ | ---------|
| Nome | `person.name.firstName` |
| Cognome | `person.name.lastName` |
| Telefono | `mobilePhone.number` |
| Città indirizzo | `homeAddress.city` |
| Stato indirizzo | `homeAddress.stateProvince` |
| Indirizzo Codice postale | `homeAddress.postalCode` |
| Compleanno | `person.birthDayAndMonth` |
| Appartenenza a un segmento | `segmentMembership.status` |

## Importare dati dalla posizione di archiviazione alla destinazione {#import-data-into-destination}

Leggi i singoli articoli sulle destinazioni di e-mail marketing per scoprire come importare i dati dalla posizione di archiviazione alle destinazioni:

* [Adobe Campaign](adobe-campaign.md)
* [Eloqua Oracle](oracle-eloqua.md)
* [Responsys Oracle](oracle-responsys.md)
* [Marketing Cloud Salesforce](salesforce-marketing-cloud.md)

## Attivare i segmenti nelle destinazioni di e-mail marketing {#activate}

Per istruzioni su come attivare i segmenti nelle destinazioni di e-mail marketing, consulta [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](../../ui/activate-batch-profile-destinations.md).

## Risorse aggiuntive

* [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](../../ui/activate-batch-profile-destinations.md)
* [Creare destinazioni di e-mail marketing e attivare i dati utilizzando l’API del servizio di flusso](../../api/connect-activate-batch-destinations.md)
