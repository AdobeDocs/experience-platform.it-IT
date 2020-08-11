---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Creare un connettore di origine di archiviazione Google Cloud nell'interfaccia utente
topic: overview
translation-type: tm+mt
source-git-commit: 41fe3e5b2a830c3182b46b3e0873b1672a1f1b03
workflow-type: tm+mt
source-wordcount: '522'
ht-degree: 1%

---


# Creare un connettore [!DNL Google Cloud Storage] sorgente nell’interfaccia utente

I connettori di origine in Adobe Experience Platform consentono di trasferire i dati esternamente originati su base programmata. Questa esercitazione fornisce i passaggi necessari per creare un connettore sorgente [!DNL Google Cloud Storage] (in seguito denominato &quot;GCS&quot;) utilizzando l&#39;interfaccia [!DNL Platform] utente.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)XDM (Experience Data Model): Il framework standard con cui  Experience Platform organizza i dati sull&#39;esperienza dei clienti.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md)dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md)sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
* [Profilo](../../../../../profile/home.md)cliente in tempo reale: Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponete già di una connessione di base GCS, potete ignorare il resto del documento e procedere all&#39;esercitazione sulla [configurazione di un flusso di dati](../../dataflow/batch/cloud-storage.md).

### Formati di file supportati

[!DNL Experience Platform] supporta i seguenti formati di file da acquisire da archivi esterni:

* Valori separati da delimitatore (DSV): Il supporto per i file di dati in formato DSV è attualmente limitato ai valori separati da virgole. Il valore delle intestazioni dei campi all&#39;interno dei file formattati DSV deve essere costituito solo da caratteri alfanumerici e caratteri di sottolineatura. In futuro verrà fornito il supporto per i file DSV generali.
* JavaScript Object Notation (JSON): I file di dati formattati JSON devono essere conformi a XDM.
* Parquet Apache: I file di dati in formato parquet devono essere conformi a XDM.

### Raccogli credenziali richieste

Per accedere ai dati GCS su [!DNL Platform], devi fornire un ID **di** accesso GCS valido e un **Segreto**. Per ulteriori informazioni su come ottenere questi valori, consultate la guida <a href="https://cloud.google.com/docs/authentication/production" target="_blank">all&#39;autenticazione da</a> server a server per [!DNL Google Cloud].

## Collegamento dell&#39;account GCS

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi descritti di seguito per creare un nuovo account GCS a cui connetterti [!DNL Platform].

Accedete ad [Adobe Experience Platform](https://platform.adobe.com) , quindi selezionate **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39; *[!UICONTROL Sources]* area di lavoro. Nella *[!UICONTROL Catalog]* schermata sono visualizzate diverse origini con le quali è possibile creare un account in entrata e ogni origine mostra il numero di account e flussi di dati esistenti associati a tali account.

Potete selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l&#39;origine specifica con cui si desidera lavorare utilizzando l&#39;opzione di ricerca.

Sotto la *[!UICONTROL Databases]* categoria, selezionare **[!UICONTROL Google Cloud Storage]** seguita da **[!UICONTROL Add data]** per creare un nuovo connettore GCS.

![catalogo](../../../../images/tutorials/create/google-cloud-storage/catalog.png)

Viene *[!UICONTROL Connect to Google Cloud Storage]* visualizzata la pagina. In questa pagina è possibile utilizzare credenziali nuove o già esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL New account]**. Nel modulo di input visualizzato, fornite alla connessione un nome, una descrizione facoltativa e le credenziali GCS. Al termine, selezionate **[!UICONTROL Connect]** e concedete un po&#39; di tempo per l&#39;impostazione del nuovo account.

![connect](../../../../images/tutorials/create/google-cloud-storage/connect.png)

### Account esistente

Per collegare un account esistente, selezionate l&#39;account GCS con cui desiderate connettervi, quindi selezionate **[!UICONTROL Next]** per continuare.

![esistenti](../../../../images/tutorials/create/google-cloud-storage/existing.png)

## Passaggi successivi

Seguendo questa esercitazione hai stabilito una connessione al tuo account GCS. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per trasferire i dati dall’archiviazione cloud alla piattaforma](../../dataflow/batch/cloud-storage.md).