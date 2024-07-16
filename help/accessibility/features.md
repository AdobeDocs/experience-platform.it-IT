---
keywords: Experience Platform;profilo;profilo cliente in tempo reale;risoluzione dei problemi;API;profilo unificato;Profilo unificato;unificato;Profilo;rtcp;XDM
title: Funzioni generali di accessibilità in Platform
type: Documentation
description: Scopri le funzioni generali di accessibilità supportate da Adobe Experience Platform, tra cui navigazione da tastiera, palette di colori e contrasto e supporto per la tecnologia di assistenza.
exl-id: 4b7e2f2b-af51-4376-8a63-16c921cc7135
source-git-commit: 7b197f253aa5ce04a682040814cf749407154ebc
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 0%

---

# Funzioni di accessibilità in Experience Platform

Adobe Experience Platform si impegna a fornire funzionalità accessibili e inclusive a tutti i singoli utenti, inclusi gli utenti che utilizzano dispositivi di assistenza come il software di riconoscimento vocale e gli assistenti vocali. Questo documento illustra le funzioni generali di accessibilità supportate da Platform, tra cui la navigazione da tastiera, la struttura semantica, un contrasto sufficiente tra elementi in primo piano ed elementi in background e il supporto per le tecnologie per l’accessibilità.

## Tecnologie assistive

Gli utenti con disabilità si affidano spesso a hardware e software, noti come tecnologie assistive, per accedere ai contenuti digitali e utilizzare prodotti software. Adobe Experience Platform supporta diversi tipi di tecnologie per l’accessibilità (AT), ad esempio utilità per la lettura dello schermo, software di zoom e riconoscimento vocale, seguendo le best practice per l’accessibilità, ad esempio utilizzando codice semantico, equivalenti testuali, etichette e ARIA dove necessario. Gli elementi interattivi nell’interfaccia utente di Experience Platform utilizzano etichette, nomi accessibili e ruoli corrispondenti che identificano sia lo scopo che lo stato corrente. In questo modo le tecnologie per l’accessibilità, come gli assistenti vocali, possono leggere le etichette e altre informazioni per consentire agli utenti di interagire facilmente con i controlli dell’applicazione.

## Accessibilità da tastiera

Experience Platform si impegna a supportare l’accessibilità completa da tastiera.

I seguenti elementi di navigazione facilitano l’accessibilità:
* Il tasto TAB consente di spostarsi tra gli elementi dell’interfaccia utente, le sezioni e i gruppi di menu.
* I tasti freccia si spostano all&#39;interno dei gruppi di menu per impostare lo stato attivo sui singoli elementi attivi.
* Maiusc + Tab si sposta all&#39;indietro nell&#39;ordine di tabulazione.
* I tasti Invio e Barra spaziatrice attivano gli elementi selezionati.
* Il tasto Esc funge da pulsante di annullamento per chiudere una finestra di dialogo, se presente.
* In Experience Platform, attorno a un elemento selezionato viene visualizzato un bordo blu con un’indicazione chiara dell’elemento dell’interfaccia attualmente attivo.

![Un bordo blu visualizzato intorno a un elemento selezionato per indicare che lo stato attivo è applicato.](images/profile-overview-tab.png)

## Palette di colori e contrasto

Experience Platform si impegna per garantire la conformità a [WCAG 2.1 AA](https://www.w3.org/TR/WCAG/), inclusi i requisiti per il contrasto del colore. L’interfaccia utente di Experience Platform fornisce un contrasto sufficiente nell’applicazione per garantire un’esperienza di visualizzazione accessibile agli utenti ipovedenti o con deficienze cromatiche.

![La palette di colori e il contrasto presenti nella home page dell&#39;interfaccia utente di Experience Platform.](images/homepage.png)

## Convalida campo obbligatoria

Quando si aggiungono dati, si creano schemi o si definiscono segmenti, i campi obbligatori vengono indicati sia visivamente, utilizzando un asterisco accanto all’etichetta di testo di un campo, sia a livello di programmazione. Questi campi attivano la convalida quando si immettono dati non validi nei campi e al momento del salvataggio. Se un campo obbligatorio non supera la convalida, viene evidenziato in rosso con un’icona di errore e viene visualizzata anche una descrizione scritta del problema da risolvere.

![Chiusura di un campo obbligatorio non convalidato. Il campo viene visualizzato in rosso ed è presente un&#39;icona di errore.](images/field-validation.png)
