---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Guida utente del profilo cliente in tempo reale
topic: guide
translation-type: tm+mt
source-git-commit: 5718a3930f1e12e62a7bbe60f249c7f6f3434fa7
workflow-type: tm+mt
source-wordcount: '880'
ht-degree: 0%

---


# Guida utente del profilo cliente in tempo reale

Profilo cliente in tempo reale crea una visualizzazione olistica di ciascuno dei tuoi clienti, combinando dati da più canali tra cui dati online, offline, CRM e di terze parti.

Questo documento funge da guida per l’interazione con il profilo cliente in tempo reale nell’interfaccia utente di Adobe Experience Platform.

## Introduzione

Questa guida utente richiede una comprensione dei diversi servizi della piattaforma Experience Manager (Piattaforma esperienza) relativi alla gestione del profilo cliente in tempo reale. Prima di leggere questa guida utente, consulta la documentazione relativa ai seguenti servizi:

* [Profilo](../home.md)cliente in tempo reale: Fornisce un profilo di consumo unificato e in tempo reale basato su dati aggregati provenienti da più origini.
* [Servizio](../../identity-service/home.md)identità: Abilita il profilo cliente in tempo reale collegando identità da origini dati diverse che vengono caricate nella piattaforma.
* [Experience Data Model (XDM)](../../xdm/home.md): Il framework standardizzato tramite il quale la piattaforma organizza i dati sull&#39;esperienza cliente.

## Panoramica

Nell’interfaccia utente [della piattaforma](http://platform.adobe.com)Experience, fai clic su **Profili** nella barra di navigazione a sinistra per aprire la scheda _Panoramica_ . Questa scheda fornisce collegamenti alla documentazione e ai video per agevolare la comprensione e l&#39;utilizzo dei profili.

![](../images/user-guide/profiles-overview.png)

## Sfoglia profilo

Fate clic sulla scheda **Sfoglia** per individuare i profili in base alle identità. Questa scheda contiene anche il numero totale di [profili](#profile-count).

![](../images/user-guide/profiles-browse.png)

### Conteggio profili {#profile-count}

Il conteggio dei profili visualizza il numero totale di profili di cui dispone l&#39;organizzazione all&#39;interno di Experience Platform, dopo che il criterio di unione predefinito dell&#39;organizzazione ha unito i frammenti di profilo per formare un unico profilo per ciascun cliente. In altre parole, l&#39;organizzazione potrebbe avere più frammenti di profilo correlati a un singolo cliente che interagisce con il proprio marchio tra canali diversi, ma tali frammenti sarebbero uniti (in base al criterio di unione predefinito) e restituirebbero un conteggio di profilo pari a &quot;1&quot; perché tutti correlati allo stesso individuo.

Il conteggio dei profili include anche profili con attributi (dati di record) e profili contenenti solo dati di serie temporali (eventi), come i profili di Adobe Analytics. Il conteggio dei profili viene aggiornato regolarmente per fornire un numero totale aggiornato di profili all&#39;interno della piattaforma.

Quando l’inserimento di profili nell’archivio profili aumenta o diminuisce il conteggio di oltre il 5%, viene attivato un processo per aggiornare il conteggio. Per i flussi di lavoro dei dati in streaming, viene effettuato un controllo ogni ora per determinare se è stata raggiunta la soglia di incremento o riduzione del 5%. In caso affermativo, viene attivato automaticamente un processo per aggiornare il conteggio dei profili. Per l’assimilazione batch, entro 15 minuti dal corretto inserimento di un batch nell’archivio profili, se viene raggiunta la soglia di incremento o riduzione del 5%, viene eseguito un processo per aggiornare il conteggio dei profili.

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

Potete visualizzare informazioni aggiuntive correlate al profilo, inclusi Attributi, Eventi e Segmenti a cui il profilo è membro.

![](../images/user-guide/profiles-attributes-events-segments.png)

## Unisci criteri

Fare clic su **Unisci criteri** per visualizzare un elenco di criteri di unione appartenenti alla propria organizzazione. Ogni criterio elencato visualizza il nome, indipendentemente dal fatto che si tratti del criterio di unione predefinito, e lo schema a cui si applica.

Per ulteriori informazioni sull&#39;utilizzo dei criteri di unione nell&#39;interfaccia utente, consulta la guida [utente](merge-policies.md)Unisci criteri.

![](../images/user-guide/profiles-merge-policies.png)

## Schema unione

Fate clic su Schema **** unione per visualizzare gli schemi unione per l&#39;archivio profili. Uno schema di unione è un&#39;unione di tutti i campi Experience Data Model (XDM) della stessa classe, i cui schemi sono stati abilitati per l&#39;utilizzo in Real-time Customer Profile (Profilo cliente in tempo reale). Fare clic su una classe nell&#39;elenco a sinistra per visualizzare la struttura dello schema di unione nel quadro.

Ad esempio, selezionando &quot;Profilo XDM&quot; viene visualizzato lo schema di unione per la classe Profilo singolo XDM.

Per ulteriori informazioni sugli schemi di unione e sul loro ruolo nel profilo cliente in tempo reale, consulta la sezione sugli schemi di unione nella guida [alla composizione](../../xdm/schema/composition.md) dello schema.

![](../images/user-guide/profiles-union-schema.png)

## Passaggi successivi

Leggendo questa guida, ora sai come visualizzare e gestire i dati del tuo profilo utilizzando l’interfaccia utente della piattaforma Experience. Per informazioni su come sfruttare i dati del profilo cliente in tempo reale per generare segmenti di pubblico, consulta la documentazione [sulla](../../segmentation/home.md)segmentazione.