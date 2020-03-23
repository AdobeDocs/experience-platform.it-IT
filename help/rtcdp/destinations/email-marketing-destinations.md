---
title: Destinazioni marketing e-mail
seo-title: Destinazioni marketing e-mail
description: I provider di servizi e-mail (ESP) consentono di gestire le attività di marketing relative alle e-mail, ad esempio per l’invio di campagne e-mail promozionali.
seo-description: I provider di servizi e-mail (ESP) consentono di gestire le attività di marketing relative alle e-mail, ad esempio per l’invio di campagne e-mail promozionali.
translation-type: tm+mt
source-git-commit: 463212a8fabb9dd5962b4d3f523a6f2d88bb1d9d

---


# Destinazioni di marketing e-mail {#email-marketing-destinations}

I provider di servizi e-mail (ESP) consentono di gestire le attività di marketing relative alle e-mail, ad esempio l&#39;invio di campagne e-mail promozionali. La piattaforma dati cliente Adobe in tempo reale si integra con ESP consentendo di attivare i segmenti per le destinazioni di e-mail marketing.

Per inviare segmenti alle destinazioni di marketing tramite e-mail per le campagne, Adobe Real-time CDP deve prima connettersi alla destinazione.

La connessione alle destinazioni di marketing tramite e-mail è un processo in tre fasi. Ciascuno dei passaggi è descritto più avanti in questa pagina.

Nel flusso di destinazione di connessione, descritto nella sezione seguente, collegatevi ad Amazon S3 o SFTP. CDP in tempo reale esporta i segmenti come `.csv` o `.txt` file e li distribuisce nella posizione desiderata. Pianificare l&#39;importazione dei dati nella piattaforma di e-mail marketing dalla posizione di archiviazione abilitata in CDP in tempo reale. Il processo di importazione dei dati varia a seconda del partner. Per ulteriori informazioni, consulta gli articoli delle singole destinazioni.

## Passaggio 1 - Connetti destinazione {#connect-destination}

1. In **[!UICONTROL Connections > Destinations]**, seleziona la destinazione di e-mail marketing a cui vuoi connetterti, quindi seleziona **[!UICONTROL Connect destination]**.

   ![Connetti alla destinazione](/help/rtcdp/destinations/assets/connect-destination.png)

2. Nella procedura guidata di Connect, selezionate il percorso **[!UICONTROL Connection type]** di memorizzazione. Potete scegliere tra **Amazon S3**, **SFTP con password**, **SFTP con chiave** SSH. Compila le informazioni riportate di seguito, a seconda del tipo di connessione, quindi seleziona **[!UICONTROL Connect]**.

Per le connessioni **** S3, dovete fornire il vostro ID chiave di accesso e la chiave di accesso segreta.

Per **SFTP con connessioni con password** , dovete fornire Domain, Port, UserName e Password.

Per **SFTP con connessioni chiavi** SSH, dovete fornire Domain, Port, Username e Chiave SSH.

## Passaggio 2: selezionare i campi dello schema da utilizzare come attributi di destinazione nei file esportati {#destination-attributes}

In questo passaggio, stai selezionando quali campi esportare per le destinazioni di marketing tramite e-mail.

![Attributi di destinazione](/help/rtcdp/destinations/assets/destination-attributes.png)

### Identità {#identity}

È consigliabile selezionare un identificatore univoco dallo schema [](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)unione. Questo è il campo di cui vengono cancellate le identità degli utenti. Nella maggior parte dei casi, questo campo è l&#39;indirizzo e-mail, ma può anche essere un ID programma fedeltà o un numero di telefono. Vedere la tabella seguente per gli identificatori univoci più comuni e il relativo campo XDM nello schema unificato.

| Identificatore univoco | Campo XDM nello schema unificato |
---------|----------
| Email Address | `personalEmail.address` |
| Telefono | `mobilePhone.number` |
| ID programma fedeltà | `Customer-defined XDM field` |

### Altri attributi di destinazione

Nel selettore del campo Schema, scegliete gli altri campi da esportare nella destinazione e-mail. Alcune opzioni consigliate sono:

| Schema | Campo XDM |
---------|----------
| Nome | `person.name.firstName` |
| Cognome | `person.name.lastName` |
| Telefono | `mobilePhone.number` |
| Indirizzo | `homeAddress.city` |
| Stato indirizzo | `homeAddress.stateProvince` |
| Indirizzo Codice postale | `homeAddress.postalCode` |
| Compleanno | `person.birthDayAndMonth` |

## Passaggio 3 - Importa i dati dalla posizione di archiviazione nella destinazione

Consulta i singoli articoli di destinazione marketing e-mail per informazioni su come importare dati dalla posizione di archiviazione nelle destinazioni:

* [Adobe Campaign](/help/rtcdp/destinations/adobe-campaign-destination.md#import-data-into-campaign)
* [Salesforce Marketing Cloud](/help/rtcdp/destinations/salesforce-marketing-cloud-destination.md#import-data-into-salesforce)
* [Oracle Eloqua](/help/rtcdp/destinations/oracle-eloqua-destination.md#import-data-into-eloqua)
* [Oracle Responsys](/help/rtcdp/destinations/oracle-responsys-destination.md#import-data-into-responsys)

## Attivare i segmenti nelle destinazioni di e-mail marketing

Per istruzioni su come attivare i segmenti nelle destinazioni di marketing tramite e-mail, vedi [Attivare i dati sulle destinazioni](/help/rtcdp/destinations/activate-destinations.md).