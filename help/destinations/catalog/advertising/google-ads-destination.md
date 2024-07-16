---
title: Connessione Google Ads
description: Google Ads, precedentemente noto come Google AdWords, è un servizio di pubblicità online che consente alle aziende di pagare per clic su ricerche testuali, visualizzazioni grafiche, video YouTube e display mobili in-app.
exl-id: 7143f476-49a8-42aa-bfb4-b11fc2b8f5c3
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '949'
ht-degree: 2%

---

# Connessione [!DNL Google Ads]

## Panoramica {#overview}

[!DNL Google Ads], precedentemente noto come [!DNL Google AdWords], è un servizio di pubblicità online che consente alle aziende di pagare per clic la pubblicità tra ricerche testuali, visualizzazioni grafiche, [!DNL YouTube] video e visualizzazioni mobili in-app.

## Specifiche della destinazione {#specifics}

Osservare i dettagli seguenti specifici per [!DNL Google Ads] destinazioni:

* I tipi di pubblico attivati vengono creati a livello di programmazione nella piattaforma [!DNL Google].
* [!DNL Platform] non include attualmente una metrica di misurazione per convalidare la corretta attivazione. Fai riferimento ai conteggi dei tipi di pubblico in Google per convalidare l’integrazione e comprendere le dimensioni di targeting del pubblico.

>[!IMPORTANT]
>
>Se stai cercando di creare la tua prima destinazione con [!DNL Google Ads] e non hai abilitato in passato la funzionalità di sincronizzazione [ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) nel servizio ID Experience Cloud (con Audience Manager o altre applicazioni), contatta Adobe Consulting o l&#39;Assistenza clienti per abilitare le sincronizzazioni ID. Se in precedenza avevi configurato le integrazioni Google in Audience Manager, le sincronizzazioni ID configurate vengono trasferite a Platform.

## Identità supportate {#supported-identities}

[!DNL Google Ads] supporta l&#39;attivazione delle identità descritte nella tabella seguente.

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Seleziona questa identità di destinazione quando l&#39;identità di origine è uno spazio dei nomi GAID. |
| IDFA | [!DNL Apple ID for Advertisers] | Selezionare questa identità di destinazione quando l&#39;identità di origine è uno spazio dei nomi IDFA. |
| UUID AAM | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html), noto anche come [!DNL Device ID]. Un ID dispositivo numerico di 38 cifre che Audience Manager associa a ogni dispositivo con cui interagisce. | Google utilizza [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html) per eseguire il targeting degli utenti in California e l&#39;ID cookie di Google per tutti gli altri utenti. |
| ID cookie [!DNL Google] | ID cookie [!DNL Google] | [!DNL Google] utilizza questo ID per eseguire il targeting degli utenti al di fuori della California. |
| RIDA | ID Roku per Advertising. Questo ID identifica in modo univoco i dispositivi Roku. |  |
| DOMESTICA | MICROSOFT ADVERTISING ID Questo ID identifica in modo univoco i dispositivi con Windows 10. |  |
| ID Amazon Fire TV | Questo ID identifica in modo univoco i televisori Amazon Fire. |  |

{style="table-layout:auto"}

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive quali tipi di pubblico puoi esportare in questa destinazione.

| Origine pubblico | Supportato | Descrizione |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Tipi di pubblico generati tramite il servizio di segmentazione [Experience Platform](../../../segmentation/home.md). |
| Caricamenti personalizzati | ✓ | Tipi di pubblico [importati](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform da file CSV. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione pubblico]** | Stai esportando tutti i membri di un pubblico nella destinazione Google. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni sulle [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Prerequisiti {#prerequisites}

### Account [!DNL Google Ads] esistente

>[!IMPORTANT]
>
> [!DNL Google] ha dichiarato obsolete le nuove integrazioni di cookie [!DNL Google Ads] con fornitori di terze parti. Per eseguire i passaggi del inserisco nell&#39;elenco Consentiti di nella sezione successiva, è necessario disporre di un&#39;integrazione esistente con [!DNL Google Ads]. Di conseguenza, l&#39;approccio consigliato per l&#39;utilizzo di [!DNL Google Ads] consiste nella configurazione di un&#39;integrazione di [!DNL Google Customer Match]. Per ulteriori dettagli sulla creazione di un&#39;integrazione [!DNL Google Customer Match], leggere l&#39;esercitazione sulla creazione di una connessione [[!DNL Google Customer Match]](./google-customer-match.md).

### Inserimento nell’elenco Consentiti {#allow-listing}

>[!NOTE]
>
>L&#39;inserimento nell&#39;elenco Consentiti è obbligatorio prima di configurare la prima destinazione [!DNL Google Ads] in Platform. Prima di creare una destinazione, assicurati che il processo di inserimento nell&#39;elenco Consentiti descritto di seguito sia stato completato da [!DNL Google].
>Eccezione a questa regola per [clienti Audience Manager](https://docs.adobe.com/content/help/it-IT/experience-cloud/user-guides/home.translate.html). Se hai già creato una connessione a questa destinazione Google in Audience Manager, non è necessario ripetere nuovamente la procedura di inserimento nell’elenco Consentiti e puoi procedere ai passaggi successivi.

Prima di creare la destinazione [!DNL Google Ads] in Platform, è necessario contattare [!DNL Google] per inserire l&#39;Adobe nell&#39;elenco dei provider di dati consentiti e per aggiungere il proprio account al inserisco nell&#39;elenco Consentiti di. Contattare [!DNL Google] e fornire le informazioni seguenti:

* **ID account**: ID account di Adobe con Google. ID account: 87933855.
* **ID cliente**: ID account cliente di Adobe con Google. ID cliente: 89690775.
* Tipo di account: **AdWords**
* **ID Google AdWords**: questo è il tuo ID con [!DNL Google]. Il formato ID è tipicamente 123-456-7890.

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, sono necessarie le **[!UICONTROL Destinazioni visualizzazione]** e le **[!UICONTROL Autorizzazioni di gestione delle destinazioni]** [per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md).

### Parametri di connessione {#parameters}

Durante la [configurazione](../../ui/connect-destination.md) di questa destinazione, è necessario fornire le seguenti informazioni:

* **[!UICONTROL Nome]**: immettere il nome preferito per la destinazione.
* **[!UICONTROL Descrizione]**: facoltativo. Ad esempio, puoi indicare per quale campagna stai utilizzando questa destinazione.
* **[!UICONTROL Tipo account]**: AdWords è l&#39;unica opzione disponibile.
* **[!UICONTROL ID account]**: inserisci l&#39;ID account con [!DNL Google Ads]. Il formato ID è tipicamente 123-456-7890.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli per la connessione di destinazione, seleziona **[!UICONTROL Avanti]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione, consulta [Attivare i dati del pubblico nelle destinazioni di esportazione del pubblico in streaming](../../ui/activate-segment-streaming-destinations.md).

## Dati esportati

Per verificare se i dati sono stati esportati correttamente nella destinazione [!DNL Google Ads], controllare l&#39;account [!DNL Google Ads]. Se l&#39;attivazione ha esito positivo, i tipi di pubblico vengono popolati nel tuo account.

## Risoluzione dei problemi {#troubleshooting}

### 400 Messaggio di errore di richiesta non valida {#bad-request}

Durante la configurazione di questa destinazione, potrebbe venire visualizzato il seguente errore:

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

Questo errore si verifica quando gli account cliente non sono conformi ai [prerequisiti](#prerequisites) o quando i clienti tentano di configurare la destinazione senza un account [!DNL Google Ads] esistente.

[!DNL Google] ha dichiarato obsolete le nuove integrazioni di cookie [!DNL Google Ads] con fornitori di terze parti. Inserire nell&#39;elenco Consentiti Per eseguire i passaggi di [](#allow-listing), è necessario disporre di un&#39;integrazione esistente con [!DNL Google Ads].

L&#39;approccio consigliato per l&#39;utilizzo di [!DNL Google Ads] consiste nella configurazione di un&#39;integrazione di [[!DNL Google Customer Match]](google-customer-match.md).
