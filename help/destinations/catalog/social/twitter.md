---
title: Connessione twitter Custom Audiences
description: Esegui il targeting dei tuoi follower e clienti esistenti in Twitter e crea campagne di ricommercializzazione pertinenti attivando i tuoi tipi di pubblico generati in Adobe Experience Platform
exl-id: fd244e58-cd94-4de7-81e4-c321eb673b65
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '812'
ht-degree: 3%

---

# [!DNL Twitter Custom Audiences] connection

## Panoramica {#overview}

Esegui il targeting dei tuoi follower e clienti esistenti in Twitter e crea campagne di ricommercializzazione pertinenti attivando i tuoi tipi di pubblico generati in Adobe Experience Platform.

## Prerequisiti {#prerequisites}

Prima di configurare il [!DNL Twitter Custom Audiences] controlla i seguenti prerequisiti Twitter da soddisfare.

1. Le [!DNL Twitter Ads] l&#39;account deve essere idoneo per la pubblicità. Nuovo [!DNL Twitter Ads] gli account non sono ammessi alla pubblicità nelle prime due settimane dalla loro creazione.
2. Il tuo account utente Twitter per il quale hai autorizzato l&#39;accesso in [!DNL Twitter Audience Manager] devono avere *[!DNL Partner Audience Manager]* autorizzazione abilitata.

## Identità supportate {#supported-identities}

[!DNL Twitter Custom Audiences] supporta l’attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni [identità](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| device_id | IDFA/AdID/Android ID | Google Advertising ID (GAID) e Apple ID per gli inserzionisti (IDFA) sono supportati in Adobe Experience Platform. Mappa di conseguenza questi namespace e/o attributi dallo schema di origine nel [fase di mappatura](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) del flusso di lavoro di attivazione della destinazione. |
| e-mail | Indirizzi e-mail per l’utente | Mappa in questo campo gli indirizzi e-mail con hash SHA256 e gli indirizzi e-mail con testo normale. Quando il campo di origine contiene attributi senza hash, seleziona la **[!UICONTROL Applica trasformazione]** opzione, per avere [!DNL Platform] hash automaticamente i dati all’attivazione. Se invii un hash agli indirizzi e-mail del cliente prima di caricarli su Adobe Experience Platform, tieni presente che queste identità devono essere hashing utilizzando SHA256, senza un sale. |

{style=&quot;table-layout:auto&quot;}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, fare riferimento alla tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione del segmento]** | Stai esportando tutti i membri di un segmento (pubblico) con gli identificatori utilizzati nella destinazione Pubblico personalizzato di Twitter. |
| Frequenza delle esportazioni | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni basate su API &quot;sempre attive&quot;. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del segmento, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Casi di utilizzo {#use-cases}

Per aiutarti a capire meglio come e quando utilizzare la [!DNL Twitter Custom Audiences] destinazione : di seguito sono riportati alcuni esempi di casi d’uso che i clienti Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### Caso d&#39;uso n. 1

Esegui il targeting dei tuoi follower e clienti esistenti in Twitter e crea campagne di ricommercializzazione pertinenti attivando i tuoi tipi di pubblico generati in Adobe Experience Platform as [!DNL List Custom Audiences] in Twitter.

## Connetti alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Per connettersi a questa destinazione, segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione , compila i campi elencati nelle due sezioni seguenti.

### Autentica a destinazione {#authenticate}

1. Trova il [!DNL Twitter Custom Audiences] destinazione nel catalogo di destinazione e selezionare **[!UICONTROL Configurazione]**.
2. Seleziona **[!UICONTROL Connetti alla destinazione]**.
   ![Autenticazione in LinkedIn](/help/destinations/assets/catalog/social/twitter/authenticate-twitter-destination.png)
3. Immetti le tue credenziali Twitter e seleziona **Accesso**.

### Compila i dettagli della destinazione {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_twitter_accountid"
>title="ID account"
>abstract="Il tuo ID account Twitter Ads. Questo si trova nelle impostazioni di Twitter Ads."

Per configurare i dettagli della destinazione, compila i campi obbligatori e facoltativi riportati di seguito. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

* **[!UICONTROL Nome]**: Nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: Una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL ID account]**: Le [!DNL Twitter Ads] ID account. Questo si trova nella [!DNL Twitter Ads] impostazioni.

### Abilitare gli avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati nella tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere le notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [iscrizione agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completati i dettagli della connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizzare i segmenti]** [autorizzazioni di controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Leggi [Attivare profili e segmenti nelle destinazioni di esportazione dei segmenti in streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per istruzioni su come attivare i segmenti di pubblico a questa destinazione.

## Utilizzo e governance dei dati {#data-usage-governance}

Tutto [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, vedi [Panoramica sulla governance dei dati](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=it).

## Risorse aggiuntive {#additional-resources}

Quando mappi segmenti di pubblico su Twitter, assicurati di soddisfare i seguenti requisiti di denominazione dei segmenti:

1. Fornisci nomi di mappatura dei segmenti leggibili dall’utente. È consigliabile utilizzare lo stesso nome utilizzato per i segmenti di Experience Platform.
2. Non utilizzare caratteri speciali (+ &amp; , % : ; @ / = ? $) nei nomi di mappatura dei segmenti e dei segmenti. Se il nome del segmento di Experience Platform contiene questi caratteri, rimuovili prima di mappare il segmento a una destinazione Twitter.

Ulteriori informazioni [!DNL List Custom Audiences] in Twitter si trova nella [Documentazione di twitter](https://business.twitter.com/en/help/campaign-setup/campaign-targeting/custom-audiences/lists.html).
