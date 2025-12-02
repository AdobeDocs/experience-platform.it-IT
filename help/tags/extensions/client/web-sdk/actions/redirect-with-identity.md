---
title: Reindirizza con identità
description: Consente di condividere un identificatore visitatore tra i domini dell’organizzazione.
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 1%

---

# Reindirizza con identità

Il tipo di azione **[!UICONTROL Redirect with identity]** ti consente di condividere un identificatore visitatore dalla pagina corrente a un altro dominio di proprietà della tua organizzazione. È progettato per essere utilizzato con un evento di clic e una condizione di confronto dei valori. Funzionalmente simile al comando [`appendIdentityToUrl`](/help/collection/js/commands/appendidentitytourl.md) nella libreria JavaScript.

1. Accedi a [experience.adobe.com](https://experience.adobe.com) utilizzando le credenziali Adobe ID.
1. Passa a **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Seleziona la proprietà tag desiderata.
1. Passa a **[!UICONTROL Rules]**, quindi seleziona la regola desiderata.
1. In [!UICONTROL Actions], selezionare un&#39;azione esistente o crearne una.
1. Imposta il campo a discesa [!UICONTROL Extension] su **[!UICONTROL Adobe Experience Platform Web SDK]**, quindi imposta [!UICONTROL Action type] su **[!UICONTROL Redirect with identity]**.

## Casi d’uso

* **Identifica un individuo tra più domini**: se un visitatore fa clic da un dominio all&#39;altro di proprietà della tua organizzazione, puoi utilizzare questa azione in modo che venga ancora considerato lo stesso individuo. Questo metodo di identificazione è particolarmente utile se disponi di rapporti che combinano dati provenienti da più domini, impedendo l’inflazione dei visitatori.
* **Identifica un utente da un&#39;app mobile a un&#39;app Web**: se un visitatore si trova all&#39;interno della tua app mobile e fa clic su un collegamento all&#39;app Web, puoi utilizzare questa azione in modo che il SDK Web riconosca che si tratta della stessa persona. Questo flusso di lavoro offre un’esperienza coerente per la generazione di rapporti e la personalizzazione.

## Campi disponibili

* **[!UICONTROL Instance]**: l&#39;istanza SDK a cui si applica l&#39;azione. Questo menu a discesa è disattivato se l’implementazione utilizza una singola istanza di SDK.
* **[!UICONTROL Datastream configuration overrides]**: questo comando supporta le sostituzioni della configurazione dello stream di dati, consentendoti di controllare quali app e servizi ricevono i dati. Quando imposti una sostituzione della configurazione dello stream di dati sia in un singolo comando che all’interno delle impostazioni di configurazione dell’estensione tag, il singolo comando ha la precedenza. Per ulteriori informazioni, vedere [Override della configurazione Datastream](../configure/configuration-overrides.md).

## Esempio di regola

Questo comando viene in genere utilizzato con una regola specifica che ascolta i clic e controlla i domini desiderati.

+++Criteri evento regola

Si attiva quando si fa clic su un tag di ancoraggio con una proprietà `href`.

* **[!UICONTROL Extension]**: Core
* **[!UICONTROL Event type]**: fare clic su
* **[!UICONTROL When the user clicks on]**: elementi specifici
* **[!UICONTROL Elements matching the CSS selector]**: `a[href]`

![Evento regola](../assets/id-sharing-event-configuration.png)

+++

+++Condizione regola

Si attiva solo sui domini desiderati.

* **[!UICONTROL Logic type]**: regolare
* **[!UICONTROL Extension]**: Core
* **[!UICONTROL Condition Type]**: Confronto valori
* **[!UICONTROL Left Operand]**: `%this.hostname%`
* **[!UICONTROL Operator]**: corrisponde a Regex
* **[!UICONTROL Right Operand]**: espressione regolare che corrisponde ai domini desiderati. Ad esempio, `adobe.com$|behance.com$`

![Condizione regola](../assets/id-sharing-condition-configuration.png)

+++

+++Azione regola

Aggiungi l’identità all’URL.

* **[!UICONTROL Extension]**: Adobe Experience Platform Web SDK
* **[!UICONTROL Action Type]**: reindirizzamento con identità

![Azione regola](../assets/id-sharing-action-configuration.png)

+++
