---
title: Connettere L’Intento Di Demandbase Ad Experience Platform Tramite L’Interfaccia Utente
description: Scopri come collegare Demandbase Intent ad Experience Platform
badgeB2B: label="B2B edition" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=it#rtcdp-editions newtab=true"
badgeB2P: label="Edizione B2P" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=it#rtcdp-editions newtab=true"
exl-id: 7dc87067-cdf6-4dde-b077-19666dcb12e2
source-git-commit: a1af85c6b76cc7bded07ab4acaec9c3213a94397
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 4%

---

# Connetti [!DNL Demandbase Intent] ad Experience Platform tramite l&#39;interfaccia utente

Leggere questa guida per scoprire come collegare l&#39;account [!DNL Demandbase Intent] a Adobe Experience Platform utilizzando l&#39;interfaccia utente.

## Introduzione

Questo tutorial richiede una buona conoscenza dei seguenti componenti di Experience Platform:

* [Real-Time CDP B2B edition](../../../../../rtcdp/b2b-overview.md): Real-Time CDP B2B edition è progettato appositamente per gli addetti al marketing che operano in un modello di servizio business-to-business. Raccoglie dati da più origini e li combina in un’unica vista di persone e profili di account. Questi dati unificati consentono ai marketer di rivolgersi con precisione a tipi di pubblico specifici e di coinvolgerli in tutti i canali disponibili.
* [Origini](../../../../home.md): Experience Platform consente di acquisire dati da varie origini e allo stesso tempo di strutturare, etichettare e migliorare i dati in arrivo tramite i servizi Experience Platform.
* [Sandbox](../../../../../sandboxes/home.md): Experience Platform fornisce sandbox virtuali che suddividono una singola istanza Experience Platform in ambienti virtuali separati, utili per le attività di sviluppo e aggiornamento delle applicazioni di esperienza digitale.

### Prerequisiti

Leggi la [[!DNL Demandbase Intent] panoramica](../../../../connectors/data-partners/demandbase.md) per informazioni su come recuperare le credenziali di autenticazione.

## Navigare nel catalogo delle origini {#navigate}

Nell&#39;interfaccia utente di Experience Platform, seleziona **[!UICONTROL Origini]** dal menu di navigazione a sinistra per accedere all&#39;area di lavoro *[!UICONTROL Origini]*. Puoi selezionare la categoria appropriata nel pannello *[!UICONTROL Categorie]*. In alternativa, è possibile utilizzare la barra di ricerca per passare all&#39;origine specifica che si desidera utilizzare.

Per utilizzare [!DNL Demandbase], selezionare la scheda di origine **[!UICONTROL Intento Demandbase]** in [!UICONTROL Partner dati e identità], quindi selezionare **[!UICONTROL Aggiungi dati]**.

>[!TIP]
>
>Le origini nel catalogo delle origini visualizzano l&#39;opzione **[!UICONTROL Configura]** quando un&#39;origine specificata non dispone ancora di un account autenticato. Quando esiste un account autenticato, questa opzione diventa **[!UICONTROL Aggiungi dati]**.

![Catalogo origini con la scheda &quot;Intento Demandbase&quot; selezionata.](../../../../images/tutorials/create/demandbase/catalog.png)

## Autenticazione {#authentication}

### Usa un account esistente {#existing}

Per utilizzare un account esistente, selezionare **[!UICONTROL Account esistente]**, quindi selezionare l&#39;account che si desidera utilizzare dall&#39;elenco di account nell&#39;interfaccia.

Dopo aver selezionato l&#39;account, seleziona **[!UICONTROL Avanti]** per procedere al passaggio successivo.

![Interfaccia account esistente del flusso di lavoro origini.](../../../../images/tutorials/create/demandbase/existing.png)

### Crea un nuovo account {#create}

Se non disponi di un account esistente, devi crearne uno nuovo fornendo le credenziali di autenticazione necessarie che corrispondono all’origine.

Per creare un nuovo account, selezionare **[!UICONTROL Nuovo account]**, quindi specificare il nome dell&#39;account e, facoltativamente, una descrizione per i dettagli dell&#39;account. Quindi, fornisci i valori di autenticazione appropriati per autenticare l’origine su Experience Platform. Per connettere l&#39;account [!DNL Demandbase Intent], è necessario disporre delle credenziali seguenti:

* **ID chiave di accesso**: ID chiave di accesso [!DNL Demandbase]. Si tratta di una stringa alfanumerica di 61 caratteri necessaria per autenticare l’account in Experience Platform.
* **Chiave di accesso segreta**: la chiave di accesso segreta [!DNL Demandbase]. Si tratta di una stringa con codifica base 64 di 40 caratteri necessaria per autenticare l’account in Experience Platform.
* **Nome bucket**: bucket [!DNL Demandbase] da cui verranno estratti i dati.

![Nuova interfaccia account del flusso di lavoro di origine.](../../../../images/tutorials/create/demandbase/new.png)

## Fornisci i dettagli del flusso di dati {#provide-dataflow-details}

Una volta autenticato e connesso l’account, è necessario fornire i seguenti dettagli per il flusso di dati:

* **Nome flusso di dati**: nome del flusso di dati. Puoi utilizzare questo nome per cercare il flusso di dati nell’interfaccia utente, una volta creato ed elaborato.
* **Descrizione**: (facoltativo) una breve spiegazione o informazioni aggiuntive per il flusso di dati.
* **Origine dominio**: il campo del dominio o del sito Web che corrisponde ai record dell&#39;account di origine rispetto agli account Experience Platform. Questo valore può dipendere dalle configurazioni. Se non specificato, il dominio predefinito è `accountOrganization.website`.

![Passaggio dei dettagli del flusso di dati del flusso di lavoro di origine.](../../../../images/tutorials/create/demandbase/dataflow-detail.png)

## Pianifica flusso di dati {#schedule-dataflow}

Quindi, utilizza l’interfaccia di pianificazione per configurare una pianificazione di acquisizione per il flusso di dati.

* **Frequenza**: configura la frequenza per indicare la frequenza con cui deve essere eseguito il flusso di dati. Puoi pianificare il flusso di dati [!DNL Demandbase] per acquisire i dati a una frequenza settimanale.
* **Intervallo**: l&#39;intervallo rappresenta il tempo che intercorre tra ciascun ciclo di acquisizione. L&#39;unico intervallo supportato per un flusso di dati [!DNL Demandbase] è `1`. Ciò significa che il flusso di dati acquisirà i dati una volta alla settimana, ogni settimana.
* **Ora di inizio**: l&#39;ora di inizio determina quando verrà eseguita la prima iterazione del flusso di dati. [!DNL Demandbase] rilascia i dati ad Adobe una volta alla settimana, il lunedì, alle 12:00 UTC. Pertanto, è necessario impostare l’ora di inizio dell’acquisizione dopo le 12:00 UTC. Inoltre, è necessario confermare il tempo di acquisizione con [!DNL Demandbase] in quanto potrebbero modificare la pianificazione quando si rilasciano file in Adobe.
* **Backfill**: il backfill determina quali dati vengono inizialmente acquisiti. Se la retrocompilazione è abilitata, tutti i file correnti nel percorso specificato verranno acquisiti durante la prima acquisizione pianificata. Se la retrocompilazione è disattivata, verranno acquisiti solo i file caricati tra la prima esecuzione dell’acquisizione e l’ora di inizio. I file caricati prima dell’ora di inizio non verranno acquisiti.

Dopo aver configurato la pianificazione dell&#39;acquisizione del flusso di dati, seleziona **[!UICONTROL Avanti]**.

![Interfaccia di pianificazione del flusso di lavoro di origine.](../../../../images/tutorials/create/demandbase/scheduling.png)

## Verifica flusso di dati {#review-dataflow}

Il passaggio finale nel processo di creazione del flusso di dati consiste nell’esaminare il flusso di dati prima di eseguirlo. Utilizza il passaggio *[!UICONTROL Rivedi]* per rivedere i dettagli del nuovo flusso di dati prima che venga eseguito. I dettagli sono raggruppati nelle seguenti categorie:

* **Connessione**: mostra il tipo di origine, il percorso pertinente del file di origine scelto e il numero di colonne all&#39;interno di tale file di origine.
* **Pianificazione**: mostra il periodo, la frequenza e l&#39;intervallo attivi della pianificazione di acquisizione.

![Interfaccia di revisione del flusso di lavoro origini.](../../../../images/tutorials/create/demandbase/review.png)

## Passaggi successivi

Seguendo questa esercitazione, è stato creato un flusso di dati per portare dati intento dall&#39;origine [!DNL Demandbase] ad Experience Platform. Per ulteriori risorse, consulta la documentazione descritta di seguito.

### Monitorare il flusso di dati

Una volta creato il flusso di dati, puoi monitorare i dati che vengono acquisiti tramite di esso per visualizzare informazioni su tassi di acquisizione, successo ed errori. Per ulteriori informazioni su come monitorare il flusso di dati, visita l&#39;esercitazione su [account di monitoraggio e flussi di dati nell&#39;interfaccia utente](../../../../../dataflows/ui/monitor-sources.md).

### Aggiornare il flusso di dati

Per aggiornare le configurazioni per la pianificazione, la mappatura e le informazioni generali dei flussi di dati, visita il tutorial su [aggiornamento dei flussi di dati di origine nell&#39;interfaccia utente](../../update-dataflows.md).

### Eliminare il flusso di dati

È possibile eliminare i flussi di dati non più necessari o creati in modo errato utilizzando la funzione **[!UICONTROL Elimina]** disponibile nell&#39;area di lavoro **[!UICONTROL Flussi di dati]**. Per ulteriori informazioni su come eliminare i flussi di dati, consulta l&#39;esercitazione su [eliminazione dei flussi di dati nell&#39;interfaccia utente](../../delete.md).
