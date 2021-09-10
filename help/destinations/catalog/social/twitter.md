---
title: Connessione twitter Custom Audiences
description: Esegui il targeting dei tuoi follower e clienti esistenti in Twitter e crea campagne di ricommercializzazione pertinenti attivando i tuoi tipi di pubblico generati in Adobe Experience Platform
source-git-commit: 3ea3f9ed156ba3a1fbc790153a4b8fa193d5e2da
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 2%

---


# [!DNL Twitter Custom Audiences] connection

## Panoramica {#overview}

Esegui il targeting dei tuoi follower e clienti esistenti in Twitter e crea campagne di ricommercializzazione pertinenti attivando i tuoi tipi di pubblico generati in Adobe Experience Platform.

## Prerequisiti {#prerequisites}

Prima di configurare la destinazione [!DNL Twitter Custom Audiences], verifica i seguenti prerequisiti Twitter che devi soddisfare.

1. Il tuo account [!DNL Twitter Ads] deve essere idoneo per la pubblicità. I nuovi account [!DNL Twitter Ads] non sono idonei per la pubblicità nelle prime due settimane dopo la loro creazione.
2. L&#39;account utente Twitter per il quale hai autorizzato l&#39;accesso in [!DNL Twitter Audience Manager] deve disporre dell&#39;autorizzazione *[!DNL Partner Audience Manager]* abilitata.


## Identità supportate {#supported-identities}

[!DNL Twitter Custom Audiences] supporta l’attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| device_id | IDFA/AdID/Android ID | Google Advertising ID (GAID) e Apple ID per gli inserzionisti (IDFA) sono supportati in Adobe Experience Platform. Mappa di conseguenza questi namespace e/o attributi dallo schema di origine nel [passaggio di mappatura](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) del flusso di lavoro di attivazione della destinazione. |
| e-mail | Indirizzi e-mail per l’utente | Mappa in questo campo gli indirizzi e-mail con hash SHA256 e gli indirizzi e-mail con testo normale. Quando il campo di origine contiene attributi senza hash, seleziona l&#39;opzione **[!UICONTROL Applica trasformazione]** per fare in modo che [!DNL Platform] hash automaticamente i dati all&#39;attivazione. Se invii un hash agli indirizzi e-mail del cliente prima di caricarli su Adobe Experience Platform, tieni presente che queste identità devono essere hashing utilizzando SHA256, senza un sale. |

{style=&quot;table-layout:auto&quot;}

## Tipo di esportazione {#export-type}

**Esportazione segmento** : stai esportando tutti i membri di un segmento (pubblico) con gli identificatori utilizzati nella destinazione Tipi di pubblico personalizzati di Twitter.

## Casi d’uso {#use-cases}

Per comprendere meglio come e quando utilizzare la destinazione [!DNL Twitter Custom Audiences], di seguito sono riportati alcuni esempi di casi d’uso che i clienti Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### Caso d&#39;uso n. 1

Esegui il targeting dei tuoi follower e clienti esistenti in Twitter e crea campagne di ricommercializzazione pertinenti attivando i tuoi tipi di pubblico generati in Adobe Experience Platform as [!DNL List Custom Audiences] in Twitter.

## Connetti alla destinazione {#connect}

Per connetterti a questa destinazione, segui i passaggi descritti nel [tutorial sulla configurazione della destinazione](../../ui/connect-destination.md).

### Parametri di connessione {#parameters}

Durante la [configurazione](../../ui/connect-destination.md) di questa destinazione, è necessario fornire le seguenti informazioni:

* **[!UICONTROL Nome]**: Nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: Una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL ID]** account: Il tuo ID  [!DNL Twitter Ads] account. Questo si trova nelle impostazioni [!DNL Twitter Ads] .

## Attiva i segmenti in questa destinazione {#activate}

Leggi [Attiva profili e segmenti nelle destinazioni di esportazione dei segmenti in streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per istruzioni sull&#39;attivazione dei segmenti di pubblico in questa destinazione.

## Utilizzo e governance dei dati {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] impone la governance dei dati, consulta la [Panoramica sulla governance dei dati](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

## Risorse aggiuntive {#additional-resources}

Quando mappi segmenti di pubblico su Twitter, assicurati di soddisfare i seguenti requisiti di denominazione dei segmenti:

1. Fornisci nomi di mappatura dei segmenti leggibili dall’utente. È consigliabile utilizzare lo stesso nome utilizzato per i segmenti di Experience Platform.
2. Non utilizzare caratteri speciali (+ &amp; , % : ; @ / = ? $) nei nomi di mappatura dei segmenti e dei segmenti. Se il nome del segmento di Experience Platform contiene questi caratteri, rimuovili prima di mappare il segmento a una destinazione Twitter.

Ulteriori informazioni su [!DNL List Custom Audiences] in Twitter sono disponibili nella [documentazione Twitter](https://business.twitter.com/en/help/campaign-setup/campaign-targeting/custom-audiences/lists.html).