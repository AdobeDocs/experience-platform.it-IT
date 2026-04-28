---
title: Rokt
description: Scopri come collegare i tipi di pubblico di Adobe Experience Platform a Rokt per migliorare le prestazioni della campagna tramite targeting, soppressione e personalizzazione più intelligenti.
source-git-commit: a281a7c961b8576105913feb7a7f8258c975e875
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 4%

---


# Connessione [!DNL Rokt] {#rokt-destination}

## Panoramica {#overview}

[[!DNL Rokt]](https://www.rokt.com) sblocca il valore in e-commerce utilizzando decisioni in tempo reale basate sull&#39;intelligenza artificiale per rendere ogni momento di transazione™ più rilevante. Offre esperienze personalizzate e collega gli inserzionisti con clienti ad alto intento. Connetti i tipi di pubblico [!DNL Adobe Experience Platform] a [!DNL Rokt] per migliorare le prestazioni della campagna tramite targeting, eliminazione e personalizzazione più intelligenti. Raggiungi i clienti giusti al momento giusto riducendo gli sprechi di spesa.

>[!IMPORTANT]
>
>Il connettore di destinazione e la pagina della documentazione vengono creati e gestiti dal team [!DNL Rokt]. Per richieste di informazioni o richieste di aggiornamento, contatta il tuo Account Manager [!DNL Rokt] o contatta il numero `support@rokt.com`.

## Casi d’uso {#use-cases}

I seguenti casi d&#39;uso mostrano come i clienti [!DNL Experience Platform] possono utilizzare la destinazione [!DNL Rokt].

### Caso d’uso #1: retargeting {#use-case-1}

Rivolgiti ai clienti ad alto intento che hanno visitato il tuo sito o la tua app ma non l’hanno convertita. Crea un pubblico in [!DNL Experience Platform] includendo gli utenti che hanno sfogliato categorie di prodotti specifiche o abbandonato un flusso di pagamento. Quindi invia il pubblico a [!DNL Rokt] per distribuire offerte personalizzate al punto di acquisto sui siti partner. [!DNL Rokt] funziona nel momento della transazione, immediatamente dopo che un cliente ha completato un acquisto altrove. Il pubblico di destinazione viene raggiunto quando la finalità di acquisto è al suo apice, determinando tassi di conversione più elevati rispetto al retargeting della visualizzazione tradizionale.

### #2 dei casi d’uso: elenchi di soppressione {#use-case-2}

Impedisci sprechi di spesa ed esperienze irrilevanti eliminando i tipi di pubblico che non dovrebbero ricevere alcune offerte [!DNL Rokt]. I casi d’uso comuni di eliminazione includono l’esclusione di convertitori recenti, membri fedeltà in una promozione attiva o utenti che hanno rinunciato al marketing. Ad esempio, escludi i clienti che hanno acquistato negli ultimi 30 giorni. Sincronizza questi tipi di pubblico di eliminazione da [!DNL Experience Platform] a [!DNL Rokt] in tempo reale. In questo modo le campagne si concentreranno sugli utenti nuovi o riconnettibili. Questo migliora il ROI e protegge l’esperienza del cliente.

## Prerequisiti {#prerequisites}

Prima di configurare la destinazione [!DNL Rokt] in [!DNL Adobe Experience Platform], è necessario ottenere le credenziali seguenti dall&#39;Account Manager **[!DNL Rokt]**:

* **Chiave API**: utilizzala come **[!UICONTROL Username]** quando [autentica la connessione di destinazione](#authenticate).
* **Segreto API**: utilizzalo come **[!UICONTROL Password]** quando [autentica la connessione di destinazione](#authenticate).

Il tuo Account Manager [!DNL Rokt] eseguirà il provisioning di queste credenziali nella piattaforma [!DNL Rokt] prima della configurazione. Se non li hai ancora ricevuti, contatta il tuo Account Manager.

## Identità supportate {#supported-identities}

[!DNL Rokt] supporta l&#39;attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/features/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| e-mail | Indirizzo e-mail in testo normale | Consigliato. Utilizzato per la corrispondenza del profilo in [!DNL Rokt]. |
| email_lc_sha256 | Indirizzi e-mail con hash con algoritmo SHA256 | Sono supportati sia gli indirizzi di posta elettronica in testo normale che quelli con hash SHA256. Quando il campo di origine contiene attributi senza hash, selezionare l&#39;opzione **[!UICONTROL Apply transformation]** per impostare [!DNL Experience Platform] per l&#39;hash automatico dei dati all&#39;attivazione. |
| telefono | Numero di telefono in testo normale | Utilizzato per la corrispondenza del profilo in [!DNL Rokt]. |
| phone_sha256 | Numeri di telefono con hash con algoritmo SHA256 | Sono supportati sia i numeri di telefono con hash di testo normale che quelli SHA256. Quando il campo di origine contiene attributi senza hash, selezionare l&#39;opzione **[!UICONTROL Apply transformation]** per impostare [!DNL Experience Platform] per l&#39;hash automatico dei dati all&#39;attivazione. |
| GAID | ID Advertising [!DNL Google] | Seleziona l’identità di destinazione GAID quando l’identità di origine è uno spazio dei nomi GAID. |
| IDFA | ID [!DNL Apple] per gli inserzionisti | Selezionare l&#39;identità di destinazione IDFA quando l&#39;identità di origine è uno spazio dei nomi IDFA. |
| aepProfileId | ID profilo [!DNL Adobe Experience Platform] | Mappa l&#39;ID profilo (`xdm:_id`) come identificatore di fallback. |

{style="table-layout:auto"}

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive quali tipi di pubblico puoi esportare in questa destinazione.

| Origine pubblico | Supportato | Descrizione |
|---------|----------|----------|
| [!DNL Segmentation Service] | Sì | Pubblico generato tramite [!DNL Experience Platform] [[!DNL Segmentation Service]](/help/segmentation/home.md). |
| Tutte le altre origini del pubblico | Sì | Questa categoria include tutte le origini del pubblico al di fuori dei tipi di pubblico generati tramite [!DNL Segmentation Service]. Leggi informazioni sulle [diverse origini del pubblico](/help/segmentation/ui/audience-portal.md#customize). Alcuni esempi includono: <ul><li> i tipi di pubblico per caricamento personalizzati [importati](/help/segmentation/ui/audience-portal.md#import-audience) in [!DNL Experience Platform] da file CSV,</li><li> pubblico simile, </li><li> pubblico federato, </li><li> tipi di pubblico generati in altre app [!DNL Experience Platform] come [!DNL Adobe Journey Optimizer], </li><li> e altro ancora. </li></ul> |

{style="table-layout:auto"}

Tipi di pubblico supportati per tipo di dati sul pubblico:

| Tipo di dati del pubblico | Supportato | Descrizione | Casi d’uso |
|--------------------|-----------|-------------|-----------|
| [Tipi di pubblico per persone](/help/segmentation/types/people-audiences.md) | Sì | In base ai profili dei clienti. Utilizzale per rivolgerti a gruppi specifici di persone per le campagne di marketing. | Acquirenti frequenti, abbandoni del carrello |
| [Pubblico dell&#39;account](/help/segmentation/types/account-audiences.md) | No | Puoi indirizzare l’attività a singoli utenti all’interno di organizzazioni specifiche per strategie di marketing basate sull’account. | Marketing B2B |
| [Pubblico potenziale](/help/segmentation/types/prospect-audiences.md) | No | Puoi indirizzare l’attività a singoli utenti che non sono ancora clienti, ma che condividono alcune caratteristiche con il tuo pubblico di destinazione. | Ricerca di dati di terze parti |
| [Esportazioni set di dati](/help/catalog/datasets/overview.md) | No | Raccolte di dati strutturati archiviati nel Data Lake [!DNL Adobe Experience Platform]. | Reporting, flussi di lavoro di data science |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
|---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Audience export]** | Stai esportando tutti i membri di un pubblico con gli identificatori (e-mail, telefono, ID annuncio mobile o altri) utilizzati nella destinazione [!DNL Rokt]. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in [!DNL Experience Platform] in base alla valutazione del pubblico, il connettore invia l&#39;aggiornamento a valle a [!DNL Rokt]. Ulteriori informazioni sulle [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
>
>Per connettersi alla destinazione, sono necessarie le **[!UICONTROL View Destinations]** e le **[!UICONTROL Manage Destinations]** [autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](/help/destinations/ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autenticarsi nella destinazione {#authenticate}

Per autenticare nella destinazione, compilare i campi obbligatori e selezionare **[!UICONTROL Connect to destination]**.

* **[!UICONTROL Username]**: la chiave API, fornita dall&#39;Account Manager [!DNL Rokt].
* **[!UICONTROL Password]**: Segreto API, fornito dal tuo Account Manager [!DNL Rokt].

  ![Schermata di configurazione della destinazione [!DNL Rokt] in [!DNL Experience Platform], con i dettagli dell&#39;account, i campi di autenticazione e i dettagli della destinazione compilati.](/help/destinations/assets/catalog/advertising/rokt/aep-configure-destination.png)

### Inserire i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

* **[!UICONTROL Name]**: nome con cui riconoscerai questa destinazione in futuro (ad esempio, &quot;[!DNL Rokt] - Retargeting di tipi di pubblico&quot;).
* **[!UICONTROL Description]**: una descrizione che ti aiuterà a identificare questa destinazione in futuro.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](/help/destinations/ui/alerts.md).

Dopo aver fornito i dettagli della connessione di destinazione, selezionare **[!UICONTROL Next]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
>
>* Per attivare i dati, sono necessarie le **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL View Identity Graph]** [per il controllo degli accessi](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Leggi [Attivare profili e tipi di pubblico nelle destinazioni di esportazione del pubblico di streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per le istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione.

### Mappare attributi e identità {#map}

La destinazione [!DNL Rokt] supporta la mappatura degli spazi dei nomi di identità da [!DNL Experience Platform] a [!DNL Rokt] campi di identità. Per attivare correttamente un pubblico, devi mappare almeno un’identità. Le mappature consigliate sono mostrate nella tabella seguente.

| Campo di origine | Campo di destinazione | Considerazioni |
|---|---|---|
| `IdentityMap: Email` | `Identity: email` | Consigliato |
| `IdentityMap: Email_LC_SHA256` | `Identity: emailSha256` | Consigliato |
| `IdentityMap: Phone` | `Identity: phone` | Facoltativo |
| `IdentityMap: Phone_SHA256` | `Identity: phoneSha256` | Facoltativo |
| `IdentityMap: GAID` | `Identity: gaid` | Facoltativo |
| `IdentityMap: IDFA` | `Identity: idfa` | Facoltativo |
| `xdm: _id` | `Identity: aepProfileId` | Facoltativo |

{style="table-layout:auto"}

Ecco un esempio di mappatura completa:

![Passaggio di mappatura del flusso di lavoro di attivazione della destinazione [!DNL Rokt] in [!DNL Experience Platform], con campi di identità di origine e di destinazione configurati.](/help/destinations/assets/catalog/advertising/rokt/aep-identity-mapping.png)

>[!NOTE]
>
>Almeno un mapping di identità basato su posta elettronica (`email` o `emailSha256`) è vivamente consigliato per massimizzare le percentuali di corrispondenza in [!DNL Rokt].

### Configurare la pianificazione del pubblico {#audience-schedule}

Dopo aver completato il passaggio di mappatura, configura una pianificazione del pubblico per ogni pubblico selezionato. Specifica un **[!UICONTROL Start date]** per indicare quando deve iniziare la sincronizzazione del pubblico e un **[!UICONTROL Mapping ID]** (un&#39;etichetta utilizzata per identificare il pubblico in [!DNL Rokt]). È possibile utilizzare il nome del pubblico [!DNL Experience Platform] o qualsiasi stringa descrittiva che consenta a te e al tuo Account Manager [!DNL Rokt] di identificare il pubblico.

## Utilizzo dei dati e governance {#data-usage-governance}

Tutte le destinazioni [!DNL Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Experience Platform] applica la governance dei dati, leggere la [Panoramica sulla governance dei dati](/help/data-governance/home.md).

## Risorse aggiuntive {#additional-resources}

* [Documentazione per gli sviluppatori di [!DNL Rokt]](https://docs.rokt.com)
* [Panoramica sulle destinazioni di Adobe Experience Platform](/help/destinations/home.md)
