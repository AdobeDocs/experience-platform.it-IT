---
keywords: DoubleClick Bid Manager;DoubleClick bid manager;DoubleClick;Display & Video 360;display 360;video 360;Video 360;Display 360;visualizzazione e video
title: Connessione Google Display & Video 360
description: Display & Video 360, precedentemente noto come DoubleClick Bid Manager è uno strumento utilizzato per eseguire il retargeting e campagne digitali mirate al pubblico tra le origini di inventario Display, Video e Mobile.
exl-id: bdd3b3fd-891f-44ec-bd47-daf7f3289f92
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 2%

---

# [!DNL Google Display & Video 360] connection

## Panoramica {#overview}

[!DNL Display & Video 360], precedentemente noto come [!DNL DoubleClick Bid Manager], è uno strumento utilizzato per eseguire campagne digitali di retargeting e mirate per il pubblico tra le origini di inventario Display, Video e Mobile.

## Specifiche di destinazione {#specifics}

Tieni presente i seguenti dettagli specifici per [!DNL Google Display & Video 360] destinazioni:

* I tipi di pubblico attivati vengono creati a livello di programmazione nella piattaforma Google.
* [!DNL Platform] al momento non include una metrica di misurazione per convalidare l’attivazione. Consulta i conteggi del pubblico in Google per convalidare l’integrazione e comprendere le dimensioni del targeting del pubblico.

>[!IMPORTANT]
>
>Se desideri creare la tua prima destinazione con Google Display &amp; Video 360 e non hai abilitato il [Funzionalità di sincronizzazione ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) in Experience Cloud ID Service in passato (con Adobe Audience Manager o altre applicazioni), contatta la Consulenza Adobe o l’Assistenza clienti per abilitare la sincronizzazione degli ID. Se in precedenza avevi impostato le integrazioni Google in Audience Manager, le sincronizzazioni ID che avevi configurato riportano a Platform.

## Identità supportate {#supported-identities}

[!DNL Google Display & Video 360] supporta l’attivazione delle identità descritte nella tabella seguente.

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | Seleziona questa identità di destinazione quando l’identità di origine è uno spazio dei nomi GAID. |
| IDFA | [!DNL Apple ID for Advertisers] | Seleziona questa identità di destinazione quando l’identità di origine è uno spazio dei nomi IDFA. |
| UUID AAM | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html), noto anche come [!DNL Device ID]. Un ID dispositivo numerico a 38 cifre associato a ciascun dispositivo con cui interagisce. | Google utilizza [UUID AAM](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en) per eseguire il targeting degli utenti in California e dell’ID cookie di Google per tutti gli altri utenti. |
| [!DNL Google] ID cookie | [!DNL Google] ID cookie | [!DNL Google] utilizza questo ID per eseguire il targeting degli utenti al di fuori della California. |
| RIDA | ID Roku per la pubblicità. Questo ID identifica in modo univoco i dispositivi Roku. |  |
| MAID | Microsoft Advertising ID. Questo ID identifica in modo univoco i dispositivi con Windows 10. |  |
| Amazon Fire TV ID | Questo ID identifica in modo univoco i Amazon Fire TV. |  |

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, fare riferimento alla tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione del segmento]** | Stai esportando tutti i membri di un segmento (pubblico) nella destinazione Google. |
| Frequenza delle esportazioni | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni basate su API &quot;sempre attive&quot;. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del segmento, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

## Prerequisiti {#prerequisites}

### Inserimento nell’elenco Consentiti {#allow-listing}

>[!NOTE]
>
>L’inserimento nell’elenco Consentiti è obbligatorio prima di configurare il primo [!DNL Google Display & Video 360] in Platform. Prima di creare una destinazione, assicurati che il processo di inserimento nell’elenco Consentiti descritto di seguito sia stato completato da Google.

Prima di creare il [!DNL Google Display & Video 360] in Platform, devi contattare Google per richiedere l’inserimento di un Adobe nell’elenco dei provider di dati consentiti e l’aggiunta del tuo account all’elenco consentiti. Contatta Google e fornisci le seguenti informazioni:

* **ID account**: ID account di Adobe con Google. ID account: 87933855.
* **ID cliente**: ID account cliente di Adobe con Google. ID cliente: 89690775.
* **Tipo di account**: use **[!DNL Invite advertiser]** per consentire ai tipi di pubblico di essere condivisi solo con un marchio specifico nel tuo account Display &amp; Video 360 o utilizzare **[!DNL Invite partner]** per consentire ai tipi di pubblico di essere condivisi con tutti i marchi del tuo account Display &amp; Video 360.

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
   * Utilizzo `Invite Advertiser` per consentire ai tipi di pubblico di essere condivisi solo con un marchio specifico nel tuo account Display &amp; Video 360.
   * Utilizzo `Invite Partner` per consentire ai tipi di pubblico di essere condivisi con tutti i marchi del tuo account Display &amp; Video 360.
* **[!UICONTROL ID account]**: Riempi il tuo **[!DNL Invite partner]** o **[!DNL Invite advertiser]** ID account con Google. In genere si tratta di un ID a sei o sette cifre.

>[!NOTE]
>
>Quando si imposta un [!DNL Google Display & Video 360] destinazione, per favore, collabora con la tua [!DNL Google Account Manager] o rappresentante di Adobe per capire quale tipo di account hai.

### Abilitare gli avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati nella tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere le notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [iscrizione agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completati i dettagli della connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizzare i segmenti]** [autorizzazioni di controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Vedi [Attivare i dati del pubblico nelle destinazioni di esportazione dei segmenti in streaming](../../ui/activate-segment-streaming-destinations.md) per istruzioni su come attivare i segmenti di pubblico a questa destinazione.

## Dati esportati

Per verificare se i dati sono stati esportati correttamente in [!DNL Google Display & Video 360] destinazione, controlla il tuo [!DNL Google Display & Video 360] conto. Se l&#39;attivazione ha avuto successo, i tipi di pubblico vengono compilati nel tuo account.

## Risoluzione dei problemi {#troubleshooting}

### 400 Messaggio di errore di richiesta non valida {#bad-request}

Durante la configurazione di questa destinazione, potresti ricevere il seguente errore:

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

Questo errore si verifica quando gli account cliente non sono conformi alla [prerequisiti](#prerequisites). Per risolvere questo problema, contatta Google e accertati che il tuo account sia inserito nell’elenco Consentiti.