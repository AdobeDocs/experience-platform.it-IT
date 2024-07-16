---
title: Note sulla versione dell’estensione Adobe Target
description: Note aggiornate sulla versione dell’estensione tag Adobe Target in Adobe Experience Platform.
exl-id: ba29f614-c3cd-4e0b-b043-2b1c17567def
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 94%

---

# Note sulla versione di Adobe Target

>[!NOTE]
>
>Adobe Experience Platform Launch è stato ridefinito come suite di tecnologie di raccolta dati in Adobe Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

## 16 settembre 2021

### Estensione Adobe Target 0.11.4

* Aggiornato a at.js v1.8.3
* Sono stati aggiunti gli attributi `SameSite=None` e `Secure` durante l&#39;impostazione dei cookie

## 24 luglio 2020

### Estensione Adobe Target 0.11.3

* È stato corretto un bug a causa del quale l’estensione non riusciva se uno script o un codice aggiungeva una proprietà `default` a `window` o `document`

## 15 giugno 2020

### Estensione Adobe Target 0.11.2

* È stato risolto un problema che si verificava durante l’utilizzo di CNAME e Edge override, a causa del quale at.js 1.x poteva creare il dominio del server in modo incorretto e la richiesta Target non riusciva

## 25 marzo 2020

### Estensione Adobe Target 0.11.1

* at.js è stato aggiornato a v1.8.1.
* È stato risolto un problema che impediva l’elaborazione corretta dei parametri e dei parametri di caricamento delle pagine.

## 10 ottobre 2019

### Estensione Adobe Target 0.11.0

* Aggiornato at.js a v1.8.
* Migliorate le prestazioni per le integrazioni tra la libreria Experience Cloud ID (ECID) v4.4 e at.js 1.8.
* In precedenza, la libreria ECID effettuava due chiamate di blocco prima che at.js potesse riportare le esperienze. Ora effettua una sola chiamata, migliorando notevolmente le prestazioni.

>[!NOTE]
>Aggiorna l’estensione tag ECID per Adobe Experience Platform alla versione 4.4.1 per approfittare di questo miglioramento delle prestazioni.

## 31 luglio 2019

### Estensione Adobe Target 0.10.1

* Hotfix per i parametri che gestiscono l’estensione tag per Adobe Target

## 4 maggio 2019

### Estensione Adobe Target 0.10.0

* Risoluzione di un problema di elementi dati causato dalle modifiche più recenti di Google Chrome.

## 14 marzo 2019

### Estensione Adobe Target 0.9.3

* Versione aggiornata dell&#39;estensione da utilizzare at.js 1.7.1.

## 20 febbraio 2019

### Estensione Adobe Target 0.9.2

* Correzione delle race condition tra le estensioni di Target e Analytics.

## 12 febbraio 2019

### Estensione Adobe Target 0.9.1

#### **Funzioni**

* Aggiornamento dell’estensione per l’utilizzo di at.js 1.7.0 con funzionalità di consenso alla privacy supportata tramite tag per controllare come e quando viene attivato il tag Target. Consulta la documentazione sui tag per scoprire come impostare l’implementazione del consenso. Possibilità di personalizzare se un parametro mbox con un valore vuoto deve essere inviato a Target o no.

## 23 gennaio 2019

### Estensione Adobe Target 0.8.4

* Aggiornamento at.js alla versione 1.6.4.
* Migrazione dell&#39;interfaccia utente dell&#39;estensione in Adobe Spectrum.

## 15 novembre 2018

### Estensione Adobe Target 0.8.2

* Aggiornamento at.js alla versione 1.6.3.

## 24 ottobre 2018

### Estensione Adobe Target 0.8.1

* Aggiornamento at.js alla versione 1.6.2.

## 23 agosto 2018

### Estensione Adobe Target 0.8.0

* Aggiornamento at.js alla versione 1.6.0.

## 10 agosto 2018

### Estensione Adobe Target 0.7.2

* Modifiche minori
* Aggiornamento della proprietà `exchangeUrl` nel file `extension.json`.

## 1 agosto 2018

### Estensione Adobe Target 0.7.1

* Correzioni minori.

## 18 giugno 2018

### Estensione Adobe Target 0.7.0

* Aggiornamento at.js alla versione 1.5.0.
* Risoluzione di un problema per cui Media Optimizer restituiva un errore di riferimento Null in IE 11.

## 15 giugno 2018

### Estensione Adobe Target 0.6.0

#### **Funzioni**

* Estensione Target è stato aggiornato per utilizzare at.js v1.3.1. Quando distribuisci Target con Analytics, attendi che tutte le chiamate di Target siano risolte (comprese le offerte di reindirizzamento) prima che Analytics venga attivato, risolvendo la race condition precedente.

## 22 febbraio 2018

### Estensione Adobe Target 0.4.1

#### **Funzioni**

* Aggiunto l&#39;elenco Adobe Exchange a extension.json.
* Aggiunte verifiche per controllare se Target è disabilitato e se Authoring è abilitato.

#### **Correzioni di bug**

* È stato risolto un errore nell’estensione Adobe Target che impediva al compositore esperienze visivo di rendere visibile una pagina nascosta nel caso di implementazione tramite tag.

## 8 febbraio 2018

### Estensione Adobe Target 0.4.0

#### **Funzioni**

* Visualizzazioni aggiornate nelle schermate di configurazione dell&#39;estensione.
* at.js è stato aggiornato alla versione 1.2.3 (aggiunge il supporto per le offerte JSON).
