---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Guida utente del profilo cliente in tempo reale
topic: guide
translation-type: tm+mt
source-git-commit: 4589d0cdca36992feea208850abdda1a9dc246c0
workflow-type: tm+mt
source-wordcount: '1208'
ht-degree: 0%

---


# Guida utente del profilo cliente in tempo reale

Profilo cliente in tempo reale crea una visualizzazione olistica di ciascuno dei tuoi clienti, combinando dati da più canali tra cui dati online, offline, CRM e di terze parti.

Questo documento funge da guida per l&#39;interazione con il profilo cliente in tempo reale nell&#39;interfaccia utente del Adobe Experience Platform .

## Introduzione

Questa guida utente richiede una comprensione dei vari servizi Experience Platform  coinvolti nella gestione dei profili cliente in tempo reale. Prima di leggere questa guida utente, consulta la documentazione relativa ai seguenti servizi:

* [Profilo](../home.md)cliente in tempo reale: Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [Servizio](../../identity-service/home.md)identità: Abilita il profilo cliente in tempo reale collegando identità da origini dati diverse durante l&#39;assimilazione ad Platform.
* [Experience Data Model (XDM)](../../xdm/home.md): Framework standard con cui Platform organizza i dati sull&#39;esperienza dei clienti.

## Panoramica

Nell’interfaccia utente [di](http://platform.adobe.com)Experience Platform, fate clic su **Profili** nella barra di navigazione a sinistra per aprire la scheda _Panoramica_ . Questa scheda fornisce collegamenti alla documentazione e ai video per agevolare la comprensione e l&#39;utilizzo dei profili.

![](../images/user-guide/profiles-overview.png)

## Sfoglia

Selezionate la scheda *Sfoglia* per individuare i profili in base all’identità.

![](../images/user-guide/profiles-browse.png)

### Metriche profilo {#profile-metrics}

Sul lato destro della scheda *Sfoglia* sono presenti diverse metriche importanti correlate ai dati del profilo, tra cui il conteggio [totale dei](#profile-count) profili e un elenco di [profili per namespace](#profiles-by-namespace).

Queste metriche del profilo vengono valutate utilizzando il criterio di unione predefinito dell&#39;organizzazione. Per ulteriori informazioni sull&#39;utilizzo dei criteri di unione, inclusa la modalità di definizione di un criterio di unione predefinito, vedere la guida [utente](merge-policies.md)Unisci criteri.

Oltre a queste metriche, la sezione delle metriche del profilo fornisce anche una data e un&#39;ora *dell&#39;ultimo aggiornamento* , che mostrano quando sono state valutate le metriche per l&#39;ultima volta.

![](../images/user-guide/profiles-profile-metrics.png)

### Conteggio profili {#profile-count}

Il conteggio dei profili visualizza il numero totale di profili di cui dispone l&#39;organizzazione in  Experience Platform, dopo che il criterio di unione predefinito dell&#39;organizzazione ha unito i frammenti di profilo per formare un unico profilo per ciascun cliente. In altre parole, l&#39;organizzazione potrebbe avere più frammenti di profilo correlati a un singolo cliente che interagisce con il proprio marchio tra canali diversi, ma tali frammenti sarebbero uniti (in base al criterio di unione predefinito) e restituirebbero un conteggio di profilo pari a &quot;1&quot; perché tutti correlati allo stesso individuo.

Il conteggio dei profili include anche profili con attributi (dati di record) e profili contenenti solo dati di serie temporali (eventi), come i profili Adobe  Analytics. Il conteggio dei profili viene aggiornato regolarmente per fornire un numero totale aggiornato di profili in Platform.

Quando l’inserimento di profili nell’archivio profili aumenta o diminuisce il conteggio di oltre il 5%, viene attivato un processo per aggiornare il conteggio. Per i flussi di lavoro dei dati in streaming, viene effettuato un controllo ogni ora per determinare se è stata raggiunta la soglia di incremento o riduzione del 5%. In caso affermativo, viene attivato automaticamente un processo per aggiornare il conteggio dei profili. Per l’assimilazione batch, entro 15 minuti dal corretto inserimento di un batch nell’archivio profili, se viene raggiunta la soglia di incremento o riduzione del 5%, viene eseguito un processo per aggiornare il conteggio dei profili.

### Profili per namespace {#profiles-by-namespace}

I *profili per metrica namespace* mostrano il conteggio totale e la suddivisione degli spazi di nomi in tutti i profili uniti nel tuo archivio profili. Il numero totale di profili per namespace (in altre parole, aggiungendo insieme i valori mostrati per ogni namespace) sarà sempre superiore alla metrica del conteggio dei profili, perché a un profilo potrebbero essere associati più spazi dei nomi. Ad esempio, se un cliente interagisce con il tuo marchio su più di un canale, a quel singolo cliente saranno associati più spazi dei nomi.

Simile alla metrica del conteggio [dei](#profile-count) profili, quando l&#39;inserimento dei profili nell&#39;archivio profili aumenta o diminuisce il conteggio di oltre il 5%, viene attivato un processo per aggiornare le metriche dello spazio nomi. Per i flussi di lavoro dei dati in streaming, viene effettuato un controllo ogni ora per determinare se è stata raggiunta la soglia di incremento o riduzione del 5%. In caso affermativo, viene attivato automaticamente un processo per aggiornare il conteggio dei profili. Per l’assimilazione batch, entro 15 minuti dal corretto inserimento di un batch nell’archivio profili, se viene raggiunta la soglia di incremento o riduzione del 5%, viene eseguito un processo per aggiornare le metriche.

### Unisci criterio

Il selettore dei criteri **di** unione seleziona automaticamente i criteri di unione predefiniti per l&#39;organizzazione. Se non si desidera utilizzare tale criterio di unione, è possibile selezionare il criterio di unione `X` accanto al criterio di unione predefinito per aprire una finestra di dialogo *Seleziona criterio* di unione in cui scegliere un altro criterio di unione. Per ulteriori informazioni sui criteri di unione, consultare la guida [utente](merge-policies.md)Unisci criteri.

![](../images/user-guide/profiles-search-merge-policy.png)

### Spazio dei nomi identità

Il selettore dello spazio dei nomi **di** identità apre una finestra di dialogo in cui è possibile scegliere lo spazio dei nomi di identità per il quale eseguire la ricerca. È inoltre possibile personalizzare gli attributi visualizzati nella ricerca selezionando l&#39;icona del filtro e scegliendo gli attributi da aggiungere o rimuovere.

![](../images/user-guide/profiles-search-filter.png)

Dalla finestra di dialogo *Seleziona spazio nomi* identità, scegliete lo spazio nomi in base al quale eseguire la ricerca oppure utilizzate la barra di **ricerca** nella finestra di dialogo per iniziare a digitare il nome di uno spazio nomi. È possibile selezionare uno spazio dei nomi per visualizzare ulteriori dettagli. Una volta trovato lo spazio dei nomi da cercare, è possibile selezionare il pulsante di scelta e premere **Seleziona** per continuare.

![](../images/user-guide/profiles-select-identity-namespace.png)

### Valore identità

Dopo aver selezionato uno spazio dei nomi **** Identità, si torna alla scheda *Sfoglia* , dove è possibile immettere un valore **** Identità. Questo valore è specifico di un profilo cliente singolo e deve essere una voce valida per lo spazio dei nomi fornito. Ad esempio, se si seleziona lo spazio nomi **** Identità &quot;E-mail&quot; sarà necessario un valore **** Identità sotto forma di indirizzo e-mail valido.

![](../images/user-guide/profiles-show-profile.png)

Dopo aver immesso un valore, selezionare **Mostra profilo** e viene restituito un profilo singolo che corrisponde al valore. Selezionate l’ID **** profilo per visualizzare i dettagli del profilo.

![](../images/user-guide/profiles-display-profile.png)

### Dettagli profilo

Dopo aver selezionato l’ID **del** profilo, si apre la scheda _Dettagli_ . In questa pagina vengono visualizzate informazioni sul profilo selezionato, inclusi gli attributi di base, le identità collegate e i canali di contatto disponibili. Le informazioni di profilo visualizzate sono state unite da più frammenti di profilo per formare una singola vista del singolo cliente.

![](../images/user-guide/profiles-profile-detail.png)

Potete visualizzare informazioni aggiuntive correlate al profilo, inclusi *Attributi*, *Eventi* e *Segmenti* ai quali il profilo è membro.

![](../images/user-guide/profiles-attributes-events-segments.png)

## Unisci criteri

Selezionate la scheda *Unisci criteri* per visualizzare un elenco di criteri di unione appartenenti alla vostra organizzazione. Ogni criterio elencato visualizza il nome, indipendentemente dal fatto che si tratti del criterio di unione predefinito, e lo schema a cui si applica.

Per ulteriori informazioni sui criteri di unione, consultare la guida [utente](merge-policies.md)Unisci criteri.

![](../images/user-guide/profiles-merge-policies.png)

## Schema unione

Selezionate la scheda Schema ** unione per visualizzare gli schemi di unione per l&#39;archivio profili. Uno schema di unione è un&#39;unione di tutti i campi Experience Data Model (XDM) della stessa classe, i cui schemi sono stati abilitati per l&#39;utilizzo in Real-time Customer Profile (Profilo cliente in tempo reale). Selezionare una classe nell&#39;elenco a sinistra per visualizzare la struttura dello schema di unione nel quadro.

Ad esempio, selezionando &quot;Profilo XDM&quot; viene visualizzato lo schema di unione per la classe Profilo singolo XDM.

Per ulteriori informazioni sugli schemi di unione e sul loro ruolo nel profilo cliente in tempo reale, consulta la sezione sugli schemi di unione nella guida [alla composizione](../../xdm/schema/composition.md) dello schema.

![](../images/user-guide/profiles-union-schema.png)

## Passaggi successivi

Leggendo questa guida, ora puoi vedere e gestire i dati del tuo profilo utilizzando l&#39;interfaccia  di Experience Platform. Per informazioni su come sfruttare i dati del profilo cliente in tempo reale per generare segmenti di pubblico, consulta la documentazione [sulla](../../segmentation/home.md)segmentazione.