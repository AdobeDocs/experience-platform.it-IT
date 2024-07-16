---
title: Connessione PX Gainsight
description: Utilizza la destinazione Gainsight PX per inviare informazioni sulla segmentazione alla piattaforma Gainsight PX.
last-substantial-update: 2024-02-20T00:00:00Z
exl-id: 0ca0d34f-f866-4f59-80f8-60198fbb86be
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 2%

---

# Connessione PX Gainsight {#gainsight-px}

## Panoramica {#overview}

[[!DNL Gainsight PX]](https://www.gainsight.com/product-experience/) è una piattaforma di esperienza del prodotto che consente ai team di prodotto di comprendere in che modo gli utenti utilizzano i loro prodotti, raccogliere feedback e creare impegni in-app, ad esempio procedure dettagliate sui prodotti, per favorire l&#39;onboarding degli utenti e l&#39;adozione dei prodotti.

>[!IMPORTANT]
>
>Il connettore di destinazione e la pagina della documentazione vengono creati e gestiti dal team *Gainsight PX*. Per richieste di informazioni o richieste di aggiornamento, contattale direttamente all&#39;indirizzo *`pxsupport@gainsight.com`*.

## Casi d’uso {#use-cases}

Per aiutarti a capire meglio come e quando utilizzare la destinazione *Gainsight PX*, ecco alcuni esempi di casi d&#39;uso che i clienti di Adobe Experience Platform possono risolvere utilizzando questa destinazione.

### Targeting degli accordi in-app {#targeting-in-app-engagements}

Un&#39;azienda SaaS vuole coinvolgere i propri clienti tramite una guida in-application costruita su Gainsight PX. Un pubblico per ricevere questo coinvolgimento è stato creato su Adobe Experience Platform. La destinazione PX di Gainsight riceve il pubblico e lo rende disponibile all&#39;interno dell&#39;ambiente PX di Gainsight.

## Prerequisiti {#prerequisites}

* Contatta il team di supporto [!DNL Gainsight] e richiedi l&#39;attivazione delle funzionalità dei segmenti esterni per il tuo abbonamento.
* Genera un valore OAuth Secret per la sottoscrizione PX, utilizzando il pulsante **[!UICONTROL Genera nuovo segreto]** nella parte inferiore della [pagina Dettagli società](https://app.aptrinsic.com/settings/subscription)
  ![Schermata Dettagli società in Gainsight PX che mostra il pulsante Genera nuovo segreto](../../assets/catalog/analytics/gainsight-px/generate_oauth_secret.png)

## Identità supportate {#supported-identities}

Gainsight PX supporta l’attivazione delle identità descritte nella tabella seguente. Ulteriori informazioni su [identità](../../../identity-service/features/namespaces.md).

| Identità di destinazione | Descrizione |
|---|----|
| IdentifyID | Identificatore utente comune che identifica in modo univoco un utente in Gainsight PX e Adobe Experience Platform |

{style="table-layout:auto"}

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive il tipo di pubblico che puoi esportare in questa destinazione.

| Origine pubblico | Supportato | Descrizione |
|---|---|---|
| [!DNL Segmentation Service] | ✓ | Tipi di pubblico generati tramite il servizio di segmentazione [Experience Platform](../../../segmentation/home.md). |
| Caricamenti personalizzati | X | Tipi di pubblico [importati](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform da file CSV. |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
|---|---|---|
| Tipo di esportazione | **[!UICONTROL Esportazione segmento]** | Stai esportando tutti i membri di un pubblico con gli identificatori (nome, numero di telefono o altri) utilizzati nella destinazione [!DNL Gainsight PX]. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Quando un profilo viene aggiornato in Experience Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni sulle [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
>
>Per connettersi alla destinazione, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Gestione destinazioni]** [controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autenticarsi nella destinazione {#authenticate}

Per eseguire l&#39;autenticazione nella destinazione, compilare i campi obbligatori e selezionare **[!UICONTROL Connetti alla destinazione]**.

![Schermata di autenticazione](../../assets/catalog/analytics/gainsight-px/auth-screen.png)

* **[!UICONTROL Password]**: password utilizzata per accedere a [[!DNL Gainsight PX]](https://app.aptrinsic.com)
* **[!UICONTROL ID client]**: ID sottoscrizione Gainsight PX nella [pagina Dettagli società](https://app.aptrinsic.com/settings/subscription)
* **[!UICONTROL Segreto client]**: il segreto OAuth generato nella parte inferiore della [pagina Dettagli società](https://app.aptrinsic.com/settings/subscription) nell&#39;interfaccia utente [!DNL Gainsight PX].
* **[!UICONTROL Nome utente]**: indirizzo e-mail utilizzato per accedere all&#39;interfaccia utente [[!DNL Gainsight PX]](https://app.aptrinsic.com)

### Inserire i dettagli della destinazione {#destination-details}

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

![Schermata dei dettagli della destinazione nell&#39;interfaccia utente dell&#39;Experience Platform che mostra come compilare i campi Nome e Descrizione](../../assets/catalog/analytics/gainsight-px/destination_details.png)

* **[!UICONTROL Nome]**: un nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: una descrizione che ti aiuterà a identificare questa destinazione in futuro.

Dopo aver fornito i dettagli per la connessione di destinazione, seleziona **[!UICONTROL Avanti]**.

## Attiva i segmenti in questa destinazione {#activate}

>[!IMPORTANT]
>
>* Per attivare i dati, è necessario **[!UICONTROL Gestire le destinazioni]**, **[!UICONTROL Attivare le destinazioni]**, **[!UICONTROL Visualizzare i profili]** e **[!UICONTROL Visualizzare i segmenti]** [accedere alle autorizzazioni di controllo](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Visualizza grafo identità]** [Controllo di accesso](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Leggi [Attivare profili e segmenti nelle destinazioni di esportazione dei segmenti di streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per le istruzioni sull&#39;attivazione dei segmenti di pubblico in questa destinazione.

### Mappare le identità {#map}

Questa destinazione supporta la mappatura degli attributi del profilo e degli spazi dei nomi di identità. La mappatura di destinazione deve essere sempre lo spazio dei nomi dell&#39;identità **[!UICONTROL IDENTIFICATION_ID]**.

Consulta gli esempi seguenti per comprendere meglio come configurare la mappatura.

#### Mappare un attributo di profilo {#map-profile-attribute}

Nell’esempio mostrato di seguito, il campo sorgente è un attributo di profilo XDM che viene mappato sullo spazio dei nomi di destinazione IDENTIFICATION_ID.

![Esempio di schermata di mappatura dello spazio dei nomi dell&#39;identità che mostra come selezionare i valori di origine e di destinazione](../../assets/catalog/analytics/gainsight-px/mapping_attribute.png)

#### Mappare uno spazio dei nomi delle identità {#map-identity-namespace}

Nell&#39;esempio riportato di seguito, il campo di origine è uno spazio dei nomi di identità (**[!UICONTROL ECID]**) che viene mappato allo spazio dei nomi di destinazione **[!UICONTROL IDENTIID]**.

![Schermata di mapping degli attributi che mostra come selezionare i valori di origine e di destinazione](../../assets/catalog/analytics/gainsight-px/mapping_identities.png)

## Dati esportati / Convalida esportazione dati {#exported-data}

I dati di segmentazione vengono inviati in streaming dall’Experience Platform al Gainsight PX.

I metadati del segmento sono visibili nella schermata Segmenti nell&#39;interfaccia utente [!DNL Gainsight PX].

![Schermata dell&#39;elenco dei segmenti in Gainsight PX che mostra i segmenti esterni.](../../assets/catalog/analytics/gainsight-px/segment_metadata.png)

Le informazioni sull&#39;appartenenza al segmento sono visibili nella scheda Segmenti della schermata Audience Explorer dell&#39;interfaccia utente [!DNL Gainsight PX].

![Schermata di Audience Explorer in Gainsight PX che mostra i segmenti associati per un utente.](../../assets/catalog/analytics/gainsight-px/PX_Segments.png)

## Utilizzo dei dati e governance {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, leggere la [Panoramica sulla governance dei dati](/help/data-governance/home.md).
