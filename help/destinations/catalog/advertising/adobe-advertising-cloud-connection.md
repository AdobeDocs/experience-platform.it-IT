---
title: Connessione Adobe Advertising DSP
description: Scopri come condividere tipi di pubblico di prime parti autenticati e non autenticati con Adobe Advertising Cloud Demand-Side Platform (DSP) utilizzando più tipi di identità.
feature: Destinations
source-git-commit: 5513e95637c1016caeb6abe699e1807cc234ed40
workflow-type: tm+mt
source-wordcount: '1342'
ht-degree: 2%

---


# Connessione Adobe Advertising DSP

## Panoramica {#overview}

La destinazione Adobe Advertising Cloud Demand-Side Platform (DSP) consente agli utenti di condividere pubblici di prime parti autenticati e non autenticati con un account DSP o un inserzionista specifico all’interno di un account.

Questa destinazione consente ai clienti di condividere tipi di pubblico di prime parti con uno o tutti gli ID seguenti:

* ID e-mail con hash, convertito in [!DNL LiveRamp RampID] o [!DNL Unified ID 2.0] (UID2.0) per il targeting in DSP

* Cookie di terze parti di Experience Cloud ID (ECID) e Adobe Advertising

* ID mobile advertising (MAID):

   * [!DNL Google] ID Advertising (GAID) per [!DNL Android] dispositivi

   * Identificatori per inserzionisti (IDFA) per dispositivi [!DNL Apple iOS]

Questa connessione sostituisce la [connessione legacy Adobe Advertising Cloud DSP](adobe-advertising-cloud-connection-legacy.md), che supporta solo indirizzi e-mail con hash.

>[!IMPORTANT]
>
>Questa pagina è stata creata dal team Adobe Advertising [!DNL DSP]. Per richieste di informazioni o richieste di aggiornamento, contatta il supporto Advertising Cloud direttamente all&#39;indirizzo `adcloud_support@adobe.com`.

## Casi d’uso {#use-cases}

Questa destinazione consente agli inserzionisti di raggiungere il proprio pubblico attraverso i browser con cookie e senza cookie.

Gli inserzionisti possono scegliere di condividere i segmenti con identificatori di prime parti autenticati (come [!DNL RampID] e [!DNL UID2.0]) o con ID non autenticati (come cookie e MAID).

## Prerequisiti {#prerequisites}

* Per [!DNL RampID activation], [!DNL DSP] impostazioni a livello di account e di campagna per abilitare la condivisione del pubblico con [!DNL LiveRamp RampID], che traduce i dati dei clienti in [!DNL RampIDs] per creare segmenti di destinazione. Il team del tuo account Adobe eseguirà questa configurazione. [!DNL RampID] è disponibile tramite una partnership tra [!DNL DSP] e [!DNL LiveRamp] e non è necessario disporre della propria appartenenza a [!DNL LiveRamp] per utilizzarlo.

* ID pubblico:

   * Per [!DNL RampID] e [!DNL UID2.0], i profili devono contenere ID e-mail con hash.

   * Per i cookie, impostare un processo di sincronizzazione dei cookie con [!DNL Web SDK] flussi di dati o [!DNL Experience Cloud ID Service]. Consulta [Configurare la sincronizzazione ID per condividere i cookie](#cookie-sync) di seguito.

   * Per i profili con MAID:

      * Per ogni GAID, includi il valore `GAID` in una colonna IdentityMap.

      * Per ogni identificatore IDFA, includere il valore `IDFA` in una colonna IdentityMap.

* L’ID organizzazione Experience Cloud per l’account Experience Platform. Puoi trovare il tuo ID nella pagina del profilo utente di Adobe Real-Time Customer Data Platform (Real-Time CDP).

* Origine [Real-Time CDP in DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html) per ricevere i tipi di pubblico per l&#39;attivazione della campagna. Il team del tuo account Adobe creerà l’origine utilizzando il tuo ID organizzazione Experience Cloud.

* Chiave di origine per l&#39;account o l&#39;inserzionista [!DNL DSP], generata quando viene creata un&#39;origine [Real-Time CDP in [!DNL DSP]](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html). Il tuo account team di [!DNL DSP] condividerà questa chiave con te. La utilizzerai in Experience Platform per creare una connessione di destinazione alla destinazione Advertising Cloud DSP, come spiegato di seguito.

### Configurare la sincronizzazione ID per condividere i cookie {#cookie-sync}

La sincronizzazione ID è un prerequisito per condividere i cookie di terze parti. Configurare un processo di sincronizzazione dei cookie con [!DNL Web SDK] flussi di dati o [!DNL Experience Cloud ID Service]. Per ulteriori informazioni sulla gestione delle identità per i cookie di terze parti, consulta [Destinazioni di Advertising basate su integrazioni di cookie di terze parti](/help/destinations/how-destinations-work/identity-handling.md#third-party-cookie-destinations).

**Abilita sincronizzazione ID di terze parti con[!DNL Web SDK]**

Se utilizzi [!DNL Experience Platform Web SDK], abilita la sincronizzazione ID di terze parti nello stream di dati configurando l&#39;opzione [!UICONTROL Third Party ID Sync] nelle impostazioni avanzate. Per istruzioni, consulta [Configurare le opzioni avanzate](/help/datastreams/configure.md#advanced-options) nella documentazione sugli stream di dati.

**Abilita la sincronizzazione ID di terze parti con[!DNL Experience Cloud ID Service]**

Se utilizzi [!DNL Experience Platform] tag con [!DNL Experience Cloud ID Service], configura la sincronizzazione ID di terze parti utilizzando l&#39;[estensione del servizio Experience Cloud ID](/help/tags/extensions/client/id-service/overview.md). Questo consente al cookie di Adobe Advertising corrispondente all’ECID specificato di essere disponibile quando attivi il pubblico da Real-Time CDP.

## Identità supportate {#supported-identities}

La destinazione Adobe Advertising Cloud DSP supporta l’attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/features/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
| --------------- | ----------- | -------------- |
| `email_lc_sha256` | Indirizzi e-mail con hash con algoritmo SHA256 | Experience Platform supporta sia indirizzi di testo normale che indirizzi e-mail con hash SHA256. Se il campo di origine contiene attributi senza hash, selezionare l&#39;opzione **[!UICONTROL Apply transformation]** per fare in modo che Experience Platform esegua automaticamente l&#39;hash dei dati all&#39;attivazione. |
| `ECID` | Cookie di prime parti per Experience Cloud | Obbligatorio per creare segmenti basati su cookie. |
| `Everesttech cookie` | Cookie di terze parti per Adobe Advertising | Obbligatorio per creare segmenti basati su cookie. |
| `GAID` | ID dispositivo [!DNL Android] | Obbligatorio per il targeting di [!DNL Android] dispositivi. |
| `IDFA` | ID dispositivo [!DNL iOS] | Obbligatorio per il targeting di [!DNL iOS] dispositivi. |

{style="table-layout:auto"}

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive quali tipi di pubblico puoi esportare in questa destinazione.

| Origine pubblico | Supportato | Descrizione |
|---------|----------|----------|
| [!DNL Segmentation Service] | Sì | Tipi di pubblico generati tramite Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Tutte le altre origini del pubblico | Sì | Questa categoria include tutte le origini del pubblico al di fuori dei tipi di pubblico generati tramite [!DNL Segmentation Service]. Leggi informazioni sulle [diverse origini del pubblico](/help/segmentation/ui/audience-portal.md#customize). Alcuni esempi includono: <ul><li> i tipi di pubblico per caricamento personalizzati [importati](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform da file CSV,</li><li> pubblico simile, </li><li> pubblico federato, </li><li> tipi di pubblico generati in altre app di Experience Platform come Adobe Journey Optimizer, </li><li> e altro ancora. </li></ul> |

{style="table-layout:auto"}

Tipi di pubblico supportati per tipo di dati sul pubblico:

| Tipo di dati del pubblico | Supportato | Descrizione | Casi d’uso |
| -------------------- | --------- | ----------- | --------- |
| [Tipi di pubblico per persone](/help/segmentation/types/people-audiences.md) | Sì | In base ai profili dei clienti, consente di eseguire il targeting di gruppi specifici di persone per campagne di marketing. | Acquirenti frequenti, abbandoni del carrello |
| [Pubblico dell&#39;account](/help/segmentation/types/account-audiences.md) | No | Puoi indirizzare l’attività a singoli utenti all’interno di organizzazioni specifiche per strategie di marketing basate sull’account. | Marketing B2B |
| [Pubblico potenziale](/help/segmentation/types/prospect-audiences.md) | No | Puoi indirizzare l’attività a singoli utenti che non sono ancora clienti, ma che condividono alcune caratteristiche con il tuo pubblico di destinazione. | Ricerca di dati di terze parti |
| [Esportazioni set di dati](/help/catalog/datasets/overview.md) | No | Raccolte di dati strutturati archiviati nel Data Lake di Adobe Experience Platform. | Reporting, flussi di lavoro di data science |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
| ---- | ---- | ----- |
| Tipo di esportazione | **[!UICONTROL Audience export]** | Stai esportando tutti i membri di un pubblico con gli identificatori scelti. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Quando un profilo viene aggiornato in Experience Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni sulle [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
>
>Per connettersi alla destinazione, è necessario disporre dell&#39;autorizzazione **[!UICONTROL View Destinations]** e **[!UICONTROL Manage Destinations]** [controllo di accesso](/help/access-control/home.md#permissions) per Experience Platform. Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi alla destinazione, seguire le istruzioni per [creare una connessione di destinazione](/help/destinations/ui/connect-destination.md) utilizzando l&#39;interfaccia utente di Experience Platform. Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle sottosezioni seguenti.

### Autenticarsi nella destinazione {#authenticate}

Per connettersi alla destinazione, fornire il seguente parametro nella sezione [!UICONTROL Connection type], quindi selezionare **[!UICONTROL Connect to destination]**:

* **[!UICONTROL Account or Advertiser Key]**: [!UICONTROL Source Key] viene generato quando viene creata un&#39;origine [Real-Time CDP nell&#39;interfaccia utente di DSP](https://experienceleague.adobe.com/docs/advertising-cloud/dsp/audiences/sources/source-create.html). Il team del tuo account Adobe condividerà con te questa chiave dopo la creazione dell’origine.

![Schermata della sezione del tipo di connessione che mostra il campo Account o Chiave inserzionista.](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/authenticate-destination.png)

### Inserire i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

* **[!UICONTROL Name]**: nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Description]**: una descrizione che ti aiuterà a identificare questa destinazione in futuro.

![Schermata dei campi dei dettagli della destinazione che mostra gli input di Nome e Descrizione.](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/destination-details.png)

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli della connessione di destinazione, selezionare **[!UICONTROL Next]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
>
>* Per attivare i dati, sono necessarie le **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare le identità, è necessario disporre dell&#39;autorizzazione **[!UICONTROL View Identity Graph]** [per il controllo degli accessi](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Leggi [Attivare profili e tipi di pubblico nelle destinazioni di esportazione del pubblico di streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per le istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione.

### Mappare attributi e identità {#map}

Puoi scegliere gli ID da inviare ad Adobe Advertising DSP. Per impostazione predefinita, gli identificatori dei cookie sono selezionati per l’inserzionista. È inoltre possibile aggiungere [!UICONTROL Hashed Email], [!UICONTROL IDFA] e [!UICONTROL GAID].

Per istruzioni, consulta [Mappare attributi e identità](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping).

![Schermata della sezione di mappatura identità che mostra gli identificatori dei cookie, le opzioni e-mail con hash, IDFA e GAID.](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/identity-mapping.png)

## Convalidare l’esportazione dei dati {#exported-data}

Per verificare che i dati del pubblico siano stati condivisi con Advertising Cloud, verifica quanto segue:

* Flusso di dati nella destinazione [!DNL Real-Time CDP] completato.

* In DSP, il pubblico è disponibile quando crei o modifichi un pubblico da **[!UICONTROL Audiences]** > **[!UICONTROL All Audiences]** o dall&#39;interno della sezione **[!UICONTROL Audience Targeting]** delle impostazioni di posizionamento. Il pubblico deve essere visibile nella scheda [!UICONTROL Adobe Segments] della cartella [!UICONTROL Real-Time CDP].

![Tipi di pubblico di Real-Time CDP nelle impostazioni del pubblico di DSP](/help/destinations/assets/catalog/advertising/adobe-advertising-cloud-connection/segments-in-dsp.png)

## Utilizzo dei dati e governance {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, vedi [Panoramica sulla governance dei dati](/help/data-governance/home.md).
