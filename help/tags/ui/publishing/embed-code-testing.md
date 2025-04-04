---
title: Test dei codici da incorporare tramite Adobe Experience Platform Debugger
description: Scopri come utilizzare Experience Platform Debugger per testare localmente diversi codici da incorporare per Adobe Experience Platform sul tuo sito web.
exl-id: ae6183b9-0d25-49d0-b0e9-f8b5ba58ab33
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 58%

---

# Test dei codici da incorporare tramite Adobe Experience Platform Debugger

>[!NOTE]
>
>Con il suo rebranding, Adobe Experience Platform Launch è ora una suite di tecnologie per la raccolta dati all’interno di Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Se desideri apportare modifiche alle versioni della libreria di tag in Adobe Experience Platform, devi testarle prima di implementarle nell’ambiente di produzione. Se non disponi di un ambiente di preproduzione o di sviluppo dedicato per il sito web, puoi utilizzare Adobe Experience Platform Debugger per testare in locale i diversi codici da incorporare all’interno del sito.

## Prerequisiti

Questo tutorial richiede una buona conoscenza dell’utilizzo di ambienti e codici di incorporamento per i tag. Per ulteriori informazioni, consulta la [panoramica degli ambienti](./environments.md).

Questo tutorial richiede anche l’installazione dell’estensione Experience Platform Debugger per il browser. Experience Platform Debugger è disponibile per il browser Chrome. Utilizza il seguente collegamento per installare l&#39;estensione prima di avviare l&#39;esercitazione:

* [Experience Platform Debugger per Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

## Apri Experience Platform Debugger sul sito web

Utilizzando il browser desiderato, accedi al sito web e apri l’estensione Experience Platform Debugger. Il sito a cui è attualmente connesso Experience Platform Debugger viene visualizzato nella parte inferiore della finestra. Se sul sito vi sono attualmente dei tag in esecuzione, questi verranno elencati nella scheda [!UICONTROL Riepilogo].

![](./images/embed-code-testing/summary.png)

>[!NOTE]
>
>Se inizialmente Experience Platform Debugger non si connette, prima di riprovare potrebbe essere necessario ricaricare la scheda del browser in cui è visualizzato il sito web.

## Sostituire i codici da incorporare

Una volta che Experience Platform Debugger si è connesso al sito, seleziona **[!UICONTROL Launch]** nell&#39;area di navigazione a sinistra. Qui puoi vedere le informazioni sulla versione della libreria attualmente in esecuzione sul tuo sito, incluso l’ambiente e le estensioni associate. Da qui, seleziona **[!UICONTROL Configurazione]** per visualizzare i controlli per la gestione dei codici da incorporare.

![](./images/embed-code-testing/launch-tab.png)

In [!UICONTROL Codici da incorporare nella pagina] viene visualizzato il codice da incorporare attualmente in uso nel sito. Seleziona **[!UICONTROL Azioni]** a destra del codice da incorporare, quindi seleziona **[!UICONTROL Sostituisci]**.

![](./images/embed-code-testing/replace.png)

Viene visualizzato un messaggio che richiede di fornire un codice da incorporare per sostituire quello corrente. Tieni presente che la sostituzione del codice di incorporamento con Experience Platform Debugger non modifica il codice di incorporamento distribuito sul sito. Viene sostituito solo il codice da incorporare eseguito in locale, in modo da poter testare ed eseguire il debug per l’implementazione.

Incolla il codice da incorporare che desideri verificare nella casella di testo fornita, quindi seleziona **[!UICONTROL Applica]**.

![](./images/embed-code-testing/paste-code.png)

Viene visualizzata di nuovo la scheda **[!UICONTROL Configurazione]** dove si vede che il codice da incorporare live è stato sostituito con quello fornito. Ora puoi utilizzare il browser web per verificare se il codice da incorporare che stai testando funziona come previsto.

![](./images/embed-code-testing/code-replaced.png)

## Passaggi successivi

Questo tutorial illustra come cambiare in locale i codici da incorporare a scopo di test utilizzando Experience Platform Debugger. Per ulteriori informazioni sulle varie funzionalità, consulta la [documentazione di Experience Platform Debugger](../../../debugger/home.md).
