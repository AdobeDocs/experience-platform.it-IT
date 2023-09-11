---
title: Connessione twitter tipi di pubblico personalizzati
description: Effettua il targeting dei tuoi follower e clienti esistenti nel Twitter e crea campagne di remarketing rilevanti attivando i tipi di pubblico incorporati in Adobe Experience Platform
exl-id: fd244e58-cd94-4de7-81e4-c321eb673b65
source-git-commit: 72225ac673ed921b5857a14070660134949e7e3e
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 4%

---

# Connessione [!DNL Twitter Custom Audiences]

## Panoramica {#overview}

Effettua il targeting dei tuoi follower e clienti esistenti nel Twitter e crea campagne di remarketing rilevanti attivando i tipi di pubblico incorporati in Adobe Experience Platform.

## Prerequisiti {#prerequisites}

Prima di configurare [!DNL Twitter Custom Audiences] destinazione, assicurati di rivedere i seguenti prerequisiti di Twitter che devi soddisfare.

1. Il tuo [!DNL Twitter Ads] l&#39;account deve essere idoneo per la pubblicità. Nuovo [!DNL Twitter Ads] gli account non sono idonei per la pubblicità nelle prime 2 settimane dopo la loro creazione.
2. L’account utente di Twitter per il quale hai autorizzato l’accesso in [!DNL Twitter Audience Manager] deve avere *[!DNL Partner Audience Manager]* autorizzazione abilitata.

## Identità supportate {#supported-identities}

[!DNL Twitter Custom Audiences] supporta l’attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| device_id | ID IDFA/AdID/Android | Google Advertising ID (GAID) e Apple ID per inserzionisti (IDFA) sono supportati in Adobe Experience Platform. Mappa questi spazi dei nomi e/o attributi dallo schema di origine di conseguenza nel [passaggio di mappatura](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) del flusso di lavoro di attivazione della destinazione. |
| e-mail | Indirizzi e-mail per l’utente | Mappa i tuoi indirizzi e-mail in testo normale e gli indirizzi e-mail con hash SHA256 su questo campo. Quando il campo sorgente contiene attributi senza hash, seleziona la **[!UICONTROL Applica trasformazione]** opzione, per avere [!DNL Platform] esegui automaticamente l’hash dei dati all’attivazione. Se esegui l’hashing degli indirizzi e-mail dei clienti prima di caricarli in Adobe Experience Platform, tieni presente che l’hashing di queste identità deve essere eseguito utilizzando SHA256, senza sale. |

{style="table-layout:auto"}

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive il tipo di pubblico che puoi esportare in questa destinazione.

| Origine pubblico | Supportati | Descrizione |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Tipi di pubblico generati dall’Experience Platform [Servizio di segmentazione](../../../segmentation/home.md). |
| Caricamenti personalizzati | ✓ | Tipi di pubblico [importato](../../../segmentation/ui/overview.md#import-audience) in Experienci Platform da file CSV. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione pubblico]** | Stai esportando tutti i membri di un pubblico con gli identificatori utilizzati nella destinazione Tipi di pubblico personalizzati del Twitter. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experienci Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni su [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Casi di utilizzo {#use-cases}

Per aiutarti a capire meglio come e quando utilizzare il [!DNL Twitter Custom Audiences] destinazione: di seguito sono riportati alcuni casi di utilizzo esemplificativi che i clienti di Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### #1 del caso d’uso

Effettua il targeting dei tuoi follower e clienti esistenti nel Twitter e crea campagne di remarketing rilevanti attivando i tipi di pubblico incorporati in Adobe Experience Platform come [!DNL List Custom Audiences] nel Twitter.

## Connetti alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autentica nella destinazione {#authenticate}

1. Trova il [!DNL Twitter Custom Audiences] nel catalogo di destinazione e seleziona **[!UICONTROL Configurazione]**.
2. Seleziona **[!UICONTROL Connetti alla destinazione]**.
   ![Autentica in LinkedIn](/help/destinations/assets/catalog/social/twitter/authenticate-twitter-destination.png)
3. Immetti le credenziali del Twitter e seleziona **Accedi**.

### Inserisci i dettagli della destinazione {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_twitter_accountid"
>title="ID account"
>abstract="ID del tuo account Twitter Ads. Si trova nelle impostazioni di Twitter Ads."

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

* **[!UICONTROL Nome]**: nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL ID account]**: il tuo [!DNL Twitter Ads] ID account. Questo si trova nel tuo [!DNL Twitter Ads] impostazioni.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completate le informazioni sulla connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva il pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Letto [Attiva profili e tipi di pubblico nelle destinazioni di esportazione del pubblico in streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per istruzioni sull’attivazione dei tipi di pubblico in questa destinazione.

## Utilizzo dei dati e governance {#data-usage-governance}

Tutti [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, consulta la sezione [Panoramica sulla governance dei dati](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=it).

## Risorse aggiuntive {#additional-resources}

Quando mappi il pubblico al Twitter, assicurati di soddisfare i seguenti requisiti di denominazione del pubblico:

1. Fornisci nomi di mappatura del pubblico leggibili dall’utente. È consigliabile utilizzare lo stesso nome utilizzato per i segmenti di Experience Platform.
2. Non utilizzare caratteri speciali (+ &amp; , % : ; @ / = ? $) nei nomi di mappatura del pubblico e del pubblico. Se il nome del pubblico di Experience Platform contiene questi caratteri, rimuovili prima di mappare il pubblico su una destinazione di Twitter.

Ulteriori informazioni su [!DNL List Custom Audiences] nel Twitter è disponibile nella sezione [Documentazione del twitter](https://business.twitter.com/en/help/campaign-setup/campaign-targeting/custom-audiences/lists.html).
