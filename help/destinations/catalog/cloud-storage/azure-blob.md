---
keywords: BLOB di Azure;destinazione BLOB;s3;destinazione BLOB di azzurro
title: Connessione BLOB di Azure
description: Crea una connessione in uscita dal vivo all’archivio BLOB di Azure per esportare periodicamente file di dati CSV da Adobe Experience Platform.
exl-id: 8099849b-e3d2-48a5-902a-ca5a5ec88207
source-git-commit: 691e3181e05a24b6bb0ebbe8e0f797a2b4c572d2
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 2%

---

# [!DNL Azure Blob] connection

## Panoramica {#overview}

[!DNL Azure Blob] (di seguito denominati [!DNL Blob]) è la soluzione di archiviazione oggetti di Microsoft per il cloud. Questa esercitazione fornisce i passaggi per la creazione di un [!DNL Blob] la destinazione che utilizza [!DNL Platform] interfaccia utente.

## Introduzione

Questa esercitazione richiede una buona comprensione dei seguenti componenti di Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../xdm/home.md): Il framework standardizzato in base al quale l’Experience Platform organizza i dati sulla customer experience.
   * [Nozioni di base sulla composizione dello schema](../../../xdm/schema/composition.md): Scopri i blocchi di base degli schemi XDM, inclusi i principi chiave e le best practice nella composizione dello schema.
   * [Esercitazione sull’Editor di schema](../../../xdm/tutorials/create-schema-ui.md): Scopri come creare schemi personalizzati utilizzando l’interfaccia utente dell’Editor di schema.
* [[!DNL Real-time Customer Profile]](../../../profile/home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.

Se disponi già di una [!DNL Blob] destinazione, puoi saltare il resto del documento e procedere all&#39;esercitazione su [attivazione dei segmenti sulla destinazione](../../ui/activate-batch-profile-destinations.md).

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, fare riferimento alla tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto nella schermata seleziona attributi profilo del [flusso di lavoro di attivazione della destinazione](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequenza delle esportazioni | **[!UICONTROL Batch]** | Le destinazioni batch esportano file su piattaforme downstream con incrementi di tre, sei, otto, dodici o ventiquattro ore. Ulteriori informazioni [destinazioni batch basate su file](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## Formati di file supportati {#file-formats}

[!DNL Experience Platform] supporta il seguente formato di file da esportare in [!DNL Blob]:

* Valori separati da virgole (CSV): Il supporto per i file di dati esportati è attualmente limitato ai valori separati da virgole.

## Collegati alla destinazione {#connect}

Per connettersi a questa destinazione, segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md).

### Parametri di connessione {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_blob_rsa"
>title="Chiave pubblica RSA"
>abstract="Facoltativamente, puoi allegare la chiave pubblica in formato RSA per aggiungere la crittografia ai file esportati. La chiave pubblica deve essere scritta come stringa codificata Base64."

Quando [configurazione](../../ui/connect-destination.md) questa destinazione, devi fornire le seguenti informazioni:

* **[!UICONTROL Stringa di connessione]**: la stringa di connessione è necessaria per accedere ai dati nell’archivio Blob. La [!DNL Blob] il pattern della stringa di connessione inizia con: `DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`.
   * Per ulteriori informazioni sulla configurazione della [!DNL Blob] stringa di connessione, vedere [Configurare una stringa di connessione per un account di archiviazione di Azure](https://docs.microsoft.com/en-us/azure/storage/common/storage-configure-connection-string#configure-a-connection-string-for-an-azure-storage-account) nella documentazione di Microsoft.

* Facoltativamente, puoi allegare la chiave pubblica in formato RSA per aggiungere la crittografia ai file esportati. La chiave pubblica deve essere scritta come [!DNL Base64] stringa codificata.
* **[!UICONTROL Nome]**: immetti un nome che ti aiuterà a identificare questa destinazione.
* **[!UICONTROL Descrizione]**: immettere una descrizione della destinazione.
* **[!UICONTROL Percorso cartella]**: immetti il percorso della cartella di destinazione che ospiterà i file esportati.
* **[!UICONTROL Contenitore]**: immetti il nome della [!DNL Azure Blob Storage] contenitore utilizzato da questa destinazione.

Facoltativamente, puoi allegare la chiave pubblica in formato RSA per aggiungere la crittografia ai file esportati. La chiave pubblica deve essere scritta come [!DNL Base64] stringa codificata.

## Attiva i segmenti in questa destinazione {#activate}

Vedi [Attivare i dati del pubblico nelle destinazioni di esportazione del profilo batch](../../ui/activate-batch-profile-destinations.md) per istruzioni su come attivare i segmenti di pubblico a questa destinazione.
