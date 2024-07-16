---
title: Destinazione di Audience Analysis
description: Visualizza i tipi di pubblico per i quali i clienti si qualificano nel Customer Journey Analytics.
badgeLimitedAvailability: label="Disponibilità limitata" type="Informative"
exl-id: 81437237-d746-4ce9-b938-7d2541f0ed32
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '801'
ht-degree: 3%

---

# Destinazione di Audience Analysis

La destinazione di [!UICONTROL Audience Analysis] ti consente di arricchire i dati del pubblico di Adobe Experience Platform in [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=it). Puoi selezionare i tipi di pubblico da includere nei dati arricchiti risultanti. Le qualifiche del pubblico sono quindi disponibili come dimensioni nel reporting di [Analysis Workspace](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/home.html).

>[!AVAILABILITY]
>
>Questa destinazione è in una fase di test limitata. Se ti interessa utilizzare questa destinazione, contatta il team del tuo account Adobe.

## Prerequisiti

Prima di utilizzare questa destinazione sono necessari i seguenti elementi:

* È necessario essere provvisti del provisioning per utilizzare la destinazione Audience Analysis. Se non hai ancora effettuato il provisioning per utilizzare questa destinazione, contatta il team del tuo account di Adobe.
* Per utilizzare il Customer Journey Analytics, è necessario disporre del provisioning.
* Devi avere almeno un pubblico creato in Adobe Experience Platform.

## Identità supportate

Audience Analysis supporta l’attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/features/namespaces.md). In genere viene utilizzato l’ID Experience Cloud (ECID).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Seleziona l’identità di destinazione GAID quando l’identità di origine è uno spazio dei nomi GAID. |
| IDFA | Apple ID per inserzionisti | Selezionare l&#39;identità di destinazione IDFA quando l&#39;identità di origine è uno spazio dei nomi IDFA. |
| ECID | Experience Cloud ID | Uno spazio dei nomi che rappresenta ECID. A questo spazio dei nomi possono fare riferimento anche i seguenti alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Per ulteriori informazioni, consulta il seguente documento su [ECID](/help/identity-service/features/ecid.md). |
| phone_sha256 | Numeri di telefono con hash con algoritmo SHA256 | I numeri di telefono con hash SHA256 e testo normale sono supportati da Adobe Experience Platform. Se il campo di origine contiene attributi senza hash, selezionare l&#39;opzione **[!UICONTROL Applica trasformazione]** per impostare [!DNL Platform] per l&#39;hashing automatico dei dati all&#39;attivazione. |
| email_lc_sha256 | Indirizzi e-mail con hash con algoritmo SHA256 | Adobe Experience Platform supporta sia gli indirizzi di posta elettronica in testo normale che quelli con hash SHA256. Se il campo di origine contiene attributi senza hash, selezionare l&#39;opzione **[!UICONTROL Applica trasformazione]** per impostare [!DNL Platform] per l&#39;hashing automatico dei dati all&#39;attivazione. |
| extern_id | ID utente personalizzati | Seleziona questa identità di destinazione quando l&#39;identità di origine è uno spazio dei nomi personalizzato. |

{style="table-layout:auto"}

## Tipi di pubblico supportati

Quando si utilizza questa destinazione sono supportati i seguenti tipi di pubblico:

| Origine pubblico | Supportato | Descrizione |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Tipi di pubblico generati tramite il servizio di segmentazione [Experience Platform](../../../segmentation/home.md). |
| Caricamenti personalizzati | ✓ | Tipi di pubblico [importati](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform da file CSV. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione pubblico]** | Stai esportando tutti i membri di un pubblico con gli identificatori (nome, numero di telefono o altri) utilizzati nella destinazione Audience Analysis. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Quando un profilo viene aggiornato in Experience Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni sulle [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Configura una nuova destinazione

>[!IMPORTANT]
> 
>Per creare la destinazione, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Visualizza destinazioni]** e **[!UICONTROL Gestione destinazioni]** [Controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per creare questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md).

### Dettagli della destinazione

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

* **[!UICONTROL Nome]**: nome della destinazione.
* **[!UICONTROL Descrizione]**: descrizione della destinazione.
* **[!UICONTROL ID dello stream di dati]**: l&#39;ID dello stream di dati che desideri arricchire con i tipi di pubblico idonei. È possibile ottenere questo ID nel [Gestore flussi di dati](/help/datastreams/overview.md).
* **[!UICONTROL Alias integrazione]**: alias integrazione.

### Avvisi

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

* **[!UICONTROL Frequenza di attivazione ignorata superata]**: ricevi una notifica quando la frequenza di attivazione ignorata supera una soglia.

Dopo aver fornito i dettagli per la connessione di destinazione, seleziona **[!UICONTROL Avanti]**.

### Politiche di governance e azioni di esecuzione

Questa sezione facoltativa ti consente di definire i criteri di governance dei dati e di garantire che i dati utilizzati siano conformi quando i tipi di pubblico vengono inviati e sono attivi.

Dopo aver selezionato le azioni di marketing desiderate per la destinazione, selezionare **[!UICONTROL Crea]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Una volta creata la destinazione, puoi attivare il pubblico desiderato per la destinazione.

1. Se non sei già nella destinazione creata, puoi individuarla nuovamente passando a **[!UICONTROL Destinazioni]** > **[!UICONTROL Sfoglia]**.
1. Seleziona **[!UICONTROL Attiva pubblico]**.
1. Seleziona i tipi di pubblico desiderati per i quali desideri analizzare le qualifiche. Al termine, selezionare **[!UICONTROL Avanti]**.
1. Rivedi la configurazione di destinazione e le impostazioni del pubblico, quindi seleziona **[!UICONTROL Fine]**.

Puoi aggiungere altri tipi di pubblico da analizzare in futuro tornando alla pagina **[!UICONTROL Attiva tipi di pubblico]**. Una volta attivati, i tipi di pubblico non possono essere rimossi.
