---
title: Creare una connessione Azure Blob Source nell’interfaccia utente
description: Scopri come creare un connettore sorgente BLOB di Azure utilizzando l’interfaccia utente di Platform.
exl-id: 0e54569b-7305-4065-981e-951623717648
source-git-commit: 922e9a26f1791056b251ead2ce2702dfbf732193
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 1%

---

# Crea un [!DNL Azure Blob] connessione sorgente nell’interfaccia utente

Questa esercitazione descrive i passaggi necessari per creare un [!DNL Azure Blob] (in appresso denominato &quot;[!DNL Blob]&quot;) la connessione sorgente tramite l’interfaccia utente di Platform.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): Il framework standardizzato per l’organizzazione dei dati sulla customer experience in Experience Platform.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’Editor di schema](../../../../../xdm/tutorials/create-schema-ui.md): Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una [!DNL Blob] è possibile ignorare il resto del documento e passare all&#39;esercitazione su [configurazione di un flusso di dati](../../dataflow/batch/cloud-storage.md).

### Formati di file supportati

Experience Platform supporta i seguenti formati di file da acquisire da archivi esterni:

* Valori separati da delimitatore (DSV): È possibile utilizzare qualsiasi carattere di delimitazione a una singola colonna, ad esempio tabulazione, virgola, barra verticale, punto e virgola o hash, per raccogliere file flat in qualsiasi formato.
* Notazione oggetto JavaScript (JSON): I file di dati formattati JSON devono essere conformi a XDM.
* Parquet Apache: I file di dati formattati per il parquet devono essere conformi a XDM.

### Raccogli credenziali richieste

Per accedere al tuo [!DNL Blob] su Platform, è necessario fornire un valore valido per le seguenti credenziali:

| Credenziali | Descrizione |
| ---------- | ----------- |
| Stringa di connessione | Una stringa contenente le informazioni di autorizzazione necessarie per l&#39;autenticazione [!DNL Blob] all&#39;Experience Platform. La [!DNL Blob] pattern di stringa di connessione: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Per ulteriori informazioni sulle stringhe di connessione, consulta [!DNL Blob] documento [configurazione di stringhe di connessione](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |
| URI SAS | URI della firma di accesso condiviso che è possibile utilizzare come tipo di autenticazione alternativo per collegare il [!DNL Blob] conto. La [!DNL Blob] Pattern URI SAS: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Per ulteriori informazioni, consulta [!DNL Blob] documento [URI della firma di accesso condiviso](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |
| Contenitore | Nome del contenitore a cui si desidera designare l’accesso. Durante la creazione di un nuovo account con [!DNL Blob] origine, è possibile specificare un nome contenitore per specificare l’accesso dell’utente alla sottocartella scelta. |
| Percorso cartella | Percorso della cartella a cui si desidera fornire l&#39;accesso. |

Una volta raccolte le credenziali richieste, puoi seguire i passaggi seguenti per collegare il tuo [!DNL Blob] a Platform.

## Collega il tuo [!DNL Blob] account

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Origini] workspace. La [!UICONTROL Catalogo] in viene visualizzata una varietà di sorgenti con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la sorgente specifica con cui si desidera lavorare utilizzando la barra di ricerca.

Sotto la [!UICONTROL archiviazione cloud] categoria, seleziona **[!UICONTROL Archiviazione BLOB di Azure]**, quindi seleziona **[!UICONTROL Aggiungi dati]**.

![Catalogo delle sorgenti Experience Platform con l’origine archiviazione BLOB di Azure selezionata.](../../../../images/tutorials/create/blob/catalog.png)

La **[!UICONTROL Connetti all’archiviazione BLOB di Azure]** viene visualizzata la pagina . In questa pagina è possibile utilizzare le nuove credenziali o le credenziali esistenti.

### Account esistente

Per utilizzare un account esistente, seleziona la [!DNL Blob] account con cui si desidera creare un nuovo flusso di dati, quindi selezionare **[!UICONTROL Successivo]** per procedere.

![esistente](../../../../images/tutorials/create/blob/existing.png)

### Nuovo account

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]**, quindi fornisci un nome e una descrizione facoltativa per il nuovo [!DNL Blob] conto.

![La nuova schermata dell’account per l’origine di archiviazione BLOB di Azure.](../../../../images/tutorials/create/blob/new.png)

La [!DNL Blob] source supporta sia l’autenticazione con chiave di account che l’autenticazione con firma di accesso condiviso (SAS). Un&#39;autenticazione basata su chiave dell&#39;account richiede una stringa di connessione per la verifica, mentre un&#39;autenticazione SAS utilizza un URI che consente un&#39;autorizzazione delegata sicura del tuo account.

Durante questo passaggio, puoi inoltre designare le sottocartelle a cui l’account avrà accesso definendo il nome del contenitore e il percorso della sottocartella.

>[!BEGINTABS]

>[!TAB Stringa di connessione]

Per eseguire l&#39;autenticazione con una chiave di account, seleziona **[!UICONTROL Autenticazione a chiave dell&#39;account]** e fornire la stringa di connessione. Durante questo passaggio, puoi anche specificare il nome e il percorso del contenitore per la sottocartella a cui desideri accedere. Al termine, seleziona **[!UICONTROL Connetti alla sorgente]**.

![stringa di connessione](../../../../images/tutorials/create/blob/connectionstring.png)

>[!TAB URI SAS]

È possibile utilizzare SAS per creare credenziali di autenticazione con diversi gradi di accesso, in quanto un&#39;autenticazione basata su SAS consente di impostare autorizzazioni, date di inizio e scadenza, nonché disposizioni per risorse specifiche.

Per eseguire l&#39;autenticazione con una firma di accesso condivisa, selezionare **[!UICONTROL Autenticazione firma di accesso condiviso]** e quindi fornire l&#39;URI SAS. Durante questo passaggio, puoi anche specificare il nome e il percorso del contenitore per la sottocartella a cui desideri accedere. Al termine, seleziona **[!UICONTROL Connetti alla sorgente]**.

![sas-uri](../../../../images/tutorials/create/blob/sas-uri.png)

>[!ENDTABS]

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione al tuo [!DNL Blob] conto. Ora puoi passare all’esercitazione successiva e [configurare un flusso di dati per l’importazione di dati dall’archiviazione cloud in Platform](../../dataflow/batch/cloud-storage.md).
