---
keywords: e-mail;e-mail;e-mail;destinazioni e-mail
title: Panoramica sulle destinazioni di e-mail marketing
type: Tutorial
description: I provider di servizi e-mail (ESP) ti consentono di gestire le attività di marketing relative alle e-mail, ad esempio per l’invio di campagne e-mail promozionali. Scopri quali ESP sono supportati come destinazioni di Experience Platform.
exl-id: e07f8c5a-0424-4de5-810f-3d5711ef4606
source-git-commit: d6ea94b275ab0ed7c0638200188fe7ada7bacf5c
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 3%

---

# Panoramica sulle destinazioni di e-mail marketing {#email-marketing-destinations}

## Panoramica {#overview}

I provider di servizi e-mail (ESP) consentono di gestire le attività di marketing relative alle e-mail, ad esempio l’invio di campagne e-mail promozionali. Adobe Experience Platform si integra con ESP e consente di attivare segmenti nelle destinazioni di marketing via e-mail.

## Destinazioni di marketing e-mail supportate {#supported-destinations}

Adobe Experience Platform supporta le seguenti destinazioni di e-mail marketing:

* [Adobe Campaign](adobe-campaign.md)
* [Adobe Campaign Managed Cloud Services](adobe-campaign-managed-services.md)
* [(API) Oracle Eloqua](oracle-eloqua-api.md)
* [Marketing Cloud Salesforce (API)](salesforce-marketing-cloud-exact-target.md)
* [(File) Oracle Eloqua](oracle-eloqua.md)
* [(File) Marketing Cloud Salesforce](salesforce-marketing-cloud.md)
* [Oracle Responsys](oracle-responsys.md)
* [SendGrid](sendgrid.md)

## Connessione a una nuova destinazione di marketing e-mail {#connect-destination}

Per inviare segmenti alle destinazioni di marketing e-mail per le campagne, Platform deve prima connettersi alla destinazione. Consulta la sezione [esercitazione sulla creazione di una destinazione](../../ui/connect-destination.md) informazioni dettagliate sulla configurazione di una nuova destinazione.

## Best practice per attivare i tipi di pubblico nelle destinazioni di marketing via e-mail {#best-practices}

### Selezione identità {#identity}

Adobe consiglia di selezionare un identificatore univoco dal [schema unione](../../../profile/home.md#profile-fragments-and-union-schemas). Questo è il campo di cui si distinguono le identità utente. Nella maggior parte dei casi, questo campo è l’indirizzo e-mail, ma può anche essere un ID programma fedeltà o un numero di telefono. Fai riferimento alla tabella seguente per gli identificatori univoci più comuni e il relativo campo XDM nello schema.

| Identificatore univoco | Campo XDM nello schema unificato |
|----------------- | ---------------------------|
| Indirizzo e-mail | `personalEmail.address` |
| Telefono | `mobilePhone.number` |
| ID programma fedeltà | `Customer-defined XDM field` |

{style="table-layout:auto"}

### Altri attributi di destinazione {#other-destination-attributes}

Nel selettore del campo Schema, scegli gli altri campi da esportare nella destinazione e-mail. Alcune opzioni consigliate sono:

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

## Attivare i segmenti nelle destinazioni di marketing via e-mail {#activate}

Alcune destinazioni di e-mail marketing nei profili di esportazione del catalogo in modo streaming, tramite un’integrazione API con la destinazione.

Altre destinazioni esportano file in un percorso di archiviazione cloud. Al termine dell’esportazione, è necessario importare i dati dal percorso di archiviazione cloud nella destinazione di e-mail marketing.

Segui i collegamenti nella [destinazioni di e-mail marketing supportate](#supported-destinations) per scoprire come attivare i segmenti in ogni destinazione di e-mail marketing.

## Risorse aggiuntive {#additional-resources}

* [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](../../ui/activate-batch-profile-destinations.md)
* [Creare destinazioni di marketing e-mail e attivare i dati utilizzando l’API del servizio di flusso](../../api/connect-activate-batch-destinations.md)
