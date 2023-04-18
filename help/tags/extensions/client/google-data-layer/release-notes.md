---
title: Note sulla versione dell’estensione Google Data Layer
description: Note aggiornate sulla versione dell’estensione tag Google Data Layer in Adobe Experience Platform.
exl-id: 740b6e3a-d469-475d-9523-03b0b48b11c8
source-git-commit: 0b9fa104777f21fc9bc893784ae3155d887a48d2
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 1%

---

# Note sulla versione dell’estensione Google Data Layer

## Versione 1.0.4

* Versione beta pubblica dell’estensione.

## Versione 1.0.6

* Aggiunta di un’azione per reimpostare il livello dati sullo stato calcolato.
* Correggere i bug negli elementi dati che impediscono il recupero dei valori dallo stato calcolato.

## Versione 1.1.1

Un miglioramento significativo e la versione della correzione dei bug derivanti dal feedback del beta testing.

* È stato risolto un problema in cui un elemento dati Google Data Layer Extension vuoto utilizzato in una regola di livello non dati (ad esempio Library Loaded) restituiva l’oggetto livello dati, non lo stato calcolato.
* Corregge un problema in cui lo stato calcolato del livello dati non veniva passato dall’helper negli eventi al momento dell’attivazione dell’evento, ma al momento dell’esecuzione della regola.
* Aggiunge un interruttore alla finestra di dialogo dell’elemento dati che consente all’utente di scegliere se restituire solo i valori degli eventi.
* È stato corretto un problema a causa del quale la cronologia degli eventi non veniva rilevata correttamente dagli ascoltatori di eventi regola.
* Miglioramenti minori alla chiarezza del codice.

## Versione 1.2.0

* Aggiunge un&#39;azione da inviare al livello dati utilizzando una finestra di dialogo a più campi chiave-valore.
* Corregge un bug che impediva il caricamento dell’estensione quando i tag venivano distribuiti in modo sincrono.
* Corregge un bug che causava un errore durante il salvataggio di un elemento dati in alcune circostanze.
* Aggiunge la documentazione alla finestra di dialogo dell&#39;evento che spiega l&#39;utilizzo dell&#39;oggetto evento Tags.
* Aggiunge un avviso sui cicli infiniti alla finestra di dialogo dell’evento.
