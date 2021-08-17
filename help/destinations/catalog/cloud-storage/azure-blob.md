---
keywords: BLOB di Azure;destinazione BLOB;s3;destinazione BLOB di azzurro
title: Connessione BLOB di Azure
description: Crea una connessione in uscita dal vivo all’archivio BLOB di Azure per esportare periodicamente file di dati CSV o delimitati da tabulazioni da Adobe Experience Platform.
exl-id: 8099849b-e3d2-48a5-902a-ca5a5ec88207
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 1%

---

# [!DNL Azure Blob] connection

## Panoramica {#overview}

[!DNL Azure Blob] (in seguito denominato  [!DNL Blob]) è la soluzione di archiviazione oggetti di Microsoft per il cloud. Questa esercitazione descrive i passaggi necessari per creare una destinazione [!DNL Blob] utilizzando l&#39;interfaccia utente [!DNL Platform] .

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../xdm/home.md): Il framework standardizzato in base al quale l’Experience Platform organizza i dati sulla customer experience.
   * [Nozioni di base sulla composizione](../../../xdm/schema/composition.md) dello schema: Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione](../../../xdm/tutorials/create-schema-ui.md) dell’Editor di schema: Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-time Customer Profile]](../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una destinazione [!DNL Blob] valida, puoi saltare il resto del documento e procedere all&#39;esercitazione sull&#39; [attivazione dei segmenti nella destinazione](../../ui/activate-batch-profile-destinations.md).

## Formati di file supportati {#file-formats}

[!DNL Experience Platform] supporta il seguente formato di file da esportare in  [!DNL Blob]:

* Valori separati da delimitatore (DSV): Il supporto per i file di dati formattati DSV è attualmente limitato ai valori separati da virgole. Il supporto per i file DSV generali verrà fornito in futuro.

## Collegati alla destinazione {#connect}

Per connetterti a questa destinazione, segui i passaggi descritti nel [tutorial sulla configurazione della destinazione](../../ui/connect-destination.md).

### Parametri di connessione {#parameters}

Durante la [configurazione](../../ui/connect-destination.md) di questa destinazione, è necessario fornire le seguenti informazioni:

* **[!UICONTROL Stringa]** di connessione: la stringa di connessione è necessaria per accedere ai dati nell’archivio Blob. Il pattern della stringa di connessione [!DNL Blob] inizia con: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`.
   * Per ulteriori informazioni sulla configurazione della stringa di connessione [!DNL Blob], vedere [Configurare una stringa di connessione per un account di archiviazione di Azure](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string#configure-a-connection-string-for-an-azure-storage-account) nella documentazione di Microsoft.

* Facoltativamente, puoi allegare la chiave pubblica in formato RSA per aggiungere la crittografia ai file esportati. La chiave pubblica deve essere scritta come stringa codificata [!DNL Base64].
* **[!UICONTROL Nome]**: immetti un nome che ti aiuterà a identificare questa destinazione.
* **[!UICONTROL Descrizione]**: immettere una descrizione della destinazione.
* **[!UICONTROL Percorso]** cartella: immetti il percorso della cartella di destinazione che ospiterà i file esportati.
* **[!UICONTROL Contenitore]**: immetti il nome del  [!DNL Azure Blob Storage] contenitore da utilizzare per la destinazione.

Facoltativamente, puoi allegare la chiave pubblica in formato RSA per aggiungere la crittografia ai file esportati. La chiave pubblica deve essere scritta come stringa codificata [!DNL Base64].

## Attiva i segmenti in questa destinazione {#activate}

Per istruzioni sull’attivazione dei segmenti di pubblico a questa destinazione, consulta [Attivare i dati di pubblico per le destinazioni di esportazione del profilo batch](../../ui/activate-batch-profile-destinations.md) .
