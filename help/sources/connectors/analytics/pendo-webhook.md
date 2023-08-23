---
title: Panoramica sulla sorgente Pendo
description: Scopri come collegare Pendo a Adobe Experience Platform utilizzando le API o l’interfaccia utente sfruttando i webhook
last-substantial-update: 2023-08-23T00:00:00Z
exl-id: 376f18ef-1eea-4c42-8041-6fadb5906e9b
source-git-commit: ce1e6c08d1e53346c11f9746cea524689f402031
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# [!DNL Pendo]

Adobe Experience Platform consente di acquisire i dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform. È possibile acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, database e molte altre.

Experienci Platform fornisce supporto per l’acquisizione di dati da applicazioni di analisi di terze parti. Il supporto per i provider di analisi include [!DNL Pendo].

[[!DNL Pendo]](https://pendo.io/) è un’app di analisi dei prodotti creata per aiutare le aziende di software a sviluppare prodotti che risuonano con i clienti. L’app consente ai produttori di software di incorporare i loro prodotti con un’ampia gamma di strumenti che possono portare a una migliore esperienza del prodotto per gli utenti e a nuove informazioni per il team di prodotto.

Il [!DNL Pendo] origine consente di acquisire gli schemi di eventi webhook supportati e i relativi dati di eventi associati da [!DNL Pendo.io] utilizzando [[!DNL Pendo] Webhook](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks). Il [!DNL Pendo] sorgente funziona con [!DNL Pendo] Webhook URL.

I webhook supportati sono:

* [Guida](https://support.pendo.io/hc/en-us/articles/8146679315867-Creating-a-Guide) Visualizzato
* [Sondaggio](https://support.pendo.io/hc/en-us/articles/360031867152-Polls-Classic-) Visualizzato/Inviato
* [Punteggio promotore netto](https://support.pendo.io/hc/en-us/articles/360033527151-Set-up-an-NPS-Survey) Visualizzato/Inviato

## Prerequisiti {#prerequisites}

Prima di creare un [!DNL Pendo] connessione di origine, è necessario verificare di disporre dei seguenti elementi:

A [!DNL Pendo] account. Se non ne hai già una, vedi [[!DNL Pendo] registrare](https://app.pendo.io/register) per registrarti e creare il tuo account.

### Configurazione [!DNL Pendo] Webhook {#set-up-webhook}

Dopo aver creato correttamente il flusso di dati, devi impostare un webhook per informare Platform su [!DNL Pendo] eventi. [!DNL Pendo] I webhook possono inviare notifiche in tempo reale ad altri servizi quando si verificano determinati eventi e inviare tali informazioni al tuo [!DNL Pendo] sorgente. Per ulteriori informazioni, consulta le esercitazioni su [recupero dell’URL dell’endpoint di streaming](../../tutorials/ui/create/analytics/pendo-webhook.md#get-streaming-endpoint) e [impostazione di un [!DNL Pendo] Webhook](../../tutorials/ui/create/analytics/pendo-webhook.md#set-up-webhook).

## Connessione [!DNL Pendo] alla piattaforma {#connect-to-platform}

La documentazione seguente fornisce informazioni su come creare un [!DNL Pendo] connettore di streaming per la connessione [!DNL Platform] utilizzando le API o l’interfaccia utente:

### Connetti [!DNL Pendo] alla piattaforma utilizzando le API {#connect-to-platform-using-api}

* [Crea una connessione sorgente da portare [!DNL Pendo] dati a Platform tramite API.](../../tutorials/api/create/analytics/pendo-webhook.md)

### Connetti [!DNL Pendo] a Platform tramite l’interfaccia utente {#connect-to-platform-using-ui}

* [Crea una connessione sorgente da portare [!DNL Pendo] dati a Platform tramite l’interfaccia utente](../../tutorials/ui/create/analytics/pendo-webhook.md)
