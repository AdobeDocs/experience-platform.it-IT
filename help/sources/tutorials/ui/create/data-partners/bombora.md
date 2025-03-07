---
title: Collegare L’Intento Di Bombora Ad Experience Platform Utilizzando L’Interfaccia Utente
description: Scopri come collegare Bombora Intent ad Experience Platform
hide: true
hidefromtoc: true
source-git-commit: 81a615b9826ed69bb050cae9c074a4e457ba128a
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 10%

---

# Connetti [!DNL Bombora Intent] ad Experience Platform tramite l&#39;interfaccia utente

Leggere questa guida per scoprire come collegare l&#39;account [!DNL Bombora Intent] a Adobe Experience Platform utilizzando l&#39;interfaccia utente.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [Real-Time CDP B2B edition](../../../../../rtcdp/b2b-overview.md): Real-Time CDP B2B edition è progettato appositamente per gli addetti al marketing che operano in un modello di servizio business-to-business. Raccoglie dati da più origini e li combina in un’unica vista di persone e profili di account. Questi dati unificati consentono ai marketer di rivolgersi con precisione a tipi di pubblico specifici e di coinvolgerli in tutti i canali disponibili.
* [Origini](../../../../home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Experience Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza Experience Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

## Navigare nel catalogo delle origini

Nell&#39;interfaccia utente di Platform, seleziona **[!UICONTROL Origini]** dal menu di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Origini]. Puoi selezionare la categoria appropriata dal catalogo sul lato sinistro dello schermo. In alternativa, è possibile trovare l’origine specifica che si desidera utilizzare utilizzando l’opzione di ricerca.

Selezionare **[!DNL Bombora Intent]** nella categoria *[!UICONTROL B2B]*, quindi selezionare **[!UICONTROL Configurazione]**.

>[!TIP]
>
>Le origini nel catalogo delle origini visualizzano l&#39;opzione **[!UICONTROL Configura]** quando un&#39;origine specificata non dispone ancora di un account autenticato. Quando esiste un account autenticato, questa opzione diventa **[!UICONTROL Aggiungi dati]**.



## Usa un account esistente {#existing}

## Crea un nuovo account {#create}

## Fornisci i dettagli del flusso di dati {#provide-dataflow-details}

>[!CONTEXTUALHELP]
>id="platform_sources_bombora_domain"
>title="Origine dominio"
>abstract="Anche se Adobe utilizza il sito web XDM accountOrganization.website, alcuni clienti potrebbero utilizzare campi personalizzati per i rispettivi siti web. Pertanto, devi assicurarti che l’origine del dominio sia il campo dominio/sito web che corrisponderà ai record del tuo account Bombora rispetto agli account Experience Platform."

## Pianifica flusso di dati {#schedule-dataflow}

>[!CONTEXTUALHELP]
>id="platform_sources_bombora_schedule"
>title="Pianificare il flusso di dati"
>abstract="Bombora rilascia i dati una volta alla settimana lunedì mattina alle 17:00 UTC. Pertanto, devi configurare l’ora di inizio dell’acquisizione dopo le 17:00 UTC. Inoltre, è necessario confermare il tempo di acquisizione con Bombora, in quanto potrebbe alterare la loro pianificazione, quando si rilasciano i file in Adobe."


## Verifica flusso di dati {#review-dataflow}
