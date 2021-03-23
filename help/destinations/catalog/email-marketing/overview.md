---
keywords: e-mail;e-mail;e-mail;destinazioni e-mail
title: Panoramica sulle destinazioni di e-mail marketing
type: Tutorial
description: I provider di servizi e-mail (ESP) ti consentono di gestire le attività di marketing relative alle e-mail, ad esempio per l’invio di campagne e-mail promozionali.
translation-type: tm+mt
source-git-commit: 02754055e2be8a45a0699386cb559dad8f25717c
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 1%

---


# Panoramica sulle destinazioni di e-mail marketing {#email-marketing-destinations}

I provider di servizi e-mail (ESP) consentono di gestire le attività di marketing relative alle e-mail, ad esempio l’invio di campagne e-mail promozionali. Adobe Experience Platform si integra con ESP e consente di attivare segmenti nelle destinazioni di marketing via e-mail.

Per inviare segmenti alle destinazioni di marketing e-mail per le campagne, Platform deve prima connettersi alla destinazione.

La connessione alle destinazioni di marketing e-mail è un processo in tre fasi ([configura destinazione](#connect-destination), [attiva segmenti](#select-segments), [importa dati dalla posizione di archiviazione nella destinazione](#import-data-into-destination)). Ciascuno dei passaggi è descritto più avanti in questa pagina.

Nel flusso di destinazione di connessione, descritto nella sezione seguente, connettiti a Amazon S3 o SFTP. Platform esporta i segmenti come file `.csv` o `.txt` e li distribuisce nella posizione desiderata. Pianifica l’importazione dei dati nella tua piattaforma di marketing e-mail dal percorso di archiviazione abilitato in Platform. Il processo di importazione dei dati varia a seconda del partner. Leggi gli articoli sulle singole destinazioni per ulteriori informazioni.

## Configurare la destinazione {#connect-destination}

In **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, seleziona la destinazione di marketing e-mail a cui desideri connetterti, quindi seleziona **[!UICONTROL Configure]**.

![Connetti alla destinazione](../../assets/catalog/email-marketing/overview/connect-email-marketing.png)

Nel passaggio **[!UICONTROL Account]** , se in precedenza hai impostato una connessione alla destinazione di marketing e-mail, seleziona **[!UICONTROL Existing Account]** e seleziona la connessione esistente. In alternativa, puoi selezionare **[!UICONTROL New Account]** per impostare una nuova connessione alla destinazione di e-mail marketing. Nel selettore **[!UICONTROL Connection type]** puoi selezionare tra [!UICONTROL Amazon S3], [!UICONTROL Azure Blob], [!UICONTROL SFTP with Password] o [!UICONTROL SFTP with SSH Key]. Compila le informazioni seguenti, a seconda del tipo di connessione, quindi seleziona **[!UICONTROL Connect]**.

- Per **S3 connections**, devi fornire il tuo ID chiave di accesso Amazon e la chiave di accesso segreto.
- Per le connessioni **SFTP con password**, devi fornire dominio, porta, nome utente e password per il server SFTP.
- Per le connessioni **SFTP con chiave SSH**, devi fornire Dominio, Porta, Nome utente e Chiave SSH per il server SFTP.

Facoltativamente, puoi allegare la chiave pubblica in formato RSA per aggiungere la crittografia ai file esportati nella sezione **[!UICONTROL Key]** . La chiave pubblica deve essere scritta come stringa codificata [!DNL Base64].

Nel passaggio **[!UICONTROL Authentication]**, immetti un nome e una descrizione per la nuova destinazione e il formato del file per i file esportati.

Se hai selezionato Amazon S3 come opzione di archiviazione nel passaggio precedente, inserisci il nome del bucket e il percorso della cartella nella destinazione di archiviazione cloud in cui verranno consegnati i file. Per l’opzione di archiviazione SFTP, inserisci il percorso della cartella in cui verranno consegnati i file.

A questo passaggio, puoi anche selezionare qualsiasi azione Marketing da applicare a questa destinazione. Le azioni di marketing indicano l’intento per il quale i dati verranno esportati nella destinazione. Puoi scegliere tra azioni di marketing definite da Adobi o creare una tua azione di marketing. Per ulteriori informazioni sulle azioni di marketing, consulta la [Panoramica sui criteri di utilizzo dei dati](../../../data-governance/policies/overview.md).

![Passaggio di configurazione e-mail](../../assets/catalog/email-marketing/overview/email-setup-step.png)

## Selezionare i membri del segmento da includere nelle esportazioni di destinazione {#select-segments}

Nella pagina **[!UICONTROL Select Segments]** , seleziona i segmenti da inviare alla destinazione. Per ulteriori informazioni sui campi, consulta le sezioni seguenti.

![Selezionare segmenti](../../assets/common/email-select-segments.png)

## Configurare i nomi dei file

Per informazioni sulla pianificazione dei segmenti e sulle opzioni di modifica dei nomi dei file, fai riferimento al passaggio [Configura](../../ui/activate-destinations.md#configure) nell&#39;esercitazione di attivazione delle destinazioni .

## Selezionare gli attributi - Selezionare i campi dello schema da utilizzare come attributi di destinazione nei file esportati {#destination-attributes}

In questo passaggio, selezioni quali campi esportare nelle destinazioni di marketing e-mail e contrassegni quali campi sono obbligatori.
Per informazioni su questo passaggio, fai riferimento al passaggio [Seleziona attributi](../../ui/activate-destinations.md#select-attributes) nell&#39;esercitazione di attivazione delle destinazioni .

## Identità {#identity}

Adobe consiglia di selezionare un identificatore univoco dal [schema di unione](../../../profile/home.md#profile-fragments-and-union-schemas). Questo è il campo di cui si distinguono le identità utente. Nella maggior parte dei casi, questo campo è l’indirizzo e-mail, ma può anche essere un ID programma fedeltà o un numero di telefono. Fai riferimento alla tabella seguente per gli identificatori univoci più comuni e il relativo campo XDM nello schema.

| Identificatore univoco | Campo XDM nello schema unificato |
----------------- | ---------------------------
| Indirizzo e-mail | `personalEmail.address` |
| Telefono | `mobilePhone.number` |
| ID programma fedeltà | `Customer-defined XDM field` |

## Altri attributi di destinazione

Nel selettore del campo Schema, scegli gli altri campi da esportare nella destinazione e-mail. Alcune opzioni consigliate sono:

| Schema | Campo XDM |
------ | ---------
| Nome | `person.name.firstName` |
| Cognome | `person.name.lastName` |
| Telefono | `mobilePhone.number` |
| Città indirizzo | `homeAddress.city` |
| Stato indirizzo | `homeAddress.stateProvince` |
| Indirizzo Codice postale | `homeAddress.postalCode` |
| Compleanno | `person.birthDayAndMonth` |
| Iscrizione al segmento | `segmentMembership.status` |

## Importa dati dalla posizione di archiviazione nella destinazione {#import-data-into-destination}

Leggi i singoli articoli di destinazione marketing e-mail per scoprire come importare dati dalla posizione di archiviazione nelle destinazioni:

- [Adobe Campaign](./adobe-campaign.md#import-data-into-campaign)
- [Oracle Eloqua](./oracle-eloqua.md#import-data-into-eloqua)
- [Oracle Responsys](./oracle-responsys.md#import-data-into-responsys)
- [Marketing Cloud Salesforce](./salesforce-marketing-cloud.md#import-data-into-salesforce)

## Attivare i segmenti nelle destinazioni di marketing via e-mail

Per istruzioni su come attivare i segmenti nelle destinazioni di marketing e-mail, consulta [Attivare profili e segmenti in una destinazione](../../ui/activate-destinations.md).

## Risorse aggiuntive

- [Attivare i dati nelle destinazioni](../../ui/activate-destinations.md)
- [Creare destinazioni di marketing e-mail e attivare i dati utilizzando l’API del servizio di flusso](../../api/email-marketing.md)