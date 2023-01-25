---
title: Creazione di una connessione Google Cloud Storage Source nell'interfaccia utente
description: Scopri come creare una connessione sorgente Google Cloud Storage utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 3258ccd7-757c-4c4a-b7bb-0e8c9de3b50a
source-git-commit: 7181cb92dd44d8005fe1054020ffeb36c309b42e
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 1%

---

# Crea un [!DNL Google Cloud Storage] connessione sorgente nell’interfaccia utente

Questa esercitazione fornisce i passaggi per la creazione di un [!DNL Google Cloud Storage] connessione sorgente tramite l’interfaccia utente di Adobe Experience Platform.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il framework standardizzato in base al quale l’Experience Platform organizza i dati sulla customer experience.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’Editor di schema](../../../../../xdm/tutorials/create-schema-ui.md): Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una [!DNL Google Cloud Storage] è possibile ignorare il resto del documento e passare all&#39;esercitazione su [configurazione di un flusso di dati](../../dataflow/batch/cloud-storage.md).

### Formati di file supportati

[!DNL Experience Platform] supporta i seguenti formati di file da acquisire da archivi esterni:

* Valori separati da delimitatore (DSV): Qualsiasi valore a carattere singolo può essere utilizzato come delimitatore per i file di dati in formato DSV.
* Notazione oggetto JavaScript (JSON): I file di dati formattati JSON devono essere conformi a XDM.
* Parquet Apache: I file di dati formattati per il parquet devono essere conformi a XDM.

### Raccogli credenziali richieste

Per accedere al tuo [!DNL Google Cloud Storage] su Platform, devi fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| ID chiave di accesso | Una stringa alfanumerica di 61 caratteri utilizzata per autenticare il tuo [!DNL Google Cloud Storage] a Platform. |
| Chiave di accesso segreta | Una stringa con codifica base a 64 caratteri utilizzata per l&#39;autenticazione [!DNL Google Cloud Storage] a Platform. |
| Nome blocco | Il nome del tuo [!DNL Google Cloud Storage] secchio. È necessario specificare un nome per il bucket se si desidera fornire l’accesso a una sottocartella specifica nell’archiviazione cloud. |
| Percorso cartella | Percorso della cartella a cui si desidera fornire l&#39;accesso. |

Per ulteriori informazioni su questi valori, consulta la sezione [Chiavi HMAC di Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) guida. Per i passaggi su come generare il tuo ID chiave di accesso e la chiave di accesso segreta, consulta [[!DNL Google Cloud Storage] panoramica](../../../../connectors/cloud-storage/google-cloud-storage.md).

Una volta raccolte le credenziali richieste, puoi seguire i passaggi seguenti per collegare il tuo [!DNL Google Cloud Storage] a Platform.

## Collega il tuo [!DNL Google Cloud Storage] account

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Origini] workspace. La [!UICONTROL Catalogo] in viene visualizzata una varietà di sorgenti con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando l’opzione di ricerca.

Sotto la [!UICONTROL archiviazione cloud] categoria, seleziona **[!UICONTROL Google Cloud Storage]** quindi seleziona **[!UICONTROL Aggiungi dati]**.

![Nella schermata dell’interfaccia utente della piattaforma viene visualizzata la pagina del catalogo origini.](../../../../images/tutorials/create/google-cloud-storage/catalog.png)

La **[!UICONTROL Connessione a Google Cloud Storage]** viene visualizzata la pagina . In questa pagina è possibile utilizzare le nuove credenziali o le credenziali esistenti.

### Account esistente

Per collegare un account esistente, seleziona la [!DNL Google Cloud Storage] account con cui desideri connetterti, quindi seleziona **[!UICONTROL Successivo]** per procedere.

![Schermata dell’interfaccia utente di Platform che mostra la pagina dell’account esistente per un’origine Google Cloud Storage](../../../../images/tutorials/create/google-cloud-storage/existing.png)

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, specificare un nome, una descrizione facoltativa e il [!DNL Google Cloud Storage] credenziali. Durante questo passaggio, puoi inoltre designare le sottocartelle a cui l’account avrà accesso definendo il nome del percorso della sottocartella.

Al termine, seleziona **[!UICONTROL Connetti alla sorgente]** e quindi lasciare un po&#39; di tempo per stabilire la nuova connessione.

![Schermata dell’interfaccia utente di Platform che mostra la nuova pagina dell’account per un’origine Google Cloud Storage.](../../../../images/tutorials/create/google-cloud-storage/new.png)


## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo [!DNL Google Cloud Storage] conto. Ora puoi passare all’esercitazione successiva e [configurare un flusso di dati per l’importazione di dati dall’archiviazione cloud in Platform](../../dataflow/batch/cloud-storage.md).
