---
keywords: e-mail;e-mail;e-mail;destinazioni e-mail
title: Panoramica delle destinazioni di e-mail marketing
type: Tutorial
description: I provider di servizi e-mail (ESP) ti consentono di gestire le attività di e-mail marketing, ad esempio per l’invio di campagne e-mail promozionali. Scopri quali ESP sono supportati come destinazioni di Experience Platform.
exl-id: e07f8c5a-0424-4de5-810f-3d5711ef4606
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 4%

---

# Panoramica delle destinazioni di e-mail marketing {#email-marketing-destinations}

## Panoramica {#overview}

I provider di servizi e-mail (ESP) ti consentono di gestire le attività di e-mail marketing, ad esempio l’invio di campagne e-mail promozionali. Adobe Experience Platform si integra con gli ESP consentendo di attivare i tipi di pubblico nelle destinazioni del marketing via e-mail.

## Destinazioni di e-mail marketing supportate {#supported-destinations}

Adobe Experience Platform supporta le seguenti destinazioni di e-mail marketing:

* [Adobe Campaign](adobe-campaign.md)
* [Adobe Campaign Managed Cloud Services](adobe-campaign-managed-services.md)
* [Categorie di interesse Mailchimp](mailchimp-interest-categories.md)
* [Eloqua Oracle (API)](oracle-eloqua-api.md)
* [(API) [!DNL Salesforce Marketing Cloud]](salesforce-marketing-cloud-exact-target.md)
* [(File) Oracle Eloqua](oracle-eloqua.md)
* [(File) [!DNL Salesforce Marketing Cloud]](salesforce-marketing-cloud.md)
* [[!DNL Salesforce Marketing Cloud Account Engagement]](salesforce-marketing-cloud-account-engagement.md)
* [Responsys Oracle](oracle-responsys.md)
* [InviaGriglia](sendgrid.md)

## Connettersi a una nuova destinazione di e-mail marketing {#connect-destination}

Per inviare i tipi di pubblico a destinazioni di e-mail marketing per le campagne, Platform deve prima connettersi alla destinazione. Consulta la [tutorial sulla creazione della destinazione](../../ui/connect-destination.md) per informazioni dettagliate sulla configurazione di una nuova destinazione.

## Best practice per l’attivazione dei tipi di pubblico nelle destinazioni di e-mail marketing {#best-practices}

### Selezione identità {#identity}

L’Adobe consiglia di selezionare un identificatore univoco dal [schema di unione](../../../profile/home.md#profile-fragments-and-union-schemas). Questo è il campo da cui le identità utente sono ricavate. Nella maggior parte dei casi, questo campo è l’indirizzo e-mail, ma può anche essere un ID programma fedeltà o un numero di telefono. Fai riferimento alla tabella seguente per gli identificatori univoci più comuni e il relativo campo XDM nello schema.

| Identificatore univoco | Campo XDM nello schema unificato |
|----------------- | ---------------------------|
| Indirizzo e-mail | `personalEmail.address` |
| Telefono | `mobilePhone.number` |
| ID programma fedeltà | `Customer-defined XDM field` |

{style="table-layout:auto"}

### Altri attributi di destinazione {#other-destination-attributes}

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

{style="table-layout:auto"}

## Attivare i tipi di pubblico per le destinazioni di e-mail marketing {#activate}

Alcune destinazioni di e-mail marketing nel catalogo esportano i profili in modo in streaming, tramite un’integrazione API con la destinazione.

Altre destinazioni esportano i file in un percorso di archiviazione cloud. Al termine dell’esportazione, devi importare i dati dalla posizione di archiviazione cloud alla destinazione di e-mail marketing.

Segui i collegamenti in [destinazioni di e-mail marketing supportate](#supported-destinations) per scoprire come attivare i tipi di pubblico per ogni destinazione di e-mail marketing.

## Risorse aggiuntive {#additional-resources}

* [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](../../ui/activate-batch-profile-destinations.md)
* [Creare destinazioni di e-mail marketing e attivare i dati utilizzando l’API del servizio di flusso](../../api/connect-activate-batch-destinations.md)
