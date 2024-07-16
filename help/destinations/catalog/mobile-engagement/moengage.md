---
title: Connessione moenging
description: Moengi è una piattaforma di coinvolgimento dei clienti che potenzia in tempo reale le interazioni incentrate sul cliente tra consumatori e marchi.
last-substantial-update: 2023-10-11T00:00:00Z
exl-id: 051f1a10-3c41-4c0a-b187-bf80de0565f0
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 2%

---

# Connessione [!DNL Moengage]

## Panoramica {#overview}

Utilizza la destinazione [!DNL Moengage] per connettere e mappare i dati di Adobe (attributi utente, segmenti ed eventi) a MoEngage in tempo reale. I clienti possono quindi agire su questi dati, distribuendo esperienze personalizzate e mirate.

Ad Adobe, l’integrazione è molto semplice e intuitiva. È sufficiente prendere un profilo utente di Adobe e mapparlo su un attributo utente MoEngage.

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
---------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Tipo di esportazione | **[!UICONTROL Basato su profilo]** | Stai esportando tutti i membri di un segmento (pubblico) con gli identificatori (user_id, anonymous_id) insieme agli attributi personalizzati definiti da te esportati in [!DNL Moengage]. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione dei segmenti, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni sulle [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, sono necessarie le **[!UICONTROL Destinazioni visualizzazione]** e le **[!UICONTROL Autorizzazioni di gestione delle destinazioni]** [per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autenticarsi nella destinazione {#authenticate}

Per eseguire l&#39;autenticazione nella destinazione, compilare i campi obbligatori e selezionare **[!UICONTROL Connetti alla destinazione]**.

![Autenticazione destinazione moenging](../../assets/catalog/mobile-engagement/moengage/authentication.png)

### Inserire i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.
![Autenticazione destinazione moenging](../../assets/catalog/mobile-engagement/moengage/settings.png)
* **[!UICONTROL NOME UTENTE]**: ID APP DATI della pagina delle impostazioni del dashboard [!DNL Moengage].
* **[!UICONTROL PASSWORD]**: CHIAVE APP DATI dalla pagina delle impostazioni del dashboard [!DNL Moengage].

![Autenticazione destinazione moenging](../../assets/catalog/mobile-engagement/moengage/destination_details.png)

* **[!UICONTROL Nome]**: un nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL Area]**: *datacenter* della tua app.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli per la connessione di destinazione, seleziona **[!UICONTROL Avanti]**.

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per istruzioni sull&#39;attivazione dei segmenti di pubblico in questa destinazione, consulta [Attiva dati pubblico nelle destinazioni di esportazione dei segmenti di streaming](../../ui/activate-segment-streaming-destinations.md).

### Mappare attributi e identità {#map}

Per inviare correttamente i dati sul pubblico da [!DNL Adobe Experience Platform] alla destinazione [!DNL Moengage], è necessario eseguire il passaggio di mappatura dei campi.

La mappatura consiste nella creazione di un collegamento tra i campi dello schema [!DNL Experience Data Model] (XDM) nell&#39;account [!DNL Platform] e gli equivalenti corrispondenti dalla destinazione.

Per mappare correttamente i campi XDM ai campi di destinazione [!DNL Moengage], effettua le seguenti operazioni:

Nel passaggio [!UICONTROL Mappatura], seleziona **[!UICONTROL Casella di controllo]**.

![Mappatura aggiunta destinazione mobile](../../assets/catalog/mobile-engagement/moengage/segments.png)

Nel passaggio [!UICONTROL Mapping], seleziona **[!UICONTROL Aggiungi nuovo mapping]**.

![Mappatura aggiunta destinazione mobile](../../assets/catalog/mobile-engagement/moengage/mapping.png)

Nella sezione [!UICONTROL Campo Source], seleziona il pulsante freccia accanto al campo vuoto.

![Mappatura Source di destinazione Moenging](../../assets/catalog/mobile-engagement/moengage/mapping-source.png)

Nella finestra [!UICONTROL Seleziona campo di origine] è possibile scegliere tra due categorie di campi XDM:
* [!UICONTROL Seleziona attributi]: utilizza questa opzione per mappare un campo specifico dallo schema XDM all&#39;attributo [!DNL Moengage].

![Attributo Source mappatura destinazione moenging](../../assets/catalog/mobile-engagement/moengage/mapping-attributes.png)

Scegli il campo di origine, quindi seleziona **[!UICONTROL Seleziona]**.

Nella sezione [!UICONTROL Campo di destinazione], seleziona l&#39;icona di mappatura a destra del campo.

![Mappatura destinazione moengdestinazione](../../assets/catalog/mobile-engagement/moengage/mapping-target.png)

Nella finestra [!UICONTROL Seleziona campo di destinazione] è possibile scegliere tra due categorie di campi di destinazione:
* [!UICONTROL Seleziona lo spazio dei nomi dell&#39;identità]: utilizzare questa opzione per mappare gli spazi dei nomi dell&#39;identità [!DNL Platform] agli spazi dei nomi dell&#39;identità [!DNL Moengage].
* [!UICONTROL Seleziona attributi personalizzati]: utilizza questa opzione per mappare gli attributi XDM agli attributi [!DNL Moengage] personalizzati definiti nell&#39;account [!DNL Moengage]. <br> È inoltre possibile utilizzare questa opzione per rinominare gli attributi XDM esistenti in [!DNL Moengage]. Ad esempio, il mapping di un attributo XDM `lastName` a un attributo `Last_Name` personalizzato in [!DNL Moengage] creerà l&#39;attributo `Last_Name` in [!DNL Moengage], se non esiste già, e mapperà l&#39;attributo XDM `lastName` a esso.

![Campi di mappatura destinazione moenging](../../assets/catalog/mobile-engagement/moengage/mapping-target-fields.png)

Scegli il campo di destinazione, quindi seleziona **[!UICONTROL Seleziona]**.

Ora dovresti visualizzare la mappatura dei campi nell’elenco.

![Mappatura destinazione moenging completata](../../assets/catalog/mobile-engagement/moengage/mapping-complete.png)

Per aggiungere altre mappature, ripeti i passaggi precedenti.

## Dati esportati / Convalida esportazione dati {#exported-data}

Per verificare se i dati sono stati esportati correttamente nella destinazione [!DNL Moengage], passare al profilo utente nell&#39;account [!DNL Moengage]. Visualizzerai un attributo utente denominato Segmento AEP.

![Mappatura destinazione moenging completata](../../assets/catalog/mobile-engagement/moengage/validation.png)

## Utilizzo dei dati e governance {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, leggere la [Panoramica sulla governance dei dati](/help/data-governance/home.md).
