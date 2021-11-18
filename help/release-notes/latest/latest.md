---
title: Note sulla versione di Adobe Experience Platform
description: Note aggiornate sulla versione di Adobe Experience Platform.
source-git-commit: aa8cafc9a40748eda3098b2af732a828d39204b2
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 15%

---

# Note sulla versione di Adobe Experience Platform

**Data di rilascio: 17 novembre 2021**

## Nuove funzionalità

Nuove funzioni in Adobe Experience Platform:

- [Edizione B2B di Real-time Customer Data Platform](#B2B)

## Aggiornamenti alle funzioni esistenti

Aggiornamenti alle funzioni esistenti in Adobe Experience Platform:

- [Attribution AI](#attribution-ai)
- [Customer AI](#customer-ai)

### Edizione B2B di Real-time Customer Data Platform {#B2B}

**Data di rilascio: 12 novembre 2021**

Basato su Real-time Customer Data Platform (Real-time CDP), Real-time CDP B2B Edition è progettato appositamente per gli esperti di marketing che operano in un modello di servizio business-to-business. Riunisce i dati provenienti da più sorgenti e li combina in un’unica vista di persone e profili di account. Questi dati unificati consentono agli esperti di marketing di eseguire il targeting preciso di tipi di pubblico specifici e coinvolgerli in tutti i canali disponibili.

Sono stati apportati miglioramenti a una varietà di funzionalità di Adobe Experience Platform che distinguono Real-time CDP B2B Edition dalla sua controparte B2C. Includono miglioramenti a Experience Data Model (XDM) per casi d’uso B2B, aggiornamenti alla risoluzione delle identità e alla segmentazione del profilo, nonché un connettore e una destinazione personalizzati per il Marketo Engage. Il connettore Marketo consente ai brand B2B di collegare i propri dati di coinvolgimento B2B leader del settore con informazioni comportamentali al fine di generare lead e migliorare le operazioni di marketing basate sull’account.

-[Nuove edizioni B2B e B2P](#editions)
-[Nuovi connettori di origine dati e destinazione Marketo](#marketo)
-[XDM standard B2B](#XDM)

### Nuove edizioni B2B e B2P {#editions}

Sono acquistabili nuove edizioni B2B e B2P che apportano dati e funzionalità B2B sia ai prodotti Real-time CDP che a Platform Activation.

Per ulteriori informazioni su Real-time CDP B2B Edition, consulta la sezione [panoramica](../../rtcdp/overview.md).

### Nuovi connettori di origine dati e destinazione Marketo {#marketo}

I nuovi connettori di origine dati e destinazione Marketo inviano i dati di Marketo ai tipi di pubblico di Platform e Platform a Marketo. Disponibile per tutti gli utenti di Platform.

| Funzione | Descrizione |
|----------|-------------|
| Connettore di origine del Marketo Engage | La [Connettore di origine del Marketo Engage](../../sources/connectors/adobe-applications/marketo/marketo.md) consente agli addetti al marketing di inserire facilmente i dati da una o più istanze Marketo nella loro istanza Adobe Experience Platform e fornisce una soluzione completa per la gestione dei lead e per gli esperti di marketing B2B. |
| Destinazione Marketo Engage | La [Destinazione Marketo](../../destinations/catalog/adobe/marketo-engage.md) consente agli addetti al marketing di inviare in Marketo i segmenti creati in Adobe Experience Platform, dove verranno visualizzati come elenchi statici. |

### XDM standard B2B {#XDM}

Le classi, i gruppi di campi e i tipi di dati XDM standard B2B sono disponibili per tutti gli utenti di Platform.

| Funzione | Descrizione |
|-----------|--------------|
| Classi XDM standard B2B | Real-time Customer Data Platform B2B Edition fornisce diversi XDM standard che acquisiscono dettagli su entità di dati B2B essenziali, come account, opportunità, campagne e altro ancora. |

Consulta la sezione [Schemi in Real-time Customer Data Platform B2B Edition](../../rtcdp/schemas/b2b.md) documentazione per ulteriori informazioni sull’acquisizione di entità dati B2B.

### Attribution AI {#attribution-ai}

Attribution AI viene utilizzato per attribuire il merito ai punti di contatto da cui derivano gli eventi di conversione. Può essere utilizzato dagli addetti al marketing per quantificare l’impatto di ogni punto di contatto marketing lungo i percorsi dei clienti.

| Funzione | Descrizione |
|-----------|---------------|
| Supporto per più set di dati | Attribution AI ora può facilmente acquisire più set di dati direttamente nell’interfaccia utente senza la necessità di mappare e unire ogni set di dati. Questa nuova funzionalità consente di risparmiare tempo e fornisce punteggi più potenti e precisi con dati più ricchi provenienti da più set di dati. |
| Mappatura del campo del canale multimediale e della campagna | Attribution AI supporta ora la mappatura dei campi del canale multimediale e della campagna. La mappatura dei canali multimediali tra set di dati migliora le informazioni derivate da Attribution AI e consente di ottenere risultati più chiari e facili da interpretare. |

Per ulteriori informazioni sulle Attribution AI, consulta la sezione [Documentazione di Attribution AI](../../intelligent-services/attribution-ai/overview.md).

### Customer AI {#customer-ai}

Customer AI disponibile in Real-time Customer Data Platform, viene utilizzato per generare punteggi di propensione personalizzati, come abbandono e conversione per singoli profili su scala. Per poter usufruire di queste funzioni non occorre trasformare le esigenze aziendali in problematiche di machine learning né scegliere un algoritmo, e non sono richieste formazione o implementazioni specifiche.

**Funzioni aggiornate**

| Funzione | Descrizione |
|-----------|-------------|
| Supporto per più set di dati | Customer AI ora può facilmente acquisire più set di dati direttamente nell’interfaccia utente senza la necessità di mappare e unire ogni set di dati. Questa nuova funzionalità consente di risparmiare tempo e fornisce punteggi più potenti e precisi con dati più ricchi provenienti da più set di dati. |
| Attributi di profilo personalizzati | Customer AI supporta ora la definizione di campi di set di dati di profilo personalizzati (con marche temporali) nei dati, oltre ai campi evento standard. L’utilizzo di questa opzione consente di aggiungere attributi di profilo aggiuntivi che ritieni influenti e che possono migliorare la qualità del modello e fornire risultati più precisi. |

Per ulteriori informazioni su Customer AI, consulta la sezione [Documentazione di Customer AI](../../intelligent-services/customer-ai/overview.md).
