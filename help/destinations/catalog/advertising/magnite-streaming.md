---
title: Connessione di destinazione Magnite in tempo reale
description: Utilizza questa destinazione per distribuire in tempo reale i tipi di pubblico di Adobe CDP alla piattaforma Magnite Streaming.
last-substantial-update: 2024-11-18T00:00:00Z
exl-id: 4e08a14b-6800-41e1-95a5-826a6241144d
source-git-commit: da05db9376893bdbe8f0aa291f19a507e4a73d4f
workflow-type: tm+mt
source-wordcount: '1317'
ht-degree: 1%

---

# Magnite: connessione di destinazione in tempo reale

## Panoramica {#overview}

Le destinazioni [!DNL Magnite: Real-Time] e [Magnite: Batch](/help/destinations/catalog/advertising/magnite-batch.md) in Adobe Experience Platform consentono di mappare ed esportare i tipi di pubblico per il targeting e l&#39;attivazione sulla piattaforma Magnite Streaming.

L&#39;attivazione dei tipi di pubblico nella piattaforma [!DNL Magnite Streaming] è un processo in due fasi che richiede l&#39;utilizzo delle destinazioni Magnite: Real-Time e Magnite: Batch.

Per attivare i tipi di pubblico in [!DNL Magnite Streaming], è necessario:

* Attiva i tipi di pubblico sulla destinazione [!DNL Magnite: Real-Time], come illustrato in questa pagina.
* Attiva lo stesso pubblico nella destinazione Magnite: Batch. La destinazione [!DNL Magnite: Batch] è un componente obbligatorio. Se non si attiva il pubblico nella destinazione batch [!DNL Magnite Streaming], si verificherà un errore di integrazione e il pubblico non verrà attivato.

Nota: quando si utilizza la destinazione in tempo reale, [!DNL Magnite Streaming] riceverà i tipi di pubblico in tempo reale, ma Magnite può memorizzare solo i tipi di pubblico in tempo reale temporaneamente nella propria piattaforma e verranno rimossi dal sistema entro un paio di giorni. Per questo motivo, se desideri utilizzare la destinazione Magnite: Real-Time, *anche* dovrai utilizzare la destinazione Magnite: Batch - ogni pubblico che attivi nella destinazione Real-Time, dovrai attivare anche nella destinazione Batch.

>[!IMPORTANT]
>
>Il connettore di destinazione e la pagina della documentazione vengono creati e gestiti dal team [!DNL Magnite]. Per richieste di informazioni o richieste di aggiornamento, contattale direttamente all&#39;indirizzo `adobe-tech@magnite.com`.

## Casi d’uso {#use-cases}

Per aiutarti a capire meglio come e quando utilizzare la destinazione [!DNL Magnite: Real-Time], ecco un esempio di caso d&#39;uso che i clienti Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### Attivazione e targeting {#activation-and-targeting}

Questa integrazione con Magnite consente ai clienti di trasmettere i propri tipi di pubblico CDP da Adobe Experience Platform a Magnite per il targeting pubblicitario. I tipi di pubblico possono essere selezionati all’interno di Magnite per il targeting positivo e negativo (soppressione).

## Prerequisiti {#prerequisites}

Per utilizzare le destinazioni [!DNL Magnite] in Adobe Experience Platform, devi prima disporre di un account [!DNL Magnite Streaming]. Se hai un account [!DNL Magnite Streaming], contatta il tuo account manager [!DNL Magnite] per ricevere le credenziali per accedere a [!DNL Magnite's] destinazioni.
Se non disponi di un account [!DNL Magnite Streaming], contatta adobe-tech@magnite.com

## Identità supportate {#supported-identities}

La destinazione [!DNL Magnite: Real-Time] supporta l&#39;attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/features/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
|-------------------|--------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| device_id | Identificatore univoco di un dispositivo o di un’identità. Accettiamo qualsiasi ID dispositivo e ID di prime parti indipendentemente dal tipo. | I tipi di identità supportati da Magnite includono, ma non sono limitati a, ID dispositivo PPUID, GAID, IDFA e TV. |

{style="table-layout:auto"}

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive il tipo di pubblico che puoi esportare in questa destinazione.

| Origine pubblico | Supportato | Descrizione |
|-----------------------------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Tipi di pubblico generati tramite il servizio di segmentazione [Experience Platform](../../../segmentation/home.md). |
| Caricamenti personalizzati | ✓ | Tipi di pubblico [importati](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform da file CSV. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
|------------------|---------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Tipo di esportazione | **[!UICONTROL Esportazione segmento]** | Stai esportando tutti i membri di un segmento (pubblico) con gli identificatori (nome, numero di telefono o altri) utilizzati nella destinazione [!DNL Magnite: Real-Time]. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione dei segmenti, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni sulle [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
>
>Per connettersi alla destinazione, è necessario disporre delle **[!UICONTROL Destinazioni di visualizzazione]** e **[!UICONTROL Gestione destinazioni]** [Autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autenticarsi nella destinazione {#authenticate}

Per eseguire l&#39;autenticazione nella destinazione, compilare i campi obbligatori e selezionare **[!UICONTROL Connetti alla destinazione]**.

![campi di autenticazione della configurazione di destinazione non compilati](../../assets/catalog/advertising/magnite/destination-realtime-config-auth-unfilled.png)

* **[!UICONTROL Nome utente]**: il nome utente fornito da [!DNL Magnite].
* **[!UICONTROL Password]**: la password fornita da [!DNL Magnite].

### Inserire i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

* **[!UICONTROL Nome]**: un nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL Nome società]**: nome cliente/società. Solo i client [!DNL Magnite Streaming] supportati sono disponibili per la selezione.

>[!NOTE]
>
>Il nome società deve essere una stringa che corrisponde al nome del bucket di consegna Amazon S3 configurato con Magnite e configurato nel passaggio [esegui autenticazione nella destinazione](#authenticate). I caratteri supportati includono &quot;a-z&quot;, &quot;A-Z&quot;, &quot;0-9&quot;, &quot;-&quot;(trattino) o &quot;_&quot;(trattino basso).

![campi di autenticazione della configurazione di destinazione compilati](../../assets/catalog/advertising/magnite/destination-realtime-config-auth-filled.png)

Al termine, seleziona il pulsante **[!UICONTROL Crea]**.

![Criteri di governance facoltativi e azioni di applicazione](../../assets/catalog/advertising/magnite/destination-realtime-config-grouping-policy.png)

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli per la connessione di destinazione, seleziona **[!UICONTROL Avanti]**.

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
>
>* Per attivare i dati, è necessario **[!UICONTROL Visualizzare le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizzare i profili]** e **[!UICONTROL Visualizzare i segmenti]** [accedere alle autorizzazioni di controllo](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Visualizza grafo identità]** [Controllo di accesso](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Leggi [Attivare profili e segmenti nelle destinazioni di esportazione dei segmenti di streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per le istruzioni sull&#39;attivazione dei segmenti di pubblico in questa destinazione.

Una volta creata la connessione di destinazione, puoi procedere al flusso di attivazione del pubblico. La sezione seguente illustra come attivare i tipi di pubblico utilizzando la destinazione in tempo reale.

### Mappare attributi e identità {#map}

Il passaggio successivo consiste nel mappare gli identificatori di origine all&#39;identificatore device_id Magnite.

* Puoi aggiungere tutte le mappature necessarie selezionando **[!UICONTROL Aggiungi nuova mappatura]**.

Questo esempio, utilizzando la destinazione in tempo reale, mostra una riga contenente un identificatore di origine deviceId generico mappato al campo di destinazione device_id Magnite. Quando utilizzi i mapping, seleziona [!UICONTROL Avanti].

![Mappa i campi dati desiderati sul campo device_ID](../../assets/catalog/advertising/magnite/destination-realtime-active-audience-field-mapping.png)

Assicurati di impostare gli ID di mappatura su tutti i tipi di pubblico attivati, o imposta NESSUNO se non è presente alcun ID di mappatura.

![Assicurarsi di impostare gli ID mappatura per tutti i tipi di pubblico attivati o impostare NONE se non è presente alcun ID mappatura](../../assets/catalog/advertising/magnite/destination-realtime-active-audience-mappingid.png)

Ora devi configurare una data di inizio (obbligatoria), una data di fine (facoltativa) e un ID di mappatura per ogni pubblico.

**ID mappatura**

* Utilizza il campo **[!UICONTROL ID mappatura]** quando un pubblico ha un ID segmento preesistente precedentemente noto a Magnite.

* Per aggiungere un **[!UICONTROL ID mappatura]** a un pubblico, seleziona ogni riga di pubblico singolarmente e immetti i dati nella colonna di destra (vedi immagine qui sopra). Se non vuoi aggiungere un ID mappatura, inserisci NESSUNO nel campo ID mappatura.

Seleziona **[!UICONTROL Avanti]** e finalizza il flusso di attivazione.

![Selezionare avanti e finalizzare il flusso di attivazione.](../../assets/catalog/advertising/magnite/destination-realtime-active-audience-review.png)

## Dati esportati / Convalida esportazione dati {#exported-data}

Dopo aver caricato i tipi di pubblico, puoi verificare che siano stati creati e caricati correttamente seguendo la procedura riportata di seguito:

<!--

* In 95% of cases, audiences will be delivered to Magnite Streaming in under 10 minutes. The actual receipt and processing of the events within Magnite Streaming depends on the shared data volume.

-->

* Dopo l&#39;acquisizione, i tipi di pubblico dovrebbero comparire in [!DNL Magnite Streaming] entro pochi minuti e possono essere applicati a un&#39;offerta. Puoi confermarlo cercando l’ID segmento condiviso durante i passaggi di attivazione in Adobe Experience Platform.

## Attiva gli stessi tipi di pubblico tramite la destinazione [!DNL Magnite: Batch]

I tipi di pubblico condivisi con [!DNL Magnite Streaming] utilizzando la destinazione in tempo reale dovranno essere condivisi anche utilizzando la destinazione Magnite: Batch. Se configurati correttamente, i nomi dei segmenti nell&#39;interfaccia utente [!DNL Magnite Streaming] vengono aggiornati per riflettere quelli utilizzati nell&#39;aggiornamento post-giornaliero di Adobe Experience Platform.

Infine, se per l’integrazione non è stata configurata una destinazione Batch, impostala ora tramite il documento di destinazione Magnite: Batch.

## Utilizzo dei dati e governance {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, leggere la [Panoramica sulla governance dei dati](/help/data-governance/home.md).

## Risorse aggiuntive {#additional-resources}

Per ulteriori informazioni, visitare il [Centro assistenza Magnite](https://help.magnite.com/help).
