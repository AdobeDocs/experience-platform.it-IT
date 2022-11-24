---
title: Note sulla versione per l’estensione Adobe Client Data Layer
description: Note aggiornate sulla versione dell’estensione per tag Adobe Client Data Layer in Adobe Experience Platform.
exl-id: 8fa3a210-6c85-4162-84cf-15c6e3cfcb9e
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 100%

---

# Note sulla versione dell’estensione Adobe Client Data Layer

## Versione 2.0.2

* Caricamento della libreria principale ACDL (versione 2.0.2)
* Nella versione 2.0.0 della libreria principale ACDL è stata rimossa la possibilità di sfruttare event.beforeState e event.afterState. Pertanto, questi oggetti sono stati modificati per restituire sempre oggetti vuoti. Le implementazioni che si basano su questa funzionalità dovranno essere aggiornate al momento del passaggio a questa versione.

## Versione 1.1.3

* Caricamento della libreria principale ACDL (versione 1.1.3)

## Versione 1.1.2

La versione iniziale dell’estensione fornisce le seguenti funzionalità:

* Caricamento della libreria principale ACDL (versione 1.1.1)
* Ridenominazione del livello dati Adobe
* Eventi:
   * Ascolto di tutti gli eventi
   * Ascolto di tutti i dati inviati
   * Ascolto di un evento specifico inviato
   * Tutti gli eventi possono essere ascoltati su diversi ambiti
* Elementi dati:
   * Stato calcolato: stato globale o specifico
   * Dimensioni livello dati
* Azioni:
   * Reimposta la dimensione del livello dati (mantenendo l’ultimo stato calcolato)
   * Invio di un oggetto al livello dati
