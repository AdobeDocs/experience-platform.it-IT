---
title: Note sulla versione di Adobe Experience Platform, novembre 2021
description: Note sulla versione di novembre 2021 per Adobe Experience Platform.
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 12%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 17 novembre 2021**

## Nuove funzionalità

Nuove funzioni di Adobe Experience Platform:

- [Edizione B2B di Real-Time Customer Data Platform](#B2B)
- [(Beta) Attiva i segmenti di pubblico in destinazioni batch tramite l’API di attivazione ad hoc](#ad-hoc-activation)

## Aggiornamenti alle funzioni esistenti

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [IA per l’attribuzione](#attribution-ai)
- [IA per l’analisi dei clienti](#customer-ai)

### Edizione B2B di Real-Time Customer Data Platform {#B2B}

**Data di rilascio: 12 novembre 2021**

Basata su Real-time Customer Data Platform (Real-Time CDP), Real-Time CDP B2B Edition è progettata appositamente per gli esperti di marketing che operano in un modello di servizio business-to-business. Raccoglie dati da più origini e li combina in un’unica vista di persone e profili di account. Questi dati unificati consentono agli addetti al marketing di rivolgersi con precisione a tipi di pubblico specifici e di coinvolgerli in tutti i canali disponibili.

Sono stati apportati miglioramenti a diverse funzionalità di Adobe Experience Platform che distinguono Real-Time CDP B2B Edition dalla sua controparte B2C. Includono miglioramenti all’Experience Data Model (XDM) per i casi d’uso B2B, aggiornamenti alla risoluzione delle identità e alla segmentazione dei profili, nonché un connettore e una destinazione personalizzati per il Marketo Engage. Il connettore Marketo consente ai brand B2B di collegare i dati del loro coinvolgimento B2B leader del settore con informazioni comportamentali per sviluppare lead e migliorare le operazioni di marketing basate sull’account.

-[Nuove edizioni B2B e B2P](#editions)
-[Nuovi connettori di origine dati e destinazione di Marketo](#marketo)
-[XDM B2B standard](#XDM)

### Nuove edizioni B2B e B2P {#editions}

Sono disponibili per l’acquisto nuove edizioni B2B e B2P che forniscono dati e funzionalità B2B sia ai prodotti Real-Time CDP che Platform Activation.

Per ulteriori informazioni sulla versione B2B di Real-Time CDP, consulta [panoramica](../../rtcdp/overview.md).

### Nuovi connettori di origine dati e destinazione di Marketo {#marketo}

Nuovi connettori di origine dati e di destinazione di Marketo inviano i dati di Marketo in streaming ai tipi di pubblico di Platform e Platform a Marketo. Disponibile per tutti gli utenti di Platform.

| Funzione | Descrizione |
|----------|-------------|
| Connettore sorgente Marketo Engage | Il [Connettore sorgente Marketo Engage](../../sources/connectors/adobe-applications/marketo/marketo.md) consente agli addetti al marketing di acquisire facilmente i dati da una o più istanze Marketo nella propria istanza Adobe Experience Platform e fornisce una soluzione completa per la gestione dei lead e gli addetti al marketing B2B. |
| Destinazione Marketo Engage | Il [Destinazione Marketo](../../destinations/catalog/adobe/marketo-engage.md) consente agli addetti al marketing di inviare i segmenti creati in Adobe Experience Platform a Marketo, dove verranno visualizzati come elenchi statici. |

### XDM B2B standard {#XDM}

Classi XDM B2B standard, gruppi di campi e tipi di dati sono disponibili per tutti gli utenti di Platform.

| Funzione | Descrizione |
|-----------|--------------|
| Classi XDM B2B standard | Real-time Customer Data Platform B2B Edition fornisce diversi XDM standard che acquisiscono dettagli sulle entità di dati B2B essenziali, come account, opportunità, campagne e altro ancora. |

Consulta la [Schemi in Real-time Customer Data Platform B2B Edition](../../rtcdp/schemas/b2b.md) per ulteriori informazioni sull’acquisizione di entità dati B2B.

### (Beta) Attiva i segmenti di pubblico in destinazioni batch tramite l’API di attivazione ad hoc {#ad-hoc-activation}

L’API di attivazione ad hoc consente agli addetti al marketing di attivare in modo programmatico i segmenti di pubblico nelle destinazioni, in modo rapido ed efficiente, per le situazioni in cui è richiesta l’attivazione immediata. L’attivazione ad hoc del pubblico è supportata solo da [destinazioni basate su file batch](../../destinations/destination-types.md#file-based) ed è attualmente in versione beta. Per ulteriori informazioni, vedere [documentazione API di attivazione ad hoc](../../destinations/api/ad-hoc-activation-api.md).

### IA per l’attribuzione {#attribution-ai}

Attribution AI viene utilizzato per attribuire il merito ai punti di contatto da cui derivano gli eventi di conversione. Può essere utilizzato dagli addetti al marketing per quantificare l’impatto di ogni punto di contatto marketing lungo i percorsi dei clienti.

| Funzione | Descrizione |
|-----------|---------------|
| Supporto per più set di dati | Attribution AI ora può acquisire facilmente più set di dati direttamente nell’interfaccia utente senza la necessità di mappare e unire ogni set di dati. Questa nuova funzionalità per risparmiare tempo fornisce punteggi più potenti e precisi con dati più ricchi da più set di dati. |
| Mappatura del canale multimediale e del campo della campagna | Attribution AI ora supporta la mappatura dei campi del canale multimediale e della campagna. La mappatura dei canali multimediali tra set di dati migliora le informazioni derivate da Attribution AI e fornisce risultati più chiari e facili da interpretare. |

Per ulteriori informazioni sull&#39;Attribution AI, vedere [Documentazione di Attribution AI](../../intelligent-services/attribution-ai/overview.md).

### IA per l’analisi dei clienti {#customer-ai}

IA per l’analisi dei clienti disponibile in Real-time Customer Data Platform, viene utilizzato per generare punteggi di propensione personalizzati, come abbandono e conversione per singoli profili su larga scala. Per poter usufruire di queste funzioni non occorre trasformare le esigenze aziendali in problematiche di machine learning né scegliere un algoritmo, e non sono richieste formazione o implementazioni specifiche.

**Funzioni aggiornate**

| Funzione | Descrizione |
|-----------|-------------|
| Supporto per più set di dati | IA per l’analisi dei clienti può ora acquisire facilmente più set di dati direttamente nell’interfaccia utente senza la necessità di mappare e unire ogni set di dati. Questa nuova funzionalità per risparmiare tempo fornisce punteggi più potenti e precisi con dati più ricchi da più set di dati. |
| Attributi di profilo personalizzati | IA per l’analisi dei clienti ora supporta la definizione di campi set di dati di profilo personalizzati (con marche temporali) nei dati, oltre ai campi evento standard. L’utilizzo di questa opzione consente di aggiungere attributi di profilo aggiuntivi che ritieni influenti, il che può migliorare la qualità del modello e fornire risultati più precisi. |

Per ulteriori informazioni su Customer AI, consulta la sezione [Documentazione di Customer AI](../../intelligent-services/customer-ai/overview.md).
