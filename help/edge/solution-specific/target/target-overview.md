---
title: 'Adobe Target e l''SDK Web per Adobe Experience Platform. '
seo-title: SDK Web per Adobe Experience Platform e utilizzo di Adobe Target
description: Scopri come eseguire il rendering del contenuto personalizzato con l’SDK Web della piattaforma Experience tramite Adobe Target
seo-description: Scopri come eseguire il rendering del contenuto personalizzato con l’SDK Web della piattaforma Experience tramite Adobe Target
translation-type: tm+mt
source-git-commit: db4bfec04a1116ce2b6a0be7ca0e8cb2f9639ad6

---


# Panoramica di Target

L’SDK Web per Adobe Experience Platform è integrato con Adobe Target tramite tale funzione [di](../../fundamentals/rendering-personalization-content.md) personalizzazione e consente di distribuire semplicemente contenuti e decisioni personalizzati.

## Abilitazione di Adobe Target

Per abilitare Target dovrete effettuare le seguenti operazioni:

- Attivate la destinazione nella configurazione [](../../fundamentals/edge-configuration.md) edge con il codice client appropriato.
- Aggiungete l&#39; `renderDecisions` opzione agli eventi.

Facoltativamente potete anche effettuare le seguenti operazioni:

- Aggiungete `scopes` agli eventi per recuperare attività specifiche (utile per le attività create con il compositore basato su modulo).
- Aggiungete lo snippet di [anteprima](../../fundamentals/managing-flicker.md) per nascondere solo alcune parti della pagina.

## Utilizzo del VEC

Con l’SDK potete utilizzare normalmente il VEC con un’eccezione. Sarà necessario installare e attivare l’estensione [helper VEC di](https://docs.adobe.com/content/help/en/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) destinazione.

## Utilizzo di Composer basato su modulo

È possibile utilizzare anche il compositore basato su modulo per restituire il contenuto. Gli ambiti verranno visualizzati come posizioni (mBox) nell&#39;interfaccia utente di Target. Inoltre, se decidete di utilizzare gli ambiti, sarà necessario verificare che lo sviluppatore stia cercando le risposte.

## Tipi di pubblico in XDM

All&#39;interno di Target i dati XDM vengono visualizzati in Audience Builder come parametro personalizzato. L&#39;XDM viene serializzato utilizzando la notazione del punto (ad es. `web.webPageDetails.name`)

## Terminologia

__Decisioni__ - In Target queste correlazioni sono correlate all&#39;esperienza selezionata da un&#39;attività.

__Ambito__ - Ambito di applicazione della decisione. In Target questo è l&#39;mBox. L&#39;mBox globale è l&#39; `__view__` ambito.

__Schema__ - Lo schema di una decisione è il tipo di offerta in Target.

__XDM__ - L&#39;XDM viene serializzato nella notazione del punto e quindi immesso in Target come parametri mBox.