---
keywords: Experience Platform;interfaccia utente;personalizzazione;dashboard utilizzo licenze;dashboard;utilizzo licenze;diritto;consumo;;user interface;UI;customization;license usage dashboard;dashboard;license usage;entitlement;usage
title: Dashboard di utilizzo delle licenze
description: Adobe Experience Platform fornisce una dashboard attraverso la quale è possibile visualizzare informazioni importanti sull’utilizzo delle licenze della tua organizzazione.
type: Documentation
exl-id: 143d16bb-7dc3-47ab-9b93-9c16683b9f3f
source-git-commit: 62f5ecf82df46284365e64d633c8242ac45567bc
workflow-type: tm+mt
source-wordcount: '3275'
ht-degree: 40%

---

# Dashboard utilizzo licenze {#license-usage-dashboard}

>[!CONTEXTUALHELP]
>id="testy-mctestface"
>title="Finestra di dialogo di prova che non deve essere visibile"
>abstract="L’oggetto {name} viene visualizzato su {date}."

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_core"
>title="Tabella dei prodotti principali"
>abstract="I prodotti principali elencati nella tabella hanno metriche, tracciamento dell’utilizzo e viste drill-through a livello di sandbox proprie. Questi prodotti principali forniscono le metriche chiave per il tracciamento ed eventuali componenti aggiuntivi sono inclusi in queste metriche."

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_addons"
>title="Tabella dei componenti aggiuntivi"
>abstract="Nella tabella Componenti aggiuntivi sono elencati i prodotti le cui quantità di licenze sono combinate con le metriche supportate dai prodotti principali. Questi componenti aggiuntivi non dispongono di metriche separate, ma migliorano il tracciamento dell’utilizzo dei prodotti principali a cui sono associati."

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseUsage"
>title="Dashboard utilizzo licenze"
>abstract="La dashboard utilizzo licenze offre informazioni approfondite sui prodotti Adobe Experience Platform acquistati. La panoramica della dashboard mostra le metriche principali dei prodotti, incluso l’utilizzo da parte dell’utente per ciascuna metrica principale e l’importo della licenza contrattuale. Nell’area di lavoro dei dettagli viene visualizzato un raggruppamento delle metriche per ciascun prodotto all’interno di sandbox specifiche."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-lifecycle/ui/dataset-expiration.html?lang=it" text="Scadenze di set di dati automatizzate"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=it" text="Scadenza dei dati dei profili pseudonimi"

>[!CONTEXTUALHELP]
>id="platform_licenseusage"
>title="Dashboard utilizzo licenze"
>abstract="La dashboard utilizzo licenze offre informazioni approfondite sui prodotti Adobe Experience Platform acquistati. La panoramica della dashboard mostra le metriche principali dei prodotti, incluso l’utilizzo da parte dell’utente per ciascuna metrica principale e l’importo della licenza contrattuale. Nell’area di lavoro dei dettagli viene visualizzato un raggruppamento delle metriche per ciascun prodotto all’interno di sandbox specifiche."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-lifecycle/ui/dataset-expiration.html?lang=it" text="Scadenze di set di dati automatizzate"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=it" text="Scadenza dei dati dei profili pseudonimi"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_computehours"
>title="Ore di calcolo previste"
>abstract="Le ore di calcolo misurano il tempo impiegato dai motori del Query Service per leggere, elaborare e scrivere dati durante l’esecuzione di query batch.<br>L’utilizzo potrebbe raggiungere la quantità concessa in licenza. Per valutare o ridurre l’utilizzo, passa a Query > Registro per rivedere la cronologia delle query. Se non disponi dell’autorizzazione necessaria per accedere all’area di lavoro Query, contatta il tuo amministratore."
>additional-url="https://experience.adobe.com/#/platform/query/log.html?lang=it" text="Area di lavoro registro query"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_addressableaudience"
>title="Pubblico indirizzabile previsto"
>abstract="Il pubblico indirizzabile è l’insieme dei profili di persona nel profilo cliente in tempo reale che la tua organizzazione è autorizzata a coinvolgere. Questa metrica include sia profili direttamente identificabili che pseudonimi.<br>L’utilizzo potrebbe raggiungere la quantità concessa in licenza. Per ridurre l’utilizzo, configura le scadenze del set di dati o del profilo pseudonimo."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html?lang=it" text="Scadenze degli eventi esperienza"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=it" text="Scadenza dei dati dei profili pseudonimi"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_engageableprofiles"
>title="Profili che potrebbero essere coinvolti previsti"
>abstract="I profili che potrebbero essere coinvolti sono profili di persona nel profilo cliente in tempo reale che la tua organizzazione ha tentato di coinvolgere utilizzando Journey Optimizer negli ultimi 12 mesi.<br>L’utilizzo potrebbe raggiungere la quantità concessa in licenza. Per ridurre l’utilizzo, configura le scadenze del set di dati o del profilo pseudonimo."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html?lang=it" text="Scadenze degli eventi esperienza"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=it" text="Scadenza dei dati dei profili pseudonimi"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_businesspersonprofile"
>title="Profilo persona aziendale previsto"
>abstract="I Profili persona aziendale sono record del profilo cliente in tempo reale che rappresentano singoli utenti in un contesto B2B.<br>L’utilizzo potrebbe raggiungere la quantità prevista dalla licenza. Per ridurre l’utilizzo, configura le scadenze del set di dati o del profilo pseudonimo."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html?lang=it" text="Scadenze degli eventi esperienza"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=it" text="Scadenza dei dati dei profili pseudonimi"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_corehours"
>title="Ore core previste"
>abstract="Le ore core rappresentano il tempo di elaborazione utilizzato da tutti i servizi Experience Platform.<br>L’utilizzo potrebbe raggiungere la quantità prevista dalla licenza. Per ridurre l’utilizzo, configura le scadenze del set di dati o del profilo pseudonimo."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html?lang=it" text="Scadenze degli eventi esperienza"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=it" text="Scadenza dei dati dei profili pseudonimi"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_totaldatavolume"
>title="Volume totale dati previsto"
>abstract="Il Volume totale dati è la quantità di dati disponibili nel profilo cliente in tempo reale da utilizzare nei flussi di lavoro di coinvolgimento e personalizzazione.<br>L’utilizzo potrebbe raggiungere la quantità prevista dalla licenza. Per ridurre l’utilizzo, configura le scadenze del set di dati o del profilo pseudonimo."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html?lang=it" text="Scadenze degli eventi esperienza"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=it" text="Scadenza dei dati dei profili pseudonimi"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_predictedusage_cjaRowsAvailable"
>title="Righe CJA disponibili previste"
>abstract="Le Righe CJA disponibili si riferiscono alla media giornaliera di righe di dati disponibili per l’analisi in Customer Journey Analytics.<br>L’utilizzo potrebbe raggiungere la quantità prevista dalla licenza. Per ridurre l’utilizzo, configura le scadenze del set di dati o del profilo pseudonimo."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html?lang=it" text="Scadenze degli eventi esperienza"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=it" text="Scadenza dei dati dei profili pseudonimi"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_exceededusage_addressableaudience"
>title="Pubblico indirizzabile previsto"
>abstract="Il pubblico indirizzabile è l’insieme dei profili di persona nel profilo cliente in tempo reale che la tua organizzazione è autorizzata a coinvolgere. Questo include sia profili direttamente identificabili che pseudonimi.<br>L’utilizzo ha superato la quantità prevista dalla licenza. Per ridurre l’utilizzo, configura le scadenze del set di dati o del profilo pseudonimo."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html?lang=it" text="Scadenze degli eventi esperienza"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=it" text="Scadenza dei dati dei profili pseudonimi"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_exceededusage_engageableprofiles"
>title="Profili che potrebbero essere coinvolti previsti"
>abstract="I profili che potrebbero essere coinvolti sono profili di persona nel profilo cliente in tempo reale che la tua organizzazione ha tentato di coinvolgere utilizzando Journey Optimizer negli ultimi 12 mesi.<br>L’utilizzo ha superato la quantità prevista dalla licenza. Per ridurre l’utilizzo, configura le scadenze del set di dati o del profilo pseudonimo."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html?lang=it" text="Scadenze degli eventi esperienza"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=it" text="Scadenza dei dati dei profili pseudonimi"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_exceededusage_businesspersonprofile"
>title="Profilo persona aziendale previsto"
>abstract="I Profili persona aziendale sono record del profilo cliente in tempo reale che rappresentano singoli utenti in un contesto B2B.<br>L’utilizzo ha superato la quantità prevista dalla licenza. Per ridurre l’utilizzo, configura le scadenze del set di dati o del profilo pseudonimo."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html?lang=it" text="Scadenze degli eventi esperienza"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=it" text="Scadenza dei dati dei profili pseudonimi"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_exceededusage_corehours"
>title="Ore core previste"
>abstract="Le ore core rappresentano il tempo di elaborazione utilizzato da tutti i servizi Experience Platform.<br>L’utilizzo potrebbe raggiungere la quantità concessa in licenza. Per ridurre l’utilizzo, configura le scadenze del set di dati o del profilo pseudonimo."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html?lang=it" text="Scadenze degli eventi esperienza"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=it" text="Scadenza dei dati dei profili pseudonimi"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_exceededusage_totaldatavolume"
>title="Volume totale dati previsto"
>abstract="Il Volume totale dati è la quantità di dati disponibili nel profilo cliente in tempo reale da utilizzare nei flussi di lavoro di coinvolgimento e personalizzazione.<br>L’utilizzo potrebbe raggiungere la quantità concessa in licenza. Per ridurre l’utilizzo, configura le scadenze del set di dati o del profilo pseudonimo."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html?lang=it" text="Scadenze degli eventi esperienza"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=it" text="Scadenza dei dati dei profili pseudonimi"

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_exceededusage_cjaRowsAvailable"
>title="Righe CJA disponibili previste"
>abstract="Le Righe CJA disponibili si riferiscono alla media giornaliera di righe di dati disponibili per l’analisi in Customer Journey Analytics.<br>L’utilizzo potrebbe raggiungere la quantità concessa in licenza. Per ridurre l’utilizzo, configura le scadenze del set di dati o del profilo pseudonimo."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/event-expirations.html?lang=it" text="Scadenze degli eventi esperienza"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=it" text="Scadenza dei dati dei profili pseudonimi"

È possibile visualizzare informazioni importanti sull&#39;utilizzo delle licenze dell&#39;organizzazione tramite il dashboard di Adobe Experience Platform [!UICONTROL License usage]. Le informazioni visualizzate qui vengono acquisite durante un’istantanea giornaliera dell’istanza Experience Platform.

I rapporti sull’utilizzo delle licenze forniscono un elevato grado di granularità. La maggior parte delle metriche è condivisa tra più prodotti e riflette l’utilizzo aggregato tra tutti i prodotti che li utilizzano, non i totali per prodotto. Il dashboard fornisce l’utilizzo consolidato di queste metriche in tutte le sandbox di produzione o di sviluppo e la metrica di utilizzo da una sandbox specifica. Con le metriche di utilizzo è possibile tenere traccia delle seguenti applicazioni Experience Platform: Real-Time Customer Data Platform, Adobe Journey Optimizer e Customer Journey Analytics.

Questa guida illustra come accedere e utilizzare il dashboard utilizzo licenze nell’interfaccia utente di e fornisce ulteriori informazioni sulle visualizzazioni visualizzate nel dashboard.

Per una panoramica generale dell&#39;interfaccia utente di Experience Platform, consulta la [guida dell&#39;interfaccia utente di Experience Platform](../../landing/ui-guide.md).

## [!UICONTROL License usage] dati dashboard

Nel dashboard di [!UICONTROL License usage] viene visualizzato un elenco di tutti i prodotti Experience Platform acquistati ed eventuali componenti aggiuntivi per tali prodotti. Da questa dashboard è possibile trovare un’istantanea dei dati relativi alla licenza dell’organizzazione per Experience Platform in qualsiasi sandbox associata.

I dati in questo dashboard vengono visualizzati esattamente come apparivano nel momento specifico in cui è stata acquisita l’istantanea. Non si tratta di un’approssimazione o di un esempio, ma il dashboard non viene aggiornato in tempo reale.

>[!NOTE]
>
>La maggior parte delle metriche nel dashboard viene aggiornata ogni giorno, in base a un’istantanea dell’istanza di Experience Platform. [!UICONTROL CJA Rows Available] è un&#39;eccezione e viene aggiornato mensilmente. Le metriche etichettate con &quot;pacchetti&quot;, come [!UICONTROL Adhoc Query Service Users Packs], [!UICONTROL Profile Richness No of Packs] e [!UICONTROL Streaming Segmentation No of Packs], riflettono i diritti di licenza per le offerte di componenti aggiuntivi e non tengono traccia dell&#39;utilizzo corrente. Le modifiche apportate dopo lo snapshot non sono visibili fino allo snapshot successivo.

## Esplorazione del dashboard utilizzo licenze {#explore}

Per passare al dashboard utilizzo licenze nell&#39;interfaccia utente di Experience Platform, seleziona **[!UICONTROL License usage]** nella barra a sinistra. Il dashboard contiene due schede: **[!UICONTROL Metrics]** e **[!UICONTROL Products]**.

>[!NOTE]
>
>Per impostazione predefinita, il dashboard utilizzo licenze non è attivato. Gli utenti devono disporre dell’autorizzazione &quot;View License Usage Dashboard&quot; (Visualizza dashboard utilizzo licenze) per visualizzare la dashboard. Per i passaggi relativi alla concessione delle autorizzazioni di accesso, fare riferimento alla [guida alle autorizzazioni del dashboard](../permissions.md).

## Scheda [!UICONTROL Metrics] {#metrics-tab}

La scheda **[!UICONTROL Metrics]** fornisce una visualizzazione centralizzata di tutte le metriche di utilizzo delle licenze nell&#39;organizzazione. Poiché la maggior parte delle metriche è condivisa tra i prodotti, non esiste una suddivisione separata per prodotto per queste metriche.

La tabella delle metriche include le colonne seguenti:

| Nome colonna | Descrizione |
|---|---|
| **[!UICONTROL Metric Name]** | Nome della metrica di utilizzo della licenza. Ogni voce include un&#39;icona di informazioni (`ⓘ`) che visualizza una descrizione e un elenco dei prodotti associati. |
| **[!UICONTROL Licensed]** | Il numero di unità che la tua organizzazione ha il diritto di utilizzare, come definito nel tuo contratto. Questa metrica corrisponde al valore della **quantità licenza** nella scheda Prodotti. |
| **[!UICONTROL Measured]** | La quantità della metrica attualmente utilizzata dall’organizzazione. |
| **[!UICONTROL Usage %]** | Percentuale del valore concesso in licenza attualmente in uso. |
| **[!UICONTROL Predicted Usage %]** | L’intervallo previsto di utilizzo della metrica nelle prossime 6 settimane. |

Utilizza l&#39;interruttore sandbox **[!UICONTROL Production]** o **[!UICONTROL Development]** per filtrare le metriche visualizzate dalle sandbox.

>[!NOTE]
>
>Il reporting sui consumi è cumulativo per tipo di sandbox. Selezionando [!UICONTROL Production] o [!UICONTROL Development] si mostra l&#39;utilizzo combinato in tutte le sandbox di quel tipo.

![La scheda Metriche della dashboard Utilizzo licenze visualizza un elenco di metriche, quantità di licenze e dati di utilizzo.](../images/license-usage/metrics-tab.png)

>[!WARNING]
>
>L’autorizzazione per visualizzare il dashboard utilizzo licenze deve essere specificata a livello di sandbox. Aggiungi le autorizzazioni a ogni singola sandbox per visualizzarle all’interno del dashboard. Questa limitazione verrà risolta in una versione futura. Nel frattempo, è disponibile la seguente soluzione alternativa:
>
>1. Creare un profilo di prodotto in Adobe Admin Console.
>2. In Autorizzazione nella categoria Sandbox, aggiungi tutte le sandbox da visualizzare nel dashboard utilizzo licenze.
>3. Nella categoria Autorizzazione dashboard utente, aggiungi l’autorizzazione &quot;Visualizza dashboard utilizzo licenze&quot;.

### Visualizzare i dettagli delle metriche {#view-metric-details}

Per visualizzare i dettagli di utilizzo per una metrica specifica, seleziona un nome di metrica nell’elenco. Viene visualizzata una vista dettagliata della metrica, che include:

- Un grafico a linee cronologico che mostra l’utilizzo nel tempo
- Confronto tra valori con licenza e valori misurati
- Utilizzo per singola sandbox
- Un selettore sandbox per filtrare i dati
- Opzione di esportazione per il download CSV

Questa visualizzazione ti consente di tracciare le tendenze, comprendere in che modo ogni sandbox contribuisce all’utilizzo complessivo ed esportare i dati per l’analisi offline.

Ogni grafico include menu a discesa per filtrare i dati. Utilizza il menu a discesa dell’intervallo di date per regolare il periodo di lookback (impostazione predefinita: ultimi 30 giorni) oppure il menu a discesa sandbox per visualizzare l’utilizzo per una sandbox specifica di produzione o sviluppo.

![Visualizzazione dei dettagli della metrica del pubblico indirizzabile con grafico cronologico di utilizzo, tabella sandbox e pulsante di esportazione.](../images/license-usage/metric-details-view.png)

È inoltre possibile selezionare **[!UICONTROL Custom date]** per scegliere il periodo di tempo visualizzato.

![Scheda Panoramica della dashboard Utilizzo licenze con le opzioni dell&#39;intervallo date personalizzate evidenziate.](../images/license-usage/custom-date-range.png)

### Esportazione CSV {#export-metric-usage-data}

Puoi esportare i dati storici sull’utilizzo per la metrica e la sandbox selezionate come file CSV direttamente dalla vista dei dettagli della metrica. Selezionare l&#39;icona **[!UICONTROL Export]** per scaricare i dati del grafico in formato tabulare. Il file CSV esportato consente di analizzare le tendenze offline o condividere informazioni sull’utilizzo tra i team.

## Scheda [!UICONTROL Products] {#products-tab}

La scheda **[!UICONTROL Products]** presenta i dati di utilizzo della licenza raggruppati per prodotti acquistati ed eventuali componenti aggiuntivi associati. La scheda [!UICONTROL Products] contiene due tabelle:

- **[!UICONTROL Core products]tabella**: questa tabella elenca i principali prodotti Adobe Experience Platform concessi in licenza dalla tua organizzazione. Ogni prodotto elenca la propria metrica principale, il tracciamento dell’utilizzo e l’utilizzo previsto.
- **[!UICONTROL Add-ons]tabella**: elenca gli elementi supplementari i cui importi di licenza contribuiscono alle metriche del prodotto di base. I componenti aggiuntivi non dispongono di metriche separate, ma migliorano il tracciamento dell’utilizzo dei prodotti core a cui sono associati.

| Nome colonna | Descrizione |
|---|---|
| **[!UICONTROL Product]** | La soluzione Adobe concessa in licenza dalla tua organizzazione. |
| **[!UICONTROL Primary Metric]** | La metrica principale utilizzata per il tracciamento all’interno di quel prodotto. |
| **[!UICONTROL License Amount]** | Il valore previsto dal contratto per l’importo massimo della metrica principale. |
| **[!UICONTROL Usage]** | Quantità della metrica principale utilizzata. |
| **[!UICONTROL Usage %]** | La percentuale della metrica principale utilizzata in base alla quantità di licenza. |
| **[!UICONTROL Predicted Usage]** | Percentuale di utilizzo prevista della metrica principale. |

>[!NOTE]
>
>[!UICONTROL License Amount] per i componenti aggiuntivi è incluso nella quantità totale di licenza del prodotto di base. I componenti aggiuntivi non vengono tracciati separatamente, ma migliorano le funzionalità dei prodotti associati. Ad esempio, se acquisti una confezione di cinque sandbox come componente aggiuntivo, l’importo viene aggiunto a quello del prodotto di base. La tabella dei componenti aggiuntivi mostra un [!UICONTROL License Amount] specifico per il componente aggiuntivo, ma l&#39;utilizzo effettivo viene registrato attraverso il prodotto di base.

![Scheda Prodotti della dashboard Utilizzo licenze con tabelle per i prodotti core e i componenti aggiuntivi.](../images/license-usage/products-tab.png)

### Utilizzo previsto {#predicted-usage}

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseUsage_prediction"
>title="Utilizzo previsto"
>abstract="Le previsioni si basano sull’utilizzo negli ultimi 6-7 mesi e vengono generate ogni venerdì su base settimanale. Tieni presente che le previsioni sull’utilizzo delle licenze sono approssimazioni basate sull’utilizzo passato. Sei responsabile della comprensione dell’utilizzo effettivo dell’organizzazione e di garantire che l’utilizzo non vada oltre l’ambito della licenza dell’organizzazione con Adobe. Per ridurre l’utilizzo, puoi configurare le scadenze del set di dati o del profilo pseudonimo di sandbox e set di dati."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-lifecycle/ui/dataset-expiration.html?lang=it" text="Scadenze di set di dati automatizzate"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=it" text="Scadenza dei dati dei profili pseudonimi"

>[!CONTEXTUALHELP]
>id="platform_licenseusage_prediction"
>title="Utilizzo previsto"
>abstract="Le previsioni si basano sull’utilizzo negli ultimi 6-7 mesi e vengono generate il 15 di ogni mese. Tieni presente che le previsioni sull’utilizzo delle licenze sono approssimazioni basate sull’utilizzo passato. Sei responsabile della comprensione dell’utilizzo effettivo dell’organizzazione e di garantire che l’utilizzo non vada oltre l’ambito della licenza dell’organizzazione con Adobe. Per ridurre l’utilizzo, puoi configurare le scadenze del set di dati o del profilo pseudonimo di sandbox e set di dati."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/data-lifecycle/ui/dataset-expiration.html?lang=it" text="Scadenze di set di dati automatizzate"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/profile/pseudonymous-profiles.html?lang=it" text="Scadenza dei dati dei profili pseudonimi"

Gestire e ottimizzare in modo proattivo le risorse di gestione delle licenze con previsioni di utilizzo precise e aggiornate. La colonna [!UICONTROL Predicted Usage] prevede l&#39;utilizzo futuro delle licenze a livello di sandbox in tutte le sandbox di produzione e sviluppo per tutti i prodotti acquistati. Le previsioni ora vengono aggiornate settimanalmente, fornendo una previsione di sei settimane basata sui dati di utilizzo più recenti. Ogni previsione include sia un limite inferiore che un limite superiore per supportare una pianificazione informata.

>[!IMPORTANT]
>
>Le previsioni vengono aggiornate settimanalmente ogni venerdì. La data di aggiornamento è inclusa in un&#39;icona di informazioni (![Icona di informazioni.](../images/license-usage/info-icon.png)) sopra il titolo della colonna.

Visualizzare un riepilogo dell&#39;utilizzo dei diritti di un prodotto dalla scheda [!UICONTROL Product] nella tabella [!UICONTROL Core products].

![Scheda [!UICONTROL License usage] [!UICONTROL Product] con un prodotto ed evidenziata la colonna dei dati di utilizzo previsti.](../images/license-usage/product-predicted-usage.png)

>[!NOTE]
>
>Tieni presente che le previsioni sull’utilizzo delle licenze sono approssimazioni basate sull’utilizzo passato. È tua responsabilità comprendere l’utilizzo effettivo dell’organizzazione e assicurarsi che non vada oltre l’ambito della licenza dell’organizzazione con Adobe.

La percentuale di utilizzo previsto è determinata come segue:

- Se i limiti inferiore e superiore sono significativamente diversi, vengono visualizzati come intervallo (ad esempio, 32% - 35%).
- Se i limiti inferiore e superiore sono quasi identici e non zero, vengono visualizzati come valore approssimativo (ad esempio, ~34%).
- Se i limiti inferiore e superiore sono quasi identici e zero, vengono visualizzati esattamente come 0%.

>[!NOTE]
>
>&quot;Quasi identici&quot; in questo contesto significa che i valori sono statisticamente significativi per due posizioni decimali (ad esempio, un limite inferiore di 0,342 e un limite superiore di 0,344 sono entrambi arrotondati al 34%).

La funzione di utilizzo previsto supporta le metriche seguenti:

- [!UICONTROL Addressable audience]
- [!UICONTROL Businessperson profiles]
- [!UICONTROL Compute hours]
- [!UICONTROL Customer Journey Audience number of rows]
- [!UICONTROL Engageable profiles]
- [!UICONTROL Total Data Volume]

## Metriche disponibili {#available-metrics}

>[!IMPORTANT]
>
>A partire dal 20 agosto, i clienti con diritti per &#39;[!UICONTROL Average Profile Richness]&#39; e &#39;[!UICONTROL Total Storage]&#39; hanno invece visto &#39;[!UICONTROL Total Data Volume]&#39; nel dashboard utilizzo licenze. Non vi sono state modifiche alle adesioni dei clienti, ma solo una semplificazione delle metriche di tracciamento. [!UICONTROL Total Data Volume] rappresenta i dati disponibili in Real-Time Customer Profile per i flussi di lavoro di coinvolgimento e personalizzazione. Questa metrica semplificata ha migliorato la gestione e la misurazione dell’utilizzo di Real-Time Customer Profile. I clienti sono stati invitati a contattare il proprio rappresentante Adobe per ulteriori chiarimenti su questa modifica.

Il dashboard utilizzo licenze riporta diverse metriche univoche applicabili a più prodotti dell’organizzazione. Le metriche disponibili sono:

| Metrica | Descrizione |
|---|---|
| [!UICONTROL Audience Activation Size] | Dimensione totale dei profili attivati in qualsiasi destinazione basata su file in un anno. Nota: non sono inclusi i profili inviati tramite le destinazioni di streaming. |
| [!UICONTROL Addressable Audience] | Il set di profili persona in Real-Time Customer Profile che la tua organizzazione è autorizzata a coinvolgere, inclusi sia i profili direttamente identificabili che quelli pseudonimi. Questi profili possono contenere attributi, comportamenti e dati di appartenenza ai segmenti. I volumi di profilo vengono calcolati utilizzando il grafo di identità deterministico predefinito di Adobe Experience Platform e sono considerati una feature condivisa. |
| [!UICONTROL Adhoc Query Service Users Packs] | Un componente aggiuntivo per aumentare il diritto di utenti simultanei autorizzati del Query Service a cinque ulteriori utenti e a un ulteriore query ad hoc per pacchetto in esecuzione contemporanea. È possibile concedere in licenza più pacchetti utente per query ad hoc aggiuntive. |
| [!UICONTROL Average profile richness] | **Obsoleto** - Somma di tutti i dati di produzione archiviati nel servizio profili hub in qualsiasi momento, divisa per cinque volte il numero di profili di persona aziendale autorizzati. [!UICONTROL Average profile richness] è una funzionalità condivisa. |
| [!UICONTROL CJA Rows Available] | Le righe medie giornaliere di dati disponibili per l’analisi in Customer Journey Analytics. |
| [!UICONTROL Computed Attributes] | Dati comportamentali aggregati del profilo basati su eventi di esperienza che vengono convertiti in un attributo di profilo e possono essere inclusi in un profilo persona. |
| [!UICONTROL Consumer Audience] | Il numero di profili di persona identificati come &quot;Pubblico consumatore&quot; nell’ordine cliente. |
| [!UICONTROL Data Export Size] | La quantità di dati inviati tramite le attivazioni dei set di dati in un anno. |
| [!UICONTROL Data Exports] | Dimensione totale dei set di dati che possono essere esportati in qualsiasi soluzione non Adobe (direttamente o indirettamente) in un anno. |
| [!UICONTROL Data Lake Storage] | Quantità utilizzata dell’archivio dati analitici in Adobe Experience Platform. |
| [!UICONTROL Engageable Audience] | Un gruppo di profili persona in Real-Time Customer Profile che hai tentato di coinvolgere negli ultimi 12 mesi utilizzando le funzionalità di authoring, decisione, consegna, sperimentazione o orchestrazione di Journey Optimizer. |
| [!UICONTROL Look-alike Audiences] | Un pubblico consumer lookalike è un pubblico generato modellando un pubblico consumer esistente per identificare profili di persone con attributi o comportamenti simili. |
| [!UICONTROL Number of AMM Models] | Un conteggio del modello di apprendimento automatico (integrato in Adobe Mix Modeler) utilizzato per misurare e/o prevedere un risultato specifico in base agli investimenti effettuati. |
| [!UICONTROL Number of Sandboxes] | Numero di separazioni logiche all’interno dell’istanza di qualsiasi servizio on-demand di Adobe che accede a dati e operazioni isolate di Adobe Experience Platform. |
| [!UICONTROL Profile Richness No of Packs] | Un aumento del volume totale di dati autorizzato di 25 KB per profilo per ogni pacchetto di ricchezza di profilo aggiuntivo. |
| [!UICONTROL Query Service Compute Hours] | Misurazione del tempo impiegato dai motori di Query Service per leggere, elaborare e riscrivere i dati nel data lake quando viene eseguita una query in batch. |
| [!UICONTROL Streaming Segmentation No of Packs] | I pacchetti aggiornano l’appartenenza al segmento per un profilo persona quando nuovi dati entrano nel servizio di segmentazione tramite un flusso di streaming. L’appartenenza al segmento viene valutata in base agli attributi correnti del profilo della persona e al valore dell’evento corrente, senza tenere conto del comportamento storico. La segmentazione in streaming è una funzione condivisa. |
| [!UICONTROL Total Data Volume] | La quantità totale di dati disponibili per Real-Time Customer Profile da utilizzare nei flussi di lavoro di coinvolgimento. Il volume totale dei dati è calcolato con la seguente formula: **Volume totale dei dati = Pubblico indirizzabile × Rendicità media del profilo**. Questa metrica riflette i dati memorizzati solo nell’archivio profili ed esclude l’archiviazione del data lake. Fornisce una visualizzazione più mirata dei dati rilevanti per il coinvolgimento basato sul profilo. Per ulteriori informazioni, consulta le [domande frequenti sul volume totale dei dati](../../landing/license-usage-and-guardrails/total-data-volume.md). |
| [!UICONTROL Total Volume of Data Egress] | Il volume annuo cumulativo di dati esportati da Adobe Experience Platform in data warehouse di terze parti. |

<!-- |  [!UICONTROL Sandbox No of Packs] |  A logical separation within your instance of any Adobe On-demand Service that accesses Adobe Experience Platform isolating data and operations | -->

>[!TIP]
>
>È possibile controllare i diritti di licenza nell&#39;ordine di vendita per calcolare metriche quali l&#39;indennità di archiviazione.<br>Ad esempio,<ul><li>Indennità di archiviazione = numero di &quot;profili autorizzati&quot; nel contratto X Ricchezza media profilo</li></ul>

La disponibilità di queste metriche e la definizione specifica di ciascuna di esse varia a seconda delle licenze acquistate dalla tua organizzazione. Per le definizioni dettagliate di ciascuna metrica, consulta l’appropriata documentazione di descrizione del prodotto:

| Licenza | Descrizione del prodotto |
| --- | --- |
| <ul><li>ADOBE EXPERIENCE PLATFORM:OD LITE</li><li>ADOBE EXPERIENCE PLATFORM:OD STANDARD</li><li>ADOBE EXPERIENCE PLATFORM:OD PESANTE</li></ul> | [Adobe Experience Platform](https://helpx.adobe.com/it/legal/product-descriptions/adobe-experience-platform.html) |
| <ul><li>ADOBE EXPERIENCE PLATFORM:OD</li></ul> | [Experience Platform, Servizi app e Intelligent Services](https://helpx.adobe.com/it/legal/product-descriptions/exp-platform-app-svcs.html) |
| <ul><li>PIATTAFORMA DATI CLIENTE RT:OD</li><li>RT CUSTOMER DATA PLATFORM:OD PRFL A 10M</li><li>RT CUSTOMER DATA PLATFORM:OD PRFL A 50M</li></ul> | [Adobe Real-Time Customer Data Platform](https://helpx.adobe.com/it/legal/product-descriptions/real-time-customer-data-platform.html) |
| <ul><li>ATTIVAZIONE DI AEP:OD</li><li>AEP:OD ACTIVATION PRFL A 10M</li><li>AEP:OD ACTIVATION PRFL FINO A 50 M</li></ul> | [Attivazione Adobe Experience Platform](https://helpx.adobe.com/it/legal/product-descriptions/adobe-experience-platform0.html) |
| <ul><li>AEP:OD INTELLIGENCE</li></ul> | [Adobe Experience Platform Intelligence](https://helpx.adobe.com/it/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html) |
| <ul><li>JOURNEY OPTIMIZER SELECT:OD</li><li>JOURNEY OPTIMIZER PRIME:OD</li><li>JOURNEY OPTIMIZER ULTIMATE:OD</li><li>UNP AJO PRIME STARTER:OD</li><li>UNP AJO ULTIMATE STARTER:OD</li><li>ORCHESTRAZIONE PROFILO Real-Time CDP:OD UNP</li></ul> | [Adobe Journey Optimizer](https://helpx.adobe.com/it/legal/product-descriptions/adobe-journey-optimizer.html) |

>[!WARNING]
>
>Il dashboard utilizzo licenze riporta solo l’ultima licenza fornita per la tua organizzazione. Se l’ultima licenza fornita per la tua organizzazione non viene visualizzata nella tabella precedente, è possibile che il dashboard utilizzo licenze non venga visualizzato correttamente. Il supporto per licenze aggiuntive e più licenze in una singola organizzazione è pianificato per una versione futura.

## Passaggi successivi

Dopo aver letto questo documento, potrai individuare la dashboard di utilizzo della licenza e visualizzare le metriche di utilizzo per ciascun prodotto acquistato, per tutte le sandbox di produzione o di sviluppo e per una sandbox specifica. Puoi trovare ulteriori informazioni sulle metriche disponibili per la tua organizzazione, in base alle licenze acquistate dalla tua organizzazione.

Per ulteriori informazioni sulle altre funzionalità disponibili nell&#39;interfaccia utente di Experience Platform, consulta la [guida dell&#39;interfaccia utente di Experience Platform](../../landing/ui-guide.md).
