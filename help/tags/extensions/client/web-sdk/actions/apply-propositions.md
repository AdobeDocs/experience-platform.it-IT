---
title: Applicare le proposte
description: Eseguire il rendering delle proposte nelle applicazioni a pagina singola senza incrementare le metriche.
source-git-commit: 217282135bcd750740f4d3f8c6e17a0b8f9578bd
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# Applicare le proposte

Il tipo di azione **[!UICONTROL Apply propositions]** consente di eseguire il rendering delle proposte nelle applicazioni a pagina singola senza incrementare le metriche. Questo tipo di azione è utile quando si lavora con applicazioni a pagina singola in cui viene eseguito nuovamente il rendering di parti della pagina, sovrascrivendo potenzialmente eventuali personalizzazioni già applicate alla pagina.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Rules]**, quindi seleziona la regola desiderata.
1. In [!UICONTROL Actions], selezionare un&#39;azione esistente o crearne una.
1. Imposta il campo a discesa [!UICONTROL Extension] su **[!UICONTROL Adobe Experience Platform Web SDK]**, quindi imposta [!UICONTROL Action type] su **[!UICONTROL Apply propositions]**.

![L&#39;interfaccia utente dei tag di Experience Platform mostra il tipo di azione Applica proposte.](../assets/apply-propositions.png)

## Casi d’uso

Puoi utilizzare questo tipo di azione per vari casi d’uso, ad esempio:

1. **Rendering offerte mbox HTML**. Le proposte esplicitamente richieste tramite un ambito o una superficie da un&#39;azione **[!UICONTROL Send event]** non vengono sottoposte a rendering automaticamente. È possibile utilizzare il tipo di azione **[!UICONTROL Apply propositions]** per indicare a Web SDK dove eseguirne il rendering specificando i metadati della proposta.
2. **Eseguire il rendering delle offerte per una visualizzazione in un&#39;applicazione a pagina singola**. Durante il rendering di un evento di modifica della visualizzazione, se i dati di analisi non sono ancora pronti, puoi utilizzare l&#39;azione **[!UICONTROL Apply propositions]** per eseguire il rendering delle proposte di visualizzazione nella parte superiore della pagina. Per ulteriori dettagli, vedi [eventi di inizio e fine pagina (seconda visualizzazione pagina - opzione 2)](/help/collection/use-cases/personalization/top-bottom-page-events.md). Per utilizzare questa proprietà, immettere un **[!UICONTROL View name]** nel modulo.
3. **Riesegui rendering delle proposte**. Quando il sito utilizza un framework come React per eseguire nuovamente il rendering del contenuto, potrebbe essere necessario riapplicare la personalizzazione. In questi casi è possibile utilizzare il tipo di azione **[!UICONTROL Apply propositions]**.

Questo tipo di azione non invia un evento di visualizzazione per le proposte sottoposte a rendering. Tiene traccia delle proposte sottoposte a rendering in modo che possano essere incluse nelle chiamate **[!UICONTROL Send event]** successive.

## Campi disponibili

Questo tipo di azione supporta i campi seguenti:

* **[!UICONTROL Instance]**: l&#39;istanza SDK a cui si applica l&#39;azione. Questo menu a discesa è disattivato se l’implementazione utilizza una singola istanza di SDK.
* **[!UICONTROL Propositions]**: array di oggetti della proposta di cui si desidera eseguire nuovamente il rendering.
* **[!UICONTROL View name]**: nome della visualizzazione da riprodurre.
* **[!UICONTROL Proposition metadata]**: oggetto che determina la modalità di applicazione delle offerte HTML. Puoi fornire queste informazioni tramite il modulo o un elemento dati. Contiene le seguenti proprietà:
   * **[!UICONTROL Scope]**
   * **[!UICONTROL Selector]**
   * **[!UICONTROL Action type]**
