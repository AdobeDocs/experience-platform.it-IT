---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Connettore di archiviazione Google Cloud
topic: overview
translation-type: tm+mt
source-git-commit: 0ed2ed3b08f262100746f255a78c248a1748eb5e
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---


# Connettore di archiviazione Google Cloud

Adobe Experience Platform offre connettività nativa per fornitori di cloud come AWS, Google Cloud Platform e Azure, consentendo di portare i dati da questi sistemi.

Le origini di archiviazione cloud possono portare i tuoi dati in Platform senza bisogno di scaricare, formattare o caricare. I dati ingeriti possono essere formattati come JSON XDM, parquet XDM o delimitati. Ogni fase del processo è integrata nel flusso di lavoro Origini. La piattaforma consente di inserire i dati da Google Cloud Storage tramite batch.

## Configurazione obbligatoria per la connessione dell&#39;account di archiviazione Google Cloud

Per collegarsi alla piattaforma, è innanzitutto necessario abilitare l&#39;interoperabilità per l&#39;account di archiviazione Google Cloud. Per accedere all’impostazione di interoperabilità, apri Google Cloud Platform e seleziona **[!UICONTROL Settings]** dall’ **[!UICONTROL Storage]** opzione nel pannello di navigazione.

![](../../images/tutorials/create/google-cloud-storage/nav.png)

Viene **[!UICONTROL Settings]** visualizzata la pagina. Da qui potete vedere informazioni sul vostro ID progetto Google e dettagli sul vostro account Google Cloud Storage. Per accedere alle impostazioni di interoperabilità, selezionare **[!UICONTROL Interoperability]** dall&#39;intestazione superiore.

![](../../images/tutorials/create/google-cloud-storage/project-access.png)

La **[!UICONTROL Interoperability]** pagina contiene informazioni sull&#39;autenticazione, le chiavi di accesso e il progetto predefinito associato al tuo account utente. Se non avete già stabilito un progetto predefinito per l&#39;accesso interoperabile, potete impostarne uno dall&#39;interno della *[!UICONTROL Default project for interoperable access]* sezione. Se è già stato stabilito un progetto predefinito, nella sezione viene visualizzato un messaggio di conferma dell’impostazione predefinita di un progetto.

Per generare un nuovo ID chiave di accesso e una chiave di accesso segreta per il vostro account utente, selezionate **[!UICONTROL Create a Key]**.

![](../../images/tutorials/create/google-cloud-storage/interoperability.png)

Puoi usare l’ID chiave di accesso e la chiave di accesso segreta appena generati per collegare l’account Google Cloud Storage alla piattaforma.

La documentazione seguente fornisce informazioni su come collegare Google Cloud Storage alla piattaforma utilizzando le API o l&#39;interfaccia utente:

## Connetti archiviazione Google Cloud alla piattaforma

La documentazione seguente fornisce informazioni su come collegare Google Cloud Storage alla piattaforma utilizzando le API o l&#39;interfaccia utente:

### Utilizzo delle API

- [Creare un connettore di archiviazione Google Cloud utilizzando l&#39;API del servizio di flusso](../../tutorials/api/create/cloud-storage/google.md)
- [Esplora un sistema di archiviazione cloud utilizzando l&#39;API del servizio di flusso](../../tutorials/api/explore/cloud-storage.md)
- [Raccolta di dati di archiviazione cloud tramite l&#39;API del servizio di flusso](../../tutorials/api/collect/cloud-storage.md)

### Utilizzo dell’interfaccia

- [Creare un connettore di origine di archiviazione Google Cloud nell&#39;interfaccia utente](../../tutorials/ui/create/cloud-storage/google-cloud-storage.md)
- [Configurare un flusso di dati per un connettore di archiviazione cloud nell&#39;interfaccia utente](../../tutorials/ui/dataflow/batch/cloud-storage.md)