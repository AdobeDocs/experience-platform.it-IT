---
keywords: piattaforma;destinazioni;area di lavoro destinazioni;area di lavoro;ui;interfaccia destinazioni;catalogo;catalogo destinazioni;
title: Area di lavoro Destinazioni
description: 'L’area di lavoro Destinazioni è composta da cinque sezioni: Panoramica, Catalogo, Sfoglia, Account e Vista sistema. Sono descritti nelle sezioni seguenti.'
exl-id: 0f46f08d-0fe3-441d-933a-86bc146c0f19
source-git-commit: 69e1f065cb3b302c4b144f39c84179075379f648
workflow-type: tm+mt
source-wordcount: '1223'
ht-degree: 2%

---

# Area di lavoro Destinazioni {#destinations-workspace}

In Adobe Experience Platform, seleziona **[!UICONTROL Destinazioni]** dalla barra di navigazione a sinistra per accedere al [!UICONTROL Destinazioni] workspace.

La [!UICONTROL Destinazioni] lo spazio di lavoro è costituito da cinque sezioni, [!UICONTROL Panoramica], [!UICONTROL Catalogo], [!UICONTROL Sfoglia], [!UICONTROL Account]e [!UICONTROL Vista di sistema], descritto nelle sezioni seguenti.

![Dashboard della panoramica delle destinazioni con tre widget.](../assets/ui/workspace/destinations-overview.png)

## [!UICONTROL Panoramica] {#overview}

La **[!UICONTROL Panoramica]** visualizza la scheda [!UICONTROL Destinazioni] dashboard, fornendo metriche chiave correlate ai dati di destinazione della tua organizzazione. Per ulteriori informazioni, visita il [[!UICONTROL Destinazioni] guida del dashboard](../../dashboards/guides/destinations.md).

>[!NOTE]
>
>Se la tua organizzazione ha poca esperienza con Experience Platform e non dispone ancora di destinazioni attive, la [!UICONTROL Destinazioni] dashboard [!UICONTROL Panoramica] non sono visibili. Invece, selezionando [!UICONTROL Destinazioni] nel menu di navigazione a sinistra viene visualizzata la [[!UICONTROL Catalogo] scheda](#catalog).

![Scheda Panoramica della dashboard Destinazioni .](../../dashboards/images/destinations/dashboard-overview.png)

## [!UICONTROL Catalogo] {#catalog}

La **[!UICONTROL Catalogo]** visualizza un elenco di tutte le destinazioni disponibili in [!DNL Platform], a cui puoi inviare i dati.

La [!DNL Platform] l’interfaccia utente fornisce diverse opzioni di ricerca e filtro nella pagina del catalogo delle destinazioni:

* Utilizza la funzionalità di ricerca nella pagina per individuare una destinazione specifica.
* Filtra le destinazioni utilizzando [!UICONTROL Categorie] controllo.
* Passa da [!UICONTROL Tutte le destinazioni] e [!UICONTROL Destinazioni personali]. Quando selezioni **[!UICONTROL Tutte le destinazioni]**, tutti disponibili [!DNL Platform] vengono visualizzate le destinazioni. Quando selezioni **[!UICONTROL Destinazioni personali]**, puoi visualizzare solo le destinazioni con le quali hai stabilito una connessione.
* Seleziona per visualizzare il **[!UICONTROL Connessioni]** e/o **[!UICONTROL Estensioni]** tipi. Per comprendere la differenza tra le due categorie, leggere [Tipi di destinazione e categorie](../destination-types.md).

![Catalogo delle destinazioni che mostra alcune destinazioni di pubblicità e archiviazione cloud.](../assets/ui/workspace/catalog.png)

Le schede di destinazione contengono opzioni di controllo principali e secondarie. I controlli principali includono [!UICONTROL Configurazione], [!UICONTROL Attiva], [!UICONTROL Attivare i segmenti]oppure [!UICONTROL Esportare i set di dati]. I controlli secondari consentono opzioni di visualizzazione. Questi controlli sono descritti di seguito:

| control | Descrizione |
|---------|----------|
| [!UICONTROL Configurazione] | Consente di creare una connessione alla destinazione. |
| [!UICONTROL Attiva] | Una volta stabilita una connessione alla destinazione, puoi attivare segmenti o esportare set di dati in questa destinazione. |
| [!UICONTROL Attivare i segmenti] | Una volta stabilita una connessione alla destinazione, puoi attivare i segmenti su questa destinazione. |
| [!UICONTROL Esportare i set di dati] | Una volta stabilita una connessione alla destinazione, puoi esportare i set di dati in questa destinazione. |
| [!UICONTROL Visualizza account] | Visualizzare gli account connessi a una destinazione. |
| [!UICONTROL Visualizzare i flussi di dati] | Visualizza i flussi di attivazione dei dati esistenti per una destinazione. |
| [!UICONTROL Visualizza la documentazione] | Apre un collegamento alla pagina di documentazione per la destinazione specifica, per ulteriori informazioni e per facilitarne la configurazione. |

{style=&quot;table-layout:auto&quot;}

![Controlli sulla scheda delle destinazioni](../assets/ui/workspace/destination-card-options.png)

Seleziona una scheda di destinazione nel catalogo per aprire la barra a destra. Qui puoi vedere una descrizione della destinazione. La barra a destra fornisce gli stessi controlli descritti nella tabella precedente, compresa una descrizione della destinazione e un’indicazione della categoria e del tipo di destinazione.

![Opzioni del catalogo di destinazione](../assets/ui/workspace/destination-right-rail.png)

Per ulteriori informazioni sulle categorie di destinazione e informazioni su ciascuna destinazione, consulta la sezione [Catalogo di destinazione](../catalog/overview.md) e [Tipi di destinazione e categorie](../destination-types.md).

## [!UICONTROL Account] {#accounts}

La **[!UICONTROL Account]** La scheda ti mostra i dettagli delle connessioni stabilite con varie destinazioni e ti consente di aggiornare o eliminare i dettagli dell’account esistenti. Vedi la tabella seguente per tutte le informazioni che puoi ottenere su ogni account di destinazione.

>[!TIP]
>
> * Seleziona i puntini di sospensione (`...`) nel [!UICONTROL Piattaforma] e utilizza ![Attiva controllo](../assets/ui/workspace/add-data-symbol.png)**[!UICONTROL Attiva ]**/**[!UICONTROL  Attivare i segmenti ]**/**[!UICONTROL  Esportare i set di dati ]**per esportare segmenti o set di dati in tale destinazione.
> * Seleziona i puntini di sospensione (`...`) nel [!UICONTROL Piattaforma] e utilizza ![Controllo dei dettagli di modifica](../assets/ui/workspace/pencil-icon.png)**[!UICONTROL Modifica dettagli ]**controllo [update](update-accounts.md) i dettagli di un account di destinazione esistente.
> * Seleziona i puntini di sospensione (`...`) nel [!UICONTROL Piattaforma] e utilizza ![Elimina controllo](../assets/ui/workspace/delete-destination-symbol.png)**[!UICONTROL Elimina ]**controllo [delete](delete-destination-account.md) un account di destinazione esistente.


![Scheda Account](../assets/ui/workspace/destination-account-options.png)

| Elemento | Descrizione |
|---|---|
| [!UICONTROL Piattaforma] | Destinazione per la quale è stata impostata la connessione. |
| [!UICONTROL Tipo connessione] | Rappresenta il tipo di connessione dell&#39;account al bucket o alla destinazione di archiviazione. A seconda della destinazione, le opzioni di autenticazione sono: <ul><li>Per le destinazioni di marketing e-mail: Può essere S3, FTP o Azure Blob.</li><li>Per le destinazioni pubblicitarie in tempo reale: Server-to-server</li><li>Per le destinazioni di archiviazione cloud Amazon S3: Chiave di accesso </li><li>Per le destinazioni di archiviazione cloud SFTP: Autenticazione di base per SFTP</li><li>Autenticazione OAuth 1 o OAuth 2</li><li>Autenticazione token portatore</li></ul> |
| [!UICONTROL Nome utente] | Il nome utente selezionato nel [connessione guidata destinazione](../catalog/email-marketing/overview.md#connect-destination). |
| [!UICONTROL Destinazioni] | Rappresenta il numero di flussi di dati di destinazione univoci collegati alle informazioni di base create per una destinazione. |
| [!UICONTROL Autorizzato] | Data di autorizzazione della connessione a questa destinazione. |

{style=&quot;table-layout:auto&quot;}

## [!UICONTROL Sfogliare] {#browse}

La **[!UICONTROL Sfoglia]** visualizza le destinazioni con cui hai stabilito una connessione. Destinazioni con **[!UICONTROL Abilitato/Disabilitato]** attivata imposta la destinazione rispettivamente su attiva o inattiva. Puoi anche visualizzare le destinazioni in cui scorrono i dati selezionando **[!UICONTROL Segmenti]** > **[!UICONTROL Sfoglia]** e selezionando un segmento da esaminare. Vedi la tabella seguente per tutte le informazioni fornite per ogni destinazione nel [!UICONTROL Sfoglia] scheda:

>[!TIP]
>
> * Seleziona i puntini di sospensione (`...`) nel [!UICONTROL Nome] e utilizza ![Attiva il controllo dei segmenti](../assets/ui/workspace/add-data-symbol.png)**[!UICONTROL Attiva ]**per esportare segmenti o set di dati in tale destinazione.
> * Seleziona i puntini di sospensione (`...`) nel [!UICONTROL Nome] e utilizza ![Elimina controllo](../assets/ui/workspace/delete-destination-symbol.png)**[!UICONTROL Elimina ]**controllo [remove](delete-destinations.md) una connessione esistente a una destinazione.
> * Seleziona i puntini di sospensione (`...`) nel [!UICONTROL Nome] e utilizza ![Visualizzazione del controllo di monitoraggio](../assets/ui/workspace/monitoring-icon.png)**[!UICONTROL Visualizza nel monitoraggio ]**per visualizzare le informazioni di attivazione per questa destinazione nel [dashboard di monitoraggio](/help/dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard).
> * Seleziona i puntini di sospensione (`...`) nel [!UICONTROL Nome] e utilizza ![Iscriviti agli avvisi ](../assets/ui/workspace/alerts-icon.png)**[!UICONTROL Iscriviti agli avvisi ]**per effettuare la sottoscrizione agli avvisi relativi al flusso di dati di destinazione. Puoi abbonarti a avvisi per ricevere messaggi relativi allo stato, al successo o all’errore dell’esecuzione del flusso. Vedi [Iscriviti agli avvisi di destinazione nel contesto](alerts.md) per informazioni dettagliate sugli avvisi relativi al flusso di dati di destinazione.


![Scheda Sfoglia](../assets/ui/workspace/browse-tab.png)

| Elemento | Descrizione |
|---------|----------|
| Nome | Nome fornito per il flusso di attivazione a questa destinazione. La stessa colonna include due controlli: [!UICONTROL Attiva ] e [!UICONTROL Elimina destinazione]. |
| [!UICONTROL Stato ultima esecuzione flusso] | Lo stato dell’ultima esecuzione del flusso di dati. Vedi [Visualizza dettagli destinazione](destination-details-page.md) per ulteriori informazioni sulle esecuzioni del flusso di dati. |
| [!UICONTROL Data ultima esecuzione flusso] | Ora e data dell’ultima esecuzione del flusso di dati. Vedi [Visualizza dettagli destinazione](destination-details-page.md) per ulteriori informazioni sulle esecuzioni del flusso di dati. |
| [!UICONTROL Destinazione] | La piattaforma di destinazione selezionata per il flusso di attivazione. |
| [!UICONTROL Tipo connessione] | Rappresenta il tipo di connessione al bucket di archiviazione o alla destinazione. <ul><li>Per le destinazioni di marketing e-mail: Può essere S3, FTP o [!DNL Azure Blob].</li><li>Per le destinazioni pubblicitarie in tempo reale: Server-to-server.</li><li>Per le destinazioni di streaming: Può essere [!DNL Azure Event Hubs] o [!DNL Amazon Kinesis].</li></ul> |
| [!UICONTROL Nome utente] | Le credenziali account selezionate per il flusso di destinazione. |
| [!UICONTROL Dati di attivazione] | Indica il numero di segmenti che vengono attivati nella destinazione. Seleziona questo controllo per ulteriori informazioni sui segmenti attivati. Fai riferimento a [Dati di attivazione](/help/destinations/ui/destination-details-page.md#activation-data) nella pagina dei dettagli della destinazione per ulteriori informazioni sui segmenti attivati. |
| [!UICONTROL Creato] | Data e ora UTC in cui è stato creato il flusso di attivazione alla destinazione. Seleziona il simbolo di freccia su/giù per ordinare i flussi di attivazione in base al più recente o al più vecchio. |
| [!UICONTROL Stato] | `Enabled` oppure `Disabled`. Indica se i dati vengono attivati per questa destinazione. |

Fai clic su una riga di destinazione per visualizzare ulteriori informazioni sulla destinazione nella barra a destra.

![Fai clic sulla riga di destinazione](../assets/ui/workspace/click-destination-row.png)

Seleziona il nome della destinazione per visualizzare le informazioni sui segmenti attivati in questa destinazione. Fai clic su **[!UICONTROL Modifica attivazione]** per modificare o aggiungere ai segmenti inviati a questa destinazione.

## [!UICONTROL Vista di sistema] {#system-view}

La **[!UICONTROL Vista di sistema]** visualizza una rappresentazione grafica dei flussi di attivazione impostati in Adobe Experience Platform.

![Flussi di dati1](../assets/ui/workspace/data-flows1.png)

Seleziona una delle destinazioni visualizzate sulla pagina e fai clic su **[!UICONTROL Visualizzare i flussi di dati]** per visualizzare informazioni su tutte le connessioni configurate per ogni destinazione.

![Flussi di dati2](../assets/ui/workspace/data-flows2.png)
