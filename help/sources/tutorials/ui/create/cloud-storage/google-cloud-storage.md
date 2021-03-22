---
keywords: Experience Platform;home;argomenti popolari;Google Cloud Storage;Google cloud storage;GCS;gcs
solution: Experience Platform
title: Creare una connessione Google Cloud Storage Source nell'interfaccia utente
topic: ' - Panoramica'
type: Tutorial
description: Scopri come creare una connessione sorgente di archiviazione Google Cloud utilizzando l’interfaccia utente di Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: f6a63ca1e21b3c3f6a55574f31fdf04038b7e5c4
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 1%

---


# Creare una connessione sorgente [!DNL Google Cloud Storage] nell&#39;interfaccia utente

I connettori sorgente in Adobe Experience Platform consentono di acquisire dati provenienti dall’esterno su base pianificata. Questa esercitazione descrive i passaggi necessari per creare un connettore sorgente [!DNL Google Cloud Storage] (in seguito denominato &quot;GCS&quot;) utilizzando l’ interfaccia utente [!DNL Platform] .

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il framework standardizzato in base al quale l’Experience Platform organizza i dati sulla customer experience.
   * [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md) dello schema: Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md) dell’Editor di schema: Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una connessione GCS valida, puoi saltare il resto del documento e continuare l&#39;esercitazione su [configurazione di un flusso di dati](../../dataflow/batch/cloud-storage.md).

### Formati di file supportati

[!DNL Experience Platform] supporta i seguenti formati di file da acquisire da archivi esterni:

* Valori separati da delimitatore (DSV): Il supporto per i file di dati formattati DSV è attualmente limitato ai valori separati da virgole. Il valore delle intestazioni di campo all&#39;interno dei file formattati DSV deve essere costituito solo da caratteri alfanumerici e caratteri di sottolineatura. Il supporto per i file DSV generali verrà fornito in futuro.
* Notazione oggetto JavaScript (JSON): I file di dati formattati JSON devono essere conformi a XDM.
* Parquet Apache: I file di dati formattati per il parquet devono essere conformi a XDM.

### Raccogli credenziali richieste

Per accedere ai dati GCS su [!DNL Platform], devi fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| ID chiave di accesso | Una stringa alfanumerica di 61 caratteri utilizzata per autenticare l’account [!DNL Google Cloud Storage] in Platform. |
| Chiave di accesso segreta | Una stringa con codifica base a 64 caratteri utilizzata per autenticare l&#39;account [!DNL Google Cloud Storage] in Platform. |

Per ulteriori informazioni su questi valori, consulta la guida [Chiavi HMAC di Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) . Per i passaggi su come generare il proprio ID chiave di accesso e la chiave di accesso segreta, consulta la [[!DNL Google Cloud Storage] panoramica](../../../../connectors/cloud-storage/google-cloud-storage.md).

## Connetti il tuo account [!DNL Google Cloud Storage]

Una volta raccolte le credenziali richieste, puoi seguire i passaggi seguenti per collegare il tuo account GCS a [!DNL Platform].

Accedi a [Adobe Experience Platform](https://platform.adobe.com) e seleziona **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro **[!UICONTROL Sources]**. Nella schermata **[!UICONTROL Catalog]** sono visualizzate diverse origini per le quali è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando l’opzione di ricerca.

Sotto la categoria **[!UICONTROL Databases]**, selezionare **[!UICONTROL Google Cloud Storage]**. Se questa è la prima volta che utilizzi questo connettore, seleziona **[!UICONTROL Configure]**. In caso contrario, seleziona **[!UICONTROL Add data]** per creare un nuovo connettore GCS.

![catalogo](../../../../images/tutorials/create/google-cloud-storage/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connect to Google Cloud Storage]** . In questa pagina è possibile utilizzare le nuove credenziali o le credenziali esistenti.

### Nuovo account

Se utilizzi nuove credenziali, seleziona **[!UICONTROL New account]**. Nel modulo di input visualizzato, fornisci un nome, una descrizione facoltativa e le credenziali GCS. Al termine, selezionare **[!UICONTROL Connect]** e quindi concedere un po&#39; di tempo per l&#39;impostazione della nuova connessione.

![connect](../../../../images/tutorials/create/google-cloud-storage/connect.png)

### Account esistente

Per collegare un account esistente, seleziona l’account GCS con cui desideri connetterti, quindi seleziona **[!UICONTROL Next]** per procedere.

![esistente](../../../../images/tutorials/create/google-cloud-storage/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account GCS. Ora puoi continuare l’esercitazione successiva e [configurare un flusso di dati per inserire i dati dall’archiviazione cloud in [!DNL Platform]](../../dataflow/batch/cloud-storage.md).