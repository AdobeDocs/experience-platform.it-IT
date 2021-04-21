---
keywords: Experience Platform;home;argomenti popolari;BLOB di Azure;BLOB di azzurro;Connettore BLOB di Azure
solution: Experience Platform
title: Creare una connessione Azure Blob Source nell’interfaccia utente
topic-legacy: overview
type: Tutorial
description: Scopri come creare un connettore sorgente BLOB di Azure utilizzando l’interfaccia utente di Platform.
exl-id: 0e54569b-7305-4065-981e-951623717648
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 1%

---

# Creare una connessione sorgente [!DNL Azure Blob] nell&#39;interfaccia utente

Questa esercitazione fornisce passaggi per creare un [!DNL Azure Blob] (in seguito denominato &quot;[!DNL Blob]&quot;) utilizzando l’interfaccia utente di Platform.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il framework standardizzato in base al quale l’Experience Platform organizza i dati sulla customer experience.
   - [Nozioni di base sulla composizione](../../../../../xdm/schema/composition.md) dello schema: Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   - [Esercitazione](../../../../../xdm/tutorials/create-schema-ui.md) dell’Editor di schema: Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una connessione [!DNL Blob] valida, puoi saltare il resto del documento e continuare l&#39;esercitazione su [configurazione di un flusso di dati](../../dataflow/batch/cloud-storage.md).

### Formati di file supportati

[!DNL Experience Platform] supporta i seguenti formati di file da acquisire da archivi esterni:

- Valori separati da delimitatore (DSV): Il supporto per i file di dati formattati DSV è attualmente limitato ai valori separati da virgole. Il valore delle intestazioni di campo all&#39;interno dei file formattati DSV deve essere costituito solo da caratteri alfanumerici e caratteri di sottolineatura. Il supporto per i file DSV generali verrà fornito in futuro.
- Notazione oggetto JavaScript (JSON): I file di dati formattati JSON devono essere conformi a XDM.
- Parquet Apache: I file di dati formattati per il parquet devono essere conformi a XDM.

### Raccogli credenziali richieste

Per accedere allo storage [!DNL Blob] su Platform, è necessario fornire un valore valido per le seguenti credenziali:

| Credenziali | Descrizione |
| ---------- | ----------- |
| `connectionString` | Una stringa che contiene le informazioni di autorizzazione necessarie per autenticare [!DNL Blob] in Experience Platform. Il pattern della stringa di connessione [!DNL Blob] è: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Per ulteriori informazioni sulle stringhe di connessione, vedere questo documento [!DNL Blob] in [configurazione delle stringhe di connessione](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |
| `sasUri` | URI della firma di accesso condiviso che è possibile utilizzare come tipo di autenticazione alternativo per collegare l&#39;account [!DNL Blob]. Il modello URI SAS [!DNL Blob] è: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Per ulteriori informazioni, vedere questo documento [!DNL Blob] in [URI della firma di accesso condiviso](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |

## Connetti il tuo account [!DNL Blob]

Dopo aver raccolto le credenziali richieste, puoi seguire i passaggi seguenti per collegare il tuo account [!DNL Blob] a Platform.

Nella [Interfaccia utente della piattaforma](https://platform.adobe.com), seleziona **[!UICONTROL Sources]** dalla barra di navigazione a sinistra per accedere all’area di lavoro [!UICONTROL Sources]. Nella schermata [!UICONTROL Catalog] sono visualizzate diverse origini per le quali è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando la barra di ricerca.

Sotto la categoria [!UICONTROL Cloud storage], selezionare **[!UICONTROL Azure Blob Storage]**, quindi selezionare **[!UICONTROL Add data]**.

![catalogo](../../../../images/tutorials/create/blob/catalog.png)

Viene visualizzata la pagina **[!UICONTROL Connect to Azure Blob Storage]** . In questa pagina è possibile utilizzare le nuove credenziali o le credenziali esistenti.

### Account esistente

Per utilizzare un account esistente, selezionare l&#39;account [!DNL Blob] con cui si desidera creare un nuovo flusso di dati, quindi selezionare **[!UICONTROL Next]** per continuare.

![esistente](../../../../images/tutorials/create/blob/existing.png)

### Nuovo account

Se stai creando un nuovo account, seleziona **[!UICONTROL New account]**, quindi fornisci un nome e una descrizione delle opzioni per il tuo nuovo account [!DNL Blob].

**Autenticazione tramite una stringa di connessione**

Il connettore [!DNL Blob] offre diversi tipi di autenticazione per l’accesso. In [!UICONTROL Account authentication] selezionare **[!UICONTROL ConnectionString]** per utilizzare le credenziali basate su stringhe di connessione.

![stringa di connessione](../../../../images/tutorials/create/blob/connectionstring.png)

**Autenticazione tramite un URI di firma di accesso condiviso**

Un URI di firma di accesso condiviso (SAS) consente un&#39;autorizzazione delegata sicura al tuo account [!DNL Blob]. È possibile utilizzare SAS per creare credenziali di autenticazione con diversi gradi di accesso, in quanto un&#39;autenticazione basata su SAS consente di impostare autorizzazioni, date di inizio e scadenza, nonché disposizioni per risorse specifiche.

Selezionare **[!UICONTROL SasURIAuthentication]**, quindi fornire l&#39;URI SAS [!DNL Blob]. Selezionare **[!UICONTROL Connect to source]** per continuare.

![sas-uri](../../../../images/tutorials/create/blob/sas-uri.png)

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo account [!DNL Blob] . Ora puoi continuare l’esercitazione successiva e [configurare un flusso di dati per inserire dati dall’archiviazione cloud in Platform](../../dataflow/batch/cloud-storage.md).
