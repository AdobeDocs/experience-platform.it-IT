---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API;profilo unificato;profilo unificato;unificato;profilo;rtcp;abilitare profilo;abilitare profilo;abilitare profilo;schema unione;PROFILO UNIONE;profilo unione
title: Guida all’interfaccia utente di Real-Time Customer Profile
description: Real-Time Customer Profile crea una visualizzazione olistica di ciascuno dei singoli clienti, combinando dati provenienti da più canali tra cui dati online, offline, del sistema CRM e di terze parti. Questo documento funge da guida per l’interazione con Real-Time Customer Profile nell’interfaccia utente di Adobe Experience Platform.
exl-id: 792a3a73-58a4-4163-9212-4d43d24c2770
source-git-commit: 804f87563abf36a1aa203cb675a687dd262231a7
workflow-type: tm+mt
source-wordcount: '2108'
ht-degree: 0%

---

# [!DNL Real-Time Customer Profile] Guida all’interfaccia utente

[!DNL Real-Time Customer Profile] crea una visualizzazione olistica di ciascuno dei singoli clienti, combinando dati provenienti da più canali tra cui dati online, offline, del sistema CRM e di terze parti. Questo documento funge da guida per l’interazione con [!DNL Real-Time Customer Profile] dati nell’interfaccia utente di Adobe Experience Platform.

## Introduzione

Questa guida dell’interfaccia utente richiede una comprensione dei vari [!DNL Experience Platform] servizi coinvolti nella gestione [!DNL Real-Time Customer Profiles]. Prima di leggere questa guida o di lavorare nell’interfaccia utente, consulta la documentazione dei seguenti servizi:

* [[!DNL Real-Time Customer Profile] panoramica](../home.md): fornisce un profilo consumer unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [[!DNL Identity Service]](../../identity-service/home.md): Abilita [!DNL Real-Time Customer Profile] collegando le identità da diverse origini dati quando vengono acquisite in [!DNL Platform].
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): il quadro standardizzato mediante il quale [!DNL Platform] organizza i dati sull’esperienza del cliente.

## [!UICONTROL Panoramica]

Nell’interfaccia utente di Experienci Platform, seleziona **[!UICONTROL Profili]** nel menu di navigazione a sinistra per aprire **[!UICONTROL Panoramica]** scheda che visualizza il dashboard del profilo.

>[!NOTE]
>
>Se la tua organizzazione non utilizza ancora Platform e non dispone ancora di set di dati di profilo attivi o criteri di unione creati, il [!UICONTROL Profili] dashboard non visibile. Al contrario, [!UICONTROL Panoramica] Questa scheda mostra collegamenti e documentazione utili per iniziare a utilizzare Real-Time Customer Profile.

### Dashboard profili {#profile-dashboard}

La dashboard dei profili delinea le metriche chiave relative ai dati di profilo della tua organizzazione.

Per ulteriori informazioni, visita [guida della dashboard di profilo](../../dashboards/guides/profiles.md).

![Viene visualizzato il dashboard Profilo.](../../dashboards/images/profiles/dashboard-overview.png)

## [!UICONTROL Sfoglia] metriche di tabulazione

Seleziona la **[!UICONTROL Sfoglia]** per visualizzare diverse metriche relative ai dati di profilo della tua organizzazione. È inoltre possibile utilizzare questa scheda per sfogliare l’archivio profili utilizzando un criterio di unione o un’identità, come descritto nella sezione successiva di questa guida.

Sul lato destro del **[!UICONTROL Sfoglia]** è il valore di [conteggio profili](#profile-count) nonché un elenco di [profili per spazio dei nomi](#profiles-by-namespace).

>[!NOTE]
>
>Queste metriche di profilo possono variare rispetto alle metriche visualizzate nella [dashboard dei profili](#profile-dashboard) perché vengono valutati utilizzando il criterio di unione predefinito dell’organizzazione. Per ulteriori informazioni sull&#39;utilizzo dei criteri di unione, tra cui la definizione di un criterio di unione predefinito, vedere [panoramica dei criteri di unione](../merge-policies/overview.md).

Oltre a queste metriche, questa sezione fornisce una data e un’ora dell’ultimo aggiornamento, che mostrano quando le metriche sono state valutate l’ultima volta.

![Vengono visualizzate ed evidenziate le metriche Profilo.](../images/user-guide/browse-metrics.png)

### Conteggio dei profili {#profile-count}

Nel conteggio dei profili viene visualizzato il numero totale di profili di cui dispone l’organizzazione in Experienci Platform, dopo che il criterio di unione predefinito dell’organizzazione ha unito i frammenti di profilo per formare un singolo profilo per ogni singolo cliente. In altre parole, la tua organizzazione può avere più frammenti di profilo correlati a un singolo cliente che interagisce con il tuo marchio su canali diversi, ma questi frammenti verrebbero uniti (in base al criterio di unione predefinito) e restituirebbero un conteggio di &quot;1&quot; profilo perché sono tutti correlati alla stessa persona.

Il conteggio dei profili include anche profili con attributi (dati record) e profili contenenti solo dati di serie temporali (eventi), come i profili di Adobe Analytics. Il conteggio dei profili viene aggiornato regolarmente per fornire un numero totale aggiornato di profili all’interno di Platform.

#### Aggiornamento della metrica del conteggio dei profili

Quando l’acquisizione di record in [!DNL Profile] store aumenta o diminuisce il conteggio di oltre il 5%; viene attivato un processo per aggiornare il conteggio. Per i flussi di lavoro di dati in streaming, viene eseguito un controllo su base oraria per determinare se la soglia di aumento o riduzione del 5% è stata raggiunta. In caso affermativo, viene attivato automaticamente un processo per aggiornare il conteggio dei profili. Per l’acquisizione batch, entro 15 minuti dalla corretta acquisizione di un batch nell’archivio profili, se viene raggiunta la soglia di aumento o di riduzione del 5%, viene eseguito un processo per aggiornare il conteggio dei profili.

### [!UICONTROL Profili per spazio dei nomi] {#profiles-by-namespace}

Il **[!UICONTROL Profili per spazio dei nomi]** Con la metrica vengono visualizzati il conteggio totale e il raggruppamento degli spazi dei nomi in tutti i profili uniti nell’archivio profili. Il numero totale di profili per spazio dei nomi (in altre parole, la somma dei valori mostrati per ciascuno spazio dei nomi) sarà sempre superiore alla metrica del conteggio dei profili, perché a un profilo potrebbero essere associati più spazi dei nomi. Ad esempio, se un cliente interagisce con il tuo marchio su più di un canale, a quel singolo cliente verranno associati più spazi dei nomi.

#### Aggiornamento di [!UICONTROL Profili per spazio dei nomi] metrica

Simile a [conteggio profili](#profile-count) metrica, quando l’acquisizione di record in [!DNL Profile] store aumenta o diminuisce il conteggio di oltre il 5%; viene attivato un processo per aggiornare le metriche dello spazio dei nomi. Per i flussi di lavoro di dati in streaming, viene eseguito un controllo su base oraria per determinare se la soglia di aumento o riduzione del 5% è stata raggiunta. In caso affermativo, viene attivato automaticamente un processo per aggiornare il conteggio dei profili. Per l’acquisizione batch, entro 15 minuti dalla corretta acquisizione di un batch nel [!DNL Profile] store, se viene raggiunta la soglia di aumento o riduzione del 5%, viene eseguito un processo per aggiornare le metriche.

## Utilizzare [!UICONTROL Sfoglia] scheda per visualizzare i profili

Il giorno **[!UICONTROL Sfoglia]** scheda puoi visualizzare i profili di esempio utilizzando un criterio di unione o cercare profili specifici utilizzando uno spazio dei nomi e un valore di identità.

![Vengono visualizzati i profili appartenenti all’organizzazione.](../images/user-guide/none-selected.png)

### Sfoglia per [!UICONTROL Criterio di unione]

Il **[!UICONTROL Sfoglia]** è impostata sul criterio di unione predefinito per l’organizzazione. Per scegliere un criterio di unione diverso, selezionare `X` accanto al nome del criterio di unione, quindi utilizzare il selettore per aprire **[!UICONTROL Seleziona criterio di unione]** .

>[!NOTE]
>
>Se non è selezionato alcun criterio di unione, utilizza il pulsante di selezione accanto a **[!UICONTROL Criterio di unione]** per aprire la finestra di dialogo di selezione.

![Il selettore dei criteri di unione viene evidenziato.](../images/user-guide/browse-by-merge-policy.png)

Per scegliere un criterio di unione da **[!UICONTROL Seleziona criterio di unione]** , seleziona il pulsante di opzione accanto al nome del criterio, quindi utilizza **[!UICONTROL Seleziona]** per tornare al [!UICONTROL Sfoglia] scheda. A questo punto puoi selezionare **[!UICONTROL Visualizza]** per aggiornare i profili di esempio e visualizzare un campionamento dei profili con il nuovo criterio di unione applicato.

![Viene visualizzata una finestra di dialogo in cui è possibile selezionare il criterio di unione in base al quale filtrare.](../images/user-guide/select-merge-policy.png)

I profili visualizzati rappresentano un campione di un massimo di 20 profili dall’archivio profili della tua organizzazione, dopo l’applicazione del criterio di unione selezionato. I profili di esempio per il criterio di unione selezionato vengono aggiornati quando vengono aggiunti nuovi dati all’archivio dei profili della tua organizzazione.

Per visualizzare i dettagli di uno dei profili di esempio, seleziona la **[!UICONTROL ID profilo]**. Per ulteriori informazioni, consulta la sezione più avanti in questa guida su [visualizzazione dei dettagli profilo](#profile-detail).

![Vengono visualizzati i profili di esempio che corrispondono al criterio di unione.](../images/user-guide/sample-profiles.png)

Per ulteriori informazioni sui criteri di unione e sul loro ruolo in Platform, consulta [panoramica dei criteri di unione](../merge-policies/overview.md).

### Sfoglia per [!UICONTROL Identità] {#browse-identity}

Il giorno **[!UICONTROL Sfoglia]** , puoi utilizzare uno spazio dei nomi delle identità per cercare un profilo specifico in base a un valore di identità. Per esplorare un’identità è necessario fornire un criterio di unione, uno spazio dei nomi dell’identità e un valore di identità.

![Il selettore dei criteri di unione viene evidenziato.](../images/user-guide/browse-by-merge-policy.png)

Se necessario, utilizzare **[!UICONTROL Criterio di unione]** selettore per aprire **[!UICONTROL Seleziona criterio di unione]** e scegliere il criterio di unione da utilizzare.

![Viene visualizzata una finestra di dialogo in cui è possibile selezionare il criterio di unione in base al quale filtrare.](../images/user-guide/select-merge-policy.png)

Quindi utilizza **[!UICONTROL Spazio dei nomi dell’identità]** selettore per aprire **[!UICONTROL Seleziona lo spazio dei nomi dell’identità]** e scegli lo spazio dei nomi in base al quale desideri eseguire la ricerca. Se nell’organizzazione sono presenti molti spazi dei nomi, puoi utilizzare la barra di ricerca nella finestra di dialogo per iniziare a digitare il nome di uno spazio dei nomi.

Puoi selezionare uno spazio dei nomi per visualizzare ulteriori dettagli oppure il pulsante di opzione per scegliere uno spazio dei nomi. A questo punto puoi utilizzare **[!UICONTROL Seleziona]** per continuare.

![Viene visualizzata una finestra di dialogo in cui puoi selezionare lo spazio dei nomi dell’identità in base al quale filtrare.](../images/user-guide/select-identity-namespace.png)

Dopo aver selezionato un [!UICONTROL Spazio dei nomi dell’identità] e tornando al [!UICONTROL Sfoglia] , è possibile immettere un **[!UICONTROL Valore identità]** relativo allo spazio dei nomi selezionato.

>[!NOTE]
>
>Questo valore è specifico di un singolo profilo cliente e deve essere una voce valida per lo spazio dei nomi fornito. Ad esempio, la selezione dello spazio dei nomi dell’identità &quot;E-mail&quot; richiederebbe un valore di identità sotto forma di un indirizzo e-mail valido.

![Il valore di identità in base al quale desideri filtrare viene evidenziato.](../images/user-guide/filter-identity-value.png)

Una volta inserito un valore, seleziona **[!UICONTROL Visualizza]** e viene restituito un singolo profilo corrispondente al valore. Seleziona la **[!UICONTROL ID profilo]** per visualizzare i dettagli del profilo.

![Viene evidenziato il profilo che corrisponde al valore di identità.](../images/user-guide/filtered-identity-value.png)

## Visualizza dettagli profilo {#profile-detail}

Dopo aver selezionato un **[!UICONTROL ID profilo]**, il **[!UICONTROL Dettaglio]** viene visualizzata la scheda. Le informazioni di profilo visualizzate sul **[!UICONTROL Dettaglio]** La scheda è stata unita da più frammenti di profilo per formare un’unica vista del singolo cliente. Ciò include i dettagli del cliente come attributi di base, identità collegate e preferenze di canale.

I campi predefiniti visualizzati possono anche essere modificati a livello di organizzazione per visualizzare gli attributi di profilo preferiti. Per ulteriori informazioni sulla personalizzazione di questi campi, incluse le istruzioni dettagliate per l’aggiunta e la rimozione di attributi e il ridimensionamento dei pannelli del dashboard, leggi [guida alla personalizzazione dei dettagli del profilo](profile-customization.md).

![Viene evidenziata la scheda Dettagli. Vengono visualizzati i dettagli del profilo.](../images/user-guide/profile-detail.png)

Puoi visualizzare ulteriori informazioni relative al singolo profilo cliente selezionando un’altra delle schede disponibili. Queste schede includono attributi, eventi e la scheda Appartenenza al pubblico che mostra i tipi di pubblico per i quali il profilo è attualmente qualificato.

### Scheda Attributi

Il **[!UICONTROL Attributi]** La scheda fornisce una vista a elenco che riepiloga tutti gli attributi correlati a un singolo profilo, dopo l’applicazione del criterio di unione specificato.

Questi attributi possono essere visualizzati anche come oggetto JSON selezionando per **[!UICONTROL Visualizza JSON]**. È utile per tutti gli utenti che desiderano comprendere meglio come vengono acquisiti gli attributi del profilo in Platform.

![Viene evidenziata la scheda Attributi. Vengono visualizzati gli attributi del profilo.](../images/user-guide/attributes.png)

Per visualizzare gli attributi disponibili sullo spigolo, selezionare **[!UICONTROL Bordo]** sul selettore posizione dati.

![Il selettore della posizione dei dati all’interno della scheda attributi è evidenziato.](../images/user-guide/attributes-select.png)

Per ulteriori informazioni sui profili edge, consulta la sezione [documentazione dei profili edge](../edge-profiles.md).

### Scheda Eventi

Il **[!UICONTROL Eventi]** La scheda contiene i dati dei 100 ExperienceEvents più recenti associati al cliente. Questi dati possono includere aperture e-mail, attività del carrello e visualizzazioni di pagina. Selezione **[!UICONTROL Visualizza tutto]** per ogni singolo evento fornisce campi e valori aggiuntivi acquisiti come parte dell’evento.

Gli eventi possono essere visualizzati anche come oggetto JSON selezionando per **[!UICONTROL Visualizza JSON]**. È utile per comprendere in che modo gli eventi vengono acquisiti in Platform.

![Viene evidenziata la scheda Eventi. Vengono visualizzati gli eventi del profilo.](../images/user-guide/events.png)

### Scheda Appartenenza al pubblico

Il **[!UICONTROL Iscrizione al pubblico]** Nella scheda viene visualizzato un elenco con il nome e la descrizione dei tipi di pubblico a cui appartiene attualmente il singolo profilo cliente. Questo elenco viene aggiornato automaticamente quando il profilo si qualifica o scade dai tipi di pubblico. Il numero totale di tipi di pubblico per i quali il profilo è attualmente qualificato viene visualizzato sul lato destro della scheda.

Per ulteriori informazioni sulla segmentazione nell’Experience Platform, consulta la sezione [Adobi Experience Platform di documentazione del servizio di segmentazione](../../segmentation/home.md).

![Viene evidenziata la scheda Appartenenza al pubblico. Vengono visualizzati i dettagli di iscrizione del pubblico del profilo.](../images/user-guide/audience-membership.png)

Per visualizzare l’appartenenza al pubblico dei profili disponibili su Edge, seleziona **[!UICONTROL Bordo]** nel selettore posizione dati. Ulteriori informazioni sulla segmentazione Edge sono disponibili nella sezione [guida alla segmentazione edge](../../segmentation/ui/edge-segmentation.md).

![Il selettore della posizione dei dati all’interno della scheda Appartenenza al pubblico viene evidenziato.](../images/user-guide/audience-membership-select.png)

## Criteri di unione

Dall&#39;elenco principale **[!UICONTROL Profili]** , selezionare il **[!UICONTROL Criteri di unione]** per visualizzare un elenco dei criteri di unione appartenenti alla tua organizzazione. Ogni criterio elencato visualizza il proprio nome, che si tratti o meno del criterio di unione predefinito, e la classe di schema a cui si applica.

Per ulteriori informazioni sui criteri di unione, vedi [panoramica dei criteri di unione](../merge-policies/overview.md).

![Viene evidenziata la scheda Criteri di unione. Vengono visualizzati i criteri di unione appartenenti all’organizzazione.](../images/user-guide/merge-policies.png)

## Schema di unione {#union-schema}

Dall&#39;elenco principale **[!UICONTROL Profili]** , selezionare il **[!UICONTROL Schema di unione]** per visualizzare gli schemi di unione disponibili per i dati acquisiti. Uno schema di unione è una combinazione di [!DNL Experience Data Model] (XDM) nella stessa classe, i cui schemi sono stati abilitati per l’utilizzo in [!DNL Real-Time Customer Profile].

Per ulteriori informazioni sugli schemi di unione, visita il [guida dell’interfaccia utente per lo schema di unione](union-schema.md).

![Viene evidenziata la scheda Schema di unione (Union Schema). Vengono visualizzati gli schemi di unione appartenenti all’organizzazione.](../images/user-guide/union-schema.png)

## Attributi calcolati {#computed-attributes}

Dall&#39;elenco principale **[!UICONTROL Profili]** , selezionare il **[!UICONTROL Attributi calcolati]** per visualizzare un elenco di attributi calcolati che appartengono alla tua organizzazione.

![Viene evidenziata la scheda Attributi calcolati.](../images/user-guide/computed-attributes.png)

Per ulteriori informazioni sugli attributi calcolati, consulta [panoramica degli attributi calcolati](../computed-attributes/overview.md). Per ulteriori informazioni su come utilizzare gli attributi calcolati nell’interfaccia utente di Platform, consulta [guida dell’interfaccia utente per attributi calcolati](../computed-attributes/ui.md).

## Passaggi successivi

Leggendo questa guida, sai come visualizzare e gestire i dati del profilo della tua organizzazione utilizzando l’interfaccia utente di Experienci Platform. Per informazioni su come lavorare con i dati del profilo utilizzando le API di Experienci Platform, consulta la [Guida all’API del profilo cliente in tempo reale](../api/overview.md).
