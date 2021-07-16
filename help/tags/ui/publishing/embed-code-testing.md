---
title: Test dei codici da incorporare tramite Adobe Experience Platform Debugger
description: Scopri come utilizzare Platform Debugger per testare localmente diversi codici da incorporare per Adobe Experience Platform sul tuo sito Web.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 85%

---

# Test dei codici da incorporare tramite Adobe Experience Platform Debugger

>[!NOTE]
>
>Con il suo rebranding, Adobe Experience Platform Launch viene riproposto come una suite di tecnologie per la raccolta dati all’interno di Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Man mano che apporti modifiche alle build della libreria di tag in Adobe Experience Platform, devi testarle prima di distribuire la build nell&#39;ambiente di produzione. Se non disponi di un ambiente di preproduzione o di sviluppo dedicato per il sito web, puoi utilizzare Adobe Experience Platform Debugger per testare in locale i diversi codici da incorporare all’interno del sito.

## Prerequisiti

Questa esercitazione richiede una buona comprensione dell’utilizzo di ambienti e codici di incorporamento nell’interfaccia utente di raccolta dati. Per ulteriori informazioni, consulta la [panoramica degli ambienti](./environments.md).

Questo tutorial richiede inoltre l’installazione dell’estensione Platform Debugger per il browser. Platform Debugger è disponibile solo per i browser Chrome e Firefox. Prima di iniziare il tutorial, installa l’estensione da uno dei seguenti collegamenti:

* [Platform Debugger per Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)
* [Platform Debugger per Firefox](https://addons.mozilla.org/it/firefox/addon/adobe-experience-platform-dbg/)

## Aprire Platform Debugger sul sito web

Utilizzando il browser desiderato, accedi al sito web e apri l’estensione Platform Debugger. Il sito a cui è attualmente connesso Platform Debugger viene visualizzato nella parte inferiore della finestra. Se i tag sono attualmente in esecuzione sul sito, verranno elencati nella scheda [!UICONTROL Riepilogo] .

![](./images/embed-code-testing/summary.png)

>[!NOTE]
>
>Se inizialmente Platform Debugger non si connette, prima di riprovare potrebbe essere necessario ricaricare la scheda del browser in cui è visualizzato il sito web.

## Sostituire i codici da incorporare

Una volta che Platform Debugger è connesso al sito, seleziona **[!UICONTROL Launch]** nell’area di navigazione a sinistra. Qui puoi vedere le informazioni sulla versione della libreria attualmente in esecuzione sul tuo sito, incluso l’ambiente e le estensioni associate. Da qui, seleziona **[!UICONTROL Configurazione]** per visualizzare i controlli per la gestione dei codici da incorporare.

![](./images/embed-code-testing/launch-tab.png)

In [!UICONTROL Codici da incorporare nella pagina] viene visualizzato il codice da incorporare attualmente in uso nel sito. Seleziona **[!UICONTROL Azioni]** a destra del codice da incorporare, quindi seleziona **[!UICONTROL Sostituisci]**.

![](./images/embed-code-testing/replace.png)

Viene visualizzato un messaggio che richiede di fornire un codice da incorporare per sostituire quello corrente. Attenzione: la sostituzione del codice da incorporare con Platform Debugger non modifica il codice da incorporare implementato sul sito. Viene sostituito solo il codice da incorporare eseguito in locale, in modo da poter testare ed eseguire il debug per l’implementazione.

Incolla il codice da incorporare che desideri verificare nella casella di testo fornita, quindi seleziona **[!UICONTROL Applica]**.

![](./images/embed-code-testing/paste-code.png)

Viene visualizzata di nuovo la scheda **[!UICONTROL Configurazione]** dove si vede che il codice da incorporare live è stato sostituito con quello fornito. Ora puoi utilizzare il browser web per verificare se il codice da incorporare che stai testando funziona come previsto.

![](./images/embed-code-testing/code-replaced.png)

## Passaggi successivi

Questo tutorial illustra come cambiare in locale, a scopo di test, i codici da incorporare utilizzando Platform Debugger. Per ulteriori informazioni sulle varie funzionalità, consulta la [documentazione di Platform Debugger](https://experienceleague.adobe.com/docs/debugger/using-v2/experience-cloud-debugger.html?lang=it).
