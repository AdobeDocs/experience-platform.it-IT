---
keywords: piattaforma;destinazioni;area di lavoro;area di lavoro;interfaccia utente;destinazioni;catalogo;destinazioni catalogo;platform;destinations workspace;workspace;ui;destinations ui;catalog;destinations catalog;
title: Area di lavoro destinazioni
description: 'L’area di lavoro Destinazioni è costituita da cinque sezioni: Panoramica, Catalogo, Sfoglia, Account e Visualizzazione sistema. Sono descritte nelle sezioni seguenti.'
exl-id: 0f46f08d-0fe3-441d-933a-86bc146c0f19
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '2150'
ht-degree: 0%

---

# Area di lavoro destinazioni {#destinations-workspace}

In Adobe Experience Platform, selezionare **[!UICONTROL Destinations]** dalla barra di navigazione a sinistra per accedere all&#39;area di lavoro [!UICONTROL Destinations].

L&#39;area di lavoro [!UICONTROL Destinations] è costituita da cinque sezioni, [!UICONTROL Overview], [!UICONTROL Catalog], [!UICONTROL Browse], [!UICONTROL Accounts] e [!UICONTROL System View], descritte nelle sezioni seguenti.

![Il dashboard della panoramica delle destinazioni mostra tre widget.](../assets/ui/workspace/destinations-overview.png)

## [!UICONTROL Overview] {#overview}

Nella scheda **[!UICONTROL Overview]** viene visualizzata la dashboard [!UICONTROL Destinations], che fornisce le metriche chiave relative ai dati di destinazione della tua organizzazione. Per ulteriori informazioni, visitare la guida del dashboard [[!UICONTROL Destinations]](../../dashboards/guides/destinations.md).

>[!NOTE]
>
>Se la tua organizzazione ha poca esperienza con Experience Platform e non dispone ancora di destinazioni attive, la dashboard [!UICONTROL Destinations] e la scheda [!UICONTROL Overview] non sono visibili. Se invece si seleziona [!UICONTROL Destinations] dal menu di navigazione a sinistra, verrà visualizzata la scheda [[!UICONTROL Catalog]](#catalog).

![Scheda Panoramica del dashboard Destinazioni.](../../dashboards/images/destinations/dashboard-overview.png)

## [!UICONTROL Catalog] {#catalog}

Nella scheda **[!UICONTROL Catalog]** viene visualizzato un elenco di tutte le destinazioni disponibili in [!DNL Experience Platform] a cui è possibile inviare dati.

![Il catalogo delle destinazioni mostra più destinazioni.](../assets/ui/workspace/catalog.png)

L&#39;interfaccia utente di [!DNL Experience Platform] fornisce diverse opzioni di ricerca e filtro nella pagina del catalogo delle destinazioni:

* Utilizza la funzionalità di ricerca nella pagina per individuare una destinazione specifica.
* Filtrare le destinazioni utilizzando il controllo **[!UICONTROL Categories]**.
* Consente di passare da **[!UICONTROL All destinations]** a **[!UICONTROL My destinations]**. Quando selezioni **[!UICONTROL All destinations]**, vengono visualizzate tutte le [!DNL Experience Platform] destinazioni disponibili. Quando selezioni **[!UICONTROL My destinations]**, puoi visualizzare solo le destinazioni con le quali hai stabilito una connessione.
* Selezionare per visualizzare i tipi **[!UICONTROL Connections]** e/o **[!UICONTROL Extensions]**. Per comprendere la differenza tra le due categorie, leggere [Tipi di destinazione e Categorie](../destination-types.md).
* Filtra le destinazioni disponibili in base al tipo di dati [supportato](/help/destinations/destination-sdk/functionality/destination-configuration/audience-data-type.md). Scegli tra tipi di pubblico di persone, tipi di pubblico dell’account, tipi di pubblico di potenziali clienti o esportazioni di set di dati.

Le schede di destinazione contengono opzioni di controllo primarie e secondarie. I controlli primari includono [!UICONTROL Set up], [!UICONTROL Activate], [!UICONTROL Activate audiences] o [!UICONTROL Export datasets]. I controlli secondari consentono di visualizzare le opzioni. Questi controlli sono descritti di seguito:

| Controllo | Descrizione |
|---------|----------|
| [!UICONTROL Set up] | Consente di creare una connessione alla destinazione. |
| [!UICONTROL Activate] | Dopo aver stabilito una connessione alla destinazione, puoi attivare i tipi di pubblico o esportare i set di dati in questa destinazione. |
| [!UICONTROL Activate audiences] | Dopo aver stabilito una connessione alla destinazione, puoi attivare i tipi di pubblico per questa destinazione. |
| [!UICONTROL Export datasets] | Dopo aver stabilito una connessione alla destinazione, puoi esportare i set di dati in questa destinazione. |
| [!UICONTROL View account] | Visualizzare gli account connessi per una destinazione. |
| [!UICONTROL View dataflows] | Visualizzare i flussi di attivazione dati esistenti per una destinazione. |
| [!UICONTROL View documentation] | Apre un collegamento alla pagina della documentazione della destinazione specifica, per ulteriori informazioni e per facilitare la configurazione. |

{style="table-layout:auto"}

![Controlli sulla scheda delle destinazioni](../assets/ui/workspace/destination-card-options.png)

Seleziona una scheda di destinazione nel catalogo per aprire la barra a destra. Qui puoi vedere una descrizione della destinazione. La barra a destra fornisce gli stessi controlli descritti nella tabella precedente, inclusa una descrizione della destinazione e un’indicazione della categoria e del tipo di destinazione.

![Opzioni del catalogo di destinazione](../assets/ui/workspace/destination-right-rail.png)

Per ulteriori informazioni sulle categorie di destinazione e sulle informazioni su ciascuna destinazione, vedere [Catalogo di destinazione](../catalog/overview.md) e [Tipi e categorie di destinazione](../destination-types.md).

## [!UICONTROL Browse] {#browse}

>[!NOTE]
>
>A causa delle configurazioni delle etichette di accesso, i flussi di dati di destinazione a cui un utente non ha accesso possono essere visualizzati nell’interfaccia utente in uno stato disattivato. Per ulteriori informazioni, consulta la documentazione su [utilizzo delle etichette di accesso per gestire l&#39;accesso degli utenti ai flussi di dati di destinazione](../../access-control/abac/apply-access-labels-destinations.md#important-callouts-and-items-to-know).

Nella scheda **[!UICONTROL Browse]** sono visualizzate le destinazioni con le quali è stata stabilita una connessione.

>[!TIP]
>
> Inizia con la [barra di ricerca](#search-browse) per trovare flussi di dati specifici, quindi utilizza i [filtri barra laterale](#filter-options-browse) per limitare ulteriormente i risultati.

Le destinazioni con l&#39;opzione **[!UICONTROL Enabled/Disabled]** attivata impostano la destinazione rispettivamente su **[!UICONTROL Enabled]** o **[!UICONTROL Disabled]**. È inoltre possibile visualizzare le destinazioni in cui i dati scorrono selezionando **[!UICONTROL Audiences]** > **[!UICONTROL Browse]** e un pubblico da controllare.

>[!TIP]
>
> ![Sfoglia scheda](../assets/ui/workspace/browse-tab.png)
> 
> * Selezionare i puntini di sospensione (`...`) nella colonna [!UICONTROL Name] e utilizzare il controllo ![Attiva tipi di pubblico](/help/images/icons/data-add.png) **[!UICONTROL Activate audiences]** per esportare tipi di pubblico o set di dati in tale destinazione.
> * Selezionare i puntini di sospensione (`...`) nella colonna [!UICONTROL Name] e utilizzare il controllo ![Modifica controllo di destinazione &#x200B;](/help/images/icons/edit.png)**[!UICONTROL Edit destination]**&#x200B;per modificare le connessioni di destinazione esistenti. Per ulteriori informazioni, leggi l&#39;esercitazione su [modifica destinazioni](/help/destinations/ui/edit-destination.md).
> * Selezionare i puntini di sospensione (`...`) nella colonna [!UICONTROL Name] e utilizzare il controllo ![Modifica azioni di marketing](/help/images/icons/edit-marketing-actions.svg) **[!UICONTROL Edit marketing actions]** per [modificare le azioni di marketing](/help/destinations/ui/edit-activation.md#edit-marketing-actions) per la destinazione selezionata.
> * Selezionare i puntini di sospensione (`...`) nella colonna [!UICONTROL Name] e utilizzare il controllo ![Elimina](/help/images/icons/delete.png) **[!UICONTROL Delete]** per [rimuovere](delete-destinations.md) una connessione esistente a una destinazione.
> * Selezionare i puntini di sospensione (`...`) nella colonna [!UICONTROL Name] e utilizzare ![Visualizza nel controllo di monitoraggio](/help/images/icons/monitoring.png) **[!UICONTROL View in monitoring]** per visualizzare le informazioni di attivazione per questa destinazione nel [dashboard di monitoraggio](/help/dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard).
> * Selezionare i puntini di sospensione (`...`) nella colonna [!UICONTROL Name] e utilizzare il controllo ![Sottoscrivi avvisi](/help/images/icons/alert-add.png) **[!UICONTROL Subscribe to alerts]** per sottoscrivere gli avvisi del flusso di dati di destinazione. È possibile abbonarsi agli avvisi per ricevere messaggi relativi allo stato, al completamento o al fallimento dell’esecuzione del flusso. Per informazioni dettagliate sugli avvisi del flusso di dati di destinazione, consulta [Abbonati agli avvisi di destinazione contestuali](alerts.md).
> * Selezionare i puntini di sospensione (`...`) nella colonna [!UICONTROL Name] e utilizzare il controllo ![Gestisci tag](/help/images/icons/manage-tags.png) **[!UICONTROL Manage tags]** per aggiungere o rimuovere tag da una destinazione. Consulta la sezione [Gestione dei tag di destinazione](#manage-tags) per informazioni dettagliate sull&#39;utilizzo dei tag.

Vedere la tabella seguente per tutte le informazioni fornite per ciascuna destinazione nella scheda [!UICONTROL Browse].

| Elemento | Descrizione |
|---------|----------|
| Nome | Il nome fornito per il flusso di attivazione verso questa destinazione. |
| Tipo di dati | Tipo di dati supportato dalla connessione di destinazione. Tipi di dati supportati: <ul><li>**[!UICONTROL Customers]**</li><li>**[!UICONTROL Prospects]**</li><li>**[!UICONTROL Accounts]**</li><li>**[!UICONTROL Datasets]**</li></ul> |
| [!UICONTROL Last Dataflow Run Status] | Stato dell’ultima esecuzione del flusso di dati. Per ulteriori informazioni sulle esecuzioni dei flussi di dati, vedere [Visualizza dettagli destinazione](destination-details-page.md). |
| [!UICONTROL Last Dataflow Run Date] | Ora e data in cui si è verificata l’ultima esecuzione del flusso di dati. Selezionare l&#39;intestazione di colonna per accedere alle opzioni di ordinamento (**[!UICONTROL Sort Ascending]**, **[!UICONTROL Sort Descending]**). Per ulteriori informazioni sulle esecuzioni dei flussi di dati, vedere [Visualizza dettagli destinazione](destination-details-page.md). |
| [!UICONTROL Destination] | La piattaforma di destinazione selezionata per il flusso di attivazione. |
| [!UICONTROL Account Expiration Date] | Data di scadenza dell&#39;autorizzazione di connessione a questa destinazione. <br> Un&#39;icona di avviso ![Avviso: l&#39;icona di scadenza dell&#39;account](/help/images/icons/alert-expiration.png) viene visualizzata prima della data di scadenza per avvisarti che la connessione scadrà e potrebbe richiedere il rinnovo. I flussi di dati per le connessioni scadute vengono interrotti e devi ripetere l’autenticazione per riprendere i flussi di lavoro di attivazione. <br>**Importante**: questa colonna è attualmente disponibile solo per le connessioni [Pinterest](../catalog/advertising/pinterest.md), [LinkedIn](../catalog/social/linkedin.md) e [LinkedIn Matched Audiences](../catalog/social/linkedin-b2b.md). <br> ![Esempio di avviso di scadenza account nella scheda Sfoglia](../assets/ui/workspace/account-expiration-browse.png){width="100" zoomable="yes" alt="Screenshot showing the account expiration warning icon and expiration date in the Browse tab."} |
| [!UICONTROL Username] | Credenziali account selezionate per il flusso di destinazione. |
| [!UICONTROL Activation Data] | Indica il numero di tipi di pubblico attivati in questa destinazione. Seleziona questo controllo per ulteriori informazioni sui tipi di pubblico attivati. Per ulteriori informazioni sui tipi di pubblico attivati, consulta [Dati attivazione](/help/destinations/ui/destination-details-page.md#activation-data) nella pagina dei dettagli della destinazione. |
| [!UICONTROL Created] | Data e ora di creazione del flusso di attivazione verso la destinazione. Seleziona il simbolo freccia su/giù per ordinare i flussi di attivazione in base al primo più recente o al primo meno recente. |
| [!UICONTROL Modified] | Data e ora dell’ultima modifica del flusso di attivazione verso la destinazione. |
| [!UICONTROL Status] | `Enabled` o `Disabled`. Indica se i dati vengono attivati in questa destinazione. |
| [!UICONTROL Access labels] | Visualizza tutte le etichette di accesso aggiunte al flusso di dati di destinazione. Ulteriori informazioni sull&#39;[applicazione delle etichette di accesso ai flussi di dati di destinazione](/help/access-control/abac/apply-access-labels-destinations.md). |
| [!UICONTROL Tags] | Visualizza tutti i tag aggiunti al flusso di dati di destinazione. Utilizza i tag per organizzare e classificare i flussi di dati per facilitarne la gestione. |

Fai clic su una riga di destinazione per visualizzare ulteriori informazioni sulla destinazione nella barra a destra, come ID destinazione, descrizione, numero di tipi di pubblico attivati e altro ancora.

![Fare clic sulla riga di destinazione](../assets/ui/workspace/click-destination-row.png)

Seleziona il nome della destinazione per visualizzare informazioni sui tipi di pubblico attivati per questa destinazione. Fai clic su **[!UICONTROL Edit destination]** per [modificare le impostazioni di destinazione](/help/destinations/ui/edit-destination.md) o **[!UICONTROL Activate audiences]** per aggiungere nuovi tipi di pubblico al flusso di dati.

### Filtrare i flussi di dati nella scheda Sfoglia {#filter-browse}

La scheda **[!UICONTROL Browse]** include funzionalità di filtro e ricerca avanzate che consentono di trovare e gestire rapidamente i flussi di dati di destinazione. Utilizza la barra laterale a sinistra per applicare i filtri e la barra di ricerca per trovare flussi di dati specifici per nome.

### Funzionalità di ricerca {#search-browse}

Utilizza la barra di ricerca nella parte superiore della tabella per trovare rapidamente i flussi di dati per nome. Durante la digitazione, i risultati vengono filtrati automaticamente in modo da visualizzare solo i flussi di dati corrispondenti.

![Dimostrazione animata della ricerca di un flusso di dati di destinazione nella scheda Sfoglia](../assets/ui/workspace/search.gif)

### Opzioni filtro {#filter-options-browse}

Utilizza i filtri nella barra laterale a sinistra per restringere la ricerca.

![Filtri di destinazione nella scheda Sfoglia](../assets/ui/workspace/destination-filters.png)

* **[!UICONTROL Destination platform]**: filtra i flussi di dati per piattaforme di destinazione specifiche (ad esempio [!DNL Amazon S3], [!DNL Facebook Custom Audience], [!DNL LinkedIn Matched Audience], ecc.). È possibile selezionare più piattaforme contemporaneamente.
* **[!UICONTROL Has any tag]**: filtra i flussi di dati a cui sono assegnati tag specifici. Questo consente di organizzare e trovare flussi di dati in base all’assegnazione di tag personalizzati.
* **[!UICONTROL Status]**: Filtra i flussi di dati in base al loro stato operativo:
   * **[!UICONTROL Enabled]**: mostra solo flussi di dati attivi
   * **[!UICONTROL Disabled]**: mostra solo flussi di dati inattivi
* **[!UICONTROL Account name]**: filtra i flussi di dati in base al nome account associato. Questo ti aiuta a trovare tutti i flussi di dati connessi a un account di destinazione specifico.
* **[!UICONTROL Created]**: filtra i flussi di dati in base all&#39;utente che li ha creati. Usa questo filtro per trovare i flussi di dati creati da membri specifici del team.
* **[!UICONTROL Modified by]**: Filtra i flussi di dati in base all&#39;ultimo utente che li ha modificati. Utilizza questo filtro per identificare le modifiche recenti apportate da utenti specifici.
* **[!UICONTROL Creation date]**: Filtra i flussi di dati in base alla data di creazione utilizzando un intervallo di date:
   * **[!UICONTROL Start date]**: imposta l&#39;inizio dell&#39;intervallo di date
   * **[!UICONTROL End date]**: imposta la fine dell&#39;intervallo di date
* **[!UICONTROL Modified date]**: Filtra i flussi di dati in base alla data di modifica utilizzando un intervallo di date:
   * **[!UICONTROL Start date]**: imposta l&#39;inizio dell&#39;intervallo di date
   * **[!UICONTROL End date]**: imposta la fine dell&#39;intervallo di date

### Filtri attivi {#active-filters-browse}

I filtri applicati vengono visualizzati come tag sotto la barra di ricerca.

![Filtri attivi visualizzati come tag sotto la barra di ricerca](../assets/ui/workspace/active-filters.png)

In questa sezione è possibile:

* Visualizza tutti i filtri attualmente attivi
* Rimuovere i singoli filtri facendo clic sull&#39;icona `X` su ogni tag filtro
* Cancella tutti i filtri contemporaneamente utilizzando l&#39;opzione **[!UICONTROL Clear all]**

### Gestire i tag di destinazione {#manage-tags}

I tag consentono di organizzare e classificare i flussi di dati di destinazione per semplificarne la gestione. Puoi aggiungere e rimuovere tag dai singoli flussi di dati per raggrupparli in base alle tue esigenze aziendali.

Per aggiungere un tag a un flusso di dati, selezionare i puntini di sospensione (`...`) nella colonna **[!UICONTROL Name]** e selezionare **[!UICONTROL Manage tags]** dal menu di scelta rapida.
Digitare il nome di un nuovo tag nel campo **[!UICONTROL Tags]** e selezionare **[!UICONTROL Save]** per applicare le modifiche.

![Finestra di dialogo Gestisci tag che mostra le opzioni di selezione e creazione dei tag](../assets/ui/workspace/tags.gif)

Per rimuovere un tag da un flusso di dati, selezionare i puntini di sospensione (`...`) nella colonna **[!UICONTROL Name]** e selezionare **[!UICONTROL Manage tags]** dal menu di scelta rapida, quindi selezionare l&#39;icona `X` sul tag che si desidera rimuovere.

### Best practice per l’assegnazione tag {#tag-best-practices}

Assicurati che i flussi di dati di destinazione rimangano organizzati, facili da trovare e gestibili seguendo le linee guida sui tag riportate di seguito.

* **Utilizza nomi descrittivi**: crea tag che indichino chiaramente lo scopo o la categoria del flusso di dati (ad esempio, &quot;Campagne di marketing&quot;, &quot;Fidelizzazione clienti&quot;, &quot;Promozioni stagionali&quot;)
* **Coerenza**: utilizza una convenzione di denominazione coerente nell&#39;organizzazione
* **Semplifica**: evita di creare troppi tag, in quanto ciò può rendere il filtro meno efficace
* **Usa tag gerarchici**: prova a utilizzare i prefissi per raggruppare i tag correlati (ad esempio, &quot;Campaign-Q4&quot;, &quot;Campaign-Q1&quot;)

## [!UICONTROL Accounts] {#accounts}

La scheda **[!UICONTROL Accounts]** mostra i dettagli sulle connessioni stabilite con varie destinazioni e consente di aggiornare o eliminare i dettagli dell&#39;account esistente. Vedi la tabella seguente per tutte le informazioni che puoi ottenere su ciascun account di destinazione.

>[!TIP]
>
> * Selezionare i puntini di sospensione (`...`) nella colonna [!UICONTROL Platform] e utilizzare il controllo ![Attiva &#x200B;](/help/images/icons/data-add.png)**[!UICONTROL Activate]**/**[!UICONTROL Activate audiences]**/**[!UICONTROL Export datasets]**&#x200B;per esportare tipi di pubblico o set di dati in tale destinazione.
> * Selezionare i puntini di sospensione (`...`) nella colonna [!UICONTROL Platform] e utilizzare il controllo ![Modifica dettagli &#x200B;](/help/images/icons/edit.png)**[!UICONTROL Edit details]**&#x200B;per [aggiornare](update-accounts.md) i dettagli di un account di destinazione esistente.
> * Selezionare i puntini di sospensione (`...`) nella colonna [!UICONTROL Platform] e utilizzare il controllo ![Elimina &#x200B;](/help/images/icons/delete.png)**[!UICONTROL Delete]**&#x200B;per [eliminare](delete-destination-account.md) un account di destinazione esistente.

![Scheda Account](../assets/ui/workspace/accounts-tab.png)

| Elemento | Descrizione |
|---|---|
| [!UICONTROL Name] | Il nome assegnato all&#39;account di destinazione durante [la configurazione](connect-destination.md#authenticate) della destinazione. Selezionare l&#39;intestazione di colonna per accedere alle opzioni di ordinamento (**[!UICONTROL Sort Ascending]**, **[!UICONTROL Sort Descending]**). |
| [!UICONTROL Destination] | Connettore di destinazione per il quale è stata impostata la connessione. |
| [!UICONTROL Connection Type] | Rappresenta il tipo di connessione dell’account al bucket di archiviazione o alla destinazione. A seconda della destinazione, le opzioni di autenticazione sono: <ul><li>Per le destinazioni di e-mail marketing: può essere S3, FTP o BLOB di Azure.</li><li>Per destinazioni pubblicitarie in tempo reale: server-to-server</li><li>Per le destinazioni dell’archiviazione cloud Amazon S3: chiave di accesso </li><li>Per le destinazioni di archiviazione cloud SFTP: autenticazione di base per SFTP</li><li>Autenticazione OAuth 1 o OAuth 2</li><li>Autenticazione token Bearer</li></ul> |
| [!UICONTROL Username] | Il nome utente selezionato nel flusso di lavoro [connetti destinazione](../catalog/email-marketing/overview.md#connect-destination). |
| [!UICONTROL Connections] | Rappresenta il numero di flussi di dati di destinazione univoci e riusciti connessi alle informazioni di base create per una destinazione. |
| [!UICONTROL Authorization date] | La data in cui la connessione a questa destinazione è stata autorizzata. |
| [!UICONTROL Expiration date] | Data di scadenza dell&#39;autorizzazione di connessione a questa destinazione. <br> Icona di avviso ![Icona di avviso account scaduto.](/help/images/icons/alert-expiration.png) viene visualizzato prima della data di scadenza per avvisarti che la connessione scadrà e potrebbe richiedere il rinnovo. I flussi di dati per le connessioni scadute vengono interrotti e devi ripetere l’autenticazione per riprendere i flussi di lavoro di attivazione. <br>**Importante**: questa colonna è attualmente disponibile solo per le connessioni [Pinterest](../catalog/advertising/pinterest.md), [LinkedIn](../catalog/social/linkedin.md) e [LinkedIn Matched Audiences](../catalog/social/linkedin-b2b.md). <br> ![](../assets/ui/workspace/expired-accounts.png){width="100" zoomable="yes"} |

{style="table-layout:auto"}

### Filtra account {#filter-accounts}

La scheda **[!UICONTROL Accounts]** include funzionalità di filtro e ricerca avanzate che consentono di trovare e gestire rapidamente gli account di destinazione. Utilizza la barra laterale a sinistra per applicare i filtri e la barra di ricerca per trovare account specifici per nome.

#### Cerca account {#search-accounts}

Utilizzare la barra di ricerca nella parte superiore della tabella per trovare rapidamente i conti per nome. Durante la digitazione, i risultati vengono filtrati automaticamente in modo da visualizzare solo gli account corrispondenti.

![Barra di ricerca nella scheda Account.](../assets/ui/workspace/accounts-search.gif)

#### Opzioni filtro {#filter-options-accounts}

Utilizza i filtri nella barra laterale a sinistra per restringere la ricerca.

![Filtri account nella scheda Account](../assets/ui/workspace/account-filters.png)

* **[!UICONTROL Destination platform]**: Filtra gli account in base a piattaforme di destinazione specifiche (ad esempio: [!DNL Microsoft Bing], [!DNL Amazon S3], [!DNL Facebook Custom Audiences], [!DNL LinkedIn Matched Audiences] e così via). È possibile selezionare più piattaforme contemporaneamente.
* **[!UICONTROL Created by]**: Filtra gli account in base all&#39;utente che li ha creati. Utilizzare questo filtro per trovare account creati da membri specifici del team.

#### Filtri attivi {#active-filters-accounts}

I filtri applicati vengono visualizzati come tag sotto la barra di ricerca.

![Filtri attivi visualizzati come tag nella scheda Account](../assets/ui/workspace/accounts-active-filters.png)

In questa sezione è possibile:

* Visualizza tutti i filtri attualmente attivi
* Rimuovere i singoli filtri facendo clic sull&#39;icona `X` su ogni tag filtro
* Cancella tutti i filtri contemporaneamente utilizzando l&#39;opzione **[!UICONTROL Clear all]**

## [!UICONTROL System View] {#system-view}

Nella scheda **[!UICONTROL System View]** viene visualizzata una rappresentazione grafica dei flussi di attivazione configurati in Adobe Experience Platform.

![Flussi di dati1](../assets/ui/workspace/system-view-dataflows.png)

Selezionare una delle destinazioni visualizzate nella pagina e fare clic su **[!UICONTROL View dataflows]** per visualizzare informazioni su tutte le connessioni impostate per ogni destinazione.

![Flussi di dati2](../assets/ui/workspace/system-view-dataflows-2.png)
