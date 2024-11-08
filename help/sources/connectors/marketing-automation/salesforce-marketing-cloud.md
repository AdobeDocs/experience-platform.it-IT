---
solution: Experience Platform
title: Panoramica di Salesforce Marketing Cloud Source
description: Scopri come collegare il Marketing Cloud Salesforce a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
exl-id: 2177d68c-0cef-4031-a0e7-8bf22ee2e70b
last-substantial-update: 2023-05-25T00:00:00Z
source-git-commit: 474b81aa8caf58013f8ea7cff9ad59d92466aac8
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---

# [!DNL Salesforce Marketing Cloud]

>[!WARNING]
>
>L&#39;origine [!DNL Salesforce Marketing Cloud] diventerà obsoleta alla fine di maggio 2025.

Adobe Experience Platform consente di acquisire i dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform. È possibile acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, database e molte altre.

Experience Platform fornisce supporto per l’acquisizione di dati da sistemi di automazione del marketing di terze parti. Il supporto per i provider di automazione marketing include [!DNL Salesforce Marketing Cloud].

## Prerequisiti

Prima di poter connettere l&#39;origine [!DNL Salesforce Marketing Cloud] a Platform, è necessario assicurarsi che sia stato eseguito il provisioning dei seguenti **ambiti di autorizzazione** per l&#39;ID client [!DNL Salesforce Marketing Cloud] e la combinazione di segreto client:

* `campaign_read`
* `list_and_subscribers_read`

È possibile richiedere ambiti effettuando una chiamata alla risorsa `v2/userinfo` dell&#39;API [!DNL Salesforce Marketing Cloud]. Per istruzioni su come richiedere e confrontare gli ambiti, consulta il documento [[!DNL Salesforce Marketing Cloud] Ambiti di autorizzazione dell&#39;integrazione API](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/data-access-permissions.html>).

Per ulteriori informazioni sugli ambiti, incluso un elenco delle autorizzazioni e dei comportamenti correlati, vedere questo [[!DNL Salesforce Marketing Cloud] documento REST API](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rest-permissions-and-scopes.html>).

>[!IMPORTANT]
>
>L&#39;acquisizione di oggetti personalizzati non è attualmente supportata dall&#39;integrazione di origine [!DNL Salesforce Marketing Cloud].

## ELENCO CONSENTITI di indirizzo IP

Prima di utilizzare i connettori di origine, è necessario aggiungere un elenco di indirizzi IP a un elenco consentiti. La mancata aggiunta all’elenco consentiti degli indirizzi IP specifici per l’area geografica potrebbe causare errori o prestazioni non ottimali durante l’utilizzo delle origini. Per ulteriori informazioni, vedere la pagina [elenco consentiti indirizzo IP](../../ip-address-allow-list.md).

## Connetti [!DNL Salesforce Marketing Cloud] a Platform tramite API

La documentazione seguente fornisce informazioni su come connettere [!DNL Salesforce Marketing Cloud] a Platform tramite API:

* [Creare una connessione di base al Marketing Cloud Salesforce utilizzando l’API del servizio Flusso](../../tutorials/api/create/marketing-automation/salesforce-marketing-cloud.md)
* [Esplorare le tabelle di dati utilizzando l’API del servizio Flusso](../../tutorials/api/explore/tabular.md)
* [Creare un flusso di dati per un’origine di automazione marketing utilizzando l’API del servizio Flusso](../../tutorials/api/collect/marketing-automation.md)

## Connetti [!DNL Salesforce Marketing Cloud] a Platform tramite l&#39;interfaccia utente

La documentazione seguente fornisce informazioni su come connettere [!DNL Salesforce Marketing Cloud] a Platform tramite l&#39;interfaccia utente:

* [Creare una connessione sorgente del Marketing Cloud Salesforce nell’interfaccia utente](../../tutorials/ui/create/marketing-automation/salesforce-marketing-cloud.md)
* [Creare un flusso di dati per una connessione sorgente dell’automazione marketing nell’interfaccia utente](../../tutorials/ui/dataflow/marketing-automation.md)
