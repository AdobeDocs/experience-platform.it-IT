---
title: Panoramica di PathFactory Source
description: Scopri come collegare PathFactory a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
last-substantial-update: 2024-04-30T00:00:00Z
badge: Beta
exl-id: befb73c4-fd6a-4512-9124-d23a1c27e0e0
source-git-commit: ca17854830edabaf2bd74265258d6f0096f2888e
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 3%

---

# [!DNL PathFactory]

>[!NOTE]
>
>L&#39;origine [!DNL PathFactory] è in versione beta. Per ulteriori informazioni sull&#39;utilizzo di origini con etichetta beta, leggere la [panoramica delle origini](../../home.md#terms-and-conditions).

[[!DNL PathFactory]](https://www.pathfactory.com/) offre una piattaforma basata su cloud che consente alle aziende di gestire i percorsi di contenuti e favorire il coinvolgimento attraverso informazioni intelligenti sui contenuti. Questa guida descrive come integrare i dati da PathFactory in Experience Platform, utilizzando i connettori di PathFactory per un’acquisizione ottimale dei dati.

È possibile acquisire dati da [[!DNL PathFactory]](https://www.pathfactory.com/) utilizzando tre origini primarie:

* **[!DNL Visitors]**: acquisisci i dati dei clienti e dei contatti come record per comprendere meglio il tuo pubblico.
* **[!DNL Sessions]**: eventi della serie temporale che tengono traccia delle attività delle singole sessioni utente sulla piattaforma.
* **[!DNL Page Views]**: eventi della serie temporale che forniscono informazioni approfondite sulle pagine visualizzate, utili per analizzare le prestazioni dei contenuti.

Per informazioni su come configurare l&#39;account di origine [!DNL PathFactory], leggere il documento seguente.

## ELENCO CONSENTITI di indirizzo IP {#ip-allow-list}

Prima di utilizzare i connettori di origine, potrebbe essere necessario aggiungere un elenco di indirizzi IP a un elenco consentiti. La mancata aggiunta all’elenco consentiti degli indirizzi IP specifici per l’area geografica potrebbe causare errori o prestazioni non ottimali durante l’utilizzo delle origini. Per ulteriori informazioni, vedere la pagina [elenco consentiti indirizzo IP](../../ip-address-allow-list.md).

## Prerequisiti {#prerequisites}

Prima di iniziare a integrare i connettori [[!DNL PathFactory]](https://www.pathfactory.com/) con Experience Platform, verifica di soddisfare i seguenti prerequisiti:

* **Un account [PathFactory]**.
   * Contattare [[!DNL PathFactory]](https://www.pathfactory.com/portal/company/contactus.shtml) se non si dispone già di un account valido.
* **Sottoscrizione attiva** a qualsiasi prodotto [!DNL PathFactory].
* **Nome utente, password e dominio**.
   * Queste credenziali sono necessarie per accedere all&#39;account [!DNL PathFactory] e ai relativi dati.
* **Token di accesso** e **endpoint API**.
   * Questi sono necessari per la connessione con le API [!DNL PathFactory].

### Ottenere credenziali e token di accesso {#gather-credentials}

Per connettere [!DNL PathFactory] a Experience Platform, è necessario fornire le credenziali seguenti:

| Credenziali | Descrizione | Endpoint |
| --- | --- | --- |
| Nome utente | Nome utente dell&#39;account [!DNL PathFactory]. | Non applicabile |
| Password | Password dell&#39;account [!DNL PathFactory]. | Non applicabile |
| Dominio | Il dominio associato al tuo account [!DNL PathFactory]. | Non applicabile |
| Token di accesso | Token univoco utilizzato per l’autenticazione API. | Non applicabile |
| Endpoint visitatori | L’endpoint API per i dati dei visitatori. | `/api/public/v3/data_lake_apis/visitors.json` |
| Endpoint sessioni | Endpoint API per i dati della sessione. | `/api/public/v3/data_lake_apis/sessions.json` |
| Endpoint visualizzazioni pagina | Endpoint API per i dati di visualizzazione della pagina. | `/api/public/v3/data_lake_apis/page_views.json` |

Per istruzioni dettagliate su come ottenere il nome utente, la password, il dominio e il token di accesso, visitare il [[!DNL PathFactory] Centro di assistenza](https://support.pathfactory.com/categories/adobe/). Questa risorsa fornisce guide complete sul recupero e la gestione delle credenziali.

### Configurare le autorizzazioni su Experience Platform

Per connettere l&#39;account [!DNL PathFactory] all&#39;Experience Platform, è necessario avere entrambe le autorizzazioni **[!UICONTROL Visualizza origini]** e **[!UICONTROL Gestisci origini]** abilitate per il proprio account. Contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie. Per ulteriori informazioni, leggere la [guida all&#39;interfaccia utente per il controllo degli accessi](../../../access-control/ui/overview.md).

## Connetti [!DNL PathFactory] a Platform {#pathfactory-connect}

La documentazione seguente fornisce informazioni su come connettere [!DNL PathFactory] a Platform tramite API o tramite l&#39;interfaccia utente:

* [Crea una connessione di origine e un flusso di dati per portare [!DNL PathFactory] dati in Platform tramite API](../../tutorials/api/create/marketing-automation/pathfactory.md).
* [Connetti il tuo account [!DNL PathFactory] ad Experience Platform utilizzando l&#39;interfaccia utente](../../tutorials/ui/create/marketing-automation/pathfactory.md).
* [Creare un flusso di dati per una connessione di origine utilizzando l&#39;interfaccia utente](../../tutorials/ui/dataflow/marketing-automation.md).
