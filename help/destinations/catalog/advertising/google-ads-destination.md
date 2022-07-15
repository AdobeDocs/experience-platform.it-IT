---
keywords: annunci Google;annunci google;parole adwords Google;Google AdWords;Google Adwords
title: Connessione Google Ads
description: Google Ads, precedentemente noto come Google AdWords, è un servizio di pubblicità online che consente alle aziende di effettuare pubblicità a pagamento per clic tra ricerche basate su testo, visualizzazioni grafiche, video YouTube e display mobili in-app.
exl-id: 7143f476-49a8-42aa-bfb4-b11fc2b8f5c3
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 3%

---

# [!DNL Google Ads] connection

## Panoramica {#overview}

[!DNL Google Ads], precedentemente noto come [!DNL Google AdWords], è un servizio pubblicitario online che consente alle aziende di effettuare pubblicità pay-per-click tra ricerche basate su testo, display grafici, [!DNL YouTube] video e visualizzazioni mobili in-app.

## Specifiche di destinazione {#specifics}

Tieni presente i seguenti dettagli specifici per [!DNL Google Ads] destinazioni:

* I tipi di pubblico attivati vengono creati a livello di programmazione nel [!DNL Google] piattaforma.
* [!DNL Platform] al momento non include una metrica di misurazione per convalidare l’attivazione. Consulta i conteggi del pubblico in Google per convalidare l’integrazione e comprendere le dimensioni del targeting del pubblico.

>[!IMPORTANT]
>
>Se desideri creare la tua prima destinazione con [!DNL Google Ads] e non hanno attivato il [Funzionalità di sincronizzazione ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) in Experience Cloud ID Service in passato (con Audience Manager o altre applicazioni), contatta la Consulenza Adobe o l’Assistenza clienti per abilitare la sincronizzazione degli ID. Se in precedenza avevi impostato le integrazioni Google in Audience Manager, le sincronizzazioni ID che avevi configurato riportano a Platform.

## Identità supportate {#supported-identities}

[!DNL Google Ad Manager] supporta l’attivazione delle identità descritte nella tabella seguente.

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Seleziona questa identità di destinazione quando l’identità di origine è uno spazio dei nomi GAID. |
| IDFA | [!DNL Apple ID for Advertisers] | Seleziona questa identità di destinazione quando l’identità di origine è uno spazio dei nomi IDFA. |
| UUID AAM | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html), noto anche come [!DNL Device ID]. Un ID dispositivo numerico a 38 cifre associato a ciascun dispositivo con cui interagisce. | Google utilizza [UUID AAM](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en) per eseguire il targeting degli utenti in California e dell’ID cookie di Google per tutti gli altri utenti. |
| [!DNL Google] ID cookie | [!DNL Google] ID cookie | [!DNL Google] utilizza questo ID per eseguire il targeting degli utenti al di fuori della California. |
| RIDA | ID Roku per la pubblicità. Questo ID identifica in modo univoco i dispositivi Roku. |  |
| MAID | Microsoft Advertising ID. Questo ID identifica in modo univoco i dispositivi con Windows 10. |  |
| Amazon Fire TV ID | Questo ID identifica in modo univoco i Amazon Fire TV. |  |

{style=&quot;table-layout:auto&quot;}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, fare riferimento alla tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione del segmento]** | Stai esportando tutti i membri di un segmento (pubblico) nella destinazione Google. |
| Frequenza delle esportazioni | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni basate su API &quot;sempre attive&quot;. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del segmento, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Prerequisiti {#prerequisites}

### Esistente [!DNL Google Ads] account

>[!IMPORTANT]
>
> [!DNL Google] ha dichiarato obsoleto il nuovo [!DNL Google Ads] integrazioni di cookie con fornitori di terze parti. Per eseguire i passaggi dell’elenco consentiti nella sezione successiva, devi disporre di un’integrazione esistente con [!DNL Google Ads]. Di conseguenza, si consiglia di utilizzare l&#39;approccio [!DNL Google Ads] sta configurando un [!DNL Google Customer Match] integrazione. Per ulteriori dettagli sulla creazione di un [!DNL Google Customer Match] integrazione, leggi l’esercitazione sulla creazione di un [[!DNL Google Customer Match]](./google-customer-match.md) connessione.

### Inserimento nell’elenco Consentiti {#allow-listing}

>[!NOTE]
>
>L’elenco consentiti è obbligatorio prima di configurare il primo [!DNL Google Ads] in Platform. Assicurati che il processo di elenco consentiti descritto di seguito sia stato completato da [!DNL Google] prima di creare una destinazione.

Prima di creare il [!DNL Google Ads] in Platform, devi contattare [!DNL Google] ad Adobe da inserire nell’elenco dei provider di dati consentiti e da aggiungere all’elenco consentiti il tuo account. Contatto [!DNL Google] e fornire le seguenti informazioni:

* **ID account**: ID account di Adobe con Google. ID account: 87933855.
* **ID cliente**: ID account cliente di Adobe con Google. ID cliente: 89690775.
* Tipo di account: **AdWords**
* **ID Google AdWords**: Questo è il tuo ID con [!DNL Google]. Il formato ID è tipicamente 123-456-7890.

## Collegati alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Per connettersi a questa destinazione, segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md).

### Parametri di connessione {#parameters}

Quando [configurazione](../../ui/connect-destination.md) questa destinazione, devi fornire le seguenti informazioni:

* **[!UICONTROL Nome]**: Compila il nome preferito per questa destinazione.
* **[!UICONTROL Descrizione]**: Facoltativo. Ad esempio, è possibile indicare per quale campagna si utilizza questa destinazione.
* **[!UICONTROL Tipo di conto]**: AdWords è l’unica opzione disponibile.
* **[!UICONTROL ID account]**: Compila l&#39;ID del tuo account con [!DNL Google Ads]. Il formato ID è tipicamente 123-456-7890.

### Abilitare gli avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati nella tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere le notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [iscrizione agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completati i dettagli della connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizzare i segmenti]** [autorizzazioni di controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Vedi [Attivare i dati del pubblico nelle destinazioni di esportazione dei segmenti in streaming](../../ui/activate-segment-streaming-destinations.md) per istruzioni su come attivare i segmenti di pubblico a questa destinazione.

## Dati esportati

Per verificare se i dati sono stati esportati correttamente in [!DNL Google Ads] destinazione, controlla il tuo [!DNL Google Ads] conto. Se l&#39;attivazione ha avuto successo, i tipi di pubblico vengono compilati nel tuo account.

## Risoluzione dei problemi {#troubleshooting}

### 400 Messaggio di errore di richiesta non valida {#bad-request}

Durante la configurazione di questa destinazione, potresti ricevere il seguente errore:

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

Questo errore si verifica quando gli account cliente non sono conformi alla [prerequisiti](#prerequisites) o quando i clienti tentano di configurare la destinazione senza un [!DNL Google Ads] conto.

[!DNL Google] ha dichiarato obsoleto il nuovo [!DNL Google Ads] integrazioni di cookie con fornitori di terze parti. Per eseguire la [elenco Consentiti](#allow-listing) passaggi, devi disporre di un’integrazione esistente con [!DNL Google Ads].

Approccio consigliato per l&#39;utilizzo [!DNL Google Ads] sta configurando un [[!DNL Google Customer Match]](google-customer-match.md) integrazione.
