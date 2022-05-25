---
keywords: personalizzazione mirata; destinazione; destinazione target experience platform;destinazione adobe target;
title: Connessione Adobe Target
description: Adobe Target è un’applicazione che fornisce funzionalità di personalizzazione e sperimentazione basate sull’intelligenza artificiale in tempo reale in tutte le interazioni dei clienti in entrata tra siti web, app mobili e altro ancora.
exl-id: 3e3c405b-8add-4efb-9389-5ad695bc9799
source-git-commit: 0868d81bcd1968b3223c79abb5a7bb8f279a4130
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 1%

---

# Connessione Adobe Target {#adobe-target-connection}

## Panoramica {#overview}

Adobe Target è un’applicazione che fornisce funzionalità di personalizzazione e sperimentazione basate sull’intelligenza artificiale in tempo reale in tutte le interazioni dei clienti in entrata tra siti web, app mobili e altro ancora.

Adobe Target è una connessione di personalizzazione in Adobe Experience Platform.

## Prerequisiti {#prerequisites}

Durante la configurazione della connessione Adobe Target a [utilizzare un ID datastream](#parameters), è necessario disporre del [Adobe Experience Platform Web SDK](../../../edge/home.md) implementato.

La configurazione della connessione Adobe Target senza l’utilizzo di un ID datastream non richiede l’implementazione dell’SDK web.

>[!IMPORTANT]
>
>Prima di creare un [!DNL Adobe Target] connessione, leggere la guida su come [configurare le destinazioni di personalizzazione per la personalizzazione della stessa pagina e della pagina successiva](../../ui/configure-personalization-destinations.md). Questa guida descrive i passaggi di configurazione richiesti per i casi d’uso di personalizzazione della stessa pagina e della pagina successiva, su più componenti di Experience Platform. Per la personalizzazione della stessa pagina e della pagina successiva è necessario utilizzare un ID di archivio dati per configurare la connessione Adobe Target.

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, fare riferimento alla tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!DNL Profile request]** | Stai richiedendo tutti i segmenti mappati nella destinazione Adobe Target per un singolo profilo. |
| Frequenza delle esportazioni | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni basate su API &quot;sempre attive&quot;. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del segmento, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Casi d’uso {#use-cases}

**Personalizzazione di un banner della home page**

Una società di noleggio e vendita di casa vuole personalizzare la propria home page con un banner, in base alle qualifiche del segmento di clienti in Adobe Experience Platform. L’azienda può selezionare i tipi di pubblico che devono ottenere un’esperienza personalizzata e inviarli ad Adobe Target come criteri di targeting per la loro offerta Target.

## Collegati alla destinazione {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_datastream"
>title="Informazioni sugli ID di datastream"
>abstract="Questa opzione determina in quale datastream di raccolta dati verranno inclusi i segmenti. Il menu a discesa mostra solo i datastreams con la configurazione di Target abilitata. Per utilizzare la segmentazione Edge, è necessario selezionare un ID datastream. Selezionando Nessuno vengono disattivati tutti i casi d’uso che utilizzano la segmentazione dei bordi."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html#parameters" text="Ulteriori informazioni sulla selezione dei datastreams."

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Per connettersi a questa destinazione, segui i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md).

Adobe Experience Platform si connette automaticamente all’istanza Adobe Target della tua azienda. Non è richiesta alcuna autenticazione.

### Parametri di connessione {#parameters}

Quando [configurazione](../../ui/connect-destination.md) questa destinazione, devi fornire le seguenti informazioni:

* **Nome**: Compila il nome preferito per questa destinazione.
* **Descrizione**: Inserisci una descrizione per la destinazione. Ad esempio, è possibile indicare per quale campagna si utilizza questa destinazione. Questo campo è facoltativo.
* **ID Datastream**: Questo determina in quale datastream di raccolta dati i segmenti saranno inclusi. Il menu a discesa mostra solo i datastreams con la destinazione Target abilitata. Vedi [configurazione di un datastream](../../../edge/datastreams/overview.md#target) per informazioni dettagliate su come configurare un datastream per Adobe Target.
   * **[!UICONTROL Nessuno]**: Seleziona questa opzione se hai bisogno di configurare la personalizzazione Adobe Target ma non puoi implementare il [Experience Platform Web SDK](../../../edge/home.md). Quando utilizzi questa opzione, i segmenti esportati da Experience Platform a Target supportano solo la personalizzazione a sessione successiva e la segmentazione edge viene disabilitata. Per ulteriori informazioni, consulta la tabella seguente.

| Nessun datastream selezionato | Datastream selezionato |
|---|---|
| <ul><li>[Segmentazione degli spigoli](../../../segmentation/ui/edge-segmentation.md) non è supportato.</li><li>[Personalizzazione a pagina singola e successiva](../../ui/configure-personalization-destinations.md) non sono supportati.</li><li>Puoi condividere i segmenti alla connessione Adobe Target solo per la sandbox di produzione.</li><li>Per configurare la personalizzazione di sessione successiva senza utilizzare un ID di datastream, utilizza [at.js](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/at-js/how-atjs-works.html?lang=en).</li></ul> | <ul><li>La segmentazione dei bordi funziona come previsto.</li><li>[Personalizzazione a pagina singola e successiva](../../ui/configure-personalization-destinations.md) sono supportati.</li><li>La condivisione dei segmenti è supportata per altre sandbox.</li></ul> |

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizzare i segmenti]** [autorizzazioni di controllo accessi](/help/access-control/home.md#permissions). Leggi la sezione [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni richieste.

Leggi [Attivare profili e segmenti nelle destinazioni di richieste di profilo](../../ui/activate-profile-request-destinations.md) per istruzioni su come attivare i segmenti di pubblico a questa destinazione.

## Dati esportati {#exported-data}

Adobe Target legge i dati del profilo da Adobe Experience Platform Edge Network, quindi non vengono esportati dati.

## Utilizzo e governance dei dati {#data-usage-governance}

Tutto [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] impone la governance dei dati, leggi [Panoramica sulla governance dei dati](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).
