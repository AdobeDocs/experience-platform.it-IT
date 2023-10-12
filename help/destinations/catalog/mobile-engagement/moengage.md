---
title: Connessione moenging
description: Moengi è una piattaforma di coinvolgimento dei clienti che potenzia in tempo reale le interazioni incentrate sul cliente tra consumatori e marchi.
last-substantial-update: 2023-10-11T00:00:00Z
source-git-commit: 3d5a3ce18e7f1c0e06246faf8ec4403871e1a1a9
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 0%

---


# Connessione [!DNL Moengage]

## Panoramica {#overview}

Utilizza il [!DNL Moengage] destinazione per collegare e mappare i dati di Adobe (attributi utente, segmenti ed eventi) a MoEngage in tempo reale. I clienti possono quindi agire su questi dati, distribuendo esperienze personalizzate e mirate.

Ad Adobe, l’integrazione è molto semplice e intuitiva. È sufficiente prendere un profilo utente di Adobe e mapparlo su un attributo utente MoEngage.

>[!IMPORTANT]
>
>Il connettore di destinazione e la pagina della documentazione vengono creati e gestiti da *Moengi* team. Per eventuali richieste di informazioni o richieste di aggiornamento, contattatele direttamente all&#39;indirizzo *`[amc-support@amazon.com](https://help.moengage.com/hc/en-us)`.*

## Casi d’uso {#use-cases}

Un addetto al marketing desidera eseguire il targeting di un segmento di utenti (integrato in Adobe Experience Platform) tramite [!DNL Moengage] campagne. Inoltre, desiderano personalizzare il contenuto della campagna in base agli attributi dei profili Adobe Experience Platform. Con questa integrazione, gli utenti e gli attributi vengono aggiornati in MoEngage non appena segmenti e profili vengono aggiornati in Adobe Experience Platform.

## Prerequisiti {#prerequisites}

Prima di poter inviare i dati Adobe Experience Platform a [!DNL Moengage], tieni presente i seguenti prerequisiti:

* Per utilizzare la destinazione MoEngage con Adobe Experience Platform, gli utenti devono prima avere accesso al proprio [!DNL Moengage] Account. Visita la pagina seguente per registrarti o accedere al tuo account MoEngage: https://app.moengage.com


## Identità supportate {#supported-identities}

[!DNL Moengage] supporta l’attivazione delle identità descritte nella tabella seguente.

| Identità di destinazione | Descrizione | Considerazioni |
|---|------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------|
| user_id | Identificatore univoco che identifica in modo univoco un profilo utente in [!DNL Moengage] di rete. | Questo identificatore supporta il tipo di stringa. È necessario specificare user_id o anonymous_id |
| anonymous_id | Un altro identificatore di un profilo utente sconosciuto, ovvero un profilo che non esiste nel sistema. | Questo identificatore supporta il tipo di stringa. È necessario specificare user_id o anonymous_id |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Stai esportando tutti i membri di un segmento (pubblico) con gli identificatori (user_id, anonymous_id) insieme agli attributi personalizzati definiti da te esportato in [!DNL Moengage]. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experienci Platform in base alla valutazione dei segmenti, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni su [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Connetti alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autentica nella destinazione {#authenticate}

Per autenticare nella destinazione, compila i campi obbligatori e seleziona **[!UICONTROL Connetti alla destinazione]**.

![Autenticazione di destinazione Moengi](../../assets/catalog/mobile-engagement/moengage/authentication.png)

### Inserisci i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.
![Autenticazione di destinazione Moengi](../../assets/catalog/mobile-engagement/moengage/settings.png)
* **[!UICONTROL NOME UTENTE]**: ID APP DATI della pagina delle impostazioni di [!DNL Moengage] dashboard.
* **[!UICONTROL PASSWORD]**: CHIAVE APP DATI dalla pagina delle impostazioni di [!DNL Moengage] dashboard.

![Autenticazione di destinazione Moengi](../../assets/catalog/mobile-engagement/moengage/destination_details.png)

* **[!UICONTROL Nome]**: nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL Regione]**: app *data center*.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completate le informazioni sulla connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Consulta [Attiva i dati del pubblico nelle destinazioni di esportazione di segmenti di streaming](../../ui/activate-segment-streaming-destinations.md) per istruzioni sull’attivazione dei segmenti di pubblico in questa destinazione.

### Mappare attributi e identità {#map}

Per inviare correttamente i dati sul pubblico da [!DNL Adobe Experience Platform] al [!DNL Moengage] destinazione, devi passare attraverso il passaggio di mappatura dei campi.

La mappatura consiste nella creazione di un collegamento tra [!DNL Experience Data Model] (XDM) campi schema nel tuo [!DNL Platform] e i corrispondenti equivalenti dalla destinazione di destinazione.

Per mappare correttamente i campi XDM su [!DNL Moengage] campi di destinazione, effettua le seguenti operazioni:

In [!UICONTROL Mappatura] passaggio, seleziona **[!UICONTROL Casella di controllo]**.

![Mappatura aggiunta destinazione moenging](../../assets/catalog/mobile-engagement/moengage/segments.png)

In [!UICONTROL Mappatura] passaggio, seleziona **[!UICONTROL Aggiungi nuova mappatura]**.

![Mappatura aggiunta destinazione moenging](../../assets/catalog/mobile-engagement/moengage/mapping.png)

In [!UICONTROL Campo di origine] , selezionare il pulsante freccia accanto al campo vuoto.

![Mappatura origine destinazione mobile](../../assets/catalog/mobile-engagement/moengage/mapping-source.png)

In [!UICONTROL Seleziona campo di origine] è possibile scegliere tra due categorie di campi XDM:
* [!UICONTROL Seleziona attributi]: utilizza questa opzione per mappare un campo specifico dallo schema XDM a [!DNL Moengage] attributo.

![Attributo di origine mappatura destinazione moenging](../../assets/catalog/mobile-engagement/moengage/mapping-attributes.png)

Scegli il campo di origine, quindi seleziona **[!UICONTROL Seleziona]**.

In [!UICONTROL Campo di destinazione] , seleziona l’icona di mappatura a destra del campo.

![Mappatura destinazione di destinazione Moengagement](../../assets/catalog/mobile-engagement/moengage/mapping-target.png)

In [!UICONTROL Seleziona campo di destinazione] è possibile scegliere tra due categorie di campi di destinazione:
* [!UICONTROL Seleziona lo spazio dei nomi dell’identità]: utilizza questa opzione per mappare [!DNL Platform] spazi dei nomi di identità da [!DNL Moengage] spazi dei nomi di identità.
* [!UICONTROL Seleziona attributi personalizzati]: utilizza questa opzione per mappare gli attributi XDM su personalizzati [!DNL Moengage] attributi definiti in [!DNL Moengage] account. <br> Puoi anche utilizzare questa opzione per rinominare gli attributi XDM esistenti in [!DNL Moengage]. Ad esempio, la mappatura di un `lastName` Attributo XDM a un attributo personalizzato `Last_Name` attributo in [!DNL Moengage], creerà il `Last_Name` attributo in [!DNL Moengage], se non esiste già, e mappa `lastName` Attributo XDM.

![Campi di mappatura destinazione di spostamento](../../assets/catalog/mobile-engagement/moengage/mapping-target-fields.png)

Scegli il campo di destinazione, quindi seleziona **[!UICONTROL Seleziona]**.

Ora dovresti visualizzare la mappatura dei campi nell’elenco.

![Mappatura destinazione Moengagement completata](../../assets/catalog/mobile-engagement/moengage/mapping-complete.png)

Per aggiungere altre mappature, ripeti i passaggi precedenti.

## Dati esportati / Convalida esportazione dati {#exported-data}

Per verificare se i dati sono stati esportati correttamente in [!DNL Moengage] destinazione, vai al profilo utente sul tuo [!DNL Moengage] account. Visualizzerai un attributo utente denominato Segmento AEP.

![Mappatura destinazione Moengagement completata](../../assets/catalog/mobile-engagement/moengage/validation.png)

## Utilizzo dei dati e governance {#data-usage-governance}

Tutti [!DNL Adobe Experience Platform] le destinazioni sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, leggi [Panoramica sulla governance dei dati](/help/data-governance/home.md).

