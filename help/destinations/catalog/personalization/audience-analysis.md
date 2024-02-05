---
title: Destinazione di Audience Analysis
description: Visualizza i tipi di pubblico per i quali i clienti si qualificano nel Customer Journey Analytics.
badgeLimitedAvailability: label="Disponibilità limitata" type="Informative"
source-git-commit: 83b3d40e17f444555769020526bb723265a09eb9
workflow-type: tm+mt
source-wordcount: '801'
ht-degree: 2%

---

# Destinazione di Audience Analysis

Il [!UICONTROL Analisi del pubblico] destinazione ti consente di arricchire i dati del pubblico di Adobe Experience Platform in [Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-overview.html?lang=it). Puoi selezionare i tipi di pubblico da includere nei dati arricchiti risultanti. Le qualifiche del pubblico sono quindi disponibili come dimensioni in [Analysis Workspace](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/home.html) reportistica.

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
| GAID | Google Advertising ID | Seleziona l’identità di destinazione GAID quando l’identità di origine è uno spazio dei nomi GAID. |
| IDFA | Apple ID per inserzionisti | Selezionare l&#39;identità di destinazione IDFA quando l&#39;identità di origine è uno spazio dei nomi IDFA. |
| ECID | Experience Cloud ID | Uno spazio dei nomi che rappresenta ECID. A questo spazio dei nomi possono fare riferimento anche i seguenti alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Vedi il seguente documento su [ECID](/help/identity-service/features/ecid.md) per ulteriori informazioni. |
| phone_sha256 | Numeri di telefono con hash con algoritmo SHA256 | I numeri di telefono con hash SHA256 e testo normale sono supportati da Adobe Experience Platform. Quando il campo sorgente contiene attributi senza hash, seleziona la **[!UICONTROL Applica trasformazione]** opzione, per avere [!DNL Platform] esegui automaticamente l’hash dei dati all’attivazione. |
| email_lc_sha256 | Indirizzi e-mail con hash con algoritmo SHA256 | Adobe Experience Platform supporta sia gli indirizzi di posta elettronica in testo normale che quelli con hash SHA256. Quando il campo sorgente contiene attributi senza hash, seleziona la **[!UICONTROL Applica trasformazione]** opzione, per avere [!DNL Platform] esegui automaticamente l’hash dei dati all’attivazione. |
| extern_id | ID utente personalizzati | Seleziona questa identità di destinazione quando l&#39;identità di origine è uno spazio dei nomi personalizzato. |

{style="table-layout:auto"}

## Tipi di pubblico supportati

Quando si utilizza questa destinazione sono supportati i seguenti tipi di pubblico:

| Origine pubblico | Supportati | Descrizione |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Tipi di pubblico generati dall’Experience Platform [Servizio di segmentazione](../../../segmentation/home.md). |
| Caricamenti personalizzati | ✓ | Tipi di pubblico [importato](../../../segmentation/ui/overview.md#import-audience) in Experienci Platform da file CSV. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione pubblico]** | Stai esportando tutti i membri di un pubblico con gli identificatori (nome, numero di telefono o altri) utilizzati nella destinazione Audience Analysis. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Quando un profilo viene aggiornato in Experienci Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni su [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Configurare una nuova destinazione

>[!IMPORTANT]
> 
>Per creare la destinazione, è necessario **[!UICONTROL Visualizza destinazioni]** e **[!UICONTROL Gestire le destinazioni]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per creare questa destinazione, segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md).

### Dettagli della destinazione

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

* **[!UICONTROL Nome]**: nome della destinazione.
* **[!UICONTROL Descrizione]**: descrizione della destinazione.
* **[!UICONTROL ID flusso di dati]**: l’ID dello stream di dati che desideri arricchire con i tipi di pubblico idonei. Puoi ottenere questo ID in [Gestione flussi di dati](/help/datastreams/overview.md).
* **[!UICONTROL Alias di integrazione]**: alias di integrazione.

### Avvisi

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

* **[!UICONTROL Frequenza di attivazione ignorata superata]**: Ricevi una notifica quando la velocità di attivazione saltata supera una soglia.

Una volta completate le informazioni sulla connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

### Politiche di governance e azioni di esecuzione

Questa sezione facoltativa ti consente di definire i criteri di governance dei dati e di garantire che i dati utilizzati siano conformi quando i tipi di pubblico vengono inviati e sono attivi.

Dopo aver selezionato le azioni di marketing desiderate per la destinazione, seleziona **[!UICONTROL Crea]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Una volta creata la destinazione, puoi attivare il pubblico desiderato per la destinazione.

1. Se non ti trovi già nella destinazione creata, puoi trovarla nuovamente accedendo a **[!UICONTROL Destinazioni]** > **[!UICONTROL Sfoglia]**.
1. Seleziona **[!UICONTROL Attiva tipi di pubblico]**.
1. Seleziona i tipi di pubblico desiderati per i quali desideri analizzare le qualifiche. Al termine, seleziona **[!UICONTROL Successivo]**.
1. Controlla la configurazione di destinazione e le impostazioni del pubblico, quindi seleziona **[!UICONTROL Fine]**.

Puoi aggiungere altri tipi di pubblico da analizzare in futuro tornando alla sezione **[!UICONTROL Attiva tipi di pubblico]** pagina. Una volta attivati, i tipi di pubblico non possono essere rimossi.
