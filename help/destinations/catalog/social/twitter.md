---
title: Connessione twitter tipi di pubblico personalizzati
description: Effettua il targeting dei tuoi follower e clienti esistenti nel Twitter e crea campagne di remarketing rilevanti attivando i tipi di pubblico incorporati in Adobe Experience Platform
exl-id: fd244e58-cd94-4de7-81e4-c321eb673b65
source-git-commit: ba9b59a24079b61a0f5d6076f3acfd83fc8f4092
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 5%

---

# Connessione [!DNL Twitter Custom Audiences]

## Panoramica {#overview}

Effettua il targeting dei tuoi follower e clienti esistenti nel Twitter e crea campagne di remarketing rilevanti attivando i tipi di pubblico incorporati in Adobe Experience Platform.

## Prerequisiti {#prerequisites}

Prima di configurare la destinazione [!DNL Twitter Custom Audiences], verificare i seguenti prerequisiti di Twitter che è necessario soddisfare.

1. L&#39;account [!DNL Twitter Ads] deve essere idoneo per la pubblicità. I nuovi account di [!DNL Twitter Ads] non sono idonei per la pubblicità nelle prime 2 settimane dopo la creazione.
2. L&#39;account utente di Twitter per il quale hai autorizzato l&#39;accesso in [!DNL Twitter Audience Manager] deve avere l&#39;autorizzazione *[!DNL Partner Audience Manager]* abilitata.

## Identità supportate {#supported-identities}

[!DNL Twitter Custom Audiences] supporta l&#39;attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html#getting-started).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| device_id | ID IDFA/AdID/Android | Google Advertising ID (GAID) e Apple ID per inserzionisti (IDFA) sono supportati in Adobe Experience Platform. Mappa questi spazi dei nomi e/o attributi dallo schema di origine di conseguenza nel [passaggio di mappatura](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) del flusso di lavoro di attivazione della destinazione. |
| e-mail | Indirizzi e-mail per l’utente | Mappa i tuoi indirizzi e-mail in testo normale e gli indirizzi e-mail con hash SHA256 su questo campo. Se il campo di origine contiene attributi senza hash, selezionare l&#39;opzione **[!UICONTROL Applica trasformazione]** per impostare [!DNL Platform] per l&#39;hashing automatico dei dati all&#39;attivazione. Se esegui l’hashing degli indirizzi e-mail dei clienti prima di caricarli in Adobe Experience Platform, tieni presente che l’hashing di queste identità deve essere eseguito utilizzando SHA256, senza sale. |

{style="table-layout:auto"}

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive quali tipi di pubblico puoi esportare in questa destinazione.

| Origine pubblico | Supportato | Descrizione |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Tipi di pubblico generati tramite il servizio di segmentazione [Experience Platform](../../../segmentation/home.md). |
| Caricamenti personalizzati | ✓ | Tipi di pubblico [importati](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform da file CSV. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione pubblico]** | Stai esportando tutti i membri di un pubblico con gli identificatori utilizzati nella destinazione Tipi di pubblico personalizzati del Twitter. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni sulle [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Casi d’uso {#use-cases}

Per capire meglio come e quando utilizzare la destinazione [!DNL Twitter Custom Audiences], ecco alcuni esempi di casi d&#39;uso che i clienti Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### #1 del caso d’uso

Esegui il targeting dei tuoi follower e clienti esistenti nel Twitter e crea campagne di remarketing rilevanti attivando i tipi di pubblico generati in Adobe Experience Platform come [!DNL List Custom Audiences] nel Twitter.

## Connetti alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, sono necessarie le **[!UICONTROL Destinazioni visualizzazione]** e le **[!UICONTROL Autorizzazioni di gestione delle destinazioni]** [per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autenticarsi nella destinazione {#authenticate}

1. Trovare la destinazione [!DNL Twitter Custom Audiences] nel catalogo di destinazione e selezionare **[!UICONTROL Configura]**.
2. Selezionare **[!UICONTROL Connetti alla destinazione]**.
   ![Autentica in LinkedIn](/help/destinations/assets/catalog/social/twitter/authenticate-twitter-destination.png)
3. Immetti le credenziali del Twitter e seleziona **Accedi**.

### Inserire i dettagli della destinazione {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_twitter_accountid"
>title="ID account"
>abstract="ID del tuo account Twitter Ads. Si trova nelle impostazioni di Twitter Ads."

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

* **[!UICONTROL Nome]**: un nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL ID account]**: ID account [!DNL Twitter Ads]. Questo si trova nelle impostazioni di [!DNL Twitter Ads].

>[!IMPORTANT]
>
>Non utilizzare caratteri speciali (+ &amp; , % : ; @ / = ? $ \n) nei nomi di pubblico, descrizione e mappatura del pubblico. Se il nome del pubblico di Experience Platform contiene questi caratteri, rimuovili prima di mappare il pubblico su una destinazione di Twitter.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli per la connessione di destinazione, seleziona **[!UICONTROL Avanti]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Visualizza grafo identità]** [Controllo di accesso](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Leggi [Attivare profili e tipi di pubblico nelle destinazioni di esportazione del pubblico di streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per le istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione.

### Considerazioni sulla mappatura {#mapping-considerations}

Quando mappi i tipi di pubblico al Twitter, fornisci nomi di mappatura del pubblico leggibili dall’utente. È consigliabile utilizzare lo stesso nome utilizzato per i segmenti di Experience Platform.

## Utilizzo dei dati e governance {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, vedi [Panoramica sulla governance dei dati](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=it).

## Risorse aggiuntive {#additional-resources}

Ulteriori informazioni su [!DNL List Custom Audiences] nel Twitter sono disponibili nella [documentazione del Twitter](https://business.twitter.com/en/help/campaign-setup/campaign-targeting/custom-audiences/lists.html).
