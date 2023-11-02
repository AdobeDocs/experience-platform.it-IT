---
title: Analisi e tracciamento del consenso
description: Scopri come creare un dashboard di analisi del consenso per tenere traccia delle tendenze del consenso degli utenti nel tempo.
exl-id: 34accae5-8b4f-4281-8333-187a91db8199
source-git-commit: 7cde32f841497edca7de0c995cc4c14501206b1a
workflow-type: tm+mt
source-wordcount: '1912'
ht-degree: 0%

---

# Analisi e tracciamento del consenso

Nell’attuale panorama di marketing, devi comprendere e rispettare le preferenze di consenso dei clienti. Adobe Real-time Customer Data Platform consente agli esperti di marketing di analizzare il consenso dei clienti per creare fiducia, rispettare le normative sulla privacy e fornire esperienze più personalizzate.

Questo documento illustra come creare un dashboard del consenso per vari casi di utilizzo di marketing per i dati di Real-Time CDP. In particolare, si concentra sulla creazione di un pubblico con gli attributi appropriati per le esigenze aziendali, e quindi utilizza le informazioni attraverso l’utilizzo di widget preconfigurati nell’interfaccia utente di Adobe Experience Platform. Viene inoltre presentato un metodo alternativo per la creazione di widget personalizzati con la funzione delle dashboard definite dall’utente.

## Casi d’uso {#use-cases}

I casi d’uso trattati in questa guida sono la tendenza del consenso e la sovrapposizione del consenso.

- **Tendenza del consenso** tiene traccia delle tendenze del consenso degli utenti nel tempo. L’analisi delle modifiche delle preferenze di consenso aiuta gli addetti al marketing a pianificare ed eseguire campagne in grado di adattarsi alle modifiche delle preferenze utente. Ad esempio, potrebbe essere utile eseguire campagne di istruzione mirate, campagne di trasparenza e affidabilità o campagne di incentivi per indirizzare le scelte di consenso. Puoi anche correlare le campagne che potrebbero aver avuto un impatto negativo sul consenso per ridurre in modo proattivo la frequenza di tali campagne.
- **Sovrapposizione del consenso** utilizza la sovrapposizione tra i canali di consenso per fornire messaggi personalizzati coerenti su più canali per i clienti che hanno acconsentito a più canali. Gli addetti al marketing possono assegnare priorità e allocare risorse a determinati canali in cui un livello più elevato di consenso e di messaggistica personalizzata potrebbe risuonare con i clienti e generare tassi di risposta più elevati.

<!-- ## Build a consent dashboard {#build-a-consent-dashboard} -->

## Creare tipi di pubblico consentiti {#create-consent-audiences}

Per creare una dashboard di consenso, devi innanzitutto creare un pubblico di tutti i profili che hanno acconsentito a contattare. Per passare al Generatore di segmenti di Real-time Customer Data Platform, seleziona **[!UICONTROL Tipi di pubblico]** nell’area di navigazione a sinistra dell’interfaccia utente di Platform. Dalla sezione [!UICONTROL Cliente] scheda di [!UICONTROL Tipi di pubblico] dashboard, seleziona **[!UICONTROL Creare un pubblico]** in alto a destra nella vista, quindi **[!UICONTROL Creare regole]**.

<!-- Update screenshot below to include Create audience -->s

![Il [!UICONTROL Tipi di pubblico] dashboard con [!UICONTROL Cliente], [!UICONTROL Tipi di pubblico], e [!UICONTROL Crea segmento] evidenziato.](../images/insights-use-cases/consent-analysis/create-audience.png)

Viene visualizzato il Generatore di segmenti. Quindi, seleziona **[!UICONTROL Profilo individuale XDM]** dalle opzioni disponibili. Consulta la documentazione per ulteriori informazioni su [area di lavoro generatore regole](../../segmentation/ui/segment-builder.md#rule-builder-canvas).

![Generatore di segmenti con [!UICONTROL Profilo individuale XDM] cartella attributi evidenziata.](../images/insights-use-cases/consent-analysis/xdm-individual-profile.png)

Individua gli attributi del consenso tra le opzioni disponibili. Seleziona **[!UICONTROL Consensi e preferenze]**.

>[!NOTE]
>
>Se hai mantenuto il consenso utente in un attributo diverso da quello del gruppo di campi consigliato dall’Adobe, devi selezionare tali attributi invece di quelli mostrati di seguito.

Ulteriori informazioni sono disponibili sul sito [gestione del consenso nella segmentazione](../../segmentation/consents.md#handling-consent-in-segmentation) documentazione.

![Generatore di segmenti con [!UICONTROL Consenso e preferenze] cartella attributi evidenziata.](../images/insights-use-cases/consent-analysis/consent-and-preferences.png)

Vengono visualizzate le varie opzioni relative al consenso e alle preferenze. Poiché questa dimostrazione si concentra sul consenso al contatto tramite vari canali di marketing, seleziona **[!UICONTROL Preferenze di marketing]**.

![Generatore di segmenti con [!UICONTROL Preferenze di marketing] cartella evidenziata.](../images/insights-use-cases/consent-analysis/marketing-preferences.png)

Viene visualizzato l’elenco delle preferenze di marketing. Anche se questo caso d’uso di esempio si concentra su e-mail, SMS e chiamate, puoi creare informazioni approfondite per qualsiasi altra combinazione o per tutte le opzioni. Per creare un pubblico per ciascuno dei canali, esegui i passaggi seguenti.

Per iniziare a configurare un pubblico, seleziona **[!UICONTROL Ricezione SMS]** / **[!UICONTROL Ricevi e-mail]** / **[!UICONTROL Ricezione di chiamate]**.

![I canali di contatto disponibili per il marketing sono evidenziati nel generatore di pubblico.](../images/insights-use-cases/consent-analysis/channels.png)

Il [!UICONTROL Iscrizioni] cartella. Dalle opzioni disponibili, seleziona e trascina il file **[!UICONTROL Valore scelta]** al riquadro centrale, quindi selezionare il valore desiderato dal menu a discesa. In questo caso, seleziona **Sì (consenso)**. Quindi, assegna un nome al pubblico in base alle tue esigenze aziendali e fornisci una descrizione semplice.

>[!NOTE]
>
>È previsto un limite al numero di tipi di pubblico che si consiglia di creare. Ulteriori informazioni sono disponibili nella sezione [documentazione sui guardrail di segmentazione](../../profile/guardrails.md#segmentation-guardrails).

![Il [!UICONTROL Valore scelta] attributo con [!UICONTROL Sì (consenso)] valore evidenziato nel generatore di segmenti. Vengono evidenziati anche il nome e la descrizione del pubblico.](../images/insights-use-cases/consent-analysis/choice-value.png)

Dopo aver creato i tipi di pubblico necessari, questi vengono elencati in [!UICONTROL Tipi di pubblico] [!UICONTROL Sfoglia] scheda.

>[!NOTE]
>
>Quando crei un pubblico, devi attendere il completamento del processo di segmentazione batch prima che i dati siano disponibili per iniziare a creare la dashboard di consenso. La segmentazione in batch descrive il processo di spostamento simultaneo di tutti i dati del profilo attraverso le definizioni dei segmenti per produrre i tipi di pubblico corrispondenti. Una volta creato, il pubblico viene salvato e memorizzato per l’esportazione e l’utilizzo. I segmenti batch vengono valutati automaticamente ogni 24 ore.

## Consuma informazioni {#consume-insights}

Adobe ha creato diverse informazioni che sono automaticamente disponibili nelle dashboard Profili, Tipi di pubblico e Destinazioni. Tutti i tipi di pubblico creati possono quindi essere utilizzati automaticamente con queste informazioni preconfigurate. Consulta la documentazione dei widget standard per un elenco delle informazioni disponibili nella [Profili](../guides/profiles.md#standard-widgets), [Tipi di pubblico](../guides/audiences.md#standard-widgets), e [Destinazioni](../guides/destinations.md) dashboard.

## Sovrapposizione del pubblico {#audience-overlap}

Per rivedere la sovrapposizione tra due tipi di pubblico di consenso, aggiungi [!UICONTROL Sovrapposizione del pubblico con criterio di unione] nel dashboard Profili e seleziona i tipi di pubblico desiderati nei menu a discesa. Consulta la documentazione per istruzioni su come aggiungere un widget al dashboard [*Sovrapposizione del pubblico con criterio di unione*](../guides/profiles.md#audience-overlap-by-merge-policy) per ulteriori informazioni.

<!-- Image needs updating to night mode -->

![Il dashboard Profili con il widget Sovrapposizione pubblico per criterio di unione è evidenziato. Il widget visualizza le sovrapposizioni tra due tipi di pubblico di consenso.](../images/insights-use-cases/consent-analysis/audience-overlap-by-merge-policy.png)

Puoi visualizzare la sovrapposizione di tutti i tipi di pubblico in cui gli utenti hanno acconsentito a ricevere chiamate tra tutti gli altri tipi di pubblico, con il rapporto di sovrapposizione pubblico nel dashboard Tipi di pubblico. Per visualizzare la sovrapposizione dei tipi di pubblico con consenso, passa innanzitutto alla [!UICONTROL Tipi di pubblico] [!UICONTROL Panoramica] scheda. Da qui, puoi aggiungere la [!UICONTROL Rapporto di sovrapposizione pubblico] nel dashboard Tipi di pubblico. Dopo aver creato il widget, seleziona la **[!UICONTROL L’utente ha acconsentito alle chiamate]** pubblico dal menu a discesa panoramica del pubblico, nella parte superiore della pagina. Quindi, seleziona **[!UICONTROL Visualizza altro]** nel widget Rapporto di sovrapposizione pubblico per visualizzare fino a 50 delle sovrapposizioni principali e fino a 50 delle sovrapposizioni meno rilevanti relative al segmento selezionato.

<!-- Image needs updating to night mode -->

![Viene visualizzato il dashboard Tipi di pubblico con il widget Rapporto di sovrapposizione pubblico. L’utente ha acconsentito alle chiamate pubblico come pubblico di confronto ed è evidenziato il collegamento Visualizza altro.](../images/insights-use-cases/consent-analysis/audience-overlap-report-user-consent-to-calls.png)

La finestra di dialogo Rapporto di sovrapposizione pubblico si espande per mostrare ulteriori dati di sovrapposizione pubblico.

<!-- Image needs updating to night mode -->

![Il rapporto di sovrapposizione del pubblico, in cui viene evidenziato come Utenti hanno acconsentito all’invio di e-mail al pubblico.](../images/insights-use-cases/consent-analysis/additional-audience-overlap-reports.png)

## Tendenze dimensione pubblico {#audience-size-trends}

Quando crei un pubblico basato sul consenso, viene automaticamente creata una tendenza fino a 12 mesi dalla data di creazione del pubblico. Per avere una tendenza completamente funzionale del consenso del cliente, aggiungi i seguenti widget alla [!UICONTROL Segmenti] [!UICONTROL Panoramica] pagina. Queste informazioni offrono un mezzo potente per monitorare come cambia il consenso nel tempo. Sono anche correlate a qualsiasi campagna eseguita in parallelo che potrebbe avere un impatto positivo o negativo sul consenso. Le descrizioni offerte per questi widget si applicano a un caso di utilizzo del consenso.

- [Tendenza dimensione pubblico](../guides/audiences.md#audience-size-trend): questo widget offre un modo per tenere traccia di come il rispettivo consenso è cambiato nel tempo.
- [Tendenza di modifica della dimensione del pubblico](../guides/audiences.md#audience-size-change-trend): questo widget tiene traccia delle modifiche giornaliere del consenso dei clienti. Ad esempio, se il conteggio del consenso del cliente è diminuito di 100.000, puoi vedere come si è verificata la modifica su base giornaliera.
- [Tendenza dimensione pubblico per identità](../guides/audiences.md#audience-size-trend-by-identity): con questo widget puoi tenere traccia di come il rispettivo consenso è cambiato nel tempo, ma ulteriormente filtrato da un’identità specifica, ad esempio un’e-mail.

<!-- Image needs updating to night mode -->

![Viene visualizzata la dashboard Tipi di pubblico con i widget Tendenza dimensione pubblico, Tendenza dimensione pubblico per identità e Tendenza modifica dimensione pubblico. Viene evidenziato Utenti che hanno acconsentito all’invio di e-mail al pubblico.](../images/insights-use-cases/consent-analysis/three-audience-trend-widgets.png)

## Dashboard panoramica di Audiences {#audiences-overview-dashboard}

Dopo aver creato un pubblico correlato al consenso, ad esempio &quot;Utenti autorizzati agli SMS&quot;, puoi visualizzare informazioni chiave e personalizzate sul consenso relative al pubblico aggiungendo i widget appropriati alla dashboard Panoramica tipi di pubblico. Accedi a [!UICONTROL Tipi di pubblico] [!UICONTROL Panoramica] e aggiungi i widget scelti dalla libreria di widget. Qualsiasi widget aggiunto alla vista del dashboard può essere ridimensionato e spostato utilizzando [!UICONTROL Modifica dashboard] funzionalità. La vista personalizzata può contenere informazioni come la tendenza nel tempo (fino a 12 mesi), le sovrapposizioni con altri tipi di pubblico e la composizione dell’identità del pubblico. Di seguito è riportata una visualizzazione di esempio.

![Il dashboard dei tipi di pubblico con gli utenti che hanno acconsentito all’invio di SMS è evidenziato nel menu a discesa del pubblico globale.](../images/insights-use-cases/consent-analysis/audience-dashboard-user-consent-to-sms.png)

## Dashboard definite dall’utente {#usr-defined-dashboards}

Puoi anche creare widget personalizzati con dashboard definite dall’utente. La creazione di un widget personalizzato offre il controllo completo sul tipo di widget, insieme alla flessibilità necessaria per aggiungere filtri e molto altro, direttamente in Adobe Real-Time CDP.

Ad esempio, se desideri presentare più tipi di pubblico per il consenso nello stesso grafico, in modo da poter vedere nel tempo come ciascuna delle tue preferenze di consenso è cambiata. Questo tipo di visualizzazione è possibile con dashboard definiti dall’utente in passaggi minimi e una configurazione una tantum. Seleziona innanzitutto **[!UICONTROL Dashboard]** nel menu di navigazione a sinistra. Il [!UICONTROL Dashboard] viene visualizzato workspace. Quindi seleziona **[!UICONTROL Crea dashboard]**. Istruzioni complete su come [creare un dashboard e un widget personalizzato](../user-defined-dashboards.md) sono disponibili nella guida delle dashboard definite dall’utente.

![L’area di lavoro delle dashboard con le dashboard e Crea dashboard evidenziate.](../images/user-defined-dashboards/create-dashboard.png)

Quando [seleziona il modello dati](../user-defined-dashboards.md#select-data-model) nel compositore widget, seleziona `CDPInsights` seguito da **[!UICONTROL Successivo]**. Il [!UICONTROL Seleziona tabella] viene visualizzata.

![La finestra di dialogo Seleziona modello dati con il modello CDPInsights evidenziato.](../images/user-defined-dashboards/select-data-model-dialog.png)

Nella vista successiva viene visualizzato un elenco delle tabelle disponibili nella barra a sinistra. Seleziona `adwh_fact_profile_by_segment_and_namespace_trendlines`.

![Viene evidenziata la finestra di dialogo Seleziona tabella con la tabella adwh_fact_profile_by_segment_and_namespace_trendlines.](../images/insights-use-cases/consent-analysis/select-table.png)

Dopo aver popolato il compositore di widget con i dati della tabella scelta, effettua le seguenti operazioni:

- [Ricerca [!UICONTROL Attributi]](../user-defined-dashboards.md#add-filter-attributes) per `[!UICONTROL date]`, quindi utilizza l’icona + per aggiungere `[!UICONTROL date]` all&#39;asse X dal menu a discesa.
  ![Il compositore widget con l’icona del componente aggiuntivo e il menu a discesa evidenziati.](../images/user-defined-dashboards/attributes-dropdown.png)
- Ricerca [!UICONTROL Attributi] per `[!UICONTROL count_of_profiles]`, quindi utilizza l’icona + per aggiungere `[!UICONTROL count_of_profiles]` per l&#39;asse Y dal menu a discesa.
- Seleziona la `...` (puntini di sospensione) nella [!UICONTROL Asse Y] , quindi selezionare il [!UICONTROL SOMMA] funzione di aggregazione dal menu a discesa.
  ![Il widget Compositore widget Tendenze di consenso con il modello dati, la tabella, il menu a discesa dell’asse Y e la funzione SOMMA evidenziati. ](../images/insights-use-cases/consent-analysis/y-axis-sum-function.png)
- Seleziona la [!UICONTROL Indicatori] e modificare il tipo di grafico in [!UICONTROL Linea].
- Ricerca [!UICONTROL Attributi] per `[!UICONTROL segment_name]`, quindi utilizza l’icona + per aggiungere `segment_name` as a [!UICONTROL Filtro] dal menu a discesa. Il [!UICONTROL Filtro: Nome_segmento] viene visualizzata. Seleziona i tipi di pubblico creati in precedenza che si riferiscono al consenso. Per questo esempio, seleziona **[!UICONTROL Utenti autorizzati alle chiamate]**, **[!UICONTROL Utenti autorizzati all’invio di SMS]**, e **[!UICONTROL Utenti autorizzati a inviare messaggi e-mail]**, seguito da **[!UICONTROL Applica]**.
- Ricerca [!UICONTROL Attributi] per `[!UICONTROL segment_name]`, quindi seleziona l’icona + da aggiungere `segment_name` as a [!UICONTROL Colore] dal menu a discesa.
- Apri [il [!UICONTROL Proprietà] pannello](../user-defined-dashboards.md#widget-properties) e fornire un [!UICONTROL Titolo widget] e [!UICONTROL Etichetta asse].
  ![Il compositore di widget con l&#39;icona delle proprietà e il titolo del widget evidenziato.](../images/user-defined-dashboards/properties-panel.png)
- Seleziona **[!UICONTROL Salva e chiudi]** per confermare le impostazioni.

>[!TIP]
>
>È ora possibile ridimensionare o spostare il widget alle dimensioni e alla posizione desiderate prima di salvare il dashboard.


L’immagine seguente illustra come viene visualizzato il widget finito e altre potenziali informazioni personalizzate. Per ulteriori dettagli sui tipi di widget che è possibile creare, fare riferimento a [documentazione del modello dati](../cdp-insights-data-model.md).

<!-- The diagram shows straight lines due to a lack of data, however in your environment the trends will reflect the actual changes over time. -->

![Il widget delle tendenze di consenso personalizzato finito.](../images/insights-use-cases/consent-analysis/consent-trends-widget.png)

## Tracciamento dei criteri di consenso {#consent-policies}

Le dashboard di consenso create acquisiscono **solo distribuzione del consenso e degli attributi di preferenza**.

>[!NOTE]
>
>Per i clienti di **Schermo sanitario Adobe** o **Adobe Privacy &amp; Security Shield**, queste dashboard **non** riflettere eventuali tracciamenti dei criteri di consenso. Il tracciamento disponibile include il numero di criteri creati, abilitati e l’impatto sull’iscrizione del pubblico.

## Passaggi successivi

Dopo aver letto questo documento, hai imparato a creare dashboard per una visualizzazione completa delle preferenze di consenso del cliente utilizzando Real-Time CDP Insights. Questo documento illustra come Real-Time CDP fornisce una soluzione solida per l’attuale panorama incentrato sulla privacy, in cui la raccolta, la segmentazione, l’analisi e le campagne di marketing personalizzate basate sui dati del consenso sono fondamentali per gli esperti marketing.
