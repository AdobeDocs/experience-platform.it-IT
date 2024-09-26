---
keywords: mobile; braze; messaggistica;
title: Connessione di brasatura
description: Braze è una piattaforma completa per il coinvolgimento dei clienti che offre esperienze pertinenti e memorabili tra i clienti e i marchi che amano.
last-substantial-update: 2024-08-20T00:00:00Z
exl-id: 508e79ee-7364-4553-b153-c2c00cc85a73
source-git-commit: 2b84b5106105339ab243a9f4412b47692caedf3c
workflow-type: tm+mt
source-wordcount: '1125'
ht-degree: 2%

---

# Connessione [!DNL Braze]

## Panoramica {#overview}

La destinazione [!DNL Braze] consente di inviare i dati del profilo a [!DNL Braze].

[!DNL Braze] è una piattaforma completa per il coinvolgimento dei clienti che offre esperienze significative e memorabili tra i clienti e i marchi che amano.

Per inviare i dati del profilo a [!DNL Braze], è necessario prima connettersi alla destinazione.

## Specifiche della destinazione {#specifics}

Prendere nota dei dettagli seguenti specifici per la destinazione [!DNL Braze]:

* [!DNL Adobe Experience Platform] tipi di pubblico esportati in [!DNL Braze] con l&#39;attributo `AdobeExperiencePlatformSegments`.

>[!NOTE]
>
>Tenere presente che l&#39;invio di attributi personalizzati aggiuntivi a [!DNL Braze] può causare un aumento del consumo di punti dati di [!DNL Braze]. Prima di inviare attributi personalizzati aggiuntivi, rivolgiti al tuo account manager [!DNL Braze].

## Casi d’uso {#use-cases}

In qualità di addetto al marketing, desidero indirizzare l&#39;attività agli utenti in una destinazione di interazione mobile, con il pubblico integrato in [!DNL Adobe Experience Platform]. Desidero inoltre fornire loro esperienze personalizzate, basate sugli attributi dei loro profili [!DNL Adobe Experience Platform], non appena i tipi di pubblico e i profili vengono aggiornati in [!DNL Adobe Experience Platform].

## Identità supportate {#supported-identities}

[!DNL Braze] supporta l&#39;attivazione delle identità descritte nella tabella seguente.

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| external_id | Identificatore [!DNL Braze] personalizzato che supporta la mappatura di qualsiasi identità. | Puoi inviare qualsiasi [identità](../../../identity-service/features/namespaces.md) alla destinazione [!DNL Braze], purché mappata alla [!DNL Braze] [`external_id`](https://www.braze.com/docs/api/basics/#external-user-id-explanation). |

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
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome) e/o identità, in base alla mappatura dei campi.[!DNL Adobe Experience Platform] tipi di pubblico esportati in [!DNL Braze] con l&#39;attributo `AdobeExperiencePlatformSegments`. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni sulle [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, sono necessarie le **[!UICONTROL Destinazioni visualizzazione]** e le **[!UICONTROL Autorizzazioni di gestione delle destinazioni]** [per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autenticarsi nella destinazione {#authenticate}

Per eseguire l&#39;autenticazione nella destinazione, compilare i campi obbligatori e selezionare **[!UICONTROL Connetti alla destinazione]**.

* **[!UICONTROL Braze token account]**: questa è la tua chiave [!DNL Braze] [!DNL API]. Le istruzioni dettagliate su come ottenere la chiave [!DNL API] sono disponibili qui: [Panoramica chiave REST API](https://www.braze.com/docs/api/api_key/).

### Inserire i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

* **[!UICONTROL Nome]**: immetti un nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: immetti una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL Istanza endpoint]**: chiedi al tuo rappresentante [!DNL Braze] quale istanza endpoint utilizzare.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli per la connessione di destinazione, seleziona **[!UICONTROL Avanti]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Visualizza grafo identità]** [Controllo di accesso](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Per istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione, consulta [Attivare i dati del pubblico nelle destinazioni di esportazione del pubblico in streaming](../../ui/activate-segment-streaming-destinations.md).

## Considerazioni sulla mappatura {#mapping-considerations}

Per inviare correttamente i dati sul pubblico da [!DNL Adobe Experience Platform] alla destinazione [!DNL Braze], è necessario eseguire il passaggio di mappatura dei campi.

La mappatura consiste nella creazione di un collegamento tra i campi dello schema [!DNL Experience Data Model] (XDM) nell&#39;account [!DNL Platform] e gli equivalenti corrispondenti dalla destinazione.

Per mappare correttamente i campi XDM ai campi di destinazione [!DNL Braze], effettua le seguenti operazioni:

Nel passaggio [!UICONTROL Mapping], fare clic su **[!UICONTROL Aggiungi nuovo mapping]**.

![Mappatura per aggiunta destinazione Braze](../../assets/catalog/mobile-engagement/braze/mapping.png)

Nella sezione [!UICONTROL Campo Source] fare clic sul pulsante freccia accanto al campo vuoto.

![Mappatura Source destinazione Braze](../../assets/catalog/mobile-engagement/braze/mapping-source.png)

Nella finestra [!UICONTROL Seleziona campo di origine] è possibile scegliere tra due categorie di campi XDM:
* [!UICONTROL Seleziona attributi]: utilizza questa opzione per mappare un campo specifico dallo schema XDM a un attributo [!DNL Braze].

![Mappatura destinazione Braze Attributo Source](../../assets/catalog/mobile-engagement/braze/mapping-attributes.png)

* [!UICONTROL Selezionare lo spazio dei nomi dell&#39;identità]: utilizzare questa opzione per mappare uno spazio dei nomi dell&#39;identità [!DNL Platform] a uno spazio dei nomi [!DNL Braze].

![Mappatura destinazione Braze Spazio dei nomi Source](../../assets/catalog/mobile-engagement/braze/mapping-namespaces.png)

Scegli il campo di origine, quindi fai clic su **[!UICONTROL Seleziona]**.

Nella sezione [!UICONTROL Campo di destinazione], fai clic sull&#39;icona di mappatura a destra del campo.

![Mappatura destinazione Braze](../../assets/catalog/mobile-engagement/braze/mapping-target.png)

Nella finestra [!UICONTROL Seleziona campo di destinazione] è possibile scegliere tra due categorie di campi di destinazione:
* [!UICONTROL Seleziona lo spazio dei nomi dell&#39;identità]: utilizzare questa opzione per mappare gli spazi dei nomi dell&#39;identità [!DNL Platform] agli spazi dei nomi dell&#39;identità [!DNL Braze].
* [!UICONTROL Seleziona attributi personalizzati]: utilizza questa opzione per mappare gli attributi XDM agli attributi [!DNL Braze] personalizzati definiti nell&#39;account [!DNL Braze]. <br> È inoltre possibile utilizzare questa opzione per rinominare gli attributi XDM esistenti in [!DNL Braze]. Ad esempio, il mapping di un attributo XDM `lastName` a un attributo `Last_Name` personalizzato in [!DNL Braze] creerà l&#39;attributo `Last_Name` in [!DNL Braze], se non esiste già, e mapperà l&#39;attributo XDM `lastName` a esso.

![Sfumatura campi di mappatura destinazione](../../assets/catalog/mobile-engagement/braze/mapping-target-fields.png)

Scegli il campo di destinazione, quindi fai clic su **[!UICONTROL Seleziona]**.

Ora dovresti visualizzare la mappatura dei campi nell’elenco.

![Mappatura destinazione Braze completata](../../assets/catalog/mobile-engagement/braze/mapping-complete.png)

Per aggiungere altre mappature, ripeti i passaggi precedenti.

## Esempio di mappatura {#mapping-example}

Supponiamo che lo schema del profilo XDM e l&#39;istanza [!DNL Braze] contengano i seguenti attributi e identità:

|  | Schema profilo XDM | Istanza [!DNL Braze] |
|---|---|---|
| Attributi | <ul><li><code>person.name.firstName</code></li><li><code>nome.cognome.persona</code></li><li><code>cellulare.numero</code></li></ul> | <ul><li><code>Nome</code></li><li><code>Cognome</code></li><li><code>NumeroTelefono</code></li></ul> |
| Identità | <ul><li><code>E-mail</code></li><li><code>Google Ad ID (GAID)</code></li><li><code>ID Apple per inserzionisti (IDFA)</code></li></ul> | <ul><li><code>external_id</code></li></ul> |

La mappatura corretta sarà simile alla seguente:

![Esempio di mappatura della destinazione Braze](../../assets/catalog/mobile-engagement/braze/mapping-example.png)

## Dati esportati {#exported-data}

Per verificare se i dati sono stati esportati correttamente nella destinazione [!DNL Braze], controllare l&#39;account [!DNL Braze]. [!DNL Adobe Experience Platform] tipi di pubblico esportati in [!DNL Braze] con l&#39;attributo `AdobeExperiencePlatformSegments`.

## Risoluzione dei problemi {#troubleshooting}

**Ho ricevuto un errore di timeout durante l&#39;attivazione dei miei tipi di pubblico in questa destinazione. Cosa devo fare?**

Talvolta, l’attivazione del pubblico su questa destinazione può causare un errore di timeout. Questo errore non indica sempre un problema di attivazione.

Se ricevi un errore di timeout, controlla le dimensioni del pubblico nella piattaforma di destinazione. Se la dimensione del pubblico è corretta, l’integrazione funziona come previsto.

## Utilizzo dei dati e governance {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, vedi [Panoramica sulla governance dei dati](../../../data-governance/home.md).
