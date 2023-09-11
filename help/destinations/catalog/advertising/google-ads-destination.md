---
keywords: Google ads;Google ads;Google adwords;Google AdWords;Google Adwords
title: Connessione Google Ads
description: Google Ads, precedentemente noto come Google AdWords, è un servizio di pubblicità online che consente alle aziende di pagare per clic su ricerche testuali, visualizzazioni grafiche, video YouTube e display mobili in-app.
exl-id: 7143f476-49a8-42aa-bfb4-b11fc2b8f5c3
source-git-commit: 72225ac673ed921b5857a14070660134949e7e3e
workflow-type: tm+mt
source-wordcount: '974'
ht-degree: 2%

---

# Connessione [!DNL Google Ads]

## Panoramica {#overview}

[!DNL Google Ads], precedentemente noto come [!DNL Google AdWords], è un servizio di pubblicità online che consente alle aziende di pagare per clic su ricerche testuali e visualizzazioni grafiche, [!DNL YouTube] video e display mobili in-app.

## Specifiche della destinazione {#specifics}

Tieni presente i seguenti dettagli specifici di [!DNL Google Ads] destinazioni:

* I tipi di pubblico attivati vengono creati a livello di programmazione nel [!DNL Google] piattaforma.
* [!DNL Platform] al momento non include una metrica di misurazione per convalidare la corretta attivazione. Fai riferimento ai conteggi dei tipi di pubblico in Google per convalidare l’integrazione e comprendere le dimensioni di targeting del pubblico.

>[!IMPORTANT]
>
>Se desideri creare la prima destinazione con [!DNL Google Ads] e non hanno abilitato [Funzionalità di sincronizzazione ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) nel servizio ID Experience Cloud in passato (con Audienci Manager o altre applicazioni), contatta la consulenza o l&#39;assistenza clienti Adobe per abilitare le sincronizzazioni ID. Se in precedenza avevi configurato le integrazioni Google in Audienci Manager, le sincronizzazioni ID configurate vengono trasferite a Platform.

## Identità supportate {#supported-identities}

[!DNL Google Ad Manager] supporta l’attivazione delle identità descritte nella tabella seguente.

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Seleziona questa identità di destinazione quando l&#39;identità di origine è uno spazio dei nomi GAID. |
| IDFA | [!DNL Apple ID for Advertisers] | Selezionare questa identità di destinazione quando l&#39;identità di origine è uno spazio dei nomi IDFA. |
| UUID AAM | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html), noto anche come [!DNL Device ID]. Un ID dispositivo numerico di 38 cifre che Audienci Manager associa a ogni dispositivo con cui interagisce. | Google utilizza [UUID AAM](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=it) per eseguire il targeting degli utenti in California e l’ID cookie di Google per tutti gli altri utenti. |
| [!DNL Google] ID cookie | [!DNL Google] ID cookie | [!DNL Google] utilizza questo ID per il targeting degli utenti al di fuori della California. |
| RIDA | ID Roku per la pubblicità. Questo ID identifica in modo univoco i dispositivi Roku. |  |
| DOMESTICA | ID Microsoft Advertising. Questo ID identifica in modo univoco i dispositivi con Windows 10. |  |
| ID Amazon Fire TV | Questo ID identifica in modo univoco i televisori Amazon Fire. |  |

{style="table-layout:auto"}

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive il tipo di pubblico che puoi esportare in questa destinazione.

| Origine pubblico | Supportati | Descrizione |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Tipi di pubblico generati dall’Experience Platform [Servizio di segmentazione](../../../segmentation/home.md). |
| Caricamenti personalizzati | ✓ | Tipi di pubblico [importato](../../../segmentation/ui/overview.md#import-audience) in Experienci Platform da file CSV. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione pubblico]** | Stai esportando tutti i membri di un pubblico nella destinazione Google. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experienci Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni su [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Prerequisiti {#prerequisites}

### Esistente [!DNL Google Ads] account

>[!IMPORTANT]
>
> [!DNL Google] ha dichiarato obsoleto [!DNL Google Ads] integrazioni di cookie con fornitori di terze parti. Per eseguire i passaggi di elenco consentiti nella sezione successiva, è necessario disporre di un’integrazione esistente con [!DNL Google Ads]. Di conseguenza, l’approccio consigliato per l’utilizzo di [!DNL Google Ads] sta impostando un [!DNL Google Customer Match] integrazione. Per ulteriori dettagli sulla creazione di un’ [!DNL Google Customer Match] integrazione, leggi il tutorial sulla creazione di un [[!DNL Google Customer Match]](./google-customer-match.md) connessione.

### Inserimento nell’elenco Consentiti {#allow-listing}

>[!NOTE]
>
>L’inserimento nell’elenco Consentiti è obbligatorio prima di impostare la prima [!DNL Google Ads] in Platform. Verifica che il processo di inserimento nell’elenco Consentiti descritto di seguito sia stato completato entro [!DNL Google] prima di creare una destinazione.
>L&#39;eccezione a questa regola è per [Audience Manager](https://docs.adobe.com/content/help/it-IT/experience-cloud/user-guides/home.translate.html) clienti. Se hai già creato una connessione a questa destinazione Google in Audienci Manager, non è necessario ripetere nuovamente la procedura di inserimento nell’elenco Consentiti e puoi procedere ai passaggi successivi.

Prima di creare [!DNL Google Ads] destinazione in Platform, è necessario contattare [!DNL Google] ad Adobe da inserire nell’elenco dei fornitori di dati consentiti e per aggiungere il tuo account all’elenco consentiti. Contatto [!DNL Google] e fornisci le seguenti informazioni:

* **ID account**: ID account di Adobe con Google. ID account: 87933855.
* **ID cliente**: ID account cliente di Adobe con Google. ID cliente: 89690775.
* Tipo di account: **AdWords**
* **ID Google AdWords**: questo è il tuo ID con [!DNL Google]. Il formato ID è tipicamente 123-456-7890.

## Connetti alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md).

### Parametri di connessione {#parameters}

Mentre [configurazione](../../ui/connect-destination.md) in questa destinazione, è necessario fornire le seguenti informazioni:

* **[!UICONTROL Nome]**: inserisci il nome preferito per questa destinazione.
* **[!UICONTROL Descrizione]**: facoltativo. Ad esempio, puoi indicare per quale campagna stai utilizzando questa destinazione.
* **[!UICONTROL Tipo di account]**: AdWords è l’unica opzione disponibile.
* **[!UICONTROL ID account]**: inserisci l’ID account con [!DNL Google Ads]. Il formato ID è tipicamente 123-456-7890.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completate le informazioni sulla connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva il pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Consulta [Attiva i dati del pubblico nelle destinazioni di esportazione del pubblico in streaming](../../ui/activate-segment-streaming-destinations.md) per istruzioni sull’attivazione dei tipi di pubblico in questa destinazione.

## Dati esportati

Per verificare se i dati sono stati esportati correttamente in [!DNL Google Ads] destinazione, controlla il tuo [!DNL Google Ads] account. Se l&#39;attivazione ha esito positivo, i tipi di pubblico vengono popolati nel tuo account.

## Risoluzione dei problemi {#troubleshooting}

### 400 Messaggio di errore di richiesta non valida {#bad-request}

Durante la configurazione di questa destinazione, potrebbe venire visualizzato il seguente errore:

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

Questo errore si verifica quando gli account del cliente non sono conformi al [prerequisiti](#prerequisites) o quando i clienti tentano di configurare la destinazione senza un [!DNL Google Ads] account.

[!DNL Google] ha dichiarato obsoleto [!DNL Google Ads] integrazioni di cookie con fornitori di terze parti. Per eseguire [elenco Consentiti](#allow-listing) passaggi, è necessaria un’integrazione esistente con [!DNL Google Ads].

L’approccio consigliato per l’utilizzo di [!DNL Google Ads] sta impostando un [[!DNL Google Customer Match]](google-customer-match.md) integrazione.
