---
title: Acquisire dati crittografati nel Workspace dell’interfaccia utente Sources
description: Scopri come acquisire i dati crittografati nell’area di lavoro dell’interfaccia utente delle origini.
badge: Beta
hide: true
hidefromtoc: true
exl-id: 34aaf9b6-5c39-404b-a70a-5553a4db9cdb
source-git-commit: b4545943abbb68d36a64935feb4466d075331504
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 7%

---

# Acquisire dati crittografati nell’interfaccia utente delle origini

>[!AVAILABILITY]
>
>Il supporto per l’acquisizione di dati crittografati nell’interfaccia utente di origine è in versione beta e potrebbe non essere disponibile per la tua organizzazione. La funzione e la documentazione sono soggette a modifiche.

Puoi acquisire cartelle e file di dati crittografati in Adobe Experience Platform utilizzando origini batch di archiviazione cloud. Con l’acquisizione di dati crittografati, puoi sfruttare meccanismi di crittografia asimmetrica per trasferire in modo sicuro i dati batch in Experience Platform. Attualmente, i meccanismi di crittografia asimmetrica supportati sono PGP e GPG.

Questa funzione è disponibile per le seguenti sorgenti:

* [Amazon S3]
* [BLOB di Azure]
* [Archiviazione Azure Data Lake Gen2]
* [Archiviazione file di Azure]
* [Area di destinazione dati]
* [FTP]
* [Google Cloud Storage]
* [HDFS]
* [Archiviazione oggetti Oracle]
* [SFTP]

Leggi questa guida per scoprire come acquisire dati crittografati con origini batch di archiviazione cloud utilizzando l’interfaccia utente.

## Introduzione

È utile avere una conoscenza delle seguenti funzioni e concetti di Experience Platform prima di lavorare con l’acquisizione di dati crittografati nell’interfaccia utente:

* [Origini](../../home.md): utilizza le origini in Experience Platform per acquisire dati da un&#39;applicazione Adobe o da un&#39;origine dati di terze parti.
* [Flussi dati](../../../dataflows/home.md): i flussi dati sono rappresentazioni di processi di dati che spostano i dati in Experience Platform. Puoi utilizzare l’area di lavoro origini per creare flussi di dati che acquisiscono dati da una determinata origine a Experience Platform.
* [Sandbox](../../../sandboxes/home.md): utilizza le sandbox in Experience Platform per creare partizioni virtuali tra le istanze Experience Platform e creare ambienti dedicati allo sviluppo o alla produzione.

### Profilo di alto livello

1. Crea una coppia di chiavi di crittografia utilizzando l’area di lavoro origini nell’interfaccia utente di Experience Platform. Facoltativamente, puoi anche creare una coppia di chiavi per la verifica dei segni per fornire un ulteriore livello di sicurezza ai dati crittografati.
2. Utilizza la chiave pubblica per crittografare i dati.
3. Inserisci i dati crittografati nel provider di archiviazione cloud. Durante questo passaggio, devi inoltre assicurarti di disporre di un file di esempio che possa essere utilizzato come riferimento per mappare i dati di origine su uno schema Experience Data Model (XDM).
4. Acquisisci i dati crittografati da Experience Platform creando una connessione di origine.
5. Durante la creazione della connessione di origine, fornisci l’ID della chiave che corrisponde alla chiave pubblica utilizzata per crittografare i dati. Se hai utilizzato anche il meccanismo di coppia di chiavi per la verifica dei segni, devi fornire anche l’ID della chiave per la verifica dei segni che corrisponde ai dati crittografati.
6. Procedi ai passaggi di creazione del flusso di dati.

## Creare una coppia di chiavi di crittografia {#create-an-encryption-key-pair}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_encryptionKeyId"
>title="ID chiave di crittografia"
>abstract="Specificare l&#39;ID della chiave di crittografia corrispondente alla chiave di crittografia utilizzata per crittografare i dati di origine."

* Nell&#39;interfaccia utente di Platform, passa all&#39;area di lavoro origini e seleziona [!UICONTROL Coppie di chiavi] dall&#39;intestazione superiore.
* Viene visualizzata una pagina in cui sono elencate le coppie di chiavi di crittografia esistenti nell&#39;organizzazione. Questa pagina fornisce informazioni su titolo, ID, tipo, algoritmo di crittografia, scadenza e stato di una determinata chiave. Per creare una nuova coppia di chiavi, selezionare **[!UICONTROL Crea chiave]**.
* Scegliere quindi il tipo di chiave che si desidera impostare. Per creare una chiave di crittografia, selezionare **[!UICONTROL Chiave di crittografia]**, quindi specificare un titolo e una passphrase per la chiave di crittografia. La passphrase rappresenta un ulteriore livello di protezione per le chiavi di crittografia. Al momento della creazione, Experience Platform memorizza la passphrase in un archivio protetto diverso dalla chiave pubblica. Specificare una stringa non vuota come passphrase.

### Creare una chiave di verifica della firma {#create-a-sign-verification-key}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_signVerificationKeyId"
>title="ID chiave di verifica firma"
>abstract="Fornisci l’ID della chiave di verifica della firma che corrisponde ai dati di origine crittografati e firmati."

## Acquisire dati crittografati {#ingest-encrypted-data}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_isFileEncrypted"
>title="Il file è crittografato?"
>abstract="Seleziona questo pulsante di attivazione/disattivazione se acquisisci un file già crittografato."

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_sampleFile"
>title="Selezionare file di esempio"
>abstract="Per creare una mappatura, è necessario acquisire un file di esempio durante l’acquisizione di dati crittografati."


<!-- 
## Outline

Sections:

* Create public key
* Create customer key
* Create sources flow to ingest encrypted data
  * File ingestion
  * Folder ingestion
* Updated encrypted flow

* Select [!UICONTROL Key Pairs] from the header in the sources UI workspace.
  * You are taken to the [!UICONTROL Key Pairs] page:
    * Select **[!UICONTROL Encryption key]** for list of key pairs that you have created and managed.
    * Select **[!UICONTROL Customer key]** for a list of key pairs that your customers have created and managed.
* Key Pair functions:
  * Select **[!UICONTROL Key details]** to view key details.
  * Select **[!UICONTROL Delete]** to delete.
* Select [!UICONTROL Create key] to create either an encryption key or a customer key

## Questions and clarifications

* Public key vs. customer key
* Verify E2E:
  * Create keys (encryption key or customer key)
  * Use these keys to encrypt your data
  * Place your encrypted data in your cloud storage (Amazon S3 or Google Cloud Storage)
  * Ingest that encrypted data to Experience Platform by creating a source connection
    * Select the encrypted source data
    * Enable "Is the file encrypted"
    * Select/upload sample file for mapping
    * Use the encryption key name that corresponds with the key used to encrypt the source data
      * If the data was encrypted using customer key, provide the sign verification key.
  * Proceed with source connection creation flow -->
