---
keywords: connessione facebook;connessione facebook;destinazioni facebook;facebook;instagram;messenger;facebook messenger
title: Connessione facebook
description: Attiva profili per le campagne Facebook per il targeting, la personalizzazione e l’eliminazione del pubblico in base alle e-mail con hash.
exl-id: 51e8c8f0-5e79-45b9-afbc-110bae127f76
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1952'
ht-degree: 7%

---

# [!DNL Facebook] connessione

## Panoramica {#overview}

Attivare i profili per il [!DNL Facebook] campagne per il targeting, la personalizzazione e l’eliminazione del pubblico basate su e-mail con hash.

Puoi utilizzare questa destinazione per il targeting del pubblico in [!DNL Facebook's] famiglia di app supportate da [!DNL Custom Audiences], tra cui [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network], e [!DNL Messenger]. La selezione dell’app su cui desideri eseguire la campagna è indicata al livello di posizionamento in [!DNL Facebook Ads Manager].

![Destinazione facebook nell’interfaccia utente di Adobe Experience Platform.](../../assets/catalog/social/facebook/catalog.png)

## Casi d’uso

Per aiutarti a capire meglio come e quando utilizzare il [!DNL Facebook] destinazione: ecco due casi d’uso esemplificativi che i clienti di Adobe Experience Platform possono risolvere utilizzando questa funzione.

### #1 del caso d’uso

Un rivenditore online desidera raggiungere i clienti esistenti tramite piattaforme social e mostrare loro offerte personalizzate basate sui loro ordini precedenti. Il rivenditore online può acquisire gli indirizzi e-mail dal proprio CRM per Adobe Experience Platform, creare tipi di pubblico dai propri dati offline e inviare tali tipi di pubblico a [!DNL Facebook] social, ottimizzando le spese pubblicitarie.

### #2 del caso d’uso

Una compagnia aerea ha diversi livelli di clienti (Bronzo, Argento e Oro) e vuole fornire a ciascuno di questi livelli offerte personalizzate tramite piattaforme social. Tuttavia, non tutti i clienti utilizzano l&#39;app mobile della compagnia aerea e alcuni di loro non hanno effettuato l&#39;accesso al sito web della compagnia. Gli unici identificatori di cui dispone l’azienda su questi clienti sono gli ID iscrizione e gli indirizzi e-mail.

Per eseguire il targeting tra i social media, può integrare i dati del cliente dal CRM in Adobe Experience Platform, utilizzando gli indirizzi e-mail come identificatori.

Successivamente, può utilizzare i propri dati offline, inclusi gli ID di iscrizione e i livelli cliente associati, per creare nuovi tipi di pubblico target tramite [!DNL Facebook] destinazione.

## Identità supportate {#supported-identities}

[!DNL Facebook Custom Audiences] supporta l’attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/features/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| GAID | Google Advertising ID | Seleziona l’identità di destinazione GAID quando l’identità di origine è uno spazio dei nomi GAID. |
| IDFA | Apple ID per inserzionisti | Selezionare l&#39;identità di destinazione IDFA quando l&#39;identità di origine è uno spazio dei nomi IDFA. |
| phone_sha256 | Numeri di telefono con hash con algoritmo SHA256 | I numeri di telefono con hash SHA256 e testo normale sono supportati da Adobe Experience Platform. Segui le istruzioni riportate nella sezione [Requisiti di corrispondenza ID](#id-matching-requirements-id-matching-requirements) e utilizza gli spazi dei nomi appropriati rispettivamente per i numeri di telefono con testo normale e con hash. Quando il campo sorgente contiene attributi senza hash, seleziona la **[!UICONTROL Applica trasformazione]** opzione, per avere [!DNL Platform] esegui automaticamente l’hash dei dati all’attivazione. |
| email_lc_sha256 | Indirizzi e-mail con hash con algoritmo SHA256 | Adobe Experience Platform supporta sia gli indirizzi di posta elettronica in testo normale che quelli con hash SHA256. Segui le istruzioni riportate nella sezione [Requisiti di corrispondenza ID](#id-matching-requirements-id-matching-requirements) e utilizza gli spazi dei nomi appropriati rispettivamente per gli indirizzi e-mail in testo normale e con hash. Quando il campo sorgente contiene attributi senza hash, seleziona la **[!UICONTROL Applica trasformazione]** opzione, per avere [!DNL Platform] esegui automaticamente l’hash dei dati all’attivazione. |
| extern_id | ID utente personalizzati | Seleziona questa identità di destinazione quando l&#39;identità di origine è uno spazio dei nomi personalizzato. |

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive quali tipi di pubblico puoi esportare in questa destinazione.

| Origine pubblico | Supportati | Descrizione |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Tipi di pubblico generati dall’Experience Platform [Servizio di segmentazione](../../../segmentation/home.md). |
| Caricamenti personalizzati | ✓ | Tipi di pubblico [importato](../../../segmentation/ui/overview.md#import-audience) in Experienci Platform da file CSV. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione pubblico]** | Stai esportando tutti i membri di un pubblico con gli identificatori (nome, numero di telefono o altri) utilizzati nella destinazione Facebook. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experienci Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni su [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Prerequisiti per l’account facebook {#facebook-account-prerequisites}

Prima di poter inviare i tipi di pubblico a [!DNL Facebook], assicurati di soddisfare i seguenti requisiti:

* Il tuo [!DNL Facebook] l&#39;account utente deve avere accesso completo al [!DNL Facebook Business Account] proprietario dell’account dell’annuncio che stai utilizzando.
* Il tuo [!DNL Facebook] l&#39;account utente deve avere **[!DNL Manage campaigns]** Autorizzazione abilitata per l’account annuncio che intendi utilizzare.
* Il **Adobe Experience Cloud** l&#39;account aziendale deve essere aggiunto come partner pubblicitario nel tuo [!DNL Facebook Ad Account]. Utilizza `business ID=206617933627973`. Consulta [Aggiunta di partner a Business Manager](https://www.facebook.com/business/help/1717412048538897) nella documentazione di Facebook per ulteriori dettagli.
  >[!IMPORTANT]
  >
  > Durante la configurazione delle autorizzazioni per Adobe Experience Cloud, devi abilitare **Gestire le campagne** autorizzazione. L’autorizzazione è necessaria per [!DNL Adobe Experience Platform] integrazione.
* Leggi e firma la [!DNL Facebook Custom Audiences] Termini di servizio. Per farlo, vai a `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, dove `accountID` è il tuo [!DNL Facebook Ad Account ID].
  >[!IMPORTANT]
  >
  >Al momento della firma del [!DNL Facebook Custom Audiences] Condizioni d’uso, assicurati di utilizzare lo stesso account utente utilizzato per l’autenticazione nell’API di Facebook.

## Requisiti di corrispondenza ID {#id-matching-requirements}

[!DNL Facebook] richiede che non vengano inviate informazioni personali (PII, personally identifiable information) in modo chiaro. Pertanto, il pubblico è stato attivato per [!DNL Facebook] può essere disattivato *con hash* identificatori, ad esempio indirizzi e-mail o numeri di telefono.

A seconda del tipo di ID inseriti in Adobe Experience Platform, devi rispettare i requisiti corrispondenti.

## Requisiti di hashing del numero di telefono {#phone-number-hashing-requirements}

Esistono due metodi per attivare i numeri di telefono in [!DNL Facebook]:

* **Acquisizione di numeri di telefono non elaborati**: è possibile acquisire i numeri di telefono non elaborati nel [!DNL E.164] formattare in [!DNL Platform]. Viene eseguito automaticamente l’hash al momento dell’attivazione. Se scegli questa opzione, assicurati di inserire sempre i numeri di telefono non elaborati nel `Phone_E.164` spazio dei nomi.
* **Acquisizione di numeri di telefono con hash**: puoi eseguire il pre-hashing dei numeri di telefono prima dell’acquisizione in [!DNL Platform]. Se scegli questa opzione, assicurati di inserire sempre i numeri di telefono con hash nel `Phone_SHA256` spazio dei nomi.

>[!NOTE]
>
>Numeri di telefono acquisiti in `Phone` impossibile attivare lo spazio dei nomi in [!DNL Facebook].

## Requisiti di hashing delle e-mail {#email-hashing-requirements}

Puoi eseguire l’hashing degli indirizzi e-mail prima di acquisirli in Adobe Experience Platform, oppure utilizzare gli indirizzi e-mail in chiaro nell’Experience Platform e disporre di [!DNL Platform] esegui l’hashing durante l’attivazione.

Per informazioni sull’acquisizione degli indirizzi e-mail in Experienci Platform, consulta la sezione [panoramica dell’acquisizione batch](/help/ingestion/batch-ingestion/overview.md) e [panoramica sull’acquisizione in streaming](/help/ingestion/streaming-ingestion/overview.md).

Se scegli di eseguire l’hash degli indirizzi e-mail da solo, assicurati di soddisfare i seguenti requisiti:

* Taglia tutti gli spazi iniziali e finali dalla stringa e-mail; ad esempio: `johndoe@example.com`, non `<space>johndoe@example.com<space>`;
* Quando esegui l’hashing delle stringhe e-mail, assicurati di eseguire l’hashing della stringa in minuscolo;
   * Esempio: `example@email.com`, non `EXAMPLE@EMAIL.COM`;
* Assicurati che la stringa con hash sia tutta in minuscolo
   * Esempio: `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`, non `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* Non salare la corda.

>[!NOTE]
>
>I dati provenienti da spazi dei nomi senza hash vengono automaticamente sottoposti a hashing da [!DNL Platform] all&#39;attivazione.
> L&#39;hash dei dati di origine degli attributi non viene eseguito automaticamente. Quando il campo sorgente contiene attributi senza hash, seleziona la **[!UICONTROL Applica trasformazione]** opzione, per avere [!DNL Platform] esegui automaticamente l’hash dei dati all’attivazione.
> Il **[!UICONTROL Applica trasformazione]** L&#39;opzione viene visualizzata solo quando si selezionano gli attributi come campi di origine. Non viene visualizzato quando si scelgono gli spazi dei nomi.

![Applica il controllo di trasformazione evidenziato nel passaggio di mappatura.](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## Utilizzo di spazi dei nomi personalizzati {#custom-namespaces}

Prima di utilizzare il `Extern_ID` spazio dei nomi a cui inviare i dati [!DNL Facebook], assicurati di sincronizzare i tuoi identificatori tramite [!DNL Facebook Pixel]. Consulta la [Documentazione ufficiale di facebook](https://developers.facebook.com/docs/marketing-api/audiences/guides/custom-audiences/#external_identifiers) per informazioni dettagliate.

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario **[!UICONTROL Visualizza destinazioni]** e **[!UICONTROL Gestire le destinazioni]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti in [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

Il video seguente illustra anche i passaggi per configurare una [!DNL Facebook] destinazione e attivazione dei tipi di pubblico.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>L’interfaccia utente di Experienci Platform viene aggiornata frequentemente e potrebbe essere cambiata dopo la registrazione del video. Per informazioni aggiornate, fare riferimento al [esercitazione sulla configurazione della destinazione](../../ui/connect-destination.md).

### Autenticarsi nella destinazione {#authenticate}

1. Trova la destinazione Facebook nel catalogo di destinazione e seleziona **[!UICONTROL Configurazione]**.
2. Seleziona **[!UICONTROL Connetti alla destinazione]**.
   ![Esegui l’autenticazione in Facebook, passaggio visualizzato nel flusso di lavoro di attivazione.](/help/destinations/assets/catalog/social/facebook/authenticate-facebook-destination.png)
3. Immetti le credenziali Facebook e seleziona **Accedi**.

### Inserire i dettagli della destinazione {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_facebook_accountid"
>title="ID account"
>abstract="ID del tuo account per Inserzioni Facebook. Puoi trovare questo ID nel tuo account Gestione inserzioni di Facebook. Quando immetti questo ID, devi sempre aggiungere il prefisso `act_`."

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

* **[!UICONTROL Nome]**: nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL ID account]**: il tuo [!DNL Facebook Ad Account ID]. Puoi trovare questo ID nel tuo [!DNL Facebook Ads Manager] account. Quando immetti questo ID, devi sempre aggiungere il prefisso `act_`.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento agli avvisi sulle destinazioni tramite l’interfaccia utente](../../ui/alerts.md).

Una volta completate le informazioni sulla connessione di destinazione, seleziona **[!UICONTROL Successivo]**.

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
>* Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizza profili]**, e **[!UICONTROL Visualizzare segmenti]** [autorizzazioni di controllo degli accessi](/help/access-control/home.md#permissions). Leggi le [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) oppure contatta l’amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario **[!UICONTROL Visualizza grafico delle identità]** [autorizzazione per il controllo degli accessi](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Consulta [Attiva i dati del pubblico nelle destinazioni di esportazione del pubblico in streaming](../../ui/activate-segment-streaming-destinations.md) per istruzioni sull’attivazione dei tipi di pubblico in questa destinazione.

In **[!UICONTROL Pianificazione del segmento]** passaggio, devi fornire [!UICONTROL Origine del pubblico] quando si inviano tipi di pubblico a [!DNL Facebook Custom Audiences].

![Menu a discesa Origine del pubblico visualizzato nel passaggio di attivazione di Facebook.](../../assets/catalog/social/facebook/facebook-origin-audience.png)

### Esempio di mappatura: attivazione dei dati sul pubblico in [!DNL Facebook Custom Audience] {#example-facebook}

Di seguito è riportato un esempio di corretta mappatura identità durante l’attivazione dei dati di pubblico in [!DNL Facebook Custom Audience].

Selezione dei campi di origine:

* Seleziona la `Email` spazio dei nomi come identità di origine se l’hash non viene applicato agli indirizzi e-mail in uso.
* Seleziona la `Email_LC_SHA256` spazio dei nomi come identità di origine se si esegue l’hashing degli indirizzi e-mail dei clienti al momento dell’inserimento dei dati in [!DNL Platform], secondo [!DNL Facebook] [requisiti di hashing delle e-mail](#email-hashing-requirements).
* Seleziona la `PHONE_E.164` spazio dei nomi come identità di origine se i dati sono costituiti da numeri di telefono senza hash. [!DNL Platform] eseguirà l&#39;hashing dei numeri di telefono per conformarsi a [!DNL Facebook] requisiti.
* Seleziona la `Phone_SHA256` spazio dei nomi come identità di origine se all’acquisizione dei dati in si applica l’hashing ai numeri di telefono [!DNL Platform], secondo [!DNL Facebook] [requisiti di hashing del numero di telefono](#phone-number-hashing-requirements).
* Seleziona la `IDFA` spazio dei nomi come identità di origine se i dati sono costituiti da [!DNL Apple] ID dispositivo.
* Seleziona la `GAID` spazio dei nomi come identità di origine se i dati sono costituiti da [!DNL Android] ID dispositivo.
* Seleziona la `Custom` spazio dei nomi come identità di origine se i dati sono costituiti da altri tipi di identificatori.

Selezione dei campi di destinazione:

* Seleziona la `Email_LC_SHA256` spazio dei nomi come identità di destinazione quando gli spazi dei nomi di origine sono `Email` o `Email_LC_SHA256`.
* Seleziona la `Phone_SHA256` spazio dei nomi come identità di destinazione quando gli spazi dei nomi di origine sono `PHONE_E.164` o `Phone_SHA256`.
* Seleziona la `IDFA` o `GAID` spazi dei nomi come identità di destinazione quando gli spazi dei nomi di origine sono `IDFA` o `GAID`.
* Seleziona la `Extern_ID` spazio dei nomi come identità di destinazione quando lo spazio dei nomi di origine è personalizzato.

>[!IMPORTANT]
>
>I dati provenienti da spazi dei nomi senza hash vengono automaticamente sottoposti a hashing da [!DNL Platform] all&#39;attivazione.
> 
>L&#39;hash dei dati di origine degli attributi non viene eseguito automaticamente. Quando il campo sorgente contiene attributi senza hash, seleziona la **[!UICONTROL Applica trasformazione]** opzione, per avere [!DNL Platform] esegui automaticamente l’hash dei dati all’attivazione.

![Applica il controllo di trasformazione evidenziato nel passaggio di mappatura.](../../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## Dati esportati {#exported-data}

Per [!DNL Facebook], se l&#39;attivazione ha esito positivo, significa che [!DNL Facebook] il pubblico personalizzato viene creato a livello di programmazione in [[!DNL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). L’iscrizione al pubblico viene aggiunta e rimossa quando gli utenti sono qualificati o squalificati per i tipi di pubblico attivati.

>[!TIP]
>
>L’integrazione tra Adobe Experience Platform e [!DNL Facebook] supporta retrocompilazioni storiche del pubblico. Tutti i requisiti storici del pubblico vengono inviati a [!DNL Facebook] quando attivi i tipi di pubblico nella destinazione.

## Risoluzione dei problemi {#troubleshooting}

### 400 Messaggio di errore di richiesta non valida {#bad-request}

Durante la configurazione di questa destinazione, potrebbe venire visualizzato il seguente errore:

`{"message":"Facebook Error: Permission error","code":"400 BAD_REQUEST"}`

Questo errore si verifica quando i clienti utilizzano account appena creati e il [!DNL Facebook] autorizzazioni non ancora attive.

Se riceve il `400 Bad Request` messaggio di errore dopo aver seguito i passaggi in [Prerequisiti per l’account facebook](#facebook-account-prerequisites), attendi alcuni giorni per [!DNL Facebook] autorizzazioni per entrare in vigore.
