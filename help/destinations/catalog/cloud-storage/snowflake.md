---
title: Connessione streaming Snowflake
description: Esporta dati nel tuo account Snowflake utilizzando inserzioni private.
badgeBeta: label="Beta" type="Informative"
exl-id: 4a00e46a-dedb-4dd3-b496-b0f4185ea9b0
source-git-commit: b5f28a2df411d3aa99bc2714a4e2bb569c16dda1
workflow-type: tm+mt
source-wordcount: '1128'
ht-degree: 6%

---

# Connessione streaming Snowflake {#snowflake-destination}

>[!IMPORTANT]
>
>Al momento il connettore destinazione è in versione Beta ed è disponibile solo per una clientela selezionata. Per richiedere l’accesso, contatta il tuo rappresentante Adobe.

## Panoramica {#overview}

Utilizza il connettore di destinazione Snowflake per esportare i dati nell&#39;istanza Snowflake di Adobe, che Adobe condivide con la tua istanza tramite [inserzioni private](https://other-docs.snowflake.com/en/collaboration/collaboration-listings-about).

Leggi le sezioni seguenti per scoprire come funziona la destinazione Snowflake e come i dati vengono trasferiti tra Adobe e Snowflake.

### Funzionamento della condivisione dei dati in Snowflake {#data-sharing}

Questa destinazione utilizza una condivisione dati [!DNL Snowflake], il che significa che nessun dato viene fisicamente esportato o trasferito alla tua istanza di Snowflake. Al contrario, Adobe ti consente di accedere in sola lettura a una live table ospitata nell’ambiente Snowflake di Adobe. Puoi eseguire query su questa tabella condivisa direttamente dal tuo account Snowflake, ma non sei il proprietario della tabella e non puoi modificarla o conservarla oltre il periodo di conservazione specificato. Adobe gestisce completamente il ciclo di vita e la struttura della tabella condivisa.

La prima volta che condividi i dati dall’istanza Snowflake di Adobe alla tua, ti viene richiesto di accettare l’inserzione privata da Adobe.

![Schermata che mostra la schermata di accettazione dell&#39;inserzione privata di Snowflake](../../assets/catalog/cloud-storage/snowflake/snowflake-accept-listing.png)

### Conservazione dei dati e Time-to-Live (TTL) {#ttl}

Tutti i dati condivisi tramite questa integrazione hanno un TTL (Time-to-Live) fisso di sette giorni. Sette giorni dopo l’ultima esportazione, la tabella condivisa scade automaticamente e diventa inaccessibile, indipendentemente dal fatto che il flusso di dati sia ancora attivo. Se devi conservare i dati per più di sette giorni, devi copiare il contenuto in una tabella di tua proprietà nella tua istanza di Snowflake prima della scadenza del TTL.

### Comportamento aggiornamento pubblico {#audience-update-behavior}

Se il pubblico viene valutato in [modalità batch](../../../segmentation/methods/batch-segmentation.md), i dati nella tabella condivisa vengono aggiornati ogni 24 ore. Ciò significa che può trascorrere un ritardo di 24 ore tra le modifiche nell’appartenenza al pubblico e il momento in cui tali modifiche vengono riportate nella tabella condivisa.

### Logica di esportazione incrementale {#incremental-export}

Quando un flusso di dati viene eseguito per un pubblico per la prima volta, esegue una retrocompilazione e condivide tutti i profili attualmente qualificati. Dopo questa retrocompilazione iniziale, solo gli aggiornamenti incrementali vengono rispecchiati nella tabella condivisa. Ciò significa profili che vengono aggiunti o rimossi dal pubblico. Questo approccio garantisce aggiornamenti efficienti e mantiene aggiornata la tabella condivisa.

## Prerequisiti {#prerequisites}

Prima di configurare la connessione Snowflake, accertati di soddisfare i seguenti prerequisiti:

* Si dispone dell&#39;accesso a un account [!DNL Snowflake].
* Il tuo account Snowflake è abbonato a inserzioni private. Puoi configurare questa proprietà tu o un utente della tua azienda che dispone dei privilegi di amministratore dell’account su Snowflake.

## Tipi di pubblico supportati {#supported-audiences}

Questa sezione descrive quali tipi di pubblico puoi esportare in questa destinazione. Le due tabelle seguenti indicano i tipi di pubblico supportati dal connettore, per _origine pubblico_ e _tipi di profilo inclusi nel pubblico_:

| Origine pubblico | Supportato | Descrizione |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Tipi di pubblico generati tramite Experience Platform [Segmentation Service](../../../segmentation/home.md). |
| Tutte le altre origini del pubblico | ✓ | Questa categoria include tutte le origini del pubblico al di fuori dei tipi di pubblico generati tramite [!DNL Segmentation Service]. Leggi informazioni sulle [diverse origini del pubblico](/help/segmentation/ui/audience-portal.md#customize). Alcuni esempi includono: <ul><li> i tipi di pubblico per caricamento personalizzati [importati](../../../segmentation/ui/audience-portal.md#import-audience) in Experience Platform da file CSV,</li><li> pubblico simile, </li><li> pubblico federato, </li><li> tipi di pubblico generati in altre app di Experience Platform come Adobe Journey Optimizer, </li><li> e altro ancora. </li></ul> |

{style="table-layout:auto"}

## Tipo e frequenza di esportazione {#export-type-frequency}

Per informazioni sul tipo e sulla frequenza di esportazione della destinazione, consulta la tabella seguente.

| Elemento | Tipo | Note |
---------|----------|---------|
| Tipo di esportazione | **[!UICONTROL Esportazione pubblico]** | Stai esportando tutti i membri di un pubblico con gli identificatori (nome, numero di telefono o altri) utilizzati nella destinazione [!DNL Snowflake]. |
| Frequenza di esportazione | **[!UICONTROL Streaming]** | Le destinazioni di streaming sono connessioni &quot;sempre attive&quot; basate su API. Non appena un profilo viene aggiornato in Experience Platform in base alla valutazione del pubblico, il connettore invia l’aggiornamento a valle alla piattaforma di destinazione. Ulteriori informazioni sulle [destinazioni di streaming](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Connettersi alla destinazione {#connect}

>[!IMPORTANT]
> 
>Per connettersi alla destinazione, sono necessarie le **[!UICONTROL Destinazioni visualizzazione]** e le **[!UICONTROL Autorizzazioni di gestione delle destinazioni]** [per il controllo degli accessi](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.

Per connettersi a questa destinazione, seguire i passaggi descritti nell&#39;esercitazione [sulla configurazione della destinazione](../../ui/connect-destination.md). Nel flusso di lavoro di configurazione della destinazione, compila i campi elencati nelle due sezioni seguenti.

### Autenticarsi nella destinazione {#authenticate}

Per eseguire l&#39;autenticazione nella destinazione, selezionare **[!UICONTROL Connetti alla destinazione]**.

![Schermata di esempio che mostra come autenticare nella destinazione](../../assets/catalog/cloud-storage/snowflake/authenticate-destination.png)

### Inserire i dettagli della destinazione {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_snowflake_accountID"
>title="Immetti il tuo ID account Snowflake"
>abstract="Se l’account è collegato a un’organizzazione, utilizza questo formato: `OrganizationName.AccountName`<br><br> Se invece l’account non è collegato a un’organizzazione, utilizza questo formato: `AccountName`"

Per configurare i dettagli per la destinazione, compila i campi obbligatori e facoltativi seguenti. Un asterisco accanto a un campo nell’interfaccia utente indica che il campo è obbligatorio.

![Schermata di esempio che mostra come compilare i dettagli per la destinazione](../../assets/catalog/cloud-storage/snowflake/configure-destination-details.png)

* **[!UICONTROL Nome]**: un nome con cui riconoscerai questa destinazione in futuro.
* **[!UICONTROL Descrizione]**: una descrizione che ti aiuterà a identificare questa destinazione in futuro.
* **[!UICONTROL ID account Snowflake]**: ID account Snowflake. Utilizza il seguente formato ID account, a seconda che l’account sia collegato o meno a un’organizzazione:
   * Se l&#39;account è collegato a un&#39;organizzazione:`OrganizationName.AccountName`.
   * Se l&#39;account non è collegato a un&#39;organizzazione:`AccountName`.
* **[!UICONTROL Conferma account]**: attiva la conferma ID account Snowflake per confermare che l&#39;ID account è corretto e appartiene a te.

>[!IMPORTANT]
>
> I caratteri speciali utilizzati nel nome della destinazione e nel nome della sandbox di Experience Platform vengono automaticamente convertiti in caratteri di sottolineatura (`_`) in Snowflake. Per evitare confusione, non utilizzare caratteri speciali nel nome della destinazione e della sandbox.

### Abilita avvisi {#enable-alerts}

Puoi abilitare gli avvisi per ricevere notifiche sullo stato del flusso di dati verso la tua destinazione. Seleziona un avviso dall’elenco per abbonarti e ricevere notifiche sullo stato del flusso di dati. Per ulteriori informazioni sugli avvisi, consulta la guida su [abbonamento a destinazioni avvisi tramite l&#39;interfaccia utente](../../ui/alerts.md).

Dopo aver fornito i dettagli per la connessione di destinazione, seleziona **[!UICONTROL Avanti]**.

## Attivare tipi di pubblico in questa destinazione {#activate}

>[!IMPORTANT]
> 
>* Per attivare i dati, è necessario **[!UICONTROL Visualizza destinazioni]**, **[!UICONTROL Attiva destinazioni]**, **[!UICONTROL Visualizza profili]** e **[!UICONTROL Visualizza segmenti]** [Autorizzazioni di controllo di accesso](/help/access-control/home.md#permissions). Leggi la [panoramica sul controllo degli accessi](/help/access-control/ui/overview.md) o contatta l&#39;amministratore del prodotto per ottenere le autorizzazioni necessarie.
>* Per esportare *identità*, è necessario disporre dell&#39;autorizzazione **[!UICONTROL Visualizza grafo identità]** [Controllo di accesso](/help/access-control/home.md#permissions). <br> ![Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni.](/help/destinations/assets/overview/export-identities-to-destination.png "Seleziona lo spazio dei nomi delle identità evidenziato nel flusso di lavoro per attivare i tipi di pubblico nelle destinazioni."){width="100" zoomable="yes"}

Leggi [Attivare profili e tipi di pubblico nelle destinazioni di esportazione del pubblico di streaming](/help/destinations/ui/activate-segment-streaming-destinations.md) per le istruzioni sull&#39;attivazione dei tipi di pubblico in questa destinazione.

### Mappa attributi {#map}

La destinazione Snowflake supporta la mappatura degli attributi del profilo agli attributi personalizzati.

![Immagine dell&#39;interfaccia utente di Experience Platform che mostra la schermata di mappatura per la destinazione Snowflake.](../../assets/catalog/cloud-storage/snowflake/mapping.png)

Gli attributi di destinazione vengono creati automaticamente in Snowflake utilizzando il nome di attributo specificato nel campo **[!UICONTROL Nome attributo]**.

## Dati esportati / Convalida esportazione dati {#exported-data}

Controlla il tuo account Snowflake per verificare che i dati siano stati esportati correttamente.

## Utilizzo dei dati e governance {#data-usage-governance}

Tutte le destinazioni [!DNL Adobe Experience Platform] sono conformi ai criteri di utilizzo dei dati durante la gestione dei dati. Per informazioni dettagliate su come [!DNL Adobe Experience Platform] applica la governance dei dati, leggere la [Panoramica sulla governance dei dati](/help/data-governance/home.md).
