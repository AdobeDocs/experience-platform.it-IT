---
keywords: personalizzazione target; destinazione; destinazione experience platform target;destinazione adobe target;
title: Connessione Adobe Target
description: Adobe Target è un’applicazione che fornisce funzionalità di personalizzazione e sperimentazione basate sull’intelligenza artificiale in tempo reale per tutte le interazioni dei clienti in entrata tramite siti web, app mobili e altro ancora.
exl-id: 3e3c405b-8add-4efb-9389-5ad695bc9799
source-git-commit: e5c34ffb9b27ddad0c6523a7279fdf712c84f3ff
workflow-type: tm+mt
source-wordcount: '1555'
ht-degree: 2%

---

# Connessione Adobe Target {#adobe-target-connection}

## Registro modifiche destinazione {#changelog}

| Mese di rilascio | Tipo di aggiornamento | Descrizione |
|---|---|---|
| Aprile 2024 | Aggiornamento della funzionalità e della documentazione | Quando ti connetti alla destinazione Target e utilizzi un ID dello stream di dati, ora *non è necessario* per abilitare necessariamente lo stream di dati per la segmentazione Edge. Ciò significa che la destinazione di Target funzionerà con i tipi di pubblico in batch e in streaming, anche se i casi d’uso che puoi eseguire sono diversi. Visualizzare la tabella in [parametri di connessione](#parameters) per ulteriori informazioni. |
| Gennaio 2024 | Aggiornamento della funzionalità e della documentazione | Ora puoi condividere i tipi di pubblico e gli attributi del profilo con la connessione Adobe Target per la sandbox di produzione predefinita e altre sandbox non predefinite. |
| Giugno 2023 | Aggiornamento della funzionalità e della documentazione | A partire da giugno 2023, quando configuri una nuova connessione di destinazione Adobe Target, puoi selezionare l’area di lavoro di Adobe Target a cui desideri condividere i tipi di pubblico. Consulta la sezione [parametri di connessione](#parameters) per ulteriori informazioni. Inoltre, consulta il tutorial sulla [configurazione delle aree di lavoro](https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html) in Adobe Target per ulteriori informazioni sulle aree di lavoro. |
| Maggio 2023 | Aggiornamento della funzionalità e della documentazione | A partire da maggio 2023, la **[!UICONTROL Adobe Target]** supporto di connessione [personalizzazione basata su attributi](../../ui/activate-edge-personalization-destinations.md#map-attributes) ed è generalmente disponibile per tutti i clienti. |

{style="table-layout:auto"}

## Panoramica {#overview}

Adobe Target è un’applicazione che fornisce funzionalità di personalizzazione e sperimentazione basate sull’intelligenza artificiale in tempo reale per tutte le interazioni dei clienti in entrata tramite siti web, app mobili e altro ancora.

Adobe Target è una connessione di personalizzazione nel catalogo delle destinazioni di Adobe Experience Platform.

## Panoramica video {#video-overview}

Per una breve panoramica su come configurare la connessione Adobe Target in Experienci Platform, guarda il video seguente.

>[!VIDEO](https://video.tv.adobe.com/v/3418799/?quality=12&learn=on)

## Prerequisiti {#prerequisites}

### ID flusso di dati {#datastream-id}

Durante la configurazione della connessione Adobe Target a [utilizzare un ID dello stream di dati](#parameters), è necessario disporre di [Adobe Experience Platform Web SDK](/help/web-sdk/home.md) implementato.

Per configurare la connessione Adobe Target senza utilizzare un ID dello stream di dati non è necessario implementare l’SDK per web.

>[!IMPORTANT]
>
>Prima di creare un’ [!DNL Adobe Target] connessione, leggi la guida su come [configurare le destinazioni di personalizzazione per la personalizzazione della stessa pagina e della pagina successiva](../../ui/activate-edge-personalization-destinations.md). Questa guida descrive i passaggi di configurazione richiesti per i casi di utilizzo di personalizzazione della stessa pagina e della pagina successiva, su più componenti di Experience Platform. Per ottenere casi di utilizzo di personalizzazione della stessa pagina e della pagina successiva, devi utilizzare un ID dello stream di dati durante la configurazione della connessione Adobe Target.

### Prerequisiti in Adobe Target {#prerequisites-in-adobe-target}

In Adobe Target, assicurati che l’utente disponga di:

* Accesso al [area di lavoro predefinita](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html#default-workspace);
* Il **Approvatore** [ruolo](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html#roles-and-permissions).

Ulteriori informazioni sulla concessione di autorizzazioni per [Target Premium](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html#section_8C425E43E5DD4111BBFC734A2B7ABC80) e per [Target Standard](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/users/user-management.html#roles-permissions).

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive quali tipi di pubblico puoi esportare in questa destinazione.

>[!IMPORTANT]
>
>Durante l’attivazione *casi d’uso di tipi di pubblico edge per la personalizzazione della stessa pagina e della pagina successiva*, il pubblico *deve* utilizza un [criterio di unione attivo-su-spigolo](../../../segmentation/ui/segment-builder.md#merge-policies). Il [!DNL active-on-edge] criterio di unione per garantire che i tipi di pubblico vengano valutati costantemente [sul bordo](../../../segmentation/ui/edge-segmentation.md) e sono disponibili per casi di utilizzo di personalizzazione in tempo reale e nella pagina successiva.  Ulteriori informazioni [tutti i casi d’uso disponibili](#parameter), in base al tipo di implementazione.
>Se mappi i tipi di pubblico edge che utilizzano un criterio di unione diverso sulle destinazioni di Adobe Target, tali tipi di pubblico non verranno valutati per i casi d’uso in tempo reale e nella pagina successiva.
>Segui le istruzioni su [creazione di un criterio di unione](../../../profile/merge-policies/ui-guide.md#create-a-merge-policy), e assicurati di abilitare **[!UICONTROL Criterio di unione Attivo su Edge]** attivare/disattivare.


| Origine pubblico | Supportato | Descrizione |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Tipi di pubblico generati dall’Experience Platform [Servizio di segmentazione](../../../segmentation/home.md). |
| Caricamenti personalizzati | X | Tipi di pubblico [importato](../../../segmentation/ui/overview.md#import-audience) in Experienci Platform da file CSV. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
|---------|----------|---------|
| Tipo di esportazione | **[!DNL Profile request]** | Stai richiedendo un singolo profilo a tutti i tipi di pubblico mappati nella destinazione di Adobe Target. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experienci Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni su [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Connetti alla destinazione {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_datastream"
>title="Informazioni sugli ID dello stream di dati"
>abstract="Questa opzione determina in quale flusso di dati di raccolta dati verranno inclusi i tipi di pubblico. Il menu a discesa mostra solo gli stream di dati per i quali è abilitata la configurazione Target. Per utilizzare la segmentazione Edge, devi selezionare un ID dello stream di dati. Selezionando Nessuno vengono disattivati tutti i casi d’uso che utilizzano la segmentazione Edge."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html#parameters" text="Ulteriori informazioni sulla selezione degli stream di dati"

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Visualizza destinazioni]** e **[!UICONTROL Gestire le destinazioni]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md).

Adobe Experience Platform si connette automaticamente all’istanza Adobe Target della tua azienda. Non è richiesta alcuna autenticazione.

### Parametri di connessione {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_workspace"
>title="Informazioni sulle aree di lavoro di Adobe Target"
>abstract="Seleziona l’area di lavoro di Adobe Target in cui verranno condivisi i tipi di pubblico. Puoi selezionare un’unica area di lavoro per ogni connessione Adobe Target. Al momento dell’attivazione, i tipi di pubblico vengono instradati all’area di lavoro selezionata seguendo le etichette di utilizzo dei dati di Experience Platform applicabili."
>additional-url="https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html" text="Ulteriori informazioni sulle aree di lavoro di Adobe Target"

Mentre [configurazione](../../ui/connect-destination.md) in questa destinazione, è necessario fornire le seguenti informazioni:

* **Nome**: inserisci il nome preferito per questa destinazione.
* **Descrizione**: immetti una descrizione per la destinazione. Ad esempio, puoi indicare per quale campagna stai utilizzando questa destinazione. Questo campo è facoltativo.
* **ID flusso di dati**: questo determina in quale flusso di dati di Raccolta dati verranno inclusi i tipi di pubblico. Il menu a discesa mostra solo gli stream di dati in cui sono abilitati i servizi Target e Adobe Experience Platform. Consulta [configurazione di uno stream di dati](../../../datastreams/configure.md#aep) per informazioni dettagliate su come configurare un flusso di dati per Adobe Experience Platform e Adobe Target.

  >[!IMPORTANT]
  >
  >L’ID dello stream di dati è univoco per ogni connessione di destinazione di Adobe Target. Se devi mappare lo stesso pubblico su più flussi di dati, devi [creare una nuova connessione di destinazione](../../ui/connect-destination.md) per ogni ID dello stream di dati e passare attraverso [flusso di attivazione del pubblico](#activate).

   * **[!UICONTROL Nessuno]**: seleziona questa opzione se devi configurare la personalizzazione Adobe Target ma non puoi implementare [Experienci Platform Web SDK](/help/web-sdk/home.md). Quando si utilizza questa opzione, i tipi di pubblico esportati da Experienci Platform a Target supportano solo la personalizzazione della sessione successiva e la segmentazione Edge è disabilitata. Fai riferimento alla tabella seguente per un confronto dei casi d’uso disponibili per tipo di implementazione.

  | Implementazione di Adobe Target *senza* SDK per web | Implementazione di Adobe Target *con* SDK per web | Implementazione di Adobe Target *con* SDK per web *e* segmentazione Edge disattivata |
  |---|---|---|
  | <ul><li>Non è necessario uno stream di dati. Adobe Target può essere implementato tramite [at.js](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/overview.html), [lato server](https://experienceleague.adobe.com/docs/target-dev/developer/overview.html#server-side-implementation), o [ibrido](https://experienceleague.adobe.com/docs/target-dev/developer/overview.html#hybrid-implementation) metodi di implementazione.</li><li>[Segmentazione Edge](../../../segmentation/ui/edge-segmentation.md) non è supportato.</li><li>[Personalizzazione della stessa pagina e della pagina successiva](../../ui/activate-edge-personalization-destinations.md) non sono supportati.</li><li>Puoi condividere i tipi di pubblico e gli attributi del profilo con la connessione Adobe Target per *sandbox di produzione predefinita* e sandbox non predefinite.</li><li>Per configurare la personalizzazione della sessione successiva senza utilizzare un ID dello stream di dati, utilizza [at.js](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/at-js/how-atjs-works.html).</li></ul> | <ul><li>È necessario uno stream di dati con Adobe Target e Experienci Platform configurati come servizi.</li><li>La segmentazione Edge funziona come previsto.</li><li>[Personalizzazione della stessa pagina e della pagina successiva](../../ui/activate-edge-personalization-destinations.md#use-cases) sono supportati.</li><li>È supportata la condivisione di tipi di pubblico e attributi di profilo da altre sandbox.</li></ul> | <ul><li>È necessario uno stream di dati con Adobe Target e Experienci Platform configurati come servizi.</li><li>Quando [configurazione dello stream di dati](/help/destinations/ui/activate-edge-personalization-destinations.md#configure-datastream), non selezionare **Segmentazione Edge** casella di controllo.</li><li>[Personalizzazione della sessione successiva](../../ui/activate-edge-personalization-destinations.md#next-session) è supportato.</li><li>È supportata la condivisione di tipi di pubblico e attributi di profilo da altre sandbox.</li></ul> |

* **Workspace**: seleziona l’Adobe Target [workspace](https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html) a cui verranno condivisi i tipi di pubblico. Puoi selezionare un’unica area di lavoro per ogni connessione Adobe Target. Al momento dell’attivazione, i tipi di pubblico vengono indirizzati all’area di lavoro selezionata seguendo la [Experience Platform di etichette di utilizzo dei dati](../../../data-governance/labels/overview.md).

>[!NOTE]
>
>Quando si utilizza un’area di lavoro di Target personalizzata per [personalizzazione della stessa pagina e della pagina successiva con attributi](../../ui/activate-edge-personalization-destinations.md), solo il [pubblico selezionato](../../ui/activate-edge-personalization-destinations.md#select-audiences) vengono inviati all’area di lavoro di Target selezionata. Il [attributi mappati](../../ui/activate-edge-personalization-destinations.md#mapping) vengono inviati all’area di lavoro di Target predefinita.
><br>
>Questo comportamento cambierà in un aggiornamento futuro.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completate le informazioni sulla connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva il pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Letto [Attivare i tipi di pubblico per Edge Personalization Destinations](../../ui/activate-edge-personalization-destinations.md) per istruzioni sull’attivazione dei tipi di pubblico in questa destinazione.

## Rimuovere tipi di pubblico da una destinazione {#remove}

Sono necessari passaggi aggiuntivi per rimuovere un pubblico da una connessione Adobe Target esistente quando tale pubblico è già utilizzato in un’Adobe Target [attività](https://experienceleague.adobe.com/en/docs/target/using/activities/activities). Se si tenta di rimuovere un pubblico da una connessione Adobe Target, si verifica un errore se il pubblico viene utilizzato da un’attività Adobe Target.

![L’immagine dell’interfaccia utente di Platform mostra un errore causato dal tentativo di rimuovere un pubblico utilizzato da un’attività Target.](../../assets/catalog/personalization/adobe-target-connection/remove-audience-error.png)

Per rimuovere un pubblico da una destinazione Target quando il pubblico viene utilizzato in un’attività, devi innanzitutto rimuovere il pubblico dall’attività Target che lo utilizza oppure eliminare completamente l’attività. Quindi, puoi rimuovere il pubblico dalla connessione Target.

Se il pubblico non viene utilizzato in un’attività, vai a **[!UICONTROL Destinazioni]** > **[!UICONTROL Sfoglia]** > **[!UICONTROL Seleziona flusso di dati di destinazione]** > **[!UICONTROL Dati di attivazione]**, seleziona il pubblico da rimuovere, quindi fai clic su **[!UICONTROL Rimuovi tipi di pubblico]**.

## Dati esportati {#exported-data}

Adobe Target *legge* dati di profilo dall’Edge Network di Adobe Experience Platform, in modo che non vengano esportati dati.

## Utilizzo dei dati e governance {#data-usage-governance}

Tutti [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, leggi [Panoramica sulla governance dei dati](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=it).
