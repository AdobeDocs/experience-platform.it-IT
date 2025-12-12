---
title: Impostazioni di configurazione Personalization
description: Configura le impostazioni di personalizzazione nell’estensione tag Web SDK.
source-git-commit: 9a617b6e97aec22a6726266f2628bd2c2a05da19
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 1%

---

# Impostazioni di configurazione Personalization

Questa sezione di configurazione consente di determinare come nascondere determinate parti della pagina durante il caricamento del contenuto personalizzato. Una volta configurate correttamente, queste impostazioni garantiscono che i visitatori visualizzino il contenuto personalizzato corretto.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Extensions]**, quindi seleziona **[!UICONTROL Configure]** nella scheda [!UICONTROL Adobe Experience Platform Web SDK].
1. Scorri verso il basso fino alla sezione **[!UICONTROL Personalization]**.

![Immagine che mostra le impostazioni di personalizzazione dell&#39;estensione tag Web SDK nell&#39;interfaccia utente Tag](../assets/web-sdk-ext-personalization.png)

Sono disponibili le seguenti opzioni:

## [!UICONTROL Migrate Target from at.js to the Web SDK]**

Utilizzare questa opzione per consentire al Web SDK di leggere e scrivere i cookie legacy `mbox` e `mboxEdgeCluster` utilizzati dalle librerie `at.js` 1.x o 2.x. Questa impostazione consente di mantenere intatti i profili dei visitatori durante lo spostamento tra pagine tramite Web SDK o `at.js` sullo stesso sito Web. Se `at.js` non è stato implementato in nessun punto del sito, non è necessario abilitare questa casella di controllo. La libreria JavaScript equivalente a questa casella di controllo è [`targetMigrationEnabled`](/help/collection/js/commands/configure/targetmigrationenabled.md).

Quando si abilita questa opzione, assicurarsi di abilitare anche [`overrideMboxEdgeServer`](https://experienceleague.adobe.com/en/docs/target-dev/developer/client-side/at-js-implementation/functions-overview/targetglobalsettings#overridemboxedgeserver) in `targetGlobalSettings()`.

## [!UICONTROL Prehiding style] {#prehiding-style}

L’editor di stili che nasconde anticipatamente ti consente di definire regole CSS personalizzate per nascondere sezioni specifiche di una pagina. Quando la pagina viene caricata, il Web SDK utilizza questo stile per nascondere le sezioni che devono essere personalizzate, recupera la personalizzazione e quindi rimuove le sezioni della pagina personalizzata. Questo flusso di lavoro consente ai visitatori di visualizzare contenuti personalizzati senza visualizzare il caricamento o lo sfarfallio del processo di recupero della personalizzazione. L&#39;equivalente della libreria JavaScript a questo editor di codice è [`prehidingStyle`](/help/collection/js/commands/configure/prehidingstyle.md).

## [!UICONTROL Prehiding snippet] {#prehiding-snippet}

Questa sezione non è un’impostazione di configurazione diretta, ma una posizione comoda in cui puoi ottenere il codice di implementazione. Implementare questo frammento pre-hiding all&#39;interno del tag `<head>` sul sito per nascondere il contenuto desiderato durante il caricamento della libreria Web SDK.

>[!IMPORTANT]
>
>Quando si utilizza il frammento pre-hiding, Adobe consiglia di utilizzare la stessa regola CSS tra il frammento pre-hiding e lo stile pre-hiding.

## [!UICONTROL Enable personalization storage]

Casella di controllo che consente al Web SDK di memorizzare gli eventi di personalizzazione. nell’archivio locale del browser. È utile quando desideri tenere traccia delle esperienze che il visitatore ha visto nei diversi caricamenti di pagina.

## [!UICONTROL Auto click collection for Adobe Journey Optimizer]

Menu a discesa che determina quando Web SDK raccoglie automaticamente i clic sul contenuto restituito da Adobe Journey Optimizer.

* **[!UICONTROL Always]**: raccoglie tutte le interazioni con le proposte.
* **[!UICONTROL Decorated elements only]**: raccogli solo le interazioni sugli elementi con `data-aep-click-label` o `data-aep-click-token` attributi HTML.
* **[!UICONTROL Never]**: non raccogliere le interazioni con le proposte.

L&#39;equivalente della libreria JavaScript al menu a discesa è [`autoCollectPropositionInteractions.AJO`](/help/collection/js/commands/configure/autocollectpropositioninteractions.md). Il valore predefinito è [!UICONTROL Always].

## [!UICONTROL Auto click collection for Adobe Target]

Menu a discesa che determina quando Web SDK raccoglie automaticamente i clic sul contenuto restituito da Adobe Target.

* **[!UICONTROL Always]**: raccoglie tutte le interazioni con le proposte.
* **[!UICONTROL Decorated elements only]**: raccogli solo le interazioni sugli elementi con `data-aep-click-label` o `data-aep-click-token` attributi HTML.
* **[!UICONTROL Never]**: non raccogliere le interazioni con le proposte.

L&#39;equivalente della libreria JavaScript al menu a discesa è [`autoCollectPropositionInteractions.TGT`](/help/collection/js/commands/configure/autocollectpropositioninteractions.md). Il valore predefinito è [!UICONTROL Never].
