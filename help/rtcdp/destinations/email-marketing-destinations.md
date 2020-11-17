---
keywords: email;Email;e-mail;email destinations
title: Destinazioni marketing e-mail
seo-title: Destinazioni marketing e-mail
type: Tutorial
description: I provider di servizi e-mail (ESP) consentono di gestire le attività di marketing relative alle e-mail, ad esempio per l’invio di campagne e-mail promozionali.
seo-description: I provider di servizi e-mail (ESP) consentono di gestire le attività di marketing relative alle e-mail, ad esempio per l’invio di campagne e-mail promozionali.
translation-type: tm+mt
source-git-commit: 42b694c532f140b51913ba5ceb0aaeacc2263039
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 1%

---


# Destinazioni di marketing e-mail {#email-marketing-destinations}

I provider di servizi e-mail (ESP) consentono di gestire le attività di marketing relative alle e-mail, ad esempio l&#39;invio di campagne e-mail promozionali.  Piattaforma dati cliente in tempo reale si integra con ESP consentendo di attivare i segmenti nelle destinazioni di marketing via e-mail.

Per inviare segmenti alle destinazioni di marketing via e-mail per le campagne,  CDP in tempo reale del Adobe deve prima connettersi alla destinazione.

La connessione alle destinazioni di marketing tramite e-mail è un processo in tre fasi. Ciascuno dei passaggi è descritto più avanti in questa pagina.

Nel flusso di destinazione di connessione, descritto nella sezione seguente, collegatevi a  Amazon S3 o SFTP. CDP in tempo reale esporta i segmenti come `.csv` o `.txt` file e li distribuisce nella posizione desiderata. Pianificare l&#39;importazione dei dati nella piattaforma di e-mail marketing dalla posizione di archiviazione abilitata in CDP in tempo reale. Il processo di importazione dei dati varia a seconda del partner. Per ulteriori informazioni, consulta gli articoli delle singole destinazioni.

## Configura destinazione {#connect-destination}

In **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, seleziona la destinazione di e-mail marketing a cui vuoi connetterti, quindi seleziona **[!UICONTROL Configure]**.

![Connetti alla destinazione](./assets/connect-email-marketing.png)

Nel **[!UICONTROL Authentication]** passaggio, se in precedenza hai impostato una connessione alla destinazione di marketing per e-mail, seleziona **[!UICONTROL Existing Account]** e seleziona la connessione esistente. In alternativa, potete scegliere **[!UICONTROL New Account]** di impostare una nuova connessione alla destinazione di e-mail marketing. Nel **[!UICONTROL Connection type]** selettore, potete scegliere tra  Amazon S3, SFTP con password o SFTP con chiave SSH. Compila le informazioni riportate di seguito, a seconda del tipo di connessione, quindi seleziona **[!UICONTROL Connect]**.

- Per le connessioni **** S3, dovete fornire il vostro ID chiave di accesso Amazon  e la chiave di accesso segreta.
- Per **SFTP con connessioni con password** , dovete fornire Domain, Port, Username e Password per il vostro server SFTP.
- Per **SFTP con connessioni chiavi** SSH, dovete fornire Domain, Port, Username e Chiave SSH per il vostro server SFTP.

Facoltativamente, puoi allegare la chiave pubblica in formato RSA per aggiungere la cifratura ai file esportati nella **[!UICONTROL Key]** sezione. Questa chiave pubblica **deve** essere scritta come una stringa codificata Base64.

Nel **[!UICONTROL Setup]** passaggio, immettete un nome e una descrizione per la nuova destinazione, nonché il formato del file per i file esportati.

Se nel passaggio precedente avete selezionato &#39;opzione di archiviazione Amazon S3, inserite il nome del bucket e il percorso della cartella nella destinazione di archiviazione cloud in cui verranno inviati i file. Per l&#39;opzione di memorizzazione SFTP, inserite il percorso della cartella in cui verranno inviati i file.

Inoltre in questo passaggio, puoi selezionare qualsiasi caso di utilizzo marketing da applicare a questa destinazione. I casi di utilizzo del marketing indicano l&#39;intento per il quale i dati verranno esportati nella destinazione. Puoi scegliere tra  casi di utilizzo di marketing definiti dal Adobe o creare un caso di utilizzo di marketing personale. Per ulteriori informazioni sui casi di utilizzo del marketing, consulta la pagina [Governance dei dati in CDP](/help/rtcdp/privacy/data-governance-overview.md#destinations) in tempo reale. Per informazioni sui singoli casi di utilizzo marketing definiti dal Adobe , consulta la panoramica [sui criteri di utilizzo dei](/help/data-governance/policies/overview.md#core-actions)dati.

![Passaggio di impostazione e-mail](./assets/email-setup-step.png)

## Selezionare i membri del segmento da includere nelle esportazioni di destinazione {#select-segments}

Nella **[!UICONTROL Select Segments]** pagina, seleziona i segmenti da inviare alla destinazione. Per ulteriori informazioni sui campi, consulta le sezioni seguenti.

![Seleziona segmenti](/help/rtcdp/destinations/assets/email-select-segments.png)

## Configurare i nomi dei file

Per informazioni sulle opzioni di modifica del nome del file, fare riferimento al passaggio [Configura](/help/rtcdp/destinations/activate-destinations.md#configure) nell&#39;esercitazione sulle destinazioni di attivazione.

## Seleziona attributi - Seleziona i campi dello schema da usare come attributi di destinazione nei file esportati {#destination-attributes}

In questo passaggio, stai selezionando quali campi esportare per le destinazioni di marketing tramite e-mail, oltre a indicare quali campi sono obbligatori.

![Attributi di destinazione](/help/rtcdp/destinations/assets/recommended-attributes.png)

Per ulteriori informazioni su questo passaggio, consulta il passaggio [Seleziona attributi](/help/rtcdp/destinations/activate-destinations.md#select-attributes) nell’esercitazione di attivazione delle destinazioni.

### Identità {#identity}

È consigliabile selezionare un identificatore univoco dallo schema [](../../profile/home.md#profile-fragments-and-union-schemas)unione. Questo è il campo di cui vengono cancellate le identità degli utenti. Nella maggior parte dei casi, questo campo è l&#39;indirizzo e-mail, ma può anche essere un ID programma fedeltà o un numero di telefono. Vedere la tabella seguente per gli identificatori univoci più comuni e il relativo campo XDM nello schema.

| Identificatore univoco | Campo XDM nello schema unificato |
---------|----------
| Indirizzo e-mail | `personalEmail.address` |
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
| Appartenenza al segmento | `segmentMembership.status` |

## Importa dati dalla posizione di archiviazione nella destinazione

Consulta i singoli articoli di destinazione marketing e-mail per informazioni su come importare dati dalla posizione di archiviazione nelle destinazioni:

- [Adobe Campaign](/help/rtcdp/destinations/adobe-campaign-destination.md#import-data-into-campaign)
- [Marketing Cloud Salesforce](/help/rtcdp/destinations/salesforce-marketing-cloud-destination.md#import-data-into-salesforce)
- [Oracle Eloqua](/help/rtcdp/destinations/oracle-eloqua-destination.md#import-data-into-eloqua)
- [Oracle Responsys](/help/rtcdp/destinations/oracle-responsys-destination.md#import-data-into-responsys)

## Attivare i segmenti nelle destinazioni di e-mail marketing

Per istruzioni su come attivare i segmenti nelle destinazioni di marketing tramite e-mail, vedi [Attivare i dati sulle destinazioni](/help/rtcdp/destinations/activate-destinations.md).

## Risorse aggiuntive

- [Attivare i dati per le destinazioni](/help/rtcdp/destinations/activate-destinations.md)
- [Creare le destinazioni di marketing e attivare i dati tramite l&#39;API del servizio di flusso](https://docs.adobe.com/content/help/en/experience-platform/tutorials/destinations/email-marketing-api.html)