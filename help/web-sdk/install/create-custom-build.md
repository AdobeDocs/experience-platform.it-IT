---
title: Creare una build Web SDK personalizzata utilizzando il pacchetto NPM
description: Creare una build Web SDK personalizzata contenente solo i moduli necessari.
source-git-commit: 0f77023b07102ac2bc812034afacb1522ef209e5
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 6%

---


# Creazione di una build Web SDK personalizzata

La libreria Experience Platform Web SDK include più moduli per varie funzioni come personalizzazione, identità, tracciamento dei collegamenti e altro ancora. A seconda dei casi di utilizzo, potresti aver bisogno solo di funzionalità specifiche invece che dell’intera libreria. La creazione di una build Web SDK personalizzata consente di selezionare solo i moduli necessari, riducendo le dimensioni della libreria e migliorando le prestazioni.

## Casi d’uso {#use-case}

La creazione di una build Web SDK personalizzata consente di ridurre le dimensioni della libreria e di migliorare le prestazioni. Di seguito sono riportati alcuni esempi:

### Rimozione di Media Analytics {#media-analytics-removal}

Se il sito Web non dispone di contenuti multimediali, è possibile escludere i moduli [!DNL Media Analytics] e [!DNL Streaming Media] dalla build. Questo può ridurre le dimensioni della build del Web SDK fino al 50% e migliorare la velocità di caricamento.

### Rimozione Personalization {#personalization}

Se devi solo raccogliere le metriche utente e non prevedi di utilizzare Adobe Target o Journey Optimizer per la personalizzazione, puoi escludere il modulo [!DNL Personalization]. Questo riduce le dimensioni della libreria, consentendo al tempo stesso di raccogliere le metriche necessarie.

## Prerequisiti {#prerequisites}

Per creare una build Web SDK personalizzata, è necessario il pacchetto NPM di Web SDK. Verifica che [Node.js](https://nodejs.org/en/download/package-manager/all) sia installato nel computer. Per ulteriori informazioni, vedere la documentazione su come [installare Web SDK utilizzando il pacchetto NPM](npm.md).

## Componenti e dipendenze {#components-dependencies}

Prima di creare una build di Web SDK personalizzata, definire i componenti e i comandi di Web SDK che si intende utilizzare. Alcuni comandi dipendono da moduli specifici inclusi nella build.

Nella tabella seguente viene illustrata la relazione tra i moduli di Web SDK e i comandi inclusi:

| Dipendenza modulo | Parametri di configurazione | Comandi | Categoria dimensioni |
|---------|----------|---------|---------|
| Agente di raccolta attività | [`clickCollectionEnabled`](../commands/configure/clickcollectionenabled.md) | N/D | Canale |
| Tipi di pubblico | N/D | N/D | Piccolo |
| Contesto | [`context`](../commands/configure/context.md) | N/D | Piccolo |
| Motore di regole | `personalizationStorageEnabled` | | <ul><li>`evaluateRulesets`</li><li>[`subscribeRulesetItems`](../commands/subscriberulesetitems.md)</li></ul> | Canale |
| Unione eventi | N/D | `createEventMergeId` | Piccolo |
| Bridge di Media Analytics | N/D | [`getMediaAnalyticsTracker`](../commands/getmediaanalyticstracker.md) | Grande |
| Personalizzazione | <ul><li>[`prehidingStyle`](../commands/configure/prehidingstyle.md)</li><li>[`targetMigrationEnabled`](../commands/configure/targetmigrationenabled.md)</li><li>[`autoCollectPropositionInteractions`](../commands/configure/autocollectpropositioninteractions.md)</li></ul> | N/D | Grande |
| Consenso | [`defaultConsent`](../commands/configure/defaultconsent.md) | [`setConsent`](../commands/setconsent.md) | Piccolo |
| Contenuti multimediali in streaming | [`streamingMedia`](../commands/configure/streamingmedia.md) | <ul><li>[`createMediaSession`](../commands/createmediasession.md)</li><li>[`sendMediaEvent`](../commands/sendmediaevent.md)</li></ul> | Grande |

## Creare una build Web SDK personalizzata utilizzando il pacchetto NPM {#create-custom-build}

1. Apri il terminale ed esegui `npx @adobe/alloy`. Viene chiesto di selezionare i componenti di Web SDK che si desidera includere nella build personalizzata.

   ![Immagine di un terminale che mostra la selezione del modulo di compilazione personalizzato.](../assets/custom-build/npx.png)

   Utilizzare i tasti freccia per spostarsi verso l&#39;alto o verso il basso nell&#39;elenco dei moduli.

   * Premi **Spazio** per abilitare o disabilitare il modulo selezionato.
   * Premere `A` per abilitare o disabilitare tutti i moduli.
   * Premi `I` per invertire la selezione.
   * Premi `Enter` per confermare la selezione e passare al passaggio successivo.

1. Dopo aver selezionato i moduli da includere nella build personalizzata, puoi scegliere se salvare una versione minimizzata o non minimizzata della build della libreria di Web SDK personalizzata. Selezionare l&#39;opzione desiderata e premere `Enter`.

   ![Immagine di un terminale che mostra la selezione di minimizzazione della compilazione personalizzata.](../assets/custom-build/minify.png)

1. Successivamente, viene chiesto dove si desidera salvare la build nel computer locale. Premere `Enter` per confermare la posizione preselezionata o immettere una nuova posizione.

   ![Immagine di un terminale che mostra l&#39;opzione di salvataggio della compilazione personalizzata.](../assets/custom-build/save.png)

1. Una volta confermata la posizione, la build personalizzata viene generata e salvata.

   ![Immagine di un terminale che mostra il percorso salvato della build personalizzata.](../assets/custom-build/saved.png)

