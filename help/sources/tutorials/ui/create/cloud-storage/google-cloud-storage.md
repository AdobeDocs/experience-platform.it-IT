---
title: Creare una connessione sorgente dell’archiviazione cloud di Google nell’interfaccia utente
description: Scopri come creare una connessione sorgente di Google Cloud Storage utilizzando l’interfaccia utente di Adobe Experience Platform.
exl-id: 3258ccd7-757c-4c4a-b7bb-0e8c9de3b50a
source-git-commit: 7181cb92dd44d8005fe1054020ffeb36c309b42e
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 1%

---

# Creare un [!DNL Google Cloud Storage] connessione sorgente nell’interfaccia utente

Questo tutorial descrive i passaggi necessari per creare [!DNL Google Cloud Storage] connessione sorgente tramite l’interfaccia utente di Adobe Experience Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato tramite il quale Experience Platform organizza i dati sull’esperienza del cliente.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri gli elementi di base degli schemi XDM, compresi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di un [!DNL Google Cloud Storage] connessione, è possibile saltare il resto del documento e passare all&#39;esercitazione [configurazione di un flusso di dati](../../dataflow/batch/cloud-storage.md).

### Formati di file supportati

[!DNL Experience Platform] supporta i seguenti formati di file da acquisire da archivi esterni:

* Valori delimitatori separati (DSV): qualsiasi valore a carattere singolo può essere utilizzato come delimitatore per i file di dati in formato DSV.
* JSON (JavaScript Object Notation): i file di dati formattati JSON devono essere conformi a XDM.
* Apache Parquet: i file di dati formattati con Parquet devono essere conformi a XDM.

### Raccogli le credenziali richieste

Per accedere al tuo [!DNL Google Cloud Storage] dati su Platform, è necessario fornire i seguenti valori:

| Credenziali | Descrizione |
| ---------- | ----------- |
| ID chiave di accesso | Una stringa alfanumerica di 61 caratteri utilizzata per autenticare il [!DNL Google Cloud Storage] da un account a Platform. |
| Chiave di accesso segreta | Una stringa con codifica base 64 di 40 caratteri utilizzata per autenticare il [!DNL Google Cloud Storage] da un account a Platform. |
| Nome bucket | Il nome del tuo [!DNL Google Cloud Storage] secchio. Se desideri fornire l’accesso a una sottocartella specifica nell’archiviazione cloud, devi specificare un nome di bucket. |
| Percorso cartella | Percorso della cartella a cui desideri fornire l’accesso. |

Per ulteriori informazioni su questi valori, vedere [Chiavi HMAC di Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) guida. Per i passaggi su come generare il proprio ID chiave di accesso e la propria chiave di accesso segreta, consulta [[!DNL Google Cloud Storage] panoramica](../../../../connectors/cloud-storage/google-cloud-storage.md).

Dopo aver raccolto le credenziali richieste, puoi seguire la procedura riportata di seguito per collegare il tuo [!DNL Google Cloud Storage] da un account a Platform.

## Connetti [!DNL Google Cloud Storage] account

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] Workspace. Il [!UICONTROL Catalogo] Nella schermata vengono visualizzate diverse origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Sotto [!UICONTROL Archiviazione cloud] categoria, seleziona **[!UICONTROL Archiviazione cloud Google]** e quindi seleziona **[!UICONTROL Aggiungi dati]**.

![La schermata dell’interfaccia utente di Platform mostra la pagina del catalogo delle sorgenti.](../../../../images/tutorials/create/google-cloud-storage/catalog.png)

Il **[!UICONTROL Connessione a Google Cloud Storage]** viene visualizzata. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Account esistente

Per collegare un account esistente, seleziona la [!DNL Google Cloud Storage] account con cui desideri connetterti, quindi seleziona **[!UICONTROL Successivo]** per procedere.

![La schermata dell’interfaccia utente di Platform mostra la pagina dell’account esistente per un’origine di archiviazione cloud Google](../../../../images/tutorials/create/google-cloud-storage/existing.png)

### Nuovo account

Se si utilizzano nuove credenziali, selezionare **[!UICONTROL Nuovo account]**. Nel modulo di input visualizzato, fornisci un nome, una descrizione facoltativa e il [!DNL Google Cloud Storage] credenziali. Durante questo passaggio, puoi anche designare le sottocartelle a cui il tuo account avrà accesso definendo il nome del percorso della sottocartella.

Al termine, seleziona **[!UICONTROL Connetti all&#39;origine]** e quindi lascia un po’ di tempo per stabilire la nuova connessione.

![Nella schermata dell’interfaccia utente di Platform viene visualizzata la pagina del nuovo account per un’origine di archiviazione cloud Google.](../../../../images/tutorials/create/google-cloud-storage/new.png)


## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione con il tuo [!DNL Google Cloud Storage] account. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per portare i dati dall’archiviazione cloud a Platform](../../dataflow/batch/cloud-storage.md).
