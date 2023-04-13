---
title: Panoramica di Pendo Source
description: Scopri come collegare Pendo a Adobe Experience Platform utilizzando API o l’interfaccia utente sfruttando i webhook
badge: Beta
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 376f18ef-1eea-4c42-8041-6fadb5906e9b
source-git-commit: 0cc4eab97dcd56d2b1d679cf5f35932976d22634
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# [!DNL Pendo]

>[!NOTE]
>
>La [!DNL Pendo] la sorgente è in versione beta. Per piacere, leggi le [panoramica di origini](../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo di origini con etichetta beta.

Adobe Experience Platform consente di acquisire dati da sorgenti esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, database e molti altri.

Experience Platform fornisce il supporto per l’acquisizione di dati da applicazioni di analisi di terze parti. Il supporto per i provider di analisi include [!DNL Pendo].

[[!DNL Pendo]](https://pendo.io/) è un’app di analisi dei prodotti creata per aiutare le aziende di software a sviluppare prodotti che rispondano con i clienti. L’app consente ai produttori di software di incorporare i loro prodotti con un’ampia gamma di strumenti che possono condurre sia a una migliore esperienza di prodotto per gli utenti che a nuove informazioni per il team di prodotto.

La [!DNL Pendo] source consente di acquisire gli schemi di eventi webhook supportati e i relativi dati evento associati da [!DNL Pendo.io] utilizzando [[!DNL Pendo] Webhook](https://support.pendo.io/hc/en-us/articles/360032285012-Webhooks). La [!DNL Pendo] sorgente funziona con [!DNL Pendo] Webhook URL.

I webhook supportati sono:

* [Guida](https://support.pendo.io/hc/en-us/articles/8146679315867-Creating-a-Guide) Visualizzato
* [Sondaggio](https://support.pendo.io/hc/en-us/articles/360031867152-Polls-Classic-) Visualizzato/Inviato
* [Punteggio promozionale netto](https://support.pendo.io/hc/en-us/articles/360033527151-Set-up-an-NPS-Survey) Visualizzato/Inviato

## Prerequisiti {#prerequisites}

Prima di creare un [!DNL Pendo] connessione di origine, è innanzitutto necessario assicurarsi di disporre dei seguenti elementi:

A [!DNL Pendo] conto. Se non ne hai già uno, vedi la [[!DNL Pendo] registrare](https://app.pendo.io/register) per registrare e creare il tuo account.

### Configurazione [!DNL Pendo] Webhook {#set-up-webhook}

Una volta creato correttamente il flusso di dati, devi impostare un webhook per informare Platform su [!DNL Pendo] eventi. [!DNL Pendo] I webhook possono inviare notifiche in tempo reale ad altri servizi quando si verificano determinati eventi e inviare tali informazioni ai tuoi [!DNL Pendo] sorgente. Per ulteriori informazioni, consulta le esercitazioni su [ottenimento dell’URL dell’endpoint di streaming](../../tutorials/ui/create/analytics/pendo-webhook.md#get-streaming-endpoint) e [creazione di un [!DNL Pendo] Webhook](../../tutorials/ui/create/analytics/pendo-webhook.md#set-up-webhook).

## Collegamento [!DNL Pendo] su Platform {#connect-to-platform}

La documentazione seguente fornisce informazioni su come creare un [!DNL Pendo] connettore streaming con cui connettersi [!DNL Platform] utilizzando le API o l’interfaccia utente:

### Connetti [!DNL Pendo] su Platform tramite API {#connect-to-platform-using-api}

* [Crea una connessione sorgente da portare [!DNL Pendo] in Platform tramite API.](../../tutorials/api/create/analytics/pendo-webhook.md)

### Connetti [!DNL Pendo] su Platform tramite l’interfaccia utente {#connect-to-platform-using-ui}

* [Crea una connessione sorgente da portare [!DNL Pendo] dati a Platform tramite l’interfaccia utente](../../tutorials/ui/create/analytics/pendo-webhook.md)
