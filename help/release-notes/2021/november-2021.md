---
title: Note sulla versione di Adobe Experience Platform di novembre 2021
description: Note sulla versione di Adobe Experience Platform di novembre 2021.
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 23%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: giovedì 17 novembre 2021**

## Nuove funzioni

Nuove funzioni di Adobe Experience Platform:

- [Edizione B2B di Real-Time Customer Data Platform](#B2B)
- [(Beta) Attiva i segmenti di pubblico nelle destinazioni batch tramite l’API di attivazione ad hoc](#ad-hoc-activation)

## Aggiornamenti alle funzioni esistenti

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [IA per l’attribuzione](#attribution-ai)
- [IA per l’analisi dei clienti](#customer-ai)

### Edizione B2B di Real-Time Customer Data Platform {#B2B}

**Data di rilascio: sabato 12 novembre 2021**

L’Edizione B2B di Real-Time CDP, basata su Real-Time Customer Data Platform (Real-Time CDP), è creata appositamente per i marketer che operano in un modello di servizio business-to-business. Raccoglie dati da più origini e li combina in un’unica vista di persone e profili di account. Questi dati unificati consentono ai marketer di rivolgersi con precisione a tipi di pubblico specifici e di coinvolgerli in tutti i canali disponibili.

Sono state migliorate diverse funzionalità di Adobe Experience Platform che distinguono Real-Time CDP B2B edition dalla controparte B2C. Includono miglioramenti all’Experience Data Model (XDM) per i casi d’uso B2B, aggiornamenti alla risoluzione delle identità e alla segmentazione dei profili, nonché un connettore e una destinazione personalizzati per Marketo Engage. Il connettore Marketo consente ai brand B2B di collegare i dati del loro coinvolgimento B2B leader del settore con informazioni comportamentali per sviluppare lead e migliorare le operazioni di marketing basate sull’account.

-[Nuove edizioni B2B e B2P](#editions)
-[Nuovi connettori di origine dati e di destinazione di Marketo](#marketo)
-[XDM B2B standard](#XDM)

### Nuove edizioni B2B e B2P {#editions}

Sono disponibili per l’acquisto nuove edizioni B2B e B2P che aggiungono dati e funzionalità B2B sia ai prodotti Real-Time CDP che Experience Platform Activation.

Per ulteriori informazioni su Real-Time CDP B2B edition, consulta la [panoramica](../../rtcdp/overview.md).

### Nuovi connettori di origine dati e destinazione di Marketo {#marketo}

Nuovi connettori di origine dati e di destinazione di Marketo inviano i dati di Marketo ai tipi di pubblico di Experience Platform e Experience Platform di nuovo a Marketo. Disponibile per tutti gli utenti di Experience Platform.

| Funzione | Descrizione |
|----------|-------------|
| Connettore sorgente Marketo Engage | Il [connettore di origine Marketo Engage](../../sources/connectors/adobe-applications/marketo/marketo.md) consente agli addetti al marketing di acquisire facilmente i dati da una o più istanze Marketo nella propria istanza Adobe Experience Platform e fornisce una soluzione completa per la gestione dei lead e gli addetti al marketing B2B. |
| Destinazione Marketo Engage | La [destinazione Marketo](../../destinations/catalog/adobe/marketo-engage.md) consente agli addetti al marketing di inviare i segmenti creati in Adobe Experience Platform a Marketo, dove verranno visualizzati come elenchi statici. |

### XDM B2B standard {#XDM}

Classi XDM B2B standard, gruppi di campi e tipi di dati sono disponibili per tutti gli utenti di Experience Platform.

| Funzione | Descrizione |
|-----------|--------------|
| Classi XDM B2B standard | Real-Time Customer Data Platform B2B edition fornisce diversi XDM standard che acquisiscono dettagli sulle entità di dati B2B essenziali, come account, opportunità, campagne e altro ancora. |

Per ulteriori informazioni sull&#39;acquisizione di entità dati B2B, consulta la documentazione sugli [schemi in Real-Time Customer Data Platform B2B edition](../../rtcdp/schemas/b2b.md).

### (Beta) Attiva i segmenti di pubblico nelle destinazioni batch tramite l’API di attivazione ad hoc {#ad-hoc-activation}

L’API di attivazione ad hoc consente agli addetti al marketing di attivare in modo programmatico i segmenti di pubblico nelle destinazioni, in modo rapido ed efficiente, per le situazioni in cui è richiesta l’attivazione immediata. L&#39;attivazione di un pubblico ad hoc è supportata solo da [destinazioni basate su file batch](../../destinations/destination-types.md#file-based) ed è attualmente in versione beta. Per ulteriori informazioni, consulta la [documentazione dell&#39;API di attivazione ad hoc](../../destinations/api/ad-hoc-activation-api.md).

### IA per l’attribuzione {#attribution-ai}

Attribution AI viene utilizzato per attribuire il merito ai punti di contatto da cui derivano gli eventi di conversione. Può essere utilizzata dai marketer per quantificare l’impatto di ogni punto di contatto di marketing lungo i percorsi della clientela.

| Funzione | Descrizione |
|-----------|---------------|
| Supporto per più set di dati | IA per l’attribuzione può ora acquisire facilmente più set di dati direttamente nell’interfaccia utente senza la necessità di mappare e unire ogni set di dati. Questa nuova funzionalità per risparmiare tempo fornisce punteggi più potenti e precisi con dati più ricchi da più set di dati. |
| Mappatura del canale multimediale e del campo della campagna | IA per l’attribuzione ora supporta la mappatura dei campi del canale multimediale e della campagna. La mappatura dei canali multimediali tra set di dati migliora le informazioni derivate da IA per l’attribuzione e consente di fornire risultati più chiari e facili da interpretare. |

Per ulteriori informazioni su IA per l&#39;attribuzione, consulta la [documentazione di IA per l&#39;attribuzione](../../intelligent-services/attribution-ai/overview.md).

### IA per l’analisi dei clienti {#customer-ai}

IA per l’analisi dei clienti disponibile in Real-Time Customer Data Platform, viene utilizzato per generare punteggi di propensione personalizzati, come abbandono e conversione per singoli profili su larga scala. Per poter usufruire di queste funzioni non occorre trasformare le esigenze aziendali in problematiche di apprendimento automatico né scegliere un algoritmo, e non sono richieste formazione o implementazioni specifiche.

**Funzioni aggiornate**

| Funzione | Descrizione |
|-----------|-------------|
| Supporto per più set di dati | IA per l’analisi dei clienti può ora acquisire facilmente più set di dati direttamente nell’interfaccia utente senza la necessità di mappare e unire ogni set di dati. Questa nuova funzionalità per risparmiare tempo fornisce punteggi più potenti e precisi con dati più ricchi da più set di dati. |
| Attributi di profilo personalizzati | IA per l’analisi dei clienti ora supporta la definizione di campi set di dati di profilo personalizzati (con marche temporali) nei dati, oltre ai campi evento standard. L’utilizzo di questa opzione consente di aggiungere attributi di profilo aggiuntivi che ritieni influenti, il che può migliorare la qualità del modello e fornire risultati più precisi. |

Per ulteriori informazioni su Customer AI, consulta la [documentazione di Customer AI](../../intelligent-services/customer-ai/overview.md).
