---
title: Google Display e connessione Video 360
description: Display & Video 360, precedentemente noto come DoubleClick Bid Manager, è uno strumento utilizzato per eseguire campagne digitali di retargeting e targeting del pubblico tra le origini di inventario Display, Video e Mobile.
exl-id: bdd3b3fd-891f-44ec-bd47-daf7f3289f92
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1155'
ht-degree: 2%

---

# Connessione [!DNL Google Display & Video 360]

>[!IMPORTANT]
>
> Google sta rilasciando modifiche all&#39;API [Google Ads](https://developers.google.com/google-ads/api/docs/start), [Customer Match](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html) e all&#39;API [Display &amp; Video 360](https://developers.google.com/display-video/api/guides/getting-started/overview) per supportare i requisiti relativi alla conformità e al consenso definiti nel [Digital Markets Act](https://digital-markets-act.ec.europa.eu/index_en) (DMA) nell&#39;Unione Europea ([EU User Consent Policy](https://www.google.com/about/company/user-consent-policy/)). L’applicazione di queste modifiche ai requisiti di consenso è attiva dal 6 marzo 2024.
><br/>
>Per aderire alla politica di consenso degli utenti dell’UE e continuare a creare elenchi di pubblico per gli utenti dello Spazio economico europeo (SEE), gli inserzionisti e i partner devono assicurarsi di trasmettere il consenso degli utenti finali durante il caricamento dei dati sul pubblico. In qualità di partner Google, Adobe fornisce gli strumenti necessari per soddisfare i requisiti di consenso ai sensi dell’accordo DMA nell’Unione Europea.
><br/>
>I clienti che hanno acquistato Adobe Privacy &amp; Security Shield e hanno configurato un [criterio di consenso](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) per filtrare i profili non autorizzati non devono intraprendere alcuna azione.
><br/>
>I clienti che non hanno acquistato Adobe Privacy &amp; Security Shield devono utilizzare le funzionalità [segment definition](../../../segmentation/home.md#segment-definitions) all&#39;interno di [Segment Builder](../../../segmentation/ui/segment-builder.md) per filtrare i profili non autorizzati e continuare a utilizzare senza interruzioni le destinazioni Real-Time CDP Google esistenti.

[!DNL Display & Video 360], precedentemente noto come [!DNL DoubleClick Bid Manager], è uno strumento utilizzato per eseguire campagne digitali di retargeting e targeting del pubblico tra le origini di inventario Display, Video e Mobile.

## Specifiche della destinazione {#specifics}

Osservare i dettagli seguenti specifici per [!DNL Google Display & Video 360] destinazioni:

* I tipi di pubblico attivati vengono creati a livello di programmazione nella piattaforma Google.
* L&#39;attivazione dei backfill del pubblico nella destinazione [!DNL Google Display & Video 360] è pianificata per 24-48 ore dopo che un pubblico è stato mappato per la prima volta a una connessione di destinazione. Questo aggiornamento risponde alla policy di Google di attendere 24 ore prima dell&#39;acquisizione dei dati ed è inteso a migliorare le percentuali di corrispondenza tra Real-Time CDP e [!DNL Google Display & Video 360]. Si tratta di una configurazione back-end applicabile solo a questa destinazione e non correlata ad alcuna opzione di pianificazione configurabile dal cliente nell’interfaccia utente.

>[!IMPORTANT]
>
>Se stai cercando di creare la tua prima destinazione con Google Display &amp; Video 360 e non hai abilitato in passato la funzionalità di sincronizzazione ID [1} nel servizio ID Experience Cloud (con Adobe Audience Manager o altre applicazioni), contatta Adobe Consulting o l&#39;Assistenza clienti per abilitare le sincronizzazioni ID. ](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) Se in precedenza avevi configurato le integrazioni Google in Audience Manager, le sincronizzazioni ID configurate vengono trasferite a Platform.

## Identità supportate {#supported-identities}

[!DNL Google Display & Video 360] supporta l&#39;attivazione di tipi di pubblico in base alle identità mostrate nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/features/namespaces.md).

| Identità | Descrizione | Considerazioni |
|---|---|---|
| GAID | [!DNL Google Advertising ID] |  |
| IDFA | [!DNL Apple ID for Advertisers] |  |
| UUID AAM | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html), noto anche come [!DNL Device ID]. Un ID dispositivo numerico di 38 cifre che Audience Manager associa a ogni dispositivo con cui interagisce. | Google utilizza [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html) per eseguire il targeting degli utenti in California e l&#39;ID cookie di Google per tutti gli altri utenti. |
| ID cookie [!DNL Google] | ID cookie [!DNL Google] | [!DNL Google] utilizza questo ID per eseguire il targeting degli utenti al di fuori della California. |
| RIDA | ID Roku per Advertising. Questo ID identifica in modo univoco i dispositivi Roku. |  |
| DOMESTICA | MICROSOFT ADVERTISING ID Questo ID identifica in modo univoco i dispositivi con Windows 10. |  |
| ID Amazon Fire TV | Questo ID identifica in modo univoco i televisori Amazon Fire. |  |

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
| Tipo di esportazione | **[!UICONTROL Esportazione pubblico]** | Stai esportando tutti i membri di un pubblico nella destinazione Google. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni sulle [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

## Prerequisiti {#prerequisites}

### Inserimento nell’elenco Consentiti {#allow-listing}

>[!NOTE]
>
>L&#39;inserimento nell&#39;elenco Consentiti è obbligatorio prima di configurare la prima destinazione [!DNL Google Display & Video 360] in Platform. Prima di creare una destinazione, assicurati che il processo di inserimento nell&#39;elenco Consentiti descritto di seguito sia stato completato da [!DNL Google].
>Eccezione a questa regola per [clienti Audience Manager](https://docs.adobe.com/content/help/it-IT/experience-cloud/user-guides/home.translate.html). Se hai già creato una connessione a questa destinazione Google in Audience Manager, non è necessario ripetere nuovamente la procedura di inserimento nell’elenco Consentiti e puoi procedere ai passaggi successivi.

Prima di creare la destinazione [!DNL Google Display & Video 360] in Platform, è necessario contattare Google per richiedere l&#39;inserimento di un Adobe nell&#39;elenco dei provider di dati consentiti e l&#39;aggiunta dell&#39;account al inserisco nell&#39;elenco Consentiti di. Contattare Google e fornire le seguenti informazioni:

* **ID account**: ID account di Adobe con Google. ID account: 87933855.
* **ID cliente**: ID account cliente di Adobe con Google. ID cliente: 89690775.
* **Tipo di account**: utilizza **[!DNL Invite advertiser]** per consentire la condivisione dei tipi di pubblico solo con un marchio specifico nell&#39;account Display &amp; Video 360 o **[!DNL Invite partner]** per consentire la condivisione dei tipi di pubblico con tutti i marchi nell&#39;account Display &amp; Video 360.

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, sono necessarie le **[!UICONTROL Destinazioni visualizzazione]** e le **[!UICONTROL Autorizzazioni di gestione delle destinazioni]** [per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md).

### Parametri di connessione {#parameters}

Durante la [configurazione](../../ui/connect-destination.md) di questa destinazione, è necessario fornire le seguenti informazioni:

* **[!UICONTROL Nome]**: immettere il nome preferito per la destinazione.
* **[!UICONTROL Descrizione]**: facoltativo. Ad esempio, puoi indicare per quale campagna stai utilizzando questa destinazione.
* **[!UICONTROL Tipo di account]**: seleziona un&#39;opzione, a seconda dell&#39;account con Google:
   * Utilizza `Invite Advertiser` per consentire la condivisione dei tipi di pubblico solo con un marchio specifico nell&#39;account Display &amp; Video 360.
   * Utilizza `Invite Partner` per consentire la condivisione dei tipi di pubblico con tutti i marchi presenti nel tuo account Display &amp; Video 360.
* **[!UICONTROL ID account]**: inserisci l&#39;ID account **[!DNL Invite partner]** o **[!DNL Invite advertiser]** in Google. In genere, si tratta di un ID di sei o sette cifre.

>[!NOTE]
>
>Durante la configurazione di una destinazione [!DNL Google Display & Video 360], rivolgiti al tuo rappresentante [!DNL Google Account Manager] o Adobe per capire quale tipo di account hai.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli per la connessione di destinazione, seleziona **[!UICONTROL Avanti]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione, consulta [Attivare i dati del pubblico nelle destinazioni di esportazione del pubblico in streaming](../../ui/activate-segment-streaming-destinations.md).

## Dati esportati

Per verificare se i dati sono stati esportati correttamente nella destinazione [!DNL Google Display & Video 360], controllare l&#39;account [!DNL Google Display & Video 360]. Se l&#39;attivazione ha esito positivo, i tipi di pubblico vengono popolati nel tuo account.

## Risoluzione dei problemi {#troubleshooting}

### 400 Messaggio di errore di richiesta non valida {#bad-request}

Durante la configurazione di questa destinazione, potrebbe venire visualizzato il seguente errore:

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

Questo errore si verifica quando gli account cliente non sono conformi ai [prerequisiti](#prerequisites). Per risolvere il problema, contatta Google e assicurati che il tuo account sia inserito nell’elenco Consentiti.