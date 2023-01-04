---
keywords: Experience Platform;home;argomenti comuni;Google Cloud Storage;Google cloud storage;GCS;gcs
solution: Experience Platform
title: Creazione di una connessione Google Cloud Storage Source nell'interfaccia utente
topic-legacy: overview
type: Tutorial
description: Scopri come creare una connessione sorgente Google Cloud Storage utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 3258ccd7-757c-4c4a-b7bb-0e8c9de3b50a
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 1%

---

# Crea un [!DNL Google Cloud Storage] connessione sorgente nell’interfaccia utente

I connettori sorgente in Adobe Experience Platform consentono di acquisire dati provenienti dall’esterno su base pianificata. Questa esercitazione fornisce i passaggi per la creazione di un [!DNL Google Cloud Storage] (in seguito denominato &quot;GCS&quot;) connettore di sorgente che utilizza [!DNL Platform] interfaccia utente.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il framework standardizzato in base al quale l’Experience Platform organizza i dati sulla customer experience.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’Editor di schema](../../../../../xdm/tutorials/create-schema-ui.md): Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una connessione GCS valida, puoi saltare il resto del documento e procedere all&#39;esercitazione su [configurazione di un flusso di dati](../../dataflow/batch/cloud-storage.md).

### Formati di file supportati

[!DNL Experience Platform] supporta i seguenti formati di file da acquisire da archivi esterni:

* Valori separati da delimitatore (DSV): Il supporto per i file di dati formattati DSV è attualmente limitato ai valori separati da virgole. Il valore delle intestazioni di campo all&#39;interno dei file formattati DSV deve essere costituito solo da caratteri alfanumerici e caratteri di sottolineatura. Il supporto per i file DSV generali verrà fornito in futuro.
* Notazione oggetto JavaScript (JSON): I file di dati formattati JSON devono essere conformi a XDM.
* Parquet Apache: I file di dati formattati per il parquet devono essere conformi a XDM.

### Raccogli credenziali richieste

Per accedere ai dati GCS su [!DNL Platform], è necessario fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| ID chiave di accesso | Una stringa alfanumerica di 61 caratteri utilizzata per autenticare il tuo [!DNL Google Cloud Storage] a Platform. |
| Chiave di accesso segreta | Una stringa con codifica base a 64 caratteri utilizzata per l&#39;autenticazione [!DNL Google Cloud Storage] a Platform. |

Per ulteriori informazioni su questi valori, consulta la sezione [Chiavi HMAC di Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) guida. Per i passaggi su come generare il tuo ID chiave di accesso e la chiave di accesso segreta, consulta [[!DNL Google Cloud Storage] panoramica](../../../../connectors/cloud-storage/google-cloud-storage.md).

## Collega il tuo [!DNL Google Cloud Storage] account

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi seguenti per collegare il tuo account GCS a [!DNL Platform].

Accedi a [Adobe Experience Platform](https://platform.adobe.com) quindi seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere al **[!UICONTROL Origini]** workspace. La **[!UICONTROL Catalogo]** in questa schermata vengono visualizzate diverse sorgenti per le quali è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando l’opzione di ricerca.

Sotto la **[!UICONTROL Database]** categoria, seleziona **[!UICONTROL Google Cloud Storage]**. Se questa è la prima volta che utilizzi questo connettore, seleziona **[!UICONTROL Configura]**. In caso contrario, seleziona **[!UICONTROL Aggiungi dati]** per creare un nuovo connettore GCS.

![catalogo](../../../../images/tutorials/create/google-cloud-storage/catalog.png)

La **[!UICONTROL Connessione a Google Cloud Storage]** viene visualizzata la pagina . In questa pagina è possibile utilizzare le nuove credenziali o le credenziali esistenti.

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, fornisci un nome, una descrizione facoltativa e le credenziali GCS. Al termine, seleziona **[!UICONTROL Connetti]** e quindi lasciare un po&#39; di tempo per stabilire la nuova connessione.

![connect](../../../../images/tutorials/create/google-cloud-storage/connect.png)

### Account esistente

Per collegare un account esistente, seleziona l’account GCS con cui desideri connetterti, quindi seleziona **[!UICONTROL Successivo]** per procedere.

![esistente](../../../../images/tutorials/create/google-cloud-storage/existing.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account GCS. Ora puoi passare all’esercitazione successiva e [configurare un flusso di dati per inserire i dati dall’archiviazione cloud in [!DNL Platform]](../../dataflow/batch/cloud-storage.md).
