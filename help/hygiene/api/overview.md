---
title: Guida dell’API di igiene dei dati
description: Scopri come correggere o eliminare in modo programmatico i dati personali memorizzati dai clienti in Adobe Experience Platform.
role: Developer
exl-id: 78c8b15b-b433-4168-a1e8-c97b96e4bf85
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 6%

---

# Guida dell’API di igiene dei dati

L’API di igiene dei dati consente di correggere o eliminare in modo programmatico i dati personali memorizzati dai clienti in Adobe Experience Platform, nonché di pianificare le date di scadenza dei set di dati. Questa guida descrive i passaggi preliminari per l’utilizzo dell’API e fornisce collegamenti a documentazione più specifica per l’endpoint.

## Introduzione

Puoi accedere all’API di igiene dei dati attraverso il seguente percorso principale: `https://platform.adobe.io/data/core/hygiene/`

Le sezioni seguenti descrivono i concetti di base che devi conoscere prima di tentare di effettuare chiamate all’API.

### Raccogliere i valori per le intestazioni richieste

Per effettuare chiamate all’API di igiene dei dati, devi prima raccogliere le credenziali di autenticazione. Segui le [Guida all’autenticazione API](../../landing/api-authentication.md) per generare valori per ciascuna delle intestazioni richieste per l’API di igiene dei dati, come illustrato di seguito:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Tutte le richieste che contengono un payload (POST, PUT, PATCH) richiedono un’intestazione aggiuntiva:

* `Content-Type: application/json`

### Lettura delle chiamate API di esempio

Questo documento fornisce un esempio di chiamata API per dimostrare come formattare le richieste. Per informazioni sulle convenzioni utilizzate nella documentazione per le chiamate API di esempio, consulta la sezione su [come leggere esempi di chiamate API](../../landing/api-guide.md#sample-api) nella guida introduttiva di Experienci Platform API.

## Scadenze dei set di dati

La scadenza di un set di dati è un’azione &quot;elimina un set di dati&quot; posticipata nel tempo. Creando una scadenza del set di dati, si specifica un momento futuro in cui tale set di dati deve essere eliminato. Consulta la [guida dell’endpoint &quot;dataset expiration&quot;](./dataset-expiration.md) per informazioni dettagliate sulla pianificazione delle scadenze dei set di dati nell’API.

## Eliminazioni record

>[!IMPORTANT]
>
>Le richieste di cancellazione dei record sono disponibili solo per le organizzazioni che hanno acquistato **Schermo sanitario Adobe**.
>
>
>Le eliminazioni di record devono essere utilizzate per la pulizia dei dati, la rimozione di dati anonimi o la minimizzazione dei dati. Sono **non** da utilizzare per le richieste di diritti degli interessati (conformità) relative a normative sulla privacy come il Regolamento generale sulla protezione dei dati (RGPD). Per tutti i casi di utilizzo di conformità, utilizza [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) invece.

L’API di igiene dei dati consente di eliminare tutti i record associati a un’identità in uno o tutti i set di dati. Tutte le attività del ciclo di vita dei dati che eliminano le identità sono rappresentate da un costrutto chiamato ordine di lavoro. Consulta la [guida dell’endpoint dell’ordine di lavoro](./workorder.md) per informazioni dettagliate sull’utilizzo delle eliminazioni di record nell’API.

## Quota

L&#39;organizzazione è limitata a una quota mensile predeterminata di processi per ogni tipo di operazione del ciclo di vita dei dati, che può variare a seconda della licenza. Consulta la [guida dell’endpoint &quot;quota&quot;](./quota.md) per informazioni dettagliate sulla visualizzazione dello stato attuale delle quote dei processi del ciclo di vita dei dati.

## Passaggi successivi

Questa guida illustra come gestire le richieste del ciclo di vita dei dati utilizzando le chiamate API. Per informazioni su come eseguire queste azioni nell’interfaccia utente di Platform, consulta [guida dell’interfaccia utente data lifecycle](../ui/overview.md).
