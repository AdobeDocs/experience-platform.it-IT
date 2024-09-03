---
keywords: connessione facebook;connessione facebook;destinazioni facebook;facebook;instagram;messenger;facebook messenger
title: Connessione facebook
description: Attiva profili per le campagne Facebook per il targeting, la personalizzazione e l’eliminazione del pubblico in base alle e-mail con hash.
exl-id: 51e8c8f0-5e79-45b9-afbc-110bae127f76
source-git-commit: 742801c31a0371feb42df2c98b3a4ddb63ae2f48
workflow-type: tm+mt
source-wordcount: '1985'
ht-degree: 7%

---

# Connessione [!DNL Facebook]

## Panoramica {#overview}

Attiva profili per le campagne [!DNL Facebook] per il targeting, la personalizzazione e l&#39;eliminazione del pubblico in base alle e-mail con hash.

È possibile utilizzare questa destinazione per il targeting del pubblico in tutta la famiglia di app [!DNL Facebook's] supportate da [!DNL Custom Audiences], inclusi [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network] e [!DNL Messenger]. La selezione dell&#39;app su cui desideri eseguire la campagna è indicata al livello di posizionamento in [!DNL Facebook Ads Manager].

![Destinazione Facebook nell&#39;interfaccia utente di Adobe Experience Platform.](../../assets/catalog/social/facebook/catalog.png)

## Casi d’uso

Per aiutarti a capire meglio come e quando utilizzare la destinazione [!DNL Facebook], ecco due casi d&#39;uso di esempio che i clienti di Adobe Experience Platform possono risolvere utilizzando questa funzione.

### #1 del caso d’uso

Un rivenditore online desidera raggiungere i clienti esistenti tramite piattaforme social e mostrare loro offerte personalizzate basate sui loro ordini precedenti. Il rivenditore online può acquisire gli indirizzi e-mail dal proprio CRM a Adobe Experience Platform, creare tipi di pubblico dai propri dati offline e inviare tali tipi di pubblico alla piattaforma social [!DNL Facebook], ottimizzando le spese pubblicitarie.

### #2 del caso d’uso

Una compagnia aerea ha diversi livelli di clienti (Bronzo, Argento e Oro) e vuole fornire a ciascuno di questi livelli offerte personalizzate tramite piattaforme social. Tuttavia, non tutti i clienti utilizzano l&#39;app mobile della compagnia aerea e alcuni di loro non hanno effettuato l&#39;accesso al sito web della compagnia. Gli unici identificatori di cui dispone l’azienda su questi clienti sono gli ID iscrizione e gli indirizzi e-mail.

Per eseguire il targeting tra i social media, può integrare i dati del cliente dal CRM in Adobe Experience Platform, utilizzando gli indirizzi e-mail come identificatori.

Successivamente, possono utilizzare i propri dati offline, inclusi gli ID di iscrizione e i livelli cliente associati, per creare nuovi tipi di pubblico che possono essere indirizzati tramite la destinazione [!DNL Facebook].

## Identità supportate {#supported-identities}

[!DNL Facebook Custom Audiences] supporta l&#39;attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/features/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | Seleziona l’identità di destinazione GAID quando l’identità di origine è uno spazio dei nomi GAID. |
| IDFA | Apple ID per inserzionisti | Selezionare l&#39;identità di destinazione IDFA quando l&#39;identità di origine è uno spazio dei nomi IDFA. |
| phone_sha256 | Numeri di telefono con hash con algoritmo SHA256 | I numeri di telefono con hash SHA256 e testo normale sono supportati da Adobe Experience Platform. Segui le istruzioni riportate nella sezione [Requisiti di corrispondenza ID](#id-matching-requirements-id-matching-requirements) e utilizza gli spazi dei nomi appropriati rispettivamente per i numeri di telefono con testo normale e con hash. Se il campo di origine contiene attributi senza hash, selezionare l&#39;opzione **[!UICONTROL Applica trasformazione]** per impostare [!DNL Platform] per l&#39;hashing automatico dei dati all&#39;attivazione. |
| email_lc_sha256 | Indirizzi e-mail con hash con algoritmo SHA256 | Adobe Experience Platform supporta sia gli indirizzi di posta elettronica in testo normale che quelli con hash SHA256. Segui le istruzioni riportate nella sezione [Requisiti di corrispondenza ID](#id-matching-requirements-id-matching-requirements) e utilizza gli spazi dei nomi appropriati rispettivamente per gli indirizzi e-mail in testo normale e con hash. Se il campo di origine contiene attributi senza hash, selezionare l&#39;opzione **[!UICONTROL Applica trasformazione]** per impostare [!DNL Platform] per l&#39;hashing automatico dei dati all&#39;attivazione. |
| extern_id | ID utente personalizzati | Seleziona questa identità di destinazione quando l&#39;identità di origine è uno spazio dei nomi personalizzato. |

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
| Tipo di esportazione | **[!UICONTROL Esportazione pubblico]** | Stai esportando tutti i membri di un pubblico con gli identificatori (nome, numero di telefono o altri) utilizzati nella destinazione Facebook. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni sulle [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Prerequisiti per l’account facebook {#facebook-account-prerequisites}

Prima di poter inviare i tipi di pubblico a [!DNL Facebook], assicurati di soddisfare i seguenti requisiti:

* L&#39;account utente di [!DNL Facebook] deve avere accesso completo a [!DNL Facebook Business Account], proprietario dell&#39;account dell&#39;annuncio che si sta utilizzando.
* L&#39;account utente [!DNL Facebook] deve avere l&#39;autorizzazione **[!DNL Manage campaigns]** abilitata per l&#39;account annuncio che intendi utilizzare.
* L&#39;account aziendale **Adobe Experience Cloud** deve essere aggiunto come partner pubblicitario nel tuo [!DNL Facebook Ad Account]. Usa `business ID=206617933627973`. Per ulteriori informazioni, consulta [Aggiungere partner al tuo Business Manager](https://www.facebook.com/business/help/1717412048538897) nella documentazione di Facebook.
  >[!IMPORTANT]
  >
  > Durante la configurazione delle autorizzazioni per Adobe Experience Cloud, devi abilitare l&#39;autorizzazione **Gestisci campagne**. L&#39;autorizzazione è necessaria per l&#39;integrazione di [!DNL Adobe Experience Platform].
* Leggi e firma le Condizioni per l&#39;utilizzo di [!DNL Facebook Custom Audiences]. Per farlo, vai a `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]&business_id=206617933627973`, dove `accountID` è il tuo [!DNL Facebook Ad Account ID]. Assicurati che la sezione `business_id=206617933627973` sia presente nell&#39;URL quando firmi i termini di servizio.
  >[!IMPORTANT]
  >
  >Quando si firmano i termini di servizio di [!DNL Facebook Custom Audiences], assicurarsi di utilizzare lo stesso account utente utilizzato per l&#39;autenticazione nell&#39;API Facebook.

## Requisiti di corrispondenza ID {#id-matching-requirements}

[!DNL Facebook] non richiede l&#39;invio di informazioni personali (PII, personally identifiable information) in chiaro. Pertanto, i tipi di pubblico attivati in [!DNL Facebook] possono essere ricavati da *identificatori con hash*, ad esempio indirizzi e-mail o numeri di telefono.

A seconda del tipo di ID inseriti in Adobe Experience Platform, devi rispettare i requisiti corrispondenti.

## Requisiti di hashing del numero di telefono {#phone-number-hashing-requirements}

Esistono due metodi per attivare i numeri di telefono in [!DNL Facebook]:

* **Acquisizione di numeri di telefono non elaborati**: è possibile acquisire numeri di telefono non elaborati nel formato [!DNL E.164] in [!DNL Platform]. Viene eseguito automaticamente l’hash al momento dell’attivazione. Se si sceglie questa opzione, assicurarsi di inserire sempre i numeri di telefono non elaborati nello spazio dei nomi `Phone_E.164`.
* **Inserimento di numeri di telefono con hash**: è possibile inserire i numeri di telefono con hash prima dell&#39;acquisizione in [!DNL Platform]. Se scegli questa opzione, assicurati di acquisire sempre i numeri di telefono con hash nello spazio dei nomi `Phone_SHA256`.

>[!NOTE]
>
>Impossibile attivare in [!DNL Facebook] i numeri di telefono acquisiti nello spazio dei nomi `Phone`.

## Requisiti di hashing delle e-mail {#email-hashing-requirements}

Puoi eseguire l&#39;hashing degli indirizzi e-mail prima di acquisirli in Adobe Experience Platform, oppure utilizzare gli indirizzi e-mail in chiaro nell&#39;Experience Platform e disporre di [!DNL Platform] hashing al momento dell&#39;attivazione.

Per informazioni sull&#39;acquisizione degli indirizzi e-mail in Experience Platform, consulta la [panoramica sull&#39;acquisizione batch](/help/ingestion/batch-ingestion/overview.md) e la [panoramica sull&#39;acquisizione in streaming](/help/ingestion/streaming-ingestion/overview.md).

Se scegli di eseguire l’hash degli indirizzi e-mail da solo, assicurati di soddisfare i seguenti requisiti:

* Taglia tutti gli spazi iniziali e finali dalla stringa e-mail. Esempio: `johndoe@example.com`, non `<space>johndoe@example.com<space>`;
* Quando esegui l’hashing delle stringhe e-mail, assicurati di eseguire l’hashing della stringa in minuscolo;
   * Esempio: `example@email.com`, non `EXAMPLE@EMAIL.COM`;
* Assicurati che la stringa con hash sia tutta in minuscolo
   * Esempio: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, non `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* Non salare la corda.

>[!NOTE]
>
>I dati degli spazi dei nomi senza hash vengono automaticamente sottoposti a hashing da [!DNL Platform] al momento dell&#39;attivazione.
> L&#39;hash dei dati di origine degli attributi non viene eseguito automaticamente. Se il campo di origine contiene attributi senza hash, selezionare l&#39;opzione **[!UICONTROL Applica trasformazione]** per impostare [!DNL Platform] per l&#39;hashing automatico dei dati all&#39;attivazione.
> L&#39;opzione **[!UICONTROL Applica trasformazione]** viene visualizzata solo quando si selezionano gli attributi come campi di origine. Non viene visualizzato quando si scelgono gli spazi dei nomi.

![Applica controllo di trasformazione evidenziato nel passaggio di mappatura.](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Utilizzo di spazi dei nomi personalizzati {#custom-namespaces}

Prima di poter utilizzare lo spazio dei nomi `Extern_ID` per inviare dati a [!DNL Facebook], assicurati di sincronizzare i tuoi identificatori utilizzando [!DNL Facebook Pixel]. Per informazioni dettagliate, consulta la [documentazione ufficiale di Facebook](https://developers.facebook.com/docs/marketing-api/audiences/guides/custom-audiences/#external_identifiers).

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, sono necessarie le **[!UICONTROL Destinazioni visualizzazione]** e le **[!UICONTROL Autorizzazioni di gestione delle destinazioni]** [per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

Il video seguente illustra inoltre i passaggi per configurare una destinazione [!DNL Facebook] e attivare i tipi di pubblico.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>L’interfaccia utente di Experience Platform viene aggiornata frequentemente e potrebbe essere cambiata dopo la registrazione del video. Per informazioni aggiornate, fare riferimento al [tutorial sulla configurazione della destinazione](../../ui/connect-destination.md).

### Autenticarsi nella destinazione {#authenticate}

1. Trova la destinazione Facebook nel catalogo di destinazione e seleziona **[!UICONTROL Configura]**.
2. Selezionare **[!UICONTROL Connetti alla destinazione]**.
   ![Esegui l&#39;autenticazione in Facebook, passaggio visualizzato nel flusso di lavoro di attivazione.](/help/destinations/assets/catalog/social/facebook/authenticate-facebook-destination.png)
3. Immetti le credenziali Facebook e seleziona **Accedi**.

### Inserire i dettagli della destinazione {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_facebook_accountid"
>title="ID account"
>abstract="ID del tuo account per Inserzioni Facebook. Puoi trovare questo ID nel tuo account Gestione inserzioni di Facebook. Quando immetti questo ID, devi sempre aggiungere il prefisso `act_`."

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

* **[!UICONTROL Nome]**: un nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL ID account]**: [!DNL Facebook Ad Account ID]. Puoi trovare questo ID nel tuo account [!DNL Facebook Ads Manager]. Quando immetti questo ID, devi sempre aggiungere il prefisso `act_`.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli per la connessione di destinazione, seleziona **[!UICONTROL Avanti]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience"
>title="Origine del pubblico"
>abstract="Scegli come sono stati originariamente raccolti i dati cliente nel pubblico. I dati verranno visualizzati su Facebook quando il segmento viene destinato a un utente"

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience_customers"
>title="Origine del pubblico"
>abstract="Gli inserzionisti raccolgono i dati direttamente dai clienti."

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience_partners"
>title="Origine del pubblico"
>abstract="Gli inserzionisti raccolgono i dati direttamente dai loro partner."

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience_customersandpartners"
>title="Origine del pubblico"
>abstract="Gli inserzionisti raccolgono i dati direttamente dai loro clienti e partner."

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Visualizza grafo identità]** [Controllo di accesso](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Per istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione, consulta [Attivare i dati del pubblico nelle destinazioni di esportazione del pubblico in streaming](../../ui/activate-segment-streaming-destinations.md).

Nel passaggio **[!UICONTROL Pianificazione del segmento]**, devi fornire la [!UICONTROL Origine del pubblico] durante l&#39;invio di tipi di pubblico a [!DNL Facebook Custom Audiences].

![Menu a discesa Origine del pubblico visualizzato nel passaggio di attivazione di Facebook.](../../assets/catalog/social/facebook/facebook-origin-audience.png)

### Esempio di mappatura: attivazione dei dati del pubblico in [!DNL Facebook Custom Audience] {#example-facebook}

Di seguito è riportato un esempio di corretta mappatura identità durante l&#39;attivazione dei dati del pubblico in [!DNL Facebook Custom Audience].

Selezione dei campi di origine:

* Selezionare lo spazio dei nomi `Email` come identità di origine se gli indirizzi e-mail utilizzati non sono con hash.
* Seleziona lo spazio dei nomi `Email_LC_SHA256` come identità di origine se esegui l&#39;hashing degli indirizzi e-mail dei clienti al momento dell&#39;acquisizione dei dati in [!DNL Platform], in base a [!DNL Facebook] [requisiti di hashing delle e-mail](#email-hashing-requirements).
* Selezionare lo spazio dei nomi `PHONE_E.164` come identità di origine se i dati sono costituiti da numeri di telefono senza hash. [!DNL Platform] eseguirà l&#39;hash dei numeri di telefono per soddisfare i requisiti di [!DNL Facebook].
* Seleziona lo spazio dei nomi `Phone_SHA256` come identità di origine se hai aggiunto l&#39;hashing ai numeri di telefono al momento dell&#39;acquisizione dei dati in [!DNL Platform], in base ai [!DNL Facebook] [requisiti di hashing dei numeri di telefono](#phone-number-hashing-requirements).
* Selezionare lo spazio dei nomi `IDFA` come identità di origine se i dati sono costituiti da [!DNL Apple] ID dispositivo.
* Selezionare lo spazio dei nomi `GAID` come identità di origine se i dati sono costituiti da [!DNL Android] ID dispositivo.
* Selezionare lo spazio dei nomi `Custom` come identità di origine se i dati sono costituiti da altri tipi di identificatori.

Selezione dei campi di destinazione:

* Selezionare lo spazio dei nomi `Email_LC_SHA256` come identità di destinazione quando gli spazi dei nomi di origine sono `Email` o `Email_LC_SHA256`.
* Selezionare lo spazio dei nomi `Phone_SHA256` come identità di destinazione quando gli spazi dei nomi di origine sono `PHONE_E.164` o `Phone_SHA256`.
* Selezionare gli spazi dei nomi `IDFA` o `GAID` come identità di destinazione quando gli spazi dei nomi di origine sono `IDFA` o `GAID`.
* Selezionare lo spazio dei nomi `Extern_ID` come identità di destinazione quando lo spazio dei nomi di origine è personalizzato.

>[!IMPORTANT]
>
>I dati degli spazi dei nomi senza hash vengono automaticamente sottoposti a hashing da [!DNL Platform] al momento dell&#39;attivazione.
> 
>L&#39;hash dei dati di origine degli attributi non viene eseguito automaticamente. Se il campo di origine contiene attributi senza hash, selezionare l&#39;opzione **[!UICONTROL Applica trasformazione]** per impostare [!DNL Platform] per l&#39;hashing automatico dei dati all&#39;attivazione.

![Applica controllo di trasformazione evidenziato nel passaggio di mappatura.](../../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## Dati esportati {#exported-data}

Per [!DNL Facebook], un&#39;attivazione riuscita significa che un pubblico personalizzato [!DNL Facebook] verrebbe creato a livello di programmazione in [[!DNL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). L’iscrizione al pubblico viene aggiunta e rimossa quando gli utenti sono qualificati o squalificati per i tipi di pubblico attivati.

>[!TIP]
>
>L&#39;integrazione tra Adobe Experience Platform e [!DNL Facebook] supporta i backfill cronologici del pubblico. Tutti i requisiti storici del pubblico vengono inviati a [!DNL Facebook] quando attivi i tipi di pubblico nella destinazione.

## Risoluzione dei problemi {#troubleshooting}

### 400 Messaggio di errore di richiesta non valida {#bad-request}

Durante la configurazione di questa destinazione, potrebbe venire visualizzato il seguente errore:

`{"message":"Facebook Error: Permission error","code":"400 BAD_REQUEST"}`

Questo errore si verifica quando i clienti utilizzano account appena creati e le autorizzazioni [!DNL Facebook] non sono ancora attive.

>[!IMPORTANT]
>
>Assicurarsi di accettare [!DNL Facebook Custom Audience Terms of Service] in `business ID 206617933627973`, come mostrato nel modello URL nella sezione [prerequisiti account](#facebook-account-prerequisites).

Se ricevi il messaggio di errore `400 Bad Request` dopo aver seguito i passaggi descritti in [Prerequisiti per l&#39;account Facebook](#facebook-account-prerequisites), attendi alcuni giorni per l&#39;entrata in vigore delle autorizzazioni [!DNL Facebook].


