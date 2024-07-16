---
keywords: linkedin connessione;linkedin connessione;linkedin destinazioni;linkedin connessione;linkedin destinazioni;linkedin;
title: Connessione LinkedIn Matched Audiences
description: Attiva profili per le campagne LinkedIn per il targeting, la personalizzazione e l’eliminazione del pubblico, in base alle e-mail con hash.
exl-id: 74c233e9-161a-4e4a-98ef-038a031feff0
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1099'
ht-degree: 4%

---

# Connessione [!DNL LinkedIn Matched Audiences]

## Panoramica {#overview}

Attiva profili per le campagne [!DNL LinkedIn] per il targeting, la personalizzazione e l&#39;eliminazione del pubblico, in base alle e-mail con hash e agli ID dei dispositivi mobili.

![Destinazione LinkedIn nell&#39;interfaccia utente di Adobe Experience Platform](../../assets/catalog/social/linkedin/catalog.png)

## Casi d’uso

Per aiutarti a capire meglio come e quando utilizzare la destinazione [!DNL LinkedIn Matched Audiences], ecco un caso d&#39;uso che i clienti di Adobe Experience Platform possono risolvere utilizzando questa funzione.

Una società di software organizza una conferenza e desidera tenersi in contatto con i partecipanti e mostrare loro offerte personalizzate in base al loro stato di partecipazione alla conferenza. L&#39;azienda può acquisire gli indirizzi e-mail o gli ID di dispositivi mobili dal proprio [!DNL CRM] in Adobe Experience Platform. Quindi, possono creare tipi di pubblico dai propri dati offline e inviarli alla piattaforma social [!DNL LinkedIn], ottimizzando le spese pubblicitarie.

## Identità supportate {#supported-identities}

[!DNL LinkedIn Matched Audiences] supporta l&#39;attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/features/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Seleziona questa identità di destinazione quando l&#39;identità di origine è uno spazio dei nomi GAID. |
| IDFA | Apple ID per inserzionisti | Selezionare questa identità di destinazione quando l&#39;identità di origine è uno spazio dei nomi IDFA. |
| email_lc_sha256 | Indirizzi e-mail con hash con algoritmo SHA256 | Adobe Experience Platform supporta sia gli indirizzi di posta elettronica in testo normale che quelli con hash SHA256. Segui le istruzioni riportate nella sezione [Requisiti di corrispondenza ID](#id-matching-requirements-id-matching-requirements) e utilizza gli spazi dei nomi appropriati rispettivamente per le e-mail in testo normale e con hash. Se il campo di origine contiene attributi senza hash, selezionare l&#39;opzione **[!UICONTROL Applica trasformazione]** per impostare [!DNL Platform] per l&#39;hashing automatico dei dati all&#39;attivazione. |

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
| Tipo di esportazione | **[!UICONTROL Esportazione pubblico]** | Stai esportando tutti i membri di un pubblico con gli identificatori (nome, numero di telefono e altri) utilizzati nella destinazione [!DNL LinkedIn Matched Audiences]. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni sulle [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Prerequisiti per l’account linkedIn {#LinkedIn-account-prerequisites}

Prima di poter utilizzare la destinazione [!UICONTROL LinkedIn Matched Audience], assicurati che il tuo account [!DNL LinkedIn Campaign Manager] disponga del livello di autorizzazione [!DNL Creative Manager] o superiore.

Per informazioni su come modificare le autorizzazioni utente di [!DNL LinkedIn Campaign Manager], consulta [Aggiungere, modificare e rimuovere le autorizzazioni utente per gli account Advertising](https://www.linkedin.com/help/lms/answer/5753) nella documentazione di LinkedIn.

## Requisiti di corrispondenza ID {#id-matching-requirements}

[!DNL LinkedIn Matched Audiences] non richiede l&#39;invio di informazioni personali (PII, personally identifiable information) in chiaro. Pertanto, i tipi di pubblico attivati in [!DNL LinkedIn Matched Audiences] possono essere ricavati da *identificatori con hash*, ad esempio indirizzi e-mail o ID di dispositivi mobili.

A seconda del tipo di ID inseriti in Adobe Experience Platform, devi rispettare i requisiti corrispondenti.

## Requisiti di hashing delle e-mail {#email-hashing-requirements}

Puoi eseguire l&#39;hashing degli indirizzi e-mail prima di acquisirli in Adobe Experience Platform, oppure utilizzare gli indirizzi e-mail in chiaro nell&#39;Experience Platform e disporre di [!DNL Platform] hashing al momento dell&#39;attivazione.

Per informazioni sull&#39;acquisizione degli indirizzi e-mail in Experience Platform, consulta la [panoramica sull&#39;acquisizione batch](/help/ingestion/batch-ingestion/overview.md) e la [panoramica sull&#39;acquisizione in streaming](/help/ingestion/streaming-ingestion/overview.md).

Se scegli di eseguire l’hash degli indirizzi e-mail da solo, assicurati di soddisfare i seguenti requisiti:

* Taglia tutti gli spazi iniziali e finali dalla stringa e-mail. Ad esempio: `johndoe@example.com`, non `<space>johndoe@example.com<space>`;
* Quando esegui l’hashing delle stringhe e-mail, assicurati di eseguire l’hashing della stringa in minuscolo;
   * Esempio: `example@email.com`, non `EXAMPLE@EMAIL.COM`;
* Assicurati che la stringa con hash sia tutta in minuscolo
   * Esempio: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, non `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* Non salare la corda.

>[!NOTE]
>
>I dati degli spazi dei nomi senza hash vengono automaticamente sottoposti a hashing da [!DNL Platform] al momento dell&#39;attivazione.
> L&#39;hash dei dati di origine degli attributi non viene eseguito automaticamente.
> 
> Durante il passaggio [Mappatura identità](../../ui/activate-segment-streaming-destinations.md#mapping), se il campo di origine contiene attributi senza hash, seleziona l&#39;opzione **[!UICONTROL Applica trasformazione]** per fare in modo che [!DNL Platform] esegua automaticamente l&#39;hashing dei dati all&#39;attivazione.
> 
> L&#39;opzione **[!UICONTROL Applica trasformazione]** viene visualizzata solo quando si selezionano gli attributi come campi di origine. Non viene visualizzato quando si scelgono gli spazi dei nomi.

![Trasformazione mappatura identità](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, sono necessarie le **[!UICONTROL Destinazioni visualizzazione]** e le **[!UICONTROL Autorizzazioni di gestione delle destinazioni]** [per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

Il video seguente illustra inoltre i passaggi per configurare una destinazione [!DNL LinkedIn Matched Audiences] e attivare i tipi di pubblico.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>L’interfaccia utente di Experience Platform viene aggiornata frequentemente e potrebbe essere cambiata dopo la registrazione del video. Per informazioni aggiornate, fare riferimento al [tutorial sulla configurazione della destinazione](../../ui/connect-destination.md).

### Autenticarsi nella destinazione {#authenticate}

1. Trovare la destinazione [!DNL LinkedIn Matched Audiences] nel catalogo di destinazione e selezionare **[!UICONTROL Configura]**.
2. Selezionare **[!UICONTROL Connetti alla destinazione]**.
   ![Autentica in LinkedIn](/help/destinations/assets/catalog/social/linkedin/authenticate-linkedin-destination.png)
3. Immetti le credenziali LinkedIn e seleziona **Accedi**.

### Inserire i dettagli della destinazione {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_linkedin_accountid"
>title="ID account"
>abstract="ID del tuo account Gestione campagne di LinkedIn. Puoi trovare questo ID nel tuo account Gestione campagne di LinkedIn."

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

* **[!UICONTROL Nome]**: un nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL ID account]**: [!DNL LinkedIn Campaign Manager Account ID]. Puoi trovare questo ID nel tuo account [!DNL LinkedIn Campaign Manager].

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli per la connessione di destinazione, seleziona **[!UICONTROL Avanti]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Visualizza grafo identità]** [Controllo di accesso](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Per istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione, consulta [Attivare i dati del pubblico nelle destinazioni di esportazione del pubblico in streaming](../../ui/activate-segment-streaming-destinations.md).

## Dati esportati {#exported-data}

Se l&#39;attivazione ha esito positivo, verrà creato un pubblico personalizzato [!DNL LinkedIn] a livello di programmazione in [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login). L’iscrizione al pubblico viene aggiunta e rimossa quando gli utenti sono qualificati o squalificati per i tipi di pubblico attivati.

>[!TIP]
>
>L&#39;integrazione tra Adobe Experience Platform e [!DNL LinkedIn Matched Audiences] supporta i backfill cronologici del pubblico. Tutti i requisiti storici del pubblico vengono inviati a [!DNL LinkedIn] quando attivi i tipi di pubblico nella destinazione.
