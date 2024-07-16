---
title: Panoramica del connettore Source Zendesk
description: Scopri come collegare Zendesk a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: 9f245783-949d-4f40-9cf3-8991b4b6d780
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---

# [!DNL Zendesk]

Adobe Experience Platform consente di acquisire i dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform. È possibile acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, database e molte altre.

Experience Platform fornisce supporto per l’acquisizione di dati da un’applicazione di successo per un cliente di terze parti. Il supporto per i provider di successo dei clienti include [!DNL Zendesk].

Questa [sorgente](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=it) di Adobe Experience Platform sfrutta l&#39;[API di ricerca Zendesk > Esporta risultati ricerca](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results) che restituisce le informazioni degli utenti in Experience Platform da Zendesk per ulteriori elaborazioni.

## ELENCO CONSENTITI di indirizzo IP

Prima di utilizzare i connettori di origine, è necessario aggiungere un elenco di indirizzi IP a un elenco consentiti. La mancata aggiunta all’elenco consentiti degli indirizzi IP specifici per l’area geografica potrebbe causare errori o prestazioni non ottimali durante l’utilizzo delle origini. Per ulteriori informazioni, vedere la pagina [elenco consentiti indirizzo IP](../../ip-address-allow-list.md).

## Autentica il tuo account [!DNL Zendesk]

[!DNL Zendesk] utilizza token Bearer come meccanismo di autenticazione per comunicare con l&#39;API [!DNL Zendesk].

Questa sezione descrive i passaggi preliminari da completare per autenticare l&#39;account [!DNL Zendesk].

* Il primo passaggio per autenticare l&#39;account [!DNL Zendesk] consiste nel verificare di disporre dell&#39;account di supporto [!DNL Zendesk]. Se non ne hai già una, vedi la [[!DNL Zendesk] pagina di registrazione](https://www.zendesk.com/register/) per registrarti e creare il tuo account Zendesk.
* Dopo aver completato la registrazione, passa al [[!DNL Zendesk] sito Web](https://www.zendesk.com/login/) e specifica il **sottodominio**.
* Selezionare **[!DNL Settings]** > **[!DNL Apps and Integrations]** > **[!DNL Zendesk API]**.
* Infine, recupera il token API dalla sezione **[!DNL API token]**.

![Token API Zendesk](../../images/tutorials/create/zendesk/zendesk-api-tokens.png)

Per informazioni su come recuperare il sottodominio, vedere [[!DNL Zendesk documentation on subdomains]](<https://support.zendesk.com/hc/en-us/articles/4409381383578-Where-can-I-find-my-Zendesk-subdomain->). Per informazioni sulla generazione del token API, consulta la [[!DNL Zendesk] guida sulla generazione di un nuovo token API](<https://support.zendesk.com/hc/en-us/articles/4408889192858-Generating-a-new-API-token>).

La documentazione seguente fornisce informazioni su come connettere [!DNL Zendesk] a Platform tramite API o tramite l&#39;interfaccia utente:

## Connetti [!DNL Zendesk] a Platform tramite API

* [Crea una connessione di origine e un flusso di dati per  [!DNL Zendesk]  utilizzando l&#39;API del servizio Flusso](../../tutorials/api/create/customer-success/zendesk.md)

## Connetti [!DNL Zendesk] a Platform tramite l&#39;interfaccia utente

* [Crea una connessione di origine  [!DNL Zendesk ] nell&#39;interfaccia utente](../../tutorials/ui/create/customer-success/zendesk.md)
* [Creare un flusso di dati per una connessione sorgente di successo del cliente nell’interfaccia utente](../../tutorials/ui/dataflow/customer-success.md)
