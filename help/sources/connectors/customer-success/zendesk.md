---
keywords: Experience Platform;casa;argomenti popolari;Zendesk;zendesk
solution: Experience Platform
title: Panoramica del connettore di origine Zendesk
description: Scopri come collegare Zendesk a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
exl-id: 9f245783-949d-4f40-9cf3-8991b4b6d780
source-git-commit: 61b694ca5fbd3548243663b3f1bff06aaca72434
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 2%

---

# (Beta) [!DNL Zendesk]

>[!NOTE]
>
>La [!DNL Zendesk] la sorgente è in versione beta. Consulta la sezione [panoramica di origini](../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo di origini con etichetta beta.

Adobe Experience Platform consente di acquisire dati da sorgenti esterne e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Platform. È possibile acquisire dati da diverse sorgenti, come applicazioni di Adobe, archiviazione basata su cloud, database e molti altri.

Experience Platform fornisce il supporto per l’acquisizione di dati da un’applicazione di successo per clienti di terze parti. Il supporto per i fornitori di successo dei clienti include: [!DNL Zendesk].

Questo Adobe Experience Platform [origini](https://experienceleague.adobe.com/docs/experience-platform/sources/home.html?lang=it) sfrutta [API di ricerca Zendesk > Esporta risultati di ricerca](https://developer.zendesk.com/api-reference/ticketing/ticket-management/search/#export-search-results) che restituisce le informazioni degli utenti in Experience Platform da Zendesk per ulteriori elaborazioni.

## ELENCO CONSENTITI di indirizzo IP

Prima di utilizzare i connettori sorgente, è necessario aggiungere a un elenco consentiti un elenco di indirizzi IP. Se l’utente non aggiunge all’elenco consentiti gli indirizzi IP specifici per l’area geografica, potrebbero verificarsi errori o prestazioni non soddisfacenti durante l’utilizzo delle origini. Consulta la sezione [ELENCO CONSENTITI di indirizzo IP](../../ip-address-allow-list.md) per ulteriori informazioni.

## Autentica il tuo [!DNL Zendesk] account

[!DNL Zendesk] utilizza i token portatori come meccanismo di autenticazione per comunicare con [!DNL Zendesk] API.

Questa sezione descrive i passaggi preliminari da completare per l’autenticazione del tuo [!DNL Zendesk] conto.

* Il primo passaggio nell&#39;autenticazione del tuo [!DNL Zendesk] l&#39;account deve essere [!DNL Zendesk] account di supporto. Se non ne hai già uno, vedi la [[!DNL Zendesk] pagina di registrazione](https://www.zendesk.com/register/) per registrarti e creare il tuo account Zendesk.
* Dopo aver effettuato la registrazione, passa alla [[!DNL Zendesk] sito web](https://www.zendesk.com/login/) e forniscono **sottodominio**.
* Quindi, seleziona **[!DNL Settings]** > **[!DNL Apps and Integrations]** > **[!DNL Zendesk API]**.
* Infine, recupera il token API dal **[!DNL API token]** sezione .

![Token API Zendesk](../../images/tutorials/create/zendesk/zendesk-api-tokens.png)

Consulta la sezione [[!DNL Zendesk documentation on subdomains]](https://support.zendesk.com/hc/en-us/articles/4409381383578-Where-can-I-find-my-Zendesk-subdomain-) per informazioni su come recuperare il sottodominio. Per informazioni sulla generazione del token API, consulta [[!DNL Zendesk] guida alla generazione di un nuovo token API](https://support.zendesk.com/hc/en-us/articles/4408889192858-Generating-a-new-API-token).

La documentazione seguente fornisce informazioni su come connettersi [!DNL Zendesk] su Platform utilizzando le API o l’interfaccia utente:

## Connetti [!DNL Zendesk] su Platform tramite API

* [Creare una connessione sorgente e un flusso di dati per [!DNL Zendesk] utilizzo dell’API del servizio di flusso](../../tutorials/api/create/customer-success/zendesk.md)

## Connetti [!DNL Zendesk] su Platform tramite l’interfaccia utente

* [Crea un [!DNL Zendesk ]connessione sorgente nell’interfaccia utente](../../tutorials/ui/create/customer-success/zendesk.md)
* [Creare un flusso di dati per una connessione sorgente con successo cliente nell’interfaccia utente](../../tutorials/ui/dataflow/customer-success.md)
