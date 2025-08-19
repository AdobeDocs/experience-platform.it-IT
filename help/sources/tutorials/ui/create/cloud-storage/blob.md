---
title: Collegare l’archiviazione BLOB di Azure ad Experience Platform nell’interfaccia utente
description: Scopri come collegare l’account di archiviazione Azure Blob ad Experience Platform utilizzando l’area di lavoro delle origini nell’interfaccia utente.
exl-id: 0e54569b-7305-4065-981e-951623717648
source-git-commit: 7acdc090c020de31ee1a010d71a2969ec9e5bbe1
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 1%

---

# Connetti [!DNL Azure Blob Storage] ad Experience Platform tramite l&#39;interfaccia utente

Leggi questa guida per scoprire come connettere l&#39;istanza [!DNL Azure Blob Storage] a Adobe Experience Platform utilizzando l&#39;area di lavoro origini nell&#39;interfaccia utente di Experience Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato per organizzare i dati sull&#39;esperienza del cliente in Experience Platform.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una connessione [!DNL Azure Blob Storage] valida, puoi saltare il resto del documento e passare all&#39;esercitazione [configurazione di un flusso di dati](../../dataflow/batch/cloud-storage.md).

### Formati di file supportati

Experience Platform supporta i seguenti formati di file da acquisire da archivi esterni:

* Valori separati da delimitatore (DSV): è possibile utilizzare qualsiasi delimitatore a colonna singola, ad esempio tabulazione, virgola, barra verticale, punto e virgola o hash per raccogliere file flat in qualsiasi formato.
* JavaScript Object Notation (JSON): i file di dati formattati JSON devono essere conformi a XDM.
* Apache Parquet: i file di dati formattati con Parquet devono essere conformi a XDM.

### Raccogli le credenziali richieste

Per informazioni sull&#39;autenticazione, leggere la [[!DNL Azure Blob Storage] panoramica](../../../../connectors/cloud-storage/blob.md#authentication).

## Navigare nel catalogo delle origini

Nell&#39;interfaccia utente di Experience Platform, seleziona **[!UICONTROL Origini]** dal menu di navigazione a sinistra per accedere all&#39;area di lavoro *[!UICONTROL Origini]*. Scegliere una categoria o utilizzare la barra di ricerca per trovare l&#39;origine.

Per connettersi a [!DNL Azure Blob Storage], passare alla categoria *[!UICONTROL Archiviazione cloud]*, selezionare la scheda di origine **[!UICONTROL Archiviazione BLOB di Azure]**, quindi selezionare **[!UICONTROL Configura]**.

>[!TIP]
>
>Le origini mostrano **[!UICONTROL Configurazione]** per nuove connessioni e **[!UICONTROL Aggiunta dati]** se esiste già un account.

![Catalogo delle origini con l&#39;origine Archiviazione BLOB di Azure selezionata.](../../../../images/tutorials/create/blob/catalog.png)

## Usa un account esistente

Per utilizzare un account esistente, selezionare **[!UICONTROL Account esistente]**, quindi selezionare l&#39;account [!DNL Azure Blob Storage] che si desidera utilizzare.

![Interfaccia di origine esistente per l&#39;archiviazione BLOB di Azure.](../../../../images/tutorials/create/blob/existing.png)

## Crea un nuovo account

Per creare un nuovo account, seleziona **[!UICONTROL Nuovo account]**, quindi specifica un nome e, facoltativamente, aggiungi una descrizione per l&#39;account. È possibile connettere l&#39;account [!DNL Azure Blob Storage] ad Experience Platform utilizzando i seguenti tipi di autenticazione:

* **Autenticazione chiave account**: utilizza la chiave di accesso dell&#39;account di archiviazione per autenticare e connettersi all&#39;account [!DNL Azure Blob Storage].
* **Firma di accesso condiviso (SAS)**: utilizza un URI SAS per fornire accesso delegato e limitato nel tempo alle risorse nell&#39;account [!DNL Azure Blob Storage].
* **Autenticazione basata sull&#39;entità servizio**: utilizza un&#39;entità servizio Azure Active Directory (AAD) (ID client e segreto) per l&#39;autenticazione sicura nell&#39;account di archiviazione BLOB di Azure.

>[!BEGINTABS]

>[!TAB Autenticazione chiave account]

Seleziona **[!UICONTROL Autenticazione chiave account]** e fornisci `connectionString`, `container` e `folderPath`. Quindi, selezionare **[!UICONTROL Connetti all&#39;origine]** e attendere alcuni istanti prima di stabilire la connessione.

![Opzione di autenticazione della chiave dell&#39;account nel nuovo passaggio di creazione dell&#39;account.](../../../../images/tutorials/create/blob/account-key.png)

>[!TAB Firma di accesso condiviso]

Seleziona **[!UICONTROL Firma di accesso condiviso]** e fornisci `sasUri`, `container` e `folderPath`. Quindi, selezionare **[!UICONTROL Connetti all&#39;origine]** e attendere alcuni istanti prima di stabilire la connessione.

![Opzione di autenticazione della firma di accesso condiviso nel passaggio di creazione del nuovo account.](../../../../images/tutorials/create/blob/sas.png)

>[!TAB Autenticazione basata su entità servizio]

Seleziona **[!UICONTROL Autenticazione basata su entità servizio]** e fornisci `serviceEndpoint`, `servicePrincipalId`, `servicePrincipalKey`, `accountKind`, `tenant`, `container` e `folderPath`. Quindi, selezionare **[!UICONTROL Connetti all&#39;origine]** e attendere alcuni istanti prima di stabilire la connessione.

![Opzione di autenticazione basata sull&#39;entità servizio nel passaggio di creazione del nuovo account.](../../../../images/tutorials/create/blob/service-principal.png)

>[!ENDTABS]

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account [!DNL Azure Blob Storage]. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per portare dati dall&#39;archiviazione cloud in Experience Platform](../../dataflow/batch/cloud-storage.md).
