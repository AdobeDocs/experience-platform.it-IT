---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API;profilo unificato;profilo unificato;unificato;profilo;rtcp;abilita profilo;abilita profilo;schema unione;PROFILO UNIONE;profilo unione
title: Guida all’interfaccia utente del profilo cliente in tempo reale
topic-legacy: guide
description: Profilo cliente in tempo reale crea una visualizzazione olistica di ciascuno dei tuoi singoli clienti, combinando dati provenienti da più canali tra cui online, offline, CRM e dati di terze parti. Questo documento funge da guida per l’interazione con Profilo cliente in tempo reale nell’interfaccia utente di Adobe Experience Platform.
exl-id: 792a3a73-58a4-4163-9212-4d43d24c2770
source-git-commit: 2696dab922d9c1992b61ffefe50a4e3155793282
workflow-type: tm+mt
source-wordcount: '1327'
ht-degree: 1%

---

# [!DNL Real-time Customer Profile] Guida all’interfaccia utente

[!DNL Real-time Customer Profile] crea una visualizzazione olistica di ciascuno dei tuoi singoli clienti, combinando dati provenienti da più canali tra cui dati online, offline, CRM e di terze parti. Questo documento funge da guida per l’interazione con i dati [!DNL Real-time Customer Profile] nell’interfaccia utente di Adobe Experience Platform.

## Introduzione

Questa guida all&#39;interfaccia utente richiede una comprensione dei vari servizi [!DNL Experience Platform] coinvolti nella gestione di [!DNL Real-time Customer Profiles]. Prima di leggere questa guida o di lavorare nell’interfaccia utente, controlla la documentazione relativa ai seguenti servizi:

* [[!DNL Real-time Customer Profile]](../home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [[!DNL Identity Service]](../../identity-service/home.md): Consente  [!DNL Real-time Customer Profile] di colmare le identità provenienti da origini dati diverse durante l’acquisizione in  [!DNL Platform].
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Il framework standardizzato in base al quale  [!DNL Platform] vengono organizzati i dati sulla customer experience.

## Panoramica

Nell’interfaccia utente di Experience Platform, seleziona **[!UICONTROL Profili]** nel menu di navigazione a sinistra per aprire la scheda **[!UICONTROL Panoramica]** . Questa scheda fornisce collegamenti alla documentazione e ai video per comprendere e iniziare a utilizzare i profili.

![](../images/user-guide/profiles-overview.png)

### Dashboard del profilo (alfa)

>[!IMPORTANT]
>
>La funzionalità del dashboard è attualmente in alfa e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.

Per alcuni utenti, la selezione di **[!UICONTROL Profiles]** nel menu di navigazione a sinistra e l&#39;apertura della scheda **[!UICONTROL Panoramica]** fornisce una dashboard che descrive le metriche chiave correlate ai dati del profilo.

Per ulteriori informazioni, visita la [Guida al dashboard del profilo](profile-dashboard.md).

## Sfoglia

Seleziona la scheda **[!UICONTROL Sfoglia]** per sfogliare i profili in base all’identità.

![](../images/user-guide/profiles-browse.png)

### Metriche del profilo {#profile-metrics}

Sul lato destro della scheda **[!UICONTROL Sfoglia]** sono presenti diverse metriche importanti correlate ai dati del profilo, tra cui il totale [conteggio profili](#profile-count) e un elenco di profili [per namespace](#profiles-by-namespace).

Queste metriche di profilo vengono valutate utilizzando il criterio di unione predefinito dell&#39;organizzazione. Per ulteriori informazioni sull&#39;utilizzo dei criteri di unione, tra cui la definizione di un criterio di unione predefinito, vedere la [panoramica dei criteri di unione](../merge-policies/overview.md).

Oltre a queste metriche, la sezione relativa alle metriche del profilo fornisce anche una data e un’ora dell’ultimo aggiornamento, indicando quando sono state valutate le metriche.

![](../images/user-guide/profiles-profile-metrics.png)

### Numero di profili {#profile-count}

Il conteggio dei profili visualizza il numero totale di profili di cui dispone la tua organizzazione all’interno di [!DNL Experience Platform], dopo che il criterio di unione predefinito della tua organizzazione ha unito i frammenti di profilo per formare un singolo profilo per ogni singolo cliente. In altre parole, l’organizzazione può disporre di più frammenti di profilo relativi a un singolo cliente che interagisce con il tuo marchio su diversi canali, ma questi frammenti verranno uniti (in base al criterio di unione predefinito) e restituiranno un conteggio di &quot;1&quot; profilo perché sono tutti correlati allo stesso individuo.

Il conteggio dei profili include anche profili con attributi (dati record) e profili contenenti solo dati di serie temporali (eventi), ad esempio profili Adobe Analytics. Il conteggio dei profili viene aggiornato regolarmente per fornire un numero totale aggiornato di profili all’interno di Platform.

Quando l&#39;acquisizione di record nell&#39;archivio [!DNL Profile] aumenta o diminuisce il conteggio di oltre il 5%, viene attivato un processo per aggiornare il conteggio. Per i flussi di lavoro con dati in streaming, viene eseguito un controllo su base oraria per determinare se la soglia di aumento o diminuzione del 5% è stata soddisfatta. In caso affermativo, viene attivato automaticamente un processo per aggiornare il conteggio del profilo. Per l’acquisizione batch, entro 15 minuti dal corretto inserimento di un batch nell’archivio profili, se viene soddisfatta la soglia di aumento o riduzione del 5%, viene eseguito un processo per aggiornare il conteggio dei profili.

### Profili per namespace {#profiles-by-namespace}

La metrica **[!UICONTROL Profili per namespace]** visualizza il conteggio totale e la suddivisione dei namespace in tutti i profili uniti nel tuo archivio profili. Il numero totale di profili per namespace (in altre parole, l’aggiunta insieme dei valori mostrati per ogni namespace) sarà sempre superiore alla metrica di conteggio dei profili, perché a un profilo potrebbero essere associati più namespace. Ad esempio, se un cliente interagisce con il tuo marchio su più di un canale, a quel singolo cliente saranno associati più namespace.

Simile alla metrica [conteggio profilo](#profile-count), quando l’acquisizione di record nello store [!DNL Profile] aumenta o diminuisce il conteggio di oltre il 5%, viene attivato un processo per aggiornare le metriche dello spazio dei nomi. Per i flussi di lavoro con dati in streaming, viene eseguito un controllo su base oraria per determinare se la soglia di aumento o diminuzione del 5% è stata soddisfatta. In caso affermativo, viene attivato automaticamente un processo per aggiornare il conteggio del profilo. Per l’acquisizione in batch, entro 15 minuti dal corretto inserimento di un batch nell’ archivio [!DNL Profile], se viene soddisfatta la soglia di aumento o diminuzione del 5%, viene eseguito un processo per aggiornare le metriche.

### Criteri di unione

Il selettore **[!UICONTROL Criteri di unione]** seleziona automaticamente il criterio di unione predefinito per la tua organizzazione. Se non si desidera utilizzare il criterio di unione, è possibile selezionare il `X` accanto al criterio di unione predefinito per aprire la finestra di dialogo **[!UICONTROL Seleziona criterio di unione]** in cui è possibile scegliere un altro criterio di unione.

Per ulteriori informazioni sull&#39;unione dei criteri e sul loro ruolo all&#39;interno di Platform, consulta la [panoramica dei criteri di unione](../merge-policies/overview.md).

![](../images/user-guide/profiles-search-merge-policy.png)

### Spazio dei nomi identità

Il selettore **[!UICONTROL Identity namespace]** apre una finestra di dialogo in cui è possibile scegliere lo spazio dei nomi di identità in base al quale eseguire la ricerca. Puoi personalizzare gli attributi visualizzati nella ricerca selezionando l’icona del filtro e scegliendo gli attributi da aggiungere o rimuovere.

![](../images/user-guide/profiles-search-filter.png)

Dalla finestra di dialogo **[!UICONTROL Seleziona namespace identità]**, scegli lo spazio dei nomi in base al quale desideri eseguire la ricerca oppure utilizza la barra di ricerca nella finestra di dialogo per iniziare a digitare il nome di uno spazio dei nomi. È possibile selezionare uno spazio dei nomi per visualizzare ulteriori dettagli. Una volta trovato lo spazio dei nomi desiderato, è possibile selezionare il pulsante di scelta e premere **[!UICONTROL Seleziona]** per continuare.

![](../images/user-guide/profiles-select-identity-namespace.png)

### Valore identità

Dopo aver selezionato uno spazio dei nomi di identità, torna alla scheda **[!UICONTROL Sfoglia]** in cui puoi immettere un **[!UICONTROL valore di identità]**. Questo valore è specifico per un profilo cliente individuale e deve essere una voce valida per lo spazio dei nomi fornito. Ad esempio, la selezione dello spazio dei nomi di identità &quot;E-mail&quot; richiede un valore di identità sotto forma di un indirizzo e-mail valido.

![](../images/user-guide/profiles-show-profile.png)

Una volta immesso un valore, seleziona **[!UICONTROL Mostra profilo]** e viene restituito un singolo profilo corrispondente al valore. Seleziona l&#39; **[!UICONTROL ID profilo]** per visualizzare i dettagli del profilo.

![](../images/user-guide/profiles-display-profile.png)

### Dettagli profilo {#profile-detail}

Selezionando l&#39; **[!UICONTROL ID profilo]**, si apre la scheda **[!UICONTROL Dettagli]** . Le informazioni di profilo visualizzate nella scheda **[!UICONTROL Dettaglio]** sono state unite da più frammenti di profilo per formare una singola visualizzazione del singolo cliente. Ciò include dettagli del cliente quali attributi di base, identità collegate e preferenze del canale. I campi predefiniti visualizzati possono essere modificati anche a livello organizzativo per visualizzare gli attributi di profilo preferiti. Per ulteriori informazioni sulla personalizzazione di questi campi, incluse le istruzioni dettagliate per l’aggiunta e la rimozione degli attributi e il ridimensionamento dei pannelli della dashboard, consulta la [guida alla personalizzazione dei dettagli del profilo](profile-customization.md).

![](../images/user-guide/profiles-profile-detail.png)

Puoi visualizzare ulteriori informazioni relative al singolo profilo selezionando un’altra delle schede disponibili. Queste schede includono attributi, eventi e appartenenza al segmento, che mostrano i segmenti per i quali il profilo è attualmente qualificato.

![](../images/user-guide/profiles-attributes-events-segments.png)

## Unisci criteri

Dal menu principale **[!UICONTROL Profili]**, selezionare la scheda **[!UICONTROL Criteri di unione]** per visualizzare un elenco dei criteri di unione appartenenti all&#39;organizzazione. Ogni criterio elencato visualizza il nome, indipendentemente dal fatto che si tratti del criterio di unione predefinito, e la classe dello schema a cui si applica.

Per ulteriori informazioni sui criteri di unione, vedere la [panoramica dei criteri di unione](../merge-policies/overview.md).

![](../images/user-guide/profiles-merge-policies.png)

## Schema dell&#39;Unione {#union-schema}

Dal menu principale **[!UICONTROL Profili]**, seleziona la scheda **[!UICONTROL Schema unione]** per visualizzare gli schemi di unione disponibili per i dati acquisiti. Uno schema di unione è un’unione di tutti i campi [!DNL Experience Data Model] (XDM) della stessa classe, i cui schemi sono stati abilitati per l’utilizzo in [!DNL Real-time Customer Profile].

Per ulteriori informazioni sugli schemi di unione, visita la [guida all&#39;interfaccia utente dello schema di unione](union-schema.md).

![](../images/user-guide/profiles-union-schema.png)

## Passaggi successivi

Leggendo questa guida, ora sai come visualizzare e gestire i dati [!DNL Profile] utilizzando l’ interfaccia utente [!DNL Experience Platform] . Per informazioni su come lavorare con i dati del profilo utilizzando l’API Profilo cliente in tempo reale, consulta la [Guida per gli sviluppatori di profili](../api/overview.md).
