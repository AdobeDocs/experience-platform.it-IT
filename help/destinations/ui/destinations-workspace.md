---
keywords: piattaforma;destinazioni;area di lavoro;area di lavoro;interfaccia utente;destinazioni;catalogo;destinazioni catalogo;platform;destinations workspace;workspace;ui;destinations ui;catalog;destinations catalog;
title: Area di lavoro destinazioni
description: 'L’area di lavoro Destinazioni è costituita da cinque sezioni: Panoramica, Catalogo, Sfoglia, Account e Visualizzazione sistema. Sono descritte nelle sezioni seguenti.'
exl-id: 0f46f08d-0fe3-441d-933a-86bc146c0f19
source-git-commit: dad07add8c5f9cc98a187c2e2222a51611dbd1a2
workflow-type: tm+mt
source-wordcount: '1231'
ht-degree: 0%

---

# Area di lavoro destinazioni {#destinations-workspace}

In Adobe Experience Platform, seleziona **[!UICONTROL Destinazioni]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Destinazioni].

L&#39;area di lavoro [!UICONTROL Destinazioni] è costituita da cinque sezioni, [!UICONTROL Panoramica], [!UICONTROL Catalogo], [!UICONTROL Sfoglia], [!UICONTROL Account] e [!UICONTROL Visualizzazione sistema], come descritto nelle sezioni seguenti.

![Il dashboard della panoramica delle destinazioni mostra tre widget.](../assets/ui/workspace/destinations-overview.png)

## [!UICONTROL Panoramica] {#overview}

Nella scheda **[!UICONTROL Panoramica]** è visualizzata la dashboard [!UICONTROL Destinazioni], che fornisce le metriche chiave relative ai dati di destinazione della tua organizzazione. Per ulteriori informazioni, visita la [[!UICONTROL Guida del dashboard ] Destinazioni](../../dashboards/guides/destinations.md).

>[!NOTE]
>
>Se la tua organizzazione non ha ancora Experienci Platform e non dispone ancora di destinazioni attive, la dashboard [!UICONTROL Destinazioni] e la scheda [!UICONTROL Panoramica] non sono visibili. Se invece selezioni [!UICONTROL Destinazioni] dalla navigazione a sinistra, viene visualizzata la scheda [[!UICONTROL Catalogo]](#catalog).

![Scheda Panoramica del dashboard Destinazioni.](../../dashboards/images/destinations/dashboard-overview.png)

## [!UICONTROL Catalogo] {#catalog}

Nella scheda **[!UICONTROL Catalogo]** viene visualizzato un elenco di tutte le destinazioni disponibili in [!DNL Platform] a cui è possibile inviare i dati.

L&#39;interfaccia utente di [!DNL Platform] fornisce diverse opzioni di ricerca e filtro nella pagina del catalogo delle destinazioni:

* Utilizza la funzionalità di ricerca nella pagina per individuare una destinazione specifica.
* Filtra le destinazioni utilizzando il controllo [!UICONTROL Categorie].
* Passa da [!UICONTROL Tutte le destinazioni] a [!UICONTROL Le mie destinazioni]. Quando selezioni **[!UICONTROL Tutte le destinazioni]**, vengono visualizzate tutte le [!DNL Platform] destinazioni disponibili. Quando selezioni **[!UICONTROL Le mie destinazioni]**, puoi visualizzare solo le destinazioni con le quali hai stabilito una connessione.
* Selezionare per visualizzare i tipi **[!UICONTROL Connections]** e/o **[!UICONTROL Extensions]**. Per comprendere la differenza tra le due categorie, leggere [Tipi di destinazione e Categorie](../destination-types.md).

![Il catalogo delle destinazioni mostra alcune destinazioni per annunci pubblicitari e archiviazione cloud.](../assets/ui/workspace/catalog.png)

Le schede di destinazione contengono opzioni di controllo primarie e secondarie. I controlli principali includono [!UICONTROL Configurazione], [!UICONTROL Attiva], [!UICONTROL Attiva pubblico] o [!UICONTROL Esporta set di dati]. I controlli secondari consentono di visualizzare le opzioni. Questi controlli sono descritti di seguito:

| Controllo | Descrizione |
|---------|----------|
| [!UICONTROL Configurazione] | Consente di creare una connessione alla destinazione. |
| [!UICONTROL Attiva] | Dopo aver stabilito una connessione alla destinazione, puoi attivare i tipi di pubblico o esportare i set di dati in questa destinazione. |
| [!UICONTROL Attiva pubblico] | Dopo aver stabilito una connessione alla destinazione, puoi attivare i tipi di pubblico per questa destinazione. |
| [!UICONTROL Esporta set di dati] | Dopo aver stabilito una connessione alla destinazione, puoi esportare i set di dati in questa destinazione. |
| [!UICONTROL Visualizza account] | Visualizzare gli account connessi per una destinazione. |
| [!UICONTROL Visualizza flussi di dati] | Visualizzare i flussi di attivazione dati esistenti per una destinazione. |
| [!UICONTROL Visualizza documentazione] | Apre un collegamento alla pagina della documentazione della destinazione specifica, per ulteriori informazioni e per facilitare la configurazione. |

{style="table-layout:auto"}

![Controlli sulla scheda delle destinazioni](../assets/ui/workspace/destination-card-options.png)

Seleziona una scheda di destinazione nel catalogo per aprire la barra a destra. Qui puoi vedere una descrizione della destinazione. La barra a destra fornisce gli stessi controlli descritti nella tabella precedente, inclusa una descrizione della destinazione e un’indicazione della categoria e del tipo di destinazione.

![Opzioni del catalogo di destinazione](../assets/ui/workspace/destination-right-rail.png)

Per ulteriori informazioni sulle categorie di destinazione e sulle informazioni su ciascuna destinazione, vedere [Catalogo di destinazione](../catalog/overview.md) e [Tipi e categorie di destinazione](../destination-types.md).

## [!UICONTROL Account] {#accounts}

La scheda **[!UICONTROL Account]** mostra i dettagli sulle connessioni stabilite con varie destinazioni e consente di aggiornare o eliminare i dettagli dell&#39;account esistente. Vedi la tabella seguente per tutte le informazioni che puoi ottenere su ciascun account di destinazione.

>[!TIP]
>
> * Selezionare i puntini di sospensione (`...`) nella colonna [!UICONTROL Platform] e utilizzare il controllo ![Attiva controllo](../assets/ui/workspace/add-data-symbol.png)**[!UICONTROL Attiva ]**/**[!UICONTROL  Attiva tipi di pubblico ]**/**[!UICONTROL  Esporta set di dati ]**per esportare tipi di pubblico o set di dati in tale destinazione.
> * Selezionare i puntini di sospensione (`...`) nella colonna [!UICONTROL Platform] e utilizzare il controllo ![Modifica dettagli](../assets/ui/workspace/pencil-icon.png)**[!UICONTROL Modifica dettagli ]**per [aggiornare](update-accounts.md) i dettagli di un account di destinazione esistente.
> * Selezionare i puntini di sospensione (`...`) nella colonna [!UICONTROL Platform] e utilizzare il controllo ![Elimina](../assets/ui/workspace/delete-destination-symbol.png)**[!UICONTROL Elimina ]**per [eliminare](delete-destination-account.md) un account di destinazione esistente.

![Scheda Account](../assets/ui/workspace/destination-account-options.png)

| Elemento | Descrizione |
|---|---|
| [!UICONTROL Piattaforma] | La destinazione per la quale hai impostato la connessione. |
| [!UICONTROL Tipo di connessione] | Rappresenta il tipo di connessione dell’account al bucket di archiviazione o alla destinazione. A seconda della destinazione, le opzioni di autenticazione sono: <ul><li>Per le destinazioni di e-mail marketing: può essere S3, FTP o BLOB di Azure.</li><li>Per destinazioni pubblicitarie in tempo reale: server-to-server</li><li>Per le destinazioni dell’archiviazione cloud Amazon S3: chiave di accesso </li><li>Per le destinazioni di archiviazione cloud SFTP: autenticazione di base per SFTP</li><li>Autenticazione OAuth 1 o OAuth 2</li><li>Autenticazione token Bearer</li></ul> |
| [!UICONTROL Nome utente] | Il nome utente selezionato nella procedura guidata [connetti destinazione](../catalog/email-marketing/overview.md#connect-destination). |
| [!UICONTROL Destinazioni] | Rappresenta il numero di flussi di dati di destinazione univoci e riusciti connessi alle informazioni di base create per una destinazione. |
| [!UICONTROL Autorizzato] | La data in cui la connessione a questa destinazione è stata autorizzata. |

{style="table-layout:auto"}

## [!UICONTROL Sfoglia] {#browse}

Nella scheda **[!UICONTROL Sfoglia]** sono visualizzate le destinazioni con le quali è stata stabilita una connessione. Le destinazioni con l&#39;interruttore **[!UICONTROL Abilitato/Disabilitato]** sono attivate e impostano la destinazione rispettivamente su Attivo o Inattivo. Puoi anche visualizzare le destinazioni in cui i dati scorrono selezionando **[!UICONTROL Tipi di pubblico]** > **[!UICONTROL Sfoglia]** e un pubblico da controllare. Vedi la tabella seguente per tutte le informazioni fornite per ciascuna destinazione nella scheda [!UICONTROL Sfoglia]:

>[!TIP]
>
> * Selezionare i puntini di sospensione (`...`) nella colonna [!UICONTROL Name] e utilizzare il controllo ![Activate audiences](../assets/ui/workspace/add-data-symbol.png)**[!UICONTROL Activate ]**per esportare tipi di pubblico o set di dati in tale destinazione.
> * Selezionare i puntini di sospensione (`...`) nella colonna [!UICONTROL Nome] e utilizzare il controllo ![Elimina](../assets/ui/workspace/delete-destination-symbol.png)**[!UICONTROL Elimina ]**per [rimuovere](delete-destinations.md) una connessione esistente a una destinazione.
> * Selezionare i puntini di sospensione (`...`) nella colonna [!UICONTROL Name] e utilizzare la ![View nel controllo di monitoraggio](../assets/ui/workspace/monitoring-icon.png)**[!UICONTROL View nel controllo di monitoraggio ]**per visualizzare le informazioni di attivazione per questa destinazione nel [dashboard di monitoraggio](/help/dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard).
> * Seleziona i puntini di sospensione (`...`) nella colonna [!UICONTROL Name] e utilizza il controllo ![Subscribe to alerts ](../assets/ui/workspace/alerts-icon.png)**[!UICONTROL Subscribe to alerts ]**per sottoscrivere gli avvisi sul flusso di dati di destinazione. È possibile abbonarsi agli avvisi per ricevere messaggi relativi allo stato, al completamento o al fallimento dell’esecuzione del flusso. Per informazioni dettagliate sugli avvisi del flusso di dati di destinazione, consulta [Abbonati agli avvisi contestuali di destinazione](alerts.md).

![Sfoglia scheda](../assets/ui/workspace/browse-tab.png)

| Elemento | Descrizione |
|---------|----------|
| Nome | Il nome fornito per il flusso di attivazione verso questa destinazione. La stessa colonna include due controlli: [!UICONTROL Attiva] e [!UICONTROL Elimina destinazione]. |
| [!UICONTROL Stato ultima esecuzione flusso] | Stato dell’ultima esecuzione del flusso di dati. Per ulteriori informazioni sulle esecuzioni dei flussi di dati, vedere [Visualizza dettagli destinazione](destination-details-page.md). |
| [!UICONTROL Data ultima esecuzione flusso] | Ora e data in cui si è verificata l’ultima esecuzione del flusso di dati. Per ulteriori informazioni sulle esecuzioni dei flussi di dati, vedere [Visualizza dettagli destinazione](destination-details-page.md). |
| [!UICONTROL Destinazione] | La piattaforma di destinazione selezionata per il flusso di attivazione. |
| [!UICONTROL Tipo di connessione] | Rappresenta il tipo di connessione al bucket di archiviazione o alla destinazione. <ul><li>Per le destinazioni di e-mail marketing: può essere S3, FTP o [!DNL Azure Blob].</li><li>Per destinazioni pubblicitarie in tempo reale: server-to-server.</li><li>Per le destinazioni di streaming: può essere [!DNL Azure Event Hubs] o [!DNL Amazon Kinesis].</li></ul> |
| [!UICONTROL Nome utente] | Credenziali account selezionate per il flusso di destinazione. |
| [!UICONTROL Dati attivazione] | Indica il numero di tipi di pubblico attivati in questa destinazione. Seleziona questo controllo per ulteriori informazioni sui tipi di pubblico attivati. Per ulteriori informazioni sui tipi di pubblico attivati, consulta [Dati attivazione](/help/destinations/ui/destination-details-page.md#activation-data) nella pagina dei dettagli della destinazione. |
| [!UICONTROL Creato] | Data e ora UTC in cui è stato creato il flusso di attivazione verso la destinazione. Seleziona il simbolo freccia su/giù per ordinare i flussi di attivazione in base al primo più recente o al primo meno recente. |
| [!UICONTROL Stato] | `Enabled` o `Disabled`. Indica se i dati vengono attivati in questa destinazione. |

Fai clic su una riga di destinazione per visualizzare ulteriori informazioni sulla destinazione nella barra a destra, come ID destinazione, descrizione, numero di tipi di pubblico attivati e altro ancora.

![Fare clic sulla riga di destinazione](../assets/ui/workspace/click-destination-row.png)

Seleziona il nome della destinazione per visualizzare informazioni sui tipi di pubblico attivati per questa destinazione. Fai clic su **[!UICONTROL Modifica attivazione]** per modificare o aggiungere i tipi di pubblico che vengono inviati a questa destinazione.

## [!UICONTROL Visualizzazione sistema] {#system-view}

Nella scheda **[!UICONTROL Visualizzazione sistema]** è visualizzata una rappresentazione grafica dei flussi di attivazione configurati in Adobe Experience Platform.

![Flussi di dati1](../assets/ui/workspace/data-flows1.png)

Seleziona una delle destinazioni visualizzate nella pagina e fai clic su **[!UICONTROL Visualizza flussi di dati]** per visualizzare informazioni su tutte le connessioni impostate per ciascuna destinazione.

![Flussi di dati2](../assets/ui/workspace/data-flows2.png)
