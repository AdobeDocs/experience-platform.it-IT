---
title: Customer Match Google + Display e connessione Video 360
description: Con il connettore di destinazione Google Customer Match + Display & Video 360, puoi utilizzare i dati online e offline di Experience Platform per raggiungere e coinvolgere nuovamente i clienti nelle proprietà possedute e gestite da Google, come Search, Shopping, Gmail e YouTube.
badgeBeta: label="Beta" type="Informative"
exl-id: f6da3eae-bf3f-401a-99a1-2cca9a9058d2
source-git-commit: c3de72a0f90578803b969f32cc484047089099bd
workflow-type: tm+mt
source-wordcount: '1999'
ht-degree: 1%

---

# Connessione [!DNL Google Customer Match + Display & Video 360]

Utilizzare questa destinazione per attivare gli elenchi [[!DNL Google Customer Match]](https://support.google.com/google-ads/answer/6379332?hl=en) basati su PII di prime parti direttamente nelle proprietà [!DNL Google Display & Video 360] come [!DNL Search], [!DNL YouTube], [!DNL Gmail] e [!DNL Google Display Network].

Alcune terze parti integrate in Google, come Adobe Real-Time CDP, possono utilizzare [!DNL Google Audience Partner API] per creare tipi di pubblico [!DNL Customer Match] direttamente nell&#39;account [!DNL Display & Video 360] dei clienti.

Con la funzionalità introdotta di recente di poter utilizzare [!DNL Customer Matched] tipi di pubblico in [!DNL Display & Video 360], ora puoi indirizzare i tipi di pubblico in un elenco esteso di origini inventario.

>[!IMPORTANT]
>
>Questo connettore di destinazione è in versione beta ed è disponibile solo per alcuni clienti. Per richiedere l’accesso, contatta il rappresentante del tuo Adobe.

![Google Customer Match + DV360 nell&#39;interfaccia utente di Adobe Experience Platform.](/help/destinations/assets/catalog/advertising/gcm-dv360/catalog.png)

## Avviso importante sulle modifiche alle destinazioni Google in relazione ai requisiti di consenso aggiornati nell’Unione Europea

>[!IMPORTANT]
>
> Google sta rilasciando modifiche all&#39;API [Google Ads](https://developers.google.com/google-ads/api/docs/start), [Customer Match](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html) e all&#39;API [Display &amp; Video 360](https://developers.google.com/display-video/api/guides/getting-started/overview) per supportare i requisiti relativi alla conformità e al consenso definiti nel [Digital Markets Act](https://digital-markets-act.ec.europa.eu/index_en) (DMA) nell&#39;Unione Europea ([EU User Consent Policy](https://www.google.com/about/company/user-consent-policy/)). L’applicazione di queste modifiche ai requisiti di consenso è attiva dal 6 marzo 2024.
><br/>
>Per aderire alla politica di consenso degli utenti dell’UE e continuare a creare elenchi di pubblico per gli utenti dello Spazio economico europeo (SEE), gli inserzionisti e i partner devono assicurarsi di trasmettere il consenso degli utenti finali durante il caricamento dei dati sul pubblico. In qualità di partner Google, Adobe fornisce gli strumenti necessari per soddisfare i requisiti di consenso ai sensi dell’accordo DMA nell’Unione Europea.
><br/>
>I clienti che hanno acquistato Adobe Privacy &amp; Security Shield e hanno configurato un [criterio di consenso](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) per filtrare i profili non autorizzati non devono intraprendere alcuna azione.
><br/>
>I clienti che non hanno acquistato Adobe Privacy &amp; Security Shield devono utilizzare le funzionalità [segment definition](../../../segmentation/home.md#segment-definitions) all&#39;interno di [Segment Builder](../../../segmentation/ui/segment-builder.md) per filtrare i profili non autorizzati e continuare a utilizzare senza interruzioni le destinazioni Real-Time CDP Google esistenti.

## Quando utilizzare questa destinazione

Nel catalogo delle destinazioni sono disponibili diverse integrazioni con Google e potrebbe essere difficile capire quando utilizzare ciascuna delle destinazioni Google disponibili. Valuta i diversi casi d’uso leggendo le informazioni riportate nella tabella seguente:

| [Customer Match di Google](/help/destinations/catalog/advertising/google-customer-match.md) | [Schermo e video Google 360](/help/destinations/catalog/advertising/google-dv360.md) | [!DNL Google Customer Match] + [!DNL Display & Video 360] (questo connettore) |
|---------|----------|---------|
| Esporta i tipi di pubblico basati su PII e raggiungili nell&#39;inventario disponibile in [!DNL Google Customer Match]. | Raggiungi il pubblico basato su cookie nell&#39;inventario disponibile tramite [!DNL Google Display & Video 360], nelle proprietà possedute e gestite da Google come Youtube e [!DNL Search] e oltre. | Crea tipi di pubblico basati su PII in [!DNL Google Customer Match] e raggiungili nell&#39;inventario disponibile in [!DNL Google Display & Video 360], solo nelle proprietà possedute e gestite da Google. |

## Casi d’uso {#use-cases}

Per aiutarti a capire meglio come e quando utilizzare questa destinazione, ecco alcuni casi d’uso di esempio che i clienti di Adobe Experience Platform possono risolvere utilizzando questa funzione.

### #1 del caso d’uso

Un marchio di abbigliamento sportivo desidera raggiungere i clienti esistenti tramite [!DNL Google Search] e [!DNL Google Shopping] per personalizzare offerte ed articoli in base ai loro acquisti passati e alla cronologia di navigazione. Il marchio di abbigliamento può acquisire indirizzi e-mail dal proprio CRM per Experience Platform e creare tipi di pubblico dai propri dati offline. Quindi, possono inviare questi tipi di pubblico alla destinazione [!DNL Google Customer Match + Display & Video 360] per essere utilizzati in [!DNL Google Display & Video 360] proprietà quali [!DNL Search], [!DNL YouTube], [!DNL Gmail] e [!DNL Google Display Network].

### #2 del caso d’uso

Un&#39;importante azienda tecnologica ha lanciato un nuovo telefono. Per promuovere questo nuovo modello di telefono, sono alla ricerca di far conoscere le nuove caratteristiche e funzionalità del telefono ai clienti che possiedono modelli precedenti dei loro telefoni.

Per promuovere la versione, caricano in Experience Platform gli indirizzi e-mail dal proprio database CRM, utilizzando gli indirizzi e-mail come identificatori. I tipi di pubblico vengono creati in base ai clienti che possiedono modelli di telefono meno recenti. I tipi di pubblico vengono quindi inviati a [!DNL Google Customer Match], in modo che l&#39;azienda possa eseguire il targeting dei clienti correnti, dei clienti che possiedono modelli di telefono precedenti e di clienti simili in [!DNL Google Display & Video 360] proprietà quali [!DNL Search], [!DNL YouTube], [!DNL Gmail] e [!DNL Google Display Network].

## Identità supportate {#supported-identities}

[!DNL Google Customer Match] supporta l&#39;attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/features/namespaces.md).

| Identità di destinazione | Descrizione | Considerazioni |
|---|---|---|
| phone_sha256_e.164 | Numeri di telefono in formato E164, con hash con l’algoritmo SHA256 | I numeri di telefono con hash SHA256 e testo normale sono supportati da Adobe Experience Platform. Segui le istruzioni riportate nella sezione [Requisiti di corrispondenza ID](#id-matching-requirements-id-matching-requirements) e utilizza gli spazi dei nomi appropriati rispettivamente per i numeri di telefono con testo normale e con hash. Se il campo di origine contiene attributi senza hash, selezionare l&#39;opzione **[!UICONTROL Applica trasformazione]** per impostare [!DNL Platform] per l&#39;hashing automatico dei dati all&#39;attivazione. |
| email_lc_sha256 | Indirizzi e-mail con hash con algoritmo SHA256 | Adobe Experience Platform supporta sia gli indirizzi di posta elettronica in testo normale che quelli con hash SHA256. Segui le istruzioni riportate nella sezione [Requisiti di corrispondenza ID](#id-matching-requirements-id-matching-requirements) e utilizza gli spazi dei nomi appropriati rispettivamente per gli indirizzi e-mail in testo normale e con hash. Se il campo di origine contiene attributi senza hash, selezionare l&#39;opzione **[!UICONTROL Applica trasformazione]** per impostare [!DNL Platform] per l&#39;hashing automatico dei dati all&#39;attivazione. |

{style="table-layout:auto"}

<!-- not supported in beta

|GAID|Google Advertising ID|Select this target identity when your source identity is a GAID namespace.|
|IDFA|Apple ID for Advertisers|Select this target identity when your source identity is an IDFA namespace.|
|user_id|Custom user IDs|Select this target identity when your source identity is a custom namespace.| 

-->

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
| Tipo di esportazione | **[!UICONTROL Esportazione pubblico]** | Stai esportando tutti i membri di un pubblico con gli identificatori (nome, numero di telefono e altri) utilizzati nella destinazione [!DNL Google Customer Match]. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni sulle [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Prerequisiti per l&#39;account [!DNL Google Customer Match] {#google-account-prerequisites}

Prima di configurare una destinazione [!DNL Google Customer Match] in Experience Platform, assicurarsi di leggere e rispettare i criteri di Google per l&#39;utilizzo di [!DNL Customer Match], descritti nella [documentazione di supporto Google](https://support.google.com/google-ads/answer/6299717).

Verificare quindi che l&#39;account [!DNL Google] sia configurato per un livello di autorizzazione [!DNL Standard] o superiore. Per informazioni dettagliate, consulta la [documentazione di Google Ads](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1).

### Elenco consentiti {#allowlist}

Prima di creare la destinazione [!DNL Google Customer Match] in Experience Platform, assicurati che il tuo account [!DNL Google Ads] sia conforme ai [[!DNL Google Customer Match] criteri](https://support.google.com/google-ads/answer/6299717/customer-match-policy).

I clienti con account conformi vengono inseriti nell&#39;elenco Consentiti automaticamente da Google.

## Requisiti di corrispondenza ID {#id-matching-requirements}

[!DNL Google] non richiede l&#39;invio di informazioni personali (PII, personally identifiable information) in chiaro. Pertanto, i tipi di pubblico attivati in [!DNL Google Customer Match] devono essere ricavati da *identificatori con hash*, ad esempio indirizzi e-mail con hash o numeri di telefono.

A seconda del tipo di ID inseriti in Adobe Experience Platform, devi rispettare i requisiti corrispondenti.

### Requisiti di hashing del numero di telefono {#phone-number-hashing-requirements}

Esistono due metodi per attivare i numeri di telefono in [!DNL Google Customer Match]:

* **Acquisizione di numeri di telefono non elaborati**: è possibile acquisire i numeri di telefono non elaborati nel formato [!DNL E.164] in [!DNL Platform] e vengono automaticamente sottoposti a hashing al momento dell&#39;attivazione. Se si sceglie questa opzione, assicurarsi di inserire sempre i numeri di telefono non elaborati nello spazio dei nomi `Phone_E.164`.
* **Inserimento di numeri di telefono con hash**: è possibile inserire i numeri di telefono con hash prima dell&#39;acquisizione in [!DNL Platform]. Se scegli questa opzione, assicurati di acquisire sempre i numeri di telefono con hash nello spazio dei nomi `PHONE_SHA256_E.164`.

>[!NOTE]
>
>Impossibile attivare nella destinazione [!DNL Google Customer Match + DV360] i numeri di telefono acquisiti nello spazio dei nomi `Phone`.

### Requisiti di hashing delle e-mail {#hashing-requirements}

Puoi eseguire l&#39;hashing degli indirizzi e-mail prima di acquisirli in Adobe Experience Platform, oppure utilizzare gli indirizzi e-mail in chiaro nell&#39;Experience Platform e disporre di [!DNL Platform] hashing al momento dell&#39;attivazione.

Per ulteriori informazioni sui requisiti di hashing di Google e altre restrizioni all’attivazione, consulta le seguenti sezioni nella documentazione di Google:

* [[!DNL Customer Match] con indirizzo e-mail, indirizzo o ID utente](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] considerazioni](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_considerations)
* [[!DNL Customer Match] con numero di telefono](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_phone_number)
* [[!DNL Customer Match] con ID dispositivo mobile](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_mobile_device_ids)


Per informazioni sull&#39;acquisizione degli indirizzi e-mail in Experience Platform, consulta la [panoramica sull&#39;acquisizione batch](../../../ingestion/batch-ingestion/overview.md) e la [panoramica sull&#39;acquisizione in streaming](../../../ingestion/streaming-ingestion/overview.md).

Se scegli di eseguire l’hash degli indirizzi e-mail da solo, assicurati di soddisfare i requisiti di Google, descritti nei collegamenti riportati sopra.

<!-- ### Using custom namespaces {#custom-namespaces}

Before you can use the `User_ID` namespace to send data to Google, make sure you synchronize your own identifiers using [!DNL gTag]. Refer to the [Google official documentation](https://support.google.com/google-ads/answer/9199250) for detailed information. -->

<!-- Data from unhashed namespaces is automatically hashed by [!DNL Platform] upon activation.

Attribute source data is not automatically hashed. When your source field contains unhashed attributes, check the **[!UICONTROL Apply transformation]** option, to have [!DNL Platform] automatically hash the data on activation.
![Identity mapping transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png) -->

<!-- ## Configure destination - video walkthrough {#video}

The video below demonstrates the steps to configure a [!DNL Google Customer Match] destination and activate audiences. The steps are also laid out sequentially in the next sections.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng) -->

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, sono necessarie le **[!UICONTROL Destinazioni visualizzazione]** e le **[!UICONTROL Autorizzazioni di gestione delle destinazioni]** [per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md).

### Parametri di connessione {#parameters}

Durante la [configurazione](../../ui/connect-destination.md) di questa destinazione, è necessario fornire le seguenti informazioni:

* **[!UICONTROL Nome]**: fornisci un nome per questa connessione di destinazione
* **[!UICONTROL Descrizione]**: fornisci una descrizione per questa connessione di destinazione
* **[!UICONTROL ID account]**: [ID cliente Google Ads](https://support.google.com/google-ads/answer/1704344?hl=en). Il formato dell’ID è xxx-xxx-xxxx. Se utilizzi [!DNL Google Ads Manager Account (My Client Center)], non utilizzare il tuo ID account manager. Utilizza invece l&#39;[ID cliente di Google Ads](https://support.google.com/google-ads/answer/1704344?hl=en).
* **[!UICONTROL Tipo di account]**: il tipo di account Google. Seleziona un’opzione, a seconda del tipo di account pubblicitario con Google:
   * **[!UICONTROL Visualizza partner video]**
   * **[!UICONTROL Visualizza inserzionista video]**

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli per la connessione di destinazione, seleziona **[!UICONTROL Avanti]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità* nelle destinazioni, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Visualizza grafo identità]** [Controllo di accesso](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](../../assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Per istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione, consulta [Attivare i dati del pubblico nelle destinazioni di esportazione del pubblico in streaming](../../ui/activate-segment-streaming-destinations.md).

<!-- In the **[!UICONTROL Segment schedule]** step, you must provide the [!UICONTROL App ID] when sending [!DNL IDFA] or [!DNL GAID] audiences to [!DNL Google Customer Match].

![Google Customer Match App ID field highlighted in the Segment schedule step of the activation workflow.](../../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

For details on how to find the [!DNL App ID], refer to the [Google official documentation](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.CrmBasedUserList#appid) or ask your Google representative. -->

### Esempio di mappatura: attivazione dei dati del pubblico in [!DNL Google Customer Match + Display & Video 360] {#example-gcm}

Questo è un esempio di mapping di identità corretto durante l&#39;attivazione dei dati del pubblico in [!DNL Google Customer Match + Display & Video 360].

Selezione dei campi di origine:

* Selezionare lo spazio dei nomi `Email` come identità di origine se gli indirizzi e-mail utilizzati non sono con hash.
* Seleziona lo spazio dei nomi `Email_LC_SHA256` come identità di origine se esegui l&#39;hashing degli indirizzi e-mail dei clienti al momento dell&#39;acquisizione dei dati in [!DNL Platform], in base a [!DNL Google Customer Match] [requisiti di hashing delle e-mail](#hashing-requirements).
* Selezionare lo spazio dei nomi `PHONE_E.164` come identità di origine se i dati sono costituiti da numeri di telefono senza hash. [!DNL Platform] eseguirà l&#39;hash dei numeri di telefono per soddisfare i requisiti di [!DNL Google Customer Match].
* Seleziona lo spazio dei nomi `Phone_SHA256_E.164` come identità di origine se hai aggiunto l&#39;hashing ai numeri di telefono al momento dell&#39;acquisizione dei dati in [!DNL Platform], in base ai [!DNL Facebook] [requisiti di hashing dei numeri di telefono](#phone-number-hashing-requirements).

Selezione dei campi di destinazione:

* Selezionare lo spazio dei nomi `Email_LC_SHA256` come identità di destinazione quando gli spazi dei nomi di origine sono `Email` o `Email_LC_SHA256`.
* Selezionare lo spazio dei nomi `Phone_SHA256_E.164` come identità di destinazione quando gli spazi dei nomi di origine sono `PHONE_E.164` o `Phone_SHA256_E.164`.

![Mappatura identità tra campi di origine e di destinazione visualizzata nel passaggio Mappatura del flusso di lavoro di attivazione.](../../assets/catalog/advertising/google-customer-match-dv360/identity-mapping-gcm-dv360.png)

I dati degli spazi dei nomi senza hash vengono automaticamente sottoposti a hashing da [!DNL Platform] al momento dell&#39;attivazione.

L&#39;hash dei dati di origine degli attributi non viene eseguito automaticamente. Se il campo di origine contiene attributi senza hash, selezionare l&#39;opzione **[!UICONTROL Applica trasformazione]** per impostare [!DNL Platform] per l&#39;hashing automatico dei dati all&#39;attivazione.

![Applica controllo di trasformazione evidenziato nel passaggio di mappatura del flusso di lavoro di attivazione.](../../assets/catalog/advertising/google-customer-match-dv360/transformation.png)

## Monitorare la destinazione

Dopo la connessione alla destinazione e la definizione di un flusso di dati di destinazione, puoi utilizzare la [funzionalità di monitoraggio](/help/dataflows/ui/monitor-destinations.md) in Real-Time CDP per ottenere informazioni dettagliate sui record del profilo attivati nella destinazione in ogni esecuzione del flusso di dati.

Le informazioni di monitoraggio per la connessione [!DNL Google Customer Match + Display & Video 360] includono informazioni a livello di pubblico relative a identità attivate, escluse e non riuscite in ogni flusso di dati e flusso di dati eseguito. Ulteriori informazioni sulla funzionalità.

## Verifica che l’attivazione del pubblico sia avvenuta correttamente {#verify-activation}

Dopo aver completato il flusso di attivazione, passa all&#39;account **[!UICONTROL Google Ads]**. I tipi di pubblico attivati vengono visualizzati nel tuo account Google come elenchi di clienti. A seconda della dimensione del pubblico, alcuni tipi di pubblico non si popolano a meno che non vi siano più di 1000 utenti attivi da distribuire. Ulteriori informazioni sono disponibili nella [documentazione di Google Audience Partner](https://developers.google.com/audience-partner/api/docs/customer-match/get-started#verify-list). Tieni presente che devi chiedere a Google di accedere alla documentazione nel collegamento.

## Governance dei dati

Alcune destinazioni in Experience Platform hanno determinate regole e obblighi per i dati inviati alla piattaforma di destinazione o ricevuti da essa. L’utente è responsabile della comprensione delle limitazioni e degli obblighi relativi ai suoi dati e di come utilizza tali dati in Adobe Experience Platform e nella piattaforma di destinazione. Adobe Experience Platform fornisce strumenti di governance dei dati per aiutarti a gestire alcuni di questi obblighi in materia di utilizzo dei dati. [Ulteriori informazioni](../../../data-governance/labels/overview.md) sugli strumenti e i criteri di governance dei dati.

## Risoluzione dei problemi {#troubleshooting}

### 400 Messaggio di errore di richiesta non valida {#bad-request}

Durante la configurazione di questa destinazione, potrebbe venire visualizzato il seguente errore:

`{"message":"Google Customer Match Error: OperationAccessDenied.ACTION_NOT_PERMITTED","code":"400 BAD_REQUEST"}`

Questo errore si verifica quando gli account cliente non sono conformi ai [prerequisiti](#google-account-prerequisites). Per risolvere il problema, contattare Google e verificare che l&#39;account sia inserito nell&#39;elenco Consentiti e configurato per un livello di autorizzazione [!DNL Standard] o superiore. Per informazioni dettagliate, consulta la [documentazione di Google Ads](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1).
