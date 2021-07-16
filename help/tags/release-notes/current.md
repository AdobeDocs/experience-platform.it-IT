---
title: Note sulla versione
description: Note aggiornate sulla versione dei tag in Adobe Experience Platform.
source-git-commit: 7a6bec77895458cf1735bc7a00d16b78df9776a5
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 67%

---

# Note sulla versione

>[!NOTE]
>
>Con il suo rebranding, Adobe Experience Platform Launch viene riproposto come una suite di tecnologie per la raccolta dati all’interno di Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

## 17 maggio 2021

**Gestione migliore delle modifiche non salvate**: in passato, quando ci si allontanava da una vista delle impostazioni (estensioni, elementi dati e componenti regola) veniva richiesto se si desiderasse ignorare le modifiche. Tuttavia, la logica per determinare questa situazione non era molto efficiente e spesso veniva chiesto di salvare i cambiamenti anche se non ce n’erano. Questo problema è stato corretto. Da ora in poi, il messaggio dovrebbe comparire solo se sono state effettivamente apportate delle modifiche.

## 10 maggio 2021

**Pubblicazione semplificata**: non è più necessario creare nell’ambiente di staging. Se disponi dei diritti appropriati, puoi saltare completamente lo stato Inviato e pubblicare direttamente dall’ambiente Sviluppo, purché la build sia stata compilata correttamente e non siano presenti altre librerie a monte.

## 22 aprile 2021

**Raccolta dati in Adobe Experience Platform** : l&#39;invio di dati ad Adobe non riguarda solo la distribuzione di tag sul sito o la configurazione nell&#39;app.  L’utilizzo degli SDK per Experience Platform e della rete Edge richiede l’accesso ad altre funzionalità di Platform. Questo richiedeva l’accesso ad alcuni strumenti diversi, che ora sono tutti disponibili in un unico posto.

La raccolta dati in Platform è composta da sei funzionalità e la navigazione semplificata di recente conterrà solo gli elementi a cui la tua azienda e il tuo account utente hanno accesso.  Alcuni dei nomi delle funzionalità sono stati aggiornati per corrispondere ai pattern di denominazione di Experience Platform.

* Client (precedentemente disponibile come Client Side)
* Datastream (precedentemente disponibili come Configurazioni Edge)
* Server (precedentemente disponile come Server Side)
* Configurazioni app
* Schemi
* Identità

Man mano che Experience Platform e la funzionalità di raccolta dati continuano a evolvere, verranno rilasciati ulteriori aggiornamenti.

## 18 febbraio 2021

* Aggiornamento dell’interfaccia utente per la raccolta dei dati per react-spettro v3
* Schede di estensione aggiornate ai pattern Spectrum più recenti
* Sono state aumentate le dimensioni dei campi nome in tutta l’app.

## 13 gennaio 2021

**Disponibilità generale: Event** ForwardingInvia dati a livello di evento a Adobe Experience Platform Edge Network e quindi utilizza l’inoltro eventi per trasformare, arricchire e inviare tali dati a un endpoint non Adobe utilizzando i server di Adobe, non il client, con latenza bassa.

Per ulteriori informazioni, consulta la [panoramica sull’inoltro eventi](../ui/event-forwarding/overview.md) e la [guida introduttiva](../ui/event-forwarding/getting-started.md) .
