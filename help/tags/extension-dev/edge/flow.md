---
title: Flusso per estensioni Edge
description: Scopri in che modo i componenti di un’estensione edge in Adobe Experience Platform interagiscono tra loro in fase di runtime.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 67%

---

# Flusso per estensioni Edge

>[!NOTE]
>
>Con il suo rebranding, Adobe Experience Platform Launch viene riproposto come una suite di tecnologie per la raccolta dati all’interno di Experience Platform. Di conseguenza, sono state introdotte diverse modifiche terminologiche nella documentazione del prodotto. Consulta questo [documento](../../term-updates.md) come riferimento consolidato delle modifiche terminologiche.

Nelle estensioni edge, ogni condizione, azione e tipo di elemento dati dispone di una vista mediante la quale gli utenti possono modificare le impostazioni e di un modulo libreria che agisce in base alle impostazioni definite dall&#39;utente.

Come mostra il diagramma di alto livello riportato di seguito, la vista del tipo di evento dell&#39;estensione verrà visualizzata all&#39;interno di un iframe nell&#39;applicazione integrata con Adobe Experience Platform. La visualizzazione viene quindi utilizzata per modificare le impostazioni che vengono quindi salvate in Platform. Quando la libreria di runtime di tag viene generata, sia il modulo della libreria dei tipi di azione dell’estensione che le impostazioni definite dall’utente verranno inclusi nella libreria di runtime che viene distribuita al nodo edge. Le impostazioni definite dall’utente da Platform vengono inserite nel modulo libreria in fase di esecuzione.

![diagramma del flusso per le estensioni](../images/flow/edge/event-processing-flow.png)

Il seguente diagramma illustra il collegamento tra eventi, condizioni e azioni all’interno del flusso di elaborazione delle regole.

![diagramma del flusso di elaborazione delle regole](../images/flow/edge/rule-processing-flow.png)

Il flusso di elaborazione delle regole comprende le seguenti fasi:

1. All’avvio, i metodi `settings` e `trigger` vengono trasmessi al modulo libreria di eventi.
1. Quando il modulo libreria degli eventi determina che si è verificato un determinato evento, viene richiamato `trigger`.
1. Platform trasmette `settings` nei moduli libreria delle condizioni della regola in cui vengono valutate le condizioni.
1. Ogni tipo di condizione restituisce se una condizione è stata valutata &quot;true&quot;.
1. Se tutte le condizioni risultano “true”, le azioni della regola vengono eseguite.
