---
title: Note sulla versione di Google Data Layer
description: Note aggiornate sulla versione dell’estensione tag Google Data Layer in Adobe Experience Platform.
exl-id: 740b6e3a-d469-475d-9523-03b0b48b11c8
source-git-commit: c1bad7d5414e62f4d77f7d5903f4b2bf4d9081f8
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 5%

---

# Note sulla versione dell’estensione Google Data Layer

## Versione 1.0.4

* Versione beta pubblica dell’estensione.

## Versione 1.0.6

* Aggiunta di azione per ripristinare lo stato calcolato del livello dati.
* Correggi i bug nell’elemento dati che impediscono il recupero di valori dallo stato calcolato.

## Versione 1.1.1

Un miglioramento significativo e una correzione di bug derivanti dal feedback del beta testing.

* È stato risolto un problema a causa del quale un elemento dati vuoto di Google Data Layer Extension, utilizzato in una regola non di livello dati (ad esempio Library Loaded), restituiva l’oggetto livello dati, non lo stato calcolato.
* È stato risolto un problema a causa del quale lo stato calcolato del livello dati non veniva trasmesso dall’helper negli eventi al momento dell’attivazione dell’evento, ma piuttosto al momento dell’esecuzione della regola.
* Aggiunge un interruttore alla finestra di dialogo dell’elemento dati che consente a un utente di scegliere se restituire solo i valori degli eventi.
* È stato risolto un problema a causa del quale la cronologia degli eventi non veniva rilevata correttamente dai listener di eventi delle regole.
* Miglioramenti minori alla chiarezza del codice.

## Versione 1.2.0

* Aggiunge un’azione da inviare al livello dati utilizzando una finestra di dialogo con più campi chiave-valore.
* È stato corretto un bug che impediva il caricamento dell’estensione quando i tag venivano distribuiti in modo sincrono.
* È stato corretto un bug che, in alcune circostanze, causava un errore durante il salvataggio di un elemento dati.
* Aggiunge documentazione alla finestra di dialogo dell&#39;evento che illustra l&#39;utilizzo dell&#39;oggetto evento Tag.
* Aggiunge un avviso relativo a cicli infiniti nella finestra di dialogo dell&#39;evento.

## Versione 1.2.2

* Aggiunge il supporto per gli eventi Google Analytics gtag().
