---
title: Creare una connessione di origine BLOB di Azure nell’interfaccia utente
description: Scopri come creare un connettore di origine BLOB di Azure utilizzando l’interfaccia utente di Platform.
exl-id: 0e54569b-7305-4065-981e-951623717648
source-git-commit: 922e9a26f1791056b251ead2ce2702dfbf732193
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 1%

---

# Creare un [!DNL Azure Blob] connessione sorgente nell’interfaccia utente

Questo tutorial descrive i passaggi necessari per creare [!DNL Azure Blob] (in seguito denominati &quot;[!DNL Blob]&quot;) tramite l’interfaccia utente di Platform.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): framework standardizzato per organizzare i dati sull’esperienza del cliente in Experience Platform.
   * [Nozioni di base sulla composizione dello schema](../../../../../xdm/schema/composition.md): scopri gli elementi di base degli schemi XDM, compresi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’editor di schemi](../../../../../xdm/tutorials/create-schema-ui.md): scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di un [!DNL Blob] connessione, è possibile saltare il resto del documento e passare all&#39;esercitazione [configurazione di un flusso di dati](../../dataflow/batch/cloud-storage.md).

### Formati di file supportati

Experience Platform supporta i seguenti formati di file da acquisire da archivi esterni:

* Valori separati da delimitatore (DSV): è possibile utilizzare qualsiasi delimitatore a colonna singola, ad esempio tabulazione, virgola, barra verticale, punto e virgola o hash per raccogliere file flat in qualsiasi formato.
* JSON (JavaScript Object Notation): i file di dati formattati JSON devono essere conformi a XDM.
* Apache Parquet: i file di dati formattati con Parquet devono essere conformi a XDM.

### Raccogli le credenziali richieste

Per accedere al tuo [!DNL Blob] su Platform, è necessario fornire un valore valido per le seguenti credenziali:

| Credenziali | Descrizione |
| ---------- | ----------- |
| Stringa di connessione | Stringa contenente le informazioni di autorizzazione necessarie per l&#39;autenticazione [!DNL Blob] all&#39;Experience Platform. Il [!DNL Blob] modello di stringa di connessione: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`. Per ulteriori informazioni sulle stringhe di connessione, vedere [!DNL Blob] documento su [configurazione delle stringhe di connessione](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string). |
| URI SAS | URI della firma di accesso condiviso che è possibile utilizzare come tipo di autenticazione alternativo per connettere [!DNL Blob] account. Il [!DNL Blob] Criterio URI SAS: `https://{ACCOUNT_NAME}.blob.core.windows.net/?sv=<storage version>&st={START_TIME}&se={EXPIRE_TIME}&sr={RESOURCE}&sp={PERMISSIONS}>&sip=<{IP_RANGE}>&spr={PROTOCOL}&sig={SIGNATURE}>` Per ulteriori informazioni, consulta [!DNL Blob] documento su [URI della firma di accesso condiviso](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-blob-storage#shared-access-signature-authentication). |
| Contenitore | Nome del contenitore a cui si desidera designare l&#39;accesso. Quando crei un nuovo account con [!DNL Blob] sorgente, puoi fornire un nome contenitore per specificare l’accesso utente alla sottocartella desiderata. |
| Percorso cartella | Percorso della cartella a cui desideri fornire l’accesso. |

Dopo aver raccolto le credenziali richieste, puoi seguire la procedura riportata di seguito per collegare il tuo [!DNL Blob] da un account a Platform.

## Connetti [!DNL Blob] account

Nell’interfaccia utente di Platform, seleziona **[!UICONTROL Sorgenti]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Sorgenti] Workspace. Il [!UICONTROL Catalogo] Nella schermata vengono visualizzate diverse origini con cui è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la fonte specifica che si desidera utilizzare utilizzando la barra di ricerca.

Sotto [!UICONTROL Archiviazione cloud] categoria, seleziona **[!UICONTROL Archiviazione BLOB di Azure]**, quindi selezionare **[!UICONTROL Aggiungi dati]**.

![Il catalogo delle origini Experienci Platform con l’origine Archiviazione BLOB di Azure selezionata.](../../../../images/tutorials/create/blob/catalog.png)

Il **[!UICONTROL Connetti all’archiviazione BLOB di Azure]** viene visualizzata. In questa pagina è possibile utilizzare nuove credenziali o credenziali esistenti.

### Account esistente

Per utilizzare un account esistente, seleziona la [!DNL Blob] account con cui vuoi creare un nuovo flusso di dati, quindi seleziona **[!UICONTROL Successivo]** per procedere.

![esistente](../../../../images/tutorials/create/blob/existing.png)

### Nuovo account

Se stai creando un nuovo account, seleziona **[!UICONTROL Nuovo account]** e quindi fornisci un nome e una descrizione facoltativa per il nuovo [!DNL Blob] account.

![La nuova schermata dell’account per l’origine dell’archiviazione BLOB di Azure.](../../../../images/tutorials/create/blob/new.png)

Il [!DNL Blob] l&#39;origine supporta sia l&#39;autenticazione con chiave account che l&#39;autenticazione con firma di accesso condiviso (SAS). Un&#39;autenticazione basata su chiave account richiede una stringa di connessione per la verifica, mentre un&#39;autenticazione SAS utilizza un URI che consente l&#39;autorizzazione delegata sicura dell&#39;account.

Durante questo passaggio, puoi anche designare le sottocartelle a cui il tuo account avrà accesso definendo il nome del contenitore e il percorso della sottocartella.

>[!BEGINTABS]

>[!TAB Stringa di connessione]

Per eseguire l’autenticazione con una chiave account, seleziona **[!UICONTROL Autenticazione chiave account]** e fornisci la stringa di connessione. Durante questo passaggio, puoi anche designare il nome del contenitore e il percorso della sottocartella a cui desideri accedere. Al termine, seleziona **[!UICONTROL Connetti all&#39;origine]**.

![stringa di connessione](../../../../images/tutorials/create/blob/connectionstring.png)

>[!TAB URI SAS]

È possibile utilizzare SAS per creare credenziali di autenticazione con diversi gradi di accesso, in quanto un&#39;autenticazione basata su SAS consente di impostare autorizzazioni, date di inizio e di scadenza, nonché disposizioni a risorse specifiche.

Per eseguire l&#39;autenticazione con una firma di accesso condiviso, selezionare **[!UICONTROL Autenticazione della firma di accesso condiviso]** e quindi fornire l&#39;URI SAS. Durante questo passaggio, puoi anche designare il nome del contenitore e il percorso della sottocartella a cui desideri accedere. Al termine, seleziona **[!UICONTROL Connetti all&#39;origine]**.

![sas-uri](../../../../images/tutorials/create/blob/sas-uri.png)

>[!ENDTABS]

## Passaggi successivi

Seguendo questa esercitazione, hai stabilito una connessione con il tuo [!DNL Blob] account. Ora puoi continuare con l’esercitazione successiva e [configurare un flusso di dati per portare i dati dall’archiviazione cloud a Platform](../../dataflow/batch/cloud-storage.md).
