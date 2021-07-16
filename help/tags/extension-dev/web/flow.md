---
title: Flusso per estensioni web
description: Scopri come i componenti di estensione web interagiscono tra loro in fase di runtime in Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 69%

---

# Flusso per estensioni web

>[!NOTE]
>
>Con il suo rebranding, Adobe Experience Platform Launch viene riproposto come una suite di tecnologie per la raccolta dati all’interno di Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta il seguente[documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Ogni evento, condizione, azione e tipo di elemento dati nelle estensioni Web dispone di una vista mediante la quale gli utenti possono modificare le impostazioni e di un modulo libreria che agisce in base alle impostazioni definite dall&#39;utente.

Come mostra il diagramma di alto livello riportato di seguito, la vista del tipo di evento dell’estensione verrà visualizzata all’interno di un iframe nell’applicazione integrata con Adobe Experience Platform. L’utente utilizza quindi la visualizzazione per modificare le impostazioni che vengono quindi salvate in Platform. Quando la libreria di runtime di tag viene generata, nella libreria di runtime verranno inclusi sia il modulo di libreria dei tipi di evento dell’estensione che le impostazioni definite dall’utente. In fase di runtime, Platform inserisce le impostazioni definite dall’utente nel modulo libreria.

![diagramma del flusso per le estensioni](../images/flow/web/extension-flow.png)

Il seguente diagramma illustra il collegamento tra eventi, condizioni e azioni all’interno del flusso di elaborazione delle regole.

![diagramma del flusso di elaborazione delle regole](../images/flow/web/rule-processing-flow.png)

Il flusso di elaborazione delle regole comprende le seguenti fasi:

1. All’avvio, i metodi `settings` e `trigger` vengono trasmessi al modulo libreria di eventi.
1. Quando il modulo libreria degli eventi determina che si è verificato un determinato evento, viene richiamato `trigger`.
1. I tag passano `settings` nei moduli della libreria di condizioni della regola in cui vengono valutate le condizioni.
1. Ogni modulo libreria di condizioni restituisce se una condizione è stata valutata “true”.
1. Se tutte le condizioni risultano “true”, le azioni della regola vengono eseguite.
