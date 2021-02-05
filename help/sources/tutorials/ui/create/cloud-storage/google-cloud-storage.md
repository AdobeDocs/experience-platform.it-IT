---
keywords: Experience Platform ;home;argomenti popolari;Google Cloud Storage;google cloud storage;GCS;gcs
solution: Experience Platform
title: Creare una connessione di origine di archiviazione Google Cloud nell'interfaccia utente
topic: overview
type: Tutorial
description: Scopri come creare una connessione di origine di archiviazione Google Cloud utilizzando l'interfaccia utente di Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 1%

---


# Creare una connessione di origine [!DNL Google Cloud Storage] nell&#39;interfaccia utente

I connettori di origine in Adobe Experience Platform consentono di trasferire i dati esternamente originati su base programmata. Questa esercitazione fornisce i passaggi necessari per creare un connettore sorgente [!DNL Google Cloud Storage] (di seguito &quot;GCS&quot;) utilizzando l&#39;interfaccia utente [!DNL Platform].

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il framework standard con cui  Experience Platform organizza i dati sull&#39;esperienza dei clienti.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md) dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md) sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponete già di una connessione GCS valida, potete ignorare il resto del documento e continuare l&#39;esercitazione su [configurazione di un flusso di dati](../../dataflow/batch/cloud-storage.md).

### Formati di file supportati

[!DNL Experience Platform] supporta i seguenti formati di file da acquisire da archivi esterni:

* Valori separati da delimitatore (DSV): Il supporto per i file di dati in formato DSV è attualmente limitato ai valori separati da virgole. Il valore delle intestazioni dei campi all&#39;interno dei file formattati DSV deve essere costituito solo da caratteri alfanumerici e caratteri di sottolineatura. In futuro verrà fornito il supporto per i file DSV generali.
* JavaScript Object Notation (JSON): I file di dati formattati JSON devono essere conformi a XDM.
* Parquet Apache: I file di dati in formato parquet devono essere conformi a XDM.

### Raccogli credenziali richieste

Per accedere ai dati GCS su [!DNL Platform], è necessario fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| ID chiave di accesso | ID chiave di accesso dell&#39;account [!DNL Google Cloud Storage]. |
| Chiave di accesso segreta | Il segreto client dell&#39;account [!DNL Google Cloud Storage]. |

Per ulteriori informazioni su come iniziare, fare riferimento a [guida all&#39;autenticazione server-to-server](https://cloud.google.com/docs/authentication/production) per [!DNL Google Cloud Storage].

## Collegare l&#39;account [!DNL Google Cloud Storage]

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi descritti di seguito per collegare l&#39;account GCS a [!DNL Platform].

Accedete a [Adobe Experience Platform](https://platform.adobe.com), quindi selezionate **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro **[!UICONTROL Sources]**. Nella schermata **[!UICONTROL Catalog]** sono visualizzate diverse sorgenti con le quali è possibile creare un account.

Potete selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l&#39;origine specifica con cui si desidera lavorare utilizzando l&#39;opzione di ricerca.

Sotto la categoria **[!UICONTROL Databases]**, selezionare **[!UICONTROL Google Cloud Storage]**. Se si tratta della prima volta che si utilizza questo connettore, selezionare **[!UICONTROL Configure]**. In caso contrario, selezionare **[!UICONTROL Add data]** per creare un nuovo connettore GCS.

![catalogo](../../../../images/tutorials/create/google-cloud-storage/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connect to Google Cloud Storage]**. In questa pagina è possibile utilizzare credenziali nuove o già esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL New account]**. Nel modulo di input visualizzato, fornite un nome, una descrizione facoltativa e le credenziali GCS. Al termine, selezionare **[!UICONTROL Connect]**, quindi concedere un po&#39; di tempo per stabilire la nuova connessione.

![connect](../../../../images/tutorials/create/google-cloud-storage/connect.png)

### Account esistente

Per collegare un account esistente, selezionate l&#39;account GCS con cui desiderate connettervi, quindi selezionate **[!UICONTROL Next]** per continuare.

![esistenti](../../../../images/tutorials/create/google-cloud-storage/existing.png)

## Passaggi successivi

Seguendo questa esercitazione hai stabilito una connessione al tuo account GCS. È ora possibile continuare l&#39;esercitazione successiva e [configurare un flusso di dati per portare i dati dall&#39;archiviazione cloud in  [!DNL Platform]](../../dataflow/batch/cloud-storage.md).