---
keywords: Experience Platform;home;argomenti popolari;Applicazione dei criteri;Applicazione automatica;Imposizione basata su API;governance dei dati
solution: Experience Platform
title: Applicazione automatica dei criteri
description: Questo documento illustra come i criteri di utilizzo dei dati vengono applicati automaticamente quando si attivano tipi di pubblico nelle destinazioni in Experience Platform.
exl-id: c6695285-77df-48c3-9b4c-ccd226bc3f16
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2126'
ht-degree: 0%

---

# Applicazione automatica dei criteri

Le etichette e i criteri di utilizzo dei dati sono disponibili per tutti gli utenti di Adobe Experience Platform. Definisci i criteri di utilizzo dei dati e applica le etichette di utilizzo dei dati per garantire che tutti i dati sensibili, identificabili o contrattuali vengano gestiti in modo accurato. Queste misure aiutano a applicare le regole di governance dei dati della tua organizzazione su come accedere ai dati, elaborarli, memorizzarli e condividerli.

Per proteggere la tua organizzazione da potenziali rischi e responsabilità, Experience Platform applica automaticamente i criteri di utilizzo nel caso in cui si verifichino violazioni durante l’attivazione dei tipi di pubblico nelle destinazioni.

>[!IMPORTANT]
>
>I criteri di consenso e l&#39;applicazione automatica dei criteri di consenso sono disponibili solo per le organizzazioni che hanno acquistato **Adobe Healthcare Shield** o **Adobe Privacy &amp; Security Shield**.

Questo documento si concentra sull’applicazione della governance dei dati e dei criteri di consenso. Per informazioni sui criteri di controllo di accesso, consultare la documentazione relativa al controllo di accesso [basato su attributi](../../access-control/abac/overview.md).

## Prerequisiti

Questa guida richiede una buona conoscenza dei servizi Experience Platform coinvolti nell’applicazione automatica. Per ulteriori informazioni, consulta la seguente documentazione prima di continuare con questa guida:

* [Governance dei dati di Adobe Experience Platform](../home.md): framework tramite il quale Experience Platform impone la conformità in materia di utilizzo dei dati tramite l&#39;utilizzo di etichette e criteri.
* [Profilo cliente in tempo reale](../../profile/home.md): fornisce un profilo consumatore unificato in tempo reale basato su dati aggregati provenienti da più origini.
* [Servizio di segmentazione di Adobe Experience Platform](../../segmentation/home.md): il motore di segmentazione in [!DNL Experience Platform] utilizzato per creare tipi di pubblico dai profili dei clienti in base ai comportamenti e agli attributi dei clienti.
* [Destinazioni](../../destinations/home.md): le destinazioni sono integrazioni predefinite con applicazioni di uso comune che consentono l&#39;attivazione diretta dei dati da Experience Platform per campagne di marketing cross-channel, campagne e-mail, pubblicità mirata e altro ancora.

## Flusso di applicazione {#flow}

Il diagramma seguente illustra come l’applicazione dei criteri viene integrata nel flusso di dati di Audience Activation:

![Illustrazione del modo in cui l&#39;applicazione dei criteri viene integrata nel flusso di dati di Audience Activation.](../images/enforcement/enforcement-flow.png)

Quando un pubblico viene attivato per la prima volta, [!DNL Policy Service] controlla i criteri applicabili in base ai seguenti fattori:

* Le etichette di utilizzo dei dati applicate ai campi e ai set di dati all’interno del pubblico da attivare.
* Lo scopo di marketing della destinazione.
* I profili che hanno acconsentito a essere inclusi nell’attivazione del pubblico, in base ai criteri di consenso configurati.

>[!NOTE]
>
>Se esistono etichette di utilizzo dei dati che sono state applicate solo a determinati campi, l’applicazione di tali etichette a livello di campo all’attivazione si verifica solo se è soddisfatta almeno una delle seguenti condizioni:
>
>* I campi vengono utilizzati nel pubblico.
>* I campi sono configurati come attributi previsti per la destinazione target.

## Derivazione dei dati {#lineage}

La derivazione dei dati svolge un ruolo chiave nel modo in cui i criteri vengono applicati in Experience Platform. In termini generali, la derivazione dei dati si riferisce all’origine di un set di dati e a cosa gli accade (o dove si sposta) nel tempo.

Nel contesto della governance dei dati, la derivazione consente alle etichette di utilizzo dei dati di propagarsi dagli schemi ai servizi a valle che utilizzano i loro dati, come Profilo cliente in tempo reale e Destinazioni. Questo consente di valutare e applicare i criteri in diversi punti chiave del percorso dei dati tramite Experience Platform e fornisce ai consumatori di dati il contesto necessario per capire perché si è verificata una violazione dei criteri.

In Experience Platform, l’applicazione dei criteri riguarda la seguente derivazione:

1. I dati vengono acquisiti in Experience Platform e memorizzati in **set di dati**.
1. I profili dei clienti vengono identificati e costruiti a partire da tali set di dati unendo i frammenti di dati in base al **criterio di unione**.
1. I gruppi di profili sono divisi in **tipi di pubblico** in base agli attributi comuni.
1. I tipi di pubblico sono attivati nelle **destinazioni** a valle.

Ciascuna fase del calendario di cui sopra rappresenta un’entità che può contribuire all’applicazione delle politiche, come indicato nella tabella seguente:

| Fase di derivazione dei dati | Ruolo nell’applicazione dei criteri |
| --- | --- |
| Set di dati | I set di dati contengono etichette di utilizzo dei dati (applicate a livello di campo schema o di intero set di dati) che definiscono i casi di utilizzo per i quali è possibile utilizzare l’intero set di dati o campi specifici. Se un set di dati o un campo contenente determinate etichette viene utilizzato per uno scopo limitato da un criterio, si verificheranno violazioni dei criteri.<br><br>Nei set di dati vengono memorizzati anche tutti gli attributi di consenso raccolti dai clienti. Se hai accesso ai criteri di consenso, tutti i profili che non soddisfano i requisiti di attributo del consenso dei tuoi criteri verranno esclusi dai tipi di pubblico attivati per una destinazione. |
| Criterio di unione | I criteri di unione sono le regole utilizzate da Experience Platform per determinare il modo in cui assegnare la priorità ai dati quando si uniscono frammenti da più set di dati. Se i criteri di unione sono configurati in modo che i set di dati con etichette con restrizioni vengano attivati in una destinazione, si verificheranno violazioni dei criteri. Per ulteriori informazioni, vedere [panoramica dei criteri di unione](../../profile/merge-policies/overview.md). |
| Pubblico | Le regole di segmentazione definiscono quali attributi devono essere inclusi dai profili dei clienti. A seconda dei campi inclusi in una definizione di segmento, il pubblico erediterà tutte le etichette di utilizzo applicate per tali campi. Se tenti di attivare un pubblico le cui etichette ereditate sono limitate dai criteri applicabili della destinazione target, in base al caso di utilizzo di marketing, si verificheranno violazioni dei criteri. |
| Destinazione | Durante la configurazione di una destinazione, è possibile definire un’azione di marketing (talvolta denominata caso di utilizzo di marketing). Questo caso d’uso è correlato a un’azione di marketing definita in un criterio. In altre parole, l’azione di marketing che definisci per una destinazione determina quali criteri di utilizzo dei dati e criteri di consenso sono applicabili a tale destinazione.<br><br>Le violazioni dei criteri di utilizzo dei dati si verificano se si tenta di attivare un pubblico le cui etichette di utilizzo sono limitate per l&#39;azione di marketing della destinazione.<br><br>(Beta) Quando un pubblico viene attivato, tutti i profili che non contengono gli attributi di consenso richiesti per l&#39;azione di marketing (come definiti dai criteri di consenso) vengono esclusi dal pubblico attivato. |

>[!IMPORTANT]
>
>Alcuni criteri di utilizzo dati possono specificare due o più etichette con una relazione AND. Ad esempio, un criterio potrebbe limitare un&#39;azione di marketing se le etichette `C1` E `C2` sono entrambe presenti, ma non limita la stessa azione se è presente solo una di queste etichette.
>
>Per quanto riguarda l’applicazione automatica, il framework di governance dei dati non considera l’attivazione di tipi di pubblico separati a una destinazione come una combinazione di dati. Pertanto, il criterio `C1 AND C2` di esempio è **NOT** applicato se queste etichette sono incluse in tipi di pubblico separati. Questo criterio viene invece applicato solo quando entrambe le etichette sono presenti nello stesso pubblico al momento dell’attivazione.

Quando si verificano violazioni dei criteri, i messaggi risultanti visualizzati nell’interfaccia utente forniscono utili strumenti per esplorare la derivazione dei dati che contribuiscono alla violazione e contribuire alla risoluzione del problema. Maggiori dettagli sono forniti nella sezione successiva.

## Messaggi di applicazione dei criteri {#enforcement}

Le sezioni seguenti descrivono i diversi messaggi di applicazione dei criteri visualizzati nell’interfaccia utente di Experience Platform:

* [Violazione dei criteri di utilizzo dei dati](#data-usage-violation)
* [Valutazione dei criteri di consenso](#consent-policy-evaluation)

### Violazione dei criteri di utilizzo dei dati {#data-usage-violation}

Se si verifica una violazione dei criteri durante il tentativo di attivare un pubblico (o [apportare modifiche a un pubblico già attivato](#policy-enforcement-for-activated-audiences)), l&#39;azione non viene consentita e viene visualizzato un messaggio a comparsa che indica che uno o più criteri sono stati violati. Dopo l&#39;attivazione di una violazione, il pulsante **[!UICONTROL Salva]** viene disabilitato per l&#39;entità da modificare fino a quando i componenti appropriati non vengono aggiornati per rispettare i criteri di utilizzo dei dati.

Selezionare un nome di criterio per visualizzare i dettagli della violazione.

![Finestra di dialogo che indica che si è verificata una violazione dei criteri con il nome dei criteri evidenziato.](../images/enforcement/violation-policy-select.png)

Il messaggio di violazione fornisce un riepilogo del criterio violato, incluse le condizioni che il criterio è configurato per verificare, l’azione specifica che ha attivato la violazione e un elenco delle possibili risoluzioni del problema.

![Finestra di dialogo per violazione dei criteri con riepilogo delle violazioni evidenziato.](../images/enforcement/violation-summary.png)

Sotto il riepilogo delle violazioni viene visualizzato un grafico della derivazione dei dati che consente di visualizzare i set di dati, i criteri di unione, i tipi di pubblico e le destinazioni coinvolti nella violazione dei criteri. L’entità che stai modificando viene evidenziata nel grafico, indicando quale punto del flusso sta causando la violazione. Puoi selezionare un nome di entità all’interno del grafico per aprire la pagina dei dettagli dell’entità in questione.

![Finestra di dialogo per violazione dei criteri con grafico derivazione dati evidenziato.](../images/enforcement/data-lineage.png)

È inoltre possibile utilizzare l&#39;icona **[!UICONTROL Filtro]** (![Icona filtro.](/help/images/icons/filter.png)) per filtrare le entità visualizzate per categoria. È necessario selezionare almeno due categorie per visualizzare i dati.

![Finestra di dialogo per violazione dei criteri con filtro derivazione dati e menu a discesa evidenziati.](../images/enforcement/lineage-filter.png)

Seleziona **[!UICONTROL Vista a elenco]** per visualizzare la derivazione dati come elenco. Per tornare al grafico visivo, selezionare **[!UICONTROL Visualizzazione percorso]**.

![Finestra di dialogo per violazione dei criteri con la visualizzazione del percorso di derivazione dati evidenziata.](../images/enforcement/list-view.png)

#### Etichette applicate correttamente {#labels-successfully-applied}

Se crei criteri di utilizzo dei dati prima di etichettare i campi dello schema, potresti incontrare una finestra di dialogo di violazione dei criteri di governance non appena applichi le etichette allo schema. In questo caso, puoi etichettare correttamente parte dello schema. La scheda [!UICONTROL Etichette applicate correttamente] indica le etichette applicate correttamente, in quanto non sono presenti restrizioni dei criteri per il campo.

Utilizza il diagramma di derivazione dati per capire quali altre modifiche di configurazione devono essere apportate prima di poter aggiungere l’etichetta al campo schema.

![È stata evidenziata una finestra di dialogo per violazione dei criteri con [!UICONTROL Etichette applicate correttamente].](../images/enforcement/labels-successfully-applied.png)

### Valutazione dei criteri di consenso {#consent-policy-evaluation}

Quando attivi un pubblico in una destinazione, puoi vedere in che modo i [criteri di consenso](../policies/user-guide.md) influiscono sulla portata del pubblico durante la [fase di revisione del flusso di lavoro [!UICONTROL Attiva destinazioni]](#pre-activation-evaluation).

>[!NOTE]
>
>I criteri di consenso sono disponibili solo per le organizzazioni che hanno acquistato Adobe Healthcare Shield o Adobe Privacy &amp; Security Shield.

#### Miglioramento dei criteri di consenso per gli elementi multimediali a pagamento {#consent-policy-enhancement}

È stato apportato un miglioramento all&#39;applicazione dei criteri di consenso sulle destinazioni [batch](../../destinations/destination-types.md#file-based) e [streaming](../../destinations/destination-types.md#streaming-destinations), incluse le attivazioni di file multimediali a pagamento. Questo miglioramento è disponibile per i clienti di Privacy and Security Shield o Healthcare Shield e rimuove in modo proattivo i profili da destinazioni batch e streaming quando lo stato del consenso cambia. Inoltre, assicura che le modifiche del consenso vengano propagate immediatamente in modo che il pubblico giusto sia sempre mirato.

Questi miglioramenti consentono una maggiore fiducia nella strategia di marketing, in quanto eliminano la necessità per gli addetti al marketing di aggiungere manualmente attributi di consenso alla propria espressione di segmento. In questo modo, nessun profilo viene inavvertitamente sottoposto a targeting per alcuna esperienza di marketing dopo il ritiro del consenso o la cessazione degli stessi per un criterio di consenso. I criteri di consenso marketing che impostano regole per la gestione dei dati di consenso o preferenze nei vari flussi di lavoro di marketing vengono ora applicati automaticamente nei flussi di lavoro di attivazione nelle soluzioni a valle.

>[!NOTE]
>
>Questo miglioramento non comporta modifiche all’interfaccia utente.

#### Valutazione pre-attivazione {#pre-activation-evaluation}

Una volta raggiunto il passaggio **[!UICONTROL Rivedi]** quando [attivi una destinazione](../../destinations/ui/activation-overview.md), seleziona **[!UICONTROL Visualizza criteri applicati]**.

![Pulsante Visualizza criteri applicati nel flusso di lavoro di attivazione destinazione](../images/enforcement/view-applied-policies.png)

Viene visualizzata una finestra di dialogo di verifica dei criteri, con un’anteprima di come i criteri di consenso influiscono sul pubblico autorizzato dei tipi di pubblico da attivare.

![Finestra di dialogo per la verifica dei criteri di consenso nell&#39;interfaccia utente di Experience Platform](../images/enforcement/consent-policy-check.png)

La finestra di dialogo mostra il pubblico autorizzato per un pubblico alla volta. Per visualizzare la valutazione dei criteri per un pubblico diverso, utilizza il menu a discesa sopra il diagramma per selezionarne uno dall’elenco.

![Il commutatore del pubblico nella finestra di dialogo di verifica dei criteri.](../images/enforcement/audience-switcher.png)

Utilizza la barra a sinistra per passare dai criteri di consenso applicabili per il pubblico selezionato. I criteri non selezionati sono rappresentati nella sezione &quot;[!UICONTROL Altri criteri]&quot; del diagramma.

![Commutatore criteri nella finestra di dialogo di verifica dei criteri](../images/enforcement/policy-switcher.png)

Il diagramma mostra la sovrapposizione tra tre gruppi di profili:

1. Profili idonei per il pubblico selezionato
1. Profili idonei per il criterio di consenso selezionato
1. Profili idonei per gli altri criteri di consenso applicabili per il pubblico (denominati &quot;[!UICONTROL Altri criteri]&quot; nel diagramma)

I profili idonei per tutti e tre i gruppi di cui sopra rappresentano il pubblico consentito, riassunto nella barra a destra.

![Sezione Riepilogo nella finestra di dialogo di verifica dei criteri](../images/enforcement/summary.png)

Passa il puntatore del mouse su uno dei tipi di pubblico nel diagramma per visualizzare il numero di profili in esso contenuti.

![Evidenziazione di una sezione del diagramma nella finestra di dialogo di verifica dei criteri](../images/enforcement/highlight-segment.png)

Il pubblico autorizzato è rappresentato dalla sovrapposizione centrale del diagramma e può essere evidenziato come le altre sezioni.

![Evidenziazione del pubblico autorizzato nel diagramma](../images/enforcement/consented-audience.png)

#### Applicazione esecuzione flusso

Quando i dati vengono attivati su una destinazione, i dettagli di esecuzione del flusso mostrano il numero di identità escluse a causa di criteri di consenso attivi.

![Metriche delle identità escluse per un&#39;esecuzione del flusso di dati](../images/enforcement/dataflow-run-enforcement.png)

## Applicazione dei criteri per il pubblico attivato {#policy-enforcement-for-activated-audiences}

L’applicazione dei criteri viene comunque applicata ai tipi di pubblico dopo la loro attivazione, limitando eventuali modifiche a un pubblico o alla sua destinazione che potrebbero causare una violazione dei criteri. A causa del modo in cui [derivazione dati](#lineage) funziona nell&#39;applicazione dei criteri, una qualsiasi delle seguenti azioni può potenzialmente attivare una violazione:

* Aggiornamento delle etichette di utilizzo dei dati
* Modifica dei set di dati di un pubblico
* Modifica dei predicati del pubblico
* Modifica delle configurazioni di destinazione

Se una delle azioni di cui sopra attiva una violazione, tale azione non può essere salvata e viene visualizzato un messaggio di violazione dei criteri, per garantire che i tipi di pubblico attivati continuino a rispettare i criteri di utilizzo dei dati durante la modifica.

## Passaggi successivi

Questo documento illustra il funzionamento dell’applicazione automatica delle policy in Experience Platform. Per i passaggi su come integrare a livello di programmazione l&#39;applicazione dei criteri nelle applicazioni utilizzando chiamate API, consulta la guida sull&#39;[applicazione basata su API](./api-enforcement.md).
