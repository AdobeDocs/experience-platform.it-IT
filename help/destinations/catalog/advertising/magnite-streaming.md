---
title: Connessione di destinazione in tempo reale Magnite Streaming
description: Utilizza questa destinazione per fornire Adobi di pubblico CDP alla piattaforma Magnite Streaming in tempo reale.
badgeBeta: label="Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1306'
ht-degree: 2%

---


# (Beta) Magnite Streaming: connessione di destinazione in tempo reale

## Panoramica {#overview}

Il [!DNL Magnite Streaming: Real-Time] e Magnite Streaming: le destinazioni Batch in Adobe Experience Platform consentono di mappare ed esportare i tipi di pubblico per il targeting e l’attivazione sulla piattaforma Magnite Streaming.

Attivazione dei tipi di pubblico in [!DNL Magnite Streaming] Platform è un processo in due fasi che richiede di utilizzare sia le destinazioni Magnite Streaming: Real-Time che Magnite Streaming: Batch.

Per attivare i tipi di pubblico in [!DNL Magnite Streaming], è necessario:

* Attiva i tipi di pubblico in [!DNL Magnite Streaming: Real-Time] come mostrato in questa pagina.
* Attiva lo stesso pubblico nella destinazione Magnite Streaming: Batch. Il [!DNL Magnite Streaming: Batch] la destinazione è un componente obbligatorio. Impossibile attivare il pubblico su [!DNL Magnite Streaming] La destinazione batch genera un’integrazione non riuscita e i tipi di pubblico non vengono attivati.

Nota: quando si utilizza la destinazione in tempo reale, [!DNL Magnite: Streaming] riceverà i tipi di pubblico in tempo reale, ma possiamo solo memorizzare temporaneamente i tipi di pubblico in tempo reale nella nostra piattaforma e verranno rimossi dal sistema entro un paio di giorni. Per questo motivo, se desideri utilizzare la destinazione Magnite: Streaming Real-Time, potrai *anche* necessità di utilizzare la destinazione Magnite Streaming: Batch: per ogni pubblico che si attiva nella destinazione in tempo reale, è necessario attivare anche la destinazione Batch.

>[!IMPORTANT]
>
>Questo connettore di destinazione è in versione beta ed è disponibile solo per alcuni clienti. Per richiedere l’accesso, contatta il rappresentante del tuo Adobe.
>
>Il connettore di destinazione e la pagina della documentazione vengono creati e gestiti da [!DNL Magnite] team. Per eventuali richieste di informazioni o richieste di aggiornamento, contattatele direttamente all&#39;indirizzo `adobe-tech@magnite.com`.

## Casi d’uso {#use-cases}

Per aiutarti a capire meglio come e quando utilizzare il [!DNL Magnite Streaming: Real-Time] destinazione: ecco un caso d’uso di esempio che i clienti di Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### Attivazione e targeting {#activation-and-targeting}

Questa integrazione con Magnite consente ai clienti di trasmettere i propri tipi di pubblico CDP da Adobe Experience Platform a Magnite per il targeting pubblicitario. I tipi di pubblico possono essere selezionati all’interno di Magnite per il targeting positivo e negativo (soppressione).

## Prerequisiti {#prerequisites}

Per utilizzare [!DNL Magnite] destinazioni in Adobe Experience Platform, devi prima disporre di un [!DNL Magnite Streaming] account. Se si dispone di [!DNL Magnite Streaming] account, contatta il tuo [!DNL Magnite] al responsabile dell’account devono essere fornite le credenziali per accedere [!DNL Magnite's] destinazioni.
Se non si dispone di [!DNL Magnite Streaming] account, contatta adobe-tech@magnite.com

## Identità supportate {#supported-identities}

Il [!DNL Magnite Streaming: Real-Time] la destinazione supporta l’attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/features/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
|-------------------|--------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| device_id | Identificatore univoco di un dispositivo o di un’identità. Accettiamo qualsiasi ID dispositivo e ID di prime parti indipendentemente dal tipo. | I tipi di identità supportati includono, ma non sono limitati a, PPUID, GAID, IDFA e ID dispositivo TV. |

{style="table-layout:auto"}

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive il tipo di pubblico che puoi esportare in questa destinazione.

| Origine pubblico | Supportato | Descrizione |
|-----------------------------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Tipi di pubblico generati dall’Experience Platform [Servizio di segmentazione](../../../segmentation/home.md). |
| Caricamenti personalizzati | ✓ | Tipi di pubblico [importato](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform da file CSV. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
|------------------|---------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Tipo di esportazione | **[!UICONTROL Esportazione segmento]** | Stai esportando tutti i membri di un segmento (pubblico) con gli identificatori (nome, numero di telefono o altri) utilizzati in [!DNL Magnite Streaming: Real-Time] destinazione. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione dei segmenti, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni su [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
>
>Per connettersi alla destinazione, è necessario **[!UICONTROL Visualizza destinazioni]** e **[!UICONTROL Gestione destinazioni]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autenticarsi nella destinazione {#authenticate}

Per autenticare nella destinazione, compila i campi obbligatori e seleziona **[!UICONTROL Connetti alla destinazione]**.

![campi di autenticazione della configurazione di destinazione non compilati](../../assets/catalog/advertising/magnite/destination-realtime-config-auth-unfilled.png)

* **[!UICONTROL Nome utente]**: nome utente fornito da [!DNL Magnite].
* **[!UICONTROL Password]**: password fornita da [!DNL Magnite].

### Inserire i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

* **[!UICONTROL Nome]**: nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL Nome del partner di origine]**: nome del cliente/dell’azienda. Solo supportati [!DNL Magnite Streaming] I client sono disponibili per la selezione.

![campi di autenticazione della configurazione di destinazione compilati](../../assets/catalog/advertising/magnite/destination-realtime-config-auth-filled.png)

Al termine, seleziona la **[!UICONTROL Crea]** pulsante.

![Criteri di governance facoltativi e azioni di applicazione](../../assets/catalog/advertising/magnite/destination-realtime-config-grouping-policy.png)

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completate le informazioni sulla connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
>
>* Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario **[!UICONTROL Visualizza grafico delle identità]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Letto [Attivare profili e segmenti nelle destinazioni di esportazione di segmenti in streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per istruzioni sull’attivazione dei segmenti di pubblico in questa destinazione.

Una volta creata la connessione di destinazione, puoi procedere al flusso di attivazione del pubblico. La sezione seguente illustra come attivare i tipi di pubblico utilizzando la destinazione in tempo reale.

### Mappare attributi e identità {#map}

Il passaggio successivo consiste nel mappare gli identificatori di origine all&#39;identificatore device_id Magnite.

* Puoi aggiungere tutte le mappature necessarie selezionando **[!UICONTROL Aggiungi nuova mappatura]**.

Questo esempio, utilizzando la destinazione in tempo reale, mostra una riga contenente un identificatore di origine deviceId generico mappato al campo di destinazione device_id Magnite. Quando utilizzi le mappature, seleziona [!UICONTROL Successivo].

![Mappa i campi dati desiderati sul campo device_ID](../../assets/catalog/advertising/magnite/destination-realtime-active-audience-field-mapping.png)

Assicurati di impostare gli ID di mappatura su tutti i tipi di pubblico attivati, o imposta NESSUNO se non è presente alcun ID di mappatura.

![Assicurati di impostare gli ID di mappatura su tutti i tipi di pubblico attivati, o imposta NESSUNO se non è presente alcun ID di mappatura](../../assets/catalog/advertising/magnite/destination-realtime-active-audience-mappingid.png)

Ora devi configurare una data di inizio (obbligatoria), una data di fine (facoltativa) e un ID di mappatura per ogni pubblico.

**ID mappatura**

* Utilizza il **[!UICONTROL ID mappatura]** quando un pubblico dispone di un ID segmento preesistente noto in precedenza a Magnite.

* Per aggiungere una **[!UICONTROL ID mappatura]** per un pubblico, seleziona ogni riga di pubblico singolarmente e immetti i dati nella colonna di destra (vedi immagine qui sopra). Se non vuoi aggiungere un ID mappatura, inserisci NESSUNO nel campo ID mappatura.

Seleziona **[!UICONTROL Successivo]** e finalizza il flusso di attivazione.

![Seleziona Avanti e finalizza il flusso di attivazione.](../../assets/catalog/advertising/magnite/destination-realtime-active-audience-review.png)

## Dati esportati / Convalida esportazione dati {#exported-data}

Dopo aver caricato i tipi di pubblico, puoi verificare che siano stati creati e caricati correttamente seguendo la procedura riportata di seguito:

<!--

* In 95% of cases, audiences will be delivered to Magnite Streaming in under 10 minutes. The actual receipt and processing of the events within Magnite Streaming depends on the shared data volume.

-->

* Acquisizione Post, i tipi di pubblico devono apparire in [!DNL Magnite Streaming] in pochi minuti e può essere applicata a un’offerta. Puoi confermarlo cercando l’ID segmento condiviso durante i passaggi di attivazione in Adobe Experience Platform.

## Attiva gli stessi tipi di pubblico tramite [!DNL Magnite Streaming: Batch]destinazione

Tipi di pubblico condivisi con [!DNL Magnite Streaming] l’utilizzo della destinazione in tempo reale dovrà essere condiviso anche utilizzando la destinazione Magnite Streaming: Batch. Se configurati correttamente, i nomi dei segmenti in [!DNL Magnite Streaming] L’interfaccia utente viene aggiornata per riflettere quelle utilizzate nell’aggiornamento post-giornaliero di Adobe Experience Platform.

Infine, se per l’integrazione non è stata configurata una destinazione Batch, impostala ora tramite il documento di destinazione Magnite Streaming: Batch.

## Utilizzo dei dati e governance {#data-usage-governance}

Tutti [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, leggi [Panoramica sulla governance dei dati](/help/data-governance/home.md).

## Risorse aggiuntive {#additional-resources}

Per ulteriore documentazione, visita il [Centro assistenza Magnite](https://help.magnite.com/help).
