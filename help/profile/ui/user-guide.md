---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API;profilo unificato;profilo unificato;unificato;profilo;rtcp;abilita profilo;abilita profilo;schema unione;PROFILO UNIONE;profilo unione
title: Guida all’interfaccia utente del profilo cliente in tempo reale
topic-legacy: guide
description: Profilo cliente in tempo reale crea una visualizzazione olistica di ciascuno dei tuoi singoli clienti, combinando dati provenienti da più canali tra cui online, offline, CRM e dati di terze parti. Questo documento funge da guida per l’interazione con Profilo cliente in tempo reale nell’interfaccia utente di Adobe Experience Platform.
exl-id: 792a3a73-58a4-4163-9212-4d43d24c2770
source-git-commit: b5e6376b54fe8b53fbabf85a2909293cebd93ccc
workflow-type: tm+mt
source-wordcount: '1568'
ht-degree: 0%

---

# [!DNL Real-time Customer Profile] Guida all’interfaccia utente

[!DNL Real-time Customer Profile] crea una visualizzazione olistica di ciascuno dei tuoi singoli clienti, combinando dati provenienti da più canali tra cui dati online, offline, CRM e di terze parti. Questo documento funge da guida per l’interazione con i dati [!DNL Real-time Customer Profile] nell’interfaccia utente di Adobe Experience Platform.

## Introduzione

Questa guida all&#39;interfaccia utente richiede una comprensione dei vari servizi [!DNL Experience Platform] coinvolti nella gestione di [!DNL Real-time Customer Profiles]. Prima di leggere questa guida o di lavorare nell’interfaccia utente, controlla la documentazione relativa ai seguenti servizi:

* [[!DNL Real-time Customer Profile] panoramica](../home.md): Fornisce un profilo di consumatore unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [[!DNL Identity Service]](../../identity-service/home.md): Consente  [!DNL Real-time Customer Profile] di colmare le identità provenienti da origini dati diverse durante l’acquisizione in  [!DNL Platform].
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Il framework standardizzato in base al quale  [!DNL Platform] vengono organizzati i dati sulla customer experience.

## [!UICONTROL Panoramica]

Nell’interfaccia utente di Experience Platform, seleziona **[!UICONTROL Profiles]** nel menu di navigazione a sinistra per aprire la scheda **[!UICONTROL Panoramica]** che mostra il dashboard del profilo.

>[!NOTE]
>
>Se la tua organizzazione è nuova di Platform e non dispone ancora di set di dati di profilo attivi o di criteri di unione creati, la dashboard [!UICONTROL Profiles] non è visibile. Al contrario, la scheda [!UICONTROL Panoramica] mostra collegamenti e documentazione per aiutarti a iniziare con Profilo cliente in tempo reale.

### Dashboard dei profili {#profile-dashboard}

Il dashboard del profilo delinea le metriche chiave correlate ai dati di profilo della tua organizzazione.

Per ulteriori informazioni, visita la [guida alla dashboard del profilo](../../dashboards/guides/profiles.md).

![](../../dashboards/images/profiles/dashboard-overview.png)

## [!UICONTROL Metriche ] browser

Seleziona la scheda **[!UICONTROL Sfoglia]** per visualizzare diverse metriche correlate ai dati di profilo della tua organizzazione. È inoltre possibile utilizzare questa scheda per sfogliare l’archivio dei profili utilizzando un criterio di unione o un’identità, come descritto nella sezione successiva di questa guida.

Sul lato destro della scheda **[!UICONTROL Sfoglia]** è presente il [conteggio dei profili](#profile-count) e un elenco di profili [per namespace](#profiles-by-namespace).

>[!NOTE]
>
>Queste metriche di profilo possono variare dalle metriche visualizzate nel [dashboard del profilo](#profile-dashboard) perché vengono valutate utilizzando i criteri di unione predefiniti della tua organizzazione. Per ulteriori informazioni sull&#39;utilizzo dei criteri di unione, tra cui la definizione di un criterio di unione predefinito, vedere la [panoramica dei criteri di unione](../merge-policies/overview.md).

Oltre a queste metriche, questa sezione fornisce una data e un’ora dell’ultimo aggiornamento, indicando quando sono state valutate le metriche.

![](../images/user-guide/profiles-browse-metrics.png)

### Numero di profili {#profile-count}

Il conteggio dei profili visualizza il numero totale di profili di cui dispone l’organizzazione all’interno dell’Experience Platform, dopo che il criterio di unione predefinito dell’organizzazione ha unito i frammenti di profilo per formare un singolo profilo per ogni singolo cliente. In altre parole, l’organizzazione può disporre di più frammenti di profilo relativi a un singolo cliente che interagisce con il tuo marchio su diversi canali, ma questi frammenti verranno uniti (in base al criterio di unione predefinito) e restituiranno un conteggio di &quot;1&quot; profilo perché sono tutti correlati allo stesso individuo.

Il conteggio dei profili include anche profili con attributi (dati record) e profili contenenti solo dati di serie temporali (eventi), ad esempio profili Adobe Analytics. Il conteggio dei profili viene aggiornato regolarmente per fornire un numero totale aggiornato di profili all’interno di Platform.

#### Aggiornamento della metrica del conteggio dei profili

Quando l&#39;acquisizione di record nell&#39;archivio [!DNL Profile] aumenta o diminuisce il conteggio di oltre il 5%, viene attivato un processo per aggiornare il conteggio. Per i flussi di lavoro con dati in streaming, viene eseguito un controllo su base oraria per determinare se la soglia di aumento o diminuzione del 5% è stata soddisfatta. In caso affermativo, viene attivato automaticamente un processo per aggiornare il conteggio del profilo. Per l’acquisizione batch, entro 15 minuti dal corretto inserimento di un batch nell’archivio profili, se viene soddisfatta la soglia di aumento o riduzione del 5%, viene eseguito un processo per aggiornare il conteggio dei profili.

### [!UICONTROL Profili per namespace] {#profiles-by-namespace}

La metrica **[!UICONTROL Profili per namespace]** visualizza il conteggio totale e la suddivisione dei namespace in tutti i profili uniti nel tuo archivio profili. Il numero totale di profili per namespace (in altre parole, l’aggiunta insieme dei valori mostrati per ogni namespace) sarà sempre superiore alla metrica di conteggio dei profili, perché a un profilo potrebbero essere associati più namespace. Ad esempio, se un cliente interagisce con il tuo marchio su più di un canale, a quel singolo cliente saranno associati più namespace.

#### Aggiornamento dei profili per metrica [!UICONTROL spazio dei nomi]

Simile alla metrica [conteggio profilo](#profile-count), quando l’acquisizione di record nello store [!DNL Profile] aumenta o diminuisce il conteggio di oltre il 5%, viene attivato un processo per aggiornare le metriche dello spazio dei nomi. Per i flussi di lavoro con dati in streaming, viene eseguito un controllo su base oraria per determinare se la soglia di aumento o diminuzione del 5% è stata soddisfatta. In caso affermativo, viene attivato automaticamente un processo per aggiornare il conteggio del profilo. Per l’acquisizione in batch, entro 15 minuti dal corretto inserimento di un batch nell’ archivio [!DNL Profile], se viene soddisfatta la soglia di aumento o diminuzione del 5%, viene eseguito un processo per aggiornare le metriche.

## Utilizza la scheda [!UICONTROL Sfoglia] per visualizzare i profili

Nella scheda **[!UICONTROL Sfoglia]** è possibile visualizzare profili di esempio utilizzando un criterio di unione o cercare profili specifici utilizzando uno spazio dei nomi e un valore di identità.

![](../images/user-guide/browse-by-none-selected.png)

### Sfoglia per [!UICONTROL Criteri di unione]

Per impostazione predefinita, la scheda **[!UICONTROL Sfoglia]** è impostata sul criterio di unione predefinito per la propria organizzazione. Per scegliere un criterio di unione diverso, selezionare il `X` accanto al nome del criterio di unione, quindi utilizzare il selettore per aprire la finestra di dialogo **[!UICONTROL Seleziona criterio di unione]**.

>[!NOTE]
>
>Se non è selezionato alcun criterio di unione, utilizza il pulsante di selezione accanto al campo **[!UICONTROL Criteri di unione]** per aprire la finestra di dialogo di selezione.

![](../images/user-guide/browse-by-merge-policy.png)

Per scegliere un criterio di unione dalla finestra di dialogo **[!UICONTROL Seleziona criterio di unione]**, selezionare il pulsante di scelta accanto al nome del criterio, quindi utilizzare **[!UICONTROL Seleziona]** per tornare alla scheda [!UICONTROL Sfoglia]. È quindi possibile selezionare **[!UICONTROL Visualizza]** per aggiornare i profili di esempio e visualizzare un campionamento dei profili con il nuovo criterio di unione applicato.

![](../images/user-guide/select-merge-policy-dialog.png)

I profili visualizzati rappresentano un esempio di fino a 20 profili dall’archivio profili della tua organizzazione, dopo l’applicazione del criterio di unione selezionato. I profili di esempio per il criterio di unione selezionato vengono aggiornati quando vengono aggiunti nuovi dati all’archivio profili dell’organizzazione.

Per visualizzare i dettagli di uno dei profili di esempio, seleziona l&#39; **[!UICONTROL ID profilo]**. Per ulteriori informazioni, consulta la sezione più avanti in questa guida sulla [visualizzazione dei dettagli del profilo](#profile-detail).

![](../images/user-guide/sample-profiles.png)

Per ulteriori informazioni sull&#39;unione dei criteri e sul loro ruolo all&#39;interno di Platform, consulta la [panoramica dei criteri di unione](../merge-policies/overview.md).


### Sfoglia per [!UICONTROL Identità]

Nella scheda **[!UICONTROL Sfoglia]** è possibile utilizzare uno spazio dei nomi di identità per cercare un profilo specifico in base a un valore di identità. Per effettuare la ricerca in base a un&#39;identità è necessario specificare un criterio di unione, uno spazio dei nomi di identità e un valore di identità.

![](../images/user-guide/browse-by-identity.png)

Se necessario, utilizzare il selettore **[!UICONTROL Criteri di unione]** per aprire la finestra di dialogo **[!UICONTROL Seleziona criterio di unione]** e scegliere il criterio di unione che si desidera utilizzare.

![](../images/user-guide/select-merge-policy-dialog.png)

Quindi utilizza il selettore **[!UICONTROL Identity namespace]** per aprire la finestra di dialogo **[!UICONTROL Select identity namespace]** e scegli lo spazio dei nomi in base al quale desideri eseguire la ricerca. Se l’organizzazione dispone di più spazi dei nomi, è possibile utilizzare la barra di ricerca nella finestra di dialogo per iniziare a digitare il nome di uno spazio dei nomi.

Puoi selezionare uno spazio dei nomi per visualizzare ulteriori dettagli oppure il pulsante di scelta per scegliere uno spazio dei nomi. Puoi quindi utilizzare **[!UICONTROL Seleziona]** per continuare.

![](../images/user-guide/profiles-select-identity-namespace.png)

Dopo aver selezionato uno [!UICONTROL spazio dei nomi identità] e essere tornato alla scheda [!UICONTROL Sfoglia], puoi immettere un **[!UICONTROL valore identità]** relativo allo spazio dei nomi selezionato.

>[!NOTE]
>
>Questo valore è specifico per un profilo cliente individuale e deve essere una voce valida per lo spazio dei nomi fornito. Ad esempio, la selezione dello spazio dei nomi di identità &quot;E-mail&quot; richiede un valore di identità sotto forma di un indirizzo e-mail valido.

![](../images/user-guide/browse-by-identity-values.png)

Una volta immesso un valore, seleziona **[!UICONTROL Visualizza]** e viene restituito un singolo profilo corrispondente al valore. Seleziona l&#39; **[!UICONTROL ID profilo]** per visualizzare i dettagli del profilo.

![](../images/user-guide/browse-by-identity-profile.png)

## Visualizzare i dettagli del profilo {#profile-detail}

Dopo aver selezionato un **[!UICONTROL ID profilo]**, si apre la scheda **[!UICONTROL Dettagli]** . Le informazioni di profilo visualizzate nella scheda **[!UICONTROL Dettaglio]** sono state unite da più frammenti di profilo per formare una singola visualizzazione del singolo cliente. Ciò include dettagli del cliente quali attributi di base, identità collegate e preferenze del canale.

I campi predefiniti visualizzati possono essere modificati anche a livello organizzativo per visualizzare gli attributi di profilo preferiti. Per ulteriori informazioni sulla personalizzazione di questi campi, incluse le istruzioni dettagliate per l’aggiunta e la rimozione degli attributi e il ridimensionamento dei pannelli della dashboard, consulta la [guida alla personalizzazione dei dettagli del profilo](profile-customization.md).

![](../images/user-guide/profiles-profile-detail.png)

Puoi visualizzare ulteriori informazioni relative al singolo profilo selezionando un’altra delle schede disponibili. Queste schede includono attributi, eventi e la scheda di appartenenza del segmento che mostra i segmenti per i quali il profilo è attualmente qualificato.

![](../images/user-guide/profiles-attributes-events-segments.png)

## Unisci criteri

Dal menu principale **[!UICONTROL Profili]**, selezionare la scheda **[!UICONTROL Criteri di unione]** per visualizzare un elenco dei criteri di unione appartenenti all&#39;organizzazione. Ogni criterio elencato visualizza il nome, indipendentemente dal fatto che si tratti del criterio di unione predefinito, e la classe dello schema a cui si applica.

Per ulteriori informazioni sui criteri di unione, vedere la [panoramica dei criteri di unione](../merge-policies/overview.md).

![](../images/user-guide/profiles-merge-policies.png)

## Schema dell&#39;unione {#union-schema}

Dal menu principale **[!UICONTROL Profili]**, seleziona la scheda **[!UICONTROL Schema unione]** per visualizzare gli schemi di unione disponibili per i dati acquisiti. Uno schema di unione è un’unione di tutti i campi [!DNL Experience Data Model] (XDM) della stessa classe, i cui schemi sono stati abilitati per l’utilizzo in [!DNL Real-time Customer Profile].

Per ulteriori informazioni sugli schemi di unione, visita la [guida all&#39;interfaccia utente dello schema di unione](union-schema.md).

![](../images/user-guide/profiles-union-schema.png)

## Passaggi successivi

Leggendo questa guida, sarai in grado di visualizzare e gestire i dati del profilo della tua organizzazione tramite l’interfaccia utente di Experience Platform. Per informazioni su come lavorare con i dati di profilo utilizzando le API di Experience Platform, consulta la [Guida API del profilo cliente in tempo reale](../api/overview.md).
