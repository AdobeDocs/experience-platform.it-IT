---
title: Note sulla versione per l’estensione Adobe Content Analytics
description: Note aggiornate sulla versione dell’estensione tag Content Analytics in Adobe Experience Platform.
exl-id: 37b34915-655b-40de-b17b-43028c579e37
source-git-commit: 77d19ab813f881cd3c48c27ed4a9ac02e268e23f
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 1%

---

# Note sulla versione dell’estensione Adobe Content Analytics

Di seguito è riportato un elenco delle note sulla versione dell’estensione tag Content Analytics.

| Versione | Data | Correzioni |
|---|---|---|
| 1.0.48 | 25 agosto 2025 | <ul><li>Aggiunge il supporto per il tracciamento delle risorse all&#39;interno degli elementi DOM shadow-root di un documento.</li></ul> |
| 1.0.47 | 23 luglio 2025 | <ul><li>È stato corretto un bug che si verificava quando le esperienze non erano abilitate, causando un errore nel controllo delle espressioni regolari per le esperienze. Questo problema impediva la raccolta dei dati di Content Analytics.</li><li>È stato risolto un problema con l’impostazione della lingua predefinita che impediva la visualizzazione dell’interfaccia utente Tag per alcuni utenti per i quali non era impostata la lingua primaria predefinita in Experience Cloud.</li></ul> |
| 1.0.46 | 18 giugno 2025 | <ul><li>È stata aggiunta una notifica popup durante il tentativo di salvataggio della configurazione dell’estensione, se non è presente un flusso di dati di produzione.</li><li>È stato temporaneamente risolto il problema di visibilità del payload Content Analytics, al suo posto, inserendo il contenuto del payload stratificato nella console.</li><li>È stato aggiunto il supporto per la localizzazione all’interfaccia utente dell’estensione.</li><li>È stato parzialmente risolto un problema CSS che causava una spaziatura aggiuntiva attorno al contenuto dell’interfaccia utente dell’estensione.</li></ul> |
| 1.0.45 | 14 aprile 2025 | <ul><li>Sono stati risolti diversi bug nelle impostazioni di configurazione relativi alla gestione degli eventi Content Analytics durante l’attesa degli eventi di visualizzazione della pagina. Per impostazione predefinita, Content Analytics ora attende di attivare gli eventi fino a quando non si verifica l’evento PRIMA visualizzazione pagina.</li></ul> |
| 1.0.44 | 31 marzo 2025 | <ul><li>Prima iterazione dell’integrazione AppMeasurement.</li><li>Questa versione non supporta ancora il filtraggio di richieste specifiche (ad esempio, visualizzazioni di pagina), ma questa funzionalità potrebbe essere aggiunta in un aggiornamento futuro. Attualmente utilizza la prima istanza di AppMeasurement trovata nella pagina.</li></ul> |
| 1.0.43 | 10 marzo 2025 | <ul><li>Versione iniziale dell’estensione.</li></ul> |
