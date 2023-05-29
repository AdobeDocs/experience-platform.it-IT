---
keywords: Experience Platform;home;argomenti popolari;Zendesk;zendesk
solution: Experience Platform
title: Panoramica del connettore di origine Zendesk
description: Scopri come collegare Zendesk a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
exl-id: 9f245783-949d-4f40-9cf3-8991b4b6d780
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 2%

---

# (Beta) [!DNL Zendesk]

>[!NOTE]
>
>Il [!DNL Zendesk] sorgente in versione beta. Consulta la [panoramica sulle origini](../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo di fonti etichettate beta.

Adobe Experience Platform consente di acquisire i dati da origini esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi di Platform. È possibile acquisire dati da diverse origini, ad esempio applicazioni Adobe, archiviazione basata su cloud, database e molte altre.

Experience Platform fornisce supporto per l’acquisizione di dati da un’applicazione di successo per un cliente di terze parti. Il supporto per i provider di successo dei clienti include [!DNL Zendesk].

Questo Adobe Experience Platform [sorgenti](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=it) sfrutta [API di ricerca Zendesk > Esporta risultati di ricerca](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results) che restituisce le informazioni degli utenti in Experience Platform da Zendesk per un’ulteriore elaborazione.

## ELENCO CONSENTITI di indirizzo IP

Prima di utilizzare i connettori di origine, è necessario aggiungere un elenco di indirizzi IP a un elenco consentiti. La mancata aggiunta all’elenco consentiti degli indirizzi IP specifici per l’area geografica potrebbe causare errori o prestazioni non ottimali durante l’utilizzo delle origini. Consulta la [ELENCO CONSENTITI di indirizzo IP](../../ip-address-allow-list.md) per ulteriori informazioni.

## Autentica il tuo [!DNL Zendesk] account

[!DNL Zendesk] utilizza token Bearer come meccanismo di autenticazione per comunicare con [!DNL Zendesk] API.

Questa sezione descrive i passaggi prerequisiti da completare per autenticare il [!DNL Zendesk] account.

* Il primo passaggio nell’autenticazione del [!DNL Zendesk] l&#39;account deve garantire di avere [!DNL Zendesk] account di supporto. Se non ne hai già una, vedi [[!DNL Zendesk] pagina di registrazione](https://www.zendesk.com/register/) per registrarvi e creare il vostro account Zendesk.
* Dopo aver effettuato correttamente la registrazione, accedi al [[!DNL Zendesk] sito web](https://www.zendesk.com/login/) e fornisci **sottodominio**.
* Quindi, seleziona **[!DNL Settings]** > **[!DNL Apps and Integrations]** > **[!DNL Zendesk API]**.
* Infine, recupera il token API da **[!DNL API token]** sezione.

![Token API Zendesk](../../images/tutorials/create/zendesk/zendesk-api-tokens.png)

Consulta la [[!DNL Zendesk documentation on subdomains]](https://support.zendesk.com/hc/en-us/articles/4409381383578-Where-can-I-find-my-Zendesk-subdomain-) per informazioni su come recuperare il sottodominio. Per informazioni sulla generazione del token API, vedi [[!DNL Zendesk] guida alla generazione di un nuovo token API](https://support.zendesk.com/hc/en-us/articles/4408889192858-Generating-a-new-API-token).

La documentazione seguente fornisce informazioni sulle modalità di connessione [!DNL Zendesk] in Platform tramite API o l’interfaccia utente:

## Connetti [!DNL Zendesk] alla piattaforma utilizzando le API

* [Creare una connessione di origine e un flusso di dati per [!DNL Zendesk] utilizzo dell’API del servizio Flusso](../../tutorials/api/create/customer-success/zendesk.md)

## Connetti [!DNL Zendesk] a Platform tramite l’interfaccia utente

* [Creare un [!DNL Zendesk ]connessione sorgente nell’interfaccia utente](../../tutorials/ui/create/customer-success/zendesk.md)
* [Creare un flusso di dati per una connessione sorgente di successo del cliente nell’interfaccia utente](../../tutorials/ui/dataflow/customer-success.md)
