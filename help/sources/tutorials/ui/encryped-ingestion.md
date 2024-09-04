---
title: Acquisire dati crittografati nel Workspace dell’interfaccia utente Sources
description: Scopri come acquisire i dati crittografati nell’area di lavoro dell’interfaccia utente delle origini.
hide: true
hidefromtoc: true
exl-id: 34aaf9b6-5c39-404b-a70a-5553a4db9cdb
source-git-commit: 9f827c1ba97fba237c216fce9c2966bcc91fd05b
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 30%

---

# Acquisire dati crittografati nell’interfaccia utente delle origini

Leggi questa guida per scoprire come acquisire dati crittografati in Adobe Experience Platform utilizzando origini di archiviazione cloud per i dati batch.

## Prerequisiti

* Crittografare i dati

## Acquisire dati crittografati {#ingest-encrypted-data}

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_isFileEncrypted"
>title="Il file è crittografato?"
>abstract="Seleziona questo pulsante di attivazione/disattivazione se acquisisci un file già crittografato."

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_sampleFile"
>title="Selezionare file di esempio"
>abstract="Per creare una mappatura, è necessario acquisire un file di esempio durante l’acquisizione di dati crittografati."

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_encryptionKeyId"
>title="ID chiave di crittografia"
>abstract="Specificare l&#39;ID della chiave di crittografia corrispondente alla chiave di crittografia utilizzata per crittografare i dati di origine."

>[!CONTEXTUALHELP]
>id="platform_sources_encrypted_signVerificationKeyId"
>title="ID chiave di verifica firma"
>abstract="Fornisci l’ID della chiave di verifica della firma che corrisponde ai dati di origine crittografati e firmati."

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
