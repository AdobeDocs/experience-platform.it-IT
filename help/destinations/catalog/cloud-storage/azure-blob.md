---
keywords: BLOB di Azure;destinazione BLOB;s3;destinazione BLOB di azzurro
title: Connessione BLOB di Azure
description: Crea una connessione in uscita dal vivo all’archivio BLOB di Azure per esportare periodicamente file di dati CSV o delimitati da tabulazioni da Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 02754055e2be8a45a0699386cb559dad8f25717c
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 1%

---


# [!DNL Azure Blob] connection

## Panoramica {#overview}

[!DNL Azure Blob] (in seguito denominato &quot;[!DNL Blob]&quot;) è la soluzione di archiviazione oggetti di Microsoft per il cloud. Questa esercitazione descrive i passaggi necessari per creare una destinazione [!DNL Blob] utilizzando l&#39;interfaccia utente [!DNL Platform] .

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../xdm/home.md): Il framework standardizzato in base al quale l’Experience Platform organizza i dati sulla customer experience.
   - [Nozioni di base sulla composizione](../../../xdm/schema/composition.md) dello schema: Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   - [Esercitazione](../../../xdm/tutorials/create-schema-ui.md) dell’Editor di schema: Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
- [[!DNL Real-time Customer Profile]](../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una destinazione Blob valida, puoi saltare il resto del documento e procedere all&#39;esercitazione su [attivazione dei segmenti nella destinazione](../../ui/activate-destinations.md).

## Formati di file supportati {#file-formats}

[!DNL Experience Platform] supporta il seguente formato di file da esportare in  [!DNL Blob]:

- Valori separati da delimitatore (DSV): Il supporto per i file di dati formattati DSV è attualmente limitato ai valori separati da virgole. Il supporto per i file DSV generali verrà fornito in futuro. Per ulteriori informazioni sui file supportati, consulta la sezione archiviazione cloud nell’esercitazione sull’ [attivazione delle destinazioni](../../ui/activate-destinations.md#esp-and-cloud-storage).

## Connetti l&#39;account Blob {#connect-destination}

Accedi a [Adobe Experience Platform](https://platform.adobe.com) e seleziona **[!UICONTROL Destinations]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro **[!UICONTROL Destinations]**. Nella schermata **[!UICONTROL Catalog]** sono visualizzate diverse destinazioni con le quali è possibile creare un account.

Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare la destinazione specifica con cui si desidera lavorare utilizzando l’opzione di ricerca.

Sotto la categoria **[!UICONTROL Cloud Storage]**, selezionare **[!UICONTROL Azure Blob Storage]**, seguito da **[!UICONTROL Configure]**.

![Catalogo](../../assets/catalog/cloud-storage/blob/catalog.png)

>[!NOTE]
>
>Se esiste già una connessione con questa destinazione, è possibile visualizzare un pulsante **[!UICONTROL Activate]** sulla scheda di destinazione. Per ulteriori informazioni sulla differenza tra **[!UICONTROL Activate]** e **[!UICONTROL Configure]**, consulta la sezione [Catalogo](../../ui/destinations-workspace.md#catalog) della documentazione dell&#39;area di lavoro di destinazione.

Viene visualizzata la pagina **[!UICONTROL Connect to Azure Blob Storage]** . In questa pagina è possibile utilizzare le nuove credenziali o le credenziali esistenti.

## Nuovo account {#new-account}

Se utilizzi nuove credenziali, seleziona **[!UICONTROL New account]**. Nel modulo di input visualizzato, specificare la stringa di connessione. La stringa di connessione è necessaria per accedere ai dati nell’archivio Blob. Il pattern della stringa di connessione [!DNL Blob] inizia con: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`.

Per ulteriori informazioni sulla configurazione della stringa di connessione [!DNL Blob], vedere [Configurare una stringa di connessione per un account di archiviazione di Azure](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string#configure-a-connection-string-for-an-azure-storage-account) nella documentazione di Microsoft.

Facoltativamente, puoi allegare la chiave pubblica in formato RSA per aggiungere la crittografia ai file esportati. La chiave pubblica deve essere scritta come stringa codificata [!DNL Base64].

![Nuovo account](../../assets/catalog/cloud-storage/blob/new.png)

## Account esistente {#existing-account}

Per collegare un account esistente, selezionare l&#39;account [!DNL Blob] con cui si desidera connettersi, quindi selezionare **Avanti** per continuare.

![Account esistente](../../assets/catalog/cloud-storage/blob/existing.png)

## Autenticazione {#authentication}

Viene visualizzata la pagina **Autenticazione**. Nel modulo di input visualizzato, specificare un nome, una descrizione facoltativa, il percorso della cartella e il contenitore dei file.

In questo passaggio, puoi anche selezionare qualsiasi **[!UICONTROL Marketing actions]** da applicare a questa destinazione. Le azioni di marketing indicano l’intento per il quale i dati verranno esportati nella destinazione. Puoi scegliere tra azioni di marketing definite da Adobi o creare una tua azione di marketing. Per ulteriori informazioni sulle azioni di marketing, consulta la [Panoramica sui criteri di utilizzo dei dati](../../../data-governance/policies/overview.md).

Al termine, seleziona **[!UICONTROL Create destination]**.

![Autenticazione](../../assets/catalog/cloud-storage/blob/authentication.png)

## Passaggi successivi {#activate-segments}

Seguendo questa esercitazione, hai stabilito una connessione al tuo account [!DNL Blob] . Ora puoi continuare l&#39;esercitazione successiva e [attivare i segmenti nella tua destinazione](../../ui/activate-destinations.md).
