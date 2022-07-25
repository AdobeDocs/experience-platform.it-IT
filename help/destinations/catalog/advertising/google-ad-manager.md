---
keywords: google ad manager;google ad;doubleclick;DoubleClick AdX;DoubleClick;Google Ad Manager;Google ad manager; DFP
title: Connessione Google Ad Manager
description: Google Ad Manager, precedentemente noto come DoubleClick for Publishers o DoubleClick AdX, è una piattaforma di ad serving di Google che offre agli editori i mezzi per gestire la visualizzazione degli annunci pubblicitari sui loro siti web, attraverso video e nelle app mobili.
exl-id: e93f1bd5-9d29-43a1-a9a6-8933f9d85150
source-git-commit: aed15e0abfd51a8a08290e78302239792f86535a
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 2%

---

# [!DNL Google Ad Manager] connection

## Panoramica {#overview}

[!DNL Google Ad Manager], precedentemente noto come [!DNL DoubleClick for Publishers] (DFP) o [!DNL DoubleClick AdX], è una piattaforma di ad serving da [!DNL Google] che offre agli editori i mezzi per gestire la visualizzazione degli annunci sui loro siti web, attraverso video e nelle app per dispositivi mobili.

## Specifiche di destinazione {#specifics}

Tieni presente i seguenti dettagli specifici per [!DNL Google Ad Manager] destinazioni:

* I tipi di pubblico attivati vengono creati a livello di programmazione nel [!DNL Google] piattaforma.
* [!DNL Platform] al momento non include una metrica di misurazione per convalidare l’attivazione. Consulta i conteggi del pubblico in Google per convalidare l’integrazione e comprendere le dimensioni del targeting del pubblico.

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

Se desideri creare la tua prima destinazione con [!DNL Google Ad Manager] e non hanno attivato il [Funzionalità di sincronizzazione ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) in Experience Cloud ID Service in passato (con Audience Manager o altre applicazioni), contatta la Consulenza Adobe o l’Assistenza clienti per abilitare la sincronizzazione degli ID. Se hai già configurato [!DNL Google] integrazioni in Audience Manager, le sincronizzazioni ID impostate riportano su Platform.

### Inserimento nell’elenco Consentiti {#allow-listing}

>[!NOTE]
>
>L’elenco consentiti è obbligatorio prima di configurare il primo [!DNL Google Ad Manager] in Platform. Assicurati che il processo di elenco consentiti descritto di seguito sia stato completato da [!DNL Google] prima di creare una destinazione.

Prima di creare il [!DNL Google Ad Manager] in Platform, devi contattare [!DNL Google] ad Adobe da inserire nell’elenco dei provider di dati consentiti e da aggiungere all’elenco consentiti il tuo account. Contatto [!DNL Google] e fornire le seguenti informazioni:

* **ID account**: ID account di Adobe con Google. ID account: 87933855.
* **ID cliente**: ID account cliente di Adobe con Google. ID cliente: 89690775.
* **Codice di rete**: Questo è il tuo [!DNL Google Ad Manager] identificatore di rete, trovato in **[!UICONTROL Amministratore > Impostazioni globali]** nell’interfaccia Google e nell’URL.
* **ID collegamento pubblico**: Questo è un identificatore specifico associato al [!DNL Google Ad Manager] rete (non il [!DNL Network code]), disponibile anche in **[!UICONTROL Amministratore > Impostazioni globali]** nell’interfaccia di Google.
* Tipo di account. DFP per Google o acquirente AdX.

## Collegati alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Per connettersi a questa destinazione, segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md).

### Parametri di connessione {#parameters}

Quando [configurazione](../../ui/connect-destination.md) questa destinazione, devi fornire le seguenti informazioni:

* **[!UICONTROL Nome]**: Compila il nome preferito per questa destinazione.
* **[!UICONTROL Descrizione]**: Facoltativo. Ad esempio, è possibile indicare per quale campagna si utilizza questa destinazione.
* **[!UICONTROL Tipo di conto]**: Seleziona un’opzione, a seconda dell’account con Google:
   * Utilizzo `DFP by Google` per [!DNL DoubleClick] per gli editori
   * Utilizzo `AdX buyer` per [!DNL Google AdX]
* **[!UICONTROL ID account]**: Compila l&#39;ID del tuo account con [!DNL Google]. Può essere il tuo codice di rete o il tuo ID di collegamento del pubblico. In genere si tratta di un ID a otto cifre.

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
