---
keywords: linkedin connessione;linkedin connessione;linkedin destinazioni;linkedin connessione;linkedin destinazioni;linkedin;
title: Connessione LinkedIn Matched Audiences
description: Attiva profili per le campagne LinkedIn per il targeting, la personalizzazione e l’eliminazione del pubblico, in base alle e-mail con hash.
exl-id: 74c233e9-161a-4e4a-98ef-038a031feff0
source-git-commit: 05e996f9e33e0d8be3d15a9ab3baaaf6d8152b5a
workflow-type: tm+mt
source-wordcount: '1103'
ht-degree: 2%

---

# Connessione [!DNL LinkedIn Matched Audiences]

## Panoramica {#overview}

Attivare i profili per il [!DNL LinkedIn] campagne per il targeting, la personalizzazione e l’eliminazione del pubblico, basate su e-mail con hash e ID di dispositivi mobili.

![Destinazione linkedIn nell’interfaccia utente di Adobe Experience Platform](../../assets/catalog/social/linkedin/catalog.png)

## Casi d’uso

Per aiutarti a capire meglio come e quando utilizzare il [!DNL LinkedIn Matched Audiences] destinazione, ecco un caso d’uso che i clienti Adobe Experience Platform possono risolvere utilizzando questa funzione.

Una società di software organizza una conferenza e desidera tenersi in contatto con i partecipanti e mostrare loro offerte personalizzate in base al loro stato di partecipazione alla conferenza. L’azienda può acquisire gli indirizzi e-mail o gli ID dei dispositivi mobili dai propri [!DNL CRM] in Adobe Experience Platform. Quindi, possono creare tipi di pubblico dai propri dati offline e inviarli al [!DNL LinkedIn] social, ottimizzando le spese pubblicitarie.

## Identità supportate {#supported-identities}

[!DNL LinkedIn Matched Audiences] supporta l’attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| GAID | Google Advertising ID | Seleziona questa identità di destinazione quando l&#39;identità di origine è uno spazio dei nomi GAID. |
| IDFA | Apple ID per inserzionisti | Selezionare questa identità di destinazione quando l&#39;identità di origine è uno spazio dei nomi IDFA. |
| email_lc_sha256 | Indirizzi e-mail con hash con algoritmo SHA256 | Adobe Experience Platform supporta sia gli indirizzi di posta elettronica in testo normale che quelli con hash SHA256. Segui le istruzioni riportate nella sezione [Requisiti di corrispondenza ID](#id-matching-requirements-id-matching-requirements) e utilizza gli spazi dei nomi appropriati rispettivamente per le e-mail in testo normale e con hash. Quando il campo sorgente contiene attributi senza hash, seleziona la **[!UICONTROL Applica trasformazione]** opzione, per avere [!DNL Platform] esegui automaticamente l’hash dei dati all’attivazione. |

{style="table-layout:auto"}

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive il tipo di pubblico che puoi esportare in questa destinazione.

| Origine pubblico | Supportati | Descrizione |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Tipi di pubblico generati dall’Experience Platform [Servizio di segmentazione](../../../segmentation/home.md). |
| Caricamenti personalizzati | ✓ | Tipi di pubblico [importato](../../../segmentation/ui/overview.md#import-audience) in Experienci Platform da file CSV. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione pubblico]** | Stai esportando tutti i membri di un pubblico con gli identificatori (nome, numero di telefono e altri) utilizzati in [!DNL LinkedIn Matched Audiences] destinazione. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experienci Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni su [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Prerequisiti per l’account linkedIn {#LinkedIn-account-prerequisites}

Prima di utilizzare il [!UICONTROL Pubblico linkedIn corrispondente] destinazione, assicurati che il tuo [!DNL LinkedIn Campaign Manager] l&#39;account ha [!DNL Creative Manager] livello di autorizzazione o superiore.

Per scoprire come modificare il [!DNL LinkedIn Campaign Manager] autorizzazioni utente, consulta [Aggiungere, modificare e rimuovere le autorizzazioni utente sugli account Advertising](https://www.linkedin.com/help/lms/answer/5753) nella documentazione di LinkedIn.

## Requisiti di corrispondenza ID {#id-matching-requirements}

[!DNL LinkedIn Matched Audiences] richiede che non vengano inviate informazioni personali (PII, personally identifiable information) in modo chiaro. Pertanto, il pubblico è stato attivato per [!DNL LinkedIn Matched Audiences] può essere disattivato *con hash* identificatori, ad esempio indirizzi e-mail o ID di dispositivi mobili.

A seconda del tipo di ID inseriti in Adobe Experience Platform, devi rispettare i requisiti corrispondenti.

## Requisiti di hashing delle e-mail {#email-hashing-requirements}

Puoi eseguire l’hashing degli indirizzi e-mail prima di acquisirli in Adobe Experience Platform, oppure utilizzare gli indirizzi e-mail in chiaro nell’Experience Platform e disporre di [!DNL Platform] esegui l’hashing durante l’attivazione.

Per informazioni sull’acquisizione degli indirizzi e-mail in Experienci Platform, consulta la sezione [panoramica dell’acquisizione batch](/help/ingestion/batch-ingestion/overview.md) e [panoramica sull’acquisizione in streaming](/help/ingestion/streaming-ingestion/overview.md).

Se scegli di eseguire l’hash degli indirizzi e-mail da solo, assicurati di soddisfare i seguenti requisiti:

* Taglia tutti gli spazi iniziali e finali dalla stringa e-mail. Ad esempio: `johndoe@example.com`, non `<space>johndoe@example.com<space>`;
* Quando esegui l’hashing delle stringhe e-mail, assicurati di eseguire l’hashing della stringa in minuscolo;
   * Esempio: `example@email.com`, non `EXAMPLE@EMAIL.COM`;
* Assicurati che la stringa con hash sia tutta in minuscolo
   * Esempio: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, non `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* Non salare la corda.

>[!NOTE]
>
>I dati provenienti da spazi dei nomi senza hash vengono automaticamente sottoposti a hashing da [!DNL Platform] all&#39;attivazione.
> L&#39;hash dei dati di origine degli attributi non viene eseguito automaticamente.
> 
> Durante il [Mappatura identità](../../ui/activate-segment-streaming-destinations.md#mapping) passaggio, quando il campo sorgente contiene attributi senza hash, controlla **[!UICONTROL Applica trasformazione]** opzione, per avere [!DNL Platform] esegui automaticamente l’hash dei dati all’attivazione.
> 
> Il **[!UICONTROL Applica trasformazione]** L&#39;opzione viene visualizzata solo quando si selezionano gli attributi come campi di origine. Non viene visualizzato quando si scelgono gli spazi dei nomi.

![Trasformazione mappatura identità](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Connetti alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Gestire le destinazioni]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

Il video seguente illustra anche i passaggi per configurare una [!DNL LinkedIn Matched Audiences] destinazione e attivazione dei tipi di pubblico.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>L’interfaccia utente di Experienci Platform viene aggiornata frequentemente e potrebbe essere cambiata dopo la registrazione del video. Per informazioni aggiornate, fare riferimento al [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md).

### Autentica nella destinazione {#authenticate}

1. Trova il [!DNL LinkedIn Matched Audiences] nel catalogo di destinazione e seleziona **[!UICONTROL Configurazione]**.
2. Seleziona **[!UICONTROL Connetti alla destinazione]**.
   ![Autentica in LinkedIn](/help/destinations/assets/catalog/social/linkedin/authenticate-linkedin-destination.png)
3. Immetti le credenziali LinkedIn e seleziona **Accedi**.

### Inserisci i dettagli della destinazione {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_linkedin_accountid"
>title="ID account"
>abstract="ID del tuo account Gestione campagne di LinkedIn. Puoi trovare questo ID nel tuo account Gestione campagne di LinkedIn."

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

* **[!UICONTROL Nome]**: nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL ID account]**: il tuo [!DNL LinkedIn Campaign Manager Account ID]. Puoi trovare questo ID nel tuo [!DNL LinkedIn Campaign Manager] account.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completate le informazioni sulla connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

## Attiva il pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario **[!UICONTROL Visualizza grafico delle identità]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Consulta [Attiva i dati del pubblico nelle destinazioni di esportazione del pubblico in streaming](../../ui/activate-segment-streaming-destinations.md) per istruzioni sull’attivazione dei tipi di pubblico in questa destinazione.

## Dati esportati {#exported-data}

Una corretta attivazione implica che un [!DNL LinkedIn] il pubblico personalizzato viene creato a livello di programmazione in [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/campaignmanager/login). L’iscrizione al pubblico viene aggiunta e rimossa quando gli utenti sono qualificati o squalificati per i tipi di pubblico attivati.

>[!TIP]
>
>L’integrazione tra Adobe Experience Platform e [!DNL LinkedIn Matched Audiences] supporta retrocompilazioni storiche del pubblico. Tutti i requisiti storici del pubblico vengono inviati a [!DNL LinkedIn] quando attivi i tipi di pubblico nella destinazione.
