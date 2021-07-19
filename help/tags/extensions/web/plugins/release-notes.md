---
title: Note sulla versione per l’estensione Common Analytics Plugins
description: Note aggiornate sulla versione dell’estensione tag Common Analytics Plugins in Adobe Experience Platform.
source-git-commit: cce218d984bae92428c7d48aefcd0f57dab837ea
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 92%

---

# Note sulla versione di Common Analytics Plugins

## 23 giugno 2021

### Estensione Common Analytics Plugins 3.0.6

#### Correzioni di bug

* È stato corretto un problema a causa del quale getPercentPageViewed si interrompeva quando si utilizzavano caratteri speciali

## 20 maggio 2021

### Estensione Common Analytics Plugins 3.0.5

#### Correzioni di bug

* È stato risolto un problema che impediva l’inizializzazione corretta di getTimeParting durante l’utilizzo dell’azione di inizializzazione generica.

## 26 marzo 2021

### Estensione Common Analytics Plugins 3.0.4

#### Correzioni di bug

* È stato risolto un problema a causa del quale getPageLoadTime impostava in modo errato le variabili sull&#39;oggetto finestra.
* È stato risolto un problema a causa del quale getQueryParam restituiva un valore non definito invece di &quot;&quot; se queryParam non era presente nella stringa di query.
* È stato risolto un problema che causava la visualizzazione di numeri di versione errati nell’azione di inizializzazione.

## 19 marzo 2021

### Estensione Common Analytics Plugins 3.0.2

#### Funzioni

* Sono stati aggiornamento di tutti i plug-in per includere automaticamente le informazioni sulla versione come dati contestuali.
* È stato aggiunto il plug-in getPercentPageViewed.
* Sono stati aggiunti degli elementi dati per i seguenti plug-in:
   * getGeoCoordinates
   * getNewRepeat
   * getPageName
   * getResponsiveLayout
   * getTimeParting
   * getTimeSinceLastVisit
   * getVisitDuration
   * getVisitNum
* Stili aggiornati

## 9 aprile 2020

### Estensione Common Analytics Plugins 2.2.0

#### Correzioni di bug

* È stata corretta la dicitura nelle visualizzazioni dell’estensione.

#### Funzioni

* È stata aggiornata la documentazione per l’azione di inizializzazione.

## 5 dicembre 2019

### Estensione Common Analytics Plugins 2.1.1

#### Correzioni di bug

* È stato risolto un problema che impediva la retrocompatibilità con le versioni 2.0.X.
* È stato risolto un problema di collegamenti alla documentazione con destinazione errata.
* È stato risolto un problema a causa del quale `getTimeSinceLastVisit` veniva visualizzato due volte nell’azione di inizializzazione.

## 15 novembre 2019

### Estensione Common Analytics Plugins 2.1.0

#### Correzioni di bug

* Sono state reintrodotte delle singole azioni plug-in per supportare la compatibilità con le versioni precedenti.
* È stato risolto un problema relativo al plug-in `cleanStr`.
* È stato risolto un problema relativo al plug-in `getResponsiveLayout`.
* È stato risolto un problema relativo al plug-in `getPageName`.

#### Funzioni

* È stata aggiornata la versione per `getTimeParting`
* È stata aggiornata la versione per `numberSuite`
* È stata aggiornata la versione per `getNewRepeat`
* È stata aggiornata la documentazione di tutti i plug-in.

## 30 ottobre 2019

### Estensione Common Analytics Plugins 2.0.3

#### Correzioni di bug

* È stato risolto un problema nei collegamenti alla documentazione.

## 11 ottobre 2019

### Estensione Common Analytics Plugins 2.0.2

#### Funzioni

* Sono stati aggiunti all’estensione 15 plug-in.
* È stata creata una nuova azione di inizializzazione per semplificare l’implementazione.

## 11 luglio 2019

### Estensione Common Analytics Plugins 1.0.4

#### Funzioni

* È stata rilasciata l’estensione con sette plug-in.
* Sono state introdotte singole azioni per inizializzare ciascun plug-in.
