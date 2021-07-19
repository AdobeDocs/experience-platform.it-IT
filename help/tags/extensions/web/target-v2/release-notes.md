---
title: Note sulla versione per l’estensione Adobe Target v2
description: Note aggiornate sulla versione dell’estensione tag Adobe Target v2 in Adobe Experience Platform.
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 78%

---

# Note sulla versione dell’estensione Adobe Target v2

>[!NOTE]
>
>Con il suo rebranding, Adobe Experience Platform Launch viene riproposto come una suite di tecnologie per la raccolta dati all’interno di Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

## 19 maggio 2021

### Estensione Adobe Target v2 0.14.1

- È stata corretta la regressione introdotta con la versione v0.14 in cui l’azione Load Target attivava chiamate mbox globali.

## 14 maggio 2021

### Estensione Adobe Target v2 0.14

- È stata aggiunta la nuova azione Carica Target con [decisioning sul dispositivo](./overview.md#load-target-with-on-device-decisioning), che carica at.js 2.5 con funzionalità Decisioning sul dispositivo.
- at.js è stato aggiornato a 2.5


## 25 marzo 2021

### Estensione Adobe Target v2 0.13.7

- È stato risolto un problema a causa del quale `targetPageParams` veniva incluso nelle richieste mbox. `targetPageParams` deve essere incluso solo nelle richieste `pageLoad`.
- È stato risolto un problema relativo agli oggetti globali documento e finestra nell’estensione tag sostituendo le dipendenze degli oggetti globali con riferimenti diretti ad essi.
- at.js è stato aggiornato a 2.4.1.

## 25 gennaio 2021

### Estensione Adobe Target v2 0.13.6

- Aggiunge il supporto per l&#39;ID di piattaforma/profilo unificato agli ID cliente API di consegna
- Corregge l&#39;inserimento di tag di stile non validi
- Aggiornamento di at.s a 2.4.0
- È stato risolto un problema a causa del quale parametri non definiti possono causare richieste di consegna non valide.

## 25 novembre 2020

### Estensione Adobe Target v2 0.13.4

- È stato corretto un bug a causa del quale i parametri mbox non venivano visualizzati nell’interfaccia utente.
- Aggiornamenti degli elementi di branding
- Aggiornamento di at.js alla versione 2.3.3

## 24 luglio 2020

### Estensione Adobe Target v2 0.13.3

- È stato corretto un bug a causa del quale i collegamenti in modalità QA non funzionavano per le attività inattive
- È stato corretto un bug a causa del quale l’estensione non riusciva se uno script o un codice aggiungeva una proprietà `default` a `window` o `document`

## 15 giugno 2020

### Estensione 0.13.2 di Adobe Target v2

- È stato risolto un problema che si verificava durante l’utilizzo di CNAME e Edge override, a causa del quale at.js 1.x poteva creare il dominio del server in modo incorretto e la richiesta Target non riusciva.
- È stato risolto un problema a causa del quale, quando si utilizzava l’estensione tag v2 per Target e l’estensione tag Adobe Analytics, Target ritardava la chiamata sendBeacon di Analytics
- È stata migliorata l’impostazione `deviceIdLifetime` rendendola sostituibile tramite `targetGlobalSettings`

## 25 marzo 2020

### Estensione 0.13.0 di Adobe Target v2

- At.js è stato aggiornato a v2.3.
- È stato aggiunto il supporto per Target Global Mbox nell’API adobe.target.getOffer.
- È stato risolto un problema che impediva l’elaborazione corretta dei parametri e dei parametri di caricamento delle pagine.

## 10 ottobre 2019

### Estensione 0.12.0 di Adobe Target v2

- Aggiornato at.js a v2.2.
- Migliorate le prestazioni per le integrazioni tra la libreria Experience Cloud ID (ECID) v4.4 e at.js 2.2.
- In precedenza, la libreria ECID effettuava due chiamate di blocco prima che at.js potesse riportare le esperienze. Ora effettua una sola chiamata, migliorando notevolmente le prestazioni.

>[!NOTE]
>Aggiorna l’estensione tag ECID alla versione 4.4.1 per usufruire di questo miglioramento delle prestazioni.

## 31 luglio 2019

### Estensione 0.11.1 di Adobe Target v2

- Versione aggiornata dell&#39;estensione da utilizzare at.js 2.1.1.
- È stata aggiunta una correzione per la gestione dei parametri.

## 3 giugno 2019

### Estensione 0.11.0 di Adobe Target v2

- Nuova estensione tag per supportare at.js 2.1
