---
title: Panoramica del connettore Source di Salesforce Service Cloud
description: Scopri come collegare Salesforce Service Cloud a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
exl-id: 9bebbc00-55b3-4aec-9357-4127c05844e2
source-git-commit: b9a9b00114b3c1159a14b7e39484d250fa7563ba
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 2%

---

# [!DNL Salesforce Service Cloud]

[!DNL Salesforce Service Cloud] è una piattaforma di successo del cliente progettata per automatizzare i flussi di lavoro dei servizi e semplificare la comunicazione tra le aziende e i loro clienti. Consolida le richieste provenienti da vari canali, ad esempio e-mail, telefono, social media e chat in tempo reale, in una console di agenti unificata. Questo consente ai team di supporto di gestire i &quot;casi&quot; con una visualizzazione a 360 gradi della cronologia del cliente, garantendo che le risposte siano personalizzate ed efficienti indipendentemente da come il cliente si rivolge.

È possibile utilizzare il connettore di origine [!DNL Salesforce Service Cloud] in Adobe Experience Platform Sources per connettere l&#39;account [!DNL Salesforce Service Cloud] e inserire i dati da utilizzare nei servizi Experience Platform.

Leggi questo documento per scoprire come configurare l&#39;account [!DNL Salesforce Service Cloud] e collegarlo ad Experience Platform.

## Prerequisiti {#prerequisites}

Leggi questa sezione per la configurazione dei prerequisiti che è necessario completare prima di connettersi correttamente ad Experience Platform.

### Indirizzo IP inserisco nell&#39;elenco Consentiti {#allowlist}

Prima di collegare le origini a Experience Platform, è necessario aggiungere al elenco Consentiti di indirizzi IP specifici per l’area geografica. Per ulteriori informazioni, leggere la guida in [inserire nell&#39;elenco Consentiti degli indirizzi IP per la connessione ad Experience Platform](../../ip-address-allow-list.md).

### Raccogli le credenziali richieste {#credentials}

È necessario fornire i valori per le credenziali seguenti per connettere l&#39;account [!DNL Salesforce Service Cloud] utilizzando le credenziali client OAuth2.

| Credenziali | Descrizione |
| --- | --- |
| URL ambiente | URL dell&#39;istanza di origine [!DNL Salesforce Service Cloud]. |
| ID client | L’ID client viene utilizzato insieme al segreto client come parte dell’autenticazione OAuth2. Insieme, l&#39;ID client e il segreto client consentono all&#39;applicazione di funzionare per conto dell&#39;account identificando l&#39;applicazione in [!DNL Salesforce Service Cloud]. |
| Segreto client | Il segreto client viene utilizzato insieme all’ID client come parte dell’autenticazione OAuth2. Insieme, l&#39;ID client e il segreto client consentono all&#39;applicazione di funzionare per conto dell&#39;account identificando l&#39;applicazione in [!DNL Salesforce Service Cloud]. |
| Versione API | Versione REST API dell&#39;istanza [!DNL Salesforce Service Cloud] in uso. Il valore della versione API deve essere formattato con un decimale. Ad esempio, se utilizzi la versione API `52`, devi immettere il valore come `52.0`. Se questo campo viene lasciato vuoto, Experience Platform utilizzerà automaticamente l’ultima versione disponibile. |

Per ulteriori informazioni sull&#39;utilizzo di OAuth per [!DNL Salesforce Service Cloud], leggere la [[!DNL Salesforce Service Cloud] guida sui flussi di autorizzazione OAuth](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&type=5).

## Connetti [!DNL Salesforce Service Cloud] ad Experience Platform tramite API

- [Creare una connessione di base a Salesforce Service Cloud utilizzando l’API del servizio Flow](../../tutorials/api/create/customer-success/salesforce-service-cloud.md)
- [Esplorare le tabelle di dati utilizzando l’API del servizio Flusso](../../tutorials/api/explore/tabular.md)
- [Creare un flusso di dati per un’origine di successo del cliente utilizzando l’API del servizio Flusso](../../tutorials/api/collect/customer-success.md)

## Connetti [!DNL Salesforce Service Cloud] ad Experience Platform tramite l&#39;interfaccia utente

- [Creare una connessione sorgente Salesforce Service Cloud nell’interfaccia utente](../../tutorials/ui/create/customer-success/salesforce-service-cloud.md)
- [Creare un flusso di dati per una connessione sorgente di successo del cliente nell’interfaccia utente](../../tutorials/ui/dataflow/customer-success.md)
