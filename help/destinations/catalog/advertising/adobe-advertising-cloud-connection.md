---
title: Connessione Adobe Advertising Cloud DSP
description: Adobe Advertising Cloud DSP è una destinazione integrata per Adobe Real-time Customer Data Platform che consente di condividere tipi di pubblico autenticati di prime parti con inserzionisti e utenti approvati per l’attivazione della campagna.
exl-id: 11ff7797-a9c6-4334-b843-ae9df9a48e54
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1055'
ht-degree: 2%

---

# Connessione Adobe Advertising Cloud DSP

## Panoramica {#overview}

La destinazione Adobe Advertising Cloud [!DNL Demand-Side Platform] (DSP) consente di condividere i tipi di pubblico di prime parti autenticati con inserzionisti e utenti approvati per l&#39;attivazione della campagna con DSP. Per ulteriori informazioni sull&#39;integrazione di Real-Time CDP con DSP, vedere [Informazioni sull&#39;attivazione di tipi di pubblico autenticati da origini pubblico](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-about.html).

>[!IMPORTANT]
>
>Questa pagina è stata creata dal team DSP. Per richieste di informazioni o richieste di aggiornamento, contatta il supporto Advertising Cloud direttamente all&#39;indirizzo `adcloud_support@adobe.com`.

## Casi d’uso {#use-cases}

Per aiutarti a capire meglio come e quando utilizzare la destinazione Advertising Cloud DSP, ecco alcuni casi d’uso di esempio che i clienti Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### Caso di utilizzo: pubblicità del brand

Un rivenditore online desidera effettuare il retargeting dei clienti di alto valore tramite una campagna di visualizzazione senza utilizzare i cookie per il targeting. Il rivenditore condivide un pubblico costituito dagli ID e-mail con hash dei suoi clienti di alto valore dal suo account Adobe Real-time Customer Data Platform (Real-Time CDP) al suo account DSP. L&#39;DSP converte quindi gli ID e-mail con hash in [!DNL RampIDs] autenticati tramite una partnership tra DSP e LiveRamp. L&#39;elemento [!DNL RampIDs] risultante può essere utilizzato in una campagna di visualizzazione per eseguire il targeting del pubblico.

### Caso di utilizzo dell’agenzia

Un’agenzia di media con un account DSP sta conducendo una campagna di retargeting per conto del proprio cliente, un marchio leader nel settore dell’ospitalità. Il marchio vuole effettuare il retargeting di tutti i suoi ospiti nell’ultimo anno con una nuova offerta promozionale. Il brand ospita tutte le informazioni sugli ospiti in [!DNL Real-Time CDP]. Il brand può condividere un pubblico costituito dagli ID e-mail con hash dei propri ospiti dal proprio account [!DNL Real-Time CDP] all’account DSP dell’agenzia di media per effettuare il retargeting degli ospiti attraverso una campagna mediatica.

## Prerequisiti {#prerequisites}

* Impostazioni a livello di account DSP e di campagna per abilitare la condivisione del pubblico con [!DNL LiveRamp RampID], che tradurrà i dati dei clienti in [!DNL RampIDs] per creare segmenti di destinazione. Il tuo account team DSP eseguirà questa configurazione. [!DNL RampID] è disponibile tramite una partnership tra l&#39;DSP e [!DNL LiveRamp] e non è necessaria la tua iscrizione a [!DNL LiveRamp] per utilizzarlo.
* L’ID organizzazione dell’Experience Cloud per l’account dell’Experience Platform. Puoi trovare il tuo ID nella pagina del tuo profilo utente di [!DNL Real-Time CDP].
* Un&#39;origine [[!DNL Real-Time CDP] in DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html) per ricevere i tipi di pubblico per l&#39;attivazione della campagna. Il tuo account team DSP creerà la sorgente utilizzando il tuo ID organizzazione Experience Cloud.
* Chiave di origine per l&#39;account DSP o l&#39;inserzionista, generata quando viene creata un&#39;origine [[!DNL Real-Time CDP] nell&#39;DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html). Il tuo account team DSP condividerà con te questa chiave. La utilizzerai in Experience Platform per creare una connessione di destinazione alla destinazione Advertising Cloud DSP, come [spiegato di seguito](#authenticate).
* Dati del cliente costituiti da e-mail o e-mail con hash.

## Identità supportate {#supported-identities}

La destinazione Adobe Advertising Cloud DSP supporta l’attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/features/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| email_lc_sha256 | Indirizzi e-mail con hash con algoritmo SHA256 | Experience Platform supporta sia gli indirizzi di posta elettronica in testo normale che quelli con hash SHA256. Se il campo di origine contiene attributi senza hash, selezionare l&#39;opzione **[!UICONTROL Applica trasformazione]** per fare in modo che Experience Platform esegua automaticamente l&#39;hash dei dati all&#39;attivazione. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione pubblico]** | Stai esportando tutti i membri di un pubblico con gli identificatori (e-mail o e-mail con hash) utilizzati nella destinazione Advertising Cloud DSP. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Quando un profilo viene aggiornato in Experience Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni sulle [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario, ad Experience Platform, **[!UICONTROL Visualizzare le destinazioni]** e **[!UICONTROL Gestire le destinazioni]** [Autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi alla destinazione, seguire le istruzioni per [creare una connessione di destinazione](/help/destinations/ui/connect-destination.md) utilizzando l&#39;interfaccia utente di Experience Platform. Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autenticarsi nella destinazione {#authenticate}

Per connettersi alla destinazione, fornire il parametro seguente nella sezione [!UICONTROL Tipo di connessione], quindi selezionare **[!UICONTROL Connetti alla destinazione]**.:

* **[!UICONTROL Chiave account o inserzionista]**: questa [!UICONTROL Chiave Source] viene generata quando viene creata un&#39;origine [[!DNL Real-Time CDP] nell&#39;interfaccia utente DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html). Il tuo account team DSP condividerà con te questa chiave dopo che avrà creato la sorgente.

![Campo tipo di connessione](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/authenticate-destination.png)

### Inserire i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

* **[!UICONTROL Nome]**: un nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: una descrizione che ti aiuterà a identificare questa destinazione in futuro.

![Campi dettagli destinazione](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/destination-details.png)

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli per la connessione di destinazione, seleziona **[!UICONTROL Avanti]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Visualizza grafo identità]** [Controllo di accesso](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Leggi [Attivare profili e tipi di pubblico nelle destinazioni di esportazione del pubblico di streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per le istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione.

## Convalidare l’esportazione dei dati {#exported-data}

Per verificare che il pubblico di dati sia stato condiviso con Advertising Cloud, verifica quanto segue:

* Flusso di dati nella destinazione [!DNL Real-Time CDP] completato.

* In DSP, il pubblico è disponibile quando crei o modifichi un pubblico da [!UICONTROL Tipi di pubblico] > [!UICONTROL Tutti i tipi di pubblico] o dall&#39;interno della sezione [!UICONTROL Targeting pubblico] delle impostazioni di posizionamento. Il pubblico deve essere visibile nella scheda [!UICONTROL Segmenti di Adobe] nella cartella [!UICONTROL Real-Time CDP].

![Tipi di pubblico di Real-Time CDP nelle impostazioni del pubblico DSP](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/segments-in-dsp.png)

## Utilizzo dei dati e governance {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, vedi [Panoramica sulla governance dei dati](/help/data-governance/home.md).
