---
keywords: ', Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API;profilo unificato;profilo unificato;unificato;profilo;rtcp;abilita profilo;Abilita profilo;schema unione;PROFILO UNIONE;profilo unione'
title: Guida all'interfaccia utente del profilo cliente in tempo reale
topic: guide
description: Profilo cliente in tempo reale crea una visualizzazione olistica di ciascuno dei tuoi clienti, combinando dati da più canali tra cui dati online, offline, CRM e di terze parti. Questo documento funge da guida per l'interazione con il profilo cliente in tempo reale nell'interfaccia utente di Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: cad9c690be986961aea2969ef0ade975f33a8ee5
workflow-type: tm+mt
source-wordcount: '1315'
ht-degree: 1%

---


# [!DNL Real-time Customer Profile] Guida all&#39;interfaccia

[!DNL Real-time Customer Profile] crea una visualizzazione olistica di ciascuno dei tuoi clienti, combinando dati provenienti da più canali tra cui dati online, offline, CRM e di terze parti. Questo documento funge da guida per l&#39;interazione con i dati [!DNL Real-time Customer Profile] nell&#39;interfaccia utente di Adobe Experience Platform.

## Introduzione

Questa guida all&#39;interfaccia utente richiede una conoscenza approfondita dei vari servizi [!DNL Experience Platform] coinvolti nella gestione di [!DNL Real-time Customer Profiles]. Prima di leggere questa guida o di utilizzare l&#39;interfaccia utente, consulta la documentazione relativa ai seguenti servizi:

* [[!DNL Real-time Customer Profile]](../home.md): Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [[!DNL Identity Service]](../../identity-service/home.md): Consente  [!DNL Real-time Customer Profile] di colmare le identità provenienti da origini dati diverse durante l&#39;assimilazione  [!DNL Platform].
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Il framework standard con cui  [!DNL Platform] organizzare i dati relativi all&#39;esperienza dei clienti.

## Panoramica

Nell&#39;interfaccia utente del Experience Platform , selezionare **[!UICONTROL Profiles]** nel menu di navigazione a sinistra per aprire la scheda **[!UICONTROL Overview]**. Questa scheda fornisce collegamenti alla documentazione e ai video per agevolare la comprensione e l&#39;utilizzo dei profili.

![](../images/user-guide/profiles-overview.png)

### (Alfa) Pannello profilo

>[!IMPORTANT]
>
>La funzionalità del dashboard è attualmente in alfa e non è disponibile per tutti gli utenti. La documentazione e le funzionalità sono soggette a modifiche.

Per alcuni utenti, la selezione di **[!UICONTROL Profiles]** nella navigazione a sinistra e l&#39;apertura della scheda **[!UICONTROL Overview]** fornisce una dashboard che mostra le metriche chiave correlate ai dati del profilo.

Per saperne di più, visita la [Guida del dashboard del profilo](profile-dashboard.md).

## Sfoglia

Selezionate la scheda **[!UICONTROL Browse]** per individuare i profili in base all&#39;identità.

![](../images/user-guide/profiles-browse.png)

### Metriche profilo {#profile-metrics}

Sul lato destro della scheda **[!UICONTROL Browse]** sono presenti diverse metriche importanti correlate ai dati del profilo, tra cui il numero totale di [profili](#profile-count) e un elenco di [profili per namespace](#profiles-by-namespace).

Queste metriche del profilo vengono valutate utilizzando il criterio di unione predefinito dell&#39;organizzazione. Per ulteriori informazioni sull&#39;utilizzo dei criteri di unione, inclusa la definizione di un criterio di unione predefinito, vedere la [Guida utente dei criteri di unione](merge-policies.md).

Oltre a queste metriche, la sezione relativa alle metriche del profilo fornisce anche una data e un&#39;ora dell&#39;ultimo aggiornamento, che mostrano quando le metriche sono state valutate per l&#39;ultima volta.

![](../images/user-guide/profiles-profile-metrics.png)

### Conteggio profili {#profile-count}

Il conteggio dei profili visualizza il numero totale di profili di cui dispone l&#39;organizzazione all&#39;interno di [!DNL Experience Platform], dopo che il criterio di unione predefinito dell&#39;organizzazione ha unito i frammenti di profilo per formare un unico profilo per ciascun cliente. In altre parole, l&#39;organizzazione potrebbe avere più frammenti di profilo correlati a un singolo cliente che interagisce con il proprio marchio tra canali diversi, ma tali frammenti sarebbero uniti (in base al criterio di unione predefinito) e restituirebbero un conteggio di profilo pari a &quot;1&quot; perché tutti correlati allo stesso individuo.

Il conteggio dei profili include anche profili con attributi (dati di record) e profili contenenti solo dati di serie temporali (eventi), come  profili Adobe Analytics. Il conteggio dei profili viene aggiornato regolarmente per fornire un numero totale aggiornato di profili all&#39;interno della piattaforma.

Quando l&#39;inserimento di record nello store [!DNL Profile] aumenta o diminuisce il conteggio di oltre il 5%, viene attivato un processo per aggiornare il conteggio. Per i flussi di lavoro dei dati in streaming, viene effettuato un controllo ogni ora per determinare se è stata raggiunta la soglia di incremento o riduzione del 5%. In caso affermativo, viene attivato automaticamente un processo per aggiornare il conteggio dei profili. Per l’assimilazione batch, entro 15 minuti dal corretto inserimento di un batch nell’archivio profili, se viene raggiunta la soglia di incremento o riduzione del 5%, viene eseguito un processo per aggiornare il conteggio dei profili.

### Profili per spazio dei nomi {#profiles-by-namespace}

La metrica **[!UICONTROL Profiles by namespace]** visualizza il conteggio totale e la suddivisione degli spazi di nomi in tutti i profili uniti nel tuo archivio profili. Il numero totale di profili per namespace (in altre parole, aggiungendo insieme i valori mostrati per ogni namespace) sarà sempre superiore alla metrica del conteggio dei profili, perché a un profilo potrebbero essere associati più spazi dei nomi. Ad esempio, se un cliente interagisce con il tuo marchio su più di un canale, a quel singolo cliente saranno associati più spazi dei nomi.

Simile alla metrica [conteggio profilo](#profile-count), quando l&#39;inserimento di record nello store [!DNL Profile] aumenta o diminuisce il conteggio di oltre il 5%, viene attivato un processo per aggiornare le metriche dello spazio nomi. Per i flussi di lavoro dei dati in streaming, viene effettuato un controllo ogni ora per determinare se è stata raggiunta la soglia di incremento o riduzione del 5%. In caso affermativo, viene attivato automaticamente un processo per aggiornare il conteggio dei profili. Per l&#39;assimilazione batch, entro 15 minuti dal corretto inserimento di un batch nello store [!DNL Profile], se viene raggiunta la soglia di incremento o riduzione del 5%, viene eseguito un processo per aggiornare le metriche.

### Unisci criterio

Il selettore **[!UICONTROL Merge policy]** seleziona automaticamente il criterio di unione predefinito per l&#39;organizzazione. Se non si desidera utilizzare tale criterio di unione, è possibile selezionare il criterio di unione `X` accanto al criterio di unione predefinito per aprire la finestra di dialogo **[!UICONTROL Select merge policy]** in cui è possibile scegliere un altro criterio di unione.

Per ulteriori informazioni sull&#39;unione dei criteri e il relativo ruolo all&#39;interno della piattaforma, vedere la [guida dell&#39;interfaccia utente dei criteri di unione](merge-policies.md).

![](../images/user-guide/profiles-search-merge-policy.png)

### Spazio dei nomi identità

Il selettore **[!UICONTROL Identity namespace]** apre una finestra di dialogo in cui è possibile scegliere lo spazio dei nomi di identità per il quale eseguire la ricerca. È inoltre possibile personalizzare gli attributi visualizzati nella ricerca selezionando l&#39;icona del filtro e scegliendo gli attributi da aggiungere o rimuovere.

![](../images/user-guide/profiles-search-filter.png)

Dalla finestra di dialogo **[!UICONTROL Select identity namespace]**, scegliete lo spazio dei nomi in base al quale eseguire la ricerca oppure utilizzate la barra di ricerca nella finestra di dialogo per iniziare a digitare il nome di uno spazio dei nomi. È possibile selezionare uno spazio dei nomi per visualizzare ulteriori dettagli. Una volta trovato lo spazio dei nomi da utilizzare, è possibile selezionare il pulsante di scelta e premere **[!UICONTROL Select]** per continuare.

![](../images/user-guide/profiles-select-identity-namespace.png)

### Valore identità

Dopo aver selezionato uno spazio dei nomi di identità, tornate alla scheda **[!UICONTROL Browse]** in cui è possibile inserire un **[!UICONTROL Identity value]**. Questo valore è specifico di un profilo cliente singolo e deve essere una voce valida per lo spazio dei nomi fornito. Ad esempio, se si seleziona lo spazio nomi identità &quot;E-mail&quot; sarà necessario un valore di identità sotto forma di indirizzo e-mail valido.

![](../images/user-guide/profiles-show-profile.png)

Una volta immesso un valore, selezionare **[!UICONTROL Show profile]** e viene restituito un profilo singolo corrispondente al valore. Selezionare **[!UICONTROL Profile ID]** per visualizzare i dettagli del profilo.

![](../images/user-guide/profiles-display-profile.png)

### Dettagli profilo {#profile-detail}

Dopo aver selezionato **[!UICONTROL Profile ID]**, si apre la scheda **[!UICONTROL Detail]**. Le informazioni di profilo visualizzate nella scheda **[!UICONTROL Detail]** sono state unite da più frammenti di profilo per formare una singola vista del singolo cliente. Ciò include dettagli del cliente quali attributi di base, identità collegate e preferenze del canale. I campi predefiniti visualizzati possono essere modificati anche a livello di organizzazione per visualizzare gli attributi di profilo preferiti. Per ulteriori informazioni sulla personalizzazione di questi campi, comprese istruzioni dettagliate per l&#39;aggiunta e la rimozione di attributi e il ridimensionamento dei pannelli del dashboard, consultare la [guida alla personalizzazione dei dettagli del profilo](profile-customization.md).

![](../images/user-guide/profiles-profile-detail.png)

Per visualizzare ulteriori informazioni relative al singolo profilo, seleziona un&#39;altra delle schede disponibili. Queste schede includono attributi, eventi e appartenenza al segmento, che mostra i segmenti per i quali il profilo è attualmente qualificato.

![](../images/user-guide/profiles-attributes-events-segments.png)

## Unisci criteri

Dal menu principale **[!UICONTROL Profiles]**, selezionare la scheda **[!UICONTROL Merge Policies]** per visualizzare un elenco di criteri di unione appartenenti alla propria organizzazione. Ogni criterio elencato visualizza il nome, indipendentemente dal fatto che si tratti del criterio di unione predefinito, e la classe dello schema a cui si applica.

Per ulteriori informazioni sui criteri di unione, vedere la [guida all&#39;interfaccia utente dei criteri di unione](merge-policies.md).

Per ulteriori informazioni sull&#39;utilizzo dei criteri di unione tramite l&#39;API Profilo cliente in tempo reale, fare riferimento alla [guida dell&#39;endpoint dei criteri di unione](../api/merge-policies.md).

![](../images/user-guide/profiles-merge-policies.png)

## Schema unione {#union-schema}

Dal menu principale **[!UICONTROL Profiles]**, selezionate la scheda **[!UICONTROL Union Schema]** per visualizzare gli schemi di unione disponibili per i dati acquisiti. Uno schema di unione è un&#39;unione di tutti i campi [!DNL Experience Data Model] (XDM) della stessa classe, i cui schemi sono stati abilitati per l&#39;uso in [!DNL Real-time Customer Profile].

Per ulteriori informazioni sugli schemi unione, vedere la [guida dell&#39;interfaccia utente dello schema unione](union-schema.md).

![](../images/user-guide/profiles-union-schema.png)

## Passaggi successivi

Leggendo questa guida, ora puoi vedere e gestire i dati [!DNL Profile] utilizzando l&#39;interfaccia [!DNL Experience Platform]. Per informazioni su come lavorare con i dati del profilo utilizzando l&#39;API del profilo cliente in tempo reale, fare riferimento alla [Guida per gli sviluppatori di profili](../api/overview.md).