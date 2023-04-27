---
keywords: google ad manager;google ad;doubleclick;DoubleClick AdX;DoubleClick;Google Ad Manager;Google ad manager; DFP
title: Connessione Google Ad Manager
description: Google Ad Manager, precedentemente noto come DoubleClick for Publishers o DoubleClick AdX, è una piattaforma di ad serving di Google che offre agli editori i mezzi per gestire la visualizzazione degli annunci pubblicitari sui loro siti web, attraverso video e nelle app mobili.
exl-id: e93f1bd5-9d29-43a1-a9a6-8933f9d85150
source-git-commit: 5174c65970aa8df9bc3f2c8d612c26c72c20e81f
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 2%

---

# [!DNL Google Ad Manager] connection

## Panoramica {#overview}

[!DNL Google Ad Manager], precedentemente noto come [!DNL DoubleClick for Publishers] (DFP) o [!DNL DoubleClick AdX], è una piattaforma di ad serving da [!DNL Google] che offre agli editori i mezzi per gestire la visualizzazione degli annunci sui loro siti web, attraverso video e nelle app per dispositivi mobili.

## Specifiche di destinazione {#specifics}

Tieni presente i seguenti dettagli specifici per [!DNL Google Ad Manager] destinazioni:

* I tipi di pubblico attivati vengono creati a livello di programmazione nel [!DNL Google] piattaforma.
* [!DNL Platform] al momento non include una metrica di misurazione per convalidare l’attivazione. Consulta i conteggi del pubblico in Google per convalidare l’integrazione e comprendere le dimensioni del targeting del pubblico.
* Dopo aver mappato un segmento in un [!DNL Google Ad Manager] la destinazione , il nome del segmento viene visualizzato immediatamente nel [!DNL Google Ad Manager] interfaccia utente.
* La popolazione del segmento ha bisogno di 24-48 ore per essere visualizzata in [!DNL Google Ad Manager]. Inoltre, i segmenti devono avere una dimensione di pubblico di almeno 50 profili per essere visualizzati in [!DNL Google Ad Manager]. I segmenti con dimensioni di pubblico inferiori a 50 profili non verranno compilati in [!DNL Google Ad Manager].

## Identità supportate {#supported-identities}

[!DNL Google Ad Manager] supporta l’attivazione delle identità descritte nella tabella seguente.

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Seleziona questa identità di destinazione quando l’identità di origine è uno spazio dei nomi GAID. |
| IDFA | [!DNL Apple ID for Advertisers] | Seleziona questa identità di destinazione quando l’identità di origine è uno spazio dei nomi IDFA. |
| UUID AAM | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html), noto anche come [!DNL Device ID]. Un ID dispositivo numerico a 38 cifre associato a ciascun dispositivo con cui interagisce. | Google utilizza [UUID AAM](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=it) per eseguire il targeting degli utenti in California e dell’ID cookie di Google per tutti gli altri utenti. |
| [!DNL Google] ID cookie | [!DNL Google] ID cookie | [!DNL Google] utilizza questo ID per eseguire il targeting degli utenti al di fuori della California. |
| RIDA | ID Roku per la pubblicità. Questo ID identifica in modo univoco i dispositivi Roku. |  |
| MAID | Microsoft Advertising ID. Questo ID identifica in modo univoco i dispositivi con Windows 10. |  |
| Amazon Fire TV ID | Questo ID identifica in modo univoco i Amazon Fire TV. |  |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, fare riferimento alla tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione del segmento]** | Stai esportando tutti i membri di un segmento (pubblico) nella destinazione Google. |
| Frequenza delle esportazioni | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni basate su API &quot;sempre attive&quot;. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del segmento, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Prerequisiti {#prerequisites}

Se desideri creare la tua prima destinazione con [!DNL Google Ad Manager] e non hanno attivato il [Funzionalità di sincronizzazione ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) in Experience Cloud ID Service in passato (con Audience Manager o altre applicazioni), contatta la Consulenza Adobe o l’Assistenza clienti per abilitare la sincronizzazione degli ID. Se hai già configurato [!DNL Google] integrazioni in Audience Manager, le sincronizzazioni ID impostate riportano su Platform.

### Inserimento nell’elenco Consentiti {#allow-listing}

L’inserimento nell’elenco Consentiti è obbligatorio prima di configurare il primo [!DNL Google Ad Manager] in Platform. Prima di creare la destinazione, completa il processo di inserimento nell’elenco Consentiti descritto di seguito.

1. Segui i passaggi descritti in [Documentazione di Google Ad Manager](https://support.google.com/admanager/answer/3289669?hl=en) per aggiungere Adobe come piattaforma di gestione dati (DMP, Data Management Platform) collegata.
2. In [!DNL Google Ad Manager] interfaccia, vai a **[!UICONTROL Amministratore]** > **[!UICONTROL Impostazioni globali]** > **[!UICONTROL Impostazioni di rete]** e abilita **[!UICONTROL Accesso API]** cursore.

## Collegati alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Per connettersi a questa destinazione, segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md).

### Parametri di connessione {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_gam_appendSegmentID"
>title="Aggiungi ID segmento al nome del segmento"
>abstract="Seleziona questa opzione per fare in modo che il nome del segmento in Google Ad Manager includa l’ID del segmento dall’Experience Platform, come riportato di seguito: `Segment Name (Segment ID)`"

Quando [configurazione](../../ui/connect-destination.md) questa destinazione, devi fornire le seguenti informazioni:

* **[!UICONTROL Nome]**: Compila il nome preferito per questa destinazione.
* **[!UICONTROL Descrizione]**: Facoltativo. Ad esempio, è possibile indicare per quale campagna si utilizza questa destinazione.
* **[!UICONTROL ID account]**: Inserisci il tuo [!DNL Audience Link ID] dal [!DNL Google] conto. Questo è un identificatore specifico associato al [!DNL Google Ad Manager] rete (non il [!DNL Network code]). Puoi trovarlo in **[!UICONTROL Amministratore > Impostazioni globali]** in [!DNL Google Ad Manager] interfaccia.
* **[!UICONTROL Tipo di conto]**: Seleziona un’opzione, a seconda dell’account con Google:
   * Utilizzo `DFP by Google` per [!DNL DoubleClick] per gli editori
   * Utilizzo `AdX buyer` per [!DNL Google AdX]
* **[!UICONTROL Aggiungi ID segmento al nome del segmento]**: Seleziona questa opzione per fare in modo che il nome del segmento in Google Ad Manager includa l’ID del segmento dall’Experience Platform, come riportato di seguito: `Segment Name (Segment ID)`.

>[!NOTE]
>
>Quando si imposta un [!DNL Google Ad Manager] destinazione, per favore, collabora con la tua [!DNL Google Account Manager] o rappresentante di Adobe per capire quale tipo di account hai.

### Abilitare gli avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati nella tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere le notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [iscrizione agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completati i dettagli della connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizzare i segmenti]** [autorizzazioni di controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Vedi [Attivare i dati del pubblico nelle destinazioni di esportazione dei segmenti in streaming](../../ui/activate-segment-streaming-destinations.md) per istruzioni su come attivare i segmenti di pubblico a questa destinazione.

## Dati esportati {#exported-data}

Per verificare se i dati sono stati esportati correttamente in [!DNL Google Ad Manager] destinazione, controlla il tuo [!DNL Google Ad Manager] conto. Se l&#39;attivazione ha avuto successo, i tipi di pubblico vengono compilati nel tuo account.

## Risoluzione dei problemi {#troubleshooting}

Nel caso in cui si verifichino errori durante l&#39;utilizzo di questa destinazione e sia necessario contattare Adobe o Google, mantieni a portata di mano i seguenti ID.

Questi sono gli ID account Google di Adobe:

* **[!UICONTROL ID account]**: 87933855
* **[!UICONTROL ID cliente]**: 89690775