---
keywords: ' Experience Platform;home;argomenti popolari;Azure Blob;azure blob;Azure blob Connector'
solution: Experience Platform
title: Creare un connettore di origine Azure Blob nell'interfaccia utente
topic: overview
type: Tutorial
description: Questa esercitazione fornisce passaggi per la creazione di un BLOB di Azure (in seguito denominato "Blob") tramite l'interfaccia utente della piattaforma.
translation-type: tm+mt
source-git-commit: e22e57e20b985b50e1d29e944fb8f04addc91703
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 1%

---


# Creare un connettore sorgente [!DNL Azure Blob] nell&#39;interfaccia utente

Questa esercitazione fornisce i passaggi necessari per creare un [!DNL Azure Blob] (in seguito denominato &quot;[!DNL Blob]&quot;) utilizzando l&#39;interfaccia utente della piattaforma.

## Introduzione

Questa esercitazione richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il framework standard con cui  Experience Platform organizza i dati sull&#39;esperienza dei clienti.
   - [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md) dello schema: Scoprite i componenti di base degli schemi XDM, inclusi i principi chiave e le procedure ottimali nella composizione dello schema.
   - [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md) sull&#39;Editor di schema: Scoprite come creare schemi personalizzati utilizzando l&#39;interfaccia utente dell&#39;Editor di schema.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se si dispone già di una connessione [!DNL Blob] valida, è possibile ignorare il resto del documento e procedere all&#39;esercitazione su [configurazione di un flusso di dati](../../dataflow/batch/cloud-storage.md).

### Formati di file supportati

[!DNL Experience Platform] supporta i seguenti formati di file da acquisire da archivi esterni:

- Valori separati da delimitatore (DSV): Il supporto per i file di dati in formato DSV è attualmente limitato ai valori separati da virgole. Il valore delle intestazioni dei campi all&#39;interno dei file formattati DSV deve essere costituito solo da caratteri alfanumerici e caratteri di sottolineatura. In futuro verrà fornito il supporto per i file DSV generali.
- JavaScript Object Notation (JSON): I file di dati formattati JSON devono essere conformi a XDM.
- Parquet Apache: I file di dati in formato parquet devono essere conformi a XDM.

### Raccogli credenziali richieste

Per accedere allo storage [!DNL Blob] sulla piattaforma, è necessario fornire un valore valido per le seguenti credenziali:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `connectionString` | Una stringa che contiene le informazioni di autorizzazione necessarie per autenticare [!DNL Blob]  Experience Platform. Il pattern della stringa di connessione [!DNL Blob] è: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Per ulteriori informazioni sulle stringhe di connessione, consultare questo documento [!DNL Blob] su [configurazione delle stringhe di connessione](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |
| `sasUri` | URI firma di accesso condiviso che è possibile utilizzare come tipo di autenticazione alternativo per collegare l&#39;account [!DNL Blob]. Il pattern URI SAS [!DNL Blob] è: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Per ulteriori informazioni, consultare questo documento [!DNL Blob] sugli URI delle firme di accesso condiviso [in ](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |

## Collegare l&#39;account [!DNL Blob]

Dopo aver raccolto le credenziali necessarie, puoi seguire i passaggi descritti di seguito per collegare l&#39;account [!DNL Blob] alla piattaforma.

Nell&#39; [interfaccia utente della piattaforma](https://platform.adobe.com), selezionare **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Sources]. Nella schermata [!UICONTROL Catalog] sono visualizzate diverse sorgenti con le quali è possibile creare un account.

Potete selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, potete trovare l’origine specifica con cui desiderate lavorare utilizzando la barra di ricerca.

Sotto la categoria [!UICONTROL Cloud storage], selezionare **[!UICONTROL Azure Blob Storage]**, quindi selezionare **[!UICONTROL Add data]**.

![catalogo](../../../../images/tutorials/create/blob/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connect to Azure Blob Storage]**. In questa pagina è possibile utilizzare credenziali nuove o già esistenti.

### Account esistente

Per utilizzare un account esistente, selezionare l&#39;account [!DNL Blob] con cui si desidera creare un nuovo flusso di dati, quindi selezionare **[!UICONTROL Next]** per continuare.

![esistenti](../../../../images/tutorials/create/blob/existing.png)

### Nuovo account

Se state creando un nuovo account, selezionate **[!UICONTROL New account]**, quindi fornite un nome e una descrizione dell&#39;opzione per il nuovo account [!DNL Blob].

**Eseguire l&#39;autenticazione utilizzando una stringa di connessione**

Il connettore [!DNL Blob] fornisce diversi tipi di autenticazione per l&#39;accesso. In [!UICONTROL Account authentication] selezionare **[!UICONTROL ConnectionString]** per utilizzare le credenziali basate su stringhe di connessione.

![stringa di connessione](../../../../images/tutorials/create/blob/connectionstring.png)

**Autenticazione tramite un URI firma di accesso condiviso**

L&#39;URI di firma di accesso condiviso (SAS) consente un&#39;autorizzazione delegata protetta per l&#39;account [!DNL Blob]. È possibile utilizzare SAS per creare credenziali di autenticazione con diversi gradi di accesso, in quanto un&#39;autenticazione basata su SAS consente di impostare autorizzazioni, date di inizio e scadenza, nonché disposizioni per risorse specifiche.

Selezionare **[!UICONTROL SasURIAuthentication]**, quindi specificare l&#39;URI SAS [!DNL Blob]. Selezionare **[!UICONTROL Connect to source]** per continuare.

![sas-uri](../../../../images/tutorials/create/blob/sas-uri.png)

## Passaggi successivi

Seguendo questa esercitazione, è stata stabilita una connessione all&#39;account [!DNL Blob]. È ora possibile continuare l&#39;esercitazione successiva e [configurare un flusso di dati per portare i dati dall&#39;archiviazione cloud nella piattaforma](../../dataflow/batch/cloud-storage.md).
