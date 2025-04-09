---
title: Panoramica di Source sui profili utente dell’Algolia
description: Scopri l’origine dei profili utente di Algolia in Adobe Experience Platform
hide: true
hidefromtoc: true
source-git-commit: 1bde4b831f1b79de1a8292ad5f221f522e871d08
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# [!DNL Algolia User Profiles]

[[!DNL Algolia]](https://www.algolia.com/) è una potente piattaforma API di ricerca e individuazione che consente alle aziende di fornire esperienze di ricerca veloci, pertinenti e personalizzabili. Fornisce funzionalità di ricerca in tempo reale con funzioni quali tolleranza agli errori di battitura, filtraggio, faceting e tuning di rilevanza basato sull’intelligenza artificiale. [!DNL Algolia] consente alle aziende di migliorare il coinvolgimento degli utenti, i tassi di conversione e l&#39;esperienza complessiva del cliente fornendo soluzioni di ricerca ad alte prestazioni per siti Web, piattaforme di e-commerce e applicazioni.

Alcuni dei principali vantaggi di [!DNL Algolia] includono:

* Ricerca fulminea con risultati immediati.
* Raccomandazioni altamente rilevanti basate sull’intelligenza artificiale.
* Classificazione personalizzabile per dare priorità alle esigenze aziendali.
* Scalabilità per gestire facilmente carichi di traffico elevati.

Per ulteriori informazioni, visitare la [[!DNL Algolia] documentazione del prodotto](https://resources.algolia.com/).

## Architettura

Origini self-service (Batch SDK) offre tutte le funzioni necessarie, ad esempio autenticazione, impaginazione o estrazione dati completa e parziale. L&#39;origine [!DNL Algolia User Profiles] utilizza queste funzionalità per completare l&#39;integrazione.

![Architettura dell&#39;integrazione di Algolia e Experience Platform](../../images/tutorials/create/algolia/user-profiles/algolia-aep-user-profiles-arch.png)

## Prerequisiti {#prerequisites}

Prima di connettere l&#39;account [!DNL Algolia] ad Experience Platform, è necessario completare i seguenti passaggi preliminari.

1. Utilizza il [[!DNL Algolia] dashboard](https://dashboard.algolia.com/users/sign_up) per accedere al tuo account [!DNL Algolia] o crearne uno nuovo.
2. [Prepara l&#39;indice](https://www.algolia.com/doc/guides/sending-and-managing-data/prepare-your-data/in-depth/prepare-data-in-depth/).
3. [Configura i facet](https://www.algolia.com/doc/guides/managing-results/refine-results/faceting/).
4. [Invia eventi utente](https://www.algolia.com/doc/guides/sending-events/getting-started/).
5. [Personalizza indice](https://www.algolia.com/doc/guides/personalization/advanced-personalization/configure/setup/indices/).

### Configurare le autorizzazioni su Experience Platform

Per connettere l&#39;account [!DNL Algolia] ad Experience Platform, è necessario che per l&#39;account siano abilitate le autorizzazioni **[!UICONTROL Visualizza origini]** e **[!UICONTROL Gestisci origini]**. Contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie. Per ulteriori informazioni, leggere la [guida all&#39;interfaccia utente per il controllo degli accessi](../../../access-control/abac/ui/permissions.md).

### Indirizzo IP inserisco nell&#39;elenco Consentiti

Prima di utilizzare i connettori di origine, è necessario aggiungere un elenco di indirizzi IP a un inserisco nell&#39;elenco Consentiti di. La mancata aggiunta di indirizzi IP specifici per l’area geografica al elenco Consentiti può causare errori o non prestazioni durante l’utilizzo delle origini. Per ulteriori informazioni, vedere la pagina [Indirizzo IP/inserisco nell&#39;elenco Consentiti di](../../ip-address-allow-list.md).

## Connetti il tuo account [!DNL Algolia] ad Experience Platform

Dopo aver completato i prerequisiti, puoi procedere al passaggio successivo e [connettere il tuo account [!DNL Algolia] ad Experience Platform](../../tutorials/ui/create/data-partners/algolia-user-profiles.md).
