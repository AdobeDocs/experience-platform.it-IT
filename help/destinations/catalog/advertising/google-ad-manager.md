---
keywords: google ad manager;google ad;doubleclick;DoubleClick AdX;DoubleClick;Google Ad Manager;Google ad manager; DFP
title: Connessione Google Ad Manager
description: Google Ad Manager, precedentemente noto come DoubleClick for Publishers o DoubleClick AdX, è una piattaforma di ad serving di Google che offre agli editori i mezzi per gestire la visualizzazione di annunci sui loro siti web, tramite video e nelle app mobili.
exl-id: e93f1bd5-9d29-43a1-a9a6-8933f9d85150
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1077'
ht-degree: 7%

---

# Connessione [!DNL Google Ad Manager]

>[!IMPORTANT]
>
> Google sta rilasciando modifiche all&#39;API [Google Ads](https://developers.google.com/google-ads/api/docs/start), [Customer Match](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html?lang=it) e all&#39;API [Display &amp; Video 360](https://developers.google.com/display-video/api/guides/getting-started/overview) per supportare i requisiti relativi alla conformità e al consenso definiti nel [Digital Markets Act](https://digital-markets-act.ec.europa.eu/index_it) (DMA) nell&#39;Unione Europea ([EU User Consent Policy](https://www.google.com/about/company/user-consent-policy/)). L’applicazione di queste modifiche ai requisiti di consenso è attiva dal 6 marzo 2024.
> ><br/>
> >Per aderire alla politica di consenso degli utenti dell’UE e continuare a creare elenchi di pubblico per gli utenti dello Spazio economico europeo (SEE), gli inserzionisti e i partner devono assicurarsi di trasmettere il consenso degli utenti finali durante il caricamento dei dati sul pubblico. In qualità di partner Google, Adobe fornisce gli strumenti necessari per soddisfare i requisiti di consenso ai sensi del regolamento DMA dell’Unione Europea.
> ><br/>
> >I clienti che hanno acquistato Adobe Privacy &amp; Security Shield e hanno configurato un [criterio di consenso](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) per filtrare i profili non autorizzati non devono intraprendere alcuna azione.
> ><br/>
> >I clienti che non hanno acquistato Adobe Privacy &amp; Security Shield devono utilizzare le funzionalità [segment definition](../../../segmentation/home.md#segment-definitions) all&#39;interno di [Segment Builder](../../../segmentation/ui/segment-builder.md) per filtrare i profili non autorizzati e continuare a utilizzare senza interruzioni le destinazioni Real-Time CDP Google esistenti.


[!DNL Google Ad Manager], precedentemente noto come [!DNL DoubleClick for Publishers] (DFP) o [!DNL DoubleClick AdX], è una piattaforma di ad serving di [!DNL Google] che consente agli editori di gestire la visualizzazione di annunci sui propri siti Web tramite video e app mobili.

## Specifiche della destinazione {#specifics}

Osservare i dettagli seguenti specifici per [!DNL Google Ad Manager] destinazioni:

* I tipi di pubblico attivati vengono creati a livello di programmazione nella piattaforma [!DNL Google].
* [!DNL Experience Platform] non include attualmente una metrica di misurazione per convalidare la corretta attivazione. Fai riferimento ai conteggi dei tipi di pubblico in Google per convalidare l’integrazione e comprendere le dimensioni di targeting del pubblico.
* Dopo aver mappato un pubblico a una destinazione [!DNL Google Ad Manager], il nome del pubblico viene visualizzato immediatamente nell&#39;interfaccia utente [!DNL Google Ad Manager].
* Il gruppo del segmento ha bisogno di 24-48 ore per essere visualizzato in [!DNL Google Ad Manager]. Inoltre, i tipi di pubblico devono avere una dimensione di pubblico di almeno 50 profili per essere visualizzati in [!DNL Google Ad Manager]. I tipi di pubblico con dimensioni inferiori a 50 profili non verranno popolati in [!DNL Google Ad Manager].

## Identità supportate {#supported-identities}

[!DNL Google Ad Manager] supporta l&#39;attivazione di tipi di pubblico in base alle identità mostrate nella tabella seguente. Ulteriori informazioni su [identità](/help/identity-service/features/namespaces.md).

| Identità | Descrizione | Considerazioni |
|---|---|---|
| GAID | [!DNL Google Advertising ID] |  |
| IDFA | [!DNL Apple ID for Advertisers] |  |
| UUID di AAM | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html), noto anche come [!DNL Device ID]. Un ID dispositivo numerico di 38 cifre che Audience Manager associa a ogni dispositivo con cui interagisce. | Google utilizza [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html) per eseguire il targeting degli utenti in California e l&#39;ID cookie di Google per tutti gli altri utenti. |
| ID cookie [!DNL Google] | ID cookie [!DNL Google] | [!DNL Google] utilizza questo ID per eseguire il targeting degli utenti al di fuori della California. |
| RIDA | ID Roku per Advertising. Questo ID identifica in modo univoco i dispositivi Roku. |  |
| DOMESTICA | MICROSOFT ADVERTISING ID Questo ID identifica in modo univoco i dispositivi con Windows 10. |  |
| ID Amazon Fire TV | Questo ID identifica in modo univoco i televisori Amazon Fire. |  |

{style="table-layout:auto"}

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive quali tipi di pubblico puoi esportare in questa destinazione.

| Origine pubblico | Supportato | Descrizione |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Tipi di pubblico generati tramite Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Caricamenti personalizzati | ✓ | Tipi di pubblico [importati](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform da file CSV. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
|---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Audience export]** | Stai esportando tutti i membri di un pubblico nella destinazione Google. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni sulle [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Prerequisiti {#prerequisites}

Se stai cercando di creare la tua prima destinazione con [!DNL Google Ad Manager] e non hai abilitato in passato la funzionalità di sincronizzazione [ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) nel servizio Experience Cloud ID (con Audience Manager o altre applicazioni), contatta Adobe Consulting o l&#39;Assistenza clienti per abilitare le sincronizzazioni ID. Se in precedenza avevi configurato [!DNL Google] integrazioni in Audience Manager, le sincronizzazioni ID configurate vengono trasferite ad Experience Platform.

### Inserimento nell’elenco Consentiti {#allow-listing}

L&#39;inserimento nell&#39;elenco Consentiti è obbligatorio prima di configurare la prima destinazione [!DNL Google Ad Manager] in Experience Platform. Prima di creare la destinazione, assicurati di completare il processo di inserimento nell’elenco Consentiti descritto di seguito.

1. Segui i passaggi descritti nella [documentazione di Google Ad Manager](https://support.google.com/admanager/answer/3289669?hl=en) per aggiungere Adobe come piattaforma di gestione dati collegata (DMP).
2. Nell&#39;interfaccia [!DNL Google Ad Manager], vai a **[!UICONTROL Admin]** > **[!UICONTROL Global Settings]** > **[!UICONTROL Network Settings]** e abilita il cursore **[!UICONTROL API Access]**.

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, sono necessarie le **[!UICONTROL View Destinations]** e le **[!UICONTROL Manage Destinations]** [autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md).

### Parametri di connessione {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_gam_appendSegmentID"
>title="Aggiungi ID del pubblico al nome del pubblico"
>abstract="Seleziona questa opzione per fare in modo che il nome del pubblico in Google Ad Manager includa l’ID del pubblico da Experience Platform, come riportato di seguito: `Audience Name (Audience ID)`"

Durante la [configurazione](../../ui/connect-destination.md) di questa destinazione, è necessario fornire le seguenti informazioni:

* **[!UICONTROL Name]**: immettere il nome preferito per la destinazione.
* **[!UICONTROL Description]**: facoltativo. Ad esempio, puoi indicare per quale campagna stai utilizzando questa destinazione.
* **[!UICONTROL Account ID]**: immetti [!DNL Audience Link ID] dal tuo account [!DNL Google]. Identificatore specifico associato alla rete [!DNL Google Ad Manager] (non a [!DNL Network code]). È possibile trovarlo in **[!UICONTROL Admin > Global settings]** nell&#39;interfaccia [!DNL Google Ad Manager].
* **[!UICONTROL Account Type]**: selezionare un&#39;opzione, a seconda dell&#39;account con Google:
   * Usa `DFP by Google` per [!DNL DoubleClick] per gli editori
   * Usa `AdX buyer` per [!DNL Google AdX]
* **[!UICONTROL Append audience ID to audience name]**: selezionare questa opzione affinché il nome del pubblico in Google Ad Manager includa l&#39;ID pubblico da Experience Platform, come segue: `Audience Name (Audience ID)`.

>[!NOTE]
>
>Durante la configurazione di una destinazione [!DNL Google Ad Manager], rivolgiti al tuo rappresentante [!DNL Google Account Manager] o Adobe per capire quale tipo di account hai.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli della connessione di destinazione, selezionare **[!UICONTROL Next]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>Per attivare i dati, sono necessarie le **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione, consulta [Attivare i dati del pubblico nelle destinazioni di esportazione del pubblico in streaming](../../ui/activate-segment-streaming-destinations.md).

## Dati esportati {#exported-data}

Per verificare se i dati sono stati esportati correttamente nella destinazione [!DNL Google Ad Manager], controllare l&#39;account [!DNL Google Ad Manager]. Se l&#39;attivazione ha esito positivo, i tipi di pubblico vengono popolati nel tuo account.

## Risoluzione dei problemi {#troubleshooting}

Nel caso riscontrassi errori durante l’utilizzo di questa destinazione e avessi bisogno di contattare Adobe o Google, tieni a portata di mano i seguenti ID.

Questi sono gli ID account Google di Adobe:

* **[!UICONTROL Account ID]**: 87933855
* **[!UICONTROL Customer ID]**: 89690775