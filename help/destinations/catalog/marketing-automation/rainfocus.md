---
title: Profili partecipanti RainFocus
description: Scopri come utilizzare il connettore di destinazione dei profili partecipante RainFocus per sincronizzare i profili di pubblico con il profilo partecipante globale RainFocus.
last-substantial-update: 2024-12-17T00:00:00Z
exl-id: 27c3848c-411a-4305-a5d5-00b145b95287
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 5%

---

# Profili partecipanti RainFocus {#rainfocus-destination}

## Panoramica {#overview}

Utilizza la destinazione [!DNL RainFocus Attendee Profiles] per eseguire lo streaming dei profili cliente da Adobe Experience Platform alla piattaforma [!DNL RainFocus] per creare e aggiornare i profili dei partecipanti.

>[!IMPORTANT]
>
>Il connettore di destinazione e la pagina della documentazione vengono creati e gestiti dal team [!DNL RainFocus]. Per qualsiasi richiesta di informazioni o di aggiornamento, contattarli direttamente all&#39;indirizzo `clientcare@rainfocus.com` o visitare il [Centro assistenza](https://help.rainfocus.com/hc/en-us) di RainFocus.

## Casi d’uso {#use-cases}

Per aiutarti a capire meglio come e quando utilizzare la destinazione RainFocus, ecco alcuni esempi di casi d’uso che i clienti di Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### #1 del caso d’uso {#use-case-1}

Una grande azienda tecnologica di livello Enterprise deve aprire la registrazione per la prossima esposizione globale e desidera inviare i profili dei clienti a [!DNL RainFocus] per semplificare il processo di registrazione.

### #2 del caso d’uso {#use-case-2}

Un marchio di servizi finanziari ospiterà una serie di eventi itineranti rivolti a clienti nuovi ed esistenti. Possiedono una serie di segmenti di pubblico con i clienti target in Adobe Experience Platform. Utilizzando il connettore di destinazione [!DNL RainFocus], è possibile inviare facilmente tali profili a [!DNL RainFocus] per l&#39;attivazione.

## Prerequisiti {#prerequisites}

Prima di poter utilizzare la destinazione [!DNL RainFocus], assicurarsi di soddisfare i seguenti prerequisiti:

* Crea un profilo API [!DNL RainFocus] con OAuth (globale).
   * L&#39;endpoint **Archivio partecipanti** deve essere abilitato.
   * Sarà necessario generare un **ID client** e un **Segreto client**.

È inoltre necessario disporre di un identificatore **codice evento** RainFocus in cui si desidera inviare i profili.

## Identità supportate {#supported-identities}

[!DNL RainFocus] supporta l&#39;attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/features/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| email_lc_sha256 | Indirizzi e-mail con hash con algoritmo SHA256 | Adobe Experience Platform supporta sia gli indirizzi di posta elettronica in testo normale che quelli con hash SHA256. Se il campo di origine contiene attributi senza hash, selezionare l&#39;opzione **[!UICONTROL Apply transformation]** per impostare [!DNL Experience Platform] per l&#39;hashing automatico dei dati all&#39;attivazione. |

{style="table-layout:auto"}

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive il tipo di pubblico che puoi esportare in questa destinazione.

| Origine pubblico | Supportato | Descrizione |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Tipi di pubblico generati tramite Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Caricamenti personalizzati | ✓ | Tipi di pubblico [importati](../../../segmentation/ui/overview.md#import-audience) in Experience Platform da file CSV. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
|---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Profile-based]** | Stai esportando tutti i membri di un segmento, insieme ai campi dello schema desiderati (ad esempio: indirizzo e-mail, numero di telefono, cognome), come scelto nella schermata seleziona attributi profilo del [flusso di lavoro di attivazione della destinazione](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione dei segmenti, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni sulle [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, è necessario disporre dell&#39;autorizzazione di controllo di accesso **[!UICONTROL View Destinations]** e **[!UICONTROL Manage Destinations]** [](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autenticarsi nella destinazione {#authenticate}

Per autenticare nella destinazione, compilare i campi obbligatori e selezionare **[!UICONTROL Connect to destination]**.

![Specificare i dettagli di autenticazione per il connettore di destinazione RainFocus](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-destination-authentication.png)

* **[!UICONTROL Client ID]**: compilare [!DNL Client ID] fornito dal profilo API RainFocus.
* **[!UICONTROL Client secret]**: compilare [!DNL Client Secret] fornito dal profilo API RainFocus.
* **[!UICONTROL Environment]**: specificare l&#39;ambiente RainFocus a cui ci si connette, ad esempio `dev`, `prod`.
* **[!UICONTROL Org ID]**: fornisci `orgid` univoco per l&#39;istanza di RainFocus.

### Inserire i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

![Specificare i dettagli di connessione per il connettore di destinazione RainFocus](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-configure-destination-details.png)

* **[!UICONTROL Name]**: nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Description]**: una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL Event ID]**: l&#39;identificatore del codice evento [!DNL RainFocus] in cui si desidera inviare i profili.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli della connessione di destinazione, selezionare **[!UICONTROL Next]**.

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, sono necessarie le **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Leggi [Attivare profili e segmenti nelle destinazioni di esportazione dei segmenti di streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per le istruzioni sull&#39;attivazione dei segmenti di pubblico in questa destinazione.

### Mappare attributi e identità {#map}

I seguenti spazi dei nomi delle identità di destinazione devono essere mappati a seconda del caso d’uso:

* **E-mail** deve essere mappato come campo di destinazione utilizzando **Campo di destinazione > Seleziona spazio dei nomi identità > E-mail**

![Mappatura dei campi di profilo e identità](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-destination-mapping.png)

È consigliabile eseguire il mapping di campi di profilo aggiuntivi, in modo da garantire che il profilo del partecipante in [!DNL RainFocus] sia completamente popolato. I seguenti campi di destinazione sono disponibili da [!DNL RainFocus]:

| Campo di destinazione | Descrizione |
|------------|-------------|
| `address1` | Prima riga dell&#39;indirizzo stradale |
| `address2` | Seconda riga dell’indirizzo stradale (se applicabile) |
| `city` | Il nome della città |
| `companyname` | Nome dell’azienda |
| `countryid` | Un identificatore del codice paese ISO 3166-1 alpha-2 per il paese |
| `email` | Indirizzo e-mail |
| `firstname` | Nome della persona |
| `lastname` | Cognome della persona |
| `jobtitle` | Qualifica della persona |
| `phone` | Numero di telefono |
| `state` | Codice alfa dello stato FIPS per lo stato o la provincia |
| `zip` | Codice postale o CAP |

{style="table-layout:auto"}

## Dati esportati / Convalida esportazione dati {#exported-data}

Una volta inviato un set di profili a [!DNL RainFocus], utilizzare la registrazione del profilo API in [!DNL RainFocus] per verificare che i profili siano stati acquisiti correttamente.

![Visualizza i registri nel profilo API in RainFocus](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-destination-api-profile.png)

![Verifica che i profili siano stati acquisiti correttamente](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-destination-api-logging.png)

## Utilizzo dei dati e governance {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, leggere la [Panoramica sulla governance dei dati](/help/data-governance/home.md).

## Risorse aggiuntive {#additional-resources}

* [Connettore Source streaming RainFocus](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/analytics/rainfocus)
