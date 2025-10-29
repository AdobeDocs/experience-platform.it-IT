---
title: Connessione moenging
description: Moengi è una piattaforma di coinvolgimento dei clienti che potenzia in tempo reale le interazioni incentrate sul cliente tra consumatori e marchi.
last-substantial-update: 2023-10-11T00:00:00Z
exl-id: 051f1a10-3c41-4c0a-b187-bf80de0565f0
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 2%

---

# Connessione [!DNL Moengage]

## Panoramica {#overview}

Utilizza la destinazione [!DNL Moengage] per connettere e mappare i dati di Adobe (attributi utente, segmenti ed eventi) a MoEngage in tempo reale. I clienti possono quindi agire su questi dati, distribuendo esperienze personalizzate e mirate.

Con Adobe, l’integrazione è molto semplice e intuitiva. È sufficiente acquisire un profilo utente di Adobe e mapparlo su un attributo utente di MoEngage.

>[!IMPORTANT]
>
>Il connettore di destinazione e la pagina della documentazione vengono creati e gestiti dal team *Moengi*. Per qualsiasi richiesta di informazioni o di aggiornamento, contattarli direttamente all&#39;indirizzo *`https://help.moengage.com/hc/en-us`.*

## Casi d’uso {#use-cases}

Un addetto al marketing desidera eseguire il targeting di un segmento di utenti (integrato in Adobe Experience Platform) tramite [!DNL Moengage] campagne. Inoltre, desiderano personalizzare il contenuto della campagna in base agli attributi dei profili Adobe Experience Platform. Con questa integrazione, gli utenti e gli attributi vengono aggiornati in MoEngage non appena segmenti e profili vengono aggiornati in Adobe Experience Platform.

## Prerequisiti {#prerequisites}

Prima di poter inviare i dati Adobe Experience Platform a [!DNL Moengage], tieni presente i seguenti prerequisiti:

* Per utilizzare la destinazione MoEngage con Adobe Experience Platform, gli utenti devono prima avere accesso al proprio account [!DNL Moengage]. Visita la pagina seguente per registrarti o accedere al tuo account MoEngage: https://app.moengage.com


## Identità supportate {#supported-identities}

[!DNL Moengage] supporta l&#39;attivazione delle identità descritte nella tabella seguente.

| Identità di destinazione | Descrizione | Considerazioni |
|---|------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------|
| user_id | Identificatore univoco che identifica in modo univoco un profilo utente nel sistema [!DNL Moengage]. | Questo identificatore supporta il tipo di stringa. È necessario specificare user_id o anonymous_id |
| anonymous_id | Un altro identificatore di un profilo utente sconosciuto, ovvero un profilo che non esiste nel sistema. | Questo identificatore supporta il tipo di stringa. È necessario specificare user_id o anonymous_id |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
|---------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Tipo di esportazione | **[!UICONTROL Profile-based]** | Stai esportando tutti i membri di un segmento (pubblico) con gli identificatori (user_id, anonymous_id) insieme agli attributi personalizzati definiti da te esportati in [!DNL Moengage]. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione dei segmenti, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni sulle [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, sono necessarie le **[!UICONTROL View Destinations]** e le **[!UICONTROL Manage Destinations]** [autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autenticarsi nella destinazione {#authenticate}

Per autenticare nella destinazione, compilare i campi obbligatori e selezionare **[!UICONTROL Connect to destination]**.

![Autenticazione destinazione moenging](../../assets/catalog/mobile-engagement/moengage/authentication.png)

### Inserire i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.
![Autenticazione destinazione moenging](../../assets/catalog/mobile-engagement/moengage/settings.png)

* **[!UICONTROL USERNAME]**: ID APP DATI della pagina delle impostazioni del dashboard [!DNL Moengage].
* **[!UICONTROL PASSWORD]**: CHIAVE APP DATI dalla pagina delle impostazioni del dashboard [!DNL Moengage].

![Autenticazione destinazione moenging](../../assets/catalog/mobile-engagement/moengage/destination_details.png)

* **[!UICONTROL Name]**: nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Description]**: una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL Region]**: app *data center*.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli della connessione di destinazione, selezionare **[!UICONTROL Next]**.

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, sono necessarie le **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per istruzioni sull&#39;attivazione dei segmenti di pubblico in questa destinazione, consulta [Attiva dati pubblico nelle destinazioni di esportazione dei segmenti di streaming](../../ui/activate-segment-streaming-destinations.md).

### Mappare attributi e identità {#map}

Per inviare correttamente i dati sul pubblico da [!DNL Adobe Experience Platform] alla destinazione [!DNL Moengage], è necessario eseguire il passaggio di mappatura dei campi.

La mappatura consiste nella creazione di un collegamento tra i campi dello schema [!DNL Experience Data Model] (XDM) nell&#39;account [!DNL Experience Platform] e gli equivalenti corrispondenti dalla destinazione.

Per mappare correttamente i campi XDM ai campi di destinazione [!DNL Moengage], effettua le seguenti operazioni:

Nel passaggio [!UICONTROL Mapping], selezionare **[!UICONTROL Checkbox]**.

![Mappatura aggiunta destinazione mobile](../../assets/catalog/mobile-engagement/moengage/segments.png)

Nel passaggio [!UICONTROL Mapping], selezionare **[!UICONTROL Add new mapping]**.

![Mappatura aggiunta destinazione mobile](../../assets/catalog/mobile-engagement/moengage/mapping.png)

Nella sezione [!UICONTROL Source Field], selezionare il pulsante freccia accanto al campo vuoto.

![Mappatura Source di destinazione Moenging](../../assets/catalog/mobile-engagement/moengage/mapping-source.png)

Nella finestra [!UICONTROL Select source field] è possibile scegliere tra due categorie di campi XDM:

* [!UICONTROL Select attributes]: utilizzare questa opzione per mappare un campo specifico dallo schema XDM all&#39;attributo [!DNL Moengage].

![Attributo Source mappatura destinazione moenging](../../assets/catalog/mobile-engagement/moengage/mapping-attributes.png)

Scegli il campo di origine, quindi seleziona **[!UICONTROL Select]**.

Nella sezione [!UICONTROL Target Field], seleziona l&#39;icona di mappatura a destra del campo.

![Mappatura destinazione moengdestinazione](../../assets/catalog/mobile-engagement/moengage/mapping-target.png)

Nella finestra [!UICONTROL Select target field] è possibile scegliere tra due categorie di campi di destinazione:

* [!UICONTROL Select identity namespace]: utilizzare questa opzione per mappare gli spazi dei nomi di identità [!DNL Experience Platform] a [!DNL Moengage].
* [!UICONTROL Select custom attributes]: utilizzare questa opzione per mappare gli attributi XDM agli attributi [!DNL Moengage] personalizzati definiti nell&#39;account [!DNL Moengage]. <br> È inoltre possibile utilizzare questa opzione per rinominare gli attributi XDM esistenti in [!DNL Moengage]. Ad esempio, il mapping di un attributo XDM `lastName` a un attributo `Last_Name` personalizzato in [!DNL Moengage] creerà l&#39;attributo `Last_Name` in [!DNL Moengage], se non esiste già, e mapperà l&#39;attributo XDM `lastName` a esso.

![Campi di mappatura destinazione moenging](../../assets/catalog/mobile-engagement/moengage/mapping-target-fields.png)

Scegli il campo di destinazione, quindi seleziona **[!UICONTROL Select]**.

Ora dovresti visualizzare la mappatura dei campi nell’elenco.

![Mappatura destinazione moenging completata](../../assets/catalog/mobile-engagement/moengage/mapping-complete.png)

Per aggiungere altre mappature, ripeti i passaggi precedenti.

## Dati esportati / Convalida esportazione dati {#exported-data}

Per verificare se i dati sono stati esportati correttamente nella destinazione [!DNL Moengage], passare al profilo utente nell&#39;account [!DNL Moengage]. In questo caso è necessario trovare un attributo utente denominato `AEPSegments`, creato automaticamente e gli altri attributi personalizzati mappati nei passaggi precedenti di Adobe Experience Platform.

`AEPSegments` è un attributo di tipo array in [!DNL Moengage]. Elenca tutti i nomi dei tipi di pubblico di Adobe a cui l’utente è associato in Experience Platform.


![Mappatura destinazione moenging completata](../../assets/catalog/mobile-engagement/moengage/validation.png)

## Utilizzo dei dati e governance {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, leggere la [Panoramica sulla governance dei dati](/help/data-governance/home.md).
