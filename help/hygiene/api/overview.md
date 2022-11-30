---
title: Guida all’API per l’igiene dei dati
description: Scopri come correggere o eliminare programmaticamente i dati personali memorizzati dai tuoi clienti in Adobe Experience Platform.
exl-id: 78c8b15b-b433-4168-a1e8-c97b96e4bf85
source-git-commit: da8b5d9fffdf8a176a4d70be5df5b3021cf0df7b
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---

# Guida all’API per l’igiene dei dati

>[!IMPORTANT]
>
>Le funzionalità di igiene dei dati in Adobe Experience Platform sono attualmente disponibili solo per le organizzazioni che hanno acquistato **Scudo sanitario Adobe** o **Adobe Privacy e sicurezza scudo**.

L’API di igiene dei dati ti consente di correggere o eliminare programmaticamente i dati personali memorizzati dei tuoi clienti in Adobe Experience Platform, nonché di pianificare le date di scadenza per i set di dati. Questa guida descrive i passaggi preliminari all’utilizzo dell’API e fornisce collegamenti a documentazione più specifica per l’endpoint.

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

## Scadenza set di dati

La scadenza di un set di dati è un’azione ritardata &quot;elimina un set di dati&quot;. Creando una scadenza di un set di dati, stai specificando un&#39;ora futura in cui quel set di dati deve essere eliminato. Consulta la sezione [guida all’endpoint di scadenza dei set di dati](./dataset-expiration.md) per informazioni sulla pianificazione delle scadenze dei set di dati nell’API.

## Elimina record

>[!IMPORTANT]
>
>Le richieste di eliminazione dei record sono disponibili solo per le organizzazioni che hanno acquistato **Scudo sanitario Adobe**.
>
>
>Le eliminazioni dei record sono intese per la pulizia, la rimozione di dati anonimi o la minimizzazione dei dati. Sono **not** da utilizzare per le richieste di diritti delle persone interessate (conformità) in relazione alle normative sulla privacy come il Regolamento generale sulla protezione dei dati (RGPD). Per tutti i casi di utilizzo della conformità, utilizza [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) invece.

L’API di igiene dati ti consente di eliminare tutti i record associati a un’identità in uno o tutti i set di dati. Tutte le attività di igiene dei dati che eliminano le identità sono rappresentate da un costrutto chiamato ordine di lavoro. Consulta la sezione [guida all’endpoint dell’ordine di lavoro](./workorder.md) per informazioni sull’utilizzo delle eliminazioni dei record nell’API.

## Quota

La tua organizzazione è limitata a una quota di lavoro mensile predeterminata per ogni tipo di operazione di igiene dei dati, che può variare a seconda della licenza. Consulta la sezione [guida all’endpoint quota](./quota.md) per informazioni dettagliate sulla visualizzazione dello stato attuale delle quote dei processi di igiene dei dati.

## Passaggi successivi

Questa guida illustra come gestire le richieste di igiene dei dati utilizzando le chiamate API. Per informazioni su come eseguire queste azioni nell’interfaccia utente di Platform, consulta [guida all’interfaccia utente per l’igiene dei dati](../ui/overview.md).
