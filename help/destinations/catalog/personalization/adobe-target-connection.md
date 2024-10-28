---
keywords: personalizzazione target; destinazione; destinazione experience platform target;destinazione adobe target;
title: Connessione Adobe Target
description: Adobe Target è un’applicazione che fornisce funzionalità di personalizzazione e sperimentazione basate sull’intelligenza artificiale in tempo reale per tutte le interazioni dei clienti in entrata tramite siti web, app mobili e altro ancora.
exl-id: 3e3c405b-8add-4efb-9389-5ad695bc9799
source-git-commit: dae0cb108c62b078d0c7dd5bec466091d4937c53
workflow-type: tm+mt
source-wordcount: '1768'
ht-degree: 9%

---

# Connessione Adobe Target {#adobe-target-connection}

## Registro modifiche destinazione {#changelog}

| Mese di rilascio | Tipo di aggiornamento | Descrizione |
|---|---|---|
| Aprile 2024 | Aggiornamento della funzionalità e della documentazione | Quando ti connetti alla destinazione di Target e utilizzi un ID di flusso di dati, ora *non hai bisogno* di abilitare necessariamente lo stream di dati per la segmentazione Edge. Ciò significa che la destinazione di Target funzionerà con i tipi di pubblico in batch e in streaming, anche se i casi d’uso che puoi eseguire sono diversi. Per ulteriori informazioni, vedere la tabella nella sezione [parametri di connessione](#parameters). |
| Gennaio 2024 | Aggiornamento della funzionalità e della documentazione | Ora puoi condividere i tipi di pubblico e gli attributi del profilo con la connessione Adobe Target per la sandbox di produzione predefinita e altre sandbox non predefinite. |
| Giugno 2023 | Aggiornamento della funzionalità e della documentazione | A partire da giugno 2023, quando configuri una nuova connessione di destinazione Adobe Target, puoi selezionare l’area di lavoro di Adobe Target a cui desideri condividere i tipi di pubblico. Consulta la sezione [parametri di connessione](#parameters) per ulteriori informazioni. Inoltre, consulta il tutorial sulla [configurazione delle aree di lavoro](https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html?lang=it) in Adobe Target per ulteriori informazioni sulle aree di lavoro. |
| Maggio 2023 | Aggiornamento della funzionalità e della documentazione | A maggio 2023, la connessione **[!UICONTROL Adobe Target]** supporta la [personalizzazione basata su attributi](../../ui/activate-edge-personalization-destinations.md#map-attributes) ed è generalmente disponibile per tutti i clienti. |

{style="table-layout:auto"}

## Panoramica {#overview}

Adobe Target è un’applicazione che fornisce funzionalità di personalizzazione e sperimentazione basate sull’intelligenza artificiale in tempo reale per tutte le interazioni dei clienti in entrata tramite siti web, app mobili e altro ancora.

Adobe Target è una connessione di personalizzazione nel catalogo delle destinazioni di Adobe Experience Platform.

## Panoramica video {#video-overview}

Per una breve panoramica su come configurare la connessione Adobe Target in Experience Platform, guarda il video seguente.

>[!VIDEO](https://video.tv.adobe.com/v/3418799/?quality=12&learn=on)

## Casi d’uso supportati in base al tipo di implementazione {#supported-use-cases}

La tabella seguente mostra i casi d&#39;uso supportati per la destinazione Adobe Target, in base al tipo di implementazione, con o senza [Web SDK](/help/web-sdk/home.md) e con o senza [segmentazione Edge](/help/segmentation/home.md#edge) abilitata.

| Implementazione di Adobe Target *senza* Web SDK | Implementazione di Adobe Target *con* Web SDK | Implementazione di Adobe Target *con* Web SDK *e* segmentazione Edge disattivata |
|---|---|---|
| <ul><li>Non è necessario uno stream di dati. Adobe Target può essere distribuito tramite i metodi di implementazione [at.js](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/overview.html), [lato server](https://experienceleague.adobe.com/docs/target-dev/developer/overview.html#server-side-implementation) o [ibrido](https://experienceleague.adobe.com/docs/target-dev/developer/overview.html#hybrid-implementation).</li><li>[Segmentazione Edge](../../../segmentation/ui/edge-segmentation.md) non supportata.</li><li>[La personalizzazione della stessa pagina e della pagina successiva](../../ui/activate-edge-personalization-destinations.md) non è supportata.</li><li>Puoi condividere i tipi di pubblico e gli attributi del profilo con la connessione Adobe Target per la *sandbox di produzione predefinita* e per le sandbox non predefinite.</li><li>Per configurare la personalizzazione della sessione successiva senza utilizzare un ID dello stream di dati, utilizza [at.js](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/at-js/how-atjs-works.html).</li></ul> | <ul><li>È necessario uno stream di dati con Adobe Target e Experience Platform configurati come servizi.</li><li>La segmentazione di Edge funziona come previsto.</li><li>[Sono supportate la personalizzazione della stessa pagina e della pagina successiva](../../ui/activate-edge-personalization-destinations.md#use-cases).</li><li>È supportata la condivisione di tipi di pubblico e attributi di profilo da altre sandbox.</li></ul> | <ul><li>È necessario uno stream di dati con Adobe Target e Experience Platform configurati come servizi.</li><li>Durante la [configurazione dello stream di dati](/help/destinations/ui/activate-edge-personalization-destinations.md#configure-datastream), non selezionare la casella di controllo **Segmentazione Edge**.</li><li>[È supportata la personalizzazione della sessione successiva](../../ui/activate-edge-personalization-destinations.md#next-session).</li><li>È supportata la condivisione di tipi di pubblico e attributi di profilo da altre sandbox.</li></ul> |


## Prerequisiti {#prerequisites}

### ID flusso di dati {#datastream-id}

Durante la configurazione della connessione Adobe Target a [utilizzare un ID dello stream di dati](#parameters), è necessario che sia implementato [Adobe Experience Platform Web SDK](/help/web-sdk/home.md).

Per configurare la connessione Adobe Target senza utilizzare un ID dello stream di dati non è necessario implementare l’SDK per web.

>[!IMPORTANT]
>
>Prima di creare una connessione [!DNL Adobe Target], leggere la guida su come [configurare le destinazioni di personalizzazione per la personalizzazione della stessa pagina e della pagina successiva](../../ui/activate-edge-personalization-destinations.md). Questa guida descrive i passaggi di configurazione richiesti per i casi di utilizzo di personalizzazione della stessa pagina e della pagina successiva, su più componenti di Experience Platform. Per ottenere casi di utilizzo di personalizzazione della stessa pagina e della pagina successiva, devi utilizzare un ID dello stream di dati durante la configurazione della connessione Adobe Target.

### Prerequisiti in Adobe Target {#prerequisites-in-adobe-target}

In Adobe Target, assicurati che l’utente disponga di:

* Accesso all&#39;[area di lavoro predefinita](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html#default-workspace);
* L&#39;**Approvatore** [mansione](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html#roles-and-permissions).

Ulteriori informazioni sulla concessione delle autorizzazioni per [Target Premium](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html#section_8C425E43E5DD4111BBFC734A2B7ABC80) e per [Target Standard](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/users/user-management.html#roles-permissions).

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive quali tipi di pubblico puoi esportare in questa destinazione.

>[!IMPORTANT]
>
>Quando si attivano *tipi di pubblico edge per casi di utilizzo di personalizzazione della stessa pagina e della pagina successiva*, i tipi di pubblico *devono* utilizzare un [criterio di unione attivo-su-edge](../../../segmentation/ui/segment-builder.md#merge-policies). Il criterio di unione [!DNL active-on-edge] garantisce che i tipi di pubblico vengano valutati costantemente [al limite](../../../segmentation/ui/edge-segmentation.md) e siano disponibili per i casi di utilizzo di personalizzazione in tempo reale e nella pagina successiva.  Leggi di [tutti i casi d&#39;uso disponibili](#parameters), in base al tipo di implementazione.
>Se mappi i tipi di pubblico edge che utilizzano un criterio di unione diverso sulle destinazioni di Adobe Target, tali tipi di pubblico non verranno valutati per i casi d’uso in tempo reale e nella pagina successiva.
>Segui le istruzioni relative alla [creazione di un criterio di unione](../../../profile/merge-policies/ui-guide.md#create-a-merge-policy) e assicurati di attivare/disattivare il criterio di unione **[!UICONTROL Attivo su Edge]**.


| Origine pubblico | Supportato | Descrizione |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Tipi di pubblico generati tramite il servizio di segmentazione [Experience Platform](../../../segmentation/home.md). |
| Caricamenti personalizzati | X | Tipi di pubblico [importati](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform da file CSV. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
|---------|----------|---------|
| Tipo di esportazione | **[!DNL Profile request]** | Stai richiedendo un singolo profilo a tutti i tipi di pubblico mappati nella destinazione di Adobe Target. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni sulle [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Connettersi alla destinazione {#connect}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_datastream"
>title="Informazioni sugli ID di stream di dati"
>abstract="Questa opzione determina in quale stream di dati di raccolta dati verranno inclusi i tipi di pubblico. Il menu a discesa mostra solo gli stream di dati in cui la configurazione Destinazione è abilitata. Per utilizzare la segmentazione Edge, devi selezionare un ID di stream di dati. Se selezioni Nessuno, tutti i casi d’uso che utilizzano la segmentazione Edge vengono disabilitati."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/personalization/adobe-target-connection.html?lang=it#parameters" text="Ulteriori informazioni sulla selezione degli stream di dati"

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, sono necessarie le **[!UICONTROL Destinazioni visualizzazione]** e le **[!UICONTROL Autorizzazioni di gestione delle destinazioni]** [per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md).

Adobe Experience Platform si connette automaticamente all’istanza Adobe Target della tua azienda. Non è richiesta alcuna autenticazione.

### Parametri di connessione {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_target_workspace"
>title="Informazioni sulle aree di lavoro di Adobe Target"
>abstract="Seleziona l’area di lavoro di Adobe Target in cui verranno condivisi i tipi di pubblico. Puoi selezionare un’unica area di lavoro per ogni connessione ad Adobe Target. Al momento dell’attivazione, i tipi di pubblico vengono indirizzati all’area di lavoro selezionata seguendo le etichette di utilizzo dei dati di Experience Platform applicabili."
>additional-url="https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html?lang=it" text="Ulteriori informazioni sulle aree di lavoro di Adobe Target"

Durante la [configurazione](../../ui/connect-destination.md) di questa destinazione, è necessario fornire le seguenti informazioni:

* **Nome**: immettere il nome preferito per la destinazione.
* **Descrizione**: immetti una descrizione per la destinazione. Ad esempio, puoi indicare per quale campagna stai utilizzando questa destinazione. Questo campo è facoltativo.
* **ID flusso di dati**: determina in quale flusso di dati della raccolta dati verranno inclusi i tipi di pubblico. Il menu a discesa mostra solo gli stream di dati in cui sono abilitati i servizi Target e Adobe Experience Platform. Consulta [configurazione di uno stream di dati](../../../datastreams/configure.md#aep) per informazioni dettagliate su come configurare uno stream di dati per Adobe Experience Platform e Adobe Target.

  >[!IMPORTANT]
  >
  >L’ID dello stream di dati è univoco per ogni connessione di destinazione di Adobe Target. Non puoi utilizzare lo stesso ID dello stream di dati per più connessioni di destinazione Adobe Target.
  >Se devi mappare gli stessi tipi di pubblico su più flussi di dati, devi [creare una nuova connessione di destinazione](../../ui/connect-destination.md) per ogni ID dello stream di dati e passare attraverso il [flusso di attivazione del pubblico](#activate).

   * **[!UICONTROL Nessuno]**: selezionare questa opzione se è necessario configurare la personalizzazione Adobe Target ma non è possibile implementare [Experience Platform Web SDK](/help/web-sdk/home.md). Quando si utilizza questa opzione, i tipi di pubblico esportati da Experience Platform a Target supportano solo la personalizzazione della sessione successiva e la segmentazione Edge è disabilitata. Fai riferimento alla tabella nella sezione [casi d&#39;uso supportati](#supported-use-cases) per un confronto dei casi d&#39;uso disponibili per tipo di implementazione.

  | Implementazione di Adobe Target *senza* Web SDK | Implementazione di Adobe Target *con* Web SDK | Implementazione di Adobe Target *con* Web SDK *e* segmentazione Edge disattivata |
  |---|---|---|
  | <ul><li>Non è necessario uno stream di dati. Adobe Target può essere distribuito tramite i metodi di implementazione [at.js](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/overview.html), [lato server](https://experienceleague.adobe.com/docs/target-dev/developer/overview.html#server-side-implementation) o [ibrido](https://experienceleague.adobe.com/docs/target-dev/developer/overview.html#hybrid-implementation).</li><li>[Segmentazione Edge](../../../segmentation/ui/edge-segmentation.md) non supportata.</li><li>[La personalizzazione della stessa pagina e della pagina successiva](../../ui/activate-edge-personalization-destinations.md) non è supportata.</li><li>Puoi condividere i tipi di pubblico e gli attributi del profilo con la connessione Adobe Target per la *sandbox di produzione predefinita* e per le sandbox non predefinite.</li><li>Per configurare la personalizzazione della sessione successiva senza utilizzare un ID dello stream di dati, utilizza [at.js](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/at-js/how-atjs-works.html).</li></ul> | <ul><li>È necessario uno stream di dati con Adobe Target e Experience Platform configurati come servizi.</li><li>La segmentazione di Edge funziona come previsto.</li><li>[Sono supportate la personalizzazione della stessa pagina e della pagina successiva](../../ui/activate-edge-personalization-destinations.md#use-cases).</li><li>È supportata la condivisione di tipi di pubblico e attributi di profilo da altre sandbox.</li></ul> | <ul><li>È necessario uno stream di dati con Adobe Target e Experience Platform configurati come servizi.</li><li>Durante la [configurazione dello stream di dati](/help/destinations/ui/activate-edge-personalization-destinations.md#configure-datastream), non selezionare la casella di controllo **Segmentazione Edge**.</li><li>[È supportata la personalizzazione della sessione successiva](../../ui/activate-edge-personalization-destinations.md#next-session).</li><li>È supportata la condivisione di tipi di pubblico e attributi di profilo da altre sandbox.</li></ul> |

* **Workspace**: seleziona l&#39;area di lavoro [area di lavoro](https://experienceleague.adobe.com/docs/target-learn/tutorials/administration/set-up-workspaces.html?lang=it) di Adobe Target in cui verranno condivisi i tipi di pubblico. Puoi selezionare un’unica area di lavoro per ogni connessione ad Adobe Target. Al momento dell&#39;attivazione, i tipi di pubblico vengono instradati all&#39;area di lavoro selezionata seguendo le [etichette di utilizzo dei dati di Experience Platform](../../../data-governance/labels/overview.md) applicabili.

>[!NOTE]
>
>Quando si utilizza un&#39;area di lavoro di Target personalizzata per [la personalizzazione della stessa pagina e della pagina successiva con attributi](../../ui/activate-edge-personalization-destinations.md), solo i [tipi di pubblico selezionati](../../ui/activate-edge-personalization-destinations.md#select-audiences) vengono inviati all&#39;area di lavoro di Target selezionata. I [attributi mappati](../../ui/activate-edge-personalization-destinations.md#mapping) vengono inviati all&#39;area di lavoro predefinita di Target.
><br>
>Questo comportamento cambierà in un aggiornamento futuro.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli per la connessione di destinazione, seleziona **[!UICONTROL Avanti]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Leggi [Attiva tipi di pubblico nelle destinazioni di personalizzazione Edge](../../ui/activate-edge-personalization-destinations.md) per le istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione.

## Rimuovere tipi di pubblico da una destinazione {#remove}

Sono necessari passaggi aggiuntivi per rimuovere un pubblico da una connessione Adobe Target esistente quando tale pubblico è già utilizzato in una [attività](https://experienceleague.adobe.com/en/docs/target/using/activities/activities) di Adobe Target. Se si tenta di rimuovere un pubblico da una connessione Adobe Target, si verifica un errore se il pubblico viene utilizzato da un’attività Adobe Target.

![Immagine dell&#39;interfaccia utente di Platform che mostra un errore causato dal tentativo di rimuovere un pubblico utilizzato da un&#39;attività di Target.](../../assets/catalog/personalization/adobe-target-connection/remove-audience-error.png)

Per rimuovere un pubblico da una destinazione Target quando il pubblico viene utilizzato in un’attività, devi innanzitutto rimuovere il pubblico dall’attività Target che lo utilizza oppure eliminare completamente l’attività. Quindi, puoi rimuovere il pubblico dalla connessione Target.

Se il pubblico non viene utilizzato in un&#39;attività, passa a **[!UICONTROL Destinazioni]** > **[!UICONTROL Sfoglia]** > **[!UICONTROL Seleziona flusso di dati di destinazione]** > **[!UICONTROL Dati di attivazione]**, seleziona il pubblico da rimuovere, quindi seleziona **[!UICONTROL Rimuovi tipi di pubblico]**.

## Dati esportati {#exported-data}

Adobe Target *legge* i dati del profilo dall&#39;Edge Network di Adobe Experience Platform, quindi non viene esportato alcun dato.

## Utilizzo dei dati e governance {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, leggere la [Panoramica sulla governance dei dati](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=it).
