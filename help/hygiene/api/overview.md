---
title: Guida all’API per l’igiene dei dati
description: Scopri come correggere o eliminare programmaticamente i dati personali memorizzati dai tuoi clienti in Adobe Experience Platform.
exl-id: 78c8b15b-b433-4168-a1e8-c97b96e4bf85
source-git-commit: 7f1e4bdf54314cab1f69619bcbb34216da94b17e
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 1%

---

# Guida all’API per l’igiene dei dati

>[!IMPORTANT]
>
>Le funzionalità di igiene dei dati in Adobe Experience Platform sono attualmente disponibili solo per le organizzazioni che hanno acquistato Healthcare Shield.

L’API di igiene dei dati ti consente di correggere o eliminare programmaticamente i dati personali memorizzati dei tuoi clienti in Adobe Experience Platform, nonché di pianificare i protocolli TTL (time-to-live) per i set di dati. Questa guida descrive i passaggi preliminari all’utilizzo dell’API e fornisce collegamenti a documentazione più specifica per l’endpoint.

## Introduzione

Puoi accedere all’API di igiene dati attraverso il seguente percorso principale: `https://platform.adobe.io/data/core/hygiene/`

Le sezioni seguenti descrivono i concetti di base da conoscere prima di effettuare chiamate all’API.

### Raccogli i valori delle intestazioni richieste

Per effettuare chiamate all’API di igiene dati, devi prima raccogliere le credenziali di autenticazione. Segui [Guida all’autenticazione API](../../landing/api-authentication.md) per generare valori per ciascuna delle intestazioni richieste per l’API di igiene dati, come mostrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

* `Content-Type: application/json`

### Lettura di chiamate API di esempio

Questo documento fornisce un esempio di chiamata API per dimostrare come formattare le richieste. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione sulle [come leggere le chiamate API di esempio](../../landing/api-guide.md#sample-api) nella guida introduttiva per le API di Experience Platform.

<!-- ## Work orders

A work order is a representation of a data hygiene task that deletes consumer identities from a specific dataset or all datasets. See the [work order endpoint guide](./workorder.md) for details on working with work orders in the API. -->

## Tempo di vita (TTL) per i set di dati

Un TTL di set di dati è un’azione ritardata &quot;elimina un set di dati&quot;. Creando un TTL, si specifica un’ora futura in cui il set di dati deve essere eliminato. Consulta la sezione [guida all’endpoint TTL del set di dati](./ttl.md) per informazioni sulla pianificazione dei TTL dei set di dati nell’API.

## Passaggi successivi

Questa guida illustra come gestire le richieste di igiene dei dati utilizzando le chiamate API. Per informazioni su come eseguire queste azioni nell’interfaccia utente di Platform, consulta [guida all’interfaccia utente per l’igiene dei dati](../ui/overview.md).
