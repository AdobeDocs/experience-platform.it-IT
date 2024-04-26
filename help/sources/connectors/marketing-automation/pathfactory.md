---
title: Panoramica dell’origine PathFactory
description: Scopri come collegare PathFactory a Adobe Experience Platform utilizzando le API o l’interfaccia utente.
last-substantial-update: 2024-04-30T00:00:00Z
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: 18f6c253aec6815cf84272cbce340a9aa7ed8ab9
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 3%

---

# [!DNL PathFactory]

>[!NOTE]
>
>Il [!DNL PathFactory] sorgente in versione beta. Leggi le [panoramica sulle origini](../../home.md#terms-and-conditions) per ulteriori informazioni sull’utilizzo di fonti etichettate beta.

[[!DNL PathFactory]](https://www.pathfactory.com/) offre una piattaforma basata su cloud che consente alle aziende di gestire i percorsi di contenuti e aumentare il coinvolgimento attraverso informazioni sui contenuti intelligenti. Questa guida descrive come integrare i dati da PathFactory in Experienci Platform, utilizzando i connettori di PathFactory per un’acquisizione ottimale dei dati.

Puoi acquisire dati da [[!DNL PathFactory]](https://www.pathfactory.com/) utilizzando tre fonti primarie:

* **[!DNL Visitors]**: acquisisci i dati dei clienti e dei contatti come record per comprendere meglio il pubblico.
* **[!DNL Sessions]**: eventi della serie temporale che tengono traccia delle attività delle singole sessioni utente sulla piattaforma.
* **[!DNL Page Views]**: eventi della serie temporale che forniscono informazioni approfondite sulle pagine visualizzate, utili per analizzare le prestazioni dei contenuti.

Per informazioni su come impostare il [!DNL PathFactory] account di origine.

## ELENCO CONSENTITI di indirizzo IP {#ip-allow-list}

Prima di utilizzare i connettori di origine, potrebbe essere necessario aggiungere un elenco di indirizzi IP a un elenco consentiti. La mancata aggiunta all’elenco consentiti degli indirizzi IP specifici per l’area geografica potrebbe causare errori o prestazioni non ottimali durante l’utilizzo delle origini. Consulta la [ELENCO CONSENTITI di indirizzo IP](../../ip-address-allow-list.md) per ulteriori informazioni.

## Prerequisiti {#prerequisites}

Prima di iniziare l’integrazione [[!DNL PathFactory]](https://www.pathfactory.com/) connettori con Experience Platform, assicurati di soddisfare i seguenti prerequisiti:

* **A [Account PathFactory]**.
   * Contatto [[!DNL PathFactory]](https://www.pathfactory.com/portal/company/contactus.shtml) se non disponi già di un account valido.
* **Una sottoscrizione attiva** a qualsiasi [!DNL PathFactory] prodotto.
* **Nome utente, password e dominio**.
   * Queste credenziali sono necessarie per accedere al tuo [!DNL PathFactory] account e i relativi dati.
* **Token di accesso** e **Endpoint API**.
   * Questi sono necessari per la connessione con [!DNL PathFactory] API.

### Ottenere credenziali e token di accesso {#gather-credentials}

Per connettersi [!DNL PathFactory] ad Experience Platform, devi fornire le seguenti credenziali:

| Credenziali | Descrizione | Endpoint |
| --- | --- | --- |
| Nome utente | Il tuo [!DNL PathFactory] nome utente dell’account. | Non applicabile |
| Password | Il tuo [!DNL PathFactory] password dell&#39;account. | Non applicabile |
| Dominio | Il dominio associato al tuo [!DNL PathFactory] account. | Non applicabile |
| Token di accesso | Token univoco utilizzato per l’autenticazione API. | Non applicabile |
| Endpoint visitatori | L’endpoint API per i dati dei visitatori. | `/api/public/v3/data_lake_apis/visitors.json` |
| Endpoint sessioni | Endpoint API per i dati della sessione. | `/api/public/v3/data_lake_apis/sessions.json` |
| Endpoint visualizzazioni pagina | Endpoint API per i dati di visualizzazione della pagina. | `/api/public/v3/data_lake_apis/page_views.json` |

Per istruzioni dettagliate su come ottenere nome utente, password, dominio e token di accesso, visita [[!DNL PathFactory] Centro assistenza](https://support.pathfactory.com/categories/adobe/). Questa risorsa fornisce guide complete sul recupero e la gestione delle credenziali.

### Configurare le autorizzazioni su Experienci Platform

Devi avere entrambi **[!UICONTROL Visualizza origini]** e **[!UICONTROL Gestisci origini]** autorizzazioni abilitate per il tuo account per connettersi al tuo [!DNL PathFactory] da Experience Platform. Contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie. Per ulteriori informazioni, leggere [guida all’interfaccia utente per il controllo degli accessi](../../../access-control/ui/overview.md).

## Connetti [!DNL PathFactory] alla piattaforma {#pathfactory-connect}

La documentazione seguente fornisce informazioni sulle modalità di connessione [!DNL PathFactory] in Platform tramite API o l’interfaccia utente:

* [Creare una connessione di origine e un flusso di dati per portare [!DNL PathFactory] dati per Platform tramite API](../../tutorials/api/create/marketing-automation/pathfactory.md).
* [Connetti [!DNL PathFactory] Experience Platform dell’account tramite l’interfaccia utente](../../tutorials/ui/create/marketing-automation/pathfactory.md).
* [Creare un flusso di dati per una connessione sorgente utilizzando l’interfaccia utente](../../tutorials/ui/dataflow/marketing-automation.md).
