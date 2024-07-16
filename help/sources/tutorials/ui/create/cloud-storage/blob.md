---
title: Creare una connessione Source Azure Blob nell’interfaccia utente
description: Scopri come creare un connettore di origine BLOB di Azure utilizzando l’interfaccia utente di Platform.
exl-id: 0e54569b-7305-4065-981e-951623717648
source-git-commit: d22c71fb77655c401f4a336e339aaf8b3125d1b6
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 2%

---

# Crea una connessione di origine [!DNL Azure Blob] nell&#39;interfaccia utente

Questo tutorial descrive i passaggi necessari per creare una connessione di origine [!DNL Azure Blob] (di seguito &quot;[!DNL Blob]&quot;) tramite l&#39;interfaccia utente di Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato per l&#39;organizzazione dei dati sull&#39;esperienza del cliente in Experience Platform.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri i blocchi predefiniti di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull&#39;editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;editor di schemi.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una connessione [!DNL Blob] valida, puoi saltare il resto del documento e passare all&#39;esercitazione [configurazione di un flusso di dati](../../dataflow/batch/cloud-storage.md).

### Formati di file supportati

Experience Platform supporta i seguenti formati di file da acquisire da archivi esterni:

* Valori separati da delimitatore (DSV): è possibile utilizzare qualsiasi delimitatore a colonna singola, ad esempio tabulazione, virgola, barra verticale, punto e virgola o hash per raccogliere file flat in qualsiasi formato.
* JavaScript Object Notation (JSON): i file di dati formattati JSON devono essere conformi a XDM.
* Apache Parquet: i file di dati formattati con Parquet devono essere conformi a XDM.

### Raccogli le credenziali richieste

Per accedere all&#39;archivio [!DNL Blob] su Experience Platform, è necessario fornire valori validi per le credenziali seguenti:

>[!BEGINTABS]

>[!TAB Autenticazione stringa di connessione]

| Credenziali | Descrizione |
| --- | --- |
| Stringa di connessione | Stringa contenente le informazioni di autorizzazione necessarie per autenticare [!DNL Blob] in Experience Platform. Schema della stringa di connessione [!DNL Blob]: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Per ulteriori informazioni sulle stringhe di connessione, vedere il documento [!DNL Blob] in [configurazione delle stringhe di connessione](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |

>[!TAB Autenticazione URI SAS]

| Credenziali | Descrizione |
| --- | --- |
| URI SAS | URI della firma di accesso condiviso che è possibile utilizzare come tipo di autenticazione alternativo per connettere l&#39;account [!DNL Blob]. Il modello URI SAS [!DNL Blob] è: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Per ulteriori informazioni, vedere questo documento [!DNL Blob] in [URI di firma di accesso condiviso](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |
| Contenitore | Nome del contenitore a cui si desidera designare l&#39;accesso. Durante la creazione di un nuovo account con l&#39;origine [!DNL Blob], è possibile fornire un nome contenitore per specificare l&#39;accesso utente alla sottocartella desiderata. |
| Percorso della cartella | Percorso della cartella a cui desideri fornire l’accesso. |

>[!ENDTABS]

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi seguenti per collegare l&#39;archivio [!DNL Blob] a Experience Platform

## Connetti il tuo account [!DNL Blob]

Nell&#39;interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Origini]. Nella schermata [!UICONTROL Catalogo] sono visualizzate diverse origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la fonte specifica che si desidera utilizzare utilizzando la barra di ricerca.

Nella categoria [!UICONTROL Archiviazione cloud], seleziona **[!UICONTROL Archiviazione BLOB di Azure]**, quindi seleziona **[!UICONTROL Aggiungi dati]**.

![Catalogo delle origini di Experience Platform con l&#39;origine dell&#39;archiviazione BLOB di Azure selezionata.](../../../../images/tutorials/create/blob/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connetti ad Azure Blob Storage]**. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Account esistente

Per utilizzare un account esistente, seleziona l&#39;account [!DNL Blob] con cui vuoi creare un nuovo flusso di dati, quindi seleziona **[!UICONTROL Successivo]** per continuare.

![esistente](../../../../images/tutorials/create/blob/existing.png)

### Nuovo account

>[!TIP]
>
>Una volta creata, non è possibile modificare il tipo di autenticazione di una connessione di base [!DNL Blob]. Per modificare il tipo di autenticazione, è necessario creare una nuova connessione di base.

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]**, quindi fornisci un nome e una descrizione facoltativa per il nuovo account [!DNL Blob].

![Nuova schermata dell&#39;account per l&#39;origine dell&#39;archiviazione BLOB di Azure.](../../../../images/tutorials/create/blob/new.png)

L&#39;origine [!DNL Blob] supporta sia l&#39;autenticazione con chiave account che l&#39;autenticazione con firma di accesso condiviso (SAS). Un&#39;autenticazione basata su chiave account richiede una stringa di connessione per la verifica, mentre un&#39;autenticazione SAS utilizza un URI che consente l&#39;autorizzazione delegata sicura dell&#39;account.

Durante questo passaggio, puoi anche designare le sottocartelle a cui il tuo account avrà accesso definendo il nome del contenitore e il percorso della sottocartella.

>[!BEGINTABS]

>[!TAB Stringa di connessione]

Per eseguire l&#39;autenticazione con una chiave account, selezionare **[!UICONTROL Autenticazione chiave account]** e specificare la stringa di connessione. Durante questo passaggio, puoi anche designare il nome del contenitore e il percorso della sottocartella a cui desideri accedere. Al termine, selezionare **[!UICONTROL Connetti all&#39;origine]**.

![stringa di connessione](../../../../images/tutorials/create/blob/connectionstring.png)

>[!TAB URI SAS]

È possibile utilizzare SAS per creare credenziali di autenticazione con diversi gradi di accesso, in quanto un&#39;autenticazione basata su SAS consente di impostare autorizzazioni, date di inizio e di scadenza, nonché disposizioni a risorse specifiche.

Per eseguire l&#39;autenticazione con una firma di accesso condiviso, selezionare **[!UICONTROL Autenticazione della firma di accesso condiviso]**, quindi specificare l&#39;URI SAS. Durante questo passaggio, puoi anche designare il nome del contenitore e il percorso della sottocartella a cui desideri accedere. Al termine, selezionare **[!UICONTROL Connetti all&#39;origine]**.

![sas-uri](../../../../images/tutorials/create/blob/sas-uri.png)

>[!ENDTABS]

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account [!DNL Blob]. Ora puoi continuare con l&#39;esercitazione successiva e [configurare un flusso di dati per portare i dati dall&#39;archiviazione cloud in Platform](../../dataflow/batch/cloud-storage.md).
