---
title: Panoramica sui tag
description: I tag in Adobe Experience Platform costituiscono la soluzione Adobe di nuova generazione per la gestione dei tag. I tag offrono ai clienti un modo semplice di implementare e gestire tutti i tag di analisi, marketing e annunci pubblicitari necessari per fornire ai clienti esperienze personalizzate significative.
exl-id: 23d882a5-1ddd-404b-a7e9-3000f1804971
source-git-commit: 4f31c77fd3efe06797055ca04a30ae5ff4872b4e
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 96%

---

# Panoramica sui tag

>[!NOTE]
>
>Adobe Experience Platform Launch è stato classificato come una suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](./term-updates.md) come riferimento consolidato delle modifiche terminologiche.

I tag in Adobe Experience Platform costituiscono la soluzione Adobe di nuova generazione per la gestione dei tag. I tag offrono ai clienti un modo semplice di implementare e gestire tutti i tag di analisi, marketing e annunci pubblicitari necessari per fornire ai clienti esperienze personalizzate significative.

I tag permettono a chiunque di generare e mantenere le proprie integrazioni, o *estensioni*. Queste sono disponibili per i clienti [!DNL Adobe Experience Cloud] di in un&#39;esperienza di tipo app-store per velocizzarne l&#39;installazione, la configurazione e l&#39;implementazione dei tag.

I tag sono offerti ai clienti di [!DNL Adobe Experience Cloud] come funzionalità incluse a valore aggiunto.

## Vantaggi chiave {#key-benefits}

* Time-to-value più rapido.
* Dati affidabili grazie a operazioni di raccolta, organizzazione e consegna centralizzate mediante gli elementi dei dati.
* Esperienze coinvolgenti tramite l&#39;integrazione di dati e tecnologie di marketing mediante un modulo per la generazione di regole.

## Funzioni chiave {#key-features}

### Estensioni {#extensions}

Un’estensione è un pacchetto di codice (JavaScript, HTML e CSS) che estende le funzionalità dei tag. Puoi generare, gestire e aggiornare le integrazioni tramite un&#39;interfaccia praticamente self-service. Puoi considerare le estensioni come app da utilizzare per eseguire le attività.

### Catalogo delle estensioni {#extension-catalog}

Trova, configura e distribuisci strumenti di marketing e pubblicitari generati e mantenuti da fornitori di software indipendenti.

### Generatore di regole {#rule-builder}

Crea solide regole che combinano più eventi, in una specifica sequenza definita con logica if/then con condizioni ed eccezioni. Le regole forniscono opzioni per:

* Eventi
* Condizioni
* Eccezioni
* Azioni

Il generatore di regole include funzionalità di verifica degli errori ed evidenziazione della sintassi nel codice personalizzato in tempo reale.

Quando vengono soddisfatti i criteri e le condizioni descritti dalle regole, le azioni definite vengono eseguite in ordine.

### Elementi dati {#data-elements}

Puoi raccogliere, organizzare e distribuire i dati per diverse tecnologie per marketing e annunci pubblicitari basate sul Web.

### Pubblicazione Enterprise {#enterprise-publishing}

Il processo di pubblicazione permette ai team di pubblicare il codice nelle pagine. Diverse persone possono creare un’implementazione, approvarla e pubblicarla sulle tue pagine.

* Le modifiche al codice sono racchiuse nelle librerie da te definite.
* Puoi specificare dove e quando implementare il codice.
* Team differenti possono creare più librerie in parallelo.
* Non vi è alcun limite di ambiente di sviluppo.
* Si tratta di un processo intenzionale e basato su autorizzazioni per unire le librerie.

### API aperte {#open-apis}

Puoi automatizzare le implementazioni di singole tecnologie o di un gruppo di tecnologie.

* I tag interagiscono con l’API di Reactor.
* Le implementazioni possono essere automatizzate tramite API.
* È possibile integrare le API di con i propri sistemi interni.
* Puoi scegliere di creare un’interfaccia utente personalizzata.

### Tag contenitore leggero e modulare {#modular-tag}

Il contenuto del contenitore è ridotto al minimo, compreso il tuo codice personalizzato. Ogni caratteristica è modulare. Se non hai bisogno di un elemento, non verrà incluso nella libreria. Il risultato è un&#39;implementazione veloce e compatta. Consulta [Minification](./ui/publishing/builds.md).

## Altri punti di forza {#other-highlights}

I tag offrono diversi miglioramenti rispetto ad altri sistemi simili, tra cui:

* `document.write ()` non viene utilizzato dove non è consentito da Chrome.
* Le regole Page Top (Inizio pagina) e Page Bottom (Fine pagina) sono unite nella libreria principale per ridurre al minimo le chiamate HTTP.
* Gli script di azioni personalizzati di una regola possono essere caricati in parallelo, ma vengono eseguiti in sequenza.
* Se eviti le regole Page Top (Inizio pagina) e Page Bottom (Fine pagina), il codice è principalmente asincrono, con un percorso per ottenere la piena asincronia.
